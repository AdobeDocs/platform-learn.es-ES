---
title: Configuración de permisos para el tutorial
description: Obtenga información sobre cómo solicitar acceso al SDK web de Experience Platform y configurar los permisos necesarios para completar el tutorial Implementar Adobe Experience Cloud con SDK web.
feature: Web SDK,Tags,Access Control
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 3%

---

# Configuración de permisos para el tutorial

Obtenga información sobre cómo solicitar acceso al SDK web de Experience Platform y configurar los permisos necesarios para completar este tutorial. Para implementar el SDK web de Platform mediante etiquetas en la interfaz de recopilación de datos, debe tener configurados los permisos de usuario adecuados en [Admin Console](https://adminconsole.adobe.com).

## Recopilación de datos

* Tener permiso para **[!UICONTROL Desarrollar]**, **[!UICONTROL Editar]**, **[!UICONTROL Aprobar]**, **[!UICONTROL Publish]**, **[!UICONTROL Administración de extensiones]**, **[!UICONTROL Administrar entornos]**, y **[!UICONTROL Administrar propiedades]**. Para obtener más información sobre los permisos de etiquetas, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* Si va a completar la lección opcional de reenvío de eventos, tenga una licencia de producto que incluya el reenvío de Edge y un elemento de permiso **[!UICONTROL Plataformas]** > **[!UICONTROL Edge]**

## Experience Platform

Estas funciones deben estar disponibles para todos los clientes de Experience Cloud, incluso si no es cliente de una aplicación basada en Platform como Real-Time CDP.

* Acceso a la **producción predeterminada**, **&quot;Prod&quot;** zona protegida.
* Acceso a **[!UICONTROL Administrar esquemas]** y **[!UICONTROL Esquemas de vista]** bajo **[!UICONTROL Modelado de datos]**.
* Acceso a **[!UICONTROL Administrar áreas de nombres de identidad]** y **[!UICONTROL Ver áreas de nombres de identidad]** bajo **[!UICONTROL Identity Management]**.
* Acceso a **[!UICONTROL Administrar flujos de datos]** y **[!UICONTROL Ver flujos de datos]** bajo **[!UICONTROL Recopilación de datos]**.
* Si es cliente de una aplicación basada en Platform y va a completar el [Configurar Experience Platform](setup-experience-platform.md) lección, también debe tener:
   * Acceso a un **desarrollo** zona protegida.
   * Todos los elementos de permiso de **[!UICONTROL Administración de datos]**, y **[!UICONTROL Administración de perfiles]**:


Para obtener más información sobre el control de acceso a la plataforma, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=es).

## Adobe Analytics

Para la lección opcional de Adobe Analytics, debe tener [acceso de administrador a Configuración del grupo de informes, Reglas de procesamiento y Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=es)

## Adobe Target

Para la lección opcional de Adobe Target, debe tener [Editor o aprobador](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) acceso.

## Adobe Audience Manager

* Para la lección opcional de Audience Manager, debe tener acceso para crear, leer y escribir características, segmentos y destinos. Para obtener más información, consulte el tutorial sobre [Control de acceso basado en roles de Audience Manager](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

Ahora está listo para iniciar los pasos de configuración iniciales.

[Siguiente: ](configure-schemas.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
