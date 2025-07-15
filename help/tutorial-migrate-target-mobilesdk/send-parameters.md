---
title: 'Envío de parámetros: Migre la implementación de Adobe Target en su aplicación móvil a la extensión de Offer Decisioning y Target'
description: Obtenga información sobre cómo enviar parámetros de mbox, perfil y entidad a Adobe Target mediante Experience Platform Web SDK.
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# Envío de parámetros a Target mediante la extensión Offer Decisioning y Target

Las implementaciones de Target difieren entre las aplicaciones móviles debido a la arquitectura de la aplicación, los requisitos empresariales y las funciones utilizadas. La mayoría de las implementaciones de Target incluyen pasar varios parámetros para información contextual, audiencias y recomendaciones de contenido.

Con la extensión de Target, todos los parámetros de Target se pasaron mediante la función `TargetParameters`.

Con la extensión Offer Decisioning y Target:

* Los parámetros destinados a varias aplicaciones de Adobe se pueden pasar en el objeto XDM
* Los parámetros destinados únicamente a Target se pueden pasar en el objeto `data.__adobe.target`


>[!IMPORTANT]
>
> Con la extensión Decisioning, los parámetros enviados en una solicitud se aplican a todos los ámbitos de la solicitud. Si necesita establecer parámetros diferentes para ámbitos diferentes, debe realizar solicitudes adicionales.

## Parámetros personalizados

Los parámetros de mbox personalizados son la forma más básica de pasar datos a Target y se pueden pasar en los objetos `xdm` o `data.__adobe.target`.

## Parámetros de perfil

Los parámetros de perfil almacenan datos durante un período de tiempo prolongado en el perfil de Target del usuario y deben pasarse en el objeto `data.__adobe.target`.

## Parámetros de entidad

[Los parámetros de entidad](https://experienceleague.adobe.com/es/docs/target/using/recommendations/entities/entity-attributes) se usan para pasar datos de comportamiento e información de catálogo suplementaria para las recomendaciones de Target. De forma similar a los parámetros de perfil, la mayoría de los parámetros de entidad deben pasarse bajo el objeto `data.__adobe.target`. La única excepción es que la matriz `xdm.productListItems` está presente y el primer valor `SKU` se usa como `entity.id`.

Los parámetros de entidad para un elemento específico deben tener el prefijo `entity.` para que la captura de datos sea correcta. Los parámetros reservados `cartIds` y `excludedIds` para los algoritmos de Recommendations no deben tener un prefijo y el valor de cada uno debe contener una lista separada por comas de los identificadores de entidad.

## Parámetros de compra

Los parámetros de compra se pasan en una página de confirmación de pedido después de un pedido correcto y se utilizan para los objetivos de conversión y optimización de Target. Con una implementación de Platform Mobile SDK que utiliza la extensión Offer Decisioning y Target, estos parámetros y se asignan automáticamente a partir de los datos XDM pasados como parte del grupo de campos `commerce`.

La información de compra se pasa a Target cuando el grupo de campos `commerce` tiene `purchases.value` establecido en `1`. El id. de pedido y el total del pedido se asignan automáticamente desde el objeto `order`. Si la matriz `productListItems` está presente, los valores `SKU` se utilizan para `productPurchasedId`.

Si no pasa `commerce` campos en el objeto `xdm`, puede pasar los detalles del pedido a target mediante los campos `data.__adobe.target.orderId`, `data.__adobe.target.orderTotal` y `data.__adobe.target.productPurchasedId`.

## ID del cliente (mbox3rdPartyId)

Target permite la sincronización de perfiles entre dispositivos y sistemas mediante un único ID de cliente. Este ID de cliente debe pasarse en el campo `identityMap` del objeto XDM y asignarse al campo ID de terceros de destino en la secuencia de datos.

## Tabla

| Ejemplo de parámetro at.js | Opción Platform Web SDK | Notas |
| --- | --- | --- |
| `at_property` | N/A | Los tokens de propiedad están configurados en [datastream](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure#target) y no se pueden establecer en la llamada a `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` o <br> `data.__adobe.target.pageName` | Los parámetros de mbox de destino se pueden pasar como parte del objeto `xdm` o del objeto `data.__adobe.target`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Todos los parámetros de perfil de Target deben pasarse como parte del objeto `data` y tener el prefijo `profile.` para que se asignen correctamente. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parámetro reservado utilizado para la característica de afinidad de categoría de Target, que debe pasarse como parte del objeto `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>O<br> `xdm.productListItems[0].SKU` | Los ID de entidad se utilizan para los contadores de comportamiento de Recommendations de Target. Estos identificadores de entidad se pueden pasar como parte del objeto `data` o asignarse automáticamente a partir del primer elemento de la matriz `xdm.productListItems` si su implementación utiliza ese grupo de campos. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Los identificadores de categoría de entidad se pueden pasar como parte del objeto `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Los parámetros de entidad personalizados se utilizan para actualizar el catálogo de productos de Recommendations. Estos parámetros personalizados deben pasarse como parte del objeto `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Se utiliza para los algoritmos de recomendaciones de Target basados en el carro de compras. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Se utiliza para evitar que se devuelvan ID de entidad específicos en un diseño de recomendaciones. |
| `mbox3rdPartyId` | Establecer en el objeto `xdm.identityMap` | Se utiliza para sincronizar perfiles de Target entre dispositivos y Atributos del cliente. El área de nombres que se va a usar para el ID de cliente debe especificarse en la configuración de [Target del conjunto de datos](https://experienceleague.adobe.com/es/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid). |
| `orderId` | `xdm.commerce.order.purchaseID`<br> (cuando `commerce.purchases.value` está establecido en `1`)<br> o<br> `data.__adobe.target.orderId` | Se utiliza para identificar un pedido único para el seguimiento de conversión de Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br> (cuando `commerce.purchases.value` está establecido en `1`)<br> o<br> `data.__adobe.target.orderTotal` | Se utiliza para rastrear los totales de pedidos de los objetivos de optimización y conversión de Target. |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br> (cuando `commerce.purchases.value` está establecido en `1`) <br>O<br> `data.__adobe.target.productPurchasedId` | Se utiliza para los algoritmos de seguimiento de conversión de Target y de recomendaciones. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Se usa para la meta de actividad [puntuación personalizada](https://experienceleague.adobe.com/es/docs/target/using/activities/success-metrics/capture-score). |

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

>[!TAB SDK de destino]

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

>[!TAB SDK de destino]

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






A continuación, aprenda a [rastrear eventos de conversión de Target](track-events.md) con Platform Web SDK.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Offer Decisioning y Target. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=es#M625).
