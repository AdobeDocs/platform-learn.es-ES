---
title: 'Configuración inicial: Migre la implementación de Adobe Target en su aplicación móvil a la extensión Adobe Journey Optimizer - Decisioning'
description: Obtenga información y configure los elementos básicos importantes necesarios para la implementación de Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 6%

---

# Realizar la configuración inicial de la recopilación de datos

La migración de Target SDK a Optimize SDK requiere una configuración inicial para permitir la captura de datos, las características y las funciones adecuadas de Optimize SDK. Se deben completar los siguientes pasos antes de que se produzca cualquier cambio en la implementación del sitio web:

- [Configure los permisos adecuados](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} en Adobe Admin Console para la recopilación de datos
- [Configurar un esquema XDM](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} para pasar datos estructurados a Edge Network
- [Configurar el esquema](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} para recibir datos de Adobe Target
- [Configurar un área de nombres de identidad](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} para la personalización entre dispositivos y la funcionalidad mbox3rdPartyId
- [Crear una secuencia de datos](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} para habilitar el reenvío de datos desde Edge Network
- [Configure la secuencia de datos](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} para habilitar el reenvío de datos a Adobe Target
- [Configurar la propiedad Tag](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} para la extensión Decisioning

## Configuración de extensión

>[!BEGINTABS]

>[!TAB Extensión de decisiones]

Extensiones de etiquetas instaladas al utilizar la extensión Decisioning:

1. Adobe Journey Optimizer - Toma de decisiones
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Perfil
1. Consentimiento
1. Identidad
1. AEP Assurance (opcional, necesaria para la depuración)

![Extensiones de etiquetas instaladas al utilizar la extensión Decisioning](assets/tag-extensions-decisioning.png)

>[!TAB Extensión de destino]

Extensiones de etiquetas instaladas al utilizar la extensión de Target:

1. Adobe Target
1. Mobile Core
1. Perfil
1. Adobe Analytics (opcional, necesaria si utiliza Adobe Analytics como fuente de informes para actividades de Adobe Target)

![Extensiones de etiquetas instaladas al utilizar la extensión de Target](assets/tag-extensions-target.png)

>[!ENDTABS]

## Configuración de flujo de datos

La extensión de Target tiene [configuraciones configurables](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) que con la extensión de Decisions están [configuradas en la secuencia de datos](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup).

| Extensión de Target | Extensión de Decisioning | Notas |
| --- | --- | --- | 
| Código de cliente | n/a | Establecido automáticamente por el perímetro de mediante los detalles de organización de IMS |
| ID de entorno | ID de entorno de destino | Configurado en el conjunto de datos |
| Propiedad de Workspace de destino | Token de propiedad | Configurado en el conjunto de datos |
| Tiempo de espera | No configurable | El tiempo de espera con la extensión Decisioning es de 10 segundos |
| Dominio del servidor | dominio de Edge Network | Establecido en la extensión de Adobe Experience Platform Edge Network |

A continuación, aprenda a [reemplazar Target SDK](replace-sdk.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
