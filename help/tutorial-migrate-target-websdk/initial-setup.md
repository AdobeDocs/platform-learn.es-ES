---
title: Configuración inicial | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre los elementos básicos importantes necesarios para la implementación del SDK web de Platform y configúrelos
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---

# Realizar la configuración inicial de la recopilación de datos

La migración de at.js al SDK web de Platform requiere una configuración inicial para habilitar la captura de datos, las funciones y las funciones adecuadas del SDK web de Platform. Los siguientes pasos de la sección [Tutorial de implementación del SDK web de plataforma](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) debe completarse antes de que se produzca cualquier cambio en la implementación del sitio web:

- [Configuración de los permisos adecuados](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target="_blank"} en Adobe Admin Console para la recopilación de datos
- [Configuración de un esquema XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} para pasar datos estructurados a la red perimetral
- [Configuración de un área de nombres de identidad](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} para la personalización entre dispositivos y la funcionalidad mbox3rdPartyId
- [Crear un conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} para permitir el reenvío de datos desde la red perimetral
- [Configuración del conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} para permitir el reenvío de datos a Adobe Target

>[!CAUTION]
>
>Recuerde que estos aspectos del diseño deben coordinarse entre las migraciones de Target, Analytics y Audience Manager.

Una vez completada la configuración inicial, la funcionalidad de Target debe habilitarse mediante Adobe Experience Platform Edge Network.

A continuación, aprenda a [reemplace la biblioteca at.js y configure una implementación básica del SDK web de Platform](replace-library.md).

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
