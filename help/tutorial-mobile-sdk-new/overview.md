---
title: 'Tutorial de implementación de Adobe Experience Cloud en aplicaciones móviles: información general'
description: Obtenga información sobre cómo implementar las aplicaciones móviles de Adobe Experience Cloud. Este tutorial le guía a través de una implementación de aplicaciones Experience Cloud en una aplicación Swift de ejemplo.
recommendations: noDisplay,catalog
hide: true
exl-id: 378bdf5d-c3ce-4a4c-b188-ab9e8265627f
source-git-commit: 6726b0d0570311987b7edac4bf0cd2da35e72f30
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 6%

---

# Tutorial de implementación de Adobe Experience Cloud en aplicaciones móviles

Obtenga información sobre cómo implementar aplicaciones de Adobe Experience Cloud en su aplicación móvil mediante el SDK móvil de Adobe Experience Platform.

El SDK de Experience Platform Mobile es un SDK del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con aplicaciones de Adobe y servicios de terceros a través de Adobe Experience Platform Edge Network. Consulte la [Documentación del SDK de Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/home/) para obtener información más detallada.

![Arquitectura](assets/architecture.png)


Este tutorial le guía a través de la implementación del SDK de Platform Mobile en una aplicación de venta minorista de ejemplo llamada Luma. El [Aplicación Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) tiene una funcionalidad que le permite crear una implementación realista. Después de completar este tutorial, debe estar preparado para empezar a implementar todas las soluciones de marketing mediante el SDK de Experience Platform Mobile en sus propias aplicaciones móviles.

Las lecciones están diseñadas para iOS y escritas en Swift/SwiftUI, pero muchos de los conceptos también se aplican a Android™.

Después de completar este tutorial, debe ser capaz de:

* Cree un esquema con grupos de campos estándar y personalizados.
* Configurar una secuencia de datos.
* Configure una propiedad de etiqueta móvil.
* Configure un conjunto de datos de Experience Platform (opcional).
* Instale e implemente extensiones de etiquetas en una aplicación.
* Pasar correctamente los parámetros del Experience Cloud a un [webview](web-views.md).
* Validar la implementación mediante [Adobe Experience Platform Assurance](assurance.md).
* Añada las siguientes aplicaciones/extensiones de Adobe Experience Cloud:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Recopilación de datos del ciclo vital](lifecycle-data.md)
   * [Consentimiento](consent.md)
   * [Identidad](identity.md)
   * [Perfil](profile.md)
   * [Places](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [Mensajería push con Journey Optimizer](journey-optimizer-push.md)
   * [Mensajería en la aplicación con Journey Optimizer](journey-optimizer-inapp.md)
   * [Administración de decisiones con Journey Optimizer](journey-optimizer-offers.md)
   * [Target](target.md)


>[!NOTE]
>
>Hay disponible un tutorial similar de varias soluciones para [SDK web](../tutorial-web-sdk/overview.md).

## Requisitos previos

En estas lecciones, se da por hecho que tiene un ID de Adobe y los permisos de nivel de usuario necesarios para completar los ejercicios. Si no es así, póngase en contacto con el administrador de Adobe para solicitar el acceso.

* En la recopilación de datos, debe tener:
   * **[!UICONTROL Plataformas]**—elemento de permiso **[!UICONTROL Móvil]**
   * **[!UICONTROL Derechos de propiedad]**: elementos de permiso para **[!UICONTROL Desarrollar]**, **[!UICONTROL Aprobar]**, **[!UICONTROL Publish]**, **[!UICONTROL Administración de extensiones]**, y **[!UICONTROL Administrar entornos]**.
   * **[!UICONTROL Derechos de compañía]**: elementos de permiso para **[!UICONTROL Administrar propiedades]** y, si completa la lección opcional de mensajería push, **[!UICONTROL Administrar configuraciones de aplicación]**

     Para obtener más información sobre los permisos de etiquetas, consulte [Permisos de usuario para etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=es){target="_blank"} en la documentación del producto.
* En Experience Platform, debe tener:
   * **[!UICONTROL Modelado de datos]**: elementos de permiso para gestionar y ver esquemas.
   * **[!UICONTROL Identity Management]**: elementos de permiso para administrar y ver áreas de nombres de identidad.
   * **[!UICONTROL Recopilación de datos]**: elementos de permiso para gestionar y ver flujos de datos.

   * Si es cliente de una aplicación basada en Platform, como Real-Time CDP, Journey Optimizer o Customer Journey Analytics, y va a realizar las lecciones relacionadas que también debe tener:
      * **[!UICONTROL Administración de datos]**: elementos de permiso para administrar y ver conjuntos de datos.
      * Un desarrollo **espacio aislado** que puede utilizar para este tutorial.

   * Para las lecciones de Journey Optimizer, necesita permisos para configurar el **servicio de notificaciones push** y para crear un **superficie de aplicación**, a **recorrido**, a **message**, y **ajustes preestablecidos de mensaje**. Para la administración de decisiones, necesita los permisos adecuados para **administrar ofertas** y **decisiones** como se describe [aquí](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

* Para Adobe Analytics, debe saber cuál **grupos de informes** puede utilizar para completar este tutorial.

* Para Adobe Target, debe tener permiso para crear y activar actividades.


>[!NOTE]
>
>Como parte de este tutorial, creará esquemas, conjuntos de datos, identidades, etc. Si varias personas pasan por este tutorial en una sola zona protegida, considere la posibilidad de añadir o anteponer una identificación como parte de las convenciones de nomenclatura al crear estos objetos. Por ejemplo, añada ` - <your name or initials>` al nombre del objeto que debe crear.


## Descargar la aplicación de Luma

Hay dos versiones de la aplicación de ejemplo disponibles para descargar. Ambas versiones se pueden descargar o clonar desde [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Encontrará dos carpetas:


1. [Inicio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: un proyecto sin código o con código de marcador de posición para la mayoría del código del SDK de Experience Platform Mobile que necesita utilizar para completar los ejercicios prácticos de este tutorial.
1. [Finalizar](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: una versión con la implementación completa como referencia.

>[!NOTE]
>
>Utiliza iOS como plataforma, [!DNL Swift] como lenguaje de programación, [!DNL SwiftUI] como marco de la interfaz de usuario y [!DNL Xcode] como entorno de desarrollo integrado (IDE). Sin embargo, muchos de los conceptos de implementación explicados son similares para otras plataformas de desarrollo. Muchos ya han completado correctamente este tutorial con poca o ninguna experiencia previa de iOS/Swift (IU). No necesita ser un experto para completar las lecciones, pero obtiene más información si puede leer y comprender el código con comodidad.

>[!INFO]
>
>Si solo desea experimentar con la aplicación final, también puede descargarla directamente desde Apple App Store.
>[![Descargar](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)


¡Empecemos!

>[!SUCCESS]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Creación de un esquema XDM](create-schema.md)**
