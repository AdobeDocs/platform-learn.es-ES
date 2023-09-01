---
title: Identidad
description: Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.
feature: Mobile SDK,Identities
hide: true
source-git-commit: 4101425bd97e271fa6cc15157a7be435c034e764
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 6%

---

# Identidad

Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y sus comportamientos al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real. Los campos de identidad y las áreas de nombres son el pegamento que une diferentes fuentes de datos para crear un perfil de cliente en tiempo real de 360 grados.

Obtenga más información acerca de [Extensión de identidad](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) y el [servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=es) en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Configure un área de nombres de identidad personalizada.
* Actualizar identidades.
* Valide el gráfico de identidad.
* Obtenga ECID y otras identidades.


## Configurar un área de nombres de identidad personalizada

Las áreas de nombres de identidad son componentes de [Servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=es) que sirven como indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de `name@email.com` como dirección de correo electrónico o `443522` como ID de CRM numérico.

1. En la interfaz de recopilación de datos, seleccione **[!UICONTROL Identidades]** desde el carril izquierdo.
1. Seleccione **[!UICONTROL Crear área de nombres de identidad]**.
1. Proporcione un **[!UICONTROL Nombre para mostrar]** de `Luma CRM ID` y un **[!UICONTROL Símbolo de identidad]** valor de `lumaCRMId`.
1. Seleccionar **[!UICONTROL ID entre dispositivos]**.
1. Seleccione **[!UICONTROL Crear]**.

   ![crear área de nombres de identidad](assets/identity-create.png)




## Actualización de identidades

Desea actualizar la identidad estándar (correo electrónico) y la identidad personalizada (ID de Luma CRM) cuando el usuario inicia sesión en la aplicación.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y busque la variable `func updateIdentities(emailAddress: String, crmId: String)` implementación de funciones. Agregue el siguiente código a la función.

   ```swift
   // Set up identity map
   let identityMap: IdentityMap = IdentityMap()
   
   // Add identity items to identity map
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   // Update identities
   Identity.updateIdentities(with: identityMap)
   ```

   Este código:

   1. Crea un vacío `IdentityMap` objeto.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Configuración de `IdentityItem` objetos para correo electrónico e ID de CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Añade estos `IdentityItem` objetos a la `IdentityMap` objeto.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Envía el `IdentityItem` objeto como parte de `Identity.updateIdentities` Llamada de API a la red perimetral.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. Vaya a **[!UICONTROL Luma]** **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL General]** > **[!UICONTROL LoginSheet]** en el navegador del proyecto Xcode y busque el código que se ejecutará al seleccionar el **[!UICONTROL Iniciar sesión]** botón. Añada el siguiente código:

   ```swift
   // call updaeIdentities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>Puede enviar varias identidades en una sola `updateIdentities` llamada. También puede modificar las identidades enviadas anteriormente.


## Eliminación de una identidad

Puede utilizar `removeIdentity` para eliminar la identidad del mapa de identidad del lado del cliente almacenado. La extensión de identidad deja de enviar el identificador a la red perimetral. El uso de esta API no elimina el identificador del gráfico de perfiles de usuario o del gráfico de identidad del lado del servidor.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL General]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y añada el siguiente código a `func removeIdentities(emailAddress: String, crmId: String)` función:

   ```swift
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   // reset email and CRM Id to their defaults
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL General]** > **[!UICONTROL LoginSheet]** en el navegador del proyecto Xcode y busque el código que se ejecutará al seleccionar el **[!UICONTROL Cerrar sesión]** botón. Añada el siguiente código:

   ```swift
   // call removeIdentities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
   dismiss()                   
   ```


## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md) y conecte el simulador o dispositivo a Assurance.
1. En la aplicación de Luma.
   1. Seleccione el **[!UICONTROL Inicio]** pestaña.
   1. Seleccione el <img src="assets/login.png" width="15" /> de la parte superior derecha.
   1. Proporcione una dirección de correo electrónico y un ID de CRM, o
   1. Seleccionar <img src="assets/insert.png" width="15" /> para generar de forma aleatoria una **[!UICONTROL Correo electrónico]** y **[!UICONTROL ID de CRM]**.
   1. Seleccionar **[!UICONTROL Iniciar sesión]**.

      <img src="./assets/identity1.png" width="300"> <img src="./assets/identity2.png" width="300">


1. Busque en la interfaz de usuario web de Assurance **[!UICONTROL Identidades de actualización de identidad de Edge]** evento de la **[!UICONTROL com.adobe.griffon.mobile]** proveedor.
1. Seleccione el evento y revise los datos en la **[!UICONTROL ACPExtensionEventData]** objeto. Debería ver las identidades que ha actualizado.
   ![validar actualización de identidades](assets/identity-validate-assurance.png)

## Validar con gráfico de identidad

Una vez completados los pasos en la [lección de Experience Platform](platform.md), puede confirmar la captura de identidad en el visualizador de gráficos de identidad de Plataformas:

1. Seleccionar **[!UICONTROL Identidades]** en la IU de recopilación de datos.
1. Seleccionar **[!UICONTROL Gráfico de identidad]** desde la barra superior.
1. Entrar `Luma CRM ID` como el **[!UICONTROL Área de nombres de identidad]** y su ID de CRM (por ejemplo, `24e620e255734d8489820e74f357b5c8`) como **[!UICONTROL Valor de identidad]**.
1. Verá el **[!UICONTROL Identidades]** enumerados.

   ![validar gráfico de identidad](assets/identity-validate-graph.png)


>[!SUCCESS]
>
>Ahora ha configurado la aplicación para actualizar identidades en la red perimetral y (cuando está configurada) con Adobe Experience Platform.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Perfil](profile.md)**
