---
title: Seguimiento de datos de eventos en aplicaciones móviles con Experience Platform Mobile SDK
description: Obtenga información sobre cómo rastrear datos de evento en una aplicación móvil.
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: 4a0fa85c76c00fd505118692ea4b6cbe410f5839
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Seguimiento de datos de eventos

Obtenga información sobre cómo rastrear eventos en una aplicación móvil.

La extensión de Edge Network proporciona una API para enviar eventos de experiencia a Platform Edge Network. Un evento de experiencia es un objeto que contiene datos que se ajustan a la definición de esquema XDM ExperienceEvent. De forma más sencilla, estos eventos capturan lo que las personas hacen en la aplicación móvil. Una vez que Platform Edge Network ha recibido los datos, estos se pueden reenviar a aplicaciones y servicios configurados en el conjunto de datos, como Adobe Analytics y Experience Platform. Obtenga más información acerca de [Eventos de experiencias](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) en la documentación del producto.

## Requisitos previos

* Todas las dependencias del paquete se configuran en el proyecto Xcode.
* Extensiones registradas en **[!UICONTROL AppDelegate]**.
* Se ha configurado la extensión principal de Mobile para que utilice su desarrollo `appId`.
* SDK importados.
* La aplicación se creó y ejecutó correctamente con los cambios anteriores.

## Objetivos de aprendizaje

En esta lección, debe

* Obtenga información sobre cómo estructurar datos XDM basados en un esquema.
* Envíe un evento XDM basado en un grupo de campos estándar.
* Envíe un evento XDM basado en un grupo de campos personalizados.
* Envíe un evento de compra de XDM.
* Valide con Assurance.

## Creación de un evento de experiencia

La extensión de Adobe Experience Platform Edge puede enviar eventos que siguen un esquema XDM definido anteriormente a Adobe Experience Platform Edge Network.

El proceso es así...

1. Identifique la interacción de la aplicación móvil que esté intentando rastrear.

1. Revise el esquema e identifique el evento adecuado.

1. Revise el esquema e identifique cualquier campo adicional que deba utilizarse para describir el evento.

1. Construir y rellenar el objeto de datos.

1. Crear y enviar evento.

1. Validar.


### Grupos de campo estándar

Para los grupos de campos estándar, el proceso tiene este aspecto:

* En el esquema, identifique los eventos que está intentando recopilar. En este ejemplo, está realizando un seguimiento de eventos de experiencia comercial, por ejemplo un evento de vista de producto (**[!UICONTROL productViews]**).

  ![esquema de vista de producto](assets/datacollection-prodView-schema.png){zoomable="yes"}

* Para construir un objeto que contenga los datos del evento de experiencia en la aplicación, utilice un código como el siguiente:

>[!BEGINTABS]

>[!TAB iOS]

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

En este código:

* `eventType`: describe el evento que se produjo y usa un [valor conocido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) siempre que sea posible.

* `commerce.productViews.value`: valor numérico o booleano del evento. Si es booleano (o &quot;contador&quot; en Adobe Analytics), el valor siempre se establece en 1. Si es un evento numérico o de moneda, el valor puede ser > 1.

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    )
)
```

En este código:

* `eventType`: describe el evento que se produjo y usa un [valor conocido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) siempre que sea posible.

* `commerce.productViews.value`: valor numérico o booleano del evento. Si es booleano (o &quot;contador&quot; en Adobe Analytics), el valor siempre se establece en 1. Si es un evento numérico o de moneda, el valor puede ser > 1.

>[!ENDTABS]


* En el esquema, identifique cualquier dato adicional asociado con el evento de vista de producto de comercio. En este ejemplo, incluya **[!UICONTROL productListItems]**, que es un conjunto estándar de campos utilizados con cualquier evento relacionado con el comercio:

  ![esquema de elementos de lista de productos](assets/datacollection-prodListItems-schema.png){zoomable="yes"}
   * Observe que **[!UICONTROL productListItems]** es una matriz para que se puedan proporcionar varios productos.

* Para agregar estos datos, expanda el objeto `xdmData` para incluir datos adicionales:

>[!BEGINTABS]

>[!TAB iOS]

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

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    ),
    "productListItems" to mapOf(
        "name": productName,
        "SKU": sku,
        "priceTotal", priceString,
        "quantity", 1
    )
)
```

>[!ENDTABS]

* Ahora puede usar esta estructura de datos para crear un(a) `ExperienceEvent`:

>[!BEGINTABS]

>[!TAB iOS]

```swift
let productViewEvent = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val productViewEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
```

>[!ENDTABS]

* Y envíe el evento y los datos a Platform Edge Network mediante la API `sendEvent`:

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: productViewEvent)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(productViewEvent, null)
```

>[!ENDTABS]


La API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) es el SDK móvil de AEP equivalente a las llamadas a la API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) y [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate). Consulte [Migrar de la extensión móvil de Analytics a Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) para obtener más información.

Ahora va a implementar este código en su proyecto.
Tiene diferentes acciones comerciales relacionadas con productos en la aplicación y quiere enviar eventos, según estas acciones realizadas por el usuario:

* vista: se produce cuando un usuario ve un producto específico,
* añadir al carro: cuando un usuario pulsa ![Carro de compras](/help/assets/icons/ShoppingCart.svg) en una pantalla de detalles del producto,
* guardar para más tarde: cuando un usuario pulse ![Corazón](/help/assets/icons/Heart.svg) / ![Miniatura](/help/assets/icons/ThumbUp.svg) en una pantalla de detalles del producto,
* compra: cuando un usuario pulse ![CreditCard](/help/assets/icons/CreditCard.svg) en una pantalla de detalles del producto.

Para implementar el envío de eventos de experiencia relacionados con el comercio de forma reutilizable, se utiliza una función dedicada:

>[!BEGINTABS]

>[!TAB iOS]

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y agregue lo siguiente a la función `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name": product.name,
               "priceTotal": product.price,
               "SKU": product.sku
           ]
       ]
   ]
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   Esta función toma el tipo de evento de experiencia de comercio y el producto como parámetros y

   * configura la carga útil XDM como un diccionario, utilizando los parámetros de la función,
   * configura un evento de experiencia utilizando el diccionario,
   * envía el evento de experiencia mediante la API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** en el navegador del proyecto Xcode y agregue varias llamadas a la función `sendCommerceExperienceEvent`:

   1. En el modificador `.task`, dentro del cierre `ATTrackingManager.trackingAuthorizationStatus`. Se llama a este modificador `.task` cuando se inicializa y se muestra la vista de producto, por lo que desea enviar un evento de vista de producto en ese momento específico.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. Para cada uno de los botones (![Corazón](/help/assets/icons/Heart.svg), ![Carro de compras](/help/assets/icons/ShoppingCart.svg) y ![Tarjeta de crédito](/help/assets/icons/CreditCard.svg)) de la barra de herramientas, agregue la llamada correspondiente dentro del cierre de `ATTrackingManager.trackingAuthorizationStatus == .authorized`:

      1. Para ![Heart](/help/assets/icons/Heart.svg):

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Para ![ShoppingCart](/help/assets/icons/ShoppingCart.svg):

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Para ![CreditCard](/help/assets/icons/CreditCard.svg):

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio y agregue lo siguiente a la función `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

   ```kotlin
   // Set up a data map, create an experience event and send the event.
   val xdmData = mapOf(
       "eventType" to "commerce.$commerceEventType",
       "commerce" to mapOf(commerceEventType to mapOf("value" to 1)),
       "productListItems" to listOf(
           mapOf(
               "name" to product.name,
               "priceTotal" to product.price,
               "SKU" to product.sku
           )
       )
   )
   val commerceExperienceEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
   Edge.sendEvent(commerceExperienceEvent, null)
   ```

   Esta función toma el tipo de evento de experiencia de comercio y el producto como parámetros y

   * configura la carga útil XDM como un mapa, utilizando los parámetros de la función,
   * configura un evento de experiencia utilizando el mapa,
   * envía el evento de experiencia mediante la API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Vaya a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL ProductView.kt]** en el navegador de Android Studio y agregue varias llamadas a la función `sendCommerceExperienceEvent`:

   1. En la función maquetable `LaunchedEffect(Unit)`, desea enviar un evento de vista de producto en el momento específico en que se visualiza un producto.

      ```kotlin
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent("productViews", product)
      ```

   1. Para cada uno de los botones (![ThumbUp](/help/assets/icons/ThumbUp.svg), ![ShoppingCart](/help/assets/icons/ShoppingCart.svg) y ![CreditCard](/help/assets/icons/CreditCard.svg)) de la barra de herramientas, agregue la llamada correspondiente dentro del `scope.launch` de `if (MobileSDK.shared.trackingEnabled == TrackingStatus.AUTHORIZED)  statement`:

      1. Para ![ThumbUp](/help/assets/icons/ThumbUp.svg):

         ```kotlin
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("saveForLaters", product)
         ```

      1. Para ![ShoppingCart](/help/assets/icons/ShoppingCart.svg):

         ```kotlin
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("productListAdds", product)
         ```

      1. Para ![CreditCard](/help/assets/icons/CreditCard.svg):

         ```kotlin
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("purchases", product)
         ```

>[!ENDTABS]

>[!TIP]
>
>Si está desarrollando para Android™, utilice Map (`java.util.Map`) como interfaz base para construir la carga útil XDM.


### Grupos de campos personalizados

Imagine que desea rastrear las vistas de pantalla y las interacciones en la propia aplicación. Recuerde que ha definido un grupo de campos personalizados para este tipo de eventos.

* En el esquema, identifique los eventos que intenta recopilar.
  ![esquema de interacción de la aplicación](assets/datacollection-appInteraction-schema.png){zoomable="yes"}

* Empiece a construir el objeto.

  >[!NOTE]
  >
  >* Los grupos de campos estándar siempre comienzan en la raíz del objeto.
  >
  >* Los grupos de campos personalizados siempre comienzan con un objeto único de su organización de Experience Cloud, `_techmarketingdemos` en este ejemplo.

* Para el evento de interacción de la aplicación, construiría un objeto como:

>[!BEGINTABS]

>[!TAB iOS]

```swift
let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
    "appInformation": [
        "appInteraction": [
            "name": "login",
            "appAction": [
                "value": 1
                ]
            ]
        ]
    ]
]
```

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.interaction",
    "_techmarketingdemos" to mapOf(
        "appInformation" to mapOf(
            "appInteraction" to mapOf(
                "name" to "login",
                "appAction" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]

* Para el evento de seguimiento de pantalla, construiría un objeto como:

>[!BEGINTABS]

>[!TAB iOS]

```swift
var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                "screenName": "luma: content: ios: us: en: login",
                "screenView": [
                    "value": 1
                ]
            ]
        ] 
    ]
]
```

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.scene",
    tenant.value to mapOf(
        "appInformation" to mapOf(
            "appStateDetails" to mapOf(
                "screenType" to "App",
                "screenName" to stateName,
                "screenView" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]



* Ahora puede usar esta estructura de datos para crear un(a) `ExperienceEvent`.

>[!BEGINTABS]

>[!TAB iOS]

```swift
let event = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val event = ExperienceEvent(xdmData)
```

>[!ENDTABS]


* Envíe el evento y los datos a Platform Edge Network.

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: event)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(event, null)
```

>[!ENDTABS]

De nuevo, implemente este código en el proyecto.

>[!BEGINTABS]

>[!TAB iOS]

1. Para su comodidad, usted define dos funciones en **[!UICONTROL MobileSDK]**. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode.

   * Uno para las interacciones entre aplicaciones. Agregue este código a la función `func sendAppInteractionEvent(actionName: String)`:

     ```swift
     // Set up a data dictionary, create an experience event and send the event.
     let xdmData: [String: Any] = [
         "eventType": "application.interaction",
         tenant : [
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
     let appInteractionEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: appInteractionEvent)
     ```

     Esta función utiliza el nombre de la acción como parámetro y

      * configura la carga útil XDM como un diccionario, utilizando el parámetro de la función,
      * configura un evento de experiencia utilizando el diccionario,
      * envía el evento de experiencia mediante la API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   * Y uno para el seguimiento de pantalla. Agregue este código a la función `func sendTrackScreenEvent(stateName: String) `:

     ```swift
     // Set up a data dictionary, create an experience event and send the event.
     let xdmData: [String: Any] = [
         "eventType": "application.scene",
         tenant : [
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
     ]
     let trackScreenEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: trackScreenEvent)
     ```

     Esta función utiliza el nombre de estado como parámetro y

      * configura la carga útil XDM como un diccionario, utilizando el parámetro de la función,
      * configura un evento de experiencia utilizando el diccionario,
      * envía el evento de experiencia mediante la API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]**.

   1. Agregue el siguiente código resaltado al cierre del botón Inicio de sesión:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Agregue el siguiente código resaltado al modificador `onAppear`:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

>[!TAB Android]

1. Para su comodidad, usted define dos funciones en **[!UICONTROL MobileSDK]**. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio.

   * Uno para las interacciones entre aplicaciones. Agregue este código a la función `fun sendAppInteractionEvent(actionName: String)`:

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.interaction",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appInteraction" to mapOf(
                     "name" to actionName,
                     "appAction" to mapOf("value" to 1)
                 )
             )
         )
     )
     val appInteractionEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(appInteractionEvent, null)
     ```

     Esta función utiliza el nombre de la acción como parámetro y

      * configura la carga útil XDM como un mapa, utilizando el parámetro de la función,
      * configura un evento de experiencia utilizando el mapa,
      * envía el evento de experiencia mediante la API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   * Y uno para el seguimiento de pantalla. Agregue este código a la función `fun sendTrackScreenEvent(stateName: String)`:

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.scene",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appStateDetails" to mapOf(
                     "screenType" to "App",
                     "screenName" to stateName,
                     "screenView" to mapOf("value" to 1)
                 )
             )
         )
     )
     val trackScreenEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(trackScreenEvent, null)
     ```

     Esta función utiliza el nombre de estado como parámetro y

      * configura la carga útil XDM como un mapa, utilizando el parámetro de la función,
      * configura un evento de experiencia utilizando el mapa,
      * envía el evento de experiencia mediante la API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Vaya a **[!UICONTROL Android]** ![ChevronDown ](/help/assets/icons/ChevronDown.svg)**[!DNL app]**>**[!DNL kotlin+java]**>**[!DNL com.adobe.luma.tutorial.android]**>**[!UICONTROL &#x200B; views &#x200B;]**>**[!UICONTROL &#x200B; LoginSheet.kt &#x200B;]**

   1. Agregue el siguiente código resaltado al evento **[!UICONTROL Button]** **[!UICONTROL onClick]**:

      ```kotlin
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent("login")
      ```

   1. Agregue el siguiente código resaltado a la función maquetable `LaunchedEffect(Unit)`:

      ```kotlin
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent("luma: content: android: us: en: login")
      ```

>[!ENDTABS]



## Validación

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo con Assurance.

   1. Mueva el icono de Assurance a la izquierda.
   1. Seleccione **[!UICONTROL Inicio]** en la barra de pestañas y verifique que ve un **[!UICONTROL ECID]**, **[!UICONTROL correo electrónico]** y **[!UICONTROL ID de CRM]** en la pantalla Inicio.
   1. Seleccione **[!DNL Products]** en la barra de fichas.
   1. Seleccione un producto.
   1. Seleccione ![Corazón](/help/assets/icons/Heart.svg) (iOS) o ![Miniatura](/help/assets/icons/ThumbUp.svg) (Android).
   1. Seleccione ![ShoppingCartAdd](/help/assets/icons/ShoppingCart.svg).
   1. Seleccione ![CreditCard](/help/assets/icons/CreditCard.svg).

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/mobile-app-events-3.png" width="300">

>[!TAB Android]

<img src="./assets/mobile-app-events-3-android.png" width="278">

>[!ENDTABS]

1. En la IU de Assurance, busque los eventos **[!UICONTROL hitReceived]** del proveedor **[!UICONTROL com.adobe.edge.konductor]**.
1. Seleccione el evento y revise los datos XDM en el objeto **[!UICONTROL messages]**. También puede usar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copiar evento sin procesar]** y usar un editor de texto o código de su preferencia para pegar e inspeccionar el evento.

   ![validación de recopilación de datos](assets/datacollection-validation.png){zoomable="yes"}


## Próximos pasos

Ahora debe tener todas las herramientas para empezar a añadir recopilación de datos a la aplicación. Puede añadir más inteligencia a la forma en que el usuario interactúa con sus productos en la aplicación y puede añadir más interacciones de la aplicación y llamadas de seguimiento de pantalla a la aplicación:

* Implemente las funciones de pedido, cierre de compra, cesta vacía y otras a la aplicación, y agregue eventos de experiencia comercial relevantes a esta funcionalidad.
* Repita la llamada a `sendAppInteractionEvent` con el parámetro correspondiente para rastrear otras interacciones de la aplicación por parte del usuario.
* Repita la llamada a `sendTrackScreenEvent` con el parámetro correspondiente para rastrear las pantallas que vio el usuario en la aplicación.

>[!TIP]
>
>Revise la [aplicación finalizada](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para ver más ejemplos.


## Envío de eventos a Analytics y Platform

Ahora que ha recopilado los eventos y los ha enviado a Platform Edge Network, se envían a las aplicaciones y servicios configurados en su [secuencia de datos](create-datastream.md). En lecciones posteriores, asignará estos datos a [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md) y otras soluciones de Adobe Experience Cloud (como [Adobe Target](target.md) y Adobe Journey Optimizer).

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para rastrear eventos de comercio, interacción de aplicaciones y seguimiento de pantalla en Adobe Experience Platform Edge Network. Y a todos los servicios que haya definido en su conjunto de datos.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Administrar vistas web](web-views.md)**
