---
title: Instalación de SDK de Adobe Experience Platform Mobile
description: Obtenga información sobre cómo implementar Adobe Experience Platform Mobile SDK en una aplicación móvil.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 3dd9c68203d0021e87caaa82bd962b3f9160a397
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Instalación de SDK de Adobe Experience Platform Mobile {#tutorial_install_mobile_sdks}

>[!CONTEXTUALHELP]
>
>id="platform_mobile_sdk_tutorial_install"
>title="Instalación de SDK de Adobe Experience Platform Mobile"
>abstract="Obtenga información sobre cómo implementar Adobe Experience Platform Mobile SDK en una aplicación móvil."

Obtenga información sobre cómo implementar Adobe Experience Platform Mobile SDK en una aplicación móvil.

## Requisitos previos

* Se creó correctamente una biblioteca de etiquetas con las extensiones descritas en la [lección anterior](configure-tags.md).
* ID de archivo del entorno de desarrollo de [Instrucciones de instalación móvil](configure-tags.md#generate-sdk-install-instructions).
* Descargó la [aplicación de ejemplo](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} vacía.
* Experiencia con [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Añada los SDK necesarios al proyecto mediante el Administrador de paquetes de Swift.
* Registre las extensiones.

>[!NOTE]
>
>En una implementación de aplicación móvil, los términos &quot;extensiones&quot; y &quot;SDK&quot; son casi intercambiables.

## Administrador De Paquetes Swift

En lugar de usar CocoaPods y un archivo Pod (como se describe en [Generar instrucciones de instalación de SDK](./configure-tags.md#generate-sdk-install-instructions)), agrega paquetes individuales usando el administrador de paquetes Swift nativo de Xcode. El proyecto Xcode ya tiene todas las dependencias de paquetes agregadas para usted. La pantalla de Xcode **[!UICONTROL Dependencias del paquete]** debe tener un aspecto similar al siguiente:

![Dependencias del paquete Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


En Xcode, puede usar **[!UICONTROL Archivo]** > **[!UICONTROL Agregar paquetes...]** para agregar paquetes. La siguiente tabla proporciona vínculos a las direcciones URL que utilizaría para agregar paquetes. Los vínculos también le dirigen a más información sobre cada paquete específico.

| Paquete | Descripción |
|---|---|
| [Núcleo de AEP](https://github.com/adobe/aepsdk-core-ios) | Las extensiones `AEPCore`, `AEPServices` y `AEPIdentity` representan la base de Adobe Experience Platform SDK; todas las aplicaciones que utilicen SDK deben incluirlas. Estos módulos contienen un conjunto común de funciones y servicios que son necesarios para todas las extensiones de SDK.<br/><ul><li>`AEPCore` contiene la implementación de Event Hub. Event Hub es el mecanismo que se utiliza para enviar eventos entre la aplicación y SDK. Event Hub también se utiliza para compartir datos entre extensiones.</li><li>`AEPServices` proporciona varias implementaciones reutilizables necesarias para la compatibilidad con la plataforma, incluidas la red, el acceso a disco y la administración de bases de datos.</li><li>`AEPIdentity` implementa la integración con los servicios de identidad de Adobe Experience Platform.</li><li>`AEPSignal` representa la extensión de señal del SDK de Adobe Experience Platform que permite a los especialistas en marketing enviar una &quot;señal&quot; a sus aplicaciones para enviar datos a destinos externos o para abrir direcciones URL.</li><li>`AEPLifecycle` representa la extensión del ciclo vital de los SDK de Adobe Experience Platform que ayuda a recopilar métricas del ciclo vital de la aplicación, como información de actualización o instalación de aplicaciones, información de inicio y sesión de aplicaciones, información del dispositivo y cualquier dato de contexto adicional proporcionado por el desarrollador de la aplicación.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | La extensión móvil de Edge Network de Adobe Experience Platform (`AEPEdge`) le permite enviar datos a Adobe Edge Network desde una aplicación móvil. Esta extensión le permite implementar las funcionalidades de Adobe Experience Cloud de una manera más sólida, ofrecer varias soluciones de Adobe a través de una llamada de red y enviar simultáneamente esta información a Adobe Experience Platform.<br/>La extensión móvil de Edge Network es una extensión para Adobe Experience Platform SDK y requiere las extensiones `AEPCore` y `AEPServices` para la administración de eventos, así como la extensión `AEPEdgeIdentity` para recuperar las identidades, como ECID. |
| [Identidad de Edge de AEP](https://github.com/adobe/aepsdk-edgeidentity-ios) | La extensión móvil Edge Identity de AEP (`AEPEdgeIdentity`) permite administrar los datos de identidad de un usuario desde una aplicación móvil al utilizar Adobe Experience Platform SDK y la extensión de Edge Network. |
| [Consentimiento de AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | La extensión móvil AEP Consent Collection (`AEPConsent`) habilita la recopilación de preferencias de consentimiento de la aplicación móvil al utilizar Adobe Experience Platform SDK y la extensión de Edge Network. |
| [Perfil de usuario de AEP](https://github.com/adobe/aepsdk-userprofile-ios) | La extensión móvil de perfil de usuario de Adobe Experience Platform (`AEPUserProfile`) es una extensión para administrar perfiles de usuario para Adobe Experience Platform SDK. |
| [Lugares de AEP](https://github.com/adobe/aepsdk-places-ios) | La extensión Places de AEP (`AEPPlaces`) le permite rastrear eventos de geolocalización según se definen en la interfaz de Places de Adobe y en las reglas de etiquetas de recopilación de datos de Adobe. |
| [Mensajería AEP](https://github.com/adobe/aepsdk-messaging-ios) | La extensión de mensajería de AEP (`AEPMessaging`) le permite enviar tokens de notificaciones push y comentarios sobre clics en notificaciones push a Adobe Experience Platform. |
| [Optimizar AEP](https://github.com/adobe/aepsdk-optimize-ios) | La extensión Optimizar de AEP (`AEPOptimize`) proporciona API para habilitar flujos de trabajo de personalización en tiempo real en los SDK de Adobe Experience Platform Mobile mediante Adobe Target o Adobe Journey Optimizer Offer Decisioning. Se requieren las extensiones `AEPCore` y `AEPEdge` para enviar eventos de consulta de personalización a la red de Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Assurance (también conocido como proyecto Griffon) es una extensión nueva e innovadora (`AEPAssurance`) que le ayudará a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias en su aplicación móvil. Esta extensión habilita la aplicación para Assurance. |


## Importar extensiones

En Xcode, vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** y asegúrese de que las siguientes importaciones formen parte de este archivo de origen.

```swift
// import AEP MobileSDK libraries
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

Haga lo mismo para **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**.

## Actualizar AppDelegate

Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** en el navegador del proyecto Xcode.

1. Reemplace el valor `@AppStorage` `YOUR_ENVIRONMENT_ID_GOES_HERE` de `environmentFileId` por el valor de Id. de archivo del entorno de desarrollo que recuperó de las etiquetas en [Generar instrucciones de instalación de SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Agregue el siguiente código a la función `application(_, didFinishLaunchingWithOptions)`.

   ```swift
   // Define extensions
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   
   // Register extensions
   MobileCore.registerExtensions(extensions, {
       // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
       Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
       MobileCore.configureWith(appId: self.environmentFileId)
   
       // set this to false or comment it when deploying to TestFlight (default is false),
       // set this to true when testing on your device.
       MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
       if appState != .background {
           // only start lifecycle if the application is not in the background
           MobileCore.lifecycleStart(additionalContextData: nil)
       }
   
       // assume unknown, adapt to your needs.
       MobileCore.setPrivacyStatus(.unknown)
   })
   ```

El código anterior hace lo siguiente:

1. Registra las extensiones necesarias.
1. Configura MobileCore y otras extensiones para utilizar la configuración de propiedad de etiquetas.
1. Habilita el registro de depuración. Encontrará más detalles y opciones en la [documentación de Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Inicia la supervisión del ciclo vital. Consulte el paso [Ciclo vital](lifecycle-data.md) en el tutorial para obtener más información.
1. Establece el consentimiento predeterminado como desconocido. Consulte el paso [Consentimiento](consent.md) en el tutorial para obtener más información.

>[!IMPORTANT]
>
>Asegúrese de actualizar `MobileCore.configureWith(appId: self.environmentFileId)` con `appId` en función de `environmentFileId` desde el entorno de etiqueta para el que está creando (desarrollo, ensayo o producción).
>

>[!SUCCESS]
>
>Ahora ha instalado los paquetes necesarios y ha actualizado el proyecto para registrar correctamente las extensiones de Adobe Experience Platform Mobile SDK necesarias que va a utilizar para el resto del tutorial.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Configurar Assurance](assurance.md)**
