---
title: Configuración del Audience Manager con el SDK web de Platform
description: Obtenga información sobre cómo configurar Adobe Audience Manager mediante el SDK web de Platform y validar la implementación mediante un destino de cookie. Esta lección forma parte del tutorial Implementar Adobe Experience Cloud con SDK web .
solution: Data Collection, Audience Manager
exl-id: 45db48e9-73cf-4a9c-88f4-b5872a8224d3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---

# Configuración del Audience Manager con el SDK web de Platform

Obtenga información sobre cómo configurar Adobe Audience Manager mediante el SDK web de Platform y validar la implementación mediante un destino de cookie.

[Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html) es la solución de Adobe Experience Cloud que proporciona todo lo necesario para recopilar información relevante desde el punto de vista comercial sobre los visitantes del sitio, crear segmentos comercializables y ofrecer contenido y publicidad segmentada a la audiencia adecuada.


## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Configuración de un conjunto de datos para habilitar el Audience Manager
* Habilitar un destino de cookie en el Audience Manager
* Valide la implementación del Audience Manager confirmando la calificación de la audiencia con Adobe Experience Platform Debugger

## Requisitos previos

Para completar esta lección, primero debe:

* Complete las lecciones anteriores en las secciones Configuración inicial y Configuración de etiquetas de este tutorial.
* Tener acceso a Adobe Audience Manager y los permisos adecuados para crear, leer y escribir características, segmentos y destinos. Para obtener más información, consulte [Control de acceso basado en roles del Audience Manager](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

## Configuración del conjunto de datos

La implementación del Audience Manager que utiliza el SDK web de Platform difiere de la implementación que utiliza [reenvío del lado del servidor (SSF)](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=es). El reenvío del lado del servidor pasa los datos de solicitud de Adobe Analytics al Audience Manager. Una implementación del SDK web de Platform pasa los datos XDM enviados a Platform Edge Network al Audience Manager. El Audience Manager está habilitado en el conjunto de datos:

1. Vaya a [Recopilación de datos](https://experience.adobe.com/#/data-collection)Interfaz de {target=&quot;blank&quot;}
1. En el panel de navegación izquierdo, seleccione **[!UICONTROL Datastreams]**
1. Seleccione el `Luma Web SDK` datastream

   ![Seleccione el conjunto de datos del SDK web de Luma](assets/datastream-luma-web-sdk.png)

1. Select **[!UICONTROL Añadir servicio]**

   ![Añadir un servicio al conjunto de datos](assets/aam-datastream-addService.png)
1. Select **[!UICONTROL Adobe Audience Manager]** como el **[!UICONTROL Servicio]**
1. Confirme que **[!UICONTROL Destinos de cookies habilitados]** y **[!UICONTROL Destinos de URL habilitados]** están seleccionados
1. Seleccione **[!UICONTROL Guardar]**

   ![Confirme la configuración del conjunto de datos del Audience Manager y guarde](assets/aam-datastream-save.png)

## Crear una fuente de datos

A continuación, cree un [Fuente de datos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-sources/datasources-list-and-settings.html?lang=en), una herramienta fundamental para organizar los datos dentro de Audience Manager:

1. Vaya a la [Audience Manager](https://experience.adobe.com/#/audience-manager/) interfaz
1. Select **[!UICONTROL Datos de audiencia]** desde la barra de navegación superior
1. Seleccione el **[!UICONTROL Fuentes de datos]** en el menú desplegable
1. Seleccione el **[!UICONTROL Agregar nuevo]** en la parte superior de la página Fuentes de datos

   ![Fuentes de datos del Audience Manager de Adobe Experience Platform](assets/data-sources-list.jpg)

1. Asigne un nombre y una descripción descriptivos a la fuente de datos. Para la configuración inicial, puede asignarle un nombre`Platform Web SDK tutorial`.
1. Establezca **[!UICONTROL Tipo de ID]** a **[!UICONTROL Cookie]**
1. En el **[!UICONTROL Controles de exportación de datos]** , seleccione **[!UICONTROL Sin restricciones]**

   ![Configuración de la fuente de datos del Audience Manager de Adobe Experience Platform](assets/data-source-details.png)

1. **[!UICONTROL Guardar]** la fuente de datos


## Crear un rasgo

Una vez guardada la fuente de datos, configure una [rasgo](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/traits-overview.html?lang=en). Los rasgos son una combinación de una o más señales en Audience Manager. Cree un rasgo para los visitantes de la página principal.

>[!NOTE]
>
>Todos los datos XDM se envían al Audience Manager si están habilitados en el conjunto de datos, pero los datos pueden tardar 24 horas hasta que estén disponibles en el informe Señales no utilizadas . Cree rasgos explícitos para los datos XDM que desea utilizar inmediatamente en el Audience Manager, tal como se describe en este ejercicio.

1. Select **[!UICONTROL Datos de audiencia]** >  **[!UICONTROL Rasgos]**
1. Select **[!UICONTROL Agregar nuevo]** >  **[!UICONTROL Basado en reglas]** rasgo

   ![Característica basada en reglas del Audience Manager de Adobe Experience Platform](assets/rule-based-trait.jpg)

1. Asigne un nombre y una descripción descriptivos a su rasgo. `Luma homepage view`
1. Seleccione el **[!UICONTROL Fuente de datos]** creado en la sección anterior.
1. **[!UICONTROL Seleccionar una carpeta]** en el que guardar el rasgo en el panel de la derecha. Puede que desee crear una carpeta de **selección del icono +** junto a una carpeta principal existente. Puede asignar un nombre a esta nueva carpeta `Platform Web SDK tutorial`.
1. Expanda el **[!UICONTROL Expresión de rasgo]** acento circunflejo y seleccione **[!UICONTROL Generador de expresiones]** Debe proporcionar un par clave-valor que signifique una visita a la página principal.
1. Abra el [Página de inicio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) (asignado a la propiedad tag ) y la variable **Platform Web SDK Debugger** y actualice la página.
1. Consulte las Solicitudes de red y los detalles de evento del SDK web de Platform para encontrar la clave y el valor de nombre de la página principal.
   ![Datos XDM del Audience Manager de Adobe Experience Platform](assets/xdm-keyvalue.jpg)
1. Vuelva al Generador de expresiones en la interfaz de usuario del Audience Manager e introduzca la clave como **`web.webPageDetails.name`** y el valor de **`content:luma:us:en`**. Este paso garantiza que se active un rasgo cada vez que se carga la página principal.
1. **[!UICONTROL Guardar]** el rasgo.


## Creación de segmentos

El siguiente paso es crear un **segmento** y asigne su característica recién definida a este segmento.

1. Select **[!UICONTROL Datos de audiencia]** en la barra de navegación superior y seleccione **[!UICONTROL Segmentos]**
1. Select **[!UICONTROL Agregar nuevo]** en la parte superior izquierda de la página para abrir el generador de segmentos
1. Asigne un nombre y una descripción descriptivos al segmento, como `Platform Web SDK - Homepage visitors`
1. **[!UICONTROL Seleccionar una carpeta]** donde se guardará el segmento en el panel de la derecha. Puede que desee crear una carpeta de **selección del icono +** junto a una carpeta principal existente. Puede asignar un nombre a esta nueva carpeta `Platform Web SDK tutorial`.
1. Agregue un código de integración, que en este caso es un conjunto aleatorio de números. 1. **[!UICONTROL Fuente de datos]** , seleccione **[!UICONTROL Audience Manager]** y la fuente de datos creada anteriormente
1. Expanda el **[!UICONTROL Rasgos]** y busque el rasgo que ha creado
1. Select **[!UICONTROL Agregar característica]**.
1. Select **[!UICONTROL Guardar]** en la parte inferior de la página

   ![Adobe Experience Platform Audience Manager Agregar característica](assets/add-trait-segment.jpg)

   ![Adobe Experience Platform Audience Manager Agregar característica](assets/saved-segment.jpg)

## Crear un destino

A continuación, cree un **Destino basado en cookies** usando la variable **Generador de destino**. El Generador de destinos permite crear y administrar destinos de cookies, URL y servidor a servidor.

1. Abra el Generador de destinos seleccionando **[!UICONTROL Destinos]** dentro de la variable **Datos de audiencia** en la barra de navegación superior
1. Select **[!UICONTROL Crear destino]**
1. Introduzca un nombre y una descripción. `Platform Web SDK tutorial`
1. Como **[!UICONTROL Categoría]**, seleccione **[!UICONTROL Personalizado]**
1. Como **[!UICONTROL Tipo]**, seleccione **[!UICONTROL Cookie]**

   ![Adobe Experience Platform Audience Manager Agregar característica](assets/destination-settings.jpg)

1. Abra el **[!UICONTROL Configuración]** para introducir los detalles sobre el destino de la cookie
1. Asigne un nombre descriptivo a la cookie. `platform_web_sdk_tutorial`
1. Como **[!UICONTROL Dominio de la cookie]**, añada el dominio del sitio donde está planeando la integración, para el tutorial que introduce el dominio de Luma, `luma.enablementadobe.com`
1. Como **[!UICONTROL Publicar datos en]** , seleccione **[!UICONTROL Solo los dominios seleccionados]**
1. Seleccione su dominio si aún no se ha añadido
1. Como **[!UICONTROL Formato de datos]**, seleccione **[!UICONTROL Clave única]** y proporcione una clave a su cookie. Para este tutorial, utilice `segment` como valor clave.
1. Finalmente, seleccione **[!UICONTROL Guardar]** para guardar los detalles de configuración de destino.

   ![Sección Configuración del destino del Audience Manager](assets/aam-destination-config-dw.png)

<!--
   ![Adobe Experience Platform Audience Manager Add Trait](assets/aam-destination-config.jpg)


   ![Adobe Experience Platform Audience Manager Add Trait](assets/cookie-destination-config.jpg)
-->

1. En el **[!UICONTROL Asignaciones de segmentos]** utilice la **[!UICONTROL Buscar y agregar segmentos]** para buscar la `Platform Web SDK - Homepage visitors` y seleccione **[!UICONTROL Agregar]**.


1. Una vez agregado el segmento, se abre una ventana emergente en la que debe proporcionar el valor esperado para la cookie. Para este ejercicio, introduzca el valor &quot;visitante&quot;.

1. Seleccione **[!UICONTROL Guardar]**

1. Select **[!UICONTROL Listo]**

   ![Adobe Experience Platform Audience Manager Agregar característica](assets/luma-cookie-segment-dw.png)

El periodo de asignación de segmentos requiere unas pocas horas para activarse. Una vez completada, puede actualizar la interfaz de Audience Manager y comprobar que la variable **Segmentos asignados** lista actualizada.

## Validar el segmento

Unas horas después de la creación inicial del segmento, puede validar que funcione correctamente.

En primer lugar, confirme que puede optar al segmento

1. Abra el [Página de inicio del sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con él asignado a la propiedad tag para clasificarse para el segmento recién creado.
1. Abra el **herramientas para desarrolladores**  > **Red** ficha
1. Filtre a la solicitud del SDK web de Platform utilizando `interact` como filtro de texto
1. Seleccione una llamada y abra el **Vista previa** para ver los detalles de la respuesta
1. Expanda el **carga útil** para ver los detalles de la cookie esperados, como se configuró anteriormente en Audience Manager. En este ejemplo, verá el nombre de cookie esperado `platform_web_sdk_tutorial`.

   ![Adobe Experience Platform Audience Manager Agregar característica](assets/segment-validate-response.jpg)

1. Abra el **Aplicación** y abra **Cookies** de la variable **Almacenamiento** para abrir el Navegador.
1. Seleccione el **`https://luma.enablementadobe.com`** y confirme que la cookie se ha escrito correctamente en la lista

   ![Adobe Experience Platform Audience Manager Agregar característica](assets/validate-cookie.jpg)


Finalmente, debe abrir el segmento en la interfaz de Audience Manager y asegurarse de que la variable **Poblaciones de segmentos** ha aumentado:

![Adobe Experience Platform Audience Manager Agregar característica](assets/segment-population.jpg)


Después de completar esta lección, debe poder ver cómo el SDK web de Platform pasa los datos al Audience Manager y puede establecer una cookie de origen específica del segmento con un destino de cookie.

[Siguiente: ](setup-target.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK web de Adobe Experience Platform. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
