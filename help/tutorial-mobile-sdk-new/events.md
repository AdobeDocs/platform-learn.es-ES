---
title: Eventos
description: Obtenga información sobre cómo recopilar datos de eventos en una aplicación móvil.
hide: true
source-git-commit: 371d71f06796c0f7825217a2ebd87d72ae7e8639
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 1%

---

# Eventos

Obtenga información sobre cómo rastrear eventos en una aplicación móvil.

La extensión de red perimetral proporciona una API para enviar eventos de experiencia a Platform Edge Network. Un evento de experiencia es un objeto que contiene datos que se ajustan a la definición de esquema XDM ExperienceEvent. De forma más sencilla, capturan lo que las personas hacen en su aplicación móvil. Una vez que Platform Edge Network recibe los datos, se pueden reenviar a aplicaciones y servicios configurados en el conjunto de datos, como Adobe Analytics y Experience Platform. Obtenga más información acerca de [Eventos de experiencia](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) en la documentación del producto.

## Requisitos previos

* Todas las dependencias del paquete se establecen en el proyecto Xcode.
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

La extensión de Edge de Adobe Experience Platform puede enviar eventos que siguen un esquema XDM definido anteriormente a Adobe Experience Platform Edge Network.

El proceso es así...

1. Identifique la interacción de la aplicación móvil que esté intentando rastrear.

1. Revise el esquema e identifique el evento adecuado.

1. Revise el esquema e identifique cualquier campo adicional que deba utilizarse para describir el evento.

1. Construir y rellenar el objeto de datos.

1. Crear y enviar evento.

1. Validación.


### Grupos de campo estándar

Para los grupos de campos estándar, el proceso tiene este aspecto:

* En el esquema, identifique los eventos que está intentando recopilar. En este ejemplo, se realiza un seguimiento de los eventos de experiencia comercial, por ejemplo una vista de producto (**[!UICONTROL productViews]**) evento.

  ![esquema de vista de producto](assets/datacollection-prodView-schema.png)

* Para construir un objeto que contenga los datos del evento de experiencia en la aplicación, utilice un código como el siguiente:

  ```swift
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "id": sku,
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: Describe el evento que se produjo, use un [valor conocido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) cuando sea posible.
   * `commerce.productViews.id`: un valor de cadena que representa el SKU del producto
   * `commerce.productViews.value`: el valor numérico o booleano del evento. Si es booleano (o &quot;contador&quot; en Adobe Analytics), el valor siempre se establece en 1. Si es un evento numérico o de moneda, el valor puede ser > 1.

* En el esquema, identifique cualquier dato adicional asociado con el evento de vista de producto de comercio. En este ejemplo, incluya **[!UICONTROL productListItem]** que es un conjunto estándar de campos utilizados con cualquier evento relacionado con el comercio:

  ![esquema de elementos de lista de productos](assets/datacollection-prodListItems-schema.png)
   * Observe que **[!UICONTROL productListItems]** es una matriz para poder proporcionar varios productos.

* Para agregar estos datos, expanda su `xdmData` objeto para incluir datos suplementarios:

```swift
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
        "commerce": [
        "productViews": [
            "id": sku,
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

* Ahora puede utilizar esta estructura de datos para crear un `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* Y envíe el evento y los datos a Platform Edge Network mediante el `sendEvent` API:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Ahora va a implementar realmente este código en su proyecto Xcode.
Tiene diferentes acciones comerciales relacionadas con productos en la aplicación y quiere enviar eventos, según estas acciones realizadas por el usuario:

* vista: se produce cuando un usuario ve un producto específico,
* añadir al carro: cuando un usuario pulse <img src="assets/addtocart.png" width="20" /> en una pantalla de detalles del producto,
* guardar para más tarde: cuando un usuario pulse <img src="assets/saveforlater.png" width="15" /> en una pantalla de detalles del producto,
* compra: cuando un usuario pulse <img src="assets/purchase.png" width="20" /> en una pantalla de detalles del producto.

Para implementar el envío de eventos de experiencia relacionados con el comercio de forma reutilizable, se utiliza una función dedicada:

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y añada lo siguiente a `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)` función.

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
               "id": product.sku,
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
   * envía el evento de experiencia utilizando [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL Productos]** > **[!UICONTROL ProductView]** en el navegador del proyecto Xcode y añada varias llamadas a `sendCommerceExperienceEvent` función:

   1. En el `.task` modificador, dentro de `ATTrackingManager.trackingAuthorizationStatus` cierre. Esta `.task` se llama al modificador cuando se inicializa y se muestra la vista de producto, por lo que desea enviar un evento de vista de producto en ese momento específico.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. Para cada uno de los botones (<img src="assets/saveforlater.png" width="15" />, <img src="assets/addtocart.png" width="20" /> y <img src="assets/purchase.png" width="20" />) en la barra de herramientas, añada la llamada correspondiente dentro de la variable `ATTrackingManager.trackingAuthorizationStatus == .authorized` cierre:

      1. Para  <img src="assets/saveforlater.png" width="15" />

         ```swift
         // Send saveForLaters commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Para  <img src="assets/addtocart.png" width="20" />

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Para  <img src="assets/purchase.png" width="20" />

         ```swift
         // Send purchases commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

### Grupos de campos personalizados

Imagine que desea rastrear las vistas de pantalla y las interacciones en la propia aplicación. Recuerde que ha definido un grupo de campos personalizados para este tipo de eventos.

* En el esquema, identifique los eventos que intenta recopilar.
  ![esquema de interacción de aplicación](assets/datacollection-appInteraction-schema.png)

* Empiece a construir el objeto.

  >[!NOTE]
  >
  >* Los grupos de campos estándar siempre comienzan en la raíz del objeto.
  >
  >* Los grupos de campos personalizados siempre comienzan con un objeto único de su organización de Experience Cloud, `_techmarketingdemos` en este ejemplo.

  Para el evento de interacción de la aplicación, construiría un objeto como:

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

  Para el evento de seguimiento de pantalla, construiría un objeto como:

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


* Ahora puede utilizar esta estructura de datos para crear un `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Envíe el evento y los datos a Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


De nuevo, vamos a implementar este código en su proyecto Xcode.

1. Para mayor comodidad, puede definir dos funciones en **[!UICONTROL MobileSDK]**. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode.

   1. Uno para las interacciones entre aplicaciones. Añada este código a `func sendAppInteractionEvent(actionName: String)` función:

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
      * envía el evento de experiencia utilizando [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.


   1. Y uno para el seguimiento de pantalla. Añada este código a `func sendTrackScreenEvent(stateName: String) ` función:

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
      * envía el evento de experiencia utilizando [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL General]** > **[!UICONTROL LoginSheet]**.

   1. Agregue el siguiente código resaltado al cierre del botón Inicio de sesión:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      dismiss()
      ```

   1. Agregue el siguiente código resaltado a `onAppear` modificador:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## Validación

1. Revise la [instrucciones de configuración](assurance.md) y conecte el simulador o dispositivo a Assurance.
1. Ejecute la aplicación, inicie sesión e interactúe con un producto.

   1. Mueva el icono Garantía a la izquierda.
   1. Seleccionar **[!UICONTROL Inicio]** en la barra de pestañas.
   1. Seleccione el <img src="assets/login.png" width="15" /> para abrir la hoja Inicio de sesión.

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. Seleccione el <img src="assets/insert.png" width="15" /> para insertar un correo electrónico aleatorio y un id de cliente.
   1. Seleccionar **[!UICONTROL Iniciar sesión]**.

      <img src="./assets/mobile-app-events-2.png" width="300">
   1. Seleccionar **[!UICONTROL Productos]** en la barra de pestañas.
   1. Seleccione un producto.
   1. Seleccionar <img src="assets/saveforlater.png" width="15" />.
   1. Seleccionar <img src="assets/addtocart.png" width="20" />.
   1. Seleccionar <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. En la interfaz de usuario de Assurance, busque **[!UICONTROL hitReceived]** eventos de la **[!UICONTROL com.adobe.edge.konductor]** proveedor.
1. Seleccione el evento y revise los datos XDM en la **[!UICONTROL messages]** objeto.
   ![validación de recopilación de datos](assets/datacollection-validation.png)


## Pasos siguientes

Ahora debe tener todas las herramientas para empezar a añadir recopilación de datos a la aplicación de Luma. Puede añadir más inteligencia a la forma en que el usuario interactúa con sus productos en la aplicación y puede añadir más interacciones de la aplicación y llamadas de seguimiento de pantalla a la aplicación:

* Implemente las funciones de pedido, cierre de compra, cesta vacía y otras a la aplicación, y agregue eventos de experiencia comercial relevantes a esta funcionalidad.
* Repita la llamada a `sendAppInteractionEvent` con el parámetro adecuado para rastrear otras interacciones de la aplicación por parte del usuario.
* Repita la llamada a `sendTrackScreenEvent` con el parámetro adecuado para hacer un seguimiento de las pantallas visualizadas por el usuario en la aplicación.

>[!TIP]
>
>Revise la [aplicación finalizada](https://git.corp.adobe.com/rmaur/Luma) para ver más ejemplos.


## Envío de eventos a Analytics y Platform

Ahora que ha recopilado los eventos y los ha enviado a Platform Edge Network, se envían a las aplicaciones y servicios configurados en su [secuencia de datos](create-datastream.md). En lecciones posteriores, puede asignar estos datos a [Adobe Analytics](analytics.md) y [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para rastrear eventos de comercio, interacción de aplicaciones y seguimiento de pantalla en Adobe Experience Platform Edge Network y todos los servicios definidos en el flujo de datos.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[WebViews](web-views.md)**
