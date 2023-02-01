---
title: Enviar parámetros | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo enviar parámetros de mbox, perfil y entidad a Adobe Target mediante el SDK web de Experience Platform.
source-git-commit: 43740912bc5a941aa21c5f38ed2c1aac74abffbc
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Envío de parámetros a Target mediante el SDK web de plataforma

Las implementaciones de Target difieren de un sitio a otro debido a la arquitectura del sitio, los requisitos comerciales y las características utilizadas. La mayoría de las implementaciones de Target incluyen el paso de varios parámetros para información contextual, audiencias y recomendaciones de contenido.

>[!WARNING]
>
> Es posible que las implementaciones de Platform Web SDK que se inicien después del 1 de octubre de 2022 deban utilizar la variable [solución de recuperación previa](prefetch-workaround.md) para pasar correctamente los parámetros descritos en esta página.

Vamos a usar una sencilla página de detalles del producto y una página de confirmación de pedidos para demostrar las diferencias entre las bibliotecas al pasar parámetros a Target.

Supongamos que la siguiente página de ejemplo utiliza at.js:

<!--Assume the following two example pages using at.js:-->

Detalles del producto:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Mbox parameters
        "siteSection": "product details",
        // Profile parameters
        "profile.gender": "male",
        "user.categoryId": "clothing",
        // Entity parameters for Target Recomendations
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL",
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```



Confirmación del pedido:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>-->
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Order confirmation parameters
        "orderId": "ABC123",
        "productPurchasedId": "SKU-00002,SKU-00003",
        "orderTotal": 1337.89,
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```


## Resumen de asignación de parámetros

Los parámetros de Target utilizados en estas dos páginas de ejemplo deben enviarse de forma un poco diferente mediante el SDK web de Platform. Existen varias formas de pasar parámetros a Target mediante at.js:

- Configure con `targetPageParams()` para el evento de carga de página
- Configure con `targetPageParamsAll()` para todas las solicitudes de Target de la página
- Envíe los parámetros directamente con la variable `getOffer()` para una sola ubicación
- Envíe los parámetros directamente con la variable `getOffers()` para una o más ubicaciones

Para los fines de este ejemplo, la variable `targetPageParams()` se utiliza.

El SDK web de Platform lo simplifica al proporcionar una única forma coherente de enviar datos sin necesidad de funciones adicionales. Todos los parámetros deben pasarse en la carga útil con la variable `sendEvent` comando.

Parámetros pasados con el SDK web de Platform `sendEvent` la carga útil se clasifica en dos categorías:

1. Se asigna automáticamente desde la variable `xdm` object
1. Se transfiere manualmente mediante la variable `data.__adobe.target` object

La tabla siguiente describe cómo se reasignarán los parámetros de ejemplo mediante el SDK web de Platform:

| Ejemplo de parámetro de at.js | Opción de SDK web de plataforma | Notas |
| --- | --- | --- |
| `at_property` | N/A | Los tokens de propiedad se configuran en la variable [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) y no se pueden configurar en la variable `sendEvent` llamada a . |
| `siteSection` | `xdm.web.webPageDetails.siteSection` | Todos los parámetros de mbox de Target deben pasarse como parte del `xdm` y se ajustan a un esquema utilizando la clase XDM ExperienceEvent . Los parámetros de mbox no se pueden pasar como parte del `data` objeto. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Todos los parámetros de perfil de Target deben pasarse como parte del `data` con el prefijo `profile.` para que se asigne correctamente. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parámetro reservado utilizado para la función de afinidad de la categoría de Target que debe pasarse como parte del `data` objeto. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OR<br> `xdm.productListItems[0].SKU` | Los ID de entidad se utilizan para los contadores de comportamiento de Recommendations de Target. Estos ID de entidad se pueden pasar como parte del `data` o se asigna automáticamente desde el primer elemento del `xdm.productListItems` matriz si su implementación utiliza ese grupo de campos. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Los ID de categoría de entidad se pueden pasar como parte del `data` objeto. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Los parámetros de entidad personalizados se utilizan para actualizar el catálogo de productos de Recommendations. Estos parámetros personalizados deben pasarse como parte del `data` objeto. |
| `cartIds` | `data.__adobe.target.cartIds` | Se utiliza para los algoritmos de recomendaciones basadas en el carro de compras de Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Se utiliza para evitar que los ID de entidad específicos se devuelvan en un diseño de recomendaciones. |
| `mbox3rdPartyId` | Se establece en el mapa de identidad. Consulte [Sincronización de perfiles con un ID de cliente](#synching-profiles-with-a-customer-id) | Se utiliza para sincronizar perfiles de Target entre dispositivos y atributos del cliente. El espacio de nombres que se va a usar para el ID de cliente debe especificarse en la variable [Configuración de destino del conjunto de datos](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Se utiliza para identificar un pedido único para el seguimiento de conversión de Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Se utiliza para rastrear totales de pedidos para los objetivos de optimización y conversión de Target. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>OR<br> `xdm.productListItems[0-n].SKU` | Se utiliza para el seguimiento de conversión de Target y los algoritmos de recomendaciones. Consulte la [parámetros de entidad](#entity-parameters) para obtener más información. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Se usa para la variable [puntuación personalizada](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) objetivo de la actividad. |

{style=&quot;table-layout:auto&quot;}

## Parámetros personalizados

Todos los parámetros personalizados de mbox deben pasarse como datos XDM con la variable `sendEvent` comando. Es importante asegurarse de que el esquema XDM incluya todos los puntos de datos necesarios para la implementación de Target.

Ejemplo de at.js con `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "siteSection": "product detail"
  };
};
```

Ejemplo de SDK web de plataforma mediante `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "siteSection": "product detail"
      }
    }
  }
});
```

>[!NOTE]
>
>Porque los parámetros personalizados de mbox deben enviarse como parte de `xdm` en el `sendEvent` , todos los parámetros de mbox utilizados en la implementación de at.js Target deben reasignarse a un equivalente XDM. Esto significa que debe actualizar cualquier audiencia, actividad o script de perfil que haga referencia a estos parámetros de mbox.


## Parámetros de perfil

Los parámetros de perfil de Target deben pasarse en la sección `data.__adobe.target` en el SDK web de Platform `sendEvent` carga útil del comando.

Al igual que at.js, todos los parámetros de perfil deben tener también el prefijo `profile.` para que el valor se almacene correctamente como atributo de perfil de Target persistente. El `user.categoryId` parámetro para la capacidad de afinidad de la categoría de Target tiene el prefijo `user.`.

Ejemplo de at.js con `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

Ejemplo de SDK web de plataforma mediante `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "male",
        "user.categoryId": "clothing"
      }
    }
  }
});
```

## Parámetros de entidad

Los parámetros de entidad se utilizan para pasar datos de comportamiento e información de catálogo suplementaria para Target Recommendations. De forma similar a los parámetros de perfil, todos los parámetros de entidad deben pasarse bajo la categoría `data.__adobe.target` en el SDK web de Platform `sendEvent` carga útil del comando.

Los parámetros de entidad para un elemento específico deben tener el prefijo `entity.` para una captura de datos adecuada. El `cartIds` y `excludedIds` los parámetros de los algoritmos de recomendaciones no deben tener prefijo, y el valor de cada uno debe contener una lista de ID de entidad separados por comas.

Ejemplo de at.js con `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "entity.id": "SKU-00001-LARGE",
    "entity.categoryId": "clothing,shirts",
    "entity.customEntity": "some value",
    "cartIds": "SKU-00002,SKU-00003",
    "excludedIds": "SKU-00001-SMALL"
  };
};
```

Ejemplo de SDK web de plataforma mediante `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts"
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

Todo [parámetros de entidad](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) at.js también es compatible con el SDK web de Platform.

>[!NOTE]
>
>Si la variable `commerce` se utiliza el grupo de campos y la variable `productListItems` matriz se incluye en la carga útil XDM y luego en la primera `SKU` en esta matriz se asigna a `entity.id` para incrementar una vista de producto.


## Parámetros de compra

Los parámetros de compra se pasan en una página de confirmación de pedido después de un pedido correcto y se utilizan para los objetivos de conversión y optimización de Target. Con una implementación del SDK web de Platform, estos parámetros y se asignan automáticamente a partir de datos XDM pasados como parte del `commerce` grupo de campos.

Ejemplo de at.js con `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

La información de compra se pasa a Target cuando la variable `commerce` el grupo de campos tiene `puchases.value` configure como `1`. El ID de pedido y el total del pedido se asignan automáticamente desde la variable `order` objeto. Si la variable `productListItems` la matriz está presente, luego la variable `SKU` los valores se usan para `productPurchasedId`.

Ejemplo de SDK web de plataforma mediante `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "ABC123",
        "priceTotal": 1337.89
      },
      "purchases": {
        "value": 1
      }
    },
    "productListItems": [{
      "SKU": "SKU-00002"
    }, {
      "SKU": "SKU-00003"
    }]
  }
});
```

>[!NOTE]
>
>La variable `productPurchasedId` también se puede pasar como una lista de ID de entidad separados por comas en la sección `data` objeto.


## Sincronización de perfiles con un ID de cliente

Target permite sincronizar perfiles entre dispositivos y sistemas con un solo ID de cliente. Con at.js, esto podría establecerse como el `mbox3rdPartyId` en la solicitud de Target o como el primer ID de cliente enviado al servicio de ID de Experience Cloud. A diferencia de at.js, una implementación del SDK web de plataforma le permite especificar qué ID de cliente utilizar como `mbox3rdPartyId` si hay varios. Por ejemplo, si su empresa tiene un ID de cliente global y un ID de cliente independiente para diferentes líneas de negocio, puede configurar qué ID debe utilizar Target.

Hay que seguir algunos pasos para configurar la sincronización de ID para los casos de uso de Target entre dispositivos y Atributos del cliente:

1. Cree un **[!UICONTROL área de nombres de identidad]** para el ID de cliente en **[!UICONTROL Identidades]** pantalla de la recopilación de datos o la plataforma
1. Asegúrese de que la variable **[!UICONTROL alias]** en Atributos del cliente coincide con la variable **[!UICONTROL símbolo de identidad]** de su espacio de nombres
1. Especifique la variable **[!UICONTROL símbolo de identificación]** como el **[!UICONTROL Espacio de nombres de ID de terceros de Target]** en la configuración de Target del conjunto de datos
1. Ejecutar un `sendEvent` usando la variable `identityMap` grupo de campos

Ejemplo de at.js con `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

Ejemplo de SDK web de plataforma mediante `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated"
      }]
    }
  }
});
```


## Ejemplo de SDK web de plataforma

Ahora que comprende cómo se asignan los distintos parámetros de Target mediante el SDK web de Platform, nuestras dos páginas de ejemplo se pueden migrar de at.js al SDK web de Platform, como se muestra a continuación. Las páginas de ejemplo incluyen lo siguiente:

- Fragmento de preocultación de Target para una implementación de biblioteca asíncrona
- El código base del SDK web de la plataforma
- Biblioteca JavaScript del SDK web de Platform
- A `configure` para inicializar la biblioteca
- A `sendEvent` para enviar datos y solicitar que se procese el contenido de Target

Detalles del producto:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>

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

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "renderDecisions": true,
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "web": {
          "webPageDetails": {
            // Other attributes included according to XDM schema
            "siteSection": "product detail"
          }
        }
      },
      "data": {
        "__adobe": {
          "target": {
            "profile.gender": "male",
            "user.categoryId": "clothing",
            "entity.id": "SKU-00001-LARGE",
            "entity.categoryId": "clothing,shirts",
            "entity.customEntity": "some value",
            "cartIds": "SKU-00002,SKU-00003",
            "excludedIds": "SKU-00001-SMALL"
          }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```


Confirmación del pedido:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>


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

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "commerce": {
          "order": {
            "purchaseID": "ABC123",
            "priceTotal": 1337.89
          },
          "purchases": {
            "value": 1
          }
        },
        "productListItems": [{
          "SKU": "SKU-00002"
        }, {
          "SKU": "SKU-00003"
        }]
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

A continuación, aprenda a [seguimiento de eventos de conversión de Target](track-events.md) con el SDK web de Platform.

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
