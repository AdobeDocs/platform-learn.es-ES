---
title: Seguimiento de datos de eventos en aplicaciones móviles con el SDK móvil de Platform
description: Obtenga información sobre cómo rastrear datos de evento en una aplicación móvil.
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: afb15c561179386e7846e8cd8963f67820af09f1
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---

# Seguimiento de datos de eventos

Obtenga información sobre cómo rastrear eventos en una aplicación móvil.

La extensión de Edge Network proporciona una API para enviar eventos de experiencia al Edge Network de Platform. Un evento de experiencia es un objeto que contiene datos que se ajustan a la definición de esquema XDM ExperienceEvent. De forma más sencilla, capturan lo que las personas hacen en su aplicación móvil. Una vez que Platform Edge Network recibe los datos, se pueden reenviar a aplicaciones y servicios configurados en el conjunto de datos, como Adobe Analytics y Experience Platform. Obtenga más información acerca de [Eventos de experiencias](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) en la documentación del producto.

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

La extensión de Adobe Experience Platform Edge puede enviar eventos que siguen un esquema XDM definido anteriormente al Edge Network de Adobe Experience Platform.

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

  ![esquema de vista de producto](assets/datacollection-prodView-schema.png)

* Para construir un objeto que contenga los datos del evento de experiencia en la aplicación, utilice un código como el siguiente:

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

   * `eventType`: describe el evento que se produjo y usa un [valor conocido](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) siempre que sea posible.
   * `commerce.productViews.value`: valor numérico o booleano del evento. Si es booleano (o &quot;contador&quot; en Adobe Analytics), el valor siempre se establece en 1. Si es un evento numérico o de moneda, el valor puede ser > 1.

* En el esquema, identifique cualquier dato adicional asociado con el evento de vista de producto de comercio. En este ejemplo, incluya **[!UICONTROL productListItems]**, que es un conjunto estándar de campos utilizados con cualquier evento relacionado con el comercio:

  ![esquema de elementos de lista de productos](assets/datacollection-prodListItems-schema.png)
   * Observe que **[!UICONTROL productListItems]** es una matriz para que se puedan proporcionar varios productos.

* Para agregar estos datos, expanda el objeto `xdmData` para incluir datos adicionales:

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

* Ahora puede usar esta estructura de datos para crear un(a) `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* Y envíe el evento y los datos al Edge Network de Platform mediante la API `sendEvent`:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

La API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) es el SDK de AEP Mobile equivalente a las llamadas a la API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) y [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate). Consulte [Migrar de la extensión móvil de Analytics al Edge Network de Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) para obtener más información.

Ahora va a implementar realmente este código en su proyecto Xcode.
Tiene diferentes acciones comerciales relacionadas con productos en la aplicación y quiere enviar eventos, según estas acciones realizadas por el usuario:

* vista: se produce cuando un usuario ve un producto específico,
* añadir al carro: cuando un usuario pulse <img src="assets/addtocart.png" width="20"/> en una pantalla de detalles del producto,
* guardar para más tarde: cuando un usuario pulse <img src="assets/saveforlater.png" width="15"/> en una pantalla de detalles del producto,
* compra: cuando un usuario pulse <img src="assets/purchase.png" width="20"/> en una pantalla de detalles del producto.

Para implementar el envío de eventos de experiencia relacionados con el comercio de forma reutilizable, se utiliza una función dedicada:

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

   1. Para cada uno de los botones (<img src="assets/saveforlater.png" width="15"/>, <img src="assets/addtocart.png" width="20"/> y <img src="assets/purchase.png" width="20"/>) en la barra de herramientas, agregue la llamada relevante dentro del cierre `ATTrackingManager.trackingAuthorizationStatus == .authorized`:

      1. Para <img src="assets/saveforlater.png" width="15"/>

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Para <img src="assets/addtocart.png" width="20"/>

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Para <img src="assets/purchase.png" width="20"/>

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TIP]
>
>Si está desarrollando para Android™, utilice Map (`java.util.Map`) como interfaz base para construir la carga útil XDM.


### Grupos de campos personalizados

Imagine que desea rastrear las vistas de pantalla y las interacciones en la propia aplicación. Recuerde que ha definido un grupo de campos personalizados para este tipo de eventos.

* En el esquema, identifique los eventos que intenta recopilar.
  ![esquema de interacción de la aplicación](assets/datacollection-appInteraction-schema.png)

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


* Ahora puede usar esta estructura de datos para crear un(a) `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Envíe el evento y los datos de al Edge Network de Platform.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


De nuevo, vamos a implementar este código en su proyecto Xcode.

1. Para su comodidad, usted define dos funciones en **[!UICONTROL MobileSDK]**. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode.

   1. Uno para las interacciones entre aplicaciones. Agregue este código a la función `func sendAppInteractionEvent(actionName: String)`:

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


   1. Y uno para el seguimiento de pantalla. Agregue este código a la función `func sendTrackScreenEvent(stateName: String) `:

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

## Validación

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo con Assurance.

   1. Mueva el icono de Assurance a la izquierda.
   1. Seleccione **[!UICONTROL Inicio]** en la barra de pestañas y verifique que ve un **[!UICONTROL ECID]**, **[!UICONTROL correo electrónico]** y **[!UICONTROL ID de CRM]** en la pantalla Inicio.
   1. Seleccione **[!DNL Products]** en la barra de fichas.
   1. Seleccione un producto.
   1. Seleccionar <img src="assets/saveforlater.png" width="15"/>.
   1. Seleccionar <img src="assets/addtocart.png" width="20"/>.
   1. Seleccionar <img src="assets/purchase.png" width="15"/>.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. En la IU de Assurance, busque los eventos **[!UICONTROL hitReceived]** del proveedor **[!UICONTROL com.adobe.edge.konductor]**.
1. Seleccione el evento y revise los datos XDM en el objeto **[!UICONTROL messages]**. También puede usar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copiar evento sin procesar]** y usar un editor de texto o código de su preferencia para pegar e inspeccionar el evento.

   ![validación de recopilación de datos](assets/datacollection-validation.png)


## Pasos siguientes

Ahora debe tener todas las herramientas para empezar a añadir recopilación de datos a la aplicación. Puede añadir más inteligencia a la forma en que el usuario interactúa con sus productos en la aplicación y puede añadir más interacciones de la aplicación y llamadas de seguimiento de pantalla a la aplicación:

* Implemente las funciones de pedido, cierre de compra, cesta vacía y otras a la aplicación, y agregue eventos de experiencia comercial relevantes a esta funcionalidad.
* Repita la llamada a `sendAppInteractionEvent` con el parámetro correspondiente para rastrear otras interacciones de la aplicación por parte del usuario.
* Repita la llamada a `sendTrackScreenEvent` con el parámetro correspondiente para rastrear las pantallas que vio el usuario en la aplicación.

>[!TIP]
>
>Revise la [aplicación finalizada](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para ver más ejemplos.


## Envío de eventos a Analytics y Platform

Ahora que ha recopilado los eventos y los ha enviado al Edge Network de Platform, se envían a las aplicaciones y servicios configurados en su [secuencia de datos](create-datastream.md). En lecciones posteriores, asignará estos datos a [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md) y otras soluciones de Adobe Experience Cloud como [Adobe Target](target.md) y Adobe Journey Optimizer.

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para rastrear eventos de comercio, interacción de aplicaciones y seguimiento de pantalla al Edge Network de Adobe Experience Platform y a todos los servicios definidos en el conjunto de datos.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=es).

Siguiente: **[Administrar vistas web](web-views.md)**
