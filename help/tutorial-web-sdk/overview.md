---
title: Tutorial de implementación de Adobe Experience Cloud con SDK web
description: Obtenga información sobre cómo implementar aplicaciones de Experience Cloud mediante el SDK web de Adobe Experience Platform.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 26%

---

# Tutorial de implementación de Adobe Experience Cloud con SDK web

Obtenga información sobre cómo implementar aplicaciones de Experience Cloud mediante el SDK web de Adobe Experience Platform.

El SDK web de Experience Platform es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con aplicaciones de Adobe y servicios de terceros a través de Adobe Experience Platform Edge Network. Consulte [Información general del SDK web de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es) para obtener información más detallada.

Este tutorial le guía a través de la implementación del SDK web de Platform en un sitio web de venta minorista de muestra denominado Luma. El sitio de [](https://luma.enablementadobe.com/content/luma/us/en.html)Luma tiene una capa de datos y una funcionalidad enriquecidas que permiten crear una implementación realista. Después de completar este tutorial, debe estar preparado para empezar a implementar todas las soluciones de marketing a través del SDK web de Platform en su propio sitio web.

[![Sitio web de Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## Objetivos de aprendizaje

Después de completar el tutorial, debe ser capaz de:

* Configuración de flujos de datos

* Creación de esquemas XDM

* Añada las siguientes aplicaciones de Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (y aplicaciones creadas en Platform como Adobe Real-time Customer Data Platform, Adobe Journey Optimizer y Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* Creación de reglas de etiquetas y elementos de datos de objeto XDM para enviar datos a aplicaciones de Adobe

* Validar la implementación con el Adobe Experience Platform Debugger

* Capturar el consentimiento del usuario

* Reenviar datos a terceros mediante el reenvío de eventos

>[!NOTE]
>
>Hay disponible un tutorial similar de varias soluciones para [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Requisitos previos

Todos los clientes de Experience Cloud pueden utilizar el SDK web de Platform. No es necesario obtener una licencia de una aplicación basada en Platform como Real-time Customer Data Platform o Journey Optimizer para utilizar el SDK web.

En estas lecciones, se da por hecho que tiene una cuenta Adobe y la variable [permisos necesarios](configure-permissions.md) para completar las lecciones. Si no es así, debe ponerse en contacto con el administrador del Experience Cloud para solicitar el acceso.

Además, se da por hecho que está familiarizado con los lenguajes de desarrollo front-end como HTML y JavaScript. No necesita ser un experto en estos lenguajes, pero puede obtener más información con este tutorial si puede leer y comprender el código.

¡Empecemos!

[Siguiente: ](configure-permissions.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
