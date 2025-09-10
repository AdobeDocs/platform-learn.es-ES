---
title: Recopilación de datos de identidad en una aplicación móvil con Mobile SDK
description: Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.
feature: Mobile SDK,Identities
jira: KT-14633
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 1%

---

# Recopilación de datos de identidad

Obtenga información sobre cómo recopilar datos de identidad en una aplicación móvil.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y de sus comportamientos. Los servicios vinculan identidades entre dispositivos y sistemas, y le permiten ofrecer experiencias digitales personales impactantes en tiempo real. Los campos de identidad y las áreas de nombres son el pegamento que une diferentes fuentes de datos para crear un perfil de cliente en tiempo real de 360 grados.

Obtenga más información acerca de la [extensión de identidad](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) y el [servicio de identidad](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Configure un área de nombres de identidad personalizada.
* Actualizar identidades.
* Valide el gráfico de identidad.
* Obtenga ECID y otras identidades.


## Configurar un área de nombres de identidad personalizada

Las áreas de nombres de identidad son componentes de [Identity Service](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) que sirven como indicadores del contexto al que se relaciona una identidad. Por ejemplo, distinguen un valor de `name@email.com` como dirección de correo electrónico o `443522` como ID numérico de CRM.

>[!NOTE]
>
>Mobile SDK genera una identidad única en su propia área de nombres, denominada Experience Cloud ID (ECID) cuando se instala la aplicación. Este ECID se almacena en la memoria persistente del dispositivo móvil y se envía con cada visita. El ECID se elimina cuando el usuario desinstala la aplicación o cuando establece el estado de privacidad global de Mobile SDK como de exclusión. En la aplicación de Luma de ejemplo, debe eliminar y reinstalar la aplicación para crear un nuevo perfil con su propio ECID único.


Para crear un área de nombres de identidad nueva:

1. En la interfaz de recopilación de datos, seleccione **[!UICONTROL Identidades]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Crear espacio de nombres de identidad]**.
1. Proporcione un **[!UICONTROL nombre para mostrar]** de `Luma CRM ID` y un valor de **[!UICONTROL símbolo de identidad]** de `lumaCRMId`.
1. Seleccione **[!UICONTROL ID entre dispositivos]**.
1. Seleccione **[!UICONTROL Crear]**.

   ![crear área de nombres de identidad](assets/identity-create.png){zoomable="yes"}




## Actualización de identidades

Desea actualizar la identidad estándar (correo electrónico) y la identidad personalizada (ID de Luma CRM) cuando el usuario inicia sesión en la aplicación.

>[!BEGINTABS]

>[!TAB iOS]

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y busque la implementación de la función `func updateIdentities(emailAddress: String, crmId: String)`. Agregue el siguiente código a la función.

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

   1. Crea un objeto `IdentityMap` vacío.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Configura `IdentityItem` objetos para el correo electrónico y el ID de CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Agrega estos `IdentityItem` objetos al objeto `IdentityMap`.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Envía el objeto `IdentityItem` como parte de la llamada de API `Identity.updateIdentities` a Edge Network.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** en el navegador del proyecto Xcode y busque el código que se ejecutará al seleccionar el botón **[!UICONTROL Login]**. Añada el siguiente código:

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio y busque la implementación de la función `fun updateIdentities(emailAddress: String, crmId: String) `. Agregue el siguiente código a la función.

   ```kotlin
   // Set up identity map, add identities to map and update identities
   val identityMap = IdentityMap()
   
   val emailIdentity = IdentityItem(emailAddress, AuthenticatedState.AUTHENTICATED, true)
   val crmIdentity = IdentityItem(crmId, AuthenticatedState.AUTHENTICATED, true)
   identityMap.addItem(emailIdentity, "Email")
   identityMap.addItem(crmIdentity, "lumaCRMId")
   
   Identity.updateIdentities(identityMap)
   ```

   Este código:

   1. Crea un objeto `IdentityMap` vacío.

      ```kotlin
      val identityMap = IdentityMap()
      ```

   1. Configura `IdentityItem` objetos para el correo electrónico y el ID de CRM.

      ```kotlin
      val emailIdentity = IdentityItem(emailAddress, AuthenticatedState.AUTHENTICATED, true)
      val crmIdentity = IdentityItem(crmId, AuthenticatedState.AUTHENTICATED, true)
      ```

   1. Agrega estos `IdentityItem` objetos al objeto `IdentityMap`.

      ```kotlin
      identityMap.addItem(emailIdentity, "Email")
      identityMap.addItem(crmIdentity, "lumaCRMId")
      ```

   1. Envía el objeto `IdentityItem` como parte de la llamada de API `Identity.updateIdentities` a Edge Network.

      ```kotlin
      Identity.updateIdentities(identityMap)
      ```

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL LoginSheet.kt]** en el navegador de Android Studio y busque el código que se ejecutará al seleccionar el botón **[!UICONTROL Login]**. Añada el siguiente código:

   ```kotlin
   // Update identities
   MobileSDK.shared.updateIdentities(
      MobileSDK.shared.currentEmailId.value,
      MobileSDK.shared.currentCRMId.value
   )                             
   ```


>[!ENDTABS]



>[!NOTE]
>
>Puede enviar varias identidades en una sola llamada a `updateIdentities`. También puede modificar las identidades enviadas anteriormente.


## Eliminación de una identidad

Puede usar la API [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) para quitar la identidad del mapa de identidad del lado del cliente almacenado. La extensión de identidad deja de enviar el identificador a Edge Network. El uso de esta API no elimina el identificador del gráfico de identidades del lado del servidor. Consulte [Ver gráficos de identidad](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/identities/view-identity-graphs) para obtener más información sobre los gráficos de identidad.


>[!BEGINTABS]

>[!TAB iOS]

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y agregue el siguiente código a la función `func removeIdentities(emailAddress: String, crmId: String)`:

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "b642b4217b34b1e8d3bd915fc65c4452"
   ```

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** en el navegador del proyecto Xcode y busque el código que se ejecutará al seleccionar el botón **[!UICONTROL Cerrar sesión]**. Añada el siguiente código:

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```

>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio y agregue el siguiente código a la función `fun removeIdentities(emailAddress: String, crmId: String)`:

   ```kotlin
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(IdentityItem(emailAddress), "Email")
   Identity.removeIdentity(IdentityItem(crmId), "lumaCRMId")
   currentEmailId.value = "testUser@gmail.com"
   currentCRMId.value = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1.Vaya a **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL vistas]** > **[!UICONTROL LoginSheet.kt]** en el navegador de Android Studio y busque el código que se ejecutará al seleccionar el botón **[!UICONTROL Cerrar sesión]**. Añada el siguiente código:

```kotlin
// Remove identities
MobileSDK.shared.removeIdentities(
   MobileSDK.shared.currentEmailId.value,
   MobileSDK.shared.currentCRMId.value
)              
```


>[!ENDTABS]

## Validar con Assurance

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. En la aplicación de Luma.
   1. Seleccione la ficha **[!UICONTROL Página de inicio]** y mueva el icono Assurance a la izquierda.
   1. Seleccione el Icono <img src="assets/login.png" width="15" /> de la parte superior derecha.

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/identity1.png" width="300">

>[!TAB Android]

<img src="./assets/identity1-android.png" width="300">

>[!ENDTABS]

1. Proporcione una dirección de correo electrónico y un ID de CRM, o
1. Seleccionar <img src="assets/insert.png" width="15" /> (iOS) o **[!UICONTROL Generar correo electrónico aleatorio]** (Android) para generar **[!UICONTROL correo electrónico]** y **[!UICONTROL ID de CRM]** de forma aleatoria.
1. Seleccione **[!UICONTROL Iniciar sesión]**.

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/identity2.png" width="300">

>[!TAB Android]

<img src="./assets/identity2-android.png" width="300">


>[!ENDTABS]

Vuelva a Assurance:

1. Inspeccione la interfaz web de Assurance en busca del evento **[!UICONTROL Identidades de actualización de identidad de Edge]** del proveedor **[!UICONTROL com.adobe.griffon.mobile]**.
1. Seleccione el evento y revise los datos en el objeto **[!UICONTROL ACPExtensionEventData]**. Debería ver las identidades que ha actualizado.
   ![validar actualización de identidades](assets/identity-validate-assurance.png){zoomable="yes"}

## Validar con gráfico de identidad

Una vez que complete los pasos de la [lección de Experience Platform](platform.md), podrá confirmar la captura de identidad en el visor de gráficos de identidades de Experience Platform:

1. Seleccione **[!UICONTROL Identidades]** en la IU de recopilación de datos.
1. Seleccione **[!UICONTROL Gráfico de identidad]** en la barra superior.
1. Escriba `Luma CRM ID` como **[!UICONTROL área de nombres de identidad]** y su ID de CRM (por ejemplo `24e620e255734d8489820e74f357b5c8`) como **[!UICONTROL valor de identidad]**.
1. Verá las **[!UICONTROL Identidades]** en la lista.

   ![validar gráfico de identidad](assets/identity-validate-graph.png){zoomable="yes"}

>[!INFO]
>
>No hay código en la aplicación para restablecer el ECID. Solo puede restablecer el ECID (y crear efectivamente un nuevo perfil con un nuevo ECID) mediante una desinstalación y una reinstalación de la aplicación. Para implementar el restablecimiento de identificadores, consulte las llamadas a la API [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) y [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities). Tenga en cuenta que cuando utiliza un identificador de notificación push (consulte [Envío de notificaciones push](journey-optimizer-push.md)), ese identificador se convierte en otro identificador de perfil &quot;adhesivo&quot; en el dispositivo.


>[!SUCCESS]
>
>Ahora ha configurado la aplicación para actualizar identidades en Edge Network y (cuando está configurada) con Adobe Experience Platform.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Recopilar datos de perfil](profile.md)**
