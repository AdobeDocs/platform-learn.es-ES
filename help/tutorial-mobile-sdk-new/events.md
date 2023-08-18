---
title: Eventos
description: Obtenga información sobre cómo recopilar datos de eventos en una aplicación móvil.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# Eventos

Obtenga información sobre cómo rastrear eventos en una aplicación móvil.

La extensión de red perimetral proporciona una API para enviar eventos de experiencia a Platform Edge Network. Un evento de experiencia es un objeto que contiene datos que se ajustan a la definición de esquema XDM ExperienceEvent. De forma más sencilla, capturan lo que las personas hacen en su aplicación móvil. Una vez que Platform Edge Network recibe los datos, se pueden reenviar a aplicaciones y servicios configurados en el conjunto de datos, como Adobe Analytics y Experience Platform. Obtenga más información acerca de [Eventos de experiencia](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) en la documentación del producto.

## Requisitos previos

* Todas las dependencias de paquetes en su lugar en el proyecto Xcode.
* Extensiones registradas en AppDelegate.
* MobileCore configurado para utilizar su appId de desarrollo.
* SDK importados.
* La aplicación se ha creado y ejecutado correctamente con los cambios anteriores.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

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

  ```swift {highlight="2-8"}
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
   * `commerce.productViews.value`: proporcione el valor numérico del evento. Si es booleano (o &quot;contador&quot; en Adobe Analytics), el valor siempre se establece en 1. Si es un evento numérico o de moneda, el valor puede ser > 1.

* En el esquema, identifique cualquier dato adicional asociado con el evento de vista de producto de comercio. En este ejemplo, incluya `productListItems` que es un conjunto estándar de campos utilizados con cualquier evento relacionado con el comercio:

  ![esquema de elementos de lista de productos](assets/datacollection-prodListItems-schema.png)
   * Observe que `productListItems` es una matriz para poder proporcionar varios productos.

* Para agregar estos datos, expanda su `xdmData` objeto para incluir datos suplementarios:

```swift {highlight="9-16"}
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

* A continuación, utilice la estructura de datos para crear un `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* Y envíe el evento y los datos a Platform Edge Network mediante la API sendEvent:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Ahora, vamos a implementar este código en su proyecto Xcode.
Tiene diferentes acciones comerciales relacionadas con productos (ver, agregar al carro, guardar para más tarde, comprar) en la aplicación y desea enviar eventos basados en estas acciones según lo realizado por el usuario.

1. Para estructurar el envío de eventos de experiencia, vaya a `MobileSDK`y agregue lo siguiente a `sendCommerceExperienceEvent` función. Esta función toma el evento de experiencia de comercio y el producto como parámetros:

   ```swift {highlight="2-22"}
   func sendCommerceExperienceEvent(commerceEventType: String, product: Product) {
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
   
     Logger.viewCycle.info("About to send commerce experience event of type  \(commerceEventType)..."
     let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   }
   ```

1. Entrada `ProductView` agregar varias llamadas a `sendCommerceExperienceEvent` función:

   1. En el `.task` modificador en el `ATTrackingManager.trackingAuthorizationStatus` cierre. El `.task` se llama al modificador cuando se inicializa y se muestra la vista de producto, por lo que desea enviar un evento de vista de producto en ese momento específico.

      ```swift {highlight="4-5"}
      .task {
          if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send commerce experience event
              MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
          }
      }
      ```

   1. Para cada uno de los botones (Guardado para más adelante, Añadir al carro y Comprar) de la barra de herramientas, disponible en la Vista de producto, agregue la llamada correspondiente.

      * Guardar para más tarde / Añadir a la lista de deseos:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                // Send saveForLater commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
                }
            }
            showSaveForLaterDialog.toggle()
        } label: {
            Label("", systemImage: "heart")
        }
        .alert(isPresented: $showSaveForLaterDialog, content: {
            Alert(title: Text( "Saved for later"), message: Text("The selected item is saved to your wishlist…"))
        })
        ```

      * Para Agregar Al Carro:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send productListAdds commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
                }
            }
            showAddToCartDialog.toggle()
        } label: {
                Label("", systemImage: "cart.badge.plus")
        }
        alert(isPresented: $showAddToCartDialog, content: {
            Alert(title: Text( "Added to basket"), message: Text("The selected item is added to your basket…"))
        })
        ```

      * Para la compra:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send purchase commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
                }
            }
            showPurchaseDialog.toggle()
        } label: {
            Label("", systemImage: "creditcard")
        }
        .alert(isPresented: $showPurchaseDialog, content: {
            Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
        })
        ```

### Grupos de campos personalizados

Imagine que desea rastrear las vistas de pantalla y las interacciones en la propia aplicación. Recuerde que ha definido un grupo de campos personalizados para este tipo de eventos.

* En el esquema, identifique los eventos que intenta recopilar.
  ![esquema de interacción de aplicación](assets/datacollection-appInteraction-schema.png)

* Empiece a construir el objeto.

  >[!NOTE]
  >
  >  Los grupos de campos estándar siempre comienzan en la raíz del objeto.
  >
  >  Los grupos de campos personalizados siempre comienzan con un objeto único de su organización de Experience Cloud, `_techmarketingdemos` en este ejemplo.

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


* A continuación, la estructura de datos para crear una `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Envíe el evento y los datos a Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


De nuevo, vamos a implementar este código en su proyecto Xcode.

1. Para mayor comodidad, puede definir dos funciones en `MobileSDK`.

   Uno para las interacciones entre aplicaciones. Añada el código resaltado a `sendAppInteractionEvent(actionName)` función en **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-16"}
   func sendAppInteractionEvent(actionName: String) {
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
   }
   ```

   Y uno para el seguimiento de pantalla. Añada el código resaltado en `sendTrackScreenEvent(stateName)` función en **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-17"}
   func sendTrackScreenEvent(stateName: String) {
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
   }
   ```

1. Vaya a **[!UICONTROL LoginSheet]**.

   * Agregue el siguiente código resaltado al cierre del botón Inicio de sesión:

     ```swift {highlight="3"}
     Button("Login") {                               
        // Send app interaction event
        MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
        dismiss()
     }
     .disabled(currentEmailId.isValidEmail == false)
     .buttonStyle(.bordered)
     ```

   * Agregue el siguiente código resaltado a `onAppear` modificador:

     ```swift {highlight="13"}
     .onAppear {
        Task {
            if currentEmailId == "testUser@gmail.com" || currentEmailId.isValidEmail == false {
                // still allow to log in
                disableLogin = false
            }
            else {
                disableLogin = true
            }
        }
        // Send track screen event
        MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
     }
     ```

### Validación

1. Revise la [instrucciones de configuración](assurance.md) y conecte el simulador o dispositivo a Assurance.
1. Ejecute la aplicación para iniciar sesión e interactuar con un producto.

   1. Mueva el icono Garantía a la izquierda.
   1. Seleccionar **[!UICONTROL Inicio]** en la barra de pestañas.
   1. Seleccione el **[!UICONTROL Iniciar sesión]** para abrir la hoja Inicio de sesión.
   1. Seleccione el **[!UICONTROL A|]** para insertar un correo electrónico aleatorio y un id de cliente.
   1. Seleccionar **[!UICONTROL Iniciar sesión]**.
   1. Seleccionar **[!UICONTROL Productos]** en la barra de pestañas.
   1. Seleccione un producto.
   1. Seleccionar **[!UICONTROL Guardar para más tarde]**.
   1. Seleccionar **[!UICONTROL Añadir al carro]**.
   1. Seleccionar **[!UICONTROL Comprar]**.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. Busque la variable **[!UICONTROL hitReceived]** eventos de la **[!UICONTROL com.adobe.edge.konductor]** proveedor.
1. Seleccione el evento y revise los datos XDM en la **[!UICONTROL messages]** objeto.
   ![validación de recopilación de datos](assets/datacollection-validation.png)


### Implementar en la aplicación de Luma

Ahora debe tener todas las herramientas para empezar a añadir recopilación de datos a la aplicación de Luma. Puede añadir más inteligencia a la forma en que el usuario interactúa con los productos y puede añadir más interacciones de aplicaciones y llamadas de seguimiento de pantalla a la aplicación:

* Implemente las funciones de pedido, cierre de compra, cesta vacía y otras a la aplicación, y agregue eventos de experiencia comercial relevantes a esta funcionalidad.
* Repita la llamada a `sendAppInteractionEvent` con el parámetro adecuado para rastrear otras interacciones de la aplicación en la aplicación por parte del usuario.
* Repita la llamada a `sendTrackScreenEvent` con el parámetro adecuado para rastrear cada pantalla vista por el usuario en la aplicación.

>[!TIP]
>
>Revise la [aplicación totalmente implementada](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) para ver más ejemplos.


## Envío de eventos a Analytics y Platform

Ahora que ha recopilado los eventos y los ha enviado a Platform Edge Network, se envían a las aplicaciones y servicios configurados en su [secuencia de datos](create-datastream.md). En lecciones posteriores, puede asignar estos datos a [Adobe Analytics](analytics.md) y [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para rastrear eventos de comercio, interacción de aplicaciones y seguimiento de pantalla en Adobe Experience Platform Edge Network y todos los servicios definidos en el flujo de datos.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[WebViews](web-views.md)**
