---
title: Información general sobre la implementación de Adobe Experience Cloud en aplicaciones móviles
description: Obtenga información sobre cómo implementar las aplicaciones móviles de Adobe Experience Cloud. Este tutorial le guía a través de la implementación de aplicaciones Experience Cloud en una aplicación Swift de ejemplo.
recommendation: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 10%

---

# Tutorial de implementación de Adobe Experience Cloud en aplicaciones móviles

Obtenga información sobre cómo implementar aplicaciones de Adobe Experience Cloud en su aplicación móvil mediante el SDK móvil de Adobe Experience Platform.

El SDK de Experience Platform Mobile es un SDK del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con aplicaciones de Adobe y servicios de terceros a través de Adobe Experience Platform Edge Network. Consulte la [Documentación del SDK de Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/) para obtener información más detallada.

![configuración de creación](assets/data-collection-mobile-sdk.png)


Este tutorial le guía a través de la implementación del SDK de Platform Mobile en una aplicación minorista de ejemplo llamada Luma. La variable [Aplicación de Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) tiene una funcionalidad que le permite crear una implementación realista. Después de completar este tutorial, debe estar listo para empezar a implementar todas las soluciones de marketing a través del SDK de Platform Mobile en sus propias aplicaciones móviles.

Las lecciones están diseñadas para iOS y escritas en Swift, pero muchos de los conceptos también se aplican a Android™.

Después de completar este tutorial, podrá:

* Cree un esquema utilizando grupos de campos estándar y personalizados.
* Configure un conjunto de datos.
* Configure una propiedad de etiqueta móvil.
* Configure un conjunto de datos de Experience Platform (opcional).
* Instale e implemente extensiones de etiquetas en una aplicación.
* Añada las siguientes aplicaciones/extensiones de Adobe Experience Cloud:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Recopilación de datos del ciclo vital](lifecycle-data.md)
   * [Adobe Analytics mediante XDM](analytics.md)
   * [Consentimiento](consent.md)
   * [Identidad](identity.md)
   * [Perfil](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [Mensajería push con Journey Optimizer](journey-optimizer-push.md)
* Pasar correctamente los parámetros del Experience Cloud a un [webview](web-views.md).
* Validar la implementación mediante [Adobe Experience Platform Assurance](assurance.md).

>[!NOTE]
>
>Hay disponible un tutorial de varias soluciones similar para [SDK web](../tutorial-web-sdk/overview.md).

## Requisitos previos

En estas lecciones, se da por hecho que dispone de un Adobe ID y de los permisos necesarios para completar los ejercicios. Si no es así, debe ponerse en contacto con el administrador de Adobe para solicitar acceso.

* En la recopilación de datos debe tener:
   * **[!UICONTROL Plataformas]**—elemento de permiso **[!UICONTROL Móvil]**
   * **[!UICONTROL Derechos de propiedad]**: elementos de permiso para **[!UICONTROL Desarrollo]**, **[!UICONTROL Aprobar]**, **[!UICONTROL Publicación]**, **[!UICONTROL Administrar extensiones]** y **[!UICONTROL Administrar entornos]**.
   * **[!UICONTROL Derechos de compañía]**: elementos de permiso para **[!UICONTROL Administrar propiedades]** y, si completa la lección de mensajería push opcional, **[!UICONTROL Administrar configuraciones de aplicación]**

      Para obtener más información sobre los permisos de etiquetas, consulte [Permisos de usuario para etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=es){target=&quot;_blank&quot;} en la documentación del producto.
* En Experience Platform, debe tener:
   * **[!UICONTROL Modelado de datos]**: elementos de permiso para administrar y ver esquemas.
   * **[!UICONTROL Identity Management]**: elementos de permiso para administrar y ver áreas de nombres de identidad.
   * **[!UICONTROL Recopilación de datos]**: elementos de permiso para administrar y ver conjuntos de datos.

   * Si es cliente de una aplicación basada en Platform como Real-Time CDP, Journey Optimizer o Customer Journey Analytics, también debería tener:
      * **[!UICONTROL Gestión de datos]**: elementos de permiso para administrar y ver conjuntos de datos para completar la variable _ejercicios opcionales de plataforma_ (requiere una licencia para una aplicación basada en Platform ).
      * Un desarrollo **entorno limitado** que puede utilizar para este tutorial.
* Para Adobe Analytics, debe saber cuál **grupos de informes** puede utilizar para completar este tutorial.

Todos los clientes Experience Cloud deben tener acceso a las funciones necesarias para implementar el SDK móvil.

Además, se da por hecho que está familiarizado con [!DNL Swift]. No necesita ser experto para completar las lecciones, pero obtendrá más información si puede leer y comprender el código con comodidad.

## Descargar la aplicación de Luma

Hay dos versiones de la aplicación de ejemplo disponibles para descargar.

1. [Vacío](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} - versión sin código de Experience Cloud para completar los ejercicios prácticos en este tutorial
1. [Completa implementada](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} - versión con implementación de Experience Cloud completa para referencia.

¡Empecemos!


Siguiente: **[Creación de un esquema XDM](create-schema.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)