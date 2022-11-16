---
title: Ingesta de datos de flujo continuo
seo-title: Ingest streaming data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Ingesta de datos de flujo continuo
description: En esta lección, se transmitirán datos a Experience Platform mediante el SDK web.
role: Data Engineer
feature: Data Ingestion
kt: 4348
thumbnail: 4348-ingest-streaming-data.jpg
exl-id: 09c24673-af8b-40ab-b894-b4d76ea5b112
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '3344'
ht-degree: 2%

---

# Ingesta de datos de flujo continuo

<!--1hr-->

En esta lección, se transmitirán datos mediante el SDK web de Adobe Experience Platform.

Hay dos tareas principales que debemos completar en la interfaz de recopilación de datos:

* Se debe implementar el SDK web en el sitio web de Luma para enviar datos sobre la actividad de los visitantes desde el sitio web a la red de Adobe Edge. Realizaremos una implementación sencilla mediante etiquetas (anteriormente, Launch)

* Debemos configurar un conjunto de datos, que indique a la red de Edge dónde reenviar los datos. Lo configuraremos para enviar los datos a nuestra `Luma Web Events` conjunto de datos en nuestro entorno limitado de Platform.

**Ingenieros de datos** tendrá que introducir datos de flujo continuo fuera de este tutorial. Al implementar los SDK web o móviles de Adobe Experience Platform, normalmente un desarrollador web o móvil participa en la creación de la capa de datos y la configuración de la propiedad de etiquetas.

Antes de comenzar los ejercicios, vea estos dos vídeos cortos para obtener más información sobre la ingesta de datos de flujo continuo y el SDK web:
>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

>[!NOTE]
>
>Aunque este tutorial se centra en la transmisión de la ingesta de sitios web con el SDK web, también puede transmitir datos mediante la función [SDK de Adobe Mobile](https://aep-sdks.gitbook.io/), [Apache Kafka Connect](https://github.com/adobe/experience-platform-streaming-connect)y otros mecanismos.

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) , configure todos los controles de acceso necesarios para completar esta lección.

<!--
* Permission items **[!UICONTROL Launch]** > **[!UICONTROL Property Rights]** > **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]**, and **[!UICONTROL Publish]**
* Permission item **[!UICONTROL Launch]** > **[!UICONTROL Company Rights]** > **[!UICONTROL Manage Properties]**
* User-role access to the `Luma Tutorial Launch` product profile
* Admin-role access to the `Luma Tutorial Launch` product profile
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Profiles]** > **[!UICONTROL View Profiles]**, **[!UICONTROL Manage Profiles]** and **[!UICONTROL Export Audience Segment]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

<!--## Create a streaming source

1. Log into the [Experience Platform  user interface](https://experience.adobe.com/platform/)
1. Go to **[!UICONTROL Sources]** in the left navigation
1. Filter the list by selecting **[!UICONTROL Streaming]**
1. In the **[!UICONTROL HTTP API]** section, select the **[!UICONTROL Configure]** button
    ![Configure an HTTP API streaming source](assets/websdk-source-confiigureHTTPAPI.png)
1. On the **[!UICONTROL Authentication]** step, enter `Luma Web Events Source` as the **[!UICONTROL Account name]** and select the **[!UICONTROL Connect to source]** button (we don't need to enable authentication since the data will be originating from website visitors)
    ![Configure an HTTP API streaming source](assets/websdk-source-connectSource.png)
1. Once connected, select the **[!UICONTROL Next]** button to proceed to the next step in the workflow
1. On the **[!UICONTROL Select data]** step, choose **[!UICONTROL Existing Dataset]**, select your `Luma Web Events Dataset`, and then select the **[!UICONTROL Next]** button
    ![Select your dataset](assets/websdk-source-selectDataset.png)
1. On the **[!UICONTROL Dataflow detail]** step, select the **[!UICONTROL Next]** button:
    ![Select Next](assets/websdk-source-dataflowName.png)
    <!--What is a good practice for naming the data flow vs the source-->
<!--
1. On the **[!UICONTROL Review]** step, review your source details and select the **[!UICONTROL Finish]** button:
    ![Select Finish](assets/websdk-source-review.png)
-->

## Configuración del conjunto de datos

Primero configuraremos el conjunto de datos. Un conjunto de datos indica a la red de Adobe Edge dónde enviar los datos después de recibirlos de la llamada del SDK web. Por ejemplo, ¿desea enviar los datos a Experience Platform, Adobe Analytics o Adobe Target? Los conjuntos de datos se administran en la interfaz de usuario de recopilación de datos (anteriormente Launch) y son esenciales para la recopilación de datos con el SDK web.

Para crear [!UICONTROL datastream]:

1. Inicie sesión en el [Interfaz de usuario de recopilación de datos del Experience Platform](https://experience.adobe.com/launch/)

   <!--when will the edge config go live?-->

1. Select **[!UICONTROL Datastreams]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Nuevo conjunto de datos]** en la esquina superior derecha

   ![Seleccionar conjuntos de datos en el panel de navegación izquierdo](assets/websdk-edgeConfig-clickNav.png)


1. Para la variable **[!UICONTROL Nombre reconocible]**, introduzca `Luma Platform Tutorial` (añada su nombre al final, si varias personas de su empresa están tomando este tutorial)
1. Seleccione el botón **[!UICONTROL Guardar]**

   ![Asigne un nombre al datastram y guárdelo](assets/websdk-edgeConfig-name.png)

En la siguiente pantalla, se especifica dónde se desea enviar los datos. Para enviar datos al Experience Platform:

1. Alternar en **[!UICONTROL Adobe Experience Platform]** exponer campos adicionales
1. Para **[!UICONTROL Sandbox]**, seleccione `Luma Tutorial`
1. Para **[!UICONTROL Conjunto de datos del evento]**, seleccione `Luma Web Events Dataset`
1. Si utiliza otras aplicaciones de Adobe, no dude en explorar las otras secciones para ver qué información se requiere en la Configuración de Edge de estas otras soluciones. Recuerde que el SDK web se desarrolló no solo para transmitir datos a Experience Platform, sino también para reemplazar todas las bibliotecas JavaScript anteriores utilizadas por otras aplicaciones de Adobe. La configuración de Edge se utiliza para especificar los detalles de la cuenta de cada aplicación a la que desea enviar los datos.
1. Seleccione **[!UICONTROL Guardar]**

   ![Configurar el conjunto de datos y guardar](assets/websdk-edgeConfig-addEnvironment.png)

Una vez guardada la configuración de Edge, la pantalla resultante mostrará tres entornos creados para desarrollo, ensayo y producción. Se pueden agregar entornos de desarrollo adicionales:
![Cada configuración de Edge puede tener varios entornos](assets/websdk-edgeConfig-environments.png)
Los tres entornos contienen los detalles de Platform que acaba de introducir. Sin embargo, estos detalles se pueden configurar de forma diferente para cada entorno. Por ejemplo, puede hacer que cada entorno envíe datos a un entorno limitado de Platform diferente. En este tutorial, no realizaremos ninguna personalización adicional en nuestro conjunto de datos.

## Instalación de la extensión del SDK web

### Agregar una propiedad

En primer lugar, se debe crear una propiedad de etiqueta (anteriormente, una propiedad de etiqueta). Una propiedad es un contenedor de todas las funciones, reglas y demás funciones de JavaScript necesarias para recopilar detalles de una página web y enviarlos a varias ubicaciones.

Para crear una propiedad:

1. Vaya a **[!UICONTROL Propiedades]** en la navegación izquierda
1. Seleccione el botón **[!UICONTROL Nueva propiedad]**
   ![Añadir una nueva propiedad](assets/websdk-property-addNewProperty.png)
1. Como **[!UICONTROL Nombre]**, introduzca `Luma Platform Tutorial` (añada su nombre al final, si varias personas de su empresa están tomando este tutorial)
1. Como **[!UICONTROL Dominios]**, introduzca `enablementadobe.com` (explicado más tarde)
1. Seleccione **[!UICONTROL Guardar]**

   ![Detalles de propiedad](assets/websdk-property-propertyDetails.png)

<!--
After saving the property, you might see an error message like the one below. If so, this is because you don't actually have access to the property you just created. To fix this, we need to go to the Admin Console to give yourself access:
    ![Error after saving the profile](assets/websdk-property-errorCreating.png)

To give yourself access to the property:

1. In a separate browser tab, log into the [Admin Console](https://adminconsole.adobe.com/)
1. Go to **[!UICONTROL Products]** from the top navigation
1. Select **[!UICONTROL Adobe Experience Platform Launch]** on the left navigation
1. Go to your `Luma Tutorial Launch` product profile
1. Go to the **[!UICONTROL Permissions]** tab
1. On the **[!UICONTROL Properties]** row, select **[!UICONTROL Edit]**
    ![Edit the Property Permissions](assets/websdk-adminconsole-editPermissions.png)
1. Select the "+" icon to move your `Luma Platform Tutorial` property to the right-hand side and select the **[!UICONTROL Save]** button to update the permissions
   
    ![Add the new property](assets/websdk-adminconsole-addProperty.png)

Now switch back to your browser tab with the Data Collection interface still open. Reload the page and the `Luma Platform Tutorial` property should display in the list. Select to open the property:

![Luma Platform Tutorial should appear](assets/websdk-property-showsInList.png)
-->

## Añadir la extensión del SDK web

Ahora que tiene una propiedad, puede añadir el SDK web con una extensión . Una extensión es un paquete de código que amplía la interfaz y funcionalidad de recopilación de datos. Para añadir la extensión:

1. Abra la propiedad tag
1. Vaya a **[!UICONTROL Extensiones]** en la navegación izquierda
1. Vaya a la **[!UICONTROL Catálogo]** ficha
1. Hay muchas extensiones disponibles para etiquetas. Filtrar el catálogo con el término `Web SDK`
1. En el **[!UICONTROL SDK web de Adobe Experience Platform]** , seleccione **[!UICONTROL Instalar]** botón
   ![Instalación de la extensión del SDK web de Adobe Experience Platform](assets/websdk-property-addExtension.png)
1. Hay varias configuraciones disponibles para la extensión del SDK web, pero solo hay dos que vamos a configurar para este tutorial. Actualice el **[!UICONTROL Dominio de Edge]** a `data.enablementadobe.com`. Esta configuración le permite establecer cookies de origen con su implementación del SDK web, lo que resulta útil. Más adelante en esta lección, asignará un sitio web a la `enablementadobe.com` a la propiedad tag. El CNAME de la variable `enablementadobe.com` El dominio ya se ha configurado para que `data.enablementadobe.com` se reenviará a los servidores de Adobe. Al implementar el SDK web en su propio sitio web, deberá crear un CNAME para sus propios fines de recopilación de datos, por ejemplo, `data.YOUR_DOMAIN.com`
1. En el **[!UICONTROL Datastream]** menú desplegable, seleccione su `Luma Platform Tutorial` datastream.
1. Siéntase libre de ver las otras opciones de configuración (pero no las cambie). y, a continuación, seleccione **[!UICONTROL Guardar]**
   <!--is edge domain required for first party? when will it break?-->
   <!--any other fields that should be highlighted-->
   ![](assets/websdk-property-configureExtension.png)



## Creación de una regla para enviar datos

Ahora crearemos una regla para enviar datos a Platform. Una regla es una combinación de eventos, condiciones y acciones que indican a las etiquetas que hagan algo. Para crear una regla:

1. Vaya a **[!UICONTROL Reglas]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Crear nueva regla]** botón
   ![Crear una regla](assets/websdk-property-createRule.png)
1. Asigne un nombre a la regla `All Pages - Library Loaded`.
1. En **[!UICONTROL Eventos]**, seleccione **[!UICONTROL Agregar]** botón
   ![Asigne un nombre a la regla y añada un evento](assets/websdk-property-nameRule.png)
1. Utilice la variable **[!UICONTROL Principal]** **[!UICONTROL Extensión]** y seleccione **[!UICONTROL Biblioteca cargada (Principio de página)]** como el **[!UICONTROL Tipo de evento]**. Esta configuración significa que la regla se activa cada vez que la biblioteca de Launch se carga en una página.
1. Select **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal
   ![Añadir el evento Library Loaded](assets/websdk-property-addEvent.png)
1. Leave **[!UICONTROL Condiciones]** vacío, ya que queremos que esta regla se active en todas las páginas, según el nombre que le dimos
1. En **[!UICONTROL Acciones]**, seleccione **[!UICONTROL Agregar]** botón
1. Utilice la variable **[!UICONTROL SDK web de Adobe Experience Platform]** **[!UICONTROL Extensión]** y seleccione **[!UICONTROL Enviar evento]** como el **[!UICONTROL Tipo de acción]**
1. A la derecha, seleccione **[!UICONTROL web.webpagedetails.pageViews]** de la variable **[!UICONTROL Tipo]** lista desplegable. Este es uno de los campos XDM en nuestra `Luma Web Events Schema`
1. Select **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal
   ![Añadir la acción Enviar evento](assets/websdk-property-addAction.png)
1. Select **[!UICONTROL Guardar]** para guardar la regla\
   ![Guarde la regla](assets/websdk-property-saveRule.png)

## Publicar la regla en una biblioteca

A continuación, publicaremos la regla en nuestro entorno de desarrollo para que podamos verificar que funciona.

<!--
There are a few quick steps we must take in the **[!UICONTROL Publishing]** section of Launch.


### Create a host

Launch libraries can be hosted on Adobe's Content Delivery Network (CDN) or on your own servers. In this tutorial, we will use Adobe's CDN since it is faster to set up:

1. Go to **[!UICONTROL Hosts]** in the left navigation
1. Select the **[!UICONTROL Create New Host]** button
    ![Create a new host](assets/websdk-property-createHost.png)   
1. For the **[!UICONTROL Name]**, enter `Adobe CDN`
1. For the **[!UICONTROL Type]**, select **[!UICONTROL Managed by Adobe]**
1. Select the **[!UICONTROL Save]** button to complete the setup of the host
    ![Configure the host](assets/websdk-property-hostDetails.png)   

### Create an environment

Environments allow you to have different versions of a library in different publishing environments to accommodate your publishing workflow. For example, the fully tested version of your library can be published to a Production environment, while new changes are being created in a Development environment. You can also use different hosts for each environment. To create an environment:

1. Go to **[!UICONTROL Environments]** in the left navigation
1. Select the **[!UICONTROL Create New Environment]** button
    ![Create a new environment](assets/websdk-property-createEnvironment.png) 
1. Under **[!UICONTROL Development]** select **[!UICONTROL Select]**   
    ![Select the environment type](assets/websdk-property-selectEnvironment.png) 
1. For the **[!UICONTROL Name]**, enter `Development`
1. For the **[!UICONTROL Select Host]** dropdown, select `Adobe CDN`
1. Select the **[!UICONTROL Save]** button to complete the setup of the environment
    ![Configure the environment](assets/websdk-property-configureEnv.png)
1. You will see a modal with URL and other implementation details of this library. These are critical for a real Launch implementation, but we don't need to worry about them for this tutorial. Select the **[!UICONTROL Close]** button to exit the modal.

### Create and publish the library

Now let's bundle the contents of our property&mdash;currently an extension and a rule&mdash;into a library. 
-->

Para crear una biblioteca:

1. Vaya a **[!UICONTROL Flujo de publicación]** en la navegación izquierda
1. Select **[!UICONTROL Agregar biblioteca]**
   ![Seleccionar Agregar biblioteca](assets/websdk-property-pubAddNewLib.png)
1. Para la variable **[!UICONTROL Nombre]**, introduzca `Luma Platform Tutorial`
1. Para la variable **[!UICONTROL Entorno]**, seleccione `Development`
1. Seleccione el **[!UICONTROL Agregar todos los recursos modificados]** botón. (Además del [!UICONTROL SDK web de Adobe Experience Platform] y `All Pages - Library Loaded` regla, también verá la variable [!UICONTROL Principal] extensión añadida que contiene el JavaScript base requerido por todas las propiedades web de Launch).
1. Seleccione el **[!UICONTROL Guardar y generar para desarrollo]** botón
   ![Crear y crear la biblioteca](assets/websdk-property-buildLibrary.png)

La biblioteca puede tardar unos minutos en crearse y, cuando se completa, muestra un punto verde a la izquierda del nombre de la biblioteca:
![Compilación completada](assets/websdk-property-buildComplete.png)

Como puede ver en la sección [!UICONTROL Flujo de publicación] , hay mucho más en el proceso de publicación que está fuera del alcance de este tutorial. Vamos a usar una sola biblioteca en nuestro entorno de desarrollo.

## Validación de los datos en la solicitud

### Añadir Adobe Experience Platform Debugger

Experience Platform Debugger es una extensión disponible para exploradores Chrome y Firefox que le ayuda a ver la tecnología de Adobe implementada en sus páginas web. Descargue la versión de su navegador preferido:

* [Extensión de Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/)
* [Extensión de Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si nunca antes ha utilizado Debugger (y este es diferente del anterior Adobe Experience Cloud Debugger), es posible que desee ver este vídeo de descripción general de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

### Abra el sitio web de Luma.

Para este tutorial, utilizamos una versión alojada públicamente del sitio web de demostración de Luma. Vamos a abrirlo y marcarlo como marcador:

1. En una nueva pestaña del explorador, abra la [Sitio web de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).
1. Marque la página para usarla durante el resto del tutorial.

Este sitio web alojado es la razón por la que usamos `enablementadobe.com` en el [!UICONTROL Dominios] campo de la configuración inicial de la propiedad tag y por qué se ha utilizado `data.enablementadobe.com` como nuestro dominio de origen en la variable [!UICONTROL SDK web de Adobe Experience Platform] extensión. ¡Mira, tenía un plan!

![Página de inicio de Luma](assets/websdk-luma-homepage.png)

### Usar el depurador de Experience Platform para asignar a la propiedad de etiqueta

Experience Platform Debugger tiene una funcionalidad excelente que le permite reemplazar una propiedad de etiqueta existente por otra diferente. Esto resulta útil para la validación y nos permite omitir muchos pasos de implementación en este tutorial.

1. Asegúrese de que el sitio de Luma está abierto y seleccione el icono de extensión de Experience Platform Debugger .
1. Debugger se abrirá y mostrará algunos detalles de la implementación codificada, que no está relacionada con este tutorial (puede que tenga que volver a cargar el sitio de Luma después de abrir Debugger)
1. Confirme que Debugger es &quot;**[!UICONTROL Conectado a Luma]**&quot; como se muestra a continuación y seleccione &quot;**[!UICONTROL bloquear]**&quot; para bloquear Debugger en el sitio de Luma.
1. Seleccione el **[!UICONTROL Iniciar sesión]** en la parte superior derecha para autenticarse.
1. Ahora vaya a **[!UICONTROL Launch]** en la navegación izquierda
1. Seleccione la pestaña Configuración
1. A la derecha de donde se muestra la variable **[!UICONTROL Códigos incrustados de página]**, abra el **[!UICONTROL Acciones]** y seleccione **[!UICONTROL Reemplazar]**

   ![Seleccione Acciones > Reemplazar](assets/websdk-debugger-replaceLibrary.png)
1. Como está autenticado, Debugger va a incorporar las propiedades y los entornos de Launch disponibles. Seleccione su `Luma Platform Tutorial` property
1. Seleccione su `Development` entorno
1. Seleccione el **[!UICONTROL Aplicar]** botón
   ![Seleccionar la propiedad de etiqueta alternativa](assets/websdk-debugger-selectProperty.png)
1. El sitio web de Luma ahora se vuelve a cargar _con la propiedad tag_. ¡Ayuda, me han hackeado! Estoy bromeando.
   ![se ha reemplazado la propiedad tag](assets/websdk-debugger-propertyReplaced.png)
1. Vaya a **[!UICONTROL Resumen]** en el panel de navegación izquierdo, para ver los detalles de [!UICONTROL Launch] property
   ![Ficha Resumen](assets/websdk-debugger-summary.png)
1. Ahora vaya a **[!UICONTROL SDK web de AEP]** en el panel de navegación izquierdo para ver la **[!UICONTROL Solicitudes de red]**
1. Abra el **[!UICONTROL events]** row

   ![Solicitud de SDK web de Adobe Experience Platform](assets/websdk-debugger-platformNetwork.png)
1. Observe cómo podemos ver el `web.webpagedetails.pageView` tipo de evento especificado en nuestra [!UICONTROL Enviar evento] y otras variables listas para usar que cumplan con el `AEP Web SDK ExperienceEvent Mixin` format
   ![Detalles del evento](assets/websdk-debugger-eventDetails.png)
1. Estos tipos de detalles de solicitud también están visibles en las herramientas para desarrolladores web del explorador **Red** pestaña . Ábrala y vuelva a cargar la página. Filtre las llamadas con `interact` para localizar la llamada, selecciónela y, a continuación, busque en la **Encabezados** , **Carga útil de solicitud** .
   ![Ficha Red](assets/websdk-debugger-networkTab.png)
1. Vaya a la **Respuesta** y observe cómo se incluye el valor ECID en la respuesta. Copie este valor tal como lo usará para validar la información de perfil en el siguiente ejercicio.
   ![Ficha Red](assets/websdk-debugger-networkTab-response.png)



## Validar los datos en el Experience Platform

Puede validar que los datos están aterrizando en Platform observando los lotes de datos que llegan al `Luma Web Events Dataset`. (Lo sé, se llama ingesta de transmisión de datos, pero ahora digo que llega en lotes! Se transmite en tiempo real a Perfil, de modo que se puede utilizar para la segmentación y activación en tiempo real, pero se envía en lotes cada 15 minutos al lago de datos).

Para validar los datos:

1. En la interfaz de usuario de Platform, vaya a **[!UICONTROL Conjuntos de datos]** en la navegación izquierda
1. Abra el `Luma Web Events Dataset` y confirme que ha llegado un lote. Recuerde que se envían cada 15 minutos, por lo que es posible que tenga que esperar a que se muestre el lote.
1. Seleccione el **[!UICONTROL Vista previa del conjunto de datos]** botón
   ![Abrir el conjunto de datos](assets/websdk-platform-dataset.png)
1. En el modal de vista previa, observe cómo puede seleccionar diferentes campos del esquema a la izquierda para obtener una vista previa de esos puntos de datos específicos:
   ![Vista previa de los campos](assets/websdk-platform-datasetPreview.png)

También puede confirmar que se muestra el nuevo perfil:

1. En la interfaz de usuario de Platform, vaya a **[!UICONTROL Perfiles]** en la navegación izquierda
1. Seleccione el **[!UICONTROL ECID]** y busque su valor ECID (cópielo desde la respuesta). El perfil tendrá su propio ID, independiente del ECID.
1. Seleccione el **[!UICONTROL ID de perfil]** para abrir el perfil
   ![Buscar y abrir el perfil](assets/websdk-platform-openProfile.png)
1. Seleccione el **[!UICONTROL Eventos]** para ver las páginas que ha visto
   ![Eventos de perfil](assets/websdk-platform-profileEvents.png)
   <!--![](assets/websdk-platform-confirmProfile.png)-->

## Añadir datos personalizados al evento

### Crear un elemento de datos para el nombre de página

1. En la interfaz de etiquetas de recopilación de datos, en la esquina superior derecha de su `Luma Platform Tutorial` , abra la **[!UICONTROL Seleccionar una biblioteca de trabajo]** lista desplegable y seleccione su `Luma Platform Tutorial` biblioteca. Esta configuración facilita la publicación de actualizaciones adicionales en nuestra biblioteca.
1. Ahora vaya a **[!UICONTROL Elementos de datos]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Crear nuevo elemento de datos]** botón

   ![Crear un nuevo elemento de datos](assets/websdk-property-createNewDataElement.png)
1. Como **[!UICONTROL Nombre]**, introduzca `Page Name`
1. Como **[!UICONTROL Tipo de elemento de datos]**, seleccione `JavaScript Variable`
1. Como **[!UICONTROL Nombre de variable de JavaScript]**, introduzca `digitalData.page.pageInfo.pageName`
1. Para ayudar a estandarizar el formato de los valores, marque las casillas de **[!UICONTROL Forzar valor de minúsculas]** y **[!UICONTROL Limpiar texto]**
1. Asegúrese de que `Luma Platform Tutorial` se selecciona como biblioteca de trabajo
1. Select **[!UICONTROL Guardar en biblioteca]**
   ![Crear un elemento de datos para el nombre de página](assets/websdk-property-dataElement-pageName.png)

### Asignación del nombre de página al elemento de datos Objeto XDM

Ahora asignaremos nuestro nombre de página al SDK web.

>[!IMPORTANT]
>
>Para completar esta tarea, debemos asegurarnos de que el usuario tenga acceso primero al simulador para pruebas Prod. Si todavía no tiene acceso al simulador para pruebas de producto desde un perfil de producto diferente, abra rápidamente su `Luma Tutorial Platform` perfil y añadir el elemento de permiso **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**. Después de hacerlo, realice una recarga SHIFT en la página Elementos de datos para borrar la caché
>![Agregar el simulador para pruebas de Prod](assets/websdk-property-permissionToLoadSchema.png)

En el **[!UICONTROL Elementos de datos]** página:

1. Crear un nuevo elemento de datos
1. Como **[!UICONTROL Nombre]**, introduzca `XDM Object`
1. Como **[!UICONTROL Extensión]**, seleccione `Adobe Experience Platform Web SDK`
1. Como **[!UICONTROL Tipo de elemento de datos]**, seleccione `XDM object`
1. Como **[!UICONTROL Sandbox]**, seleccione `Luma Tutorial` entorno limitado
1. Como **[!UICONTROL Esquema]**, seleccione `Luma Web Events Schema`
1. Seleccione el `web.webPageDetails.name` field
1. Como **[!UICONTROL Valor]**, seleccione el icono para abrir el modal de selección de elementos de datos y elija su `Page Name` elemento de datos
1. Select **[!UICONTROL Guardar en biblioteca]**

   ![Asignación del nombre de página al elemento de datos Objeto XDM](assets/websdk-property-dataElement-createXDMObject.png)

Este mismo proceso se utiliza para asignar datos personalizados adicionales en el sitio web a los campos XDM.

### Añadir los datos XDM a la acción Enviar evento

Ahora que tiene datos asignados a campos XDM, puede incluirlos en la acción Enviar evento :

1. Vaya a la **[!UICONTROL Reglas]** pantalla
1. Abra su `All Pages - Library Loaded` regla
1. Abra el `Adobe Experience Platform Web SDK - Send Event` acción
1. Como **[!UICONTROL Datos XDM]**, seleccione el icono para abrir el modal de selección de elementos de datos y elija su `XDM Object` elemento de datos
1. Seleccione el **[!UICONTROL Conservar cambios]** botón
   ![Añadir los datos XDM a la acción Enviar evento](assets/websdk-property-addXDMtoSendEvent.png)
1. Ahora, ya que `Luma Platform Tutorial` seleccionados como biblioteca de trabajo para los últimos ejercicios, los cambios recientes se han estado guardando directamente en la biblioteca. En lugar de tener que publicar nuestros cambios a través de la pantalla Flujo de publicación, solo puede abrir el menú desplegable del botón azul y seleccionar **[!UICONTROL Guardar en biblioteca y crear]**
   ![Guardar en biblioteca y crear](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

Esto comienza a crear una nueva biblioteca de etiquetas con los tres cambios que acaba de realizar.

### Validación de los datos XDM

Ahora debería poder volver a cargar la página de inicio de Luma, mientras está asignada a la propiedad tag usando Debugger como supo anteriormente, ¡y ver que el campo nombre de página se rellena en la solicitud!
![Validación de los datos XDM](assets/websdk-debugger-pageName.png)

También puede validar que los datos del nombre de página se recibieron en Platform, previsualizando el conjunto de datos y el perfil.

## Envío de identidades adicionales

La implementación del SDK web ahora envía eventos con el ID de Experience Cloud (ECID) como identificador principal. El SDK web genera automáticamente el ECID y es único para cada dispositivo y navegador. Un único cliente puede tener varios ECID en función del dispositivo y el navegador que utilice. Entonces, ¿cómo podemos obtener una vista unificada de este cliente y vincular su actividad en línea a nuestros datos de CRM, Lealtad y Compras sin conexión? Para ello, recopilamos identidades adicionales durante su sesión y vinculamos de forma determinista su perfil mediante la vinculación de identidades.

Si recuerda, he mencionado que utilizaríamos el ECID y el ID de CRM como identidades para nuestros datos web en la variable [Identidades de mapa](map-identities.md) lección. Así que recopilemos el ID de CRM con el SDK web.

### Añadir elemento de datos para el ID de CRM

Primero almacenamos el CRM Id en un elemento de datos:

1. En la interfaz de etiquetas, agregue un elemento de datos denominado `CRM Id`
1. Como **[!UICONTROL Tipo de elemento de datos]**, seleccione **[!UICONTROL Variable JavaScript]**
1. Como **[!UICONTROL Nombre de variable de JavaScript]**, introduzca `digitalData.user.0.profile.0.attributes.username`
1. Seleccione el **[!UICONTROL Guardar en biblioteca]** botón (`Luma Platform Tutorial` debe seguir siendo su biblioteca de trabajo)
   ![Añadir elemento de datos para el ID de CRM](assets/websdk-property-dataElement-crmId.png)

### Añadir el ID de CRM al elemento de datos del mapa de identidad

Ahora que hemos capturado el valor CRM Id, debemos asociarlo a un elemento de datos especial denominado [!UICONTROL Mapa de identidad] elemento de datos:

1. Agregue un elemento de datos con el nombre `Identities`
1. Como **[!UICONTROL Extensión]**, seleccione **[!UICONTROL SDK web de Adobe Experience Platform]**
1. Como **[!UICONTROL Tipo de elemento de datos]**, seleccione **[!UICONTROL Mapa de identidad]**
1. Como **[!UICONTROL Área de nombres]**, introduzca `Luma CRM Id`, que es el [!UICONTROL namespace] hemos creado en una lección anterior

   >[!WARNING]
   >
   >La extensión web SDK de Adobe Experience Platform versión 2.2 permite seleccionar Área de nombres de una lista desplegable previamente rellenada mediante los valores reales de la cuenta de Platform. Lamentablemente, esta función aún no es &quot;compatible con entornos limitados&quot; y, por lo tanto, la función `Luma CRM Id` puede que no aparezca en la lista desplegable. Esto puede impedir que complete este ejercicio. Publicaremos una solución una vez confirmada.

1. Como **[!UICONTROL ID]**, seleccione el icono para abrir el modal de selección de elementos de datos y elija su `CRM Id` elemento de datos
1. Como **[!UICONTROL Estado autenticado]**, seleccione **[!UICONTROL Autenticado]**
1. Leave **[!UICONTROL Principal]** _sin marcar_. Dado que el ID de CRM no está presente para la mayoría de los visitantes del sitio web de Luma, usted definitivamente _no desea anular el ECID como identificador principal_. Sería un caso de uso poco frecuente usar cualquier cosa que no sea ECID como identificador principal. Normalmente no menciono la configuración predeterminada en estas instrucciones, pero lo llamo para ayudarle a evitar dolores de cabeza más adelante en su propia implementación.
1. Seleccione el **[!UICONTROL Guardar en biblioteca]** botón (`Luma Platform Tutorial` debe seguir siendo su biblioteca de trabajo)
   ![Añadir el ID de CRM al elemento de datos del mapa de identidad](assets/websdk-property-dataElement-identityMap.png)

>[!NOTE]
>
>Puede pasar varios identificadores usando la variable [!UICONTROL Mapa de identidad] tipo de datos.

### Añadir el elemento de datos de mapa de identidad al objeto XDM

Hay un elemento de datos más que debemos actualizar: el elemento de datos Objeto XDM . Puede parecer raro tener que actualizar tres elementos de datos separados para pasar esta sola identidad, pero este proceso está diseñado para escalar para múltiples identidades. ¡No te preocupes, casi hemos terminado con esta lección!

1. Abra el elemento de datos Objeto XDM .
1. Abra el campo XDM de IdentityMap
1. Como **[!UICONTROL Elemento de datos]**, seleccione el icono para abrir el modal de selección de elementos de datos y elija su `Identities` elemento de datos
1. Ahora, ya que `Luma Platform Tutorial` seleccionados como biblioteca de trabajo para los últimos ejercicios, los cambios recientes se han estado guardando directamente en la biblioteca. En lugar de tener que publicar los cambios a través de la pantalla Flujo de publicación , puede abrir el menú desplegable del botón azul y seleccionar **[!UICONTROL Guardar en biblioteca y crear]**
   ![Agregue el elemento de datos IdentityMap al objeto XDM](assets/websdk-property-dataElement-addIdentitiesToXDMObject.png)


### Validar la identidad

Para validar que el SDK web está enviando el ID de CRM:

1. Abra el [Sitio web de Luma](https://luma.enablementadobe.com/content/luma/us/en.html)
1. Asignarlo a la propiedad de etiqueta mediante Debugger, según las instrucciones anteriores
1. Seleccione el **Inicio de sesión** vínculo en la parte superior derecha del sitio web de Luma
1. Iniciar sesión con las credenciales `test@adobe.com`/`test`
1. Una vez autenticado, inspeccione la llamada del SDK web del Experience Platform en Debugger (**[!UICONTROL SDK web de Adobe Experience Platform]** > **[!UICONTROL Solicitudes de red]** > **[!UICONTROL events]** de la solicitud más reciente) y debería ver la variable `lumaCrmId`:
   ![Validar la identidad en Debugger](assets/websdk-debugger-confirmIdentity.png)
1. Busque el perfil de usuario mediante el espacio de nombres y valor de ECID de nuevo. En el perfil, verá el CRM Id y también el Loyalty Id y los detalles del perfil como el nombre y el número de teléfono. Todas las identidades y los datos se han unido en un único perfil de cliente en tiempo real.
   ![Validación de la identidad en Platform](assets/websdk-platform-lumaCrmIdProfile.png)


## Recursos adicionales

* [Implementación de Adobe Experience Cloud con SDK web](/help/tutorial-web-sdk/overview.md)
* [Documentación de ingesta de flujos](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=es)
* [Referencia de la API de ingesta de flujos](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Streaming-Ingestion)

¡bueno trabajo! Se trataba de mucha información sobre el SDK web y Launch. Hay mucha más participación en una implementación completa, pero estos son los conceptos básicos para ayudarle a empezar y ver los resultados en Platform.

>[!NOTE]
>
>Ahora que ha terminado con la lección de ingesta de transmisión, puede eliminar la variable [!UICONTROL Prod] entorno limitado de su `Luma Tutorial Platform` perfil de producto


Ingenieros de datos, si lo desea, puede avanzar hacia el [lección ejecutar consultas](run-queries.md).

Arquitectos de datos, puede pasar a [combinar directivas](create-merge-policies.md)!
