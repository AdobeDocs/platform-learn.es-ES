---
title: 'Migración de Adobe Target a Adobe Journey Optimizer: extensión de Decisioning Mobile'
description: Obtenga información sobre cómo migrar la implementación de su aplicación móvil de Adobe Target a la extensión Adobe Journey Optimizer - Decisioning
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Migración de Adobe Target a Adobe Journey Optimizer: extensión de Decisioning Mobile

Esta guía es para que los implementadores con experiencia en Adobe Target aprendan a migrar las implementaciones existentes de Adobe Experience Platform Mobile SDK de la extensión de Adobe Target a la extensión Adobe Journey Optimizer - Decisioning.

Adobe Experience Platform Mobile SDK potencia la participación integral en sus aplicaciones móviles. La extensión de Target se basa en Mobile SDK para ayudarle a personalizar las experiencias de la aplicación con Adobe Target. La extensión de Decisioning es un enfoque más reciente para implementar Adobe Target en aplicaciones móviles que utiliza funciones de Edge Network de Adobe Experience Platform que ayudan a integrar Target con aplicaciones basadas en Platform, como Real-Time CDP y Journey Optimizer.

## Ventajas principales

Algunas de las ventajas de la extensión de Adobe Journey Optimizer Decisioning en comparación con la extensión de Target son:

* Se comparten audiencias más rápido desde [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)
* Integrando Target con Journey Optimizer para admitir [entrega de Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Una integración más estrecha con Adobe Analytics que no depende de la vinculación de información de llamadas de red independientes
* Flexibilidad de implementación adicional para desarrolladores

Podría decirse que la mayor ventaja de migrar para los clientes de Target es la integración con Real-time Customer Data Platform. Real-Time CDP ofrece enormes capacidades de creación de audiencias en función de la gama completa de datos introducidos en Experience Platform y su capacidad de Perfil del cliente en tiempo real. Un marco de trabajo de control de datos integrado automatiza el uso responsable de esos datos. La inteligencia artificial aplicada al cliente permite utilizar fácilmente modelos de aprendizaje automático para construir modelos de tendencia y pérdida cuya salida se pueda compartir de nuevo con Adobe Target. Por último, los clientes de los complementos opcionales de Healthcare y Privacy &amp; Security Shield pueden utilizar la función de aplicación del consentimiento para aplicar fácilmente las preferencias de consentimiento de los clientes individuales. Platform Mobile SDK y la extensión Decisioning son requisitos para utilizar estas funciones de Real-Time CDP en el canal móvil.


>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
