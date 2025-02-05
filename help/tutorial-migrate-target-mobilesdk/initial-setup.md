---
title: 'Configuración inicial: Migrar de Adobe Target a Adobe Journey Optimizer, extensión de Decisioning Mobile'
description: Obtenga información y configure los elementos básicos importantes necesarios para la implementación de Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 5%

---

# Realizar la configuración inicial de la recopilación de datos

La migración de Target SDK a Optimize SDK requiere una configuración inicial para permitir la captura de datos, las características y las funciones adecuadas de Optimize SDK. Se deben completar los siguientes pasos antes de que se produzca cualquier cambio en la implementación del sitio web:

- [Configure los permisos adecuados](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} en Adobe Admin Console para la recopilación de datos
- [Configurar un esquema XDM](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} para pasar datos estructurados al Edge Network
- [Configurar el esquema](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema) para recibir datos de Adobe Target
- [Configurar un área de nombres de identidad](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} para la personalización entre dispositivos y la funcionalidad mbox3rdPartyId
- [Crear una secuencia de datos](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} para habilitar el reenvío de datos del Edge Network
- [Configure la secuencia de datos](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} para habilitar el reenvío de datos a Adobe Target
- [Configurar la propiedad Tag](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension) para la extensión Decisioning

>[!BEGINTABS]

>[!TAB Extensión de destino]

Extensiones de etiquetas instaladas al utilizar la extensión de Target:

1. Mobile Core
1. Perfil
1. Adobe Target
1. Adobe Analytics (opcional, necesaria si utiliza Adobe Analytics como fuente de informes para actividades de Adobe Target)

![Extensiones de etiquetas instaladas al utilizar la extensión de Target](assets/tag-extensions-target.png)


>[!TAB Extensión de decisiones]

Extensiones de etiquetas instaladas al utilizar la extensión Decisioning:

1. Mobile Core
1. Perfil
1. Consentimiento
1. Identidad
1. Adobe Experience Platform Edge Network
1. Adobe Journey Optimizer - Toma de decisiones
1. AEP Assurance (opcional, necesaria para la depuración)

![Extensiones de etiquetas instaladas al utilizar la extensión Decisioning](assets/tag-extensions-decisioning.png)


>[!ENDTABS]

A continuación, aprenda a [reemplazar la biblioteca at.js y configurar una implementación básica de Platform Web SDK](replace-library.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
