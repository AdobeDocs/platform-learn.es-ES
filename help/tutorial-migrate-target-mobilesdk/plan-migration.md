---
title: 'Planifique la migración: Migración de Adobe Target a Adobe Journey Optimizer, extensión de Decisioning Mobile'
description: Obtenga información sobre las diferencias clave entre at.js y Platform Web SDK y cómo planificar el esfuerzo de migración.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Planificación de la migración

El nivel de esfuerzo para migrar de la extensión de Target a la extensión de Decisioning depende de la complejidad de la implementación actual y de las funciones de producto utilizadas.

Independientemente de lo simple o compleja que sea su implementación, es importante comprender completamente su estado actual antes de migrar. Esta guía le ayuda a desglosar los componentes de la implementación actual y a desarrollar un plan manejable para migrar cada parte.

El proceso de migración incluye los siguientes pasos clave:

1. Evalúe la implementación actual y determine un enfoque de migración
1. Configuración de los componentes iniciales para conectarse al Edge Network de Adobe Experience Platform
1. Actualice la implementación fundacional para reemplazar la extensión de Target y la extensión de Decisioning.
1. Mejore la implementación de Optimize SDK para sus casos de uso específicos. Esto puede implicar pasar parámetros adicionales, utilizar tokens de respuesta, etc.
1. Actualizar objetos en la interfaz de Target, como scripts de perfil, actividades y definiciones de audiencia
1. Valide la implementación final antes de realizar el cambio en el entorno de producción.

## Diferencias clave entre la extensión de Target y la extensión de Decisioning

Antes de iniciar el proceso de migración, es importante comprender las diferencias entre la extensión de Target y la extensión de Decisioning.

### Diferencias operativas

| | Target at.js 2.x | SDK web de Platform |
|---|---|---|
| Proceso | Los cambios en una implementación de Target pueden seguir un proceso que tenga una cadencia o requisitos de control de calidad diferentes a los de otras aplicaciones, como Analytics. | Los cambios en la implementación de una extensión de Decisioning deben tener en cuenta todas las aplicaciones de flujo descendente, y el control de calidad y el proceso de publicación deben ajustarse en consecuencia. |
| Colaboración | Los datos específicos de Target se pueden pasar directamente en las llamadas de Target. Si la fuente de informes de Target es Adobe Analytics, también se pueden pasar datos específicos de Target a Adobe Analytics cuando se soliciten los métodos de seguimiento adecuados en la extensión de Target para la visualización y la interacción del contenido de Target. | Los datos pasados en las llamadas de extensión de Decisioning se pueden reenviar tanto a Target como a Analytics si la fuente de informes de Target es Adobe Analytics, Adobe Analytics está habilitado en el flujo de datos y se llama a los métodos de seguimiento adecuados en la extensión de Decisioning cuando se muestra contenido de Target y se interactúa con él. |

### Diferencias técnicas

| | Extensión de Target | Extensión de Decisioning |
|---|---|---|
| Dependencias | Solo depende de Mobile Core SDK | Depende de Mobile Core y Edge Network SDK |
| Funcionalidad de biblioteca | Admite recuperar contenido solo de Adobe Target | Compatibilidad con la recuperación de contenido desde Adobe Target y Offer decisioning |
| Solicitudes | Las llamadas de Target son en gran medida independientes de otras llamadas de red | Las llamadas de red de Target se ponen en cola junto con las llamadas de red para otras soluciones basadas en Edge, como Mensajería en Edge SDK, y se ejecutan en serie. |
| Edge Network | Utiliza el valor del servidor de Target o el Edge Network de Adobe Experience Cloud con el código de cliente (clientcode.tt.omtrdc.net), ambos especificados en la [configuración de Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) en la IU de recopilación de datos | Utiliza el dominio de red de Edge especificado en la [configuración del Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) de Adobe Experience Platform en la IU de recopilación de datos. |
| Terminología básica | mbox, TargetParameters | DecisionScope, Map (Android)/dictionary (iOS) para parámetros de destinatario |
| Contenido predeterminado | Permite pasar contenido predeterminado del lado del cliente en TargetRequest, que se devuelve si la llamada de red falla o genera un error. | No permite pasar contenido predeterminado del lado del cliente. No devuelve ningún contenido si la llamada de red falla o genera un error. |
| Parámetros de destino | Permite pasar TargetParameters globales por solicitud y diferentes TargetParameters por mbox | Permite pasar TargetParameters globales solo por solicitud |

A continuación, revise la [comparación detallada de la extensión de Target y la extensión de Decisioning](detailed-comparison.md) para comprender mejor las diferencias técnicas e identificar las áreas que requieren un enfoque adicional.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
