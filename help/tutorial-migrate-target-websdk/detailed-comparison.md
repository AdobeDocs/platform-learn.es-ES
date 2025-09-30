---
title: 'Comparación de at.js 2.x con Web SDK: Migración de Target de at.js 2.x a Web SDK'
description: Obtenga información sobre las diferencias entre at.js 2.x y Platform Web SDK, incluidas las funciones, la configuración y el flujo de datos.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 7d3c1728925e322f9313cf71f081500e0c0bac0b
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 4%

---

# Comparación de at.js con Platform Web SDK

La biblioteca independiente Adobe Target at.js difiere considerablemente de Platform Web SDK. Las siguientes tablas son una referencia para ayudarle a evaluar las áreas de la implementación en las que puede que tenga que centrarse durante el proceso de migración.

Después de revisar la información que aparece a continuación y evaluar su implementación técnica actual de at.js, debería poder comprender lo siguiente:

- Qué funciones de Target admite Platform Web SDK
- Qué funciones de at.js tienen equivalentes en Platform Web SDK
- Aplicación de la configuración de Target con Platform Web SDK
- Diferencias entre el flujo de datos de at.js y Platform Web SDK

Si es nuevo en Platform Web SDK, no se preocupe: los elementos siguientes se tratan con más detalle a lo largo de este tutorial.

## Comparación de características

| | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Actualizar perfil de Target | Admitido | Admitido |
| Vista de déclencheur para SPA | Admitido | Admitido |
| Recomendaciones de Target | Admitido | Admitido |
| Buscar ofertas basadas en formularios | Admitido | Admitido |
| Seguimiento de eventos | Admitido | Admitido |
| A4T: aplicación de una sola página | Admitido | Admitido |
| A4T: rastreo de clics | Admitido | Admitido |
| A4T: Registro en el lado del cliente | Admitido | Admitido |
| A4T: Registro en el servidor | Admitido | Admitido |
| Aplicar ofertas | Admitido | Admitido |
| Volver a procesar la vista en SPA sin notificaciones | Admitido | Admitido |
| Aplicaciones híbridas | Admitido | Admitido |
| URL de QA | Admitido | Admitido |
| ID de terceros de Mbox | Admitido | Admitido |
| Atributos del cliente | Admitido | Admitido |
| Ofertas remotas | Admitido | Admitido parcialmente. No se admiten ofertas remotas dinámicas. |
| Ofertas de redirección | Admitido | Compatible. Sin embargo, no se admite el redireccionamiento de una página con Platform Web SDK a una página con at.js (y en la dirección opuesta). |
| Toma de decisiones en el dispositivo | Admitido | Actualmente no es compatible |
| Mboxes de recuperación previa | Compatible con ámbitos personalizados y VEC de SPA | La recuperación previa es el modo predeterminado para Web SDK |
| Eventos personalizados | Admitido | No compatible. Consulte la [hoja de ruta pública](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"}) para ver el estado actual. |
| Tokens de respuesta | Admitido | Compatible. Consulte la [documentación de tokens de respuesta específicos](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) para ver ejemplos de código y las diferencias entre at.js y Platform Web SDK |
| Proveedores de datos | Admitido | No compatible. Se puede usar código personalizado para almacenar en déclencheur un comando de Platform Web SDK `sendEvent` después de recuperar datos de otro proveedor. |


## Llamadas dignas de mención

| | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Mitigación de parpadeo | El fragmento preocultado para implementaciones asincrónicas usa un id. de estilo de `at-body-style`. at.js busca este ID de elemento para eliminar el estilo una vez que se reciba una respuesta. | El fragmento preocultado predeterminado utiliza un identificador de estilo de `alloy-prehiding`. Web SDK no es compatible con el fragmento preocultado at.js, por lo que debe cambiarse como parte del proceso de migración. |
| Representación automática del contenido al cargar la página | Se controla con una configuración global de Target. Se habilitó cuando `pageLoadEnabled` está establecido en `true`. | Especificado en el comando de Platform Web SDK `sendEvent`. Se habilitó al establecer la opción `renderDecisions` en `true`. |
| Representación manual del contenido | Las funciones `applyOffer()` y `applyOffers()` admiten la configuración de HTML solamente | El comando `applyPropositions` admite la configuración, el reemplazo o la adición de HTML para una mayor flexibilidad |
| Seguimiento de eventos personalizados | Compatible con las funciones `trackEvent()` y `sendNotifications()`. Estas funciones son específicas de Target y no afectan a las métricas de Adobe Analytics. | Todos los datos de las llamadas de Platform Web SDK `sendEvent` se reenvían a Target. Los datos adicionales necesarios específicamente para Target deben incluirse con el comando `sendEvent` con un eventType de `decisioning.propositionDisplay` o `decisioning.propositionInteract` para garantizar que las métricas de Adobe Analytics no se vean afectadas. |
| CNAME de Target | Compatible. Es independiente del CNAME utilizado para Analytics y del servicio de Experience Cloud ID. | Ya no es relevante. Se puede utilizar un único CNAME para todas las llamadas de Platform Web SDK. |
| Depuración | Los parámetros de URL `mboxDisable`, `mboxDebug` y `mboxTrace` se pueden usar para la depuración con las herramientas para desarrolladores del explorador.<br><br>Adobe Experience Platform Debugger también es una herramienta de depuración compatible. | No se admiten los parámetros de dirección URL `mboxDisable`, `mboxDebug` y `mboxTrace`.<br><br>Puede activar la depuración de Web SDK agregando `alloy_debug=true` a la cadena de consulta o ejecutando `alloy("setDebug", { "enabled": true });` en la consola de desarrollador.<br><br>La extensión del explorador Adobe Experience Platform Debugger se puede usar para iniciar un seguimiento de Edge para la depuración.<br><br>Consulte la documentación de [depuración de Platform Web SDK](debugging.md) para obtener más información. |
| Analytics para Target (A4T) | Utiliza valores SDID para unir las llamadas de Target y Analytics | Compatible de forma nativa sin necesidad de vinculación |

>[!NOTE]
>
>No se admite la migración de Target a Platform Web SDK mientras se conserva una implementación de AppMeasurement Adobe Analytics existente para una página determinada.
>
> Es posible migrar la implementación de at.js (y AppMeasurement.js) a Platform Web SDK de página en página. Si adopta este enfoque, es mejor establecer las opciones [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) y [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) en `true` con el comando `configure`.

## Funciones de at.js y equivalentes de Platform Web SDK

Muchas funciones de at.js tienen un enfoque equivalente al utilizar Platform Web SDK que se describe en la siguiente tabla. Para obtener más información sobre las [funciones de at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte la Guía para desarrolladores de Adobe Target.

| Función at.js 2.x | Equivalente de Platform Web SDK |
| --- | --- | 
| `getOffer()` y `getOffers()` | Para solicitar y [procesar automáticamente](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) experiencias basadas en VEC de Target, use el comando `sendEvent` y establezca la opción `renderDecisions` en true.<br><br>Para solicitar experiencias basadas en formularios o [procesar contenido](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) manualmente, especifique una matriz de `decisionScopes` (mboxes) con el comando `sendEvent`. |
| `applyOffer()` y `applyOffers()` | Utilice el comando [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) para aplicar contenido. Puede elegir establecer, reemplazar o anexar HTML a un selector específico. |
| `triggerView()` | Platform Web SDK almacena automáticamente en déclencheur un [cambio de vista](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) a los efectos del VEC de SPA si la propiedad `web.webPageDetails.viewName` está establecida en la opción `xdm` del comando `sendEvent`. |
| `trackEvent()` y `sendNotifications()` | Usar el comando `sendEvent` con un conjunto [specific `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events):<br><br>`decisioning.propositionDisplay` indica la representación de una actividad<br><br>`decisioning.propositionInteract` indica una interacción del usuario con una actividad, como un clic del mouse (ratón). |
| `targetGlobalSettings()` | No hay equivalente directo. Consulte la [comparación de la configuración de Target](detailed-comparison.md) para obtener más detalles. |
| `targetPageParams()` y `targetPageParamsAll()` | Todos los datos pasados en la opción `xdm` del comando `sendEvent` se asignan a parámetros de mbox de Target. Dado que los parámetros de mbox se denominan con notación de puntos serializada, la migración a Platform Web SDK puede requerir la actualización de las audiencias y actividades existentes para utilizar los nuevos nombres de parámetros de mbox. <br><br>Los datos pasados como parte de `data.__adobe.target` del comando `sendEvent` se han asignado a [parámetros específicos del perfil de Target y de Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| Eventos personalizados de at.js | No compatible. Consulte la [hoja de ruta pública](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"}) para ver el estado actual. [Los tokens de respuesta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) se exponen como parte de `propositions` en la respuesta de la llamada a `sendEvent`. |

## Configuración de at.js y equivalentes de Platform Web SDK

La biblioteca at.js se puede configurar y descargar con varias opciones en la interfaz de usuario de Target. Esta configuración también se puede actualizar con la función [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/). La siguiente tabla compara estas configuraciones con las disponibles con Platform Web SDK.

| Configuración de at.js | Equivalente de Platform Web SDK |
| --- | --- |
| `bodyHiddenStyle` | Establecer [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) con el comando `configure` |
| `bodyHidingEnabled` | Si se define un(a) `prehidingStyle` con el comando `configure`, entonces esta característica está habilitada. Si no se define un estilo, Platform Web SDK no intenta ocultar ningún contenido. |
| `clientCode` | Configurado automáticamente |
| `cookieDomain` | No aplicable |
| `crossDomain` | Establezca la opción `thirdPartyCookiesEnabled` en `true` con el comando `configure` para habilitar las cookies de origen y de terceros en los casos de uso entre dominios |
| `cspScriptNonce` y `cspStyleNonce` | Consulte la documentación para [configurar un CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | No compatible |
| `decisioningMethod` | Todos los comandos de Platform Web SDK `sendEvent` utilizan la toma de decisiones del lado del servidor. No se admite la toma de decisiones híbrida y en el dispositivo. |
| `defaultContentHiddenStyle` y `defaultContentVisibleStyle` | Solo se aplica con at.js 1.x. Al igual que at.js 2.x, cualquier mitigación de parpadeo para experiencias basadas en formularios se puede realizar mediante código personalizado. |
| `deviceIdLifetime` | No compatible. Si `targetMigrationEnabled` se establece en `true` con el comando `configure`, la cookie `mbox` se establece con la duración del dispositivo establecida en 2 años. Este valor no se puede configurar. |
| `enabled` | La funcionalidad de Target se habilita o deshabilita con la configuración del flujo de datos |
| `globalMboxAutoCreate` | Establezca la opción `renderDecisions` en `true` con el comando `sendEvent` para recuperar y procesar automáticamente experiencias basadas en VEC.<br><br>Solicite un `decisionScope` para `__view__` si prefiere procesar manualmente experiencias basadas en VEC. |
| `imsOrgId` | Establecer `orgId` con el comando `configure` |
| `optinEnabled` y `optoutEnabled` | Consulte las [opciones de privacidad](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html) de Platform Web SDK. La opción `defaultConsent` se aplica a todas las soluciones de Adobe que admite Platform Web SDK. |
| `overrideMboxEdgeServer` y `overrideMboxEdgeServerTimeout` | No aplicable. Todas las solicitudes de Platform Web SDK utilizan la red de Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Establecer la opción `renderDecisions` en `true` con el comando `sendEvent` |
| `secureOnly` | No compatible. Platform Web SDK establece todas las cookies con los atributos `secure` y `sameSite="none"`. |
| `selectorsPollingTimeout` | No compatible. Platform Web SDK utiliza un valor de 5 segundos. El código personalizado se puede utilizar para procesar contenido manualmente si es necesario. |
| `serverDomain` | Usar la configuración `edgeDomain` con el comando `configure` |
| `telemetryEnabled` | No aplicable |
| `timeout` | No compatible. Se recomienda asegurarse de que cualquier código de mitigación de parpadeo incluya un tiempo de espera adecuado. |
| `viewsEnabled` | No compatible. El contenido de las vistas de Target siempre se recupera en la primera llamada de `sendEvent()` si `renderDecisions` se establece en `true` o si `__view__` decisionScope se incluye en la solicitud. |
| `visitorApiTimeout` | No aplicable |


## Comparación del diagrama del sistema

Los siguientes diagramas le ayudarán a comprender las diferencias del flujo de datos entre una implementación de Target con at.js y una implementación con Platform Web SDK.

### Diagrama del sistema de at.js 2.x

![comportamiento de at.js 2.0 al cargar la página](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| Llamada | Detalles |
| --- | --- |
| 1 | La llamada devuelve el ID de Experience Cloud (ECID). Si el usuario está autenticado, otra llamada sincroniza el ID de cliente. |
| 2 | La biblioteca at.js se carga sincrónicamente y oculta el cuerpo del documento (at.js también se puede cargar asincrónicamente con un fragmento de ocultamiento previo opcional implementado en la página). |
| 3 | Se realiza una solicitud de carga de página que incluye todos los parámetros configurados, ECID, SDID y el ID de cliente. |
| 4 | Los scripts de perfil se ejecutan y se alimentan del Almacenamiento de perfiles. El Almacenamiento solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de Analytics, Audience Manager, etc.). Los atributos del cliente se envían al Almacenamiento de perfiles en un proceso por lotes. |
| 5 | En función de la dirección URL, los parámetros de solicitud y los datos de perfil, Target decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras. |
| 6 | Contenido dirigido devuelto a la página, incluyendo, de manera opcional, los valores de perfil para una personalización adicional.<br><br>El contenido dirigido en la página actual se muestra lo más rápido posible y sin parpadeo del contenido predeterminado.<br><br>El contenido dirigido para vistas futuras de una aplicación de una sola página se almacena en caché en el explorador, por lo que se puede aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. |
| 7 | Datos de Analytics enviados desde la página a los servidores de recopilación de datos. |
| 8 | Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en Target mediante los informes de A4T. |

Consulte la guía para desarrolladores para obtener más información sobre cómo [implementar Target mediante at.js para aplicaciones de una sola página](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagrama del sistema de Platform Web SDK

![Diagrama de la toma de decisiones perimetral de Adobe Target con Platform Web SDK](assets/target-platform-web-sdk.png)

| Llamada | Detalles |
| --- | --- |
| 1 | El dispositivo carga Platform Web SDK. Platform Web SDK envía una solicitud a la red perimetral con datos XDM, el ID de entorno de flujos de datos, los parámetros transferidos y el ID de cliente (opcional). La página (o los contenedores) está preoculta. |
| 2 | La red perimetral envía la solicitud a los servicios Edge para enriquecerla con el ID de visitante, el consentimiento y otra información de contexto del visitante, como la geolocalización y los nombres descriptivos del dispositivo. |
| 3 | La red perimetral envía la solicitud de personalización enriquecida al perímetro de Target con el ID de visitante y los parámetros pasados. |
| 4 | Se ejecutan los scripts de perfil y se incluyen en el almacenamiento de perfiles de Target. El almacenamiento de perfiles recupera segmentos de la biblioteca de audiencias (por ejemplo, segmentos compartidos de Adobe Analytics, Adobe Audience Manager y Adobe Experience Platform). |
| 5 | En función de los parámetros de la solicitud de la URL y los datos de perfil, Target determina qué actividades y experiencias se mostrarán al visitante en la vista de página actual y en futuras vistas recuperadas previamente. A continuación, Target lo devuelve a la red perimetral. |
| 6 | a. La red perimetral envía la respuesta de personalización de vuelta a la página, incluyendo, de forma opcional, los valores de perfil para una personalización adicional. El contenido personalizado de la página actual se muestra lo más rápido posible y sin parpadeo del contenido predeterminado.<br><br>b. El contenido personalizado para vistas que se muestran como resultado de acciones del usuario en una aplicación de una sola página (SPA) se almacena en caché para un procesamiento instantáneo sin llamadas al servidor adicionales.<br><br>c. La red perimetral envía el ID de visitante y otros valores en cookies (por ejemplo, consentimiento, ID de sesión, identidad, comprobación de cookies, personalización, etc.). |
| 7 | La red perimetral reenvía detalles de Analytics for Target (A4T) (metadatos de actividad, experiencia y conversión) al perímetro de Analytics. |

Consulte la guía para desarrolladores para obtener más información sobre cómo [implementar Target mediante Platform Web SDK para aplicaciones de una sola página](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Después de tener una buena comprensión técnica de su implementación actual de Target y de las características que utiliza, el siguiente paso es realizar la [configuración inicial](initial-setup.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con la migración de Target de at.js a Web SDK. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
