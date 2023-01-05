---
title: Validación de implementaciones de Target con el SDK web | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo validar actividades y depurar una implementación de Adobe Target mediante el SDK web de Adobe Experience Platform.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Validación de la implementación del SDK web de Platform

Después de haber migrado la implementación de Target de at.js al SDK web de Platform, es importante validar que todo funcione correctamente antes de publicar cualquier cambio en el sitio de producción. Adobe recomienda lo siguiente, que se explica en detalle en esta página:

* Realice una validación técnica para asegurarse de que la implementación básica y las solicitudes y respuestas del SDK web de Platform tengan el aspecto correcto
* Asegúrese de que las actividades de Target se entregan y procesan correctamente
* Comprobar que los informes funcionen correctamente
* Revise las audiencias y los scripts de perfil para asegurarse de que son compatibles con el SDK web de Platform.
* Garantizar que las integraciones con aplicaciones de Adobe o de terceros funcionen correctamente

Cada implementación de Target es diferente según la arquitectura del sitio y las características utilizadas. Puede utilizar las tablas siguientes como punto de partida y agregar cualquier elemento exclusivo de su implementación. La variable [Página de depuración](debugging.md) en este tutorial se muestran las herramientas que puede utilizar para ayudarle con esta validación.

## Validación técnica

| Elemento de validación | Notas |
|---|---|
| El fragmento de preocultación de at.js ya no está presente en la página | El SDK web de Platform no elimina automáticamente el estilo con el ID `at-body-style`. Si deja este fragmento antiguo en la página, el resultado es contenido oculto hasta que se alcanza el tiempo de espera del fragmento. |
| La biblioteca at.js ya no está presente en la página | Compruebe que no haya ningún objeto &quot;adobe.target&quot; en la consola de herramientas para desarrolladores del explorador. La inclusión del SDK web de Platform y at.js provoca un comportamiento de procesamiento no deseado |
| Los parámetros esperados se encuentran en el XDM y los objetos de datos del `sendEvent` solicitud |  |
| El catálogo de Recommendations se actualiza según lo esperado si se utilizan solicitudes de página para rellenar el catálogo |  |
| Los parámetros de perfil se pasan correctamente a Target | Ver trazos de Edge en Debugger |
| Los parámetros asignados a XDM en el asignador de conjuntos de datos se pasan correctamente a Target | Validar con la función de seguimiento de Edge de Debugger o Assurance |
| El contenido de destino se devuelve en la variable correspondiente `sendEvent` respuestas | Se espera cuando `renderDecisions` está configurada en `true` o los ámbitos se solicitan y el usuario cumple los requisitos para una actividad de Target en particular |
| A `decisioning.propositionDisplay` se activa después de procesar las actividades basadas en VEC | Se espera que las actividades procesadas automáticamente y bajo demanda tengan llamadas de evento independientes |
| A `decisioning.propositionDisplay` se activa después del procesamiento de actividades basadas en formularios | Solo aplicable a determinadas implementaciones. Requiere código personalizado para ejecutar esta llamada. |
| A `decisioning.propositionDisplay` se activa cuando se aplica una oferta en un cambio de vista de SPA | Solo aplicable para implementaciones de SPA |
| A `decisioning.propositionDisplay` NO se activa cuando un componente SPA vuelve a procesarse para una vista determinada | Solo aplicable para implementaciones de SPA |
| A `decisioning.propsitionInteract` el evento se activa después de una conversión de actividad | El mensaje &quot;Se hizo clic en un elemento&quot; y las conversiones personalizadas migradas desde at.js `trackEvent` o `sendNotifications` se espera que tengan llamadas de evento separadas |
| Los tokens de respuesta se devuelven en la variable `sendEvent` Respuesta y tienen valores esperados | Los tokens de respuesta deben funcionar normalmente con el SDK web |
| Los ECID son coherentes en todas las páginas con el SDK web y at.js | Se aplica a las migraciones página por página. No se espera que las ofertas de redireccionamiento funcionen en estos tipos de migraciones |


## Entrega y renderización de actividades

| Elemento de validación | Notas |
|---|---|
| Las actividades basadas en VEC se representan correctamente al cargar la página | Es mejor validar tanto las modificaciones del código personalizado como las modificaciones básicas, como la reorganización de elementos o la sustitución de texto |
| Las actividades basadas en VEC se representan correctamente en SPA cambios de vista | Solo aplicable para implementaciones de SPA |
| Las actividades basadas en formularios se representan correctamente | Solo aplicable a determinadas implementaciones. El procesamiento de actividades basadas en formularios requiere un código personalizado similar a at.js. |
| Las actividades que utilizan redirecciones funcionan correctamente | Las redirecciones son compatibles si la página de origen y la de destino utilizan Platform Web SDK. No se admite el redireccionamiento de Target de una página de at.js a una página de SDK web de plataforma o del modo contrario. |
| Las actividades que utilizan ofertas remotas funcionan correctamente | No es habitual, compruebe el inventario de ofertas de Target para ofertas remotas |
| El parpadeo se mitiga correctamente | La administración de parpadeo es opcional, pero asegúrese de que las tácticas de mitigación que tiene en su sitio estén funcionando según lo esperado para un rendimiento de página óptimo y la experiencia del usuario |
| Los vínculos de control de calidad funcionan según lo esperado | Si no funciona, confirme que web.webPageDetails.URL coincide exactamente con la dirección URL del explorador |
| Todos los tipos de oferta que utiliza con frecuencia se representan según lo esperado |  |

## Informes

| Elemento de validación | Notas |
|---|---|
| Los visitantes se atribuyen a actividades basadas en VEC | Es mejor validar los informes según lo esperado para modificaciones de carga de página y modificaciones de vista de SPA |
| Los visitantes se atribuyen a actividades basadas en formularios | Según el método de renderización utilizado, la implementación puede requerir que el código personalizado ejecute un `decisioning.propositionDisplay` evento |
| Los objetivos de conversión estándar se capturan correctamente | Se aplica a Target o Analytics como fuente de informes |
| Las conversiones y los detalles del pedido se capturan correctamente | Comprobar el informe de auditoría |
| Las conversiones de rastreo de clics se capturan correctamente |  |
| Los objetivos de conversión personalizados se capturan correctamente | Por ejemplo, los objetivos de conversión se migraron desde at.js `trackEvent` o `sendNotifications` que normalmente se usan con el objetivo &quot;ha visto un mbox&quot; |

## Audiencias y scripts de perfil

| Elemento de validación | Notas |
|---|---|
| Las audiencias utilizadas en actividades activas son compatibles con el SDK web de Platform | Las audiencias que utilizan el componente &quot;Personalizado&quot; (parámetro de mbox) deben actualizarse para incluir atributos XDM |
| Todos los scripts de perfil son compatibles con el SDK web de Platform | Cualquier script de perfil que utilice parámetros de mbox debe actualizarse para incluir atributos XDM |
| Devolución de actividades para audiencias de Target | Es mejor realizar una validación completa de las audiencias que modifique para que sean compatibles con el SDK web de Platform |
| Los scripts de perfil se evalúan como se espera | Ver trazos de Edge en Debugger |

## Integraciones con aplicaciones de Adobe

| Elemento de validación | Notas |
|---|---|
| Devolución de actividades para audiencias de Experience Cloud | Por ejemplo, un segmento publicado desde Adobe Analytics |
| Devolución de actividades para audiencias de Experience Platform | Sólo se aplica si tiene una licencia para una aplicación basada en Experience Platform como RTCDP |
| Devolución de actividades para audiencias de Audience Manager | Por ejemplo, un segmento basado en la visita a una página específica |
| Se muestran los datos de actividad de Target en Analysis Workspace | Se aplica a actividades que utilizan Adobe Analytics como fuente de informes |

## Integraciones con aplicaciones de terceros

| Elemento de validación | Notas |
|---|---|
| Los datos del token de respuesta se pasan correctamente a aplicaciones de terceros | Los enfoques de integración pueden variar, pero un método común es usar tokens de respuesta de Target para pasar información de actividad y experiencia a otras herramientas de análisis, como los Google Analytics |
| La información de terceros se pasa como XDM o como datos de perfil | Toda la información relevante de terceros debe transmitirse `sendEvent` llamadas a Target |

Después de realizar los pasos de validación anteriores, puede estar seguro de que la implementación del SDK web de Platform está lista para pasar a la fase de producción.

A continuación, aprenda a [resolución de problemas de una implementación de Target mediante el SDK web de Platform](debugging.md).

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).