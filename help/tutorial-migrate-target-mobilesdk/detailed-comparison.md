---
title: Comparación de la extensión de Target con la extensión de Decisioning
description: Obtenga información sobre las diferencias entre la extensión de Target y la extensión Decisioning, incluidas las funciones, la configuración y el flujo de datos.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 8e4e23413c842f84159891287d09e8a6cfbbbc53
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Comparación de la extensión de Target con la extensión de Decisioning

La extensión de Adobe Journey Optimizer - Decisioning difiere de la extensión de Adobe Target para aplicaciones móviles. Las siguientes tablas son una referencia para ayudarle a evaluar las áreas de la implementación en las que puede que tenga que centrarse durante el proceso de migración.

Después de revisar la información siguiente y evaluar la implementación técnica actual de la extensión de Target, debería poder comprender lo siguiente:

- Qué funciones de Target son compatibles con Adobe Journey Optimizer: Decisioning
- Qué funciones de extensión de Adobe Target tienen equivalentes en Adobe Journey Optimizer y Decisioning
- Aplicación de la configuración de Target con Adobe Journey Optimizer: decisiones
- Flujo de datos con la extensión Adobe Journey Optimizer - Decisioning


## Comparación de características

| Función | Extensión de Target | Extensión de Decisioning (Target a través de Edge) |
|---|---|---|
| Modo de recuperación previa | Admitido | Admitido |
| Modo de ejecución | Admitido | No compatible |
| Parámetros personalizados | Admitido | Compatible* |
| Parámetros de perfil | Admitido | Compatible* |
| Parámetros de entidad | Admitido | Compatible* |
| Públicos destinatarios | Admitido | Admitido |
| Audiencias de Real-Time CDP | No compatible | Admitido |
| Atributos de Real-Time CDP | No compatible | Admitido |
| Métricas del ciclo vital | Admitido | Compatible mediante reglas de recopilación de datos |
| thirdPartyId (mbox3rdPartyId) | Admitido | Compatible mediante mapa de identidad y área de nombres de ID de terceros de Target en el conjunto de datos |
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
>Mantenga la configuración y los ajustes de Etiquetas de extensión de Target en su lugar incluso después de haber migrado el código de la aplicación a la extensión Decisioning. Esto garantizará que Target siga funcionando para los clientes que aún no han actualizado la aplicación a la nueva versión.
>
>Si utiliza la integración de Analytics para Target (A4T), asegúrese de migrar también su implementación de Analytics con la extensión Bridge de Edge al mismo tiempo que migra la implementación de Target a la extensión Decisioning.

## Funciones de extensión de Target y equivalentes de extensión de Decisioning

Muchas funciones de extensión de Target tienen un enfoque equivalente que utiliza la extensión Decisioning descrita en la tabla siguiente. Para obtener más información sobre [funciones](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte la Guía para desarrolladores de Adobe Target.

| Extensión de Target | Extensión de Decisioning | Notas |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Al usar la API `getPropositions`, no se realiza ninguna llamada remota para recuperar ámbitos no almacenados en caché en el SDK. |
| `displayedLocations` | Oferta -> `displayed()` | Además, se puede utilizar el método de oferta `generateDisplayInteractionXdm` para generar el XDM para la visualización del elemento. Posteriormente, la API sendEvent del SDK de la red de Edge se puede utilizar para adjuntar datos de XDM y de forma libre adicionales y enviar un evento de experiencia al remoto. |
| `clickedLocation` | Oferta -> `tapped()` | Además, se puede usar el método de oferta `generateTapInteractionXdm` para generar el XDM al tocar el elemento. Posteriormente, la API sendEvent del SDK de la red de Edge se puede utilizar para adjuntar datos de XDM y de forma libre adicionales y enviar un evento de experiencia al remoto. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | n/a | Utilice la API `removeIdentity` de Identity para la extensión de Edge Network para que el SDK deje de enviar el identificador de visitante a la red de Edge. Para obtener más información, consulte [la documentación de la API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Nota: la API `resetIdentities` de Mobile Core borra todas las identidades almacenadas en el SDK, incluido el ID de Experience Cloud (ECID), y debe usarse con moderación. |
| `getSessionId` | n/a | El identificador de respuesta `state:store` contiene información relacionada con la sesión. La extensión de red de Edge ayuda a administrarla adjuntando elementos de almacén de estado no caducados a solicitudes posteriores. |
| `setSessionId` | n/a | El identificador de respuesta `state:store` contiene información relacionada con la sesión. La extensión de red de Edge ayuda a administrarla adjuntando elementos de almacén de estado no caducados a solicitudes posteriores. |
| `getThirdPartyId` | n/a | Utilice la API updateIdentities de Identity para la extensión de Edge Network para proporcionar el valor de ID de terceros. A continuación, configure el área de nombres de ID de terceros en el conjunto de datos. Para obtener más información, consulte [la documentación móvil del ID de terceros de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/a | Utilice la API updateIdentities de Identity para la extensión de Edge Network para proporcionar el valor de ID de terceros. A continuación, configure el área de nombres de ID de terceros en el conjunto de datos. Para obtener más información, consulte [la documentación móvil del ID de terceros de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` | n/a | El identificador de respuesta `locationHint:result` lleva la información de indicio de ubicación de Target. Se supone que Target Edge se ubicará en el mismo sitio que Experience Edge. <br> <br>La extensión de red de Edge usa la sugerencia de ubicación EdgeNetwork para determinar el clúster de red de Edge al que enviar solicitudes. Para compartir sugerencias de ubicación de red de Edge entre SDK (aplicaciones híbridas), use las API `getLocationHint` y `setLocationHint` de la extensión de Edge Network. Para obtener más información, consulte [la documentación de la API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` | n/a | El identificador de respuesta `locationHint:result` lleva la información de indicio de ubicación de Target. Se supone que Target Edge se ubicará en el mismo sitio que Experience Edge. <br> <br>La extensión de red de Edge usa la sugerencia de ubicación EdgeNetwork para determinar el clúster de red de Edge al que enviar solicitudes. Para compartir sugerencias de ubicación de red de Edge entre SDK (aplicaciones híbridas), use las API `getLocationHint` y `setLocationHint` de la extensión de Edge Network. Para obtener más información, consulte [la documentación de la API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |

## Configuración de la extensión de Target y equivalentes de la extensión Decisioning

La extensión de Target tiene [opciones configurables](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) que están [configuradas en la secuencia de datos](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup) con la extensión Decisioning.

| Extensión de Target | Extensión de Decisioning | Notas |
| --- | --- | --- | 
| Código de cliente | n/a | Establecido automáticamente por el perímetro de mediante los detalles de organización de IMS |
| ID de entorno | ID de entorno de destino | Configurado en el conjunto de datos |
| Propiedad de Workspace de destino | Token de propiedad | Configurado en el conjunto de datos |
| Tiempo de espera | No configurable | El tiempo de espera con la extensión Decisioning es de 10 segundos |
| Dominio del servidor | dominio de Edge Network | Establecido en la extensión de Edge Network de Adobe Experience Platform |

>[!IMPORTANT]
>
> Mantenga la configuración de la extensión de Target en su lugar incluso después de haber migrado el código de la aplicación a la extensión de Decisioning. Esto garantizará que Target siga funcionando para los usuarios que aún no han actualizado su aplicación.

## Diagrama del sistema de extensión de Decisioning

El diagrama siguiente debería ayudarle a comprender el flujo de datos mediante la extensión Adobe Journey Optimizer - Decisioning.

![Adobe Target Edge Decisioning con el SDK móvil del lado del cliente](assets/diagram.png)


>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
