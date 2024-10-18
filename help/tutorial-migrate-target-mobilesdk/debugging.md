---
title: 'Depuración: migración de Adobe Target a Adobe Journey Optimizer, extensión de Decisioning Mobile'
description: Obtenga información sobre cómo depurar una implementación de Adobe Target mediante el SDK para móviles de Adobe Experience Platform.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 3%

---

# Depurar Target con el SDK de Platform Mobile

Verificar las actividades de Target y depurar el SDK móvil para solucionar problemas de implementación, entrega de contenido o calificación de audiencia. En esta página de la guía de migración se explican las diferencias entre la depuración con at.js y el SDK web de Platform.

La tabla siguiente resume las funciones y la compatibilidad con los enfoques de prueba y depuración.

| Función o herramienta | Compatibilidad con at.js | Compatibilidad con SDK web de Platform |
| --- | --- | --- |
| URL de QA de actividad | Sí | Sí |
| `mboxDisable` parámetro de URL | Sí | Consulte la siguiente información para [deshabilitar la funcionalidad de Target](#disable-target-functionality) |
| `mboxDebug` parámetro de URL | Sí | Usar parámetro `alloy_debug` para información de depuración similar |
| `mboxTrace` parámetro de URL | Sí | Utilice la extensión del explorador de Experience Platform Debugger. |
| extensión de Adobe Experience Platform Debugger | Sí | Sí |
| `alloy_debug` parámetro de URL | No aplicable | Sí |
| Adobe Experience Platform Assurance | No aplicable | Sí |

## extensión del explorador de Adobe Experience Platform Debugger

La extensión de Adobe Experience Platform Debugger para Chrome y Firefox examina sus páginas web y le ayuda a validar las implementaciones de Adobe Experience Cloud.

Puede ejecutar Platform Debugger en cualquier página web y la extensión tendrá acceso a los datos públicos. Para acceder a datos que no son públicos mediante la extensión, como la información de seguimiento de Target, debe autenticarse en el Experience Cloud a través del vínculo **[!UICONTROL Iniciar sesión]**.


## Previsualización de actividades de Target con direcciones URL de control de calidad

Tanto at.js como el SDK web de Platform le permiten previsualizar actividades de Target mediante direcciones URL de control de calidad de Target, y ambos métodos de implementación admiten las mismas funciones de control de calidad.

Direcciones URL de control de calidad de Target que funcionan indicando a at.js o al SDK web de Platform que escriban una cookie específica en el explorador denominada `at_qa_mode`. Esta cookie se utiliza para forzar la calificación para una actividad y experiencia en particular.

>[!CAUTION]
>
>La funcionalidad del modo de control de calidad de Target es compatible con la versión 2.13.0 o superior del SDK web de Platform. El modo de control de calidad de destino está habilitado en función del valor `xdm.web.webPageDetails.URL` pasado en la llamada `sendEvent`. Cualquier modificación en este valor, como la reversión en minúsculas de todos los caracteres, puede impedir que el modo de control de calidad de Target funcione correctamente.

Consulte la guía dedicada para obtener más información sobre el control de calidad de la actividad de [Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).

## Implementación de Debug Target

En la tabla siguiente se describen las diferencias entre at.js y las tácticas de depuración del SDK web de Platform:

| Función at.js | Equivalente de SDK web de Platform |
| --- | --- |
| **Mbox Disable** - deshabilitar Target para que no recupere ni procese para comprobar si la página está dañada sin interacciones de Target<br><br>Cargar página con parámetro de URL: `mboxDisable=true` | No hay equivalente directo. Puede bloquear todas las solicitudes del SDK web de Platform con las herramientas para desarrolladores del explorador. |
| **Depuración de mbox**: registra todas las acciones de at.js en la consola del explorador para solucionar los problemas de procesamiento<br><br>Cargar página con parámetro de URL: `mboxDebug=true` | **Alloy Debug**: registra acciones detalladas del SDK, incluidas, entre otras, las acciones de personalización de Target.<br><br>Cargar página con parámetro de URL: `alloy_debug=true` <br /><br />O ejecutar `alloy("setDebug", { "enabled": true });` en la consola de desarrollador |
| **Seguimiento de Target**: con un token de seguimiento de mbox generado en la interfaz de usuario de Target, hay disponible un objeto de seguimiento con detalles que participaron en el proceso de toma de decisiones en el objeto `window.___target_trace`.<br><br>Cargar página con el parámetro de URL: `mboxTrace=window&authorization={TOKEN}` | Utilice la extensión de Adobe Experience Platform Debugger o Platform Assurance. |

>[!NOTE]
>
>Todas las funciones de depuración de at.js enumeradas anteriormente están disponibles con funciones mejoradas en Adobe Experience Platform Debugger.

### Deshabilitar funcionalidad de Target

En la actualidad, el SDK web de Platform no tiene una función para suprimir selectivamente las respuestas de Target. Sin embargo, es posible suprimir las solicitudes del SDK web de Platform con las herramientas para desarrolladores del explorador, varias extensiones del explorador o aplicaciones de terceros. Por ejemplo, para bloquear el SDK web de Platform con Google Chrome:

1. Haga clic con el botón derecho en cualquier lugar de la página y seleccione **Inspect**
1. Seleccione la ficha **Red**
1. Filtre por la cadena `//ee//` para ver solo las llamadas del SDK web de Platform
1. Volver a cargar la página
1. Haga clic con el botón derecho en una de las solicitudes de red filtradas y seleccione **Bloquear dominio de solicitud**
1. Vuelva a cargar la página y observe que la solicitud de red está bloqueada
1. Cuando haya terminado de depurar, haga clic con el botón derecho en la solicitud de red bloqueada y seleccione **Desbloquear** o cierre el panel Herramientas para desarrolladores

### Ver registro de depuración

El registro de depuración para at.js mediante el parámetro de URL `mboxDebug=true` muestra información detallada sobre cada solicitud, respuesta e intento de Target de procesar el contenido en la página. El SDK web de Platform tiene un registro de depuración similar que utiliza el parámetro de URL `alloy_debug=true`.

| Información registrada | at.js (`mboxDebug=true`) | SDK web de Platform (`alloy_debug=true`) |
| --- | --- | --- |
| Prefijo de registro para filtrado | `AT:` | `[alloy]` |
| Detalles de solicitud de carga de página | Sí | Sí |
| Detalles de solicitud de ámbito o mbox | Sí | Sí |
| Estado de solicitud | Sí | Sí |
| Detalles de respuesta | Sí | Sí |
| Estado de procesamiento | Éxito y errores | Solo errores |
| Detalles de procesamiento | Sí | Sí |

>[!NOTE]
>
>Los registros de depuración para at.js y el SDK web de Platform proporcionan un nivel de detalle similar con la notable excepción de que el SDK web solo notifica los errores de procesamiento debido a selectores no válidos. El registro de depuración no confirma actualmente que el procesamiento se haya realizado correctamente.

### Ver seguimientos de Target

Los seguimientos de Target proporcionan información detallada sobre las cualificaciones de la actividad y el perfil de Target del visitante. Dado que los seguimientos de Target contienen información que no está disponible públicamente, su visualización requiere un token de autorización o autenticación dentro de la ventana de extensión del explorador de Adobe Experience Platform Debugger.

| Método de seguimiento de destino | at.js | SDK web de Platform |
| --- | --- | --- |
| `mboxTrace` parámetro de URL | Sí | No |
| extensión del explorador de Adobe Experience Platform Debugger | Sí | Sí |
| Adobe Experience Platform Assurance | No | Sí |



<!--![How to view Target traces with Adobe Experience Platform Debugger](assets/target-trace-debugger.png){zoomable="yes"}-->

Después de seleccionar **[!UICONTROL Ver]**, aparecerá una superposición que le permitirá ver la siguiente información relacionada con la solicitud:

- Actividades coincidentes
- Actividades no coincidentes
- Solicitar detalles
- Instantánea de perfil

Consulte la guía dedicada sobre [depuración de la entrega de contenido de Target](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html) para obtener más información sobre los seguimientos de Target.

### Solucionar problemas con Assurance

La información de seguimiento de Target se puede ver tanto en la extensión del explorador de Adobe Experience Platform Debugger como en la aplicación Assurance (anteriormente conocida como Project Griffon). Para ver los seguimientos de Target en Assurance, haga lo siguiente:

1. Abra la extensión del explorador de Adobe Experience Platform Debugger y conecte una sesión de depuración remota como se ha descrito anteriormente
1. Seleccione el vínculo con el nombre de la sesión sobre el registro de depuración
1. Platform Assurance carga y muestra el registro detallado de todas las aplicaciones de Adobe configuradas en el flujo de datos de su implementación
1. Filtrar el registro por `adobe.target`
1. Seleccione una entrada de registro con el tipo `com.adobe.target.trace`
1. Expanda los detalles de la carga útil y vea la información en `context > targetTrace`

<!--![How to view Target traces with Assurance](assets/target-trace-assurance.png){zoomable="yes"}-->

## Examinar solicitud y respuesta de red

La carga útil de solicitud y la respuesta de las llamadas del SDK web de Platform `sendEvent` difieren de at.js. La descripción siguiente le ayudará a comprender la estructura de la solicitud y la respuesta mientras examina las llamadas de red con las herramientas para desarrolladores del explorador.

### Carga útil de solicitud de contenido

<!--![Target specific elements of the Platform Web SDK payload](assets/target-payload.png){zoomable="yes"}-->

- El perfil, la entidad y otros parámetros que no son de mbox se pasan en la matriz de eventos en `data.__adobe.target`
- Los ámbitos de decisión se encuentran en la matriz de eventos en `query.personalization.decisionScopes`
- Los datos XDM asignados a parámetros de mbox descendentes se encuentran en la matriz de eventos en `xdm`

### Cuerpo de respuesta de contenido

<!--![Target specific elements of the Platform Web SDK response body](assets/target-response.png){zoomable="yes"}-->

- El SDK web de Platform devuelve acciones para todas las aplicaciones de Adobe bajo el objeto `handle`
- La acción `personalization:decisions` significa una respuesta del offer decisioning o destinatario
- Las propuestas de destino se presentan como una matriz, cada una con un identificador de propuesta único con el prefijo `AT:`
- El ámbito de decisión y los detalles de la actividad se encuentran en la matriz de propuestas
- Los detalles de la oferta se encuentran en la matriz `items` en `data`
- Los tokens de respuesta se encuentran en la matriz `items` en `meta`

### Carga útil de evento de propuesta

<!--![Target proposition event example](assets/target-proposition-event.png){zoomable="yes"}-->

- Los eventos específicos de SDK de destino son `decisioning.propositionDisplay` para una impresión o `decisioning.propositionInteract` para una interacción, como un clic
- Los detalles del evento de propuesta se encuentran en la matriz de eventos bajo `xdm._experience.decisioning`
- El ID de propuesta del evento de visualización o interacción debe coincidir con el ID de propuesta del contenido devuelto desde Target


¡Felicidades, ha llegado al final del tutorial! ¡Buena suerte al migrar su implementación de Adobe Target al SDK web!

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
