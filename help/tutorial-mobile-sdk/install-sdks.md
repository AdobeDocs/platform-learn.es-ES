---
title: Instalación de SDK de Adobe Experience Platform Mobile
description: Obtenga información sobre cómo implementar el SDK de Adobe Experience Platform Mobile en una aplicación móvil.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: deea910040382142fe0b26893b9b20a949cb0974
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 1%

---

# Instalación de SDK de Adobe Experience Platform Mobile

Obtenga información sobre cómo implementar el SDK de Adobe Experience Platform Mobile en una aplicación móvil.

## Requisitos previos

* Se ha creado correctamente una biblioteca de etiquetas con las extensiones descritas en la [lección anterior](configure-tags.md).
* ID de archivo del entorno de desarrollo de [Instrucciones de instalación de Mobile](configure-tags.md#generate-sdk-install-instructions).
* Se descargó el vacío [aplicación de ejemplo](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Experiencia con [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Añada los SDK necesarios al proyecto mediante el Administrador de paquetes de Swift.
* Registre las extensiones.

>[!NOTE]
>
>En una implementación de aplicación móvil, los términos &quot;extensiones&quot; y &quot;SDK&quot; son casi intercambiables.

## Administrador De Paquetes Swift

En lugar de usar CocoaPods y un archivo Pod (como se describe en [Generar instrucciones de instalación del SDK](./configure-tags.md#generate-sdk-install-instructions)), puede agregar paquetes individuales utilizando el gestor de paquetes Swift nativo de Xcode. El proyecto Xcode ya tiene todas las dependencias de paquetes agregadas para usted. El Xcode **[!UICONTROL Dependencias del paquete]** La pantalla debería tener un aspecto similar al siguiente:

![Dependencias del paquete Xcode](assets/xcode-package-dependencies.png){zoomable=&quot;yes&quot;}


En Xcode, puede utilizar **[!UICONTROL Archivo]** > **[!UICONTROL Agregar paquetes...]** para agregar paquetes. La siguiente tabla proporciona vínculos a las direcciones URL que utilizaría para agregar paquetes. Los vínculos también le dirigen a más información sobre cada paquete específico.

| Paquete | Descripción |
|---|---|
| [Núcleo de AEP](https://github.com/adobe/aepsdk-core-ios) | El `AEPCore`, `AEPServices`, y `AEPIdentity` Las extensiones representan la base del SDK de Adobe Experience Platform. Todas las aplicaciones que utilicen el SDK deben incluirlas. Estos módulos contienen un conjunto común de funcionalidades y servicios que son necesarios para todas las extensiones de SDK.<br/><ul><li>`AEPCore` contiene la implementación del centro de eventos. Event Hub es el mecanismo que se utiliza para enviar eventos entre la aplicación y el SDK. Event Hub también se utiliza para compartir datos entre extensiones.</li><li>`AEPServices` proporciona varias implementaciones reutilizables necesarias para la compatibilidad con la plataforma, incluidas las de red, acceso a disco y administración de bases de datos.</li><li>`AEPIdentity` implementa la integración con los servicios de Adobe Experience Platform ID.</li><li>`AEPSignal` representa la extensión de señal del SDK de Adobe Experience Platform que permite a los especialistas en marketing enviar una &quot;señal&quot; a sus aplicaciones para enviar datos a destinos externos o para abrir direcciones URL.</li><li>`AEPLifecycle` representa la extensión del ciclo vital de los SDK de Adobe Experience Platform que ayuda a recopilar métricas del ciclo vital de la aplicación, como información de instalación o actualización de aplicaciones, información de inicio y sesión de aplicaciones, información del dispositivo y cualquier dato de contexto adicional proporcionado por el desarrollador de aplicaciones.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | La extensión móvil Adobe Experience Platform Edge Network (`AEPEdge`) permite enviar datos a Adobe Edge Network desde una aplicación móvil. Esta extensión le permite implementar las funcionalidades de Adobe Experience Cloud de una manera más sólida, ofrecer varias soluciones de Adobe a través de una llamada de red y enviar simultáneamente esta información a Adobe Experience Platform.<br/>La extensión móvil Edge Network es una extensión para el SDK de Adobe Experience Platform y requiere lo siguiente `AEPCore` y `AEPServices` extensiones para la gestión de eventos, así como el `AEPEdgeIdentity` extensión para recuperar las identidades, como ECID. |
| [Identidad de AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios) | La extensión móvil AEP Edge Identity (`AEPEdgeIdentity`) permite la administración de datos de identidad de usuario desde una aplicación móvil al utilizar el SDK de Adobe Experience Platform y la extensión de red perimetral. |
| [Consentimiento de AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | La extensión móvil AEP Consent Collection (`AEPConsent`) habilita la recopilación de preferencias de consentimiento de la aplicación móvil al utilizar el SDK de Adobe Experience Platform y la extensión de red perimetral. |
| [Perfil de usuario de AEP](https://github.com/adobe/aepsdk-userprofile-ios) | La extensión móvil del perfil de usuario de Adobe Experience Platform (`AEPUserProfile`) es una extensión para administrar perfiles de usuario para el SDK de Adobe Experience Platform. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | La extensión Places de AEP (`AEPPlaces`) le permite realizar un seguimiento de los eventos de geolocalización tal como se definen en la interfaz Lugares de Adobe y en las reglas de Etiquetas de recopilación de datos de Adobe. |
| [Mensajería AEP](https://github.com/adobe/aepsdk-messaging-ios) | La extensión de mensajería de AEP (`AEPMessaging`) le permite enviar tokens de notificaciones push y comentarios sobre clics en notificaciones push a Adobe Experience Platform. |
| [Optimización de AEP](https://github.com/adobe/aepsdk-optimize-ios) | La extensión Optimizar de AEP (`AEPOptimize`) proporciona API para habilitar flujos de trabajo de personalización en tiempo real en los SDK de Adobe Experience Platform Mobile mediante Adobe Target o Adobe Journey Optimizer Offer Decisioning. Requiere `AEPCore` y `AEPEdge` extensiones para enviar eventos de consulta de personalización a la red de Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Assurance (también conocido como proyecto Griffon) es una nueva e innovadora extensión (`AEPAssurance`) para ayudarle a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias en su aplicación móvil. Esta extensión habilita la aplicación para Assurance. |


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

1. Reemplace el `@AppStorage` valor `YOUR_ENVIRONMENT_ID_GOES_HERE` para `environmentFileId` al valor de ID de archivo del entorno de desarrollo que recuperó de las etiquetas en [Generar instrucciones de instalación del SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Añada el siguiente código a `application(_, didFinishLaunchingWithOptions)` función.

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
1. Habilita el registro de depuración. Encontrará más detalles y opciones en la [Documentación del SDK de Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Inicia la supervisión del ciclo vital. Consulte [Ciclo de vida](lifecycle-data.md) paso en el tutorial para obtener más información.
1. Establece el consentimiento predeterminado como desconocido. Consulte [Consentimiento](consent.md) paso en el tutorial para obtener más información.

>[!IMPORTANT]
>
>Asegúrese de actualizar `MobileCore.configureWith(appId: self.environmentFileId)` con el `appId` basado en el `environmentFileId` desde el entorno de etiquetas que está creando para (desarrollo, ensayo o producción).
>

>[!SUCCESS]
>
>Ahora ha instalado los paquetes necesarios y ha actualizado el proyecto para registrar correctamente las extensiones del SDK de Adobe Experience Platform Mobile necesarias que va a utilizar para el resto del tutorial.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Configurar Assurance](assurance.md)**
