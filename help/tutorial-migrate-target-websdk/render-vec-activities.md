---
title: Procesar actividades VEC | Migración de Target de at.js 2.x a SDK web
description: Obtenga información sobre cómo recuperar y aplicar actividades del Compositor de experiencias visuales con una implementación SDK web de Adobe Target.
exl-id: bbbbfada-e236-44de-a7bf-5c63ff840db4
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Procesar actividades del Compositor de experiencias visuales (VEC) de Adobe Target

Las actividades de Target se configuran mediante el Compositor de experiencias visuales (VEC) o el Compositor basado en formularios. El SDK web de Platform puede recuperar y aplicar actividades basadas en VEC a la página como at.js. En esta parte de la migración, deberá hacer lo siguiente:

* Instale la extensión de explorador Ayuda de edición visual
* Ejecute una llamada de `sendEvent` con el SDK web de Platform para solicitar actividades.
* Actualice cualquier referencia de su implementación de at.js que use `getOffers()` para ejecutar una solicitud de Target `pageLoad`.

## Extensión de explorador Ayuda de edición visual

La extensión del explorador Ayuda de edición visual de Adobe Experience Cloud para Google Chrome le permite cargar sitios web de forma fiable dentro del Compositor de experiencias visuales (VEC) de Adobe Target para crear y realizar controles de calidad de experiencias web rápidamente.

La extensión de explorador Ayuda de edición visual funciona con sitios web que utilizan at.js o SDK web de Platform.

### Obtener e instalar el Asistente de edición visual

1. Vaya a la extensión de explorador [Ayuda de edición visual de Adobe Experience Cloud en Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Haga clic en Agregar a **Chrome** > **Agregar extensión**.
1. Abra el VEC en Target.
1. Para usar la extensión, haga clic en el icono de la extensión del explorador Ayuda de edición visual ![icono de Extensión de edición visual](assets/VEC-Helper.png){zoomable="yes"} en la barra de herramientas del explorador Chrome mientras está en VEC o en modo control de calidad.

La Ayuda de edición visual se activa automáticamente cuando se abre un sitio web en el VEC de Target para la creación de contenido. La extensión no tiene ninguna configuración condicional. La extensión gestiona todas las configuraciones automáticamente, incluida la configuración de cookies de SameSite.

Consulte la documentación dedicada para obtener más información sobre la [extensión Ayuda de edición visual](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) y [solución de problemas del Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

>[!IMPORTANT]
>
>La nueva extensión [Ayuda de edición visual](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca) reemplaza a la extensión de explorador [Target VEC Helper anterior](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). Si se instala la extensión VEC Helper más antigua, debe eliminarse o deshabilitarse antes de utilizar la extensión Visual Editing Helper.

## Solicitar y aplicar contenido automáticamente

Una vez configurado el SDK web de Platform en la página, puede solicitar contenido a Target. A diferencia de at.js, que se puede configurar para que solicite contenido automáticamente cuando se carga la biblioteca, el SDK web de Platform requiere que ejecute explícitamente un comando.

Si su implementación de at.js tiene la configuración `pageLoadEnabled` establecida en `true`, que permite el procesamiento automático de actividades basadas en VEC, debe ejecutar el siguiente comando `sendEvent` con el SDK web de Platform:

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB Etiquetas]

En las etiquetas, use el tipo de acción [!UICONTROL Enviar evento] con la opción [!UICONTROL Procesar decisiones de personalización visual] seleccionada:

![Enviar un evento con Procesar decisiones de personalización visual seleccionadas en etiquetas](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## Solicitud y aplicación de contenido bajo demanda

Algunas implementaciones de Target requieren un procesamiento personalizado de las ofertas VEC antes de aplicarlas a la página. O bien, solicitan varias ubicaciones en una sola llamada. En una implementación de at.js, esto se puede hacer estableciendo `pageLoadEnabled` en `false` y utilizando la función `getOffers()` para ejecutar una solicitud `pageLoad`.

+++ Ejemplo de at.js con `getOffers()` y `applyOffers()` para procesar manualmente actividades basadas en VEC

```JavaScript
adobe.target.getOffers({
  request: {
    execute: {
      pageLoad: {}
    }
  }
}).
then(response => adobe.target.applyOffers({ response: response }));
```

+++

El SDK web de Platform no tiene un evento `pageLoad` específico. Todas las solicitudes de contenido de Target se controlan con la opción `decisionScopes` con el comando `sendEvent`. El ámbito `__view__` sirve al propósito de la solicitud `pageLoad`.

+++ Un enfoque equivalente del SDK web de Platform `sendEvent`:

1. Ejecutar un comando `sendEvent` que incluye el ámbito de decisión `__view__`
1. Aplicar el contenido devuelto a la página con el comando `applyPropositions`
1. Ejecute un comando `sendEvent` con el tipo de evento `decisioning.propositionDisplay` y los detalles de la propuesta para aumentar una impresión

```Javascript
alloy("sendEvent", {
  // Request the special "__view__" scope for target-global-mbox / pageLoad
  decisionScopes: ["__view__"]
}).then(function(result) {
  // Check if content (propositions) were returned
  if (result.propositions) {
    var retrievedPropositions = result.propositions;
    // Apply propositions to the page
    return alloy("applyPropositions", {
      propositions: retrievedPropositions
    }).then(function(applyPropositionsResult) {
      var renderedPropositions = applyPropositionsResult.propositions;
      // Send a display notification with the sendEvent command
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
  }
});
```

+++

>[!NOTE]
>
>Es posible [procesar manualmente las modificaciones](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) realizadas en el Compositor de experiencias visuales. No es común el procesamiento manual de modificaciones basadas en VEC. Compruebe si su implementación de at.js utiliza la función `getOffers()` para ejecutar manualmente una solicitud de Target `pageLoad` sin usar `applyOffers()` para aplicar el contenido a la página.

El SDK web de Platform ofrece a los desarrolladores una gran flexibilidad para solicitar y procesar contenido. Consulte la [documentación específica sobre la representación de contenido personalizado](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) para obtener más opciones y detalles.

## Ejemplo de implementación

La implementación básica del SDK web de Platform ha finalizado.

>[!BEGINTABS]

>[!TAB JavaScript]

Ejemplo de JavaScript con representación automática del contenido de Target:

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

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
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
    
    // Send an event to the Adobe edge network and render Target content automatically 
    alloy("sendEvent", {
      "renderDecisions": true
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


>[!TAB Etiquetas]

Página de ejemplo de etiquetas con representación automática del contenido de Target:


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

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
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

En las etiquetas, agregue la extensión SDK para web de Adobe Experience Platform:

![Agregar la extensión del SDK web de Adobe Experience Platform](assets/library-tags-addExtension.png){zoomable="yes"}

Añada las configuraciones deseadas:
![configurar las opciones de migración de la extensión de etiquetas del SDK web](assets/tags-config-migration.png){zoomable="yes"}

Cree una regla con una acción [!UICONTROL Enviar evento] y [!UICONTROL Procesar decisiones de personalización visual] seleccionadas:
![Enviar un evento con las personalizaciones de procesamiento seleccionadas en las etiquetas](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

A continuación, aprenda a solicitar y [procesar actividades de Target basadas en formularios](render-form-based-activities.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
