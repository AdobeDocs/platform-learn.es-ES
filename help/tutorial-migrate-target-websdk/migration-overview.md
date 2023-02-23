---
title: Información general sobre migración | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre las diferencias clave entre at.js y el SDK web de plataforma y cómo planificar su esfuerzo de migración.
source-git-commit: 4b695b4578f0e725fc3fe1e455aa4886b9cc0669
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# Información general sobre la migración de at.js a Platform Web SDK

El nivel de esfuerzo para migrar de at.js al SDK web de Platform depende de la complejidad de la implementación actual y de las funciones de producto utilizadas.

Independientemente de lo sencilla o compleja que sea su implementación, es importante comprender completamente su estado actual antes de migrar. Esta guía le ayuda a desglosar los componentes de su implementación actual y a desarrollar un plan manejable para migrar cada pieza.

El proceso de migración implica los siguientes pasos clave:

1. Evaluar la implementación actual y determinar un enfoque de migración
1. Configuración de los componentes iniciales para conectarse a la red perimetral de Adobe Experience Platform
1. Actualice la implementación fundamental para reemplazar at.js por el SDK web de Platform
1. Mejore la implementación del SDK web de Platform para sus casos de uso específicos. Esto puede implicar pasar parámetros adicionales, tener en cuenta los cambios de vista de aplicaciones de una sola página (SPA), usar tokens de respuesta y mucho más.
1. Actualizar objetos en la interfaz de Target, como scripts de perfil, actividades y definiciones de audiencia
1. Valide la implementación final antes de realizar el cambio en el entorno de producción

## Diferencias clave entre at.js y el SDK web de plataforma

Antes de iniciar el proceso de migración, es importante comprender las diferencias entre at.js y el SDK web de Platform.

### Diferencias operativas

El SDK web de Platform combina la funcionalidad de varias aplicaciones de Adobe en una sola biblioteca. Este enfoque unificado significa que debe tener en cuenta las responsabilidades y los procesos entre equipos para garantizar una implementación saludable.

|  | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Propiedad | La biblioteca at.js es independiente de otras bibliotecas de aplicaciones. Las personalizaciones y la propiedad de estas bibliotecas dispares pueden alinearse con diferentes equipos de la organización. | La biblioteca del SDK web de Platform y los datos pasados están unificados para todas las aplicaciones de Adobe. La propiedad de la implementación del SDK web de Platform debe representar a las partes interesadas de todas las aplicaciones descendentes. |
| Mantenimiento | Los equipos independientes pueden trabajar en mejoras de implementación para cada aplicación de Adobe, como Target y Analytics. | Lo ideal es que un solo equipo sea responsable de las mejoras que afecten a la implementación del SDK web de Platform. |
| Proceso | Los cambios en una implementación de Target pueden seguir un proceso que tenga una cadencia o requisitos de control de calidad diferentes a otros procesos de aplicaciones como Analytics. | Los cambios en una implementación del SDK web de Platform deben tener en cuenta todas las aplicaciones posteriores, y el proceso de control de calidad y publicación debe ajustarse en consecuencia. |
| Colaboración | Los datos específicos de Target se pueden pasar directamente en las llamadas de Target . Según la implementación, puede haber llamadas de Target adicionales. Esto no afecta directamente a los datos de Adobe Analytics y la coordinación con el equipo de análisis no es tan importante. | Los datos pasados en llamadas del SDK web de Platform se pueden reenviar a Target y a Analytics. La coordinación entre los equipos es necesaria para garantizar que los cambios no afecten negativamente a una aplicación específica. |

### Diferencias técnicas

El SDK web de Platform no es una evolución de la biblioteca at.js de Target. Es un enfoque nuevo y unificado para implementar todas las aplicaciones de Adobe para el canal web. Hay varias diferencias técnicas que hay que tener en cuenta.

|  | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Funcionalidad de la biblioteca | Funcionalidad de Target proporcionada por at.js. Integraciones con otras aplicaciones proporcionadas por Visitor.js y AppMeasurement.js | Funcionalidad para todas las aplicaciones de Adobe proporcionadas por una sola biblioteca del SDK web de la plataforma: alloy.js |
| Rendimiento | at.js es una de las bibliotecas múltiples que se deben cargar para lograr la integración adecuada en todas las aplicaciones. Esto resulta en menos de un tiempo de carga óptimo. | El SDK web de Platform es una única biblioteca ligera que elimina la necesidad de varias bibliotecas específicas de la aplicación, lo que mejora el rendimiento de carga de la página. |
| Solicitudes | Separe las llamadas para cada aplicación de Adobe. Las llamadas de Target son en gran medida independientes de otras llamadas de red. | Una sola llamada para todas las aplicaciones de Adobe. Los cambios en los datos pasados en estas llamadas podrían afectar a varias aplicaciones descendentes. |
| Orden de carga | La integración adecuada con otras aplicaciones de Adobe requiere un orden de carga específico de bibliotecas y llamadas de red. | La integración adecuada no depende de la vinculación de datos de llamadas de red dispares específicas de la aplicación, por lo que el orden de carga no es un problema. |
| Red perimetral | Utiliza la red perimetral de Adobe Experience Cloud (tt.omtrdc.net), opcionalmente con un CNAME específico para Target. | Utiliza la red perimetral de Adobe Experience Platform (edge.adobedc.net), opcionalmente con un solo CNAME. |
| Terminología básica | Nombre de at.js: <br> - `mbox` <br> - `pageLoad` Evento (mbox global) <br> - `offer` | Equivalente de SDK web de plataforma: <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### Información general del vídeo

El siguiente vídeo ofrece información general sobre el SDK web de Adobe Experience Platform y la red perimetral de Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

Ahora que comprende las diferencias de alto nivel entre at.js y el SDK web de Platform, puede [planificar la migración](plan-migration.md).

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).