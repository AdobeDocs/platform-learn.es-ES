---
title: Instalación de los SDK de Adobe Experience Platform Mobile
description: Obtenga información sobre cómo implementar el SDK de Adobe Experience Platform Mobile en una aplicación móvil.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# Instalación de los SDK de Adobe Experience Platform Mobile

Obtenga información sobre cómo implementar el SDK de Adobe Experience Platform Mobile en una aplicación móvil.

## Requisitos previos

* La biblioteca de etiquetas se ha creado correctamente con las extensiones descritas en la variable [lección anterior](configure-tags.md).
* ID del archivo de entorno de desarrollo de [Instrucciones de instalación de Mobile](configure-tags.md#generate-sdk-install-instructions).
* Descargado, vacío [aplicación de ejemplo](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;}.
* Experiencia con [XCode](https://developer.apple.com/xcode/){target=&quot;_blank&quot;}.
* Básico [línea de comandos](https://en.wikipedia.org/wiki/Command-line_interface){target=&quot;_blank&quot;} conocimiento.

## Objetivos de aprendizaje

En esta lección:

* Actualice el archivo CocoaPod .
* Importe los SDK necesarios.
* Registre las extensiones.

>[!NOTE]
>
>En una implementación de aplicación móvil, los términos &quot;extensiones&quot; y &quot;SDK&quot; son casi intercambiables.


## Actualizar PodFile

>[!NOTE]
>
> Si no está familiarizado con CocoaPods, consulte el [guía de introducción](https://guides.cocoapods.org/using/getting-started.html).

La instalación suele ser un simple comando sudo:

```console
sudo gem install cocoapods
```

Una vez instalados CocoaPods, abra el Podfile.

![Podfile inicial](assets/mobile-install-initial-podfile.png)

Actualice el archivo para incluir los siguientes pods:

```swift
pod 'AEPCore', '~> 3'
pod 'AEPEdge', '~> 1'
pod 'AEPUserProfile', '~> 3'
pod 'AEPAssurance', '~> 3'
pod 'AEPServices', '~> 3'
pod 'AEPEdgeConsent', '~> 1'
pod 'AEPLifecycle', '~>3'
pod 'AEPMessaging', '~>1'
pod 'AEPEdgeIdentity', '~>1'
pod 'AEPSignal', '~>3'
```

>[!NOTE]
>
> `AEPMessaging` solo es necesario si planea implementar la mensajería push mediante Adobe Journey Optimizer. Lea el tutorial en [implementación de la mensajería push con Adobe Journey Optimizer](journey-optimizer-push.md) para obtener más información.

Después de guardar los cambios en el Podfile, vaya a la carpeta con el proyecto y ejecute el `pod install` para instalar los cambios.

![instalación del pod](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> Si obtiene el &quot;No se ha encontrado ningún Podfile en el directorio del proyecto&quot;. , el terminal está en la carpeta incorrecta. Vaya a la carpeta con el Podfile que ha actualizado e inténtelo de nuevo.

Si desea actualizar a la versión más reciente, ejecute el `pod update` comando.

>[!INFO]
>
>Si no puede usar CocoaPods en sus propias aplicaciones, puede obtener más información sobre otras [implementaciones compatibles](https://github.com/adobe/aepsdk-core-ios#binaries) en el proyecto GitHub.

## Generar CocoaPods

Para crear CocoaPods, abra `Luma.xcworkspace`y seleccione **Product**, seguido de **Borrar carpeta de compilación**.

>[!NOTE]
>
> Es posible que tenga que configurar **Crear solo arquitectura activa** a **No**. Para ello, seleccione el proyecto Pods en el navegador de proyectos, seleccione **Configuración de compilación** y establezca la variable **Crear arquitectura activa** a **No**.

Ahora puede crear y ejecutar el proyecto.

![configuración de creación](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>El proyecto de Luma se creó con Xcode v12.5 en un chipset M1 y se ejecuta en el simulador de iOS. Si utiliza una configuración diferente, es posible que tenga que cambiar la configuración de la compilación para que refleje su arquitectura.
>
>Si la compilación no se realizó correctamente, intente revertir la variable **Crear arquitectura activa** > **Depuración** volver a configurar **Sí**.
>
>Se ha utilizado la configuración del simulador &quot;iPod touch (7ª generación)&quot; durante la creación de este tutorial.

## Importar extensiones

En cada una de las `.swift` agregue las siguientes importaciones. Comience agregando a `AppDelegate.swift`.

```swift
import AEPUserProfile
import AEPAssurance
import AEPEdge
import AEPCore
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPMessaging //Optional, used for AJO push messaging
import AEPSignal
import AEPServices
```

## Actualizar AppDelegate

En el `AppDelegate.swift` , agregue el siguiente código a `didFinishLaunchingWithOptions`. Reemplace currentAppId con el valor de ID del archivo de entorno de desarrollo que recuperó de las etiquetas en la variable [lección anterior](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` solo es necesario si planea implementar la mensajería push a través de Adobe Journey Optimizer como se describe [here](journey-optimizer-push.md).

El código anterior hace lo siguiente:

* Registra las extensiones requeridas.
* Configura MobileCore y otras extensiones para utilizar la configuración de la propiedad de etiquetas.
* Habilita el registro de depuración. Encontrará más detalles y opciones en la [Documentación del SDK móvil](https://aep-sdks.gitbook.io/docs/getting-started/enable-debug-logging).

>[!IMPORTANT]
>En una aplicación de producción, debe cambiar AppId según el entorno actual (dev/stag/prod).

Siguiente: **[Configuración de Assurance](assurance.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)