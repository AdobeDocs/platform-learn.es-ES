---
title: Implementación del consentimiento para implementaciones del SDK de Platform Mobile
description: Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# Implementación del consentimiento

Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.

La extensión móvil Adobe Experience Platform Consent habilita la recopilación de preferencias de consentimiento de su aplicación móvil al utilizar el SDK móvil de Adobe Experience Platform y la extensión de Edge Network. Obtenga más información acerca de la [extensión de consentimiento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Solicitar el consentimiento al usuario.
* Actualice la extensión en función de la respuesta del usuario.
* Obtenga información sobre cómo obtener el estado de consentimiento actual.

## Pedir consentimiento

Si ha seguido el tutorial desde el principio, es posible que recuerde que ha establecido el consentimiento predeterminado en la extensión de consentimiento en **[!UICONTROL Pendiente: eventos de cola que se producen antes de que el usuario proporcione preferencias de consentimiento.]**

Para empezar a recopilar datos, debe obtener el consentimiento del usuario. En una aplicación real, le recomendamos que consulte las prácticas recomendadas de consentimiento para su región. En este tutorial, obtiene el consentimiento del usuario simplemente pidiéndolo con una alerta:

1. Solo desea solicitar el consentimiento al usuario una vez. Puede hacerlo combinando el consentimiento del SDK móvil con la autorización necesaria para el seguimiento mediante el [marco de trabajo de transparencia de seguimiento de aplicaciones](https://developer.apple.com/documentation/apptrackingtransparency) de Apple. En esta aplicación, se supone que cuando el usuario autoriza el seguimiento, consiente en recopilar eventos.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode.

   Agregue este código a la función `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL Vista de exención de responsabilidad]** en el explorador de proyectos de Xcode, que es la vista que se muestra después de instalar o reinstalar la aplicación e iniciar la aplicación por primera vez. Se le pide al usuario que autorice el seguimiento según el [marco de trabajo de transparencia de seguimiento de aplicaciones](https://developer.apple.com/documentation/apptrackingtransparency) de Apple. Si el usuario lo autoriza, también debe actualizar el consentimiento.

   Agregue el código siguiente al cierre de `ATTrackingManager.requestTrackingAuthorization { status in`.

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## Obtener estado de consentimiento actual

La extensión móvil de consentimiento suprime automáticamente / suspende / permite el seguimiento en función del valor de consentimiento actual. También puede acceder al estado de consentimiento actual usted mismo:

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador de proyectos de Xcode.

   Agregue el siguiente código a la función `getConsents`:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** en el navegador de proyectos de Xcode.

   Agregue el siguiente código al modificador `.task`:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

En el ejemplo anterior, simplemente está registrando el estado de consentimiento en la consola en Xcode. En un escenario real, puede usarlo para modificar qué menús u opciones se muestran al usuario.

## Validar con Assurance

1. Elimine la aplicación del dispositivo o simulador para restablecer e inicializar correctamente el seguimiento y el consentimiento.
1. Para conectar el simulador o dispositivo a Assurance, consulte la sección [instrucciones de configuración](assurance.md#connecting-to-a-session).
1. Al pasar en la aplicación de la pantalla **[!UICONTROL Inicio]** a la pantalla **[!UICONTROL Productos]** y de nuevo a la pantalla **[!UICONTROL Inicio]**, debería ver el evento **[!UICONTROL Obtener respuesta de consentimiento]** en la interfaz de usuario de Assurance.
   ![validar consentimiento](assets/consent-update.png)


>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para solicitar al usuario de su inicio inicial después de la instalación (o reinstalación) el consentimiento mediante el SDK para móviles de Adobe Experience Platform.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Recopilar datos del ciclo vital](lifecycle-data.md)**
