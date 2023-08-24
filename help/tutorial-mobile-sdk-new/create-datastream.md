---
title: Configurar una secuencia de datos
description: Obtenga información sobre cómo crear una secuencia de datos en Experience Platform.
feature: Mobile SDK,Datastreams
hide: true
source-git-commit: 7de7c7e13ea6d02f1193620e0cc35299e07d59e5
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 9%

---


# Crear un flujo de datos

Obtenga información sobre cómo crear una secuencia de datos en Experience Platform.

Un conjunto de datos es una configuración del lado del servidor en Platform Edge Network. La secuencia de datos garantiza que los datos entrantes en la red perimetral de Platform se enruten correctamente a las aplicaciones y servicios de Adobe Experience Cloud. Para obtener más información, consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es) o esto [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=es).

## Requisitos previos

Para crear una secuencia de datos, su organización debe estar aprovisionada para esta función en la interfaz de recopilación de datos (anteriormente, [!UICONTROL Launch]) y debe tener permisos de usuario para [!UICONTROL Experience Platform] > [!UICONTROL Recopilación de datos] > **[!UICONTROL Administrar flujos de datos]** y **[!UICONTROL Ver flujos de datos]**.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Saber cuándo utilizar un conjunto de datos.
* Crear un flujo de datos.
* Configurar una secuencia de datos.

## Crear un flujo de datos

Las secuencias de datos se pueden crear en la variable [!UICONTROL Recopilación de datos] interfaz con el [!UICONTROL Datastream] herramienta de configuración. Para crear una secuencia de datos:

1. Asegúrese de que está en el entorno limitado del Experience Platform correcto, ya que las secuencias de datos se definen en un nivel de entorno limitado.
1. Seleccionar **[!UICONTROL Datastreams]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Nueva secuencia de datos]**.

   ![inicio de flujos de datos](assets/datastream-new.png)

1. Proporcione un **[!UICONTROL Nombre]**, por ejemplo `Luma Mobile App` y una **[!UICONTROL Descripción]**, por ejemplo `Datastream for Luma Mobile App`.
1. Seleccione el esquema que ha creado en la lección anterior en la **Esquema del evento** una lista.
1. Seleccione **[!UICONTROL Guardar]**.

   ![nuevos flujos de datos](assets/datastream-name.png)


## Agregar servicios

A continuación, conecte los servicios de Experience Cloud a la secuencia de datos. Cuando el SDK de Platform Mobile envía datos a Edge Network, el conjunto de datos envía los datos a estos servicios:

1. Seleccione **[!UICONTROL Agregar servicio]**.

1. Añadir **[!UICONTROL Adobe Analytics]** desde el [!UICONTROL Servicio] lista,

1. Escriba el nombre del grupo de informes que desee usar en **[!UICONTROL ID del grupo de informes]**.

1. Habilitar el servicio cambiando **[!UICONTROL Habilitado]** en.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir Adobe Analytics como servicio de flujo de datos](assets/datastream-service-aa.png)

También es posible que desee habilitar el servicio Adobe Experience Platform.

>[!IMPORTANT]
>
>Solo puede habilitar el servicio Adobe Experience Platform cuando haya creado un conjunto de datos de evento. Si aún no ha creado un conjunto de datos de evento, siga las instrucciones [aquí](platform.md).

1. Clic ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir servicio]** para agregar otro servicio.

1. Seleccione **[!UICONTROL Adobe Experience Platform]** en la lista [!UICONTROL Servicio].

1. Habilitar el servicio cambiando **[!UICONTROL Habilitado]** en.

1. Seleccione el **[!UICONTROL Conjunto de datos de evento]** que ha creado como parte de [Crear un conjunto de datos](platform.md#create-a-dataset) instrucción, por ejemplo **Conjunto de datos de evento de aplicación móvil Luma**

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir el servicio Adobe Experience Platform as a Datastream](assets/datastream-service-aep.png)
1. La configuración final debería tener un aspecto similar al siguiente.

   ![configuración de secuencia de datos](assets/datastream-settings.png)


>[!NOTE]
>
>Al habilitar cada uno de los servicios que utiliza su organización, se garantiza que los datos recopilados en la aplicación móvil se puedan utilizar en todas partes. Para obtener más información sobre la configuración del flujo de datos, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Al implementar el SDK de Platform Mobile en su propia aplicación, debe crear tres flujos de datos para asignarlos a sus tres entornos de etiquetas (desarrollo, fase y producción). Si utiliza el SDK de Platform Mobile con aplicaciones basadas en Platform, como Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, debe asegurarse de crear dichos flujos de datos en los entornos limitados de Platform correspondientes.

>[!SUCCESS]
>
>Ahora tiene una secuencia de datos para utilizar durante el resto del tutorial.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Configuración de etiquetas](configure-tags.md)**
