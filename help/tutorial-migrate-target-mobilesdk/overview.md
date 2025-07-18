---
title: Migre su aplicación móvil de Adobe Target a la extensión de Offer Decisioning y Target
description: Obtenga información sobre cómo migrar la implementación de su aplicación móvil de Adobe Target a la extensión de Offer Decisioning y Target
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---

# Migre su aplicación móvil de Adobe Target a la extensión de Offer Decisioning y Target

Esta guía es para que los implementadores con experiencia en Adobe Target aprendan a migrar las implementaciones existentes de Adobe Experience Platform Mobile SDK de la extensión de Adobe Target a la extensión de Offer Decisioning y Target.

Adobe Experience Platform Mobile SDK potencia la participación integral en sus aplicaciones móviles. La extensión de Target se basa en Mobile SDK para ayudarle a personalizar las experiencias de la aplicación con Adobe Target. La extensión de Offer Decisioning y Target es un enfoque más reciente para implementar Adobe Target en aplicaciones móviles que utiliza las funcionalidades de Adobe Experience Platform Edge Network que ayudan a integrar Target con aplicaciones basadas en Platform, como Real-Time CDP y Journey Optimizer.

![Diagrama que muestra el SDK móvil conectándose a Target a través de Edge Network con la extensión Offer Decisioning y Target](assets/datacollection.png)

## Ventajas principales

Algunas de las ventajas de la extensión de Adobe Journey Optimizer Offer Decisioning y Target en comparación con la extensión de Target son:

* Se comparten audiencias más rápido desde [Real-Time Customer Data Platform](https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)
* Integrando Target con Journey Optimizer para admitir [Offer Decisioning delivery](https://experienceleague.adobe.com/es/docs/target/using/integrate/ajo/offer-decision)
* Una integración más estrecha con Adobe Analytics que no depende de la vinculación de información de llamadas de red independientes
* Flexibilidad de implementación adicional para desarrolladores

Podría decirse que la mayor ventaja de migrar para los clientes de Target es la integración con Real-Time Customer Data Platform. Real-Time CDP ofrece enormes capacidades de creación de audiencias en función de la gama completa de datos ingeridos en Experience Platform y su capacidad de Perfil del cliente en tiempo real. Un marco de trabajo de control de datos integrado automatiza el uso responsable de esos datos. La inteligencia artificial aplicada al cliente permite utilizar fácilmente modelos de aprendizaje automático para construir modelos de tendencia y pérdida cuya salida se pueda compartir de nuevo con Adobe Target. Y, por último, los clientes de los complementos opcionales de Healthcare y Privacy &amp; Security Shield pueden utilizar la función de aplicación del consentimiento para aplicar las preferencias de consentimiento de los clientes individuales. Platform Mobile SDK y la extensión de Offer Decisioning y Target son requisitos para utilizar estas funciones de Real-Time CDP en el canal móvil.

## Pasos de migración

El nivel de esfuerzo para migrar de la extensión de Target a la extensión de Offer Decisioning y Target depende de la complejidad de la implementación actual y de las funciones de Target utilizadas.

Independientemente de lo simple o compleja que sea su implementación, es importante comprender completamente su estado actual antes de migrar. Esta guía le ayuda a desglosar los componentes de la implementación actual y a desarrollar un plan manejable para migrar cada parte.

El proceso de migración incluye los siguientes pasos clave:

1. Evalúe la implementación actual, lo que incluye:
   1. Todas las API de SDK de Target utilizadas
   1. Modificaciones en la configuración global de Target
   1. Integración con Adobe Analytics
   1. Uso de parámetros de mbox, perfil y entidad
   1. Uso de scripts de perfil y audiencias
   1. Código personalizado exclusivo de la implementación
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

A continuación, revise la [comparación detallada de la extensión de Target y la extensión de Offer Decisioning y Target](comparison.md) para comprender mejor las diferencias técnicas e identificar las áreas que requieren un enfoque adicional.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Offer Decisioning y Target. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=es#M625).
