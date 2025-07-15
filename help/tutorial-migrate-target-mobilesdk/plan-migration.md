---
title: 'Planifique la migración: Migre la implementación de Adobe Target en su aplicación móvil a la extensión de Offer Decisioning y Target'
description: Obtenga información sobre las diferencias clave entre at.js y Platform Web SDK y cómo planificar el esfuerzo de migración.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Planificación de la migración

El nivel de esfuerzo para migrar de la extensión de Target a la extensión de Offer Decisioning y Target depende de la complejidad de la implementación actual y de las funciones de Target utilizadas.

Independientemente de lo simple o compleja que sea su implementación, es importante comprender completamente su estado actual antes de migrar. Esta guía le ayuda a desglosar los componentes de la implementación actual y a desarrollar un plan manejable para migrar cada parte.

El proceso de migración incluye los siguientes pasos clave:

1. Evalúe la implementación actual y determine un enfoque de migración
1. Configuración de los componentes iniciales para conectarse a Adobe Experience Platform Edge Network
1. Actualice la implementación base para reemplazar la extensión de Target con la extensión de Offer Decisioning y Target
1. Mejore la implementación de Optimize SDK para sus casos de uso específicos. Esto puede implicar pasar parámetros adicionales, utilizar tokens de respuesta, etc.
1. Actualizar objetos en la interfaz de Target, como scripts de perfil, actividades y definiciones de audiencia
1. Valide la implementación final antes de realizar el cambio en la aplicación de producción.

>[!INFO]
>
>Dentro del ecosistema de Adobe Experience Platform Mobile SDK, las extensiones se implementan mediante SDK importados en las aplicaciones que pueden tener nombres diferentes:
>
> * **Target SDK** implementa la **extensión de Adobe Target**
> * **Optimizar SDK** implementa la extensión **Offer Decisioning and Target**


A continuación, revise la [comparación detallada de la extensión de Target y la extensión de Offer Decisioning y Target](detailed-comparison.md) para comprender mejor las diferencias técnicas e identificar las áreas que requieren un enfoque adicional.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Offer Decisioning y Target. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=es#M625).
