---
title: Instalación de SDK de Adobe Experience Platform Mobile
description: Obtenga información sobre cómo implementar el SDK de Adobe Experience Platform Mobile en una aplicación móvil.
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 1%

---

# Instalación de SDK de Adobe Experience Platform Mobile

Obtenga información sobre cómo implementar el SDK de Adobe Experience Platform Mobile en una aplicación móvil.

## Requisitos previos

* La biblioteca de etiquetas se ha creado correctamente con las extensiones descritas en la [lección anterior](configure-tags.md).
* ID de archivo del entorno de desarrollo de [Instrucciones de instalación de Mobile](configure-tags.md#generate-sdk-install-instructions).
* Descargado, vacío [aplicación de ejemplo](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App{target="_blank"}).
* Experiencia con [XCode](https://developer.apple.com/xcode/{target="_blank"}).

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Añada los SDK necesarios a su proyecto mediante el Administrador de paquetes de Swift.
* Registre las extensiones.

>[!NOTE]
>
>En una implementación de aplicación móvil, los términos &quot;extensiones&quot; y &quot;SDK&quot; son casi intercambiables.

## Administrador De Paquetes Swift

En lugar de utilizar CocoaPods y un archivo Pod (como se describe en las Instrucciones de instalación móvil, consulte ) [Generar instrucciones de instalación del SDK](./configure-tags.md#generate-sdk-install-instructions)), puede agregar paquetes individuales utilizando el gestor de paquetes Swift nativo de Xcode.

En Xcode, utilice **[!UICONTROL Archivo]** > **[!UICONTROL Agregar paquetes...]** e instale todos los paquetes enumerados en la tabla siguiente. Seleccione el vínculo del paquete en la tabla para obtener la URL completa del paquete específico.

| Paquete | Descripción |
|---|---|
| [Núcleo de AEP](https://github.com/adobe/aepsdk-core-ios.git) | El `AEPCore`, `AEPServices`, y `AEPIdentity` Las extensiones representan la base del SDK de Adobe Experience Platform. Todas las aplicaciones que utilicen el SDK deben incluirlas. Estos módulos contienen un conjunto común de funcionalidades y servicios que son necesarios para todas las extensiones de SDK.<br/>`AEPCore` contiene la implementación del centro de eventos. Event Hub es el mecanismo que se utiliza para enviar eventos entre la aplicación y el SDK. Event Hub también se utiliza para compartir datos entre extensiones.<br/>`AEPServices` proporciona varias implementaciones reutilizables necesarias para la compatibilidad con la plataforma, incluidas las de red, acceso a disco y administración de bases de datos.<br/>`AEPIdentity` implementa la integración con los servicios de Adobe Experience Platform ID.<br/>`AEPSignal` representa la extensión Signal del SDK de Adobe Experience Platform que permite a los especialistas en marketing enviar una &quot;señal&quot; a sus aplicaciones para enviar datos a destinos externos o para abrir direcciones URL.<br/>`AEPLifecycle` representa la extensión Lifecycle del SDK de Adobe Experience Platform que ayuda a recopilar métricas del ciclo vital de la aplicación, como información de instalación o actualización de aplicaciones, información de inicio y sesión de aplicaciones, información del dispositivo y cualquier dato de contexto adicional proporcionado por el desarrollador de la aplicación. |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | La extensión móvil Adobe Experience Platform Edge Network permite enviar datos a Adobe Edge Network desde una aplicación móvil. Esta extensión le permite implementar las funcionalidades de Adobe Experience Cloud de una manera más sólida, ofrecer varias soluciones de Adobe a través de una llamada de red y enviar simultáneamente esta información a Adobe Experience Platform.<br/>La extensión móvil Edge Network es una extensión para el SDK de Adobe Experience Platform y requiere lo siguiente `AEPCore` y `AEPServices` extensiones para la gestión de eventos, así como el `AEPEdgeIdentity` extensión para recuperar las identidades, como ECID. |
| [Identidad de AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | La extensión móvil AEP Edge Identity permite administrar los datos de identidad de los usuarios desde una aplicación móvil al utilizar el SDK y la extensión de red perimetral de Adobe Experience Platform. |
| [Consentimiento de AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | La extensión móvil AEP Consent Collection permite la recopilación de preferencias de consentimiento de la aplicación móvil al utilizar el SDK de Adobe Experience Platform y la extensión de red perimetral. |
| [Perfil de usuario de AEP](https://github.com/adobe/aepsdk-userprofile-ios.git) | La extensión móvil de perfil de usuario de Adobe Experience Platform es una extensión para administrar perfiles de usuario para el SDK de Adobe Experience Platform. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | La extensión Adobe Experience Platform Places es una extensión del SDK de Adobe Experience Platform Swift. La extensión de AEP Places le permite rastrear eventos de geolocalización tal como se definen en la interfaz de usuario de Adobe Places y en las reglas de Launch de Adobe. |
| [Mensajería AEP](https://github.com/adobe/aepsdk-messaging-ios.git) | La extensión de mensajería de AEP es una extensión del SDK de Adobe Experience Platform Swift. La extensión de mensajería de AEP le permite enviar tokens de notificaciones push y comentarios sobre clics en notificaciones push a Adobe Experience Platform. |
| [Optimización de AEP](https://github.com/adobe/aepsdk-optimize-ios) | La extensión Optimizar de AEP proporciona API para habilitar flujos de trabajo de personalización en tiempo real en los SDK de Adobe Experience Platform Mobile mediante Adobe Target o Adobe Journey Optimizer Offer Decisioning. Requiere `AEPCore` y `AEPEdge` extensiones para enviar eventos de consulta de personalización a la red de Experience Edge. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance (también conocido como proyecto Griffon) es un producto nuevo e innovador que le ayudará a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias en su aplicación móvil. |


Una vez instalados todos los paquetes, su Xcode **[!UICONTROL Dependencias del paquete]** La pantalla debería tener un aspecto similar al siguiente:

![Dependencias del paquete Xcode](assets/xcode-package-dependencies.png)


## Importar extensiones

En Xcode, vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** y agregue las siguientes importaciones.

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

Haga lo mismo para **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]**.

## Actualizar AppDelegate

Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **AppDelegate** en el navegador del proyecto Xcode.

1. Configure las variables `@AppStorage` valor de `environmentFileId` al valor de ID de archivo del entorno de desarrollo que recuperó de las etiquetas en el paso 6 en [Generar instrucciones de instalación del SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "b5cbd1a1220e/1857ef6cacb5/launch-2594f26b23cd-development"
   ```

1. Añada el siguiente código a `application(_, didFinishLaunchingWithOptions)` función.

   ```swift
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
   
       // update version and build
       Logger.configuration.info("Luma - Updating version and build number...")
       SettingsBundleHelper.setVersionAndBuildNumber()
   })
   ```

El código anterior hace lo siguiente:

1. Registra las extensiones necesarias.
1. Configura MobileCore y otras extensiones para utilizar la configuración de propiedad de etiquetas.
1. Habilita el registro de depuración. Encontrará más detalles y opciones en la [Documentación del SDK de Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>
>Asegúrese de actualizar `MobileCore.configureWith(appId: self.environmentFileId)` con el `appId` basado en el `environmentFileId` desde el entorno de etiquetas que está creando para (desarrollo, ensayo o producción).
>

>[!SUCCESS]
>
>Ahora ha instalado los paquetes necesarios y ha actualizado el proyecto para registrar correctamente las extensiones del SDK de Adobe Experience Platform Mobile necesarias que va a utilizar para el resto del tutorial.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Configurar Assurance](assurance.md)**
