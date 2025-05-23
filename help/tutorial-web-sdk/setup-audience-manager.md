---
title: Configuración del Audience Manager con el SDK web de Platform
description: Obtenga información sobre cómo configurar Adobe Audience Manager mediante el SDK web de Platform y validar la implementación mediante un destino de cookie. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
solution: Data Collection, Audience Manager
jira: KT-15409
exl-id: 45db48e9-73cf-4a9c-88f4-b5872a8224d3
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 4%

---

# Configuración del Audience Manager con el SDK web de Platform

Obtenga información sobre cómo configurar Adobe Audience Manager con el SDK web de Adobe Experience Platform y validar la implementación mediante un destino de cookie.

[Adobe Audience Manager](https://experienceleague.adobe.com/es/docs/audience-manager) es la solución de Adobe Experience Cloud que proporciona todo lo necesario para recopilar información comercial relevante acerca de los visitantes del sitio, crear segmentos comercializables y ofrecer contenido y publicidad segmentada a la audiencia adecuada.

![Diagrama de SDK web y Adobe Audience Manager](assets/dc-websdk-aam.png)

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Configuración de una secuencia de datos para habilitar Audience Manager
* Habilitar un destino de cookie en Audience Manager
* Valide la implementación del Audience Manager confirmando la calificación de la audiencia con el Adobe Experience Platform Debugger.

## Requisitos previos

Para completar esta lección, primero debe:

* Complete las lecciones anteriores de las secciones Configuración inicial y Configuración de etiquetas de este tutorial.
* Tener acceso a Adobe Audience Manager y los permisos adecuados para crear, leer y escribir características, segmentos y destinos. Para obtener más información, consulte [Control de acceso basado en roles de Audience Manager](https://experienceleague.adobe.com/es/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).

## Configuración de la secuencia de datos

La implementación del Audience Manager mediante el SDK web de Platform difiere de la implementación mediante [reenvío del lado del servidor (SSF)](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/server-side-forwarding/ssf). El reenvío del lado del servidor pasa los datos de solicitud de Adobe Analytics al Audience Manager. Una implementación del SDK web de Platform pasa los datos XDM enviados al Edge Network de Platform al Audience Manager. El Audience Manager está habilitado en el conjunto de datos:

1. Ir a la interfaz de [recopilación de datos](https://experience.adobe.com/#/data-collection){target="blank"}
1. En el panel de navegación izquierdo, seleccione **[!UICONTROL Datastreams]**
1. Seleccione la secuencia de datos `Luma Web SDK: Development Environment` creada anteriormente

   ![Seleccione la secuencia de datos del SDK web de Luma](assets/datastream-luma-web-sdk-development.png)

1. Seleccionar **[!UICONTROL Agregar servicio]**
   ![Agregar un servicio al conjunto de datos](assets/aam-datastream-addService.png)
1. Seleccione **[!UICONTROL Adobe Audience Manager]** como **[!UICONTROL servicio]**
1. Confirme que **[!UICONTROL Destinos de cookies habilitados]** y **[!UICONTROL Destinos de URL habilitados]** están seleccionados
1. Seleccionar **[!UICONTROL Guardar]**
   ![Confirme la configuración del flujo de datos del Audience Manager y guarde](assets/aam-datastream-save.png)

## Crear una fuente de datos

A continuación, cree un [Source de datos](https://experienceleague.adobe.com/es/docs/audience-manager/user-guide/features/data-sources/datasources-list-and-settings), una herramienta fundamental para organizar los datos dentro de Audience Manager:

1. Ir a la interfaz de [Audience Manager](https://experience.adobe.com/#/audience-manager/)
1. Seleccione **[!UICONTROL Datos de audiencia]** en la barra de navegación superior
1. Seleccione **[!UICONTROL Fuentes de datos]** en el menú desplegable
1. Seleccione el botón **[!UICONTROL Agregar nuevo]** de la parte superior de la página Fuentes de datos

   ![Fuentes de datos del Audience Manager de Adobe Experience Platform](assets/data-sources-list.jpg)

1. Asigne un nombre descriptivo a Data Source. Para la configuración inicial, puede asignar un nombre a este(a) `Platform Web SDK tutorial`.
1. Establecer **[!UICONTROL tipo de identificador]** en **[!UICONTROL cookie]**
1. En la sección **[!UICONTROL Controles de exportación de datos]**, seleccione **[!UICONTROL Sin restricciones]**

   ![Configuración de Adobe Experience Platform Audience Manager Data Source](assets/data-source-details.png)

1. **[!UICONTROL Guardar]** el Source de datos


## Crear un rasgo

Una vez guardado el Data Source, configure un [rasgo](https://experienceleague.adobe.com/es/docs/audience-manager/user-guide/features/traits/traits-overview). Los rasgos son una combinación de una o más señales en Audience Manager. Cree una característica para los visitantes de la página principal.

>[!NOTE]
>
>Todos los datos XDM se envían al Audience Manager si están habilitados en el conjunto de datos, pero los datos pueden tardar 24 horas hasta que estén disponibles en el informe Señales no utilizadas. Cree rasgos explícitos para los datos XDM que desee utilizar inmediatamente en Audience Manager, tal como se describe en este ejercicio.

1. Seleccionar **[!UICONTROL datos de audiencia]** > **[!UICONTROL rasgos]**
1. Seleccionar **[!UICONTROL Agregar nuevo]** > **[!UICONTROL rasgo basado en reglas]**

   ![Rasgo basado en reglas de Audience Manager de Adobe Experience Platform](assets/rule-based-trait.jpg)

1. Asigne un nombre descriptivo y una descripción a su característica, `Luma homepage view`
1. Seleccione el **[!UICONTROL Source de datos]** que creó en la sección anterior.
1. **[!UICONTROL Seleccione una carpeta]** en la que guardar el rasgo en el panel de la derecha. Es posible que desee crear una carpeta **seleccionando el icono +** junto a una carpeta principal existente. Puede asignar un nombre a esta nueva carpeta `Platform Web SDK tutorial`.
1. Expanda el símbolo de intercalación **[!UICONTROL Expresión de característica]** y seleccione **[!UICONTROL Generador de expresiones]**. Debe proporcionar un par de valor clave que signifique una visita a la página principal.
1. Abra la [página principal de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) (asignada a su propiedad de etiquetas) y el **Adobe Experience Platform Debugger**, y actualice la página.
1. Consulte las Solicitudes de red y los detalles del evento para el SDK web de Platform para encontrar la clave y el valor del nombre para la página principal.
   ![Datos XDM del Audience Manager de Adobe Experience Platform](assets/xdm-keyvalue.jpg)
1. Vuelva al Generador de expresiones en la interfaz de usuario del Audience Manager e introduzca la clave como **`web.webPageDetails.name`** y el valor de **`content:luma:us:en`**. Este paso garantiza que active una característica cada vez que cargue la página principal.
1. **[!UICONTROL Guardar]** el rasgo.


## Crear un segmento

Los siguientes pasos son crear un **segmento** y asignar el rasgo recién definido a este segmento.

1. Seleccione **[!UICONTROL Datos de audiencia]** en la barra de navegación superior y seleccione **[!UICONTROL Segmentos]**
1. Seleccione **[!UICONTROL Agregar nuevo]** en la parte superior izquierda de la página para abrir el generador de segmentos
1. Asigne a su segmento un nombre descriptivo y una descripción, como `Platform Web SDK - Homepage visitors`
1. **[!UICONTROL Seleccione una carpeta]** en la que se guardará el segmento en el panel de la derecha. Es posible que desee crear una carpeta **seleccionando el icono +** junto a una carpeta principal existente. Puede asignar un nombre a esta nueva carpeta `Platform Web SDK tutorial`.
1. Añada un código de integración, que en este caso es un conjunto aleatorio de números.
1. En la sección **[!UICONTROL Data Source]**, seleccione **[!UICONTROL Audience Manager]** y el origen de datos que creó anteriormente
1. Expanda la sección **[!UICONTROL Características]** y busque la característica que ha creado
1. Seleccione **[!UICONTROL Agregar característica]**.
1. Seleccione **[!UICONTROL Guardar]** en la parte inferior de la página

   ![Audience Manager de Adobe Experience Platform Agregar característica](assets/add-trait-segment.jpg)

   ![Audience Manager de Adobe Experience Platform Agregar característica](assets/saved-segment.jpg)

## Crear un destino

A continuación, cree un **destino basado en cookies** con **Generador de destinos**. El Generador de destinos permite crear y administrar destinos de servidor a servidor, direcciones URL y cookies.

1. Abra el Generador de destinos seleccionando **[!UICONTROL Destinos]** en el menú **Datos de audiencia** de la barra de navegación superior
1. Seleccionar **[!UICONTROL Crear destino]**
1. Escriba un nombre y una descripción, `Platform Web SDK tutorial`
1. Como **[!UICONTROL categoría]**, seleccione **[!UICONTROL Personalizado]**
1. Como **[!UICONTROL tipo]**, seleccione **[!UICONTROL cookie]**

   ![Audience Manager de Adobe Experience Platform Agregar característica](assets/destination-settings.jpg)

1. Abra la sección **[!UICONTROL Configuración]** para escribir los detalles sobre el destino de la cookie
1. Asigne un nombre descriptivo a su cookie, `platform_web_sdk_tutorial`
1. Como **[!UICONTROL dominio de cookies]**, agregue el dominio del sitio donde planea la integración para la entrada del tutorial en el dominio de Luma `luma.enablementadobe.com`
1. Como opción **[!UICONTROL Publish data to]**, seleccione **[!UICONTROL Solo los dominios seleccionados]**
1. Seleccione su dominio si aún no lo ha agregado
1. Como **[!UICONTROL Formato de datos]**, seleccione **[!UICONTROL Clave única]** y asígnele una clave a la cookie. Para este tutorial, use `segment` como valor clave.
1. Finalmente, seleccione **[!UICONTROL Guardar]** para guardar los detalles de configuración de destino.

   ![Sección de configuración de destino de Audience Manager](assets/aam-destination-config-dw.png)

<!--
   ![Adobe Experience Platform Audience Manager Add Trait](assets/aam-destination-config.jpg)


   ![Adobe Experience Platform Audience Manager Add Trait](assets/cookie-destination-config.jpg)
-->

1. En la sección **[!UICONTROL Asignaciones de segmentos]**, usa la función **[!UICONTROL Buscar y agregar segmentos]** para buscar tu `Platform Web SDK - Homepage visitors` creado anteriormente y selecciona **[!UICONTROL Agregar]**.


1. Una vez que agregue el segmento, se abrirá una ventana emergente en la que debe proporcionar un valor esperado para la cookie. Para este ejercicio, introduzca el valor &quot;visitante&quot;.

1. Seleccionar **[!UICONTROL Guardar]**

1. Seleccionar **[!UICONTROL Listo]**
   ![Audience Manager de Adobe Experience Platform Agregar característica](assets/luma-cookie-segment-dw.png)

El periodo de asignación de segmentos requiere que se activen unas horas. Una vez finalizado, puede actualizar la interfaz del Audience Manager y ver que la lista **Segmentos asignados** se ha actualizado.

## Validación del segmento

Unas horas después de la creación inicial del segmento, puede validar que funciona correctamente.

En primer lugar, confirme que puede optar al segmento

1. Abra la [página principal del sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con él asignado a su propiedad de etiquetas para cumplir los requisitos para el segmento recién creado.
1. Abra la ficha **herramientas para desarrolladores** > **Red** de su explorador
1. Filtrar a la solicitud del SDK web de Platform usando `interact` como filtro de texto
1. Seleccione una llamada y abra la ficha **Vista previa** para ver los detalles de la respuesta
1. Expanda **payload** para ver los detalles de la cookie esperados, tal como se configuró anteriormente en el Audience Manager. En este ejemplo, verá el nombre de cookie esperado `platform_web_sdk_tutorial`.

   ![Audience Manager de Adobe Experience Platform Agregar característica](assets/segment-validate-response.jpg)

1. Abra la ficha **Aplicación** y abra **Cookies** desde el menú **Almacenamiento**.
1. Seleccione el dominio **`https://luma.enablementadobe.com`** y confirme que la cookie se ha escrito correctamente en la lista

   ![Audience Manager de Adobe Experience Platform Agregar característica](assets/validate-cookie.jpg)


Por último, debe abrir el segmento en la interfaz de Audience Manager y asegurarse de que **Poblaciones de segmentos** haya incrementado:

![Audience Manager de Adobe Experience Platform Agregar característica](assets/segment-population.jpg)


Ahora que ha completado esta lección, debe poder ver cómo el SDK web de Platform pasa datos a Audience Manager y puede establecer una cookie de origen específica de un segmento con un destino de cookie.

[Siguiente: ](setup-target.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=es)
