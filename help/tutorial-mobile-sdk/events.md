---
title: Eventos
description: Obtenga información sobre cómo recopilar datos de eventos en una aplicación móvil.
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Eventos

Obtenga información sobre cómo rastrear eventos en una aplicación móvil.

La extensión de red perimetral proporciona una API para enviar eventos de experiencia a la red perimetral de plataforma. Un evento de experiencia es un objeto que contiene datos que se ajustan a la definición del esquema XDM ExperienceEvent. Más simplemente, capturan lo que la gente hace en su aplicación móvil. Una vez que Platform Edge Network recibe los datos, estos se pueden reenviar a aplicaciones y servicios configurados en el conjunto de datos, como Adobe Analytics y Experience Platform. Obtenga más información sobre [Eventos de experiencias](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk) en la documentación del producto.

## Requisitos previos

* Se ha actualizado PodFile con los SDK necesarios.
* Extensiones registradas en AppDelegate.
* Se ha configurado MobileCore para que utilice su AppId de desarrollo.
* SDK importados.
* La aplicación se ha creado y ejecutado correctamente con los cambios anteriores.

## Objetivos de aprendizaje

En esta lección:

* Aprenda a estructurar los datos XDM basados en un esquema.
* Envíe un evento XDM basado en un grupo de campos estándar.
* Envíe un evento XDM basado en un grupo de campos personalizado.
* Envíe un evento de compra XDM.
* Valide con Assurance.

## Construcción de un evento de experiencia

La extensión Adobe Experience Platform Edge puede enviar eventos que siguen un esquema XDM definido anteriormente a Adobe Experience Platform Edge Network.

El proceso va así...

1. Identifique la interacción de la aplicación móvil que está intentando rastrear.

1. Revise el esquema e identifique el evento adecuado.

1. Revise el esquema e identifique cualquier campo adicional que deba utilizarse para describir el evento.

1. Construya y rellene el objeto de datos.

1. Crear y enviar evento.

1. Validación.

Veamos un par de ejemplos.

### Ejemplo 1: grupos de campos estándar

Revise el siguiente ejemplo sin intentar implementarlo en la aplicación de ejemplo:

1. En su esquema, identifique el evento que está intentando recopilar. En este ejemplo, estamos rastreando una vista de producto.
   ![esquema de vista de producto](assets/mobile-datacollection-prodView-schema.png)

1. Comience a construir el objeto:

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
       "commerce": [
           "productViews": [
           "value": 1
           ]
       ]
   ]
   ```

   * eventType: Describe el evento que se produjo y utilice un [valor conocido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) cuando sea posible.
   * commerce.productViews.value: Proporcione el valor numérico del evento. Si es booleano (o &quot;Contador&quot; en Adobe Analytics), el valor será siempre 1. Si es un evento numérico o de divisa, el valor puede ser > 1.

1. En el esquema, identifique los datos adicionales asociados al evento. En este ejemplo, incluya `productListItems` que es un conjunto estándar de campos utilizados con eventos relacionados con el comercio:
   ![esquema de elementos de la lista de productos](assets/mobile-datacollection-prodListItems-schema.png)
   * Observe que `productListItems` es una matriz para poder proporcionar varios productos.

1. Expanda el objeto xdmData para incluir datos adicionales:

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
           "commerce": [
           "productViews": [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name":  productName,
               "SKU": sku,
               "priceTotal": priceString,
               "quantity": 1
           ]
       ]
   ]
   ```

1. Utilice la estructura de datos para crear un `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Envíe el evento y los datos a Platform Edge Network:

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### Ejemplo 2: grupos de campos personalizados

Revise el siguiente ejemplo sin intentar implementarlo en la aplicación de ejemplo:

1. En el esquema, identifique el evento que está intentando recopilar. En este ejemplo, rastree una &quot;Interacción de aplicación&quot; que consiste en un evento y un nombre de Acción de aplicación.
   ![esquema de interacción de la aplicación](assets/mobile-datacollection-appInteraction-schema.png)

1. Empiece a construir el objeto.

   >[!NOTE]
   >
   >  Los grupos de campos estándar siempre comienzan en la raíz del objeto.
   >
   >  Los grupos de campos personalizados siempre comienzan bajo un objeto exclusivo de su organización Experience Cloud, &quot;_techmarketingdemos&quot; en este ejemplo.

   ```swift
   var xdmData: [String: Any] = [
   "_techmarketingdemos": [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
                   ]
               ]
           ]
       ]
   ]
   ```

   O alternativamente...

   ```swift
   var xdmData: [String: Any] = [:]
   xdmData["_techmarketingdemos"] = [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
               ]
           ]
       ]
   ]
   ```

1. Utilice la estructura de datos para crear un `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Envíe el evento y los datos a Platform Edge Network.

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### Añadir el seguimiento de vista de pantalla a la aplicación Luma

Es de esperar que los ejemplos anteriores hayan explicado el proceso de reflexión al construir un objeto de datos XDM. A continuación, agregaremos el seguimiento de vista de pantalla en la aplicación Luma.

1. Vaya a `Home.swift`.
1. Añada el siguiente código a `viewDidAppear(...)`.

   ```swift
           let stateName = "luma: content: ios: us: en: home"
           var xdmData: [String: Any] = [:]
           //Page View
           xdmData["_techmarketingdemos"] = [
               "appInformation": [
                   "appStateDetails": [
                       "screenType": "App",
                       "screenName": stateName,
                       "screenView": [
                           "value": 1
                       ]
                   ]
               ]
           ]
           let experienceEvent = ExperienceEvent(xdm: xdmData)
           Edge.sendEvent(experienceEvent: experienceEvent)
   ```

1. Repita el proceso para cada pantalla de la aplicación y actualice `stateName` a medida que vas.



### Validación

1. Consulte la [instrucciones de configuración](assurance.md) y conecte su simulador o dispositivo a Assurance.
1. Realice la acción y busque la variable `hitReceived` del evento `com.adobe.edge.konductor` proveedor.
1. Seleccione el evento y revise los datos XDM en la `messages` objeto.
   ![validación de recopilación de datos](assets/mobile-datacollection-validation.png)

### Ejemplo 3 - compra

En este ejemplo, suponga que el usuario realizó correctamente la siguiente compra:

* Producto #1 - Yoga Mat.
   * 49,99 $ x1
   * SKU: 5829
* Producto #2 - Botella de agua.
   * $10,00 x3
   * SKU: 9841
* Total de pedido: 79,99 $
* Id De Pedido Único: 298234720
* Tipo de pago: Tarjeta de crédito Visa
* Id. de transacción de pago único: 847361

#### Esquema

Estos son los campos de esquema relacionados para utilizar:

* eventType: &quot;commerce.purchases&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails (personalizado)

>[!TIP]
>
>Los grupos de campos personalizados siempre se colocan bajo el identificador de organización del Experience Cloud.
>
>&quot;_techmarketingdemos&quot; se sustituye por el valor único de su organización.

![esquema de compra](assets/mobile-datacollection-purchase-schema.png)


#### Código

Así es como construiría y enviaría el objeto XDM en la aplicación.

```swift
let stateName = "luma: content: ios: us: en: orderconfirmation"
let currencyCode = "USD"
let orderTotal = "79.99"
let paymentType = "Visa Credit Card"
let orderId = "298234720"
let paymentTransactionId = "847361"
var xdmData: [String: Any] = [
  "eventType": "commerce.purchases",
  "commerce": [
    "purchases": [
      "value": 1
    ],
    "order": [
      "currencyCode": currencyCode,
      "priceTotal": orderTotal,
      "purchaseID": orderId,
      "purchaseOrderNumber": orderId,
      "payments": [ //Assuming only 1 payment type is used
        [
          "currencyCode": currencyCode,
          "paymentAmount": orderTotal,
          "paymentType": paymentType,
          "transactionID": paymentTransactionId
        ]
      ]
    ]
  ],
  "productListItems": [
      [
          "name":  "Yoga Mat",
          "SKU": "5829",
          "priceTotal": "49.99",
          "quantity": 1
      ],
      [
        "name":  "Water Bottle",
        "SKU": "9841",
        "priceTotal": "30.00",
        "quantity": 3
      ]
  ]
]

//Custom field group
xdmData["_techmarketingdemos"] = [
  "appInformation": [
    "appStateDetails": [
      "screenType": "App",
      "screenName": stateName,
      "screenView": [
        "value": 1
      ]
    ]
  ]
]
let experienceEvent = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: experienceEvent)
```

>[!NOTE]
>
>Para una mayor claridad, todos los valores están codificados de forma rígida. En una situación real, los valores se rellenarían dinámicamente.


### Implementar en la aplicación de Luma

Debe tener todas las herramientas necesarias para empezar a agregar recopilación de datos a la aplicación de ejemplo de Luma. A continuación se muestra una lista de requisitos de seguimiento hipotéticos que puede seguir.

* Rastree cada vista de pantalla.
   * Campos de esquema: screenType, screenName, screenView
* Rastree las acciones que no sean de comercio.
   * Campos de esquema: appInteraction.name, appAction
* Acciones comerciales:
   * Página de productos: productViews
   * Agregar al carro de compras: productListAdd
   * Eliminar del carro de compras: productListRemovals
   * Iniciar cierre de compra: cierres de compra
   * Ver carro: productListViews
   * Agregar a la lista de deseos: saveForLaters
   * Compra: compras, pedido

>[!TIP]
>
>Consulte la [aplicación completamente implementada](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para ver más ejemplos.

### Validación

1. Consulte la [instrucciones de configuración](assurance.md) y conecte su simulador o dispositivo a Assurance.

1. Realice la acción y busque la variable `hitReceived` del evento `com.adobe.edge.konductor` proveedor.

1. Seleccione el evento y revise los datos XDM en la `messages` objeto.
   ![validación de recopilación de datos](assets/mobile-datacollection-validation.png)

## Envío de eventos a Analytics y Platform

Ahora que ha recopilado los eventos y los ha enviado a Platform Edge Network, se enviarán a las aplicaciones y servicios configurados en su [datastream](create-datastream.md). En lecciones posteriores, asignará estos datos a [Adobe Analytics](analytics.md) y [Adobe Experience Platform](platform.md).

Siguiente: **[WebViews](web-views.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)