---
title: Instalar los SDK móviles de Adobe Experience Platform
description: Obtenga información sobre cómo implementar el SDK móvil de Adobe Experience Platform en una aplicación móvil.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 3%

---

# Instalar los SDK móviles de Adobe Experience Platform {#tutorial_install_mobile_sdks}

>[!CONTEXTUALHELP]
>
>id="platform_mobile_sdk_tutorial_install"
>title="Instalar los SDK móviles de Adobe Experience Platform"
>abstract="Obtenga información sobre cómo implementar el SDK móvil de Adobe Experience Platform en una aplicación móvil."

Obtenga información sobre cómo implementar el SDK móvil de Adobe Experience Platform en una aplicación móvil.

## Requisitos previos

* Se creó correctamente una biblioteca de etiquetas con las extensiones descritas en la [lección anterior](configure-tags.md).
* ID de archivo del entorno de desarrollo de [Instrucciones de instalación móvil](configure-tags.md#generate-sdk-install-instructions).
* Se ha descargado la aplicación de ejemplo [para iOS](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) o [para Android](https://github.com/adobe/Luma-Android).
* Experiencia con [Xcode](https://developer.apple.com/xcode/) (iOS) o [Android Studio](https://developer.android.com/studio/intro?utm_source=android-studio) (Android)

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Añada los SDK necesarios al proyecto.
* Registre las extensiones.

>[!NOTE]
>
>En una implementación de aplicación móvil, los términos *extensiones* y *SDK* son casi intercambiables.

>[!BEGINTABS]

>[!TAB iOS]

## Administrador De Paquetes Swift

En lugar de usar CocoaPods y un archivo Pod (como se describe en [Generar instrucciones de instalación de SDK](./configure-tags.md#generate-sdk-install-instructions)), agrega paquetes individuales usando el administrador de paquetes Swift nativo de Xcode. El proyecto Xcode ya tiene todas las dependencias de paquetes agregadas para usted. La pantalla de Xcode **[!UICONTROL Dependencias del paquete]** debe tener un aspecto similar al siguiente:

![Dependencias del paquete Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


En Xcode, puede usar **[!UICONTROL Archivo]** > **[!UICONTROL Agregar paquetes...]** para agregar paquetes. La siguiente tabla proporciona vínculos a las direcciones URL que utilizaría para agregar paquetes. Los vínculos también le dirigen a más información sobre cada paquete específico.

| Paquete | Descripción |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Las extensiones `AEPCore`, `AEPServices` y `AEPIdentity` representan la base de Adobe Experience Platform SDK; todas las aplicaciones que utilicen SDK deben incluirlas. Estos módulos contienen un conjunto común de funciones y servicios que todas las extensiones de SDK requieren.<br/><ul><li>`AEPCore` contiene la implementación de Event Hub. Event Hub es el mecanismo que se utiliza para enviar eventos entre la aplicación y SDK. Event Hub también se utiliza para compartir datos entre extensiones.</li><li>`AEPServices` proporciona varias implementaciones reutilizables necesarias para la compatibilidad con la plataforma, incluidas la red, el acceso a disco y la administración de bases de datos.</li><li>`AEPIdentity` implementa la integración con los servicios de identidad de Adobe Experience Platform.</li><li>`AEPSignal` representa la extensión de señal del SDK de Adobe Experience Platform que permite a los especialistas en marketing enviar una &quot;señal&quot; a sus aplicaciones para enviar datos a destinos externos o para abrir direcciones URL.</li><li>`AEPLifecycle` representa la extensión del ciclo vital de los SDK de Adobe Experience Platform que ayuda a recopilar métricas del ciclo vital de la aplicación, como información de actualización o instalación de aplicaciones, información de inicio y sesión de aplicaciones, información del dispositivo y cualquier dato de contexto adicional proporcionado por el desarrollador de la aplicación.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | La extensión móvil Adobe Experience Platform Edge Network (`AEPEdge`) permite enviar datos a Adobe Edge Network desde una aplicación móvil. Esta extensión le permite implementar las funcionalidades de Adobe Experience Cloud de una manera más sólida, ofrecer varias soluciones de Adobe a través de una llamada de red y reenviar simultáneamente esta información a Adobe Experience Platform.<br/>La extensión móvil de Edge Network es una extensión para Adobe Experience Platform SDK. La extensión requiere las extensiones `AEPCore` y `AEPServices` para la administración de eventos, así como la extensión `AEPEdgeIdentity` para recuperar las identidades, como ECID. |
| [Identidad de AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios) | La extensión móvil Adobe Experience Platform Edge Identity (`AEPEdgeIdentity`) habilita la administración de datos de identidad de usuario desde una aplicación móvil al usar Adobe Experience Platform SDK y la extensión de Edge Network. |
| [Consentimiento de AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | La extensión móvil Adobe Experience Platform Consent Collection (`AEPConsent`) habilita la recopilación de preferencias de consentimiento de la aplicación móvil al utilizar Adobe Experience Platform SDK y la extensión de Edge Network. |
| [Perfil de usuario de AEP](https://github.com/adobe/aepsdk-userprofile-ios) | La extensión móvil de perfil de usuario de Adobe Experience Platform (`AEPUserProfile`) es una extensión para administrar perfiles de usuario para Adobe Experience Platform SDK. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | La extensión Adobe Experience Platform Places (`AEPPlaces`) le permite realizar un seguimiento de los eventos de geolocalización tal como se definen en la interfaz de Adobe Places y en las reglas de etiquetas de recopilación de datos de Adobe. |
| [Mensajería de AEP](https://github.com/adobe/aepsdk-messaging-ios) | La extensión de mensajería de Adobe Experience Platform (`AEPMessaging`) le permite enviar tokens de notificaciones push y comentarios sobre clics en notificaciones push a Adobe Experience Platform. |
| [Optimizar AEP](https://github.com/adobe/aepsdk-optimize-ios) | La extensión Adobe Experience Platform Optimize (`AEPOptimize`) proporciona API para habilitar flujos de trabajo de personalización en tiempo real en los SDK de Adobe Experience Platform Mobile mediante Adobe Target o Adobe Journey Optimizer Offer Decisioning. Se requieren las extensiones `AEPCore` y `AEPEdge` para enviar eventos de consulta de personalización a Experience Edge Network. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Adobe Experience Platform Assurance es un producto de Adobe Experience Cloud que le ayuda a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias en su aplicación móvil. |


## Importar extensiones

Abra en Xcode el proyecto en la carpeta **[!UICONTROL Start]** de la aplicación de ejemplo.

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

1. Reemplace el valor `@AppStorage` `YOUR_ENVIRONMENT_ID_GOES_HERE` para `environmentFileId` por el valor de Id. de archivo de entorno que recuperó de las etiquetas en [Generar instrucciones de instalación de SDK](configure-tags.md#generate-sdk-install-instructions).

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

Asegúrese de actualizar `MobileCore.configureWith(appId: self.environmentFileId)` con `appId` en función de `environmentFileId` desde el entorno de etiqueta para el que está creando (desarrollo, ensayo o producción).

>[!TAB Android]

## Gradle

Utiliza las dependencias de [Generate SDK install instructions](./configure-tags.md#generate-sdk-install-instructions) para agregar paquetes individuales mediante la integración de Gradle con Android Studio. El proyecto de Android Studio ya tiene todas las dependencias de paquetes agregadas para usted.

1. Seleccione ![FolderOutline](/help/assets/icons/FolderOutline.svg) como herramienta.
1. Seleccione la vista **[!UICONTROL Android]**.
1. Seleccione **[!UICONTROL Gradle scripts]** > **[!UICONTROL build.gradle.kts (Módulo :app)]** en el panel izquierdo. A continuación, en el panel derecho, desplácese hasta que vea `dependencies`.

   ![Dependencias de Android Gradle](assets/androidstudio-package-dependencies.png){zoomable="yes"}

En Android Studio, puede usar **[!UICONTROL Archivo]** > **[!UICONTROL Estructura del proyecto...]** para agregar dependencias de módulo. Seleccione **[!UICONTROL Dependencias]** y luego use **[!UICONTROL Módulos]** ![Agregar](/help/assets/icons/Add.svg) para agregar módulos. La siguiente tabla proporciona vínculos a las direcciones URL que utilizaría para agregar módulos de dependencia. Los vínculos también le dirigen a más información sobre cada módulo específico.

| Paquete<br/>com.adobe.<br/>marketing.mobile: | Descripción |
|---|---|
| [core](https://github.com/adobe/aepsdk-core-android) | Las extensiones `MobileCore` y `Identity` representan la base de Adobe Experience Platform SDK. Todas las aplicaciones que utilicen SDK deben incluirlas. Estos módulos contienen un conjunto común de funcionalidades y servicios que todas las extensiones de SDK no requieren.<ul><li>`MobileCore` contiene la implementación de Event Hub. Event Hub es el mecanismo que se utiliza para enviar eventos entre la aplicación y SDK. El centro de eventos también se utiliza para compartir datos entre extensiones y proporciona varias implementaciones reutilizables necesarias para la compatibilidad con la plataforma, incluidas la red, el acceso a disco y la administración de bases de datos.</li><li>`Identity` implementa la integración con los servicios de identidad de Adobe Experience Platform.</li><li>`Signal` representa la extensión de señal de Adobe Experience Platform SDK que permite a los especialistas en marketing enviar una &quot;señal&quot; a sus aplicaciones para enviar datos a destinos externos o para abrir direcciones URL.</li><li>`Lifecycle` representa la extensión de ciclo vital de Adobe Experience Platform SDK que ayuda a recopilar métricas del ciclo vital de la aplicación, como información de actualización o instalación de aplicaciones, información de inicio y sesión de aplicaciones, información del dispositivo y cualquier dato de contexto adicional proporcionado por el desarrollador de la aplicación.</li></ul> |
| [edge](https://github.com/adobe/aepsdk-edge-android) | La extensión móvil Adobe Experience Platform Edge Network (`AEPEdge`) permite enviar datos a Adobe Edge Network desde una aplicación móvil. Esta extensión le permite implementar las funcionalidades de Adobe Experience Cloud de una manera más sólida, ofrecer varias soluciones de Adobe a través de una llamada de red y reenviar simultáneamente esta información a Adobe Experience Platform.<br/>La extensión móvil de Edge Network es una extensión para Adobe Experience Platform SDK. La extensión requiere las extensiones `Mobile Core` y `Services` para la administración de eventos. Y la extensión `Identity for Edge Network` para recuperar las identidades, como ECID. |
| [edgeidentity](https://github.com/adobe/aepsdk-edgeidentity-android) | La extensión móvil Adobe Experience Platform Edge Identity permite administrar los datos de identidad de los usuarios desde una aplicación móvil al utilizar Adobe Experience Platform SDK y la extensión de Edge Network. |
| [edgeconsent](https://github.com/adobe/aepsdk-edgeconsent-android) | La extensión móvil Adobe Experience Platform Consent Collection permite la recopilación de preferencias de consentimiento de la aplicación móvil al utilizar la extensión Adobe Experience Platform SDK y Edge Network. |
| [perfil de usuario](https://github.com/adobe/aepsdk-userprofile-android) | La extensión móvil de perfil de usuario de Adobe Experience Platform es una extensión para administrar perfiles de usuario para Adobe Experience Platform SDK. |
| [aepplaces](https://github.com/adobe/aepsdk-places-android) | El servicio Adobe Places es un servicio de localización geográfica que permite a las aplicaciones móviles conocer la ubicación. Y comprender el contexto de la ubicación utilizando interfaces de SDK enriquecidas y fáciles de usar, acompañadas de una base de datos flexible de puntos de interés (POI). Para obtener más información, consulte la Documentación del servicio Places.<br/>Este servicio es la extensión móvil Places para Android 2.x Adobe Experience Platform SDK y requiere la extensión Core para la administración de eventos. |
| [mensajes](https://github.com/adobe/aepsdk-messaging-android) | La extensión de mensajería de Adobe Experience Platform alimenta las notificaciones push, los mensajes en la aplicación y las experiencias basadas en código para sus aplicaciones móviles. Esta extensión también le ayuda a recopilar tokens push de usuario y gestiona la medición de interacciones con los servicios de Adobe Experience Platform. |
| [optimizar](https://github.com/adobe/aepsdk-optimize-android) | La extensión Adobe Experience Platform Optimize proporciona API para habilitar flujos de trabajo de personalización en tiempo real en los SDK de Adobe Experience Platform mediante Adobe Target o Adobe Journey Optimizer Offer Decisioning. Depende de Mobile Core y requiere Edge Extension para enviar eventos de consulta de personalización a Experience Edge Network. |
| [garantía](https://github.com/adobe/aepsdk-assurance-android) | Assurance (también conocido como proyecto Griffon) es una extensión móvil para Adobe Experience Platform que permite la integración con Adobe Experience Platform Assurance. La extensión ayuda a inspeccionar, probar, simular y validar el modo en que se recopilan datos o se sirven las experiencias en la aplicación móvil. Esta extensión requiere MobileCore. |

## Importar extensiones

En Android Studio, vaya a **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** y asegúrese de que las siguientes importaciones formen parte del archivo de origen.

```kotlin
import com.adobe.marketing.mobile.Assurance
import com.adobe.marketing.mobile.Edge
import com.adobe.marketing.mobile.Lifecycle
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.Messaging
import com.adobe.marketing.mobile.MobileCore
import com.adobe.marketing.mobile.MobilePrivacyStatus
import com.adobe.marketing.mobile.Places
import com.adobe.marketing.mobile.Signal
import com.adobe.marketing.mobile.UserProfile
import com.adobe.marketing.mobile.edge.consent.Consent
import com.adobe.marketing.mobile.edge.identity.Identity
import com.adobe.marketing.mobile.optimize.Optimize
```

Haga lo mismo para **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]**.


## Actualizar aplicación de Luma

En la vista de **[!UICONTROL Android]**, vaya a **[!UICONTROL aplicación]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** en Android Studio.

1. Reemplace `"YOUR_ENVIRONMENT_FILE_ID"` en `private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"` por el valor de Id. de archivo de entorno que recuperó de las etiquetas en [Generar instrucciones de instalación de SDK](configure-tags.md#generate-sdk-install-instructions).

   ```kotlin
   private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Agregue el siguiente código a la función `override fun onCreate()` en `class LumaApplication : Application()`.

   ```kotlin
   // Define extensions
   val extensions = listOf(
      Identity.EXTENSION,
      Lifecycle.EXTENSION,
      Signal.EXTENSION,
      Edge.EXTENSION,
      Consent.EXTENSION,
      UserProfile.EXTENSION,
      Places.EXTENSION,
      Messaging.EXTENSION,
      Optimize.EXTENSION,
      Assurance.EXTENSION
   )
   
   // Register extensions
   MobileCore.registerExtensions(extensions) {
   // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
     Log.i("Luma", "Using mobile config: $environmentFileId")
     MobileCore.configureWithAppID(environmentFileId)
   
     // set this to true when testing on your device, default is false.
     //MobileCore.updateConfiguration(mapOf("messaging.useSandbox" to true))
   
     // assume unknown, adapt to your needs.
     MobileCore.setPrivacyStatus(MobilePrivacyStatus.UNKNOWN)
   }
   ```

   El código anterior hace lo siguiente:

   1. Registra las extensiones necesarias.
   1. Configura MobileCore y otras extensiones para utilizar la configuración de propiedad de etiquetas.
   1. Habilita el registro de depuración. Encontrará más detalles y opciones en la [documentación de Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
   1. Inicia la supervisión del ciclo vital. Consulte el paso [Ciclo vital](lifecycle-data.md) en el tutorial para obtener más información.
   1. Establece el consentimiento predeterminado como desconocido. Consulte el paso [Consentimiento](consent.md) en el tutorial para obtener más información.

Asegúrese de actualizar `MobileCore.configureWith(environmentFileId)` con `environmentFileId` en función del ID de archivo de entorno del entorno de etiqueta para el que está creando (desarrollo, ensayo o producción).


>[!ENDTABS]

>[!SUCCESS]
>
>Ahora ha instalado los paquetes necesarios y ha actualizado el proyecto para registrar las extensiones de Adobe Experience Platform Mobile SDK necesarias que va a utilizar para el resto del tutorial.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=es)

Siguiente: **[Configurar Assurance](assurance.md)**
