---
title: Comparación de at.js 2.x con el SDK web | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre las diferencias entre at.js 2.x y el SDK web de Platform, incluidas las funciones, la configuración y el flujo de datos.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Comparación de at.js con el SDK web de Platform

La biblioteca independiente at.js de Adobe Target difiere considerablemente del SDK web de Platform. Las siguientes tablas son una referencia para ayudarle a evaluar áreas de la implementación en las que puede necesitar centrarse durante el proceso de migración.

Después de revisar la información siguiente y evaluar su implementación técnica actual de at.js, debe ser capaz de comprender lo siguiente:

- ¿Qué funciones de Target admite el SDK web de Platform?
- Qué funciones de at.js tienen equivalentes en el SDK web de plataforma
- Aplicación de la configuración de Target con el SDK web de Platform
- Diferencia entre el flujo de datos de at.js y el SDK web de plataforma

Si es nuevo en el SDK web de Platform, no se preocupe: los elementos siguientes se tratan con más detalle en este tutorial.

## Comparación de características

|  | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Actualizar perfil de Target | Admitido | Admitido |
| vista déclencheur para SPA | Admitido | Admitido |
| Target Recommendations | Admitido | Admitido |
| Recuperar ofertas basadas en formularios | Admitido | Admitido |
| Seguimiento de eventos | Admitido | Admitido |
| A4T: Aplicación de una sola página | Admitido | Admitido |
| A4T: Rastreo de clics | Admitido | Admitido |
| A4T: Registro en el lado del cliente | Admitido | Admitido |
| A4T: Registro en el lado del servidor | Admitido | Admitido |
| Aplicar ofertas | Admitido | Admitido |
| Volver a procesar la vista en SPA sin notificaciones | Admitido | Admitido |
| Aplicaciones híbridas | Admitido | Admitido |
| URL de control de calidad | Admitido | Admitido |
| ID de terceros de mbox | Admitido | Admitido |
| Atributos del cliente | Admitido | Compatible |
| Ofertas remotas | Admitido | Admitido |
| Ofertas de redireccionamiento | Admitido | Admitido. Sin embargo, no se admite la redirección de una página con el SDK web de Platform a una página con at.js (y en la dirección opuesta). |
| Toma de decisiones en el dispositivo | Admitido | No admitido actualmente |
| Recuperación previa de mboxes | Admitido | Parcialmente compatible. Póngase en contacto con el servicio de atención al cliente para habilitar esta función, ya que altera el comportamiento de recuperación previa de la actividad. |
| Eventos personalizados | Admitido | Se admite parcialmente mediante [monitorización de enlaces](https://github.com/adobe/alloy/wiki/Monitoring-Hooks) |
| Tokens de respuesta | Admitido | Admitido. Consulte la [documentación dedicada de tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) para ver ejemplos de código y diferencias entre at.js y el SDK web de plataforma |
| Proveedores de datos   | Admitido | No admitido. Se puede utilizar código personalizado para almacenar en déclencheur un SDK web de plataforma `sendEvent` después de recuperar los datos de otro proveedor. |


## Llamadas importantes

|  | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Mitigación del parpadeo | El fragmento de preocultación para implementaciones asíncronas utiliza un ID de estilo de `at-body-style`. at.js busca este ID de elemento para eliminar el estilo una vez que se recibe una respuesta. | El fragmento predeterminado de preocultación utiliza un ID de estilo de `alloy-prehiding`. El SDK web no es compatible con el fragmento de preocultación de at.js, por lo que debe cambiarse como parte del proceso de migración. |
| Representación automática del contenido al cargar la página | Controlado con una configuración global de Target. Habilitado cuando `pageLoadEnabled` está configurado como `true`. | Especificado en el SDK web de Platform `sendEvent` comando. Habilitado configurando la variable `renderDecisions` a `true`. |
| Representación manual de contenido | La variable `applyOffer()` y `applyOffers()` solo admite HTML de configuración | La variable `applyPropositions` admite la configuración, sustitución o adición de un HTML para una mayor flexibilidad |
| Seguimiento de eventos personalizados | Admitido con `trackEvent()` y `sendNotifications()` funciones. Estas funciones son específicas de Target y no afectan a las métricas de Adobe Analytics. | Todos los datos del SDK web de Platform `sendEvent` las llamadas de se reenvían a Target. Los datos adicionales necesarios específicamente para Target deben incluirse en la `sendEvent` con un eventType de `decisioning.propositionDisplay` o `decisioning.propositionInteract` para garantizar que las métricas de Adobe Analytics no se vean afectadas. |
| CNAME de Target | Admitido. Es independiente del CNAME utilizado para Analytics y del servicio de ID de Experience Cloud. | Ya no es relevante. Se puede utilizar un solo CNAME para todas las llamadas del SDK web de la plataforma. |
| Depuración | La variable `mboxDisable`, `mboxDebug`y `mboxTrace` Los parámetros de URL se pueden usar para depurar con las herramientas para desarrolladores del explorador.<br><br>Adobe Experience Platform Debugger es también una herramienta de depuración compatible. | La variable `mboxDisable`, `mboxDebug`y `mboxTrace` No se admiten los parámetros de URL.<br><br>Puede activar la depuración del SDK web añadiendo la variable `alloy_debug=true` a su cadena de consulta o ejecutando `alloy("setDebug", { "enabled": true });` en la consola del desarrollador.<br><br>La extensión del explorador de Adobe Experience Platform Debugger se puede utilizar para iniciar un seguimiento perimetral para la depuración.<br><br>Consulte la [depuración del SDK web de Platform](debugging.md) documentación para obtener más información. |
| Analytics para Target (A4T) | Utiliza valores SDID para unir llamadas de Target y Analytics | Compatibilidad nativa sin necesidad de unión |

>[!NOTE]
>
>No se admite la migración de Target al SDK web de la plataforma mientras se conserva una implementación de Adobe Analytics de AppMeasurement existente para una página determinada.
>
> Es posible migrar la implementación de at.js (y AppMeasurement.js) al SDK web de plataforma de una página a la vez. Si sigue este enfoque, es mejor configurar la variable [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) y [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) opciones `true` con la variable `configure` comando.

## Funciones de at.js y equivalentes del SDK web de plataforma

Muchas funciones de at.js tienen un enfoque equivalente mediante el SDK web de Platform que se describe en la tabla siguiente. Para obtener más información sobre la variable [Funciones de at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte la guía para desarrolladores de Adobe Target.

| Función at.js 2.x | Equivalente del SDK web de la plataforma |
| --- | --- | 
| `getOffer()` y `getOffers()` | Para solicitar y [procesar automáticamente](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) Dirija las experiencias basadas en VEC y utilice la variable `sendEvent` y configure la variable `renderDecisions` como true.<br><br>Para solicitar experiencias basadas en formularios o para [renderización manual](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) contenido, especifique una matriz de `decisionScopes` (mboxes) con la variable `sendEvent` comando. |
| `applyOffer()` y `applyOffers()` | Utilice la variable [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) para aplicar contenido. Puede elegir establecer, reemplazar o anexar un HTML a un selector específico. |
| `triggerView()` | Platform Web SDK déclencheur automáticamente un [cambio de vista](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) a efectos del VEC SPA si `web.webPageDetails.viewName` se establece en `xdm` de `sendEvent` comando. |
| `trackEvent()` y `sendNotifications()` | Utilice la variable `sendEvent` con un [específico `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) configurado:<br><br>`decisioning.propositionDisplay` indica la renderización de una actividad<br><br>`decisioning.propositionInteract` indica la interacción del usuario con una actividad, como un clic del ratón. |
| `targetGlobalSettings()` | Sin equivalente directo. Consulte la [Comparación de la configuración de Target](detailed-comparison.md) para obtener más información. |
| `targetPageParams()` y `targetPageParamsAll()` | Todos los datos pasados a la `xdm` de `sendEvent` está asignado a los parámetros de mbox de Target. Dado que los parámetros de mbox reciben notación de puntos serializada, la migración al SDK web de Platform puede requerir que actualice las audiencias y actividades existentes para que utilicen los nuevos nombres de parámetros de mbox. <br><br>Datos pasados como parte de `data.__adobe.target` del `sendEvent` está asignado a [Perfil de Target y parámetros específicos de Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| Eventos personalizados de at.js | No admitido. Sin embargo, [tokens de respuesta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) se exponen como parte del `propositions` en respuesta a la `sendEvent` llamada a . |

## Configuración de at.js y equivalentes del SDK web de plataforma

La biblioteca at.js se puede configurar y descargar con varias configuraciones en la interfaz de usuario de Target. Esta configuración también se puede actualizar con la variable [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) función. La siguiente tabla compara estos ajustes con los disponibles con el SDK web de Platform.

| Configuración de at.js | Equivalente del SDK web de la plataforma |
| --- | --- |
| `bodyHiddenStyle` | Configure las variables [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) con la variable `configure` command |
| `bodyHidingEnabled` | Si `prehidingStyle` se define con la variable `configure` , esta función está habilitada. Si no se define un estilo, el SDK web de Platform no intenta ocultar ningún contenido. |
| `clientCode` | Configurado automáticamente |
| `cookieDomain` | No aplicable |
| `crossDomain` | Configure las variables `thirdPartyCookiesEnabled` a `true` con la variable `configure` para habilitar las cookies de origen y de terceros en los casos de uso entre dominios |
| `cspScriptNonce` y `cspStyleNonce` | Consulte la documentación de [configuración de un CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | No admitido |
| `decisioningMethod` | Todos los SDK web de Platform `sendEvent` utilizan la toma de decisiones del lado del servidor. No se admite la toma de decisiones híbrida y en dispositivos. |
| `defaultContentHiddenStyle` y `defaultContentVisibleStyle` | Solo aplicable con at.js 1.x. Al igual que at.js 2.x, cualquier mitigación de parpadeo para experiencias basadas en formularios se puede realizar mediante código personalizado. |
| `deviceIdLifetime` | No admitido. If `targetMigrationEnabled` está configurado como `true` con la variable `configure` el comando `mbox` se establece con la duración del dispositivo establecida en 2 años. Este valor no se puede configurar. |
| `enabled` | La funcionalidad de Target está habilitada o deshabilitada con la configuración del flujo de datos |
| `globalMboxAutoCreate` | Configure las variables `renderDecisions` a `true` con la variable `sendEvent` para recuperar y procesar automáticamente experiencias basadas en VEC.<br><br>Solicitar un `decisionScope` para `__view__` si prefiere renderizar manualmente experiencias basadas en VEC. |
| `imsOrgId` | Configure las variables `orgId` con la variable `configure` command |
| `optinEnabled` y `optoutEnabled` | Consulte el SDK web de Platform [opciones de privacidad](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). La variable `defaultConsent` se aplica a todas las soluciones de Adobe compatibles con el SDK web de Platform. |
| `overrideMboxEdgeServer` y `overrideMboxEdgeServerTimeout` | No aplicable. Todas las solicitudes del SDK web de Platform utilizan la red Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Configure las variables `renderDecisions` a `true` con la variable `sendEvent` command |
| `secureOnly` | No admitido. El SDK web de Platform establece todas las cookies con la variable `secure` y `sameSite="none"` atributos. |
| `selectorsPollingTimeout` | No admitido. El SDK web de Platform utiliza un valor de 5 segundos. El código personalizado se puede utilizar para procesar contenido manualmente si es necesario. |
| `serverDomain` | Utilice la variable `edgeDomain` con la variable `configure` command |
| `telemetryEnabled` | No aplicable |
| `timeout` | No admitido. Se recomienda asegurarse de que cualquier código de mitigación de parpadeo incluya un tiempo de espera adecuado. |
| `viewsEnabled` | No admitido. El contenido de las vistas de Target siempre se obtiene en la primera `sendEvent()` call if `renderDecisions` está configurado como `true` o `__view__` decisionScope se incluye en la solicitud. |
| `visitorApiTimeout` | No aplicable |


## Comparación del diagrama del sistema

Los siguientes diagramas deberían ayudarle a comprender las diferencias de flujo de datos entre una implementación de Target que utiliza at.js y una implementación que utiliza el SDK web de Platform.

### Diagrama del sistema de at.js 2.x

![Comportamiento de at.js 2.0 al cargar la página](assets/target-at-js-2x-diagram.png)

| La llamada | Detalles |
| --- | --- |
| 1 | La llamada devuelve un ID de Experience Cloud (ECID). Si el usuario está autenticado, otra llamada sincroniza el ID del cliente. |
| 2 | La biblioteca at.js carga de forma sincrónica y oculta el cuerpo del documento (at.js también se puede cargar de forma asíncrona con un fragmento de ocultamiento previo opcional implementado en la página). |
| 3 | La solicitud de carga de página se realiza incluyendo todos los parámetros configurados, ECID, SDID y el ID de cliente. |
| 4 | Los scripts de perfil se ejecutan y se incluyen en el Almacenamiento de perfiles. El Almacenamiento solicita audiencias de la Biblioteca de audiencias que cumplan los requisitos (por ejemplo, audiencias compartidas de Analytics, Audience Manager, etc.). Los Atributos del cliente se envían al Almacenamiento de perfiles en un proceso por lotes. |
| 5 | En función de la dirección URL, los parámetros de solicitud y los datos de perfil, Target decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras. |
| 6 | Contenido dirigido devuelto a la página, incluyendo de forma opcional los valores de perfil para una personalización adicional.<br><br>El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.<br><br>El contenido dirigido para vistas futuras de una aplicación de una sola página se almacena en caché en el explorador, por lo que se puede aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. (Consulte el siguiente diagrama para ver el comportamiento triggerView() ). |
| 7 | Datos de Analytics enviados desde la página a los servidores de recopilación de datos. |
| 8 | Se comparan los datos de Target con los datos de Analytics mediante el SDID y se procesan en el almacén de informes de Analytics. Por lo tanto, los datos de Analytics se pueden visualizar tanto en Analytics como en Target mediante los informes de A4T. |

Consulte la guía para desarrolladores para obtener más información sobre cómo [implementar Target mediante at.js para aplicaciones de una sola página](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagrama del sistema del SDK web de Platform

![Diagrama de la toma de decisiones perimetrales de Adobe Target con el SDK web de Platform](assets/target-platform-web-sdk.png)

| La llamada | Detalles |
| --- | --- |
| 1 | El dispositivo carga el SDK web de Platform. El SDK web de Platform envía una solicitud a la red perimetral con datos XDM, el ID de entorno de Datastreams, parámetros transferidos y el ID de cliente (opcional). La página (o contenedores) está oculta previamente. |
| 2 | La red perimetral envía la solicitud a los servicios Edge para enriquecerla con el ID del visitante, el consentimiento y otra información de contexto del visitante, como la geolocalización y los nombres descriptivos del dispositivo. |
| 3 | La red perimetral envía la solicitud de personalización enriquecida al perímetro de Target con el ID de visitante y los parámetros transferidos. |
| 4 | Los scripts de perfil se ejecutan y luego se incluyen en el almacenamiento de perfiles de Target. El almacenamiento de perfiles obtiene segmentos de la biblioteca de audiencias (por ejemplo, segmentos compartidos desde Adobe Analytics, Adobe Audience Manager y Adobe Experience Platform). |
| 5 | En función de los parámetros de solicitud de URL y los datos de perfil, Target determina qué actividades y experiencias se mostrarán para el visitante en la vista de página actual y para futuras vistas de recuperación previa. A continuación, Target lo devuelve a la red perimetral. |
| 6 | a. La red perimetral envía la respuesta de personalización a la página, incluyendo de forma opcional los valores de perfil para una personalización adicional. El contenido personalizado de la página actual se muestra lo más rápido posible y sin parpadeo del contenido predeterminado.<br><br>b. El contenido personalizado para las vistas que se muestran como resultado de acciones del usuario en una aplicación de una sola página (SPA) se almacena en caché para el procesamiento instantáneo sin llamadas al servidor adicionales.<br><br>c. La red perimetral envía el ID de visitante y otros valores en cookies (por ejemplo, consentimiento, ID de sesión, identidad, comprobación de cookies, personalización, etc.). |
| 7 | La red perimetral reenvía los detalles de Analytics for Target (A4T) (actividad, experiencia y metadatos de conversión) al perímetro de Analytics. |

Consulte la guía para desarrolladores para obtener más información sobre cómo [implementación de Target mediante el SDK web de Platform para aplicaciones de una sola página](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Una vez que conozca bien la implementación actual de Target y las funciones que utiliza, el siguiente paso es realizar la [configuración inicial](initial-setup.md).

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
