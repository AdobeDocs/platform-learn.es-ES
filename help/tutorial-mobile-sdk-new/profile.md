---
title: Perfil
description: Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Perfil

Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.

Puede utilizar la extensión de perfil para almacenar atributos sobre el usuario en el cliente. Esta información se puede utilizar posteriormente para dirigir y personalizar mensajes durante escenarios en línea o sin conexión, sin tener que conectarse a un servidor para obtener un rendimiento óptimo. La extensión de perfil administra el perfil de operación del lado del cliente (CSOP), proporciona una forma de reaccionar a las API, actualiza los atributos del perfil de usuario y comparte los atributos del perfil de usuario con el resto del sistema como un evento generado.

Otras extensiones utilizan los datos del perfil para realizar acciones relacionadas con el perfil. Un ejemplo es la extensión del motor de reglas, que consume los datos del perfil y ejecuta reglas basadas en los datos del perfil. Obtenga más información acerca de [Extensión de perfil](https://developer.adobe.com/client-sdks/documentation/profile/) en la documentación de

>[!IMPORTANT]
>
>La funcionalidad de perfil que se describe en esta lección es independiente de la funcionalidad de perfil del cliente en tiempo real de las aplicaciones basadas en Adobe Experience Platform y en Platform.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Se ha importado el SDK de perfil.

  ```swift
  import AEPUserProfile
  ```

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Establecer o actualizar atributos de usuario.
* Recuperar atributos de usuario.


## Configurar y actualizar

Sería útil que, al segmentar o personalizar, se supiera rápidamente si un usuario ya había realizado alguna compra en la aplicación anteriormente. Vamos a configurarlo en la aplicación de Luma.

1. Vaya a **[!UICONTROL ProductView]** (en **[!UICONTROL Vistas]** > **[!UICONTROL Productos]**) en el proyecto de aplicación de Xcode Luma y busque la llamada a `updateUserAttributes` (en el botón Compras ):

   ```swift {highlight="8-9"}
   Button {
       Task {
           if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send purchase commerce experience event
               MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
               // Update attributes
               MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
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

2. Vaya a **[!UICONTROL MobileSDK]** y busque el `updateUserAttributes` función. Añada el siguiente código resaltado:

   ```swift {highlight="2-4"}
   func updateUserAttributes(attributeName: String, attributeValue: String) {
       var profileMap = [String: Any]()
       profileMap[attributeName] = attributeValue
       UserProfile.updateUserAttributes(attributeDict: profileMap)
   }
   ```

   Este código:

   1. Establece un diccionario vacío denominado `profileMap`.

   1. Agrega un elemento al diccionario mediante `attributeName` (por ejemplo, `isPaidUser`), y `attributeValue` (por ejemplo, `yes`).

   1. Utiliza el `profileMap` como valor del diccionario de `attributeDict` parámetro del `UserProfile.updateUserAttributes` Llamada de API.


Adicional `updateUserAttributes` se puede encontrar la documentación [aquí](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Obtenga

Una vez que haya actualizado el atributo de un usuario, estará disponible para otros SDK de Adobe, pero también podrá recuperar atributos explícitamente.

1. Vaya a **[!UICONTROL HomeView]** (en **[!UICONTROL Vistas]** > **[!UICONTROL General]**) y busque la `.onAppear` modificador. Añada el siguiente código:

   ```swift {highlight="3-11"}
   .onAppear {
       // Track view screen
       MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: home")
       // Get attributes
       UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
           if attributes?["isPaidUser"] as! String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Este código:

   1. Llama al `UserProfile.getUserAttributes` cierre con el `iPaidUser` nombre del atributo como elemento único en el `attributeNames` matriz.
   1. Entonces comprueba el valor del `isPaidUser` atributo y cuándo `yes`, coloca un distintivo en el icono Persona en la parte superior derecha.

Adicional `getUserAttributes` se puede encontrar la documentación [aquí](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md) sección.
1. Instale la aplicación.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. Ejecute la aplicación para iniciar sesión e interactuar con un producto.

   1. Mueva el icono Garantía a la izquierda.
   1. Seleccionar **[!UICONTROL Inicio]** en la barra de pestañas.
   1. Para abrir la hoja Inicio de sesión, seleccione **[!UICONTROL Iniciar sesión]** botón.
   1. Para insertar un correo electrónico y un ID de cliente aleatorios, seleccione la **[!UICONTROL A|]** botón .
   1. Seleccionar **[!UICONTROL Iniciar sesión]**.
   1. Seleccionar **[!UICONTROL Productos]** en la barra de pestañas.
   1. Seleccione un producto.
   1. Seleccionar **[!UICONTROL Guardar para más tarde]**.
   1. Seleccionar **[!UICONTROL Añadir al carro]**.
   1. Seleccionar **[!UICONTROL Comprar]**.
   1. Volver atrás a **[!UICONTROL Inicio]** pantalla. Debería ver un botón de inicio de sesión actualizado.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200"> <img src="./assets/personbadges.png" width="200">

1. Debería ver una **[!UICONTROL UserProfileUpdate]** y **[!UICONTROL getUserAttributes]** eventos en la interfaz de usuario de Assurance con el `profileMap` valor.
   ![validar perfil](assets/profile-validate.png)

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para actualizar los atributos de los perfiles de la red perimetral y (cuando está configurada) con Adobe Experience Platform.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Asignación de datos a Adobe Analytics](analytics.md)**
