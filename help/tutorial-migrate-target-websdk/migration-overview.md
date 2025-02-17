---
title: 'Información general sobre la migración: Migración de Target de at.js 2.x a Web SDK'
description: Obtenga información sobre las diferencias clave entre at.js y Platform Web SDK y cómo planificar el esfuerzo de migración.
exl-id: a8ed78e4-c8c2-4505-b4b5-e5d508f5ed87
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---

# Información general sobre la migración de at.js a Platform Web SDK

El nivel de esfuerzo para migrar de at.js a Platform Web SDK depende de la complejidad de la implementación actual y de las funciones del producto utilizadas.

Independientemente de lo simple o compleja que sea su implementación, es importante comprender completamente su estado actual antes de migrar. Esta guía le ayuda a desglosar los componentes de la implementación actual y a desarrollar un plan manejable para migrar cada parte.

El proceso de migración incluye los siguientes pasos clave:

1. Evalúe la implementación actual y determine un enfoque de migración
1. Configuración de los componentes iniciales para conectarse a Adobe Experience Platform Edge Network
1. Actualice la implementación básica para reemplazar at.js por Platform Web SDK.
1. Mejore la implementación de Platform Web SDK para sus casos de uso específicos. Esto puede implicar pasar parámetros adicionales, tener en cuenta los cambios de vista de la aplicación de una sola página (SPA), utilizar tokens de respuesta y mucho más.
1. Actualizar objetos en la interfaz de Target, como scripts de perfil, actividades y definiciones de audiencia
1. Valide la implementación final antes de realizar el cambio en el entorno de producción.

## Diferencias clave entre at.js y Platform Web SDK

Antes de iniciar el proceso de migración, es importante comprender las diferencias entre at.js y Platform Web SDK.

### Diferencias operativas

Platform Web SDK combina la funcionalidad de varias aplicaciones de Adobe en una sola biblioteca. Este enfoque unificado significa que debe tener en cuenta las responsabilidades y los procesos entre equipos para garantizar una implementación saludable.

| | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Propiedad | La biblioteca at.js es independiente de otras bibliotecas de aplicaciones. Las personalizaciones y la propiedad de estas bibliotecas dispares pueden alinearse con diferentes equipos de la organización. | La biblioteca de Platform Web SDK y los datos pasados se unifican para todas las aplicaciones de Adobe. La propiedad de la implementación de Platform Web SDK debe representar a las partes interesadas de todas las aplicaciones de flujo descendente. |
| Mantenimiento | Hay equipos independientes que pueden trabajar en las mejoras de implementación para cada aplicación de Adobe, como Target y Analytics. | Lo ideal es que un solo equipo sea responsable de las mejoras que afecten a la implementación de Platform Web SDK. |
| Proceso | Los cambios en una implementación de Target pueden seguir un proceso que tenga una cadencia o requisitos de control de calidad diferentes a los de otras aplicaciones, como Analytics. | Los cambios en una implementación de Platform Web SDK deben tener en cuenta todas las aplicaciones de flujo descendente, y el control de calidad y el proceso de publicación deben ajustarse en consecuencia. |
| Colaboración | Los datos específicos de Target se pueden pasar directamente en las llamadas de Target. Según la implementación, puede haber llamadas de Target adicionales. Esto no afecta directamente a los datos de Adobe Analytics y la coordinación con el equipo de análisis no es tan crítica. | Los datos pasados en las llamadas de Platform Web SDK se pueden reenviar tanto a Target como a Analytics. Es necesaria la coordinación entre equipos para garantizar que los cambios no afecten negativamente a una aplicación específica. |

### Diferencias técnicas

Platform Web SDK no es una evolución de la biblioteca at.js de Target. Se trata de un enfoque nuevo y unificado para implementar todas las aplicaciones de Adobe para el canal web. Hay varias diferencias técnicas que hay que tener en cuenta.

| | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Funcionalidad de biblioteca | Funcionalidad de Target proporcionada por at.js. Integraciones con otras aplicaciones proporcionadas por Visitor.js y AppMeasurement.js | Funcionalidad para todas las aplicaciones de Adobe proporcionadas por una sola biblioteca de Platform Web SDK: alloy.js |
| Rendimiento | at.js es una de las múltiples bibliotecas que se deben cargar para una integración adecuada entre aplicaciones. Esto resulta en un tiempo de carga inferior al óptimo. | Platform Web SDK es una única biblioteca ligera que elimina la necesidad de utilizar varias bibliotecas específicas de la aplicación, lo que mejora el rendimiento de carga de la página. |
| Solicitudes | Llamadas independientes para cada aplicación de Adobe. Las llamadas de Target son en gran medida independientes de otras llamadas de red. | Una sola llamada para todas las aplicaciones de Adobe. Los cambios en los datos pasados en estas llamadas podrían afectar a varias aplicaciones descendentes. |
| Orden de carga | La integración adecuada con otras aplicaciones de Adobe requiere un orden de carga específico de bibliotecas y llamadas de red. | La integración adecuada no depende de la vinculación de datos de distintas llamadas de red específicas a aplicaciones, por lo que el orden de carga no es un problema. |
| Edge Network | Utiliza Adobe Experience Cloud Edge Network (tt.omtrdc.net), opcionalmente con un CNAME específico de Target. | Utiliza Adobe Experience Platform Edge Network (edge.adobedc.net), opcionalmente con un solo CNAME. |
| Terminología básica | Nomenclatura de at.js: <br> - `mbox` <br> - `pageLoad` evento (mbox global) <br> - `offer` | Equivalente de Platform Web SDK: <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### Vídeo introductorio

El siguiente vídeo ofrece información general sobre Adobe Experience Platform Web SDK y Adobe Experience Platform Edge Network.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?learn=on&enablevpops)

Ahora que comprende las grandes diferencias entre at.js y Platform Web SDK, puede [planificar la migración](plan-migration.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con la migración de Target de at.js a Web SDK. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
