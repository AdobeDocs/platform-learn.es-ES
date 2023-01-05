---
title: Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo migrar una implementación de Adobe Target de at.js 2.x al SDK web de Adobe Experience Platform. Los temas incluyen descripción general de la biblioteca, diferencias de implementación y otras llamadas importantes.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Procesar actividades de Target que utilizan el compositor basado en formularios

Algunas implementaciones de Target pueden utilizar mboxes regionales (ahora conocidos como &quot;ámbitos&quot;) para ofrecer contenido de actividades que utilizan el Compositor de experiencias basadas en formularios. Si la implementación de at.js Target usa mboxes, debe hacer lo siguiente:

* Actualice cualquier referencia de la implementación de at.js que use `getOffer()` o `getOffers()` a los métodos equivalentes de Platform Web SDK.
* Añadir código al déclencheur de un `propositionDisplay` para que se cuente una impresión.

## Solicitar y aplicar contenido bajo demanda

Las actividades creadas con el compositor basado en formularios de Target y entregadas a mboxes regionales no se pueden procesar automáticamente con el SDK web de Platform. Al igual que at.js, las ofertas entregadas a ubicaciones de Target específicas deben procesarse bajo demanda.

Ejemplo de at.js con `getOffer()` y `applyOffer()`:

1. Ejecutar `getOffer()` para solicitar una oferta para una ubicación
1. Ejecutar `applyOffer()` representar la oferta en un selector especificado
1. Una impresión de actividad se incrementa automáticamente en el momento del `getOffer()` solicitud

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

Equivalente de SDK web de plataforma con `applyPropositions` comando:

1. Ejecutar `sendEvent` para solicitar ofertas (propuestas) para una o más ubicaciones (ámbitos)
1. Ejecutar `applyPropositions` con el objeto metadata que proporciona instrucciones sobre cómo aplicar contenido a la página para cada ámbito
1. Ejecutar `sendEvent` con eventType de `decisioning.propositionDisplay` para rastrear una impresión

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

El SDK web de Platform ofrece bueno control para aplicar actividades basadas en formularios a la página mediante el uso de `applyPropositions` con un `actionType` especificado:

| `actionType` | Descripción | at.js `applyOffer()` | SDK web de Platform `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | Borre el contenido del contenedor y luego agregue la oferta al contenedor | Sí (siempre utilizado) | Sí |
| `replaceHtml` | Eliminar el contenedor y reemplazarlo por la oferta | No | Sí |
| `appendHtml` | Anexa la oferta después del selector especificado | No | Sí |

Consulte la [documentación dedicada](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) acerca de la renderización de contenido mediante el SDK web de Platform para obtener opciones y ejemplos de renderización adicionales.

## Ejemplo de implementación

La página de ejemplo siguiente se basa en la implementación descrita en la sección anterior, solo que agrega ámbitos adicionales al `sendEvent` comando.

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
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).