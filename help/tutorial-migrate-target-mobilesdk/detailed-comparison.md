---
title: Comparación de la extensión de Target con la extensión de Decisioning
description: Obtenga información sobre las diferencias entre la extensión de Target y la extensión Decisioning, incluidas las funciones, la configuración y el flujo de datos.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 05b0146256c6f8644e42f851498a0f49ff44bf68
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---

# Comparación de la extensión de Target con la extensión de Decisioning

La extensión de Adobe Journey Optimizer - Decisioning difiere de la extensión de Adobe Target para aplicaciones móviles. Las siguientes tablas son una referencia para ayudarle a evaluar las áreas de la implementación en las que puede que tenga que centrarse durante el proceso de migración.

Después de revisar la información siguiente y evaluar la implementación técnica actual de la extensión de Target, debería poder comprender lo siguiente:

- Qué funciones de Target son compatibles con Adobe Journey Optimizer: Decisioning
- Qué funciones de extensión de Adobe Target tienen equivalentes en Adobe Journey Optimizer y Decisioning
- Aplicación de la configuración de Target con Adobe Journey Optimizer: decisiones
- Diferencias entre el flujo de datos de la extensión de Adobe Target y la extensión de Adobe Journey Optimizer - Decisioning

Si es nuevo en el SDK web de Platform, no se preocupe: los elementos siguientes se tratan con más detalle a lo largo de este tutorial.

## Comparación de características

| Función | Extensión de Target | Extensión de Decisioning (Target a través de Edge) |
|---|---|---|
| Modo de recuperación previa | Admitido | Admitido |
| Modo de ejecución | Admitido | No compatible |
| Parámetros personalizados | Admitido | Compatible* |
| Parámetros de perfil | Admitido | Compatible* |
| Parámetros de entidad | Admitido | Compatible* |
| Públicos destinatarios | Admitido | Admitido |
| Audiencias de Real-Time CDP | ??? | Admitido |
| Atributos de Real-Time CDP | ??? | Admitido |
| Métricas del ciclo vital | Admitido | Compatible mediante reglas de recopilación de datos |
| thirdPartyId (mbox3rdPartyId) | Admitido | Compatible mediante el mapa de identidad y la configuración del área de nombres en el conjunto de datos |
| Notificaciones (mostrar, hacer clic) | Admitido | Admitido |
| Tokens de respuesta | Admitido | Admitido |
| Analytics para Target (A4T) | Solo del lado del cliente | Lado del cliente y lado del servidor |
| Vistas previas móviles (modo de control de calidad) | Admitido | Compatibilidad limitada con Assurance |

>[!IMPORTANT]
>
> \* Los parámetros enviados en una solicitud se aplican a todos los ámbitos de la solicitud. Si necesita establecer parámetros diferentes para ámbitos diferentes, debe realizar solicitudes adicionales.



## Llamadas dignas de mención

>[!NOTE]
>
>No se admite la migración de Target al SDK web de Platform mientras se mantiene una implementación de Adobe Analytics de AppMeasurement existente para una página determinada.
>
> Es posible migrar la implementación de at.js (y AppMeasurement.js) al SDK web de Platform de una en una. Si adopta este enfoque, es mejor establecer las opciones [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) y [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) en `true` con el comando `configure`.

## Funciones de extensión de Target y equivalentes de extensión de Decisioning

Muchas funciones de extensión de Target tienen un enfoque equivalente que utiliza la extensión Decisioning descrita en la tabla siguiente. Para obtener más información sobre [funciones](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte la Guía para desarrolladores de Adobe Target.

| Extensión de Target | Extensión de Decisioning | Notas |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Al usar la API `getPropositions`, no se realiza ninguna llamada remota para recuperar ámbitos no almacenados en caché en el SDK. |
| `displayedLocations` | Oferta -> `displayed()` | Además, se puede utilizar el método de oferta `generateDisplayInteractionXdm` para generar el XDM para la visualización del elemento. Posteriormente, la API sendEvent del SDK de la red de Edge se puede utilizar para adjuntar datos de XDM y de forma libre adicionales y enviar un evento de experiencia al remoto. |
| `clickedLocation` | Oferta -> `tapped()` | Además, se puede usar el método de oferta `generateTapInteractionXdm` para generar el XDM al tocar el elemento. Posteriormente, la API sendEvent del SDK de la red de Edge se puede utilizar para adjuntar datos de XDM y de forma libre adicionales y enviar un evento de experiencia al remoto. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` |  | Utilice la API `removeIdentity` de Identity para la extensión de Edge Network para que el SDK deje de enviar el identificador de visitante a la red de Edge. Para obtener más información, consulte [la documentación de la API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Nota: la API `resetIdentities` de Mobile Core borra todas las identidades almacenadas en el SDK, incluido el ID de Experience Cloud (ECID), y debe usarse con moderación. |
| `getSessionId` |  | El identificador de respuesta `state:store` contiene información relacionada con la sesión. La extensión de red de Edge ayuda a administrarla adjuntando elementos de almacén de estado no caducados a solicitudes posteriores. |
| `setSessionId` |  | El identificador de respuesta `state:store` contiene información relacionada con la sesión. La extensión de red de Edge ayuda a administrarla adjuntando elementos de almacén de estado no caducados a solicitudes posteriores. |
| `getThirdPartyId` | n/a | Utilice la API updateIdentities de Identity para la extensión de Edge Network para proporcionar el valor de ID de terceros. A continuación, configure el área de nombres de ID de terceros en el conjunto de datos. Para obtener más información, consulte [la documentación móvil del ID de terceros de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/a | Utilice la API updateIdentities de Identity para la extensión de Edge Network para proporcionar el valor de ID de terceros. A continuación, configure el área de nombres de ID de terceros en el conjunto de datos. Para obtener más información, consulte [la documentación móvil del ID de terceros de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` |  | El identificador de respuesta `locationHint:result` lleva la información de indicio de ubicación de Target. Se supone que Target Edge se ubicará en el mismo sitio que Experience Edge. <br> <br>La extensión de red de Edge usa la sugerencia de ubicación EdgeNetwork para determinar el clúster de red de Edge al que enviar solicitudes. Para compartir sugerencias de ubicación de red de Edge entre SDK (aplicaciones híbridas), use las API `getLocationHint` y `setLocationHint` de la extensión de Edge Network. Para obtener más información, consulte [la documentación de la API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

## Configuración de la extensión de Target y equivalentes de la extensión Decisioning

La extensión de Target se puede configurar y descargar con varios ajustes en la ...

| Extensión de Target | Extensión de Decisioning |
| --- | --- | 
| |  |


## Comparación del diagrama del sistema

Los siguientes diagramas le ayudarán a comprender las diferencias del flujo de datos entre una implementación de Target con la extensión Adobe Journey Optimizer - Decisioning y una implementación con la extensión Adobe Target.

### Diagrama del sistema de extensiones de Target



### Diagrama del sistema de extensión de Decisioning




>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
