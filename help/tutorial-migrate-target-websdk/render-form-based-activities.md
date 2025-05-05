---
title: Migración de Target de at.js 2.x a SDK web
description: Obtenga información sobre cómo migrar una implementación de Adobe Target de at.js 2.x al SDK web de Adobe Experience Platform. Los temas incluyen información general de la biblioteca, diferencias de implementación y otras llamadas importantes.
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# Procesar actividades de Target que utilicen el Compositor basado en formularios

Algunas implementaciones de Target pueden utilizar mboxes regionales (ahora conocidos como &quot;ámbitos&quot;) para entregar contenido desde actividades que utilizan el Compositor de experiencias basadas en formularios. Si su implementación de at.js en Target usa mboxes, debe hacer lo siguiente:

* Actualice cualquier referencia de su implementación de at.js que use `getOffer()` o `getOffers()` a los métodos del SDK web de Platform equivalentes.
* Agregue código para almacenar en déclencheur un evento `propositionDisplay` de modo que se cuente una impresión.

## Solicitud y aplicación de contenido bajo demanda

El SDK web de Platform no puede procesar automáticamente las actividades creadas con el compositor basado en formularios de Target y enviadas a mboxes regionales. Al igual que at.js, las ofertas enviadas a ubicaciones de Target específicas deben procesarse bajo demanda.


+++Ejemplo de at.js con `getOffer()` y `applyOffer()`:

1. Ejecute `getOffer()` para solicitar una oferta para una ubicación
1. Ejecute `applyOffer()` para procesar la oferta en un selector especificado
1. Una impresión de actividad se incrementa automáticamente en el momento de la solicitud `getOffer()`

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

+++

+++Equivalente del SDK web de Platform con el comando `applyPropositions`:

1. Ejecute el comando `sendEvent` para solicitar ofertas (propuestas) para una o varias ubicaciones (ámbitos)
1. Ejecute el comando `applyPropositions` con el objeto de metadatos, que proporciona instrucciones sobre cómo aplicar contenido a la página para cada ámbito
1. Ejecute el comando `sendEvent` con eventType de `decisioning.propositionDisplay` para realizar el seguimiento de una impresión

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": renderedPropositions
          }
        }
      }
    });
  });
});
```

+++

El SDK web de Platform ofrece un mayor control para aplicar actividades basadas en formularios a la página mediante el comando `applyPropositions` con un `actionType` especificado:

| `actionType` | Descripción | `applyOffer()` de at.js | SDK web de Platform `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | Borre el contenido del contenedor y, a continuación, añada la oferta al contenedor | Sí (siempre se usa) | Sí |
| `replaceHtml` | Retirar el contenedor y sustituirlo por la oferta | No | Sí |
| `appendHtml` | Adjunta la oferta después del selector especificado | No | Sí |

Consulte la [documentación dedicada](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=es) acerca de la representación de contenido mediante el SDK web de Platform para obtener opciones y ejemplos adicionales de representación.

## Ejemplo de implementación

La página de ejemplo siguiente se basa en la implementación descrita en la sección anterior, solo agrega ámbitos adicionales al comando `sendEvent`.

+++Ejemplo del SDK web de Platform con varios ámbitos

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
          "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
              "decisioning": {
                "propositions": renderedPropositions
              }
            }
          }
        });
      });
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

A continuación, aprenda a [pasar parámetros de Target mediante el SDK web de Platform](send-parameters.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=es#M463).
