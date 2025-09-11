---
title: Recopilación de datos de perfil con Platform Mobile SDK
description: Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.
jira: KT-14634
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 49d8c53d2ba2f9dcecf2470d855ad22f44763f6f
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 2%

---

# Recopilación de datos de perfil

Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.

Puede utilizar la extensión de perfil para almacenar atributos sobre el usuario en el cliente. Esta información se puede utilizar posteriormente para dirigir y personalizar mensajes durante escenarios en línea o sin conexión, sin tener que conectarse a un servidor para obtener un rendimiento óptimo.

La extensión de perfil administra el perfil de operación del lado del cliente (CSOP), proporciona una forma de reaccionar a las API, actualiza los atributos del perfil de usuario y comparte los atributos del perfil de usuario con el resto del sistema como un evento generado.

Otras extensiones utilizan los datos del perfil para realizar acciones relacionadas con el perfil. Un ejemplo es la extensión del motor de reglas, que consume los datos del perfil y ejecuta reglas basadas en los datos del perfil. Obtenga más información acerca de la [extensión de perfil](https://developer.adobe.com/client-sdks/documentation/profile/) en la documentación

>[!IMPORTANT]
>
>La funcionalidad de perfil que se describe en esta lección es independiente de la funcionalidad de perfil del cliente en tiempo real de las aplicaciones basadas en Adobe Experience Platform y en Platform.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Establecer o actualizar atributos de usuario.
* Recuperar atributos de usuario.


## Establecer y actualizar atributos de usuario

Sería útil que los objetivos y la personalización de la aplicación supieran rápidamente si un usuario ha realizado una compra en el pasado o recientemente. Vamos a configurarlo en la aplicación de Luma.

>[!BEGINTABS]

>[!TAB iOS]

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** en el navegador del proyecto Xcode y busque la función `func updateUserAttribute(attributeName: String, attributeValue: String)`. Añada el siguiente código:

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Este código:

   1. Configura un diccionario vacío denominado `profileMap`.

   1. Agrega un elemento al diccionario utilizando `attributeName` (por ejemplo `isPaidUser`) y `attributeValue` (por ejemplo `yes`).

   1. Utiliza el diccionario `profileMap` como valor para el parámetro `attributeDict` de la llamada a la API [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** en el navegador del proyecto Xcode y busque la llamada a `updateUserAttributes` (dentro del código de las compras) <img src="assets/purchase.png" width="15" /> botón). Añada el siguiente código:

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```

>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio y busque la función `func updateUserAttribute(attributeName: String, attributeValue: String)`. Añada el siguiente código:

   ```kotlin
   // Create a profile map, add attributes to the map and update profile using the map
   val profileMap = mapOf(attributeName to attributeValue)
   UserProfile.updateUserAttributes(profileMap)
   ```

   Este código:

   1. Establece un mapa vacío denominado `profileMap`.

   1. Agrega un elemento al mapa mediante `attributeName` (por ejemplo `isPaidUser`) y `attributeValue` (por ejemplo `yes`).

   1. Utiliza la asignación `profileMap` como valor para el parámetro `attributeDict` de la llamada a la API [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL ProductView.kt]** y busque la llamada a `updateUserAttributes` (dentro del código de las Compras) <img src="assets/purchase.png" width="15" /> botón). Añada el siguiente código:

   ```kotlin
   // Update attributes
   MobileSDK.shared.updateUserAttribute("isPaidUser", "yes")
   ```

>[!ENDTABS]

## Obtener atributos de usuario

Una vez que haya actualizado el atributo de un usuario, estará disponible para otros SDK de Adobe, pero también podrá recuperar atributos explícitamente para permitir que la aplicación se comporte como desee.

>[!BEGINTABS]

>[!TAB iOS]

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** en el navegador del proyecto Xcode y busque el modificador `.onAppear`. Añada el siguiente código:

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?.count ?? 0 > 0 {
           if attributes?["isPaidUser"] as? String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Este código:

   1. Llama a la API [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) con el nombre de atributo `isPaidUser` como un solo elemento en la matriz `attributeNames`.
   1. Entonces comprueba el valor del atributo `isPaidUser` y, cuando `yes`, coloca un distintivo en la etiqueta Icono <img src="assets/paiduser.png" width="20"> en la barra de herramientas en la parte superior derecha.

>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.androi]** > **[!DNL views]** > **[!DNL HomeView.kt]** en el navegador de proyectos de Android Studio y busque el modificador `.onAppear`. Añada el siguiente código:

   ```kotlin
   // Get attributes
   UserProfile.getUserAttributes(listOf("isPaidUser")) { attributes ->
       showBadgeForUser = attributes?.get("isPaidUser") == "yes"
   }
   ```

   Este código:

   1. Llama a la API [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) con el nombre de atributo `isPaidUser` como un solo elemento en la matriz `attributeNames`.
   1. Entonces comprueba el valor del atributo `isPaidUser`. Cuando `yes`, el código reemplaza el icono de la persona con un distintivo en la etiqueta Icono <img src="assets/paiduser.png" width="20"> en la barra de herramientas en la parte superior derecha.

>[!ENDTABS]

Consulte la [referencia de API](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) para obtener más información.

## Validar con Assurance

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. Ejecute la aplicación para iniciar sesión e interactuar con un producto.

>[!BEGINTABS]

>[!TAB iOS]

1. Seleccione **[!UICONTROL Inicio]** en la barra de fichas.
1. Mueva el icono de Assurance a la izquierda.
1. Para abrir la hoja Inicio de sesión, seleccione Botón <img src="assets/login.png" width="15" />.

   <img src="./assets/mobile-app-events-1.png" width="300">

1. Para insertar un correo electrónico y un ID de cliente aleatorios, seleccione la Botón <img src="assets/insert.png" width="15" />
1. Seleccione **[!UICONTROL Iniciar sesión]**.

   <img src="./assets/mobile-app-events-2.png" width="300">

1. Seleccione **[!DNL Products]** en la barra de fichas.
1. Seleccione un producto.
1. Seleccionar <img src="assets/saveforlater.png" width="15" />.
1. Seleccionar <img src="assets/addtocart.png" width="20">.
1. Seleccionar <img src="assets/purchase.png" width="15" />.

   <img src="./assets/mobile-app-events-3.png" width="300">

1. Volver a la pantalla **[!UICONTROL Inicio]**. Debería ver que se ha añadido una insignia <img src="assets/person-badge-icon.png" width="15" />.

   <img src="./assets/personbadges.png" width="300">


>[!TAB Android]

1. Seleccione **[!UICONTROL Inicio]** en la barra de fichas.
1. Mueva el icono de Assurance a la izquierda.
1. Para abrir la hoja Inicio de sesión, seleccione Botón <img src="assets/login.png" width="15" />.

   <img src="./assets/mobile-app-events-1-android.png" width="300">

1. Para insertar un correo electrónico y un ID de cliente aleatorios, seleccione la Botón <img src="assets/insert.png" width="15" />
1. Seleccione **[!UICONTROL Iniciar sesión]**.

   <img src="./assets/mobile-app-events-2-android.png" width="300">

1. Seleccione **[!DNL Products]** en la barra de fichas.
1. Seleccione un producto.
1. Seleccionar<img src="assets/heart.png" width="25">.
1. Seleccionar <img src="assets/addtocart.png" width="20">.
1. Seleccionar <img src="assets/purchase.png" width="15" />.

   <img src="./assets/mobile-app-events-3-android.png" width="300">

1. Volver a la pantalla **[!UICONTROL Inicio]**. Debería ver que se ha actualizado el icono de la persona.

   <img src="./assets/personbadges-android.png" width="300">

>[!ENDTABS]


En la interfaz de usuario de Assurance, debería ver los eventos **[!UICONTROL UserProfileUpdate]** y **[!UICONTROL getUserAttributes]** con el valor `profileMap` actualizado.

![validar perfil](assets/profile-validate.png){zoomable="yes"}

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para actualizar los atributos de los perfiles en Edge Network y (cuando está configurada) con Adobe Experience Platform.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Usar lugares](places.md)**
