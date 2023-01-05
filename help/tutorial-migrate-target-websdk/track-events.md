---
title: Seguimiento de eventos | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo rastrear eventos de conversión de Adobe Target mediante el SDK web de Experience Platform.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Seguimiento de eventos de conversión de Target mediante el SDK web de Platform

Los eventos de conversión para Target se pueden rastrear con el SDK web de Platform similar a at.js. Los eventos de conversión suelen clasificarse en las siguientes categorías:

* Eventos rastreados automáticamente que no requieren ninguna configuración
* Eventos de conversión de compra que deben ajustarse para una implementación de SDK web de Platform recomendada
* Eventos de conversión que no son de compra y que requieren actualizaciones de código

## Comparación de seguimiento de objetivos

La siguiente tabla compara el modo en que at.js y el SDK web de plataforma rastrean eventos de conversión

| Objetivo de la actividad | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Conversión > Visualizó una página | Se rastrea automáticamente. Basado en el valor de `context.address.url` en la carga útil de solicitud at.js. | Se rastrea automáticamente. Basado en el valor de `xdm.web.webPageDetails.URL` en el `sendEvent` carga útil |
| Conversión > Visualizó un mbox | Rastreado con la solicitud de una ubicación de mbox de visualización o una notificación mediante `trackEvent()` o `sendNotifications()` con un `type` valor de `display`. | Seguimiento con un SDK web de plataforma `sendEvent` con la variable `eventType` de `decisioning.propositionDisplay`. |
| Conversión > Se hizo clic en un elemento | Se rastrea automáticamente para actividades basadas en VEC. Aparece como una llamada de red de at.js con un `notifications` en la carga útil de la solicitud in y un `type` valor de `click`. | Se rastrea automáticamente para actividades basadas en VEC. Aparece como un SDK web de plataforma `sendEvent` con la variable `eventType` de `decisioning.propositionInteract`. |
| Participación > Vistas de página | Seguimiento automático | Seguimiento automático |
| Participación > Tiempo en el sitio | Seguimiento automático | Seguimiento automático |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Eventos rastreados automáticamente

Los siguientes objetivos de conversión no requieren ajustes específicos en la implementación:

* Conversión > Visualizó una página
* Conversión > Se hizo clic en un elemento
* Participación > Vistas de página
* Participación > Tiempo en el sitio

>[!NOTE]
>
>El SDK web de Platform permite un bueno control sobre los valores pasados en la carga útil de la solicitud. Para garantizar que las funciones de Target, como las URL de control de calidad y los objetivos de conversión &quot;Visualizó una página&quot;, funcionen correctamente, compruebe que la variable `xdm.web.webPageDetails.URL` contiene la dirección URL de la página completa con el caso de caracteres adecuado.

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## Eventos seguidos personalizados

Las implementaciones de Target suelen utilizar eventos de conversión personalizados para rastrear clics en actividades basadas en formularios, para indicar una conversión en un flujo o para pasar parámetros sin solicitar nuevo contenido.

La siguiente tabla describe el enfoque de at.js y el SDK web de plataforma equivalente para algunos casos de uso comunes de seguimiento de conversión.

| Caso de uso | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Seguimiento de un evento de conversión de clics para una ubicación de mbox (ámbito) | Ejecutar `trackEvent()` o `sendNotifications()` con un `type` valor de `click` para una ubicación de mbox específica | Ejecutar un `sendEvent` con un tipo de evento de `decisioning.propositionInteract` |
| Realizar el seguimiento de un evento de conversión personalizado que también puede incluir datos adicionales, como parámetros de perfil de Target | Ejecutar `trackEvent()` o `sendNotifications()` con un `type` valor de `display` para una ubicación de mbox específica | Ejecutar un `sendEvent` con un tipo de evento de `decisioning.propositionDisplay` |

>[!NOTE]
>
>Aunque `decisioning.propositionDisplay` se utiliza generalmente para incrementar impresiones para ámbitos específicos, también debe utilizarse como reemplazo directo de at.js `trackEvent()` normalmente. La variable `trackEvent()` la función predeterminada es un tipo de `display` si no se especifica. Compruebe la implementación para asegurarse de que utiliza el tipo de evento correcto para las conversiones personalizadas que pueda haber definido.

Consulte la documentación de at.js para obtener más información sobre cómo utilizar [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) y [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) para rastrear eventos de Target.

Ejemplo de at.js con `trackEvent()` para rastrear un clic en una ubicación de mbox:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Con una implementación del SDK web de Platform, puede realizar el seguimiento de eventos y acciones del usuario llamando a la función `sendEvent` rellenando la variable `_experience.decisioning.propositions` Grupo de campos XDM y configuración del `eventType` a uno de dos valores:

* `decisioning.propositionDisplay`: Indica la renderización de la actividad de Target.
* `decisioning.propositionInteract`: Indica la interacción del usuario con la actividad, como un clic del ratón.

La variable `_experience.decisioning.propositions` El grupo de campos XDM es una matriz de objetos. Las propiedades de cada objeto se derivan de la variable `result.propositions` que se devuelve en la variable `sendEvent` comando: `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

A continuación, aprenda a [habilitar el uso compartido de ID entre dominios](cross-domain.md) para perfiles de visitante coherentes.

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).