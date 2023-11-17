---
title: Recopilación de datos de identidad
description: Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.
feature: Mobile SDK,Identities
hide: true
exl-id: e6ec9a4f-3163-47fd-8d5c-6e640af3b4ba
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 5%

---

# Recopilación de datos de identidad

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

>[!NOTE]
>
>El SDK de Mobile genera una identidad única en su propia área de nombres, denominada ID de Experience Cloud (ECID) cuando se instala la aplicación. Este ECID se almacena en la memoria persistente del dispositivo móvil y se envía con cada visita. El ECID se elimina cuando el usuario desinstala la aplicación o cuando establece el estado de privacidad global del SDK móvil como de exclusión. En la aplicación de Luma de ejemplo, debe eliminar y reinstalar la aplicación para crear un nuevo perfil con su propio ECID único.


Para crear un área de nombres de identidad nueva:

1. En la interfaz de recopilación de datos, seleccione **[!UICONTROL Identidades]** desde el carril izquierdo.
1. Seleccione **[!UICONTROL Crear área de nombres de identidad]**.
1. Proporcione un **[!UICONTROL Nombre para mostrar]** de `Luma CRM ID` y un **[!UICONTROL Símbolo de identidad]** valor de `lumaCRMId`.
1. Seleccionar **[!UICONTROL ID entre dispositivos]**.
1. Seleccione **[!UICONTROL Crear]**.

   ![crear área de nombres de identidad](assets/identity-create.png)




## Actualización de identidades

Desea actualizar la identidad estándar (correo electrónico) y la identidad personalizada (ID de Luma CRM) cuando el usuario inicia sesión en la aplicación.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y busque la variable `func updateIdentities(emailAddress: String, crmId: String)` implementación de funciones. Agregue el siguiente código a la función.

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
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

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** en el navegador del proyecto Xcode y busque el código que se ejecutará al seleccionar el **[!UICONTROL Iniciar sesión]** botón. Añada el siguiente código:

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>Puede enviar varias identidades en una sola `updateIdentities` llamada. También puede modificar las identidades enviadas anteriormente.


## Eliminación de una identidad

Puede usar el complemento [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) API para eliminar la identidad del mapa de identidad del lado del cliente almacenado. La extensión de identidad deja de enviar el identificador a la red perimetral. El uso de esta API no elimina el identificador del gráfico de identidades del lado del servidor. Consulte [Visualización de gráficos de identidad](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en) para obtener más información sobre los gráficos de identidad.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y añada el siguiente código a `func removeIdentities(emailAddress: String, crmId: String)` función:

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** en el navegador del proyecto Xcode y busque el código que se ejecutará al seleccionar el **[!UICONTROL Cerrar sesión]** botón. Añada el siguiente código:

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. En la aplicación de Luma.
   1. Seleccione el **[!UICONTROL Inicio]** y mueva el icono de Assurance a la izquierda.
   1. Seleccione el <img src="assets/login.png" width="15" /> de la parte superior derecha.

      <img src="./assets/identity1.png" width="300">

   1. Proporcione una dirección de correo electrónico y un ID de CRM, o
   1. Seleccionar <img src="assets/insert.png" width="15" /> para generar de forma aleatoria una **[!UICONTROL Correo electrónico]** y **[!UICONTROL ID de CRM]**.
   1. Seleccionar **[!UICONTROL Iniciar sesión]**.

      <img src="./assets/identity2.png" width="300">


1. Busque en la interfaz web de Assurance la variable **[!UICONTROL Identidades de actualización de identidad de Edge]** evento de la **[!UICONTROL com.adobe.griffon.mobile]** proveedor.
1. Seleccione el evento y revise los datos en la **[!UICONTROL ACPExtensionEventData]** objeto. Debería ver las identidades que ha actualizado.
   ![validar actualización de identidades](assets/identity-validate-assurance.png)

## Validar con gráfico de identidad

Una vez completados los pasos en la [lección de Experience Platform](platform.md), puede confirmar la captura de identidad en el visualizador de gráficos de identidad de Platform:

1. Seleccionar **[!UICONTROL Identidades]** en la IU de recopilación de datos.
1. Seleccionar **[!UICONTROL Gráfico de identidad]** desde la barra superior.
1. Entrar `Luma CRM ID` como el **[!UICONTROL Área de nombres de identidad]** y su ID de CRM (por ejemplo, `24e620e255734d8489820e74f357b5c8`) como **[!UICONTROL Valor de identidad]**.
1. Verá el **[!UICONTROL Identidades]** enumerados.

   ![validar gráfico de identidad](assets/identity-validate-graph.png)

>[!INFO]
>
>No hay código en la aplicación para restablecer el ECID, lo que significa que solo puede restablecer el ECID (y crear de forma eficaz un nuevo perfil con un nuevo ECID) mediante una desinstalación y una reinstalación de la aplicación. Para implementar el restablecimiento de identificadores, consulte la [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) y [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities) Llamadas de API. Sin embargo, tenga en cuenta que cuando utilice un identificador de notificaciones push (consulte [Envío de notificaciones push](journey-optimizer-push.md)), ese identificador se convierte en otro identificador de perfil &quot;adhesivo&quot; en el dispositivo.


>[!SUCCESS]
>
>Ahora ha configurado la aplicación para actualizar identidades en la red perimetral y (cuando está configurada) con Adobe Experience Platform.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Recopilación de datos de perfil](profile.md)**
