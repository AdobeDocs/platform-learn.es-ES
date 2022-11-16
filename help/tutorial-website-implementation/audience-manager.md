---
title: Añadir Adobe Audience Manager
description: Obtenga información sobre cómo implementar Adobe Audience Manager en el sitio web mediante el reenvío del lado del servidor y las etiquetas. Esta lección forma parte del tutorial Implementación del Experience Cloud en sitios web .
solution: Data Collection, Audience Manager
exl-id: ddc77dc5-bfb5-4737-b6b6-47d37c9f0528
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 84%

---

# Añadir Adobe Audience Manager

Esta lección le guiará a través de los pasos para habilitar Adobe Audience Manager mediante el reenvío del lado del servidor.

[Adobe Audience Manager](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html) (AAM) proporciona servicios líderes en el sector para la administración de datos de audiencias en línea, lo cual proporciona a los anunciantes y editores digitales las herramientas necesarias para controlar y aprovechar sus recursos de datos para ayudar a impulsar la eficacia de las ventas.

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al usar este contenido:
>
> * El platform launch (lado del cliente) ya está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El servidor de platform launch está ahora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Las configuraciones de Edge ahora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**


## Objetivos de aprendizaje

Al final de esta lección, debe poder:

1. Describir las dos maneras principales de implementar Audience Manager en un sitio web.
1. Añadir Audience Manager mediante el reenvío del lado del servidor de la señalización de Analytics.
1. Validar la implementación de Audience Manager.

## Requisitos previos

Para completar esta lección, debe:

1. Haber completado las lecciones de [Configuración de etiquetas](create-a-property.md), [Añadir Adobe Analytics](analytics.md)y [Añadir el servicio de identidad](id-service.md).

1. Acceso de administrador a Adobe Analytics para habilitar el reenvío del lado del servidor para el grupo de informes que se utiliza en este tutorial. También puede pedir a un administrador existente de su organización que lo haga siguiendo las instrucciones que se indican a continuación.

1. Su “subdominio de Audience Manager” (también conocido como “nombre de socio”, “ID de socio” o “subdominio de socio”). Si ya ha implementado Audience Manager en su sitio web, la manera más sencilla de obtener esto es ir al sitio web real y abrir Debugger. El subdominio está disponible en la pestaña Resumen, en la sección de Audience Manager:

   ![Puede utilizar Debugger para buscar el subdominio de Audience Manager en el sitio Web real](images/aam-debugger-partner.png)

Si aún no ha implementado Audience Manager, siga estas instrucciones para [obtener el subdominio de Audience Manager](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/web-implementation/how-to-identify-your-partner-id-or-subdomain.html).

## Opciones de implementación

Existen dos maneras de implementar Audience Manager en un sitio web:

* **Reenvío del lado del servidor (SSF):** para los clientes con Adobe Analytics, esta es la manera más fácil y recomendada de realizar implementaciones. Adobe Analytics envía datos a AAM en el backend de Adobe, lo que permite realizar una solicitud menos en la página. Esto también permite las funciones de integración clave y cumple con las prácticas recomendadas para la implementación y el despliegue de código de Audience Manager.

* **DIL del lado del cliente:** este enfoque es para clientes que no tienen Adobe Analytics. El código DIL (código de biblioteca de integración de datos, el código de configuración JavaScript de AAM) envía datos directamente desde la página web a Audience Manager.

Como ya ha implementado Adobe Analytics en este tutorial, ahora se implementa Audience Manager mediante el reenvío del lado del servidor. Para obtener una descripción completa y una lista de requisitos para el reenvío del lado del servidor, consulte [la documentación](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=es) para poder familiarizarse con su funcionamiento, sus necesidades y su validación.

## Activación del reenvío del lado del servidor

Existen dos pasos principales para realizar una implementación de SSF:

1. Activar un “conmutador” en la Admin Console de Analytics para reenviar datos de Analytics a Audience Manager *por grupo de informes*.
1. Colocación del código en su lugar, que se realiza mediante etiquetas. Para que esto funcione correctamente, debe tener instalada la extensión del servicio de ID de Adobe Experience Platform, así como la extensión de Analytics (de hecho, *no necesitará* la extensión de AAM, que se explica a continuación).

### Habilitar el reenvío del lado del servidor en la Admin Console de Analytics

Se requiere configurar la Admin Console de Adobe Analytics para empezar a reenviar datos de Adobe Analytics a Adobe Audience Manager. Como puede tardar hasta cuatro horas en empezar a reenviar los datos, primero debe realizar este paso.

#### Para activar el SSF en la Admin Console de Analytics

1. Inicie sesión en Analytics mediante la interfaz de usuario de Experience Cloud. Si no tiene acceso de administrador a Analytics, debe hablar con el administrador de Experience Cloud o de Analytics para que le asigne el acceso o completar estos pasos en su lugar.

   ![Iniciar sesión en Adobe Analytics](images/aam-logIntoAnalytics.png)

1. En el panel de navegación superior de Analytics, seleccione **[!UICONTROL Administración > Grupos de informes]** y, en la lista, seleccione (selección múltiple) los grupos de informes que desee reenviar a Audience Manager.

   ![Haga clic en la Admin Console](images/aam-analyticsAdminConsoleReportSuites.png)

1. En la pantalla Grupos de informes y con los grupos de informes seleccionados, seleccione **[!UICONTROL Editar configuración > General > Reenvío del lado del servidor]**.

   ![Seleccione el menú SSF](images/aam-selectSSFmenu.png)

   >[!WARNING]
   >
   >Como se ha indicado anteriormente, debe tener privilegios de administrador para ver este elemento de menú.

1. Una vez en la página Reenvío del lado del servidor, lea la información y marque la casilla de verificación **[!UICONTROL Habilitar reenvío del lado del servidor]** para los grupos de informes.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Configuración completa de SSF](images/aam-enableSSFcomplete.png)

>[!NOTE]
>
>Ya que es necesario habilitar el reenvío del lado del servidor para cada grupo de informes, asegúrese de repetir estos pasos para los grupos de informes reales cuando implemente el reenvío en su grupo de informes del sitio.
>
>Además, si la opción SSF está atenuada, debe asignar los grupos de informes a su organización de Experience Cloud para habilitar la opción. Esto se explica en [la documentación](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html?lang=es).

Una vez completado este paso, y si tiene habilitado el servicio de ID de Adobe Experience Platform, los datos se reenvían de Analytics a AAM. Sin embargo, para completar el proceso de modo que la respuesta regrese correctamente de AAM a la página (y también a Analytics mediante la función de Audience Analytics), también debe completar el siguiente paso en las etiquetas . No se preocupe, es muy fácil.

### Habilitar el reenvío del lado del servidor en las etiquetas

Este es el segundo de dos pasos para habilitar el SSF. Ya ha cambiado el conmutador en el Admin Console de Analytics y ahora solo necesita añadir el código, lo que le servirá si simplemente marca la casilla de verificación correcta.

>[!NOTE]
>
>Para implementar el reenvío de datos de Analytics del lado del servidor en AAM, en realidad editaremos/configuraremos la extensión de Analytics en etiquetas. **not** la extensión de AAM. La extensión de AAM se utiliza exclusivamente para implementaciones DIL del lado del cliente, para aquellos que no tienen Adobe Analytics. Por lo tanto, los siguientes pasos son correctos cuando le envían a la extensión de Analytics para configurarla.

#### Para habilitar el reenvío del lado del servidor en las etiquetas

1. Vaya a **[!UICONTROL Extensiones > Instaladas]** y haga clic para configurar la extensión de Analytics.

   ![Configurar la extensión de Analytics.](images/aam-configAnalyticsExtension.png)

1. Expanda la sección `Adobe Audience Manager`.

1. Marque la casilla para **[!UICONTROL compartir automáticamente datos de Analytics con Audience Manager]**. Así se añade el “módulo” (código) de Audience Manager a la implementación de `AppMeasurement.js` de Analytics.

1. Añada su “subdominio de Audience Manager” (también conocido como “nombre de socio”, “ID de socio” o “subdominio de socio”). Siga estas instrucciones para [obtener el subdominio de Audience Manager](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/web-implementation/how-to-identify-your-partner-id-or-subdomain.html).

1. Haga clic en **[!UICONTROL Guardar en biblioteca y crear]**.

   ![Configurar SSF](images/aam-configLaunchSSF.png)

Ya se ha implementado el código de reenvío del lado del servidor.

### Validación del reenvío del lado del servidor

La manera principal de comprobar que el reenvío del lado del servidor funciona es consultar la respuesta a cualquiera de sus visitas de Adobe Analytics. Enseguida nos ponemos con este tema. Mientras tanto, revisemos un par de otras cosas que nos pueden ayudar a asegurarnos de que funciona tal como queremos.

#### Verificar que el código se esté cargando correctamente

El código que etiqueta las instalaciones para gestionar el reenvío, y especialmente la respuesta de AAM a la página, se denomina &quot;módulo&quot; al Audience Manager. Podemos usar Experience Cloud Debugger para garantizar que se haya cargado.

1. Abra el sitio de Luma.
1. Haga clic en el icono de Debugger en el navegador para abrir Experience Cloud Debugger.
1. En la pestaña Resumen, desplácese hacia abajo hasta la sección Analytics.
1. Compruebe que **AudienceManagement** se encuentre dentro de la sección de los módulos.

   ![Validación del módulo de AAM en Debugger](images/aam-verifyAAMmodule.png)

#### Compruebe el ID de socio en Debugger

A continuación, también podemos verificar que Debugger está recopilando el “ID del socio” correcto (subdominio de socio AKA, etc.) del código.

1. Mientras sigue en Debugger y en la pestaña Resumen, desplácese hacia abajo hasta la sección Audience Manager.
1. Compruebe su ID o subdominio de socio en “Socio” (Partner).

   ![Validar el ID de socio en Debugger](images/aam-verifyPartnerID.png)

>[!WARNING]
>
>Es posible que observe que la sección Audience Manager de Debugger hace referencia a “DIL”, que es la “Biblioteca de integración de datos” y que, generalmente, hace referencia a una implementación del lado del cliente, a diferencia del enfoque del lado del servidor que hemos implementado aquí. La verdad es que el “módulo” de AAM (utilizado en este enfoque de SSF) utiliza mucho del mismo código que la biblioteca DIL del lado del cliente, por lo que Debugger lo identifica como tal. Si ha seguido los pasos de este tutorial y los demás elementos de esta sección de validación son correctos, puede estar seguro de que el reenvío del lado del servidor funciona.

#### Comprobar la solicitud y respuesta de Analytics

Aquí está el problema. Si no utiliza el reenvío de datos del lado del servidor de Analytics a Audience Manager, no hay respuesta a la señalización de Analytics (más allá de un píxel 2x2). Sin embargo, si lo utiliza, puede comprobar ciertos elementos en la solicitud y la respuesta de Analytics que le permiten saber que funciona correctamente. Lamentablemente, en este momento Experience Cloud Debugger no permite mostrar la respuesta a las señalizaciones. Por lo tanto, debe utilizar otro depurador o detector de paquetes, como Charles Proxy o las herramientas para desarrolladores del navegador.

1. Abra las herramientas para desarrolladores en el navegador y vaya a la pestaña Red (Network).
1. En el campo de filtro, escriba `b/ss` que limitará lo que ve para las solicitudes de Adobe Analytics.
1. Actualice la página para ver la solicitud de Analytics.

   ![Abrir las herramientas para desarrolladores](images/aam-openTheJSConsole.png)

1. En la señalización (solicitud) de Analytics, busque un parámetro “callback”. Se establecerá en algo así: `s_c_il[1].doPostbacks`.

   ![Solicitud AA: parámetro de devolución de llamada](images/aam-callbackParam.png)

1. Tendrá una respuesta a la señalización de Analytics. Contendrá referencias a doPostbacks, como se llama en la solicitud, y lo más importante, debe tener un objeto “material”. Aquí es donde los ID de segmento de AAM se devuelven al navegador. Si dispone del objeto “material”, el reenvío del lado del servidor funciona.

   ![Respuesta de AA: objeto material](images/aam-stuffObjectInResponse.png)

>[!WARNING]
>
> Cuidado con el falso “SUCCESS”: si hay una respuesta, y todo parece estar funcionando, **asegúrese** de que dispone de ese objeto “material”. Si no lo tiene, puede que se muestre un mensaje en la respuesta que dice &quot;status&quot;:&quot;SUCCESS&quot;. Aunque parezca absurdo, es prueba de que **NO** funciona correctamente. Si lo ve, significa que ha completado el segundo paso (el código de las etiquetas ), pero que el reenvío en el Admin Console de Analytics (primer paso de esta sección) aún no ha finalizado. En este caso, debe comprobar que ha activado SSF en la Admin Console de Analytics. Si lo ha hecho y aún no han pasado cuatro horas, tenga paciencia.

![Respuesta de AA: falso éxito](images/aam-responseFalseSuccess.png)

[Siguiente: “Integraciones de Experience Cloud” >](integrations.md)
