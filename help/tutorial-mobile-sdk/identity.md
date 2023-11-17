---
title: Identidad
description: Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.
feature: Mobile SDK,Identities
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 4%

---

# Identidad

Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.

>[!INFO]
>
> Este tutorial se reemplazará con un nuevo tutorial con una nueva aplicación móvil de ejemplo a finales de noviembre de 2023

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y sus comportamientos al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real. Los campos de identidad y las áreas de nombres son el pegamento que une diferentes fuentes de datos para crear un perfil de cliente en tiempo real de 360 grados.

Obtenga más información acerca de [Extensión de identidad](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) y el [servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=es) en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Actualizar una identidad estándar.
* Configure una identidad personalizada.
* Actualizar una identidad personalizada.
* Valide el gráfico de identidad.
* Obtenga ECID y otras identidades.

## Actualización de una identidad estándar

Para empezar, actualice el mapa de identidad del usuario cuando inicie sesión.

1. Vaya a `Login.swift` si la aplicación de Luma y encuentra la función llamada a `loginButt`.

   En la aplicación de ejemplo de Luma no hay validación de nombre de usuario o contraseña. Simplemente pulse los botones para &quot;iniciar sesión&quot;.

1. Cree el `IdentityMap` y `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. Añada el `IdentityItem` a la `IdentityMap`

   ```swift
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   ```

1. Llamada `updateIdentities` para enviar los datos a Platform Edge Network.

   ```swift
   Identity.updateIdentities(with: identityMap)
   ```

>[!NOTE]
>
>Puede enviar varias identidades en una sola llamada updateIdentities. También puede modificar las identidades enviadas anteriormente.


## Configurar un área de nombres de identidad personalizada

Las áreas de nombres de identidad son componentes de [Servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=es) que sirven como indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de &quot;name@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID numérico de CRM.

1. En la interfaz de recopilación de datos, seleccione **[!UICONTROL Identidades]** desde el carril izquierdo.
1. Seleccione **[!UICONTROL Crear área de nombres de identidad]**.
1. Proporcione un **[!UICONTROL Nombre para mostrar]** de `Luma CRM ID` y un **[!UICONTROL Símbolo de identidad]** valor de `lumaCrmId`.
1. Seleccionar **[!UICONTROL ID entre dispositivos]**.
1. Seleccione **[!UICONTROL Crear]**.

![crear área de nombres de identidad](assets/mobile-identity-create.png)

## Actualización de una identidad personalizada

Ahora que ha creado una identidad personalizada, empiece a recopilarla modificando la `updateIdentities` código que agregó en el paso anterior. Basta con crear un elemento de identidad y agregarlo al mapa de identidad. Este es el aspecto que debería tener el bloque de código completo:

```swift
//Hardcoded identity values
let emailAddress = "testuser@gmail.com"
let crmId = "112ca06ed53d3db37e4cea49cc45b71e"

// Create identity map
let identityMap: IdentityMap = IdentityMap()
// Add email (standard)
let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item:emailIdentity, withNamespace: "Email")
// Add lumaCrmId (custom)
let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item: crmIdentity, withNamespace: "lumaCrmId")
// Update
Identity.updateIdentities(with: identityMap)
```

## Eliminación de una identidad

Puede utilizar `removeIdentity` para eliminar la identidad del mapa de identidad del lado del cliente almacenado. La extensión de identidad deja de enviar el identificador a la red perimetral. El uso de esta API no elimina el identificador del gráfico de perfiles de usuario o del gráfico de identidad del lado del servidor.

Añada lo siguiente `removeIdentity` código para el botón de cierre de sesión haga clic en `Account.swift`.

```swift
// Logout
let logout = UIAlertAction(title: "Logout", style: .destructive, handler: { (action) -> Void in
    isLoggedIn = false;
    ////Hardcoded identity values
    let emailAddress = "testuser@gmail.com"
    let crmId = "112ca06ed53d3db37e4cea49cc45b71e"
    // Adobe Experience Platform - Remove Identity
    Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
    Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCrmId")
})
```

>[!NOTE]
>En los ejemplos anteriores, `crmId` y `emailAddress` están codificados, pero en una aplicación real los valores serían dinámicos.

## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md) y conecte el simulador o dispositivo a Assurance.
1. En la aplicación, seleccione el icono Cuenta en la parte inferior derecha.

   ![cuenta de aplicación de luma](assets/mobile-identity-login.png)
1. Seleccione el **Iniciar sesión** botón.
1. Se le presenta la opción de introducir un nombre de usuario y una contraseña, ambos son opcionales y simplemente puede seleccionar **Iniciar sesión**.

   ![inicio de sesión en luma app](assets/mobile-identity-login-final.png)
1. Busque en la interfaz de usuario web de Assurance `Edge Identity Update Identities` evento de la `com.adobe.griffon.mobile` proveedor.
1. Seleccione el evento y revise los datos en la `ACPExtensionEventData` objeto. Debería ver las identidades que ha actualizado.
   ![validar actualización de identidades](assets/mobile-identity-validate-assurance.png)

## Validar con gráfico de identidad

Una vez completados los pasos en la [lección de Experience Platform](platform.md), también podrá confirmar la captura de identidad en el visualizador de gráficos de identidad de Plataformas:

![validar gráfico de identidad](assets/mobile-identity-validate.png)


Siguiente: **[Perfil](profile.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)