---
title: Perfil
description: Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# Perfil

Obtenga información sobre cómo recopilar datos de perfil en una aplicación móvil.

Puede utilizar la extensión de perfil para almacenar atributos sobre el usuario en el cliente. Esta información se puede utilizar más adelante para dirigir y personalizar mensajes durante situaciones en línea o sin conexión, sin tener que conectarse a un servidor para obtener un rendimiento óptimo. La extensión de perfil administra el perfil de operación del lado del cliente (CSOP), proporciona una forma de reaccionar a las API, actualiza los atributos del perfil del usuario y comparte los atributos del perfil del usuario con el resto del sistema como un evento generado.

Otras extensiones utilizan los datos de perfil para realizar acciones relacionadas con perfiles. Un ejemplo es la extensión del motor de reglas que consume los datos de perfil y ejecuta reglas basadas en los datos de perfil. Obtenga más información sobre [Extensión de perfil](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) en la documentación

>[!IMPORTANT]
>
>La funcionalidad Perfil descrita en esta lección es independiente de la funcionalidad Perfil del cliente en tiempo real de las aplicaciones basadas en Adobe Experience Platform y en Platform.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con SDK instalados y configurados.
* Se ha importado el SDK de perfil.

   ```swift
   import AEPUserProfile
   ```

## Objetivos de aprendizaje

En esta lección:

* Establezca o actualice los atributos de usuario.
* Recupere atributos de usuario.


## Establecer y actualizar

Sería útil para la segmentación o personalización saber rápidamente si un usuario ha realizado compras en la aplicación anteriormente. Vamos a configurar eso en la aplicación Luma.

1. Vaya a `Cart.swift`

1. Agregue el código siguiente al `processOrder() `función.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Es posible que el equipo de personalización también desee segmentar según el nivel de lealtad del usuario. Vamos a configurar eso en la aplicación Luma.

1. Vaya a `Account.swift`

1. Agregue el código siguiente al `showUserInfo()` función.

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Adicional `updateUserAttributes` se puede encontrar documentación [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#update-user-attributes).

## Obtenga

Una vez que haya actualizado el atributo de un usuario, estará disponible para otros SDK de Adobe, pero también puede recuperar atributos explícitamente.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Adicional `getUserAttributes` se puede encontrar documentación [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#get-user-attributes).

## Validar con Assurance

1. Consulte la [instrucciones de configuración](assurance.md) para obtener más información.
1. Instale la aplicación.
1. Inicie la aplicación con la URL generada por Assurance.
1. Seleccione el icono Cuenta y, a continuación, Inicio de sesión. Nota: no tiene credenciales proporcionadas.
1. Cierre los menús de inicio de sesión y, a continuación, seleccione de nuevo el icono Cuenta . Esto le lleva a la pantalla de detalles de la cuenta donde `loyaltyLevel` está configurado.
1. Debería ver un **[!UICONTROL UserProfileUpdate]** en la interfaz de usuario de Assurance con la actualización `profileMap` valor.
   ![validar perfil](assets/mobile-profile-validate.png)

Siguiente: **[Asignación de datos a Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)