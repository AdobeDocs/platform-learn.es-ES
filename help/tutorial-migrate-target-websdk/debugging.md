---
title: Depuración | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo depurar una implementación de Adobe Target mediante el SDK web de Adobe Experience Platform. Los temas incluyen opciones de depuración, extensiones de explorador y diferencias entre at.js y el SDK web de Platform.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 3%

---

# Depuración de Target con el SDK web de Platform

Verificación de las actividades de Target y depuración del SDK web para solucionar problemas de implementación, entrega de contenido o cualificación de audiencias. Esta página de la guía de migración explica las diferencias entre la depuración con at.js y el SDK web de plataforma.

La siguiente tabla resume las funciones y la compatibilidad con los enfoques de prueba y depuración.

| Función o herramienta | Compatibilidad con at.js | Compatibilidad con el SDK web de plataforma |
| --- | --- | --- |
| URL de control de calidad de la actividad | Sí | Sí |
| `mboxDisable` Parámetro de URL | Sí | Consulte la información siguiente para [deshabilitar la funcionalidad de Target](#disable-target-functionality) |
| `mboxDebug` Parámetro de URL | Sí | Uso `alloy_debug` parámetro para información de depuración similar |
| `mboxTrace` Parámetro de URL | Sí | Utilice la extensión del explorador de Experience Platform Debugger |
| Extensión de Adobe Experience Platform Debugger | Sí | Sí |
| `alloy_debug` Parámetro de URL | No aplicable | Sí |
| Adobe Experience Platform Assurance | No aplicable | Sí |

## Extensión del explorador de Adobe Experience Platform Debugger

La extensión de Adobe Experience Platform Debugger para Chrome y Firefox examina sus páginas web y le ayuda a validar las implementaciones de Adobe Experience Cloud.

Puede ejecutar Platform Debugger en cualquier página web y la extensión tiene acceso a datos públicos. Para acceder a datos que no son públicos mediante la extensión, como información de seguimiento de Target, debe autenticarse en el Experience Cloud mediante la variable **[!UICONTROL Iniciar sesión]** vínculo.

### Obtención e instalación de Adobe Experience Platform Debugger

Adobe Experience Platform Debugger se puede instalar en los navegadores Google Chrome o Mozilla Firefox. Siga el vínculo correspondiente a continuación para instalar la extensión en el explorador que prefiera:

- [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
- [Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/)

Después de instalar la extensión de Chrome o el complemento de Firefox, aparece un icono (![](assets/start-icon.jpg)) se agrega a la barra de extensiones. Seleccione este icono para abrir la extensión.

Consulte la guía dedicada para obtener más información sobre la [Extensión de Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) y cómo depurar todas las aplicaciones web de Adobe.

## Vista previa de actividades de Target con direcciones URL de control de calidad

Tanto at.js como el SDK web de la plataforma le permiten previsualizar las actividades de Target mediante URL de control de calidad de Target, y ambos métodos de implementación admiten las mismas funciones de control de calidad.

Direcciones URL de control de calidad de Target que funcionen indicando a at.js o al SDK web de plataforma que escriban una cookie específica en su explorador con el nombre `at_qa_mode`. Esta cookie se utiliza para forzar la calificación para una actividad y experiencia en particular.

>[!CAUTION]
>
>La funcionalidad del modo de control de calidad de Target es compatible con Platform Web SDK versión 2.13.0 o superior. El modo de control de calidad de Target está habilitado en función de la variable `xdm.web.webPageDetails.URL` valor pasado en la variable `sendEvent` llamada a . Cualquier modificación a este valor, como la reducción de mayúsculas y minúsculas en todos los caracteres, puede impedir que el modo de control de calidad de Target funcione correctamente.

Consulte la guía dedicada para obtener más información sobre [Control de calidad de la actividad de Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).

## Implementación de Debug Target

La tabla siguiente describe las diferencias entre las tácticas de depuración de at.js y del SDK web de plataforma:

| función de at.js | Equivalente del SDK web de la plataforma |
| --- | --- |
| **Desactivación de mbox** : deshabilite Target para recuperar y procesar y comprobar si la página está rota sin interacciones de Target.<br><br>Cargar página con parámetro de URL: `mboxDisable=true` | Sin equivalente directo. Puede bloquear todas las solicitudes de SDK web de Platform con las herramientas para desarrolladores del explorador. |
| **Depuración de mbox** : registra todas las acciones de at.js en la consola del explorador para ayudar a solucionar problemas de renderización<br><br>Cargar página con parámetro de URL: `mboxDebug=true` | **Alloy Debug** : registra las acciones detalladas del SDK, incluidas, entre otras, las acciones de personalización de Target.<br><br>Cargar página con parámetro de URL: `alloy_debug=true`  <br /><br />O ejecutar `alloy("setDebug", { "enabled": true });` en la consola del desarrollador |
| **Seguimiento de destino** : con un token de seguimiento de mbox generado en la interfaz de usuario de Target, un objeto de seguimiento con detalles que participaron en el proceso de toma de decisiones está disponible en `window.___target_trace` objeto.<br><br>Cargar página con parámetro de URL: `mboxTrace=window&authorization={TOKEN}` | Utilice la extensión de Adobe Experience Platform Debugger o Platform Assurance. |

>[!NOTE]
>
>Todas las funciones de depuración de at.js que se enumeran arriba están disponibles con funciones mejoradas en Adobe Experience Platform Debugger.

### Deshabilitar funcionalidad de Target

El SDK web de Platform no tiene actualmente una función para suprimir selectivamente las respuestas de Target. Sin embargo, es posible suprimir las solicitudes del SDK web de la plataforma con las herramientas para desarrolladores del explorador, varias extensiones de navegador o aplicaciones de terceros. Por ejemplo, para bloquear el SDK web de Platform con Google Chrome:

1. Haga clic con el botón derecho en cualquier lugar de la página y seleccione **Inspect**
1. Seleccione el **Red** ficha
1. Filtrar por la cadena `//ee//` para ver solo las llamadas del SDK web de Platform
1. Vuelva a cargar la página
1. Haga clic con el botón derecho en una de las solicitudes de red filtradas y seleccione **Bloquear dominio de solicitud**
1. Vuelva a cargar la página y observe que la solicitud de red está bloqueada
1. Cuando termine la depuración, haga clic con el botón derecho en la solicitud de red bloqueada y seleccione **Desbloquear** o cierre el panel Herramientas para desarrolladores

### Ver registro de depuración

Registro de depuración para at.js mediante el uso de `mboxDebug=true` El parámetro de URL muestra información detallada sobre cada solicitud, respuesta e intento de procesar el contenido en la página. El SDK web de Platform tiene un registro de depuración similar usando `alloy_debug=true` parámetro de URL.

| Información registrada | at.js (`mboxDebug=true`) | SDK web de Platform (`alloy_debug=true`) |
| --- | --- | --- |
| Prefijo de registro para filtrar | `AT:` | `[alloy]` |
| Detalles de la solicitud de carga de página | Sí | Sí |
| Detalles de solicitud de mbox o ámbito | Sí | Sí |
| Estado de la solicitud | Sí | Sí |
| Detalles de respuesta | Sí | Sí |
| Estado de procesamiento | Éxito y errores | Solo errores |
| Detalles de renderización | Sí | Sí |

>[!NOTE]
>
>Los registros de depuración para at.js y el SDK web de plataforma ofrecen un nivel de detalle similar, con la notable excepción de que el SDK web solo notifica errores de procesamiento debido a selectores no válidos. El registro de depuración no confirma actualmente que la renderización se haya realizado correctamente.

### Ver trazos de Target

Los seguimientos de Target proporcionan información detallada sobre las cualificaciones de la actividad y el perfil de Target del visitante. Dado que los seguimientos de Target contienen información que no está disponible para el público, verlos requiere un token de autorización o autenticarse dentro de la ventana de extensión del explorador de Adobe Experience Platform Debugger.

| Método de seguimiento de Target | at.js | SDK web de Platform |
| --- | --- | --- |
| `mboxTrace` Parámetro de URL | Sí | No |
| Extensión del explorador de Adobe Experience Platform Debugger | Sí | Sí |
| Adobe Experience Platform Assurance | No | Sí |


Para ver los seguimientos de Platform Web SDK Target con Adobe Experience Platform Debugger, haga lo siguiente:

1. Vaya a una página de su sitio que tenga Target implementado con el SDK web de la plataforma
1. Abra la extensión de Adobe Experience Platform Debugger seleccionando el icono (![](assets/start-icon.jpg)) en la barra de navegación del explorador
1. Seleccione el **[!UICONTROL Iniciar sesión]** vínculo
1. Autenticar mediante el inicio de sesión de Adobe Experience Cloud
1. Seleccione el **[!UICONTROL Registros]** a la izquierda
1. Seleccione el **[!UICONTROL Edge]** en la parte superior
1. Si lo desea, asigne un nombre a la sesión de depuración y haga clic en el botón **[!UICONTROL Connect]** botón
1. Vuelva a cargar la página y el registro debe rellenarse con información detallada sobre las interacciones de red perimetral
1. Céntrese en las entradas de registro que comienzan con &quot;Rastreos de destino&quot; en la descripción y seleccione **[!UICONTROL Ver]** para ver los detalles de seguimiento de Target

![Ver los seguimientos de Target con Adobe Experience Platform Debugger](assets/target-trace-debugger.png){zoomable=&quot;yes&quot;}

Después de seleccionar **[!UICONTROL Ver]**, aparecerá una superposición que le permitirá ver la siguiente información relacionada con la solicitud:

- Actividades coincidentes
- Actividades no coincidentes
- Detalles de la solicitud
- Instantánea de perfil

Consulte la guía dedicada sobre [depuración de la entrega de contenido de Target](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html) para obtener más información sobre los seguimientos de Target.

### Resolución de problemas con Assurance

La información de seguimiento de Target se puede ver tanto en la extensión del explorador de Adobe Experience Platform Debugger como dentro de la aplicación Assurance (anteriormente conocida como Project Griffon). Para ver los seguimientos de Target dentro de Assurance, haga lo siguiente:

1. Abra la extensión del explorador de Adobe Experience Platform Debugger y conecte una sesión de depuración remota como se describe anteriormente
1. Seleccione el vínculo con el nombre de la sesión encima del registro de depuración
1. Platform Assurance carga y muestra el registro detallado de todas las aplicaciones de Adobe configuradas en el flujo de datos para la implementación
1. Filtre el registro por `adobe.target`
1. Seleccione una entrada de registro con el tipo `com.adobe.target.trace`
1. Expanda los detalles de la carga útil y vea la información en `context > targetTrace`

![Ver los seguimientos de Target con Assurance](assets/target-trace-assurance.png){zoomable=&quot;yes&quot;}

## Examinar la solicitud y la respuesta de red

Carga útil de la solicitud y respuesta del SDK web de Platform `sendEvent` Las llamadas de difieren de at.js. El siguiente esquema le ayudará a comprender la estructura de la solicitud y la respuesta mientras examina las llamadas de red con las herramientas para desarrolladores del explorador.

### Carga útil de solicitud de contenido

![Segmente elementos específicos de la carga útil del SDK web de Platform](assets/target-payload.png){zoomable=&quot;yes&quot;}

- Los parámetros de perfil, entidad y otros que no son de mbox se pasan en la matriz de eventos en `data.__adobe.target`
- Los ámbitos de decisión se encuentran en la matriz de eventos de `query.personalization.decisionScopes`
- Los datos XDM asignados a parámetros de mbox descendentes se encuentran en la matriz de eventos debajo de `xdm`

### Cuerpo de respuesta de contenido

![Segmente elementos específicos del cuerpo de respuesta del SDK web de Platform](assets/target-response.png){zoomable=&quot;yes&quot;}

- El SDK web de Platform devuelve acciones para todas las aplicaciones de Adobe en la sección `handle` object
- La variable `personalization:decisions` significa una respuesta de Target o offer decisioning
- Las propuestas de destino se presentan como una matriz, cada una con un ID de propuesta único con el prefijo `AT:`
- El ámbito de decisión y los detalles de la actividad se encuentran dentro de la matriz de propuestas
- Los detalles de la oferta se encuentran en la `items` matriz bajo `data`
- Los tokens de respuesta se encuentran en la `items` matriz bajo `meta`

### Carga útil de evento de propuesta

![Ejemplo de evento de propuesta de destino](assets/target-proposition-event.png){zoomable=&quot;yes&quot;}

- Los eventos de SDK específicos de Target son: `decisioning.propositionDisplay` para una impresión o `decisioning.propositionInteract` para una interacción, como un clic
- Los detalles del evento de propuesta se encuentran en la matriz de eventos debajo de `xdm._experience.decisioning`
- El ID de la propuesta del evento de visualización o interacción debe coincidir con el ID de la propuesta del contenido devuelto desde Target


¡Felicidades, ha llegado al final del tutorial! Buena suerte al migrar su implementación de Adobe Target al SDK web.

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
