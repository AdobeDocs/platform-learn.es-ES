---
title: Identidad
description: Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 4%

---

# Identidad

Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y sus comportamientos al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real. Los campos de identidad y los espacios de nombres son el pegamento que une diferentes fuentes de datos para crear el perfil de cliente en tiempo real de 360 grados.

Obtenga más información sobre [Extensión de identidad](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) y [servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=es) en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección:

* Actualizar una identidad estándar.
* Configure una identidad personalizada.
* Actualizar una identidad personalizada.
* Valide el gráfico de identidad.
* Obtenga ECID y otras identidades.

## Actualizar una identidad estándar

Comience por actualizar el mapa de identidad del usuario cuando inicie sesión.

1. Vaya a `Login.swift` si la aplicación de Luma y encuentra la función llamada `loginButt`.

   En la aplicación de ejemplo de Luma, no hay validación de nombre de usuario ni contraseña. Basta con pulsar los botones para &quot;iniciar sesión&quot;.

1. Cree la variable `IdentityMap` y `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. Agregue la variable `IdentityItem` a `IdentityMap`

   ```swift
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   ```

1. La llamada `updateIdentities` para enviar los datos a Platform Edge Network.

   ```swift
   Identity.updateIdentities(with: identityMap)
   ```

>[!NOTE]
>
>Puede enviar varias identidades en una sola llamada a updateIdentities . También puede modificar las identidades enviadas anteriormente.


## Configuración de un área de nombres de identidad personalizada

Las áreas de nombres de identidad son componentes de [Servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en) que sirven de indicadores del contexto al que se refiere una identidad. Por ejemplo, distinguen un valor de &quot;name@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID de CRM numérico.

1. En la interfaz de recopilación de datos, seleccione **[!UICONTROL Identidades]** desde la navegación del carril izquierdo.
1. Select **[!UICONTROL Crear área de nombres de identidad]**.
1. Proporcione un **[!UICONTROL Nombre para mostrar]** de `Luma CRM ID` y **[!UICONTROL Símbolo de identidad]** valor de `lumaCrmId`.
1. Select **[!UICONTROL ID entre dispositivos]**.
1. Seleccione **[!UICONTROL Crear]**.

![crear área de nombres de identidad](assets/mobile-identity-create.png)

## Actualizar una identidad personalizada

Ahora que ha creado una identidad personalizada, comience a recopilarla modificando la variable `updateIdentities` código que agregó en el paso anterior. Simplemente creando un elemento de identidad y agregándolo al mapa de identidad. Este es el aspecto que debería tener el bloque de código completo:

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

## Eliminar una identidad

Puede usar `removeIdentity` para eliminar la identidad del mapa de identidad del lado del cliente almacenado. La extensión de identidad deja de enviar el identificador a la red perimetral. El uso de esta API no elimina el identificador del gráfico de perfil de usuario o del gráfico de identidad del lado del servidor.

Agregue lo siguiente `removeIdentity` para acceder al botón de cierre de sesión, haga clic en `Account.swift`.

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
>En los ejemplos anteriores, `crmId` y `emailAddress` están codificados pero en una aplicación real los valores serían dinámicos.

## Validar con Assurance

1. Consulte la [instrucciones de configuración](assurance.md) y conecte su simulador o dispositivo a Assurance.
1. En la aplicación, seleccione el icono Cuenta en la parte inferior derecha.

   ![cuenta de aplicación de luma](assets/mobile-identity-login.png)
1. Seleccione el **Iniciar sesión** botón.
1. Se le presenta la opción de introducir un nombre de usuario y una contraseña, ambos son opcionales y simplemente puede seleccionar **Iniciar sesión**.

   ![inicio de sesión en la aplicación luma](assets/mobile-identity-login-final.png)
1. Busque en la interfaz de usuario web de Assurance la `Edge Identity Update Identities` del evento `com.adobe.griffon.mobile` proveedor.
1. Seleccione el evento y revise los datos en el `ACPExtensionEventData` objeto. Debería ver las identidades que ha actualizado.
   ![validación de la actualización de identidades](assets/mobile-identity-validate-assurance.png)

## Validar con gráfico de identidad

Una vez completados los pasos de la sección [lección de Experience Platform](platform.md), también podrá confirmar la captura de identidades en el visor de gráficos de identidad de Plataformas:

![validar gráfico de identidad](assets/mobile-identity-validate.png)


Siguiente: **[Perfil](profile.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)