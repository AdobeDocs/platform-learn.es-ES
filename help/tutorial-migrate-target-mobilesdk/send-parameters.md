---
title: 'Parámetros de envío: migración del implementación Adobe Target de la aplicación móvil a la Adobe Systems Journey Optimizer: extensión de toma de decisiones'
description: Obtenga información sobre cómo enviar parámetros de mbox, perfil y entidad a Adobe Target mediante Experience Platform SDK web.
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: 2ebad2014d4c29a50af82328735258958893b42c
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# Enviar parámetros a Target con la extensión Decisioning

Target implementaciones difieren entre las aplicaciones móviles debido a la arquitectura de la aplicación, los requisitos empresariales y las funciones utilizadas. La mayoría de las implementaciones Target incluyen la transmisión de diversos parámetros para información contextual, audiencias y recomendaciones contenido.

Con la extensión Target, todos los parámetros Target se pasaban utilizando la `TargetParameters` función.

With the Decisioning extension:

* Parameters intended for multiple Adobe applications can be passed in the XDM object
* Parameters intended only for Target can be passed in the `data.__adobe.target` object


>[!IMPORTANT]
>
> With the Decsioning extension, parameters sent in a request apply to all scopes in the request. If you need to set different parameters for different scopes you must make additional requests.

## Custom parameters

Los parámetros de mbox personalizados son la forma más básica de pasar datos a Target y se pueden pasar en los objetos `xdm` o `data.__adobe.target`.

## Parámetros de perfil

Los parámetros de perfil almacenan datos durante un período de tiempo prolongado en el perfil de Target del usuario y deben pasarse en el objeto `data.__adobe.target`.

## Parámetros de entidad

[Los parámetros de entidad](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/entity-attributes) se usan para pasar datos de comportamiento e información de catálogo suplementaria para las recomendaciones de Target. De forma similar a los parámetros de perfil, la mayoría de los parámetros de entidad deben pasarse bajo el objeto `data.__adobe.target`. La única excepción es que la `xdm.productListItems` matriz está presente, entonces el primer valor se utiliza como el `entity.id`archivo `SKU` .

Los parámetros de entidad para un elemento específico deben tener un prefijo para `entity.` la captura de datos adecuada. Los algoritmos reservados `cartIds` y `excludedIds` parámetros para recomendaciones no deben tener el prefijo y el valor de cada uno debe contener un lista separado por comas de los ID de entidad.

## Parámetros de compra

Los parámetros de compra se pasan en una página de confirmación de pedido después de un pedido correcto y se utilizan para los objetivos de conversión y optimización de Target. Con una implementación de Platform Mobile SDK que utiliza la extensión Decisioning, estos parámetros y se asignan automáticamente a partir de los datos XDM pasados como parte del grupo de campos `commerce`.

La información de compra se pasa a Target cuando el grupo de campos `commerce` tiene `purchases.value` establecido en `1`. El ID del pedido y el total del pedido se asignan automáticamente desde el `order` objeto. Si la `productListItems` matriz está presente, los `SKU` valores se utilizan para `productPurchasedId`.

Si no está pasando `commerce` campos en el `xdm` objeto, puede pasar el detalles del pedido a destino utilizando los `data.__adobe.target.orderId`campos , `data.__adobe.target.orderTotal`, y `data.__adobe.target.productPurchasedId` .

## ID de cliente (mbox3rdPartyId)

Target permite la sincronización perfil entre dispositivos y sistemas utilizando un único ID de cliente. Este ID de cliente debe pasarse en el `identityMap` campo del objeto XDM y asignarse al campo ID de Target terceros del flujo de datos.

## Tabla

| Example at.js parameter | Platform Web SDK option | Notas |
| --- | --- | --- |
| `at_property` | N/A | Property tokens are configured in the [datastream](https://experienceleague.adobe.com/en/docs/experience-platform/edge/datastreams/configure#target) and cannot be set in the `sendEvent` call. |
| `pageName` | `xdm.web.webPageDetails.name` o <br> `data.__adobe.target.pageName` | Los parámetros de mbox de destino se pueden pasar como parte del objeto `xdm` o del objeto `data.__adobe.target`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Todos los parámetros de perfil de Target deben pasarse como parte del objeto `data` y tener el prefijo `profile.` para que se asignen correctamente. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parámetro reservado utilizado para la característica de afinidad de categoría de Target, que debe pasarse como parte del objeto `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>O<br> `xdm.productListItems[0].SKU` | Los ID de entidad se utilizan para los contadores de comportamiento de Recommendations de Target. Estos ID de entidad se pueden pasar como parte del `data` objeto o asignarse automáticamente desde el primer elemento de la `xdm.productListItems` matriz si el implementación utiliza ese campo grupo. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Las ID de categoría de entidad se pueden pasar como parte del `data` objeto. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Los parámetros de entidad personalizados se utilizan para actualizar el catálogo de productos de Recommendations. Estos parámetros personalizados deben pasarse como parte del objeto `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Se utiliza para los algoritmos de recomendaciones de Target basados en el carro de compras. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Se utiliza para evitar que se devuelvan ID de entidad específicos en un diseño de recomendaciones. |
| `mbox3rdPartyId` | Set in the `xdm.identityMap` object | Used for synching Target profiles across devices and Customer Attributes. The namespace to use for the customer ID must be specified in the [Target configuration of the datastream](https://experienceleague.adobe.com/en/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid). |
| `orderId` | `xdm.commerce.order.purchaseID`<br> (when `commerce.purchases.value` is set to `1`)<br> or<br> `data.__adobe.target.orderId` | Used for identifying a unique order for Target conversion tracking. |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br> (when `commerce.purchases.value` is set to `1`)<br> or<br> `data.__adobe.target.orderTotal` | Se utiliza para rastrear los totales de pedidos de los objetivos de optimización y conversión de Target. |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br> (cuando `commerce.purchases.value` está establecido en `1`) <br>O<br> `data.__adobe.target.productPurchasedId` | Se utiliza para los algoritmos de seguimiento de conversión de Target y de recomendaciones. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Se usa para la meta de actividad [puntuación personalizada](https://experienceleague.adobe.com/en/docs/target/using/activities/success-metrics/capture-score). |

{style="table-layout:auto"}


## Ejemplos de paso de parámetros

Veamos un ejemplo sencillo para demostrar las diferencias entre las extensiones al pasar parámetros a Target.

### Android

>[!BEGINTABS]

>[!TAB Optimizar SDK]

```Java
final Map<String, Object> data = new HashMap<>();
final Map<String, String> targetParameters = new HashMap<>();
 
// Mbox parameters
targetParameters.put("status", "platinum");
 
// Profile parameters - prefix with profile.
targetParameters.put("profile.gender", "male");
 
// Product parameters
targetParameters.put("productId", "pId1");
targetParameters.put("categoryId", "cId1");
 
// Order parameters
targetParameters.put("orderId", "id1");
targetParameters.put("orderTotal", "1.0");
targetParameters.put("purchasedProductIds", "ppId1");
 
data.put("__adobe", new HashMap<String, Object>() {
  {
    put("target", targetParameters);
  }
});
 
// Target location (or mbox)
final DecisionScope decisionScope = DecisionScope("myTargetLocation")
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope);
 
Optimize.updatePropositions(decisionScopes, null, data);
```

>[!TAB Target SDK]

```Java
Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");
 
Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");
 
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("ppId1");
TargetOrder targetOrder = new TargetOrder("id1", 1.0, purchasedProductIds);
 
TargetProduct targetProduct = new TargetProduct("pId1", "cId1");
 
TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters)
                                    .profileParameters(profileParameters)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

>[!ENDTABS]

### iOS

>[!BEGINTABS]

>[!TAB Optimizar SDK]

```Swift
var data: [String: Any] = [:]
var targetParameters: [String: String] = [:]
 
// Mbox parameters
targetParameters["status"] = "platinum"
 
// Profile parameters - prefix with profile.
targetParameters["profile.gender"] = "make"
 
// Product parameters
targetParameters["productId"] = "pId1"
targetParameters["categoryId"] = "cId1"
 
// Add order parameters
targetParameters["orderId"] = "id1"
targetParameters["orderTotal"] = "1.0"
targetParameters["purchasedProductIds"] = "ppId1"
 
data["__adobe"] = [
  "target": targetParameters
]
 
// Target location (or mbox)
let decisionScope = DecisionScope(name: "myTargetLocation")
Optimize.updatePropositions(for: [decisionScope] withXdm: nil andData: data)
```

>[!TAB Target SDK]

```Swift
let mboxParameters = [
                        "status": "platinum"
                     ]
 
let profileParameters = [
                            "gender": "male"
                        ]
 
let order = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
 
let product = TargetProduct(productId: "pId1", categoryId: "cId1")
 
let targetParameters = TargetParameters(parameters: mboxParameters, profileParameters: profileParameters, order: order, product: product))
```


>[!ENDTABS]






Siguiente, aprenda a realizar un [seguimiento de Target eventos](track-events.md) de Conversión con el SDK web de Platform.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con la migración de su Target móvil de la extensión Target a la extensión Decisioning. Si se encuentra con obstáculos con su migración o siente gustar falta esencial información en este guía, háganoslo saber publicando en [esta discusión](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625) de la Comunidad.
