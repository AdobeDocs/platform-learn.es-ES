---
title: 'Tutorial de implementación de Adobe Experience Cloud en aplicaciones móviles: información general'
description: Obtenga información sobre cómo implementar las aplicaciones móviles de Adobe Experience Cloud. Este tutorial le guía a través de una implementación de aplicaciones de Experience Cloud en una aplicación Swift de ejemplo.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 9129d7ab2ac33626240b0375e6424c0f6943290f
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---

# Tutorial de implementación de Adobe Experience Cloud en aplicaciones móviles

Obtenga información sobre cómo implementar aplicaciones de Adobe Experience Cloud en su aplicación móvil mediante Adobe Experience Platform Mobile SDK.

Experience Platform Mobile SDK es un SDK del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con aplicaciones de Adobe y servicios de terceros a través de Adobe Experience Platform Edge Network. Consulte la [documentación de Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) para obtener información más detallada.

![Arquitectura](assets/architecture.png){zoomable="yes"}


Este tutorial le guía a través de la implementación de Platform Mobile SDK en una aplicación de ejemplo llamada Luma. La aplicación de Luma tiene una funcionalidad que le permite crear una implementación realista. Después de completar este tutorial, debe estar preparado para empezar a implementar todas las soluciones de marketing a través de Experience Platform Mobile SDK en sus propias aplicaciones móviles.

Las lecciones están diseñadas para:

* iOS, utilizando el lenguaje de programación Swift y el marco de trabajo SwiftUI.
* Android, utilizando el lenguaje de programación Kotlin y Java y el módulo JetPack Compose.

Después de completar este tutorial, debe ser capaz de:

* Cree un esquema con grupos de campos estándar y personalizados.
* Configurar una secuencia de datos.
* Configure una propiedad de etiqueta móvil.
* Configure un conjunto de datos de Experience Platform (opcional).
* Instale e implemente extensiones de etiquetas en una aplicación.
* Pasar correctamente los parámetros de Experience Cloud a [webview](web-views.md).
* Valide la implementación con [Adobe Experience Platform Assurance](assurance.md).
* Añada las siguientes aplicaciones o extensiones de Adobe Experience Cloud:
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
>Hay disponible un tutorial similar de varias soluciones para [Web SDK](../tutorial-web-sdk/overview.md).

## Permisos

En estas lecciones, se da por hecho que dispone de un Adobe ID y de los permisos de nivel de usuario necesarios para completar los ejercicios. Si no es así, póngase en contacto con el administrador de Adobe para solicitar el acceso.

* En la recopilación de datos, debe tener:
   * **[!UICONTROL Plataformas]**: elemento de permiso **[!UICONTROL Móvil]**
   * **[!UICONTROL Derechos de propiedad]**: elementos de permiso para **[!UICONTROL desarrollar]**, **[!UICONTROL aprobar]**, **[!UICONTROL publicar]**, **[!UICONTROL administrar extensiones]** y **[!UICONTROL administrar entornos]**.
   * **[!UICONTROL Derechos de compañía]**—elementos de permiso para **[!UICONTROL Administrar propiedades]**

     Para obtener más información sobre los permisos de etiquetas, consulte [Permisos de usuario para etiquetas](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions){target="_blank"} en la documentación del producto.
* En Experience Platform, debe tener:
   * **[!UICONTROL Modelado de datos]**: elementos de permiso para administrar y ver esquemas.
   * **[!UICONTROL Identity Management]**: elementos de permiso para administrar y ver áreas de nombres de identidad.
   * **[!UICONTROL Recopilación de datos]**: elementos de permiso para administrar y ver flujos de datos.

   * Si es cliente de una aplicación basada en Platform como Real-Time CDP, Journey Optimizer o Customer Journey Analytics, y planea hacer las lecciones relacionadas también debe tener:
      * **[!UICONTROL Administración de datos]**: elementos de permiso para administrar y ver conjuntos de datos.
      * Una **zona protegida** de desarrollo que puede usar para este tutorial.

   * Para las lecciones de Journey Optimizer, necesita permisos para configurar el **servicio de notificaciones push** y crear una **superficie de aplicación**, un **recorrido**, un **mensaje** y **ajustes preestablecidos de mensaje**. Además, para Administración de decisiones, necesita los permisos adecuados para **administrar ofertas** y **decisiones**, tal como se describe en [Niveles de permisos](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/high-low-permissions).

* Para Adobe Analytics, debe saber qué **grupos de informes** puede utilizar para completar este tutorial.

* Para Adobe Target, debe tener permiso para crear y activar actividades.


>[!NOTE]
>
>Como parte de este tutorial, creará esquemas, conjuntos de datos, identidades, etc. Si varias personas pasan por este tutorial en una sola zona protegida, considere la posibilidad de añadir o anteponer una identificación como parte de las convenciones de nomenclatura al crear estos objetos. Por ejemplo, agregue ` - <your name or initials>` al nombre del objeto que debe crear.

## Historial de versiones

* 9 de septiembre de 2025:
   * Versión de Android de la aplicación con instrucciones correspondientes.
   * Actualizaciones de cambios en la superficie de la aplicación y la funcionalidad de la campaña en Journey Optimizer.
* 29 de noviembre de 2023: revisión general con una nueva aplicación de ejemplo y nuevas lecciones para la mensajería en la aplicación, la administración de decisiones y Adobe Target.
* 9 de marzo de 2022: Primera publicación

## Descargar la aplicación de Luma

>[!BEGINTABS]

>[!TAB iOS]

Hay dos versiones de la aplicación de ejemplo disponibles para descargar. Ambas versiones se pueden descargar o clonar desde [GitHub](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Encontrará dos carpetas:

1. [Inicio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: un proyecto sin código o con código de marcador de posición para la mayoría del código de Experience Platform Mobile SDK que necesita usar para completar los ejercicios prácticos de este tutorial.
1. [Finalizar](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: una versión con la implementación completa como referencia.

Utiliza iOS como plataforma, [!DNL Swift] como lenguaje de programación, [!DNL SwiftUI] como marco de la interfaz de usuario y [!DNL Xcode] como entorno de desarrollo integrado (IDE). Sin embargo, muchos de los conceptos de implementación explicados son similares para otras plataformas de desarrollo. Muchos ya han completado correctamente este tutorial con poca o ninguna experiencia de desarrollo previa de iOS y Swift (IU). No necesita ser un experto para completar las lecciones, pero obtiene más información si puede leer y comprender el código con comodidad.

Puede descargar la versión final producida de la aplicación desde App Store.

[![Descargar](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)

>[!TAB Android]

Hay dos versiones de la aplicación de ejemplo disponibles para descargar. Ambas versiones se pueden descargar o clonar desde [GitHub](https://github.com/adobe/Luma-Android). Encontrará dos carpetas:

1. [Inicio](https://github.com/adobe/Luma-Android){target="_blank"}: un proyecto sin código o con código de marcador de posición para la mayoría del código de Experience Platform Mobile SDK que necesita usar para completar los ejercicios prácticos de este tutorial.
1. [Finalizar](https://github.com/adobe/Luma-Android){target="_blank"}: una versión con la implementación completa como referencia.

Utiliza Android como plataforma, [!DNL Kotlin]+[!DNL Java] como lenguaje de programación, [!DNL JetPack Compose] como marco de la interfaz de usuario y [!DNL Android Studio] como entorno de desarrollo integrado (IDE). Sin embargo, muchos de los conceptos de implementación explicados son similares para otras plataformas de desarrollo. Muchos ya han completado con éxito este tutorial con poca o ninguna experiencia previa de Android / Kotlin+Java / JetPack Compose. No necesita ser un experto para completar las lecciones, pero obtiene más información si puede leer y comprender el código con comodidad.

Si lo prefiere, puede [unirse a una prueba para obtener una versión de la aplicación con productos](https://play.google.com/apps/internaltest/4700642199234438150) de Google Play.


>[!ENDTABS]

¡Empecemos!

>[!SUCCESS]
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Crear un esquema XDM](create-schema.md)**
