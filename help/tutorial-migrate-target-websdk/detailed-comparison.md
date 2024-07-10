---
title: Comparación de at.js 2.x con el SDK web | Migración de Target de at.js 2.x a SDK web
description: Obtenga información sobre las diferencias entre at.js 2.x y el SDK web de Platform, incluidas las funciones, la configuración y el flujo de datos.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 299b9586fb5c8e9c9ef3427e08035806af1d9a6b
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 3%

---

# Comparación de at.js con el SDK web de Platform

La biblioteca independiente at.js de Adobe Target difiere considerablemente del SDK web de Platform. Las siguientes tablas son una referencia para ayudarle a evaluar las áreas de la implementación en las que puede que tenga que centrarse durante el proceso de migración.

Después de revisar la información que aparece a continuación y evaluar su implementación técnica actual de at.js, debería poder comprender lo siguiente:

- Qué funciones de Target son compatibles con el SDK web de Platform
- Qué funciones de at.js tienen equivalentes del SDK web de Platform
- Aplicación de la configuración de Target con el SDK web de Platform
- Diferencias entre el flujo de datos de at.js y el SDK web de Platform

Si es nuevo en el SDK web de Platform, no se preocupe: los elementos siguientes se tratan con más detalle a lo largo de este tutorial.

## Comparación de características

| | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Actualizar perfil de Target | Admitido | Admitido |
| Vista de déclencheur SPA para la | Admitido | Admitido |
| Target Recommendations | Admitido | Admitido |
| Buscar ofertas basadas en formularios | Admitido | Admitido |
| Seguimiento de eventos | Admitido | Admitido |
| A4T: aplicación de una sola página | Admitido | Admitido |
| A4T: rastreo de clics | Admitido | Admitido |
| A4T: Registro en el lado del cliente | Admitido | Admitido |
| A4T: Registro en el servidor | Admitido | Admitido |
| Aplicar ofertas | Admitido | Admitido |
| SPA Volver a procesar la vista en los informes de sin notificaciones | Admitido | Admitido |
| Aplicaciones híbridas | Admitido | Admitido |
| URL de QA | Admitido | Admitido |
| ID de terceros de Mbox | Admitido | Admitido |
| Atributos del cliente | Admitido | Admitido |
| Ofertas remotas | Admitido | Admitido |
| Ofertas de redirección | Admitido | Compatible. Sin embargo, no se admite el redireccionamiento de una página con el SDK web de Platform a una página con at.js (y en la dirección opuesta). |
| Toma de decisiones en el dispositivo | Admitido | Actualmente no es compatible |
| Mboxes de recuperación previa | SPA Admitido para ámbitos personalizados y VEC de | La recuperación previa es el modo predeterminado para el SDK web |
| Eventos personalizados | Admitido | No compatible. Consulte la [hoja de ruta pública](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) para el estado actual. |
| Tokens de respuesta | Admitido | Compatible. Consulte la [documentación de tokens de respuesta dedicados](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) para ver ejemplos de código y las diferencias entre at.js y el SDK web de Platform |
| Proveedores de datos | Admitido | No compatible. Se puede utilizar código personalizado para almacenar en déclencheur un SDK web de Platform `sendEvent` después de recuperar los datos de otro proveedor. |


## Llamadas dignas de mención

| | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Mitigación de parpadeo | El fragmento preocultado para implementaciones asincrónicas utiliza un ID de estilo de `at-body-style`. at.js busca este ID de elemento para eliminar el estilo una vez que se reciba una respuesta. | El fragmento preocultado predeterminado utiliza un ID de estilo de `alloy-prehiding`. El SDK web no es compatible con el fragmento preocultado de at.js, por lo que debe cambiarse como parte del proceso de migración. |
| Representación automática del contenido al cargar la página | Se controla con una configuración global de Target. Habilitado cuando `pageLoadEnabled` se establece en `true`. | Especificado en el SDK web de Platform `sendEvent` comando. Habilitado mediante la configuración de `renderDecisions` opción para `true`. |
| Representación manual del contenido | El `applyOffer()` y `applyOffers()` funciones solo admiten el HTML de configuración | El `applyPropositions` El comando admite la configuración, el reemplazo o la adición del HTML para una mayor flexibilidad |
| Seguimiento de eventos personalizados | Compatible con `trackEvent()` y `sendNotifications()` funciones. Estas funciones son específicas de Target y no afectan a las métricas de Adobe Analytics. | Todos los datos del SDK web de Platform `sendEvent` Las llamadas de se reenvían a Target. Los datos suplementarios necesarios específicamente para Target deben incluirse con el `sendEvent` con un eventType de `decisioning.propositionDisplay` o `decisioning.propositionInteract` para garantizar que las métricas de Adobe Analytics no se vean afectadas. |
| CNAME de Target | Compatible. Es independiente del CNAME utilizado para Analytics y del servicio de ID de Experience Cloud. | Ya no es relevante. Se puede utilizar un único CNAME para todas las llamadas al SDK web de Platform. |
| Depuración | El `mboxDisable`, `mboxDebug`, y `mboxTrace` Los parámetros de URL se pueden utilizar para depurar con las herramientas para desarrolladores del explorador.<br><br>El Adobe Experience Platform Debugger también es una herramienta de depuración compatible. | El `mboxDisable`, `mboxDebug`, y `mboxTrace` No se admiten parámetros de URL.<br><br>Puede activar la depuración del SDK web agregando el `alloy_debug=true` a la cadena de consulta o ejecutando `alloy("setDebug", { "enabled": true });` en la consola de desarrollador.<br><br>La extensión del explorador de Adobe Experience Platform Debugger se puede utilizar para iniciar un seguimiento de Edge para la depuración.<br><br>Consulte la [depurar el SDK web de Platform](debugging.md) para obtener más información. |
| Analytics para Target (A4T) | Utiliza valores SDID para unir las llamadas de Target y Analytics | Compatible de forma nativa sin necesidad de vinculación |

>[!NOTE]
>
>No se admite la migración de Target al SDK web de Platform mientras se mantiene una implementación de Adobe Analytics de AppMeasurement existente para una página determinada.
>
> Es posible migrar la implementación de at.js (y AppMeasurement.js) al SDK web de Platform de una en una. Si sigue este enfoque, es mejor configurar la variable [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) y [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) opciones para `true` con el `configure` comando.

## Funciones de at.js y equivalentes del SDK web de Platform

Muchas funciones de at.js tienen un enfoque equivalente al utilizar el SDK web de Platform que se describe en la siguiente tabla. Para obtener más información sobre [Funciones de at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte la Guía para desarrolladores de Adobe Target.

| Función at.js 2.x | Equivalente de SDK web de Platform |
| --- | --- | 
| `getOffer()` y `getOffers()` | Para solicitar y [procesar automáticamente](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) Experiencias basadas en VEC de Target, use `sendEvent` y establezca el `renderDecisions` opción a true.<br><br>Para solicitar experiencias basadas en formularios o para [procesamiento manual](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) contenido, especifique una matriz de `decisionScopes` (mboxes) con `sendEvent` comando. |
| `applyOffer()` y `applyOffers()` | Utilice el [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) para aplicar contenido. Puede elegir establecer, reemplazar o anexar el HTML a un selector específico. |
| `triggerView()` | El SDK web de Platform almacena automáticamente en déclencheur un [ver cambio](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) SPA a los efectos del VEC de la, si `web.webPageDetails.viewName` se establece en la propiedad `xdm` de la opción `sendEvent` comando. |
| `trackEvent()` y `sendNotifications()` | Utilice el `sendEvent` comando con a [específico `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) set:<br><br>`decisioning.propositionDisplay` indica la renderización de una actividad<br><br>`decisioning.propositionInteract` indica la interacción del usuario con una actividad, como un clic del ratón. |
| `targetGlobalSettings()` | No hay equivalente directo. Consulte la [Comparación de configuración de Target](detailed-comparison.md) para obtener más información. |
| `targetPageParams()` y `targetPageParamsAll()` | Todos los datos pasados en el `xdm` de la opción `sendEvent` El comando se asigna a los parámetros de mbox de Target. Dado que los parámetros de mbox se denominan con notación de puntos serializada, la migración al SDK web de Platform puede requerir la actualización de las audiencias y actividades existentes para utilizar los nuevos nombres de parámetros de mbox. <br><br>Datos pasados como parte de `data.__adobe.target` de la `sendEvent` el comando está asignado a [Parámetros específicos de perfil de Target y Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| Eventos personalizados de at.js | No compatible. Consulte la [hoja de ruta pública](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) para el estado actual. [Tokens de respuesta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) se exponen como parte de la `propositions` en la respuesta de la `sendEvent` llamada. |

## Configuración de at.js y equivalentes del SDK web de Platform

La biblioteca at.js se puede configurar y descargar con varias opciones en la interfaz de usuario de Target. Esta configuración también se puede actualizar con el [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) función. La siguiente tabla compara estas configuraciones con las disponibles con el SDK web de Platform.

| Configuración de at.js | Equivalente de SDK web de Platform |
| --- | --- |
| `bodyHiddenStyle` | Configure las variables [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) con el `configure` mando |
| `bodyHidingEnabled` | Si un `prehidingStyle` se define con la variable `configure` y, a continuación, esta función está habilitada. Si no se define un estilo, el SDK web de Platform no intenta ocultar ningún contenido. |
| `clientCode` | Configurado automáticamente |
| `cookieDomain` | No aplicable |
| `crossDomain` | Configure las variables `thirdPartyCookiesEnabled` opción para `true` con el `configure` para habilitar cookies de origen y de terceros en casos de uso entre dominios |
| `cspScriptNonce` y `cspStyleNonce` | Consulte la documentación de [configuración de un CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | No compatible |
| `decisioningMethod` | Todo el SDK web de Platform `sendEvent` Los comandos de utilizan la toma de decisiones del lado del servidor. No se admite la toma de decisiones híbrida y en el dispositivo. |
| `defaultContentHiddenStyle` y `defaultContentVisibleStyle` | Solo se aplica con at.js 1.x. Al igual que at.js 2.x, cualquier mitigación de parpadeo para experiencias basadas en formularios se puede realizar mediante código personalizado. |
| `deviceIdLifetime` | No compatible. If `targetMigrationEnabled` se establece en `true` con el `configure` , el comando `mbox` La cookie se establece con la duración del dispositivo establecida en 2 años. Este valor no se puede configurar. |
| `enabled` | La funcionalidad de Target se habilita o deshabilita con la configuración del flujo de datos |
| `globalMboxAutoCreate` | Configure las variables `renderDecisions` opción para `true` con el `sendEvent` para recuperar y procesar automáticamente experiencias basadas en VEC.<br><br>Solicite un `decisionScope` para `__view__` si prefiere procesar manualmente experiencias basadas en VEC. |
| `imsOrgId` | Configure las variables `orgId` con el `configure` mando |
| `optinEnabled` y `optoutEnabled` | Consulte el SDK web de Platform [opciones de privacidad](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). El `defaultConsent` se aplica a todas las soluciones de Adobe que admite el SDK web de Platform. |
| `overrideMboxEdgeServer` y `overrideMboxEdgeServerTimeout` | No aplicable. Todas las solicitudes del SDK web de Platform utilizan la red de Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Configure las variables `renderDecisions` opción para `true` con el `sendEvent` mando |
| `secureOnly` | No compatible. El SDK web de Platform establece todas las cookies con la variable `secure` y `sameSite="none"` atributos. |
| `selectorsPollingTimeout` | No compatible. El SDK web de Platform utiliza un valor de 5 segundos. El código personalizado se puede utilizar para procesar contenido manualmente si es necesario. |
| `serverDomain` | Utilice el `edgeDomain` configuración con la variable `configure` mando |
| `telemetryEnabled` | No aplicable |
| `timeout` | No compatible. Se recomienda asegurarse de que cualquier código de mitigación de parpadeo incluya un tiempo de espera adecuado. |
| `viewsEnabled` | No compatible. El contenido de las vistas de Target siempre se recupera en el primer momento `sendEvent()` llamar a si `renderDecisions` se establece en `true` o el `__view__` decisionScope se incluye en la solicitud. |
| `visitorApiTimeout` | No aplicable |


## Comparación del diagrama del sistema

Los siguientes diagramas le ayudarán a comprender las diferencias del flujo de datos entre una implementación de Target con at.js y una implementación con el SDK web de Platform.

### Diagrama del sistema de at.js 2.x

![Comportamiento de at.js 2.0 al cargar la página](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| Llamada | Detalles |
| --- | --- |
| 1 | La llamada devuelve el ID del Experience Cloud (ECID). Si el usuario está autenticado, otra llamada sincroniza el ID de cliente. |
| 2 | La biblioteca at.js se carga sincrónicamente y oculta el cuerpo del documento (at.js también se puede cargar asincrónicamente con un fragmento de ocultamiento previo opcional implementado en la página). |
| 3 | Se realiza una solicitud de carga de página que incluye todos los parámetros configurados, ECID, SDID y el ID de cliente. |
| 4 | Los scripts de perfil se ejecutan y se alimentan del Almacenamiento de perfiles. El Almacenamiento solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de Analytics, Audience Manager, etc.). Los atributos del cliente se envían al Almacenamiento de perfiles en un proceso por lotes. |
| 5 | En función de la dirección URL, los parámetros de solicitud y los datos de perfil, Target decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras. |
| 6 | Contenido dirigido devuelto a la página, incluyendo, de manera opcional, los valores de perfil para una personalización adicional.<br><br>El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.<br><br>El contenido dirigido para futuras vistas de una aplicación de una sola página se almacena en caché en el explorador, por lo que se puede aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. |
| 7 | Datos de Analytics enviados desde la página a los servidores de recopilación de datos. |
| 8 | Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en Target mediante los informes de A4T. |

Consulte la guía para desarrolladores para obtener más información sobre cómo [implementación de Target mediante at.js para aplicaciones de una sola página](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagrama del sistema del SDK web de Platform

![Diagrama de Adobe Target Edge Decisioning con el SDK web de Platform](assets/target-platform-web-sdk.png)

| Llamada | Detalles |
| --- | --- |
| 1 | El dispositivo carga el SDK web de Platform. El SDK web de Platform envía una solicitud a la red perimetral con datos XDM, el ID de entorno de flujos de datos, los parámetros pasados y el ID de cliente (opcional). La página (o los contenedores) está preoculta. |
| 2 | La red perimetral envía la solicitud a los servicios Edge para enriquecerla con el ID de visitante, el consentimiento y otra información de contexto del visitante, como la geolocalización y los nombres descriptivos del dispositivo. |
| 3 | La red perimetral envía la solicitud de personalización enriquecida al perímetro de Target con el ID de visitante y los parámetros pasados. |
| 4 | Se ejecutan los scripts de perfil y se incluyen en el almacenamiento de perfiles de Target. El almacenamiento de perfiles recupera segmentos de la biblioteca de audiencias (por ejemplo, segmentos compartidos de Adobe Analytics, Adobe Audience Manager y Adobe Experience Platform). |
| 5 | En función de los parámetros de la solicitud de la URL y los datos de perfil, Target determina qué actividades y experiencias se mostrarán al visitante en la vista de página actual y en futuras vistas recuperadas previamente. A continuación, Target lo devuelve a la red perimetral. |
| 6 | a. La red perimetral envía la respuesta de personalización de vuelta a la página, incluyendo, de forma opcional, los valores de perfil para una personalización adicional. El contenido personalizado de la página actual se muestra lo más rápido posible y sin parpadeo del contenido predeterminado.<br><br>SPA b. El contenido personalizado para vistas que se muestran como resultado de acciones del usuario en una aplicación de una sola página () se almacena en caché para un procesamiento instantáneo sin llamadas adicionales al servidor.<br><br>c. La red perimetral envía el ID de visitante y otros valores en cookies (por ejemplo, consentimiento, ID de sesión, identidad, comprobación de cookies, personalización, etc.). |
| 7 | La red perimetral reenvía detalles de Analytics for Target (A4T) (metadatos de actividad, experiencia y conversión) al perímetro de Analytics. |

Consulte la guía para desarrolladores para obtener más información sobre cómo [implementar Target mediante el SDK web de Platform para aplicaciones de una sola página](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Después de tener una buena comprensión técnica de la implementación actual de Target y de las funciones que utiliza, el siguiente paso es realizar las siguientes acciones [configuración inicial](initial-setup.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra algún obstáculo con la migración o cree que falta información esencial en esta guía, indíquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
