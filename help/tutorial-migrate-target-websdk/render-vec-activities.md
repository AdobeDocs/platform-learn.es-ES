---
title: Procesar actividades de VEC | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo recuperar y aplicar actividades del compositor de experiencias visuales con una implementación de SDK web de Adobe Target.
feature: Visual Experience Composer (VEC),Implement Client-side,APIs/SDKs,at.js,AEP Web SDK, Web SDK,Implementation
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 5%

---

# Procesar actividades del Compositor de experiencias visuales (VEC) de Adobe Target

Las actividades de Target se configuran mediante el Compositor de experiencias visuales (VEC) o el Compositor basado en formularios. El SDK web de Platform puede recuperar y aplicar actividades basadas en VEC a la página, como at.js. Para esta parte de la migración, debe:

* Instalación de la extensión del explorador de Visual Editing Helper
* Ejecutar un `sendEvent` invoque con el SDK web de Platform para solicitar actividades.
* Actualice cualquier referencia de la implementación de at.js que use `getOffers()` para ejecutar un objetivo `pageLoad` solicitud.

## Extensión del explorador de Visual Editing Helper

La extensión del explorador Adobe Experience Cloud Visual Editing Helper para Google Chrome permite cargar sitios web de forma fiable dentro del Compositor de experiencias visuales (VEC) de Adobe Target para crear y realizar controles de calidad de experiencias rápidamente.

La extensión del explorador de Visual Editing Helper funciona con sitios web que utilizan at.js o Platform Web SDK.

>[!IMPORTANT]
>
>La nueva extensión de ayuda de edición visual sustituye a la anterior [Extensión de explorador de VEC Helper de Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). Si está instalada la extensión anterior de VEC Helper, debe eliminarse o deshabilitarse antes de utilizar la extensión de Visual Editing Helper.

### Obtenga e instale el Asistente de edición visual

1. Vaya a la [Extensión del explorador Adobe Experience Cloud Visual Editing Helper en Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Haga clic en Agregar a **Chrome** > **Agregar extensión**.
1. Abra el VEC en Target.
1. Para utilizar la extensión, haga clic en el icono de extensión del explorador de Visual Editing Helper ![Icono de extensión de edición visual](assets/VEC-Helper.png){zoomable=&quot;yes&quot;} en la barra de herramientas del explorador Chrome mientras está en modo VEC o QA.

La Ayuda de edición visual se activa automáticamente cuando se abre un sitio web en el VEC de Target para la creación de contenido. La extensión no tiene ninguna configuración condicional. La extensión gestiona todas las configuraciones automáticamente, incluida la configuración de cookies de SameSite.

Consulte la documentación dedicada para obtener más información sobre la [Extensión de Visual Editing Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) y [solución de problemas del Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

## Solicitar y aplicar contenido automáticamente

Una vez configurado el SDK web de Platform en la página, puede solicitar contenido desde Target. A diferencia de at.js, que se puede configurar para que solicite contenido automáticamente cuando se carga la biblioteca, el SDK web de Platform requiere que ejecute explícitamente un comando.

Si la implementación de at.js tiene la variable `pageLoadEnabled` configurar como `true` que habilita el procesamiento automático de actividades basadas en VEC, entonces se ejecuta lo siguiente `sendEvent` con el SDK web de Platform:

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB Etiquetas]

En las etiquetas , use la variable [!UICONTROL Enviar evento] tipo de acción con la variable [!UICONTROL Procesar decisiones de personalización visual] opción seleccionada:

![Enviar un evento con Renderizar decisiones de personalización visual seleccionadas en etiquetas](assets/vec-sendEvent-renderTrue.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## Solicitar y aplicar contenido bajo demanda

Algunas implementaciones de Target requieren cierto procesamiento personalizado de las ofertas de VEC antes de aplicarlas a la página. O bien, solicitan varias ubicaciones en una sola llamada. En una implementación de at.js, esto se puede hacer estableciendo `pageLoadEnabled` a `false` y utilizando `getOffers()` para ejecutar una función `pageLoad` solicitud.

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

El SDK web de Platform no tiene un `pageLoad` evento. Todas las solicitudes de contenido de Target se controlan con la variable `decisionScopes` con la opción `sendEvent` comando. La variable `__view__` el ámbito de aplicación cumple el objetivo del `pageLoad` solicitud.

+++ SDK web de plataforma equivalente `sendEvent` enfoque:

1. Ejecutar un `sendEvent` que incluye el comando `__view__` ámbito de decisión
1. Aplique el contenido devuelto a la página con la variable `applyPropositions` command
1. Ejecutar un `sendEvent` con la variable `decisioning.propositionDisplay` tipo de evento y detalles de propuesta para aumentar una impresión

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
>Es posible [modificaciones de renderización manual](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) realizado en el Compositor de experiencias visuales. El procesamiento manual de modificaciones basadas en VEC no es común. Compruebe si la implementación de at.js utiliza la variable `getOffers()` para ejecutar manualmente un Target `pageLoad` solicitud sin usar `applyOffers()` para aplicar el contenido a la página.

El SDK web de Platform ofrece a los desarrolladores una buena flexibilidad para solicitar y procesar contenido. Consulte la [documentación dedicada sobre la renderización de contenido personalizado](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) para obtener más información y opciones.

## Ejemplo de implementación

La implementación básica del SDK web de Platform ya ha finalizado.

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

Página de ejemplo de etiquetas con representación automática de contenido de Target:


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

En las etiquetas , agregue la extensión web SDK de Adobe Experience Platform:

![Añadir la extensión del SDK web de Adobe Experience Platform](assets/library-tags-addExtension.png){zoomable=&quot;yes&quot;}

Añada las configuraciones deseadas:
![configuración de las opciones de migración de la extensión de etiqueta SDK web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}

Cree una regla con un [!UICONTROL Enviar evento] acción y [!UICONTROL Procesar decisiones de personalización visual] seleccionados:
![Enviar un evento con Personalizaciones de procesamiento seleccionadas en etiquetas](assets/vec-sendEvent-renderTrue.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

A continuación, aprenda a solicitar y [procesar actividades de Target basadas en formularios](render-form-based-activities.md).

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
