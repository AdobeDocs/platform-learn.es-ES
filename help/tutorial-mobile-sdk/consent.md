---
title: Implementación del consentimiento para implementaciones de Platform Mobile SDK
description: Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# Implementación del consentimiento

Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.

La extensión móvil Adobe Experience Platform Consent habilita la recopilación de preferencias de consentimiento de su aplicación móvil al utilizar las extensiones Adobe Experience Platform Mobile SDK y Edge Network. Obtenga más información acerca de la [extensión de consentimiento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) en la documentación.

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

>[!BEGINTABS]

>[!TAB iOS]

1. Solo desea solicitar el consentimiento al usuario una vez. Combina el consentimiento de Mobile SDK con la autorización necesaria para realizar el seguimiento mediante el [marco de trabajo de transparencia de seguimiento de aplicaciones](https://developer.apple.com/documentation/apptrackingtransparency) de Apple. En esta aplicación, se supone que cuando el usuario autoriza el seguimiento, consiente en recopilar eventos.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode.

   Agregue este código a la función `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL Vista de exención de responsabilidad]** en el navegador de proyectos de Xcode. El explorador de proyectos de Xode es la vista que se muestra después de instalar o reinstalar la aplicación e iniciar la aplicación por primera vez. Se le pide al usuario que autorice el seguimiento según el [marco de trabajo de transparencia de seguimiento de aplicaciones](https://developer.apple.com/documentation/apptrackingtransparency) de Apple. Si el usuario lo autoriza, también debe actualizar el consentimiento.

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

>[!TAB Android]

1. Solo desea solicitar el consentimiento al usuario una vez. En esta aplicación, se supone que cuando el usuario autoriza el seguimiento, consiente en recopilar eventos.

1. Vaya a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio.

   Agregue este código a la función `updateConsent(value: String)`.

   ```kotlin
   // Update consent
   val collectConsent = mapOf("collect" to mapOf("val" to value))
   val currentConsents = mapOf("consents" to collectConsent)
   Consent.update(currentConsents)
   MobileCore.updateConfiguration(currentConsents)
   ```

1. Vaya a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL DisclaimerView.kt]** en el navegador de Android Studio.

   Agregue el código siguiente a la función `DisclaimerView(navController: NavController)` debajo de `// Set content to yes` y `// Set content to no`.

   ```kotlin
   // Add consent based on authorization
   if (status) {
      showPersonalizationWarning = false
   
      // Set consent to yes
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.AUTHORIZED)
      MobileSDK.shared.updateConsent("y")
   } else {
      Toast.makeText(
            context,
            "You will not receive offers and location tracking will be disabled.",
            Toast.LENGTH_LONG
      ).show()
      showPersonalizationWarning = true
   
      // Set consent to no
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.DENIED)
      MobileSDK.shared.updateConsent("n")
   }
   ```

>[!ENDTABS]

## Obtener estado de consentimiento actual

La extensión móvil de consentimiento suprime automáticamente / suspende / permite el seguimiento en función del valor de consentimiento actual. También puede acceder al estado de consentimiento actual usted mismo:

>[!BEGINTABS]

>[!TAB iOS]

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

>[!TAB Android]

1. Vaya a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio.

   Agregue el siguiente código a la función `getConsents()`:

   ```kotlin
   // Get consents
   Consent.getConsents { callback ->
      if (callback != null) {
            val jsonStr = JSONObject(callback).toString(4)
            Log.i("MobileSDK", "Consent getConsents: $jsonStr")
      }
   }
   ```

1. Vaya a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL HomeView.kt]** en el navegador de Android Studio.

   Agregue el siguiente código a `LaunchedEffect(unit)`:

   ```kotlin
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

En el ejemplo anterior, simplemente registra el estado de consentimiento en la consola de Android Studio. En un escenario real, puede usarlo para modificar qué menús u opciones se muestran al usuario.

>[!ENDTABS]

## Validar con Assurance

1. Elimine la aplicación del dispositivo o simulador para restablecer e inicializar el seguimiento y el consentimiento correctamente.
1. Para conectar el simulador o dispositivo a Assurance, revise la sección [instrucciones de instalación](assurance.md#connecting-to-a-session).
1. Al pasar en la aplicación de la pantalla **[!UICONTROL Inicio]** a la pantalla **[!UICONTROL Productos]** y de nuevo a la pantalla **[!UICONTROL Inicio]**, debería ver el evento **[!UICONTROL Obtener respuesta de consentimientos]** en la interfaz de usuario de Assurance.
   ![validar consentimiento](assets/consent-update.png){zoomable="yes"}


>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para solicitar al usuario de Adobe Experience Platform Mobile SDK su consentimiento al inicio tras la instalación (o reinstalación).
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Recopilar datos del ciclo vital](lifecycle-data.md)**
