---
title: Implementar el Experience Cloud de en sitios web con etiquetas
description: La implementación del Experience Cloud en sitios web con etiquetas es el punto de partida perfecto para desarrolladores de front-end o especialistas en marketing técnico que deseen aprender a implementar las soluciones de Adobe Experience Cloud en su sitio web.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 39%

---

# Información general

_Implementar el Experience Cloud de en sitios web con etiquetas_ es el punto de partida perfecto para desarrolladores de front-end o especialistas en marketing técnico que deseen aprender a implementar las soluciones de Adobe Experience Cloud en su sitio web.

Cada lección contiene ejercicios prácticos e información fundamental para ayudarle a implementar Experience Cloud y comprender su valor.  Se proporcionan sitios de muestra para completar el tutorial, lo que le permite aprender las técnicas subyacentes en un entorno seguro. Después de completar este tutorial, debe estar preparado para empezar a implementar todas las soluciones de marketing a través de las etiquetas en su propio sitio web.

>[!INFO]
>
>Este tutorial utiliza extensiones y bibliotecas específicas de la aplicación (AppMeasurement.js para Adobe Analytics, at.js para Adobe Target). Si desea implementar el SDK web de Adobe Experience Platform, consulte la [Implementar Adobe Experience Cloud con SDK web](/help/tutorial-web-sdk/overview.md) tutorial.


Tras completar esta formación, debe ser capaz de:

* Creación de una propiedad de etiqueta

* Instalación de una propiedad de etiquetas en un sitio web

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
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al utilizar este contenido:
>
> * El platform launch (lado del cliente) ahora es **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El lado del servidor de platform launch ahora es **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Las configuraciones de Edge ahora son **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**

>[!NOTE]
>
>También hay tutoriales de varias soluciones similares disponibles para [SDK web](../tutorial-web-sdk/overview.md) y [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Requisitos previos

En estas lecciones, se da por hecho que dispone de un Adobe ID y de los permisos necesarios para completar los ejercicios. Si no es así, es posible que deba ponerse en contacto con el administrador de Experience Cloud para solicitar acceso.

* Para las etiquetas, debe tener permiso para desarrollar, aprobar, publicar, gestionar extensiones y entornos. Para obtener más información sobre los permisos de usuario de etiquetas, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* Para Adobe Analytics, debe conocer su servidor de seguimiento y qué grupos de informes desea utilizar para completar este tutorial.
* Para Audience Manager, debe conocer su subdominio de Audience Manager (también conocido como &quot;nombre de socio&quot;, &quot;ID de socio&quot; o &quot;subdominio de socio&quot;)

Además, se da por hecho que está familiarizado con los lenguajes de desarrollo front-end como HTML y JavaScript. No necesita ser un experto en estos lenguajes para completar las lecciones, pero obtendrá más información si puede leer y comprender el código con comodidad.

## Acerca de las etiquetas

La función de etiquetas de Adobe Experience Platform es la nueva generación de funcionalidades de administración de etiquetas de sitios web y SDK móvil de Adobe. Las etiquetas ofrecen a los clientes una alternativa sencilla para implementar y gestionar todas las soluciones de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Las etiquetas no suponen ningún coste adicional. Está disponible para cualquier cliente de Adobe Experience Cloud.

Las etiquetas para sitios web le permiten administrar de forma centralizada todo el código JavaScript relacionado con las soluciones de análisis, marketing y publicidad utilizadas en los sitios con versión escritorio y móviles. Por ejemplo, si implementa Adobe Analytics, las etiquetas administran la biblioteca JavaScript de AppMeasurement, rellenan variables y activan solicitudes.

El contenido del contenedor se minimiza, incluido el código personalizado. Todo es modular. Si no necesita un elemento, este no se incluye en la biblioteca. El resultado es una implementación rápida y compacta.

Las etiquetas también son una plataforma que permite a los proveedores externos crear extensiones para facilitar la implementación de sus soluciones mediante etiquetas. Una extensión es un paquete de código (JavaScript, HTML y CSS) que amplía la interfaz de etiquetas y la funcionalidad del cliente. Podríamos equiparar las etiquetas con un sistema operativo y las extensiones con las aplicaciones que usa para realizar sus tareas.

## Acerca de las lecciones

En estas lecciones, debe implementar Adobe Experience Cloud en un sitio web de venta minorista ficticio denominado Luma. El [sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) tiene una capa de datos y una funcionalidad enriquecidas que permiten crear una implementación realista. Debe crear su propia propiedad de etiquetas, en su propia organización de Experience Cloud, y asignarla a nuestro sitio de Luma alojado mediante el Experience Cloud Debugger.

[![Sitio web de Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Obtención de las herramientas

1. Ya que se utilizan varias extensiones específicas del navegador, le recomendamos que complete el tutorial utilizando el navegador web [Chrome](https://www.google.com/chrome/).
1. Añada el [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Extensión de a su explorador Chrome
1. Copie el código de página HTML de ejemplo

   +++Código de página HTML de muestra

   ```html
   <!doctype html>
   <html lang="en">
   <head>
       <title>Tags: Sample HTML Page</title>
       <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
       <link rel="preconnect" href="//dpm.demdex.net">
       <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//cm.everesttech.net">
       <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
       <link rel="dns-prefetch" href="//dpm.demdex.net">
       <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//cm.everesttech.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
       <!--/Preconnect and DNS-Prefetch-->
       <!--Data Layer to enable rich data collection and targeting-->
       <script>
       var digitalData = {
           "page": {
               "pageInfo" : {
                   "pageName": "Home"
                   }
               }
       };
       </script>
       <!--/Data Layer-->
       <!--jQuery or other helper libraries-->
       <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
       <!--/jQuery-->
       <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
       <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
       <!--/Tags Header Embed Code-->
   </head>
   <body>
       <h1>Tags: Sample HTML Page</h1>
       <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
       <p>See <a href="https://docs.adobe.com/content/help/en/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
   </body>
   </html>
   ```

+++

1. Obtenga un editor de texto en el que pueda realizar cambios en la página HTML de ejemplo. (Si no tiene uno, le recomendamos que pruebe [Brackets](https://brackets.io/)).
1. Marcar el sitio de [Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!NOTE]
>
>Puede que le resulte más fácil completar este tutorial con el sitio Luma abierto en Chrome, mientras lee este tutorial y completa los pasos de la interfaz de recopilación de datos en un explorador diferente.

¡Empecemos!

[Siguiente: &quot;Crear una propiedad de etiqueta&quot; >](create-a-property.md)
