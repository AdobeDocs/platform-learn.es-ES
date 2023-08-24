---
title: Consentimiento
description: Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.
feature: Mobile SDK,Consent
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 2%

---

# Consentimiento

Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.

La extensión móvil Adobe Experience Platform Consent habilita la recopilación de preferencias de consentimiento de su aplicación móvil al utilizar el SDK móvil de Adobe Experience Platform y la extensión de red perimetral. Obtenga más información acerca de [Extensión de consentimiento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/), en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Solicitar el consentimiento al usuario.
* Actualice la extensión en función de la respuesta del usuario.
* Obtenga información sobre cómo obtener el estado de consentimiento actual.

## Pedir consentimiento

Si ha seguido el tutorial desde el principio, puede recordar que ha establecido el consentimiento predeterminado en la extensión de consentimiento en **[!UICONTROL Pendiente: eventos de cola que se producen antes de que el usuario proporcione preferencias de consentimiento.]**

Para empezar a recopilar datos, debe obtener el consentimiento del usuario. En este tutorial, obtiene el consentimiento del usuario simplemente pidiéndolo con una alerta. En una aplicación real, le recomendamos que consulte las prácticas recomendadas de consentimiento para su región.

1. Solo desea preguntar al usuario una vez. Por lo tanto, desea combinar el consentimiento del SDK móvil con las autorizaciones necesarias para el seguimiento mediante el de Apple [Marco de transparencia de seguimiento de aplicaciones](https://developer.apple.com/documentation/apptrackingtransparency). En esta aplicación, se da por hecho que, cuando el usuario autoriza el seguimiento, también consiente la recopilación de eventos.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el Navegador de proyectos de Xcode.

   Añada este código a `updateConsent` función.

   ```swift
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL General]** > **[!UICONTROL DisclaimerView]** en el navegador de proyectos de Xcode, que es la vista que se muestra después de instalar o reinstalar la aplicación e iniciar la aplicación por primera vez. Se solicita al usuario que autorice el seguimiento según el de Apple [Marco de transparencia de seguimiento de aplicaciones](https://developer.apple.com/documentation/apptrackingtransparency). Si el usuario lo autoriza, también debe actualizar el consentimiento.

   Añada el siguiente código a `ATTrackingManager.requestTrackingAuthorization { status in` cierre.

   ```swift
   if status == .authorized {
         // Set consent to yes
         MobileSDK.shared.updateConsent(value: "y")
   }
   else {
         MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## Obtener estado de consentimiento actual

La extensión móvil de consentimiento suprime automáticamente / suspende / permite el seguimiento en función del valor de consentimiento actual. También puede acceder al estado de consentimiento actual usted mismo:

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el navegador de proyectos de Xcode.

   Añada el siguiente código a `getConsents` función:

   ```swift
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL General]** > **[!UICONTROL HomeView]** en el navegador de proyectos de Xcode.

   Añada el siguiente código a `.task` modificador:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

En el ejemplo anterior, simplemente está registrando el estado de consentimiento en la consola en Xcode. En un escenario real, puede usarlo para modificar qué menús u opciones se muestran al usuario.

## Validar con Assurance

1. Revise la [Assurance](assurance.md) lección.
1. Instale la aplicación.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. Si agregó el código anterior correctamente, se le pedirá que proporcione consentimiento.

   Seleccionar **[!UICONTROL Continuar...]** y luego seleccione **[!UICONTROL Permitir]**.

   <img src="./assets/consent-update-1.png" width="300" /> 
   <img src="./assets/consent-update-2.png" width="300" />

1. Debería ver una **[!UICONTROL Obtener respuesta de consentimientos]** en la interfaz de usuario de Assurance.
   ![validación del consentimiento](assets/consent-update.png)



>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para solicitar al usuario de su inicio inicial después de la instalación (o reinstalación) el consentimiento mediante el SDK para móviles de Adobe Experience Platform.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Recopilar datos del ciclo vital](lifecycle-data.md)**
