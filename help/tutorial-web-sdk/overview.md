---
title: Tutorial de implementación de Adobe Experience Cloud con SDK web
description: 'Obtenga información sobre cómo implementar aplicaciones de Experience Cloud mediante el SDK web de Adobe Experience Platform. '
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 7%

---

# Tutorial de implementación de Adobe Experience Cloud con SDK web

Obtenga información sobre cómo implementar aplicaciones de Experience Cloud mediante el SDK web de Adobe Experience Platform. 

Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con aplicaciones de Adobe y servicios de terceros a través de Adobe Experience Platform Edge Network. Consulte [Información general de Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge/home) para obtener información más detallada.

![Arquitectura de Experience Platform Web SDK](assets/dc-websdk.png)

Este tutorial le guía a través de la implementación de Platform Web SDK en un sitio web de venta minorista de muestra denominado Luma. El [sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) tiene una capa de datos y una funcionalidad enriquecidas que permiten crear una implementación realista. Para este tutorial, debe:

* Cree su propia propiedad de etiquetas, en su propia cuenta, con una implementación de Platform Web SDK para el sitio web de Luma.
* Configure todas las funciones de recopilación de datos para implementaciones de Web SDK como flujos de datos, esquemas y áreas de nombres de identidad.
* Añada las siguientes aplicaciones de Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (y aplicaciones creadas en plataformas como Adobe Real-Time Customer Data Platform, Adobe Journey Optimizer y Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implemente el reenvío de eventos para enviar los datos recopilados por Web SDK a destinos que no sean de Adobe.
* Valide su propia implementación de Platform Web SDK con Experience Platform Debugger y Assurance.

Después de completar este tutorial, debe estar preparado para empezar a implementar todas las aplicaciones de marketing a través de Platform Web SDK en su propio sitio web.


>[!NOTE]
>
>Hay disponible un tutorial similar de varias soluciones para [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Requisitos previos

Todos los clientes de Experience Cloud pueden utilizar Platform Web SDK. No es obligatorio obtener una licencia de una aplicación basada en Platform como Real-Time Customer Data Platform o Journey Optimizer para utilizar Web SDK.

En estas lecciones, se da por hecho que tiene una cuenta de Adobe y los permisos necesarios para completarlas. Si no es así, debe ponerse en contacto con un administrador de Experience Cloud de su empresa para obtener acceso.

* Para **recopilación de datos**, debe contar con:
   * **[!UICONTROL Plataformas]**: permiso para **[!UICONTROL Web]** y, si tiene licencia, **[!UICONTROL Edge]**
   * **[!UICONTROL Derechos de propiedad]**—permiso para **[!UICONTROL aprobar]**, **[!UICONTROL desarrollar]**, **[!UICONTROL editar propiedad]**, **[!UICONTROL administrar entornos]**, **[!UICONTROL administrar extensiones]** y **[!UICONTROL publicar]**,
   * **[!UICONTROL Derechos de compañía]**—permiso para **[!UICONTROL administrar propiedades]**

     Para obtener más información acerca de los permisos de etiquetas, consulte [la documentación](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions).

* Para **Experience Platform**, debe tener:

   * Acceso a la zona protegida **producción predeterminada**, **&quot;Prod&quot;**.
   * Acceso a **[!UICONTROL Administrar esquemas]** y **[!UICONTROL Ver esquemas]** en **[!UICONTROL Modelado de datos]**.
   * Acceso a **[!UICONTROL Administrar áreas de nombres de identidad]** y **[!UICONTROL Ver áreas de nombres de identidad]** en **[!UICONTROL Identity Management]**.
   * Acceso a **[!UICONTROL Administrar flujos de datos]** y **[!UICONTROL Ver flujos de datos]** en **[!UICONTROL Recopilación de datos]**.
   * Si es cliente de una aplicación basada en Platform y va a completar la lección [Configurar Experience Platform](setup-experience-platform.md), también debe tener lo siguiente:
      * Acceso a una zona protegida **development**.
      * Todos los elementos de permiso bajo **[!UICONTROL Administración de datos]** y **[!UICONTROL Administración de perfiles]**:

     Las funciones requeridas deben estar disponibles para todos los clientes de Experience Cloud, incluso si no es cliente de una aplicación basada en Platform como Real-Time CDP.

     Para obtener más información sobre el control de acceso a la plataforma, consulte [la documentación](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home).

* Para la lección opcional de **Adobe Analytics**, debe tener [acceso de administrador a la configuración del grupo de informes, las reglas de procesamiento y Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-console/home)

* Para la lección opcional de **Adobe Target**, debes tener acceso de [Editor o Aprobador](https://experienceleague.adobe.com/en/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80).

* Para la lección opcional de **Audience Manager**, debe tener acceso para crear, leer y escribir características, segmentos y destinos. Para obtener más información, consulte el tutorial sobre [Control de acceso basado en roles de Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).


>[!NOTE]
>
>Se da por hecho que está familiarizado con los lenguajes de desarrollo front-end como HTML y JavaScript. No necesita ser un experto en estos lenguajes, pero puede obtener más información con este tutorial si puede leer y comprender el código.

## Actualizaciones

* 24 de abril de 2024: Actualizaciones principales que incluyen la adición de Establecer variable/Actualizar variable, solicitudes de personalización y análisis divididas, lecciones de Journey Optimizer

## Carga del sitio web de Luma

Cargue el [sitio web de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} en una ficha de navegador independiente y márquelo como favorito para que pueda cargarlo fácilmente siempre que lo necesite durante el tutorial. No necesita ningún acceso adicional a Luma aparte de poder cargar nuestro sitio de producción alojado.

[![Sitio web de Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

¡Empecemos!

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Web SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
