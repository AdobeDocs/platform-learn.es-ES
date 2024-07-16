---
title: Seguimiento de eventos | Migración de Target de at.js 2.x a SDK web
description: Obtenga información sobre cómo rastrear eventos de conversión de Adobe Target mediante el SDK web de Experience Platform.
exl-id: 5da772bc-de05-4ea9-afbd-3ef58bc7f025
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# Seguimiento de eventos de conversión de Target mediante el SDK web de Platform

Los eventos de conversión para Target se pueden rastrear con el SDK web de Platform similar a at.js. Los eventos de conversión suelen clasificarse en las siguientes categorías:

* Eventos rastreados automáticamente que no requieren ninguna configuración
* Adquiera eventos de conversión que deban ajustarse para una implementación de SDK web de Platform de prácticas recomendadas.
* Eventos de conversión que no son de compra y que requieren actualizaciones de código

## Comparación de seguimiento de objetivos

La siguiente tabla compara cómo at.js y el SDK web de Platform rastrean los eventos de conversión

| Objetivo de actividad | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Conversión > Visualizó una página | Seguimiento automático. Basado en el valor de `context.address.url` en la carga útil de la solicitud at.js. | Seguimiento automático. Basado en el valor de `xdm.web.webPageDetails.URL` en la carga útil `sendEvent` |
| Conversión > Visualizó un mbox | Se ha registrado con la solicitud de una ubicación de mbox de visualización o una notificación que usa `trackEvent()` o `sendNotifications()` con un valor `type` de `display`. | Seguimiento con una llamada del SDK web de Platform `sendEvent` con `eventType` de `decisioning.propositionDisplay`. |
| Conversión > Se hizo clic en un elemento | Se rastrea automáticamente para actividades basadas en VEC. Aparece como una llamada de red at.js con un objeto `notifications` en la carga de la solicitud y un valor `type` de `click`. | Se rastrea automáticamente para actividades basadas en VEC. Aparece como una llamada del SDK web de Platform `sendEvent` con `eventType` de `decisioning.propositionInteract`. |
| Participación > Vistas de página | Seguimiento automático | Seguimiento automático |
| Participación > Tiempo en el sitio | Seguimiento automático | Seguimiento automático |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Eventos rastreados automáticamente

Los siguientes objetivos de conversión no requieren ningún ajuste específico en la implementación:

* Conversión > Visualizó una página
* Conversión > Se hizo clic en un elemento
* Participación > Vistas de página
* Participación > Tiempo en el sitio

>[!NOTE]
>
>El SDK web de Platform permite un mayor control sobre los valores pasados en la carga útil de la solicitud. Para garantizar que las funciones de Target, como las direcciones URL de control de calidad y los objetivos de conversión &quot;Visualizó una página&quot;, funcionen correctamente, compruebe que el valor `xdm.web.webPageDetails.URL` contenga la dirección URL de página completa con el carácter adecuado.

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

## Eventos con seguimiento personalizado

Las implementaciones de Target suelen utilizar eventos de conversión personalizados para rastrear clics en actividades basadas en formularios, para significar una conversión en un flujo o para pasar parámetros sin solicitar contenido nuevo.

La siguiente tabla describe el método at.js y el equivalente del SDK web de Platform para algunos casos de uso de seguimiento de conversión comunes.

| Ejemplo de uso | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Seguimiento de un evento de conversión de clics para una ubicación (ámbito) de mbox | Ejecutar `trackEvent()` o `sendNotifications()` con un valor `type` de `click` para una ubicación de mbox específica | Ejecutar un comando `sendEvent` con un tipo de evento de `decisioning.propositionInteract` |
| Realizar un seguimiento de un evento de conversión personalizado que también pueda incluir datos adicionales, como parámetros de perfil de Target | Ejecutar `trackEvent()` o `sendNotifications()` con un valor `type` de `display` para una ubicación de mbox específica | Ejecutar un comando `sendEvent` con un tipo de evento de `decisioning.propositionDisplay` |

>[!NOTE]
>
>Aunque `decisioning.propositionDisplay` se utiliza habitualmente para incrementar impresiones de ámbitos específicos, también debería utilizarse como reemplazo directo de at.js `trackEvent()`. La función `trackEvent()` toma como valor predeterminado un tipo de `display` si no se especifica. Compruebe la implementación para asegurarse de utilizar el tipo de evento correcto para cualquier conversión personalizada que haya definido.

Consulte la documentación de at.js dedicada para obtener más información sobre cómo usar [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) y [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) para el seguimiento de eventos de Target.

Ejemplo de at.js con `trackEvent()` para rastrear un clic en una ubicación de mbox:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Con una implementación del SDK web de Platform, puede realizar un seguimiento de eventos y acciones del usuario llamando al comando `sendEvent`, rellenando el grupo de campos XDM `_experience.decisioning.propositions` y estableciendo `eventType` en uno de los dos valores siguientes:

* `decisioning.propositionDisplay`: indica la representación de la actividad de Target.
* `decisioning.propositionInteract`: indica la interacción de un usuario con la actividad, como un clic del ratón.

El grupo de campos XDM `_experience.decisioning.propositions` es una matriz de objetos. Las propiedades de cada objeto se derivan del objeto `result.propositions` devuelto en el comando `sendEvent`: `{ id, scope, scopeDetails }`

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

A continuación, aprenda a [habilitar el uso compartido de ID entre dominios](cross-domain.md) para perfiles de visitantes consistentes.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
