---
title: 'Envío de parámetros: Migre Target de at.js 2.x al SDK web'
description: Obtenga información sobre cómo enviar parámetros de mbox, perfil y entidad a Adobe Target mediante el SDK web de Experience Platform.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---

# Envío de parámetros a Target mediante el SDK web de Platform

Las implementaciones de Target difieren entre sitios web debido a la arquitectura del sitio, los requisitos comerciales y las características utilizadas. La mayoría de las implementaciones de Target incluyen pasar varios parámetros para información contextual, audiencias y recomendaciones de contenido.

Usemos una página de detalles de producto sencilla y una página de confirmación de pedido para demostrar las diferencias entre las extensiones al pasar parámetros a Target.


| Ejemplo de parámetro at.js | Opción SDK web de Platform | Notas |
| --- | --- | --- |
| `at_property` | N/A | Los tokens de propiedad están configurados en [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) y no se pueden establecer en la llamada a `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` | Todos los parámetros de mbox de Target deben pasarse como parte del objeto `xdm` y ajustarse a un esquema mediante la clase XDM ExperienceEvent. Los parámetros de mbox no se pueden pasar como parte del objeto `data`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Todos los parámetros de perfil de Target deben pasarse como parte del objeto `data` y tener el prefijo `profile.` para que se asignen correctamente. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parámetro reservado utilizado para la característica de afinidad de categoría de Target, que debe pasarse como parte del objeto `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>O<br> `xdm.productListItems[0].SKU` | Los ID de entidad se utilizan para los contadores de comportamiento de Target Recommendations. Estos identificadores de entidad se pueden pasar como parte del objeto `data` o asignarse automáticamente a partir del primer elemento de la matriz `xdm.productListItems` si su implementación utiliza ese grupo de campos. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Los identificadores de categoría de entidad se pueden pasar como parte del objeto `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Los parámetros de entidad personalizados se utilizan para actualizar el catálogo de productos de Recommendations. Estos parámetros personalizados deben pasarse como parte del objeto `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Se utiliza para los algoritmos de recomendaciones de Target basados en el carro de compras. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Se utiliza para evitar que se devuelvan ID de entidad específicos en un diseño de recomendaciones. |
| `mbox3rdPartyId` | Establecer en el objeto `xdm.identityMap` | Se utiliza para sincronizar perfiles de Target entre dispositivos y Atributos del cliente. El área de nombres que se va a usar para el ID de cliente debe especificarse en la configuración de [Target del conjunto de datos](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Se utiliza para identificar un pedido único para el seguimiento de conversión de Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Se utiliza para rastrear los totales de pedidos de los objetivos de optimización y conversión de Target. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>O<br> `xdm.productListItems[0-n].SKU` | Se utiliza para los algoritmos de seguimiento de conversión de Target y de recomendaciones. Consulte la sección [parámetros de entidad](#entity-parameters) más abajo para obtener detalles. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Se usa para la meta de actividad [puntuación personalizada](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}

## Parámetros personalizados

Los parámetros de mbox personalizados deben pasarse como XDM o utilizando el objeto de datos con el comando `sendEvent`. Es importante asegurarse de que el esquema XDM incluya todos los campos necesarios para la implementación de Target.


## Parámetros de perfil

Se deben pasar los parámetros de perfil de destino...

## Parámetros de entidad

Los parámetros de entidad se utilizan para pasar datos de comportamiento e información de catálogo suplementaria para Target Recommendations. Todos los [parámetros de entidad](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) admitidos por at.js también son compatibles con el SDK web de Platform. De forma similar a los parámetros de perfil, todos los parámetros de entidad deben pasarse bajo el objeto `data.__adobe.target` en la carga del comando `sendEvent` del SDK web de Platform.

Los parámetros de entidad para un elemento específico deben tener el prefijo `entity.` para que la captura de datos sea correcta. Los parámetros reservados `cartIds` y `excludedIds` para los algoritmos de Recommendations no deben tener un prefijo y el valor de cada uno debe contener una lista separada por comas de los identificadores de entidad.



## Parámetros de compra

Los parámetros de compra se pasan en una página de confirmación de pedido después de un pedido correcto y se utilizan para los objetivos de conversión y optimización de Target. Con una implementación del SDK de Platform Mobile que utiliza la extensión Optimize, estos parámetros y se asignan automáticamente a partir de los datos XDM pasados como parte del grupo de campos `commerce`.


La información de compra se pasa a Target cuando el grupo de campos `commerce` tiene `purchases.value` establecido en `1`. El id. de pedido y el total del pedido se asignan automáticamente desde el objeto `order`. Si la matriz `productListItems` está presente, los valores `SKU` se utilizan para `productPurchasedId`.


## ID del cliente (mbox3rdPartyId)

Target permite la sincronización de perfiles entre dispositivos y sistemas mediante un único ID de cliente.



A continuación, aprenda a [rastrear eventos de conversión de Target](track-events.md) con el SDK web de Platform.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Optimize. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
