---
title: Añadir el código incrustado
description: Obtenga información sobre cómo obtener los códigos incrustados de la propiedad de etiquetas e implementarlos en el sitio web. Esta lección forma parte del tutorial Implementación del Experience Cloud en sitios web .
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 50%

---

# Añadir el código incrustado

En esta lección, debe implementar el código incrustado asincrónico del entorno de desarrollo de su propiedad de etiqueta. A lo largo del camino, aprenderá sobre dos conceptos principales de etiquetas: Entornos y Códigos incrustados.

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al usar este contenido:
>
> * El platform launch (lado del cliente) ya está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El servidor de platform launch está ahora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Las configuraciones de Edge ahora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**


## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Obtener el código incrustado de la propiedad de etiqueta
* Comprender la diferencia entre los entornos de desarrollo, de ensayo y de producción.
* Añadir un código incrustado de etiqueta a un documento HTML
* Explicar la ubicación óptima del código incrustado de la etiqueta en relación con otro código en la variable `<head>` de un documento html

## Copiar el código de incrustación

El código incrustado es un `<script>` que se coloca en las páginas web para cargar y ejecutar la lógica que se genera en las etiquetas. Si carga la biblioteca de forma asíncrona, el explorador continúa cargando la página, recuperando la biblioteca de etiquetas y ejecutándola en paralelo. En este caso, solo hay un código de incrustación, que usted pone en `<head>`. (Cuando las etiquetas se implementan sincrónicamente, hay dos códigos incrustados, uno que se coloca en la variable `<head>` y otro que usted puso ante el `</body>`).

En la pantalla Información general de la propiedad, haga clic en **[!UICONTROL Entornos]** en la navegación izquierda para ir a la página entornos . Tenga en cuenta que los entornos de desarrollo, de estado y de producción ya se han creado.

![Haga clic en Entornos en la barra de navegación superior](images/launch-environments.png)

Los entornos de desarrollo, de ensayo y de producción se corresponden con los entornos habituales en el proceso de programación y desarrollo de códigos. Los desarrolladores escriben un código primero en un entorno de desarrollo (Development). Cuando han completado su trabajo, lo envían a un entorno de ensayo (Staging) para que el control de calidad y otros equipos lo revisen. Una vez estén conformes los equipos de control de calidad y otros equipos, el código se publica en el entorno de producción (Production), que es el entorno del público que los visitantes ven cuando llegan al sitio web.

Las etiquetas permiten entornos de desarrollo adicionales, lo que resulta útil en organizaciones grandes en las que varios desarrolladores trabajan en distintos proyectos al mismo tiempo.

Son los únicos entornos necesarios para completar el tutorial. Los entornos permiten tener diferentes versiones de trabajo de las bibliotecas de etiquetas alojadas en distintas direcciones URL, por lo que puede añadir nuevas funciones y ponerlas a disposición de los usuarios adecuados (por ejemplo, desarrolladores, ingenieros de control de calidad, el público, etc.) en el momento adecuado.

Ahora vamos a copiar el código de incrustación:

1. En la fila **[!UICONTROL Development]**, haga clic en el ![icono Instalar](images/launch-installIcon.png) para abrir el modal.

1. Tenga en cuenta que las etiquetas se asignarán de forma predeterminada a los códigos incrustados asincrónicos.

1. Haga clic en el ![icono Copiar](images/launch-copyIcon.png) para copiar el código de incrustación en el portapapeles.

1. Haga clic en **[!UICONTROL Cerrar]** para cerrar el modal.

   ![Icono Instalar](images/launch-copyInstallCode.png)

## Implemente el código de incrustación en el `<head>` de la página HTML de ejemplo.

El código de incrustación debe implementarse en el elemento `<head>` de todas las páginas HTML que comparten la propiedad. Puede tener uno o varios archivos de plantilla que controlan el `<head>` globalmente en todo el sitio, lo que lo convierte en un proceso directo para agregar etiquetas.

Si aún no lo ha hecho, descargue [la página HTML de ejemplo](https://www.enablementadobe.com/multi/web/basic-sample.html) (haga clic con el botón derecho en este vínculo, haga clic en &quot;Guardar vínculo como&quot;) y ábralo en un editor de código. [Brackets](https://brackets.io/) es un editor de código abierto gratuito si lo necesita.

Reemplace el código de incrustación existente en la línea 34 (o alrededor) con el que lleva en el portapapeles y guarde la página. A continuación, abra la página en un navegador web. Si está cargando la página mediante el protocolo `file://`, debe agregar “https:” al principio de la URL del código de incrustación en el editor de código). Las líneas 33-36 de la página de ejemplo pueden tener un aspecto similar al siguiente:

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

Abra las herramientas para desarrolladores del navegador web y vaya a la pestaña Red (Network). En este punto, debería ver un error 404 para la URL del entorno de etiquetas:
![Error 404](images/samplepage-404.png)

Se espera el error 404 porque aún no ha creado una biblioteca en este entorno de etiquetas. Lo hará en la siguiente lección. Si ve un mensaje “failed” en lugar de un error 404, probablemente olvidó agregar el protocolo `https://` en el código de incrustación. De nuevo, solo debe especificar el protocolo `https://` si está cargando la página de muestra mediante el protocolo `file://`. Realice un cambio y vuelva a cargar la página hasta que aparezca el error 404.

## Prácticas recomendadas en la implementación de etiquetas

Dediquemos un momento a revisar algunas de las prácticas recomendadas de implementación de etiquetas que se muestran en la página de muestra:

* **Capa de datos**:

   * Recomendamos *encarecidamente* la creación de una capa de datos en su sitio que contenga todos los atributos necesarios para rellenar variables en Analytics, Target y otras soluciones de marketing. Esta página de muestra solo contiene una capa de datos muy sencilla, pero una capa de datos real puede contener muchos más detalles sobre la página, el visitante, los detalles del carro de compras, etc. Para obtener más información sobre las capas de datos, consulte [Customer Experience Digital Data Layer 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf).

   * Defina la capa de datos antes del código incrustado de la etiqueta para maximizar lo que puede hacer con las soluciones de Experience Cloud.

* **Bibliotecas de ayuda de JavaScript**: Si ya tiene una biblioteca como JQuery implementada en la variable `<head>` de sus páginas, cárguelo antes de las etiquetas para aprovechar su sintaxis en las etiquetas y Target

* **Doctype HTML 5**: se requiere el doctype HTML 5 para Target.

* **Preconnect y dns-prefetch**: utilice preconnect y dns-prefetch para mejorar el tiempo de carga de la página. Consulte también: [https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **ocultación previa de fragmento para implementaciones asíncronas de Target**: Aprenderá más sobre esto en la lección de Target, pero cuando Target se implemente mediante códigos incrustados de etiquetas asincrónicas, debe codificar mediante hardcode un fragmento de ocultamiento previo en las páginas antes de los códigos incrustados de etiquetas para administrar el parpadeo del contenido

Este es un resumen de cómo se ven estas prácticas recomendadas en el orden sugerido. Tenga en cuenta que hay algunos marcadores de posición para detalles específicos de la cuenta:

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
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
    <!--prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of tags</p>
</body>
</html>
```

Ahora sabe cómo agregar el código incrustado de la etiqueta a su sitio.

[Siguiente: &quot;Añadir un elemento de datos, una regla y una biblioteca&quot; >](add-data-elements-rules.md)
