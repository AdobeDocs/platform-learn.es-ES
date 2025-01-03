---
title: 'Configuración inicial: Migrar de Adobe Target a Adobe Journey Optimizer, extensión de Decisioning Mobile'
description: Obtenga información y configure los elementos básicos importantes necesarios para la implementación del SDK web de Platform
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Realizar la configuración inicial de la recopilación de datos

La migración de at.js al SDK web de Platform requiere una configuración inicial para permitir la captura de datos, las características y las funciones adecuadas del SDK web de Platform. Los siguientes pasos del [tutorial de implementación del SDK web de Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) deben completarse antes de que se produzca cualquier cambio en la implementación del sitio web:

- [Configure los permisos adecuados](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} en Adobe Admin Console para la recopilación de datos
- [Configurar un esquema XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} para pasar datos estructurados al Edge Network
- [Configurar un área de nombres de identidad](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} para la personalización entre dispositivos y la funcionalidad mbox3rdPartyId
- [Crear una secuencia de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} para habilitar el reenvío de datos del Edge Network
- [Configure la secuencia de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} para habilitar el reenvío de datos a Adobe Target

>[!CAUTION]
>
>Recuerde que estos aspectos del diseño deben coordinarse entre Target, Analytics y las migraciones de Audience Manager.

Una vez completada la configuración inicial, la funcionalidad de Target debe habilitarse con el Edge Network de Adobe Experience Platform.

A continuación, aprenda a [reemplazar la biblioteca at.js y configurar una implementación básica del SDK web de Platform](replace-library.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
