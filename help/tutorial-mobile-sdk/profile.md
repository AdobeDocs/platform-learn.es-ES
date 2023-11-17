---
title: Perfil
description: Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 2%

---

# Perfil

Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.

>[!INFO]
>
> Este tutorial se reemplazará con un nuevo tutorial con una nueva aplicación móvil de ejemplo a finales de noviembre de 2023

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

1. Navegue hasta `Cart.swift`

1. Agregue el siguiente código a la `processOrder() `función.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Es posible que el equipo de personalización también desee segmentar según el nivel de lealtad del usuario. Vamos a configurarlo en la aplicación de Luma.

1. Navegue hasta `Account.swift`

1. Agregue el siguiente código a la `showUserInfo()` función.

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Adicional `updateUserAttributes` se puede encontrar la documentación [aquí](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Obtenga

Una vez que haya actualizado el atributo de un usuario, estará disponible para otros SDK de Adobe, pero también puede recuperar atributos explícitamente.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Adicional `getUserAttributes` se puede encontrar la documentación [aquí](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md) sección.
1. Instale la aplicación.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. Seleccione el icono Cuenta y, a continuación, Iniciar sesión. Nota: no ha proporcionado ninguna credencial.
1. Cierre los menús de inicio de sesión y, a continuación, vuelva a seleccionar el icono Cuenta. Esto le lleva a la pantalla de detalles de la cuenta, donde `loyaltyLevel` está configurado.
1. Debería ver una **[!UICONTROL UserProfileUpdate]** en la interfaz de usuario de Assurance con el evento actualizado `profileMap` valor.
   ![validar perfil](assets/mobile-profile-validate.png)

Siguiente: **[Asignación de datos a Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)