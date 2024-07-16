---
title: Validación de implementaciones de Target con SDK web | Migración de Target de at.js 2.x a SDK web
description: Obtenga información sobre cómo validar actividades y depurar una implementación de Adobe Target mediante el SDK web de Adobe Experience Platform.
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# Validación de la implementación del SDK web de Platform

Después de migrar la implementación de Target de at.js al SDK web de Platform, es importante validar que todo funciona correctamente antes de publicar cualquier cambio en el sitio de producción. El Adobe recomienda lo siguiente, que se trata en detalle en esta página:

* Realice una validación técnica para asegurarse de que la implementación básica y las solicitudes y respuestas del SDK web de Platform tengan un aspecto correcto
* Asegúrese de que las actividades de Target se entreguen y representen correctamente
* Compruebe que la creación de informes funciona correctamente
* Vuelva a visitar las audiencias y los scripts de perfil para asegurarse de que son compatibles con el SDK web de Platform
* Asegúrese de que las integraciones con aplicaciones de Adobe o de terceros funcionan correctamente

Cada implementación de Target es diferente según la arquitectura y las funciones del sitio utilizadas. Puede utilizar las tablas siguientes como punto de partida y añadir cualquier elemento exclusivo a la implementación. La [página de depuración](debugging.md) de este tutorial muestra las herramientas que puede utilizar para ayudarle con esta validación.

## Validación técnica

| Elemento de validación | Notas |
|---|---|
| El fragmento preocultado de at.js ya no está presente en la página | El SDK web de Platform no quita automáticamente el estilo con el ID `at-body-style`. Si se deja este fragmento antiguo en la página, se obtiene contenido oculto hasta que se alcanza el tiempo de espera del fragmento. |
| La biblioteca at.js ya no está presente en la página | Compruebe que no haya ningún objeto &quot;adobe.target&quot; en la consola de herramientas para desarrolladores del explorador. Al incluir el SDK web de Platform y at.js, se obtiene un comportamiento de procesamiento no deseado |
| Los parámetros esperados están en el XDM y en los objetos de datos de la solicitud `sendEvent` | |
| El catálogo de Recommendations se actualiza según lo esperado si se utilizan solicitudes de página para rellenar el catálogo | |
| Los parámetros de perfil se han pasado correctamente a Target | Ver los seguimientos de Edge en Debugger |
| Los parámetros asignados a XDM en el asignador de flujos de datos se pasan correctamente a Target | Validar utilizando la función Edge Trace de Debugger o Assurance. |
| El contenido de destino devuelve en las respuestas `sendEvent` aplicables | Se esperaba cuando la opción `renderDecisions` se estableció en `true` o se solicitaron ámbitos y el usuario cumple los requisitos para una actividad de Target en particular |
| Un evento `decisioning.propositionDisplay` se activa después de que se representen las actividades basadas en VEC | Se espera que las actividades procesadas automáticamente y bajo demanda tengan llamadas de evento independientes |
| Un evento `decisioning.propositionDisplay` se desencadena después de que se representen las actividades basadas en formularios | Solo se aplica a determinadas implementaciones. Requiere código personalizado para ejecutar esta llamada. |
| SPA Un evento `decisioning.propositionDisplay` se desencadena cuando se aplica una oferta en un cambio de vista de la | SPA Solo se aplica a implementaciones de |
| SPA Un evento `decisioning.propositionDisplay` NO se desencadena cuando un componente de la vuelve a procesarse para una vista determinada | SPA Solo se aplica a implementaciones de |
| Un evento `decisioning.propsitionInteract` se desencadena después de una conversión de actividad | Se espera que &quot;Se hizo clic en un elemento&quot; y las conversiones personalizadas migradas desde at.js `trackEvent` o `sendNotifications` tengan llamadas de evento independientes |
| Los tokens de respuesta se devuelven en la respuesta `sendEvent` y tienen valores esperados | Los tokens de respuesta deben funcionar normalmente con el SDK web |
| Los ECID son coherentes en todas las páginas con el SDK web y at.js | Se aplica a las migraciones página por página. No se espera que las ofertas de redireccionamiento funcionen en estos tipos de migraciones |


## Entrega y renderización de actividades

| Elemento de validación | Notas |
|---|---|
| Las actividades basadas en VEC se representan correctamente al cargar la página | Es mejor validar tanto las modificaciones de código personalizado como las modificaciones básicas, como reorganizar elementos o reemplazar texto |
| SPA Las actividades basadas en VEC se representan correctamente en los cambios de vista de la | SPA Solo se aplica a implementaciones de |
| Las actividades basadas en formularios se representan correctamente | Solo se aplica a determinadas implementaciones. El procesamiento de actividades basadas en formularios requiere un código personalizado similar al de at.js. |
| Las actividades que utilizan redirecciones funcionan correctamente | Las redirecciones son compatibles si la página de origen y la de destino utilizan el SDK web de Platform. No se admite el redireccionamiento de Target desde una página at.js a una página del SDK web de Platform o viceversa. |
| Las actividades que utilizan ofertas remotas funcionan correctamente | No es habitual, compruebe el inventario de ofertas de Target para ver si hay ofertas remotas |
| El parpadeo se mitiga correctamente | La administración del parpadeo es opcional, pero asegúrese de que las tácticas de mitigación que haya implementado funcionen según lo esperado para obtener un rendimiento de página y una experiencia de usuario óptimos |
| Los vínculos de control de calidad funcionan según lo esperado | Si no funciona, confirme que web.webPageDetails.URL coincide exactamente con la dirección URL del explorador |
| Todos los tipos de oferta utilizados comúnmente se representan según lo esperado |  |

## Informes

| Elemento de validación | Notas |
|---|---|
| Los visitantes se atribuyen a actividades basadas en VEC | SPA Es mejor validar que el sistema de informes funciona según lo esperado, tanto para las modificaciones de carga de página como para las modificaciones de vista de la vista de la vista de datos |
| Los visitantes se atribuyen a actividades basadas en formularios | Según el método de renderización utilizado, la implementación puede requerir código personalizado para ejecutar un evento `decisioning.propositionDisplay` |
| Los objetivos de conversión estándar se capturan correctamente | Se aplica a Target o Analytics como fuente de informes |
| Las conversiones y los detalles de los pedidos se capturan correctamente | Comprobación del informe de auditoría |
| Las conversiones de rastreo de clics se capturan correctamente |  |
| Los objetivos de conversión personalizados se capturan correctamente | Por ejemplo, los objetivos de conversión migraron de at.js `trackEvent` o `sendNotifications`, que se usan comúnmente con el objetivo &quot;visualizó un mbox&quot; |

## Audiencias y scripts de perfil

| Elemento de validación | Notas |
|---|---|
| Las audiencias utilizadas en las actividades activas son compatibles con el SDK web de Platform | Las audiencias que utilizan el componente &quot;Personalizado&quot; (parámetro de mbox) deben actualizarse para incluir atributos XDM |
| Todos los scripts de perfil son compatibles con el SDK web de Platform | Cualquier script de perfil que utilice parámetros de mbox debe actualizarse para incluir atributos XDM |
| Devolución de actividades para audiencias de Target | Se recomienda realizar una validación de extremo a extremo en las audiencias que modifique para que sean compatibles con el SDK web de Platform |
| Los scripts de perfil se evalúan según lo esperado | Ver los seguimientos de Edge en Debugger |

## Integraciones con aplicaciones de Adobe

| Elemento de validación | Notas |
|---|---|
| Devolución de actividades para audiencias de Experience Cloud | Por ejemplo, un segmento publicado desde Adobe Analytics |
| Devolución de actividades para audiencias de Experience Platform | Solo se aplica si tiene una licencia para una aplicación basada en Experience Platform como RTCDP |
| Devolución de actividades para audiencias de Audience Manager | Por ejemplo, un segmento basado en visitar una página específica |
| Los datos de actividad de Target se muestran en Analysis Workspace | Se aplica a las actividades que utilizan Adobe Analytics como fuente de informes |

## Integraciones con aplicaciones de terceros

| Elemento de validación | Notas |
|---|---|
| Los datos del token de respuesta se pasan correctamente a aplicaciones de terceros | Los enfoques de integración pueden variar, pero un método común es utilizar tokens de respuesta de Target para pasar la información de actividades y experiencias a otras herramientas de análisis como los Google Analytics |
| La información de terceros se pasa como datos de perfil o XDM | Toda la información relevante de terceros debe pasarse en `sendEvent` llamadas a Target |

Después de realizar los pasos de validación anteriores, puede estar seguro de que la implementación del SDK web de Platform está lista para pasar a producción.

A continuación, aprenda a [solucionar problemas de una implementación de Target mediante el SDK web de Platform](debugging.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
