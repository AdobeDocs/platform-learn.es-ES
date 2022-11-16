---
title: Implementar el Experience Cloud en sitios web con etiquetas
description: Implementar el Experience Cloud en sitios web con etiquetas es el punto de partida perfecto para los desarrolladores de front-end o los especialistas en marketing técnico que deseen aprender a implementar las soluciones de Adobe Experience Cloud en su sitio web.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 43%

---

# Información general

_Implementar el Experience Cloud en sitios web con etiquetas_ es el punto de partida perfecto para desarrolladores de front-end o especialistas en marketing técnico que deseen aprender a implementar las soluciones de Adobe Experience Cloud en su sitio web.

Cada lección contiene ejercicios prácticos e información fundamental para ayudarle a implementar Experience Cloud y comprender su valor.  Se proporcionan sitios de muestra para completar el tutorial, lo que le permite aprender las técnicas subyacentes en un entorno seguro. Después de completar este tutorial, debe estar listo para empezar a implementar todas las soluciones de marketing a través de etiquetas en su propio sitio web.

>[!INFO]
>
>Este tutorial utiliza bibliotecas y extensiones específicas de la aplicación (AppMeasurement.js para Adobe Analytics, at.js para Adobe Target). Si desea implementar el SDK web de Adobe Experience Platform, consulte la [Implementación de Adobe Experience Cloud con SDK web](/help/tutorial-web-sdk/overview.md) tutorial.


Tras completar esta formación, debe ser capaz de:

* Crear una propiedad de etiqueta

* Instalar una propiedad de etiqueta en un sitio web

* Añadir las siguientes soluciones de Adobe Experience Cloud:
   * **[Servicio de ID de Adobe Experience Platform](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* Crear reglas y elementos de datos para enviar datos a las soluciones de Adobe.

* Validar la implementación con Adobe Experience Cloud Debugger.

* Publicar cambios mediante entornos de desarrollo, ensayo y producción

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al usar este contenido:
>
> * El platform launch (lado del cliente) ya está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El servidor de platform launch está ahora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Las configuraciones de Edge ahora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**


>[!NOTE]
>
>También hay tutoriales de varias soluciones similares disponibles para [SDK web](../tutorial-web-sdk/overview.md) y [SDK móvil](../tutorial-mobile-sdk/overview.md).

## Requisitos previos

En estas lecciones, se da por hecho que dispone de un Adobe ID y de los permisos necesarios para completar los ejercicios. Si no es así, es posible que deba ponerse en contacto con el administrador de Experience Cloud para solicitar acceso.

* Para las etiquetas, debe tener permiso para desarrollar, aprobar, publicar, administrar extensiones y administrar entornos. Para obtener más información sobre los permisos de usuario de etiquetas, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* Para Adobe Analytics, debe conocer su servidor de seguimiento y qué grupos de informes desea utilizar para completar este tutorial.
* Para el Audience Manager, debe conocer su subdominio de Audience Manager (también conocido como &quot;nombre de socio&quot;, &quot;ID de socio&quot; o &quot;subdominio de socio&quot;)

Además, se da por hecho que está familiarizado con los lenguajes de desarrollo front-end como HTML y JavaScript. No necesita ser experto en estos idiomas para completar las lecciones, pero obtendrá más información si puede leer y comprender el código con comodidad.

## Acerca de las etiquetas

La función de etiquetas de Adobe Experience Platform es la nueva generación de funcionalidades de administración de etiquetas de sitios web y SDK móvil de Adobe. Etiquetas ofrece una alternativa sencilla para implementar y gestionar todas las soluciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes. Las etiquetas no suponen ningún coste adicional. Está disponible para cualquier cliente de Adobe Experience Cloud.

Las etiquetas de sitios web le permiten administrar de forma centralizada todo el código JavaScript relacionado con las soluciones de análisis, marketing y publicidad que se usan en los sitios de escritorio y móviles. Por ejemplo, si implementa Adobe Analytics, las etiquetas administrarán la biblioteca JavaScript de AppMeasurement, rellenarán las variables y activarán las solicitudes.

El contenido del contenedor se minimiza, incluido el código personalizado. Todo es modular. Si no necesita un elemento, este no se incluye en la biblioteca. El resultado es una implementación rápida y compacta.

Tags es también una plataforma que permite a los proveedores externos crear extensiones para facilitar la implementación de sus soluciones mediante etiquetas. Una extensión es un paquete de código (JavaScript, HTML y CSS) que amplía la interfaz de etiquetas y la funcionalidad del cliente. Puede considerar las etiquetas como un sistema operativo y las extensiones como las aplicaciones que utiliza para realizar sus tareas.

## Acerca de las lecciones

En estas lecciones, debe implementar Adobe Experience Cloud en un sitio web de venta minorista ficticio denominado Luma. El [sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) tiene una capa de datos y una funcionalidad enriquecidas que permiten crear una implementación realista. Construirá su propia propiedad de etiqueta, en su propia organización de Experience Cloud, y la asignará a nuestro sitio de Luma alojado mediante el Experience Cloud Debugger .

[![Sitio web de Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Obtención de las herramientas

1. Ya que se utilizan varias extensiones específicas del navegador, le recomendamos que complete el tutorial utilizando el navegador web [Chrome](https://www.google.com/chrome/).
1. Añada la extensión de [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) a su navegador.
1. Descargue la [página HTML de ejemplo](https://www.enablementadobe.com/multi/web/basic-sample.html) (haga clic con el botón derecho en este vínculo y haga clic en “Guardar vínculo como”).
1. Obtenga un editor de texto en el que pueda realizar cambios en la página HTML de ejemplo. (Si no tiene uno, le recomendamos que pruebe [Brackets](https://brackets.io/)).
1. Marcar el sitio de [Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!NOTE]
>
>Puede que le resulte más fácil completar este tutorial con el sitio de Luma abierto en Chrome, mientras lee este tutorial y completa los pasos de la interfaz de recopilación de datos en un explorador diferente.

¡Empecemos!

[Siguiente: &quot;Crear una propiedad de etiqueta&quot; >](create-a-property.md)
