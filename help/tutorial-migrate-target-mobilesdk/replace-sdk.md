---
title: Reemplace la extensión SDK - Migrar de Adobe Target a Adobe Journey Optimizer - Decisioning Mobile
description: Obtenga información sobre cómo reemplazar SDK al migrar del Adobe Target a la extensión Adobe Journey Optimizer - Decisioning Mobile.
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: 62afd1f41b3d20c04782a2b18423683ed3b49d1f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---

# Reemplace Target SDK por Optimize SDK

Obtenga información sobre cómo reemplazar los SDK de Adobe Target con los SDK de Optimización en su implementación móvil. Un reemplazo básico consiste en los siguientes pasos:

* Actualizar dependencias en el Podfile o archivo `build.gradle`
* Actualizar importaciones
* Actualizar código de aplicación

>[!INFO]
>
>Dentro del ecosistema de Adobe Experience Platform Mobile SDK, las extensiones se implementan mediante SDK importados en las aplicaciones que pueden tener nombres diferentes:
>
> * **Target SDK** implementa la **extensión de Adobe Target**
> * **Optimizar SDK** implementa la extensión **Adobe Journey Optimizer - Decisioning**

## Actualizar dependencias

Ejemplo de +++Android

>[!BEGINTABS]

>[!TAB Optimizar SDK]

`build.gradle` dependencias después de migrar

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:edgeconsent'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:assurance'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!TAB SDK de destino]

`build.gradle` dependencias antes de migrar

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!ENDTABS]

+++

+++ Ejemplo de iOS

>[!BEGINTABS]


>[!TAB Optimizar SDK]

`Podfile` dependencias después de migrar

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB SDK de destino]

`Podfile` dependencias antes de migrar

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]

+++

## Actualización de importaciones y códigos

+++ Ejemplo de Android

>[!BEGINTABS]

>[!TAB Optimizar SDK]

Código de inicialización de Java después de migrar

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Assurance;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
import com.adobe.marketing.mobile.edge.consent.Consent;
import com.adobe.marketing.mobile.edge.identity.Identity;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Consent.EXTENSION,
            com.adobe.marketing.mobile.edge.identity.Identity.EXTENSION,
            com.adobe.marketing.mobile.Identity.EXTENSION,
            Edge.EXTENSION,
            Assurance.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!TAB SDK de destino]

Código de inicialización de Java antes de migrar

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB Optimizar SDK]

Código de inicialización de Swift después de migrar

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Consent.self,
            AEPEdgeIdentity.Identity.self,
            AEPIdentity.Identity.self,
            Edge.self,
            Assurance.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!TAB SDK de destino]

Código de inicialización de Swift antes de migrar

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]

+++

## Comparación de funciones

Muchas funciones de extensión de Target tienen un enfoque equivalente que utiliza la extensión Decisioning descrita en la tabla siguiente. Para obtener más información sobre [funciones](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte la Guía para desarrolladores de Adobe Target.

| Extensión de Target | Extensión de Decisioning | Notas |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Al usar la API `getPropositions`, no se realiza ninguna llamada remota para recuperar ámbitos no almacenados en caché en SDK. |
| `displayedLocations` | Oferta -> `displayed()` | Además, se puede utilizar el método de oferta `generateDisplayInteractionXdm` para generar el XDM para la visualización del elemento. Posteriormente, la API sendEvent de Edge network SDK se puede utilizar para adjuntar datos de XDM y de forma libre adicionales y enviar un evento de experiencia al remoto. |
| `clickedLocation` | Oferta -> `tapped()` | Además, se puede usar el método de oferta `generateTapInteractionXdm` para generar el XDM al tocar el elemento. Posteriormente, la API sendEvent de Edge network SDK se puede utilizar para adjuntar datos de XDM y de forma libre adicionales y enviar un evento de experiencia al remoto. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | n/a | Utilice la API `removeIdentity` de Identity for Edge Network para que SDK deje de enviar el identificador de visitante a la red de Edge. Para obtener más información, consulte [la documentación de la API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Nota: la API `resetIdentities` de Mobile Core borra todas las identidades almacenadas en SDK, incluido el Experience Cloud ID (ECID), y debe usarse con moderación. |
| `getSessionId` | n/a | El identificador de respuesta `state:store` contiene información relacionada con la sesión. La extensión de red de Edge ayuda a administrarla adjuntando elementos de almacén de estado no caducados a solicitudes posteriores. |
| `setSessionId` | n/a | El identificador de respuesta `state:store` contiene información relacionada con la sesión. La extensión de red de Edge ayuda a administrarla adjuntando elementos de almacén de estado no caducados a solicitudes posteriores. |
| `getThirdPartyId` | n/a | Utilice la API updateIdentities de Identity para la extensión de Edge Network para proporcionar el valor de ID de terceros. A continuación, configure el área de nombres de ID de terceros en el conjunto de datos. Para obtener más información, consulte [la documentación móvil del ID de terceros de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/a | Utilice la API updateIdentities de Identity para la extensión de Edge Network para proporcionar el valor de ID de terceros. A continuación, configure el área de nombres de ID de terceros en el conjunto de datos. Para obtener más información, consulte [la documentación móvil del ID de terceros de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` | n/a | El identificador de respuesta `locationHint:result` lleva la información de indicio de ubicación de Target. Se supone que Target Edge se ubicará en el mismo sitio que Experience Edge. <br> <br>La extensión de red de Edge usa la sugerencia de ubicación EdgeNetwork para determinar el clúster de red de Edge al que enviar solicitudes. Para compartir sugerencias de ubicación de red de Edge entre SDK (aplicaciones híbridas), use las API `getLocationHint` y `setLocationHint` de la extensión de Edge Network. Para obtener más información, consulte [la documentación de la API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` | n/a | El identificador de respuesta `locationHint:result` lleva la información de indicio de ubicación de Target. Se supone que Target Edge se ubicará en el mismo sitio que Experience Edge. <br> <br>La extensión de red de Edge usa la sugerencia de ubicación EdgeNetwork para determinar el clúster de red de Edge al que enviar solicitudes. Para compartir sugerencias de ubicación de red de Edge entre SDK (aplicaciones híbridas), use las API `getLocationHint` y `setLocationHint` de la extensión de Edge Network. Para obtener más información, consulte [la documentación de la API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |


A continuación, aprenda a [solicitar y procesar actividades](render-activities.md) en la página.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
