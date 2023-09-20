---
title: Configuración de una secuencia de datos
description: Obtenga información sobre cómo crear una secuencia de datos en Experience Platform.
feature: Mobile SDK,Datastreams
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 10%

---


# Crear un flujo de datos

Obtenga información sobre cómo crear una secuencia de datos en Experience Platform.

Un conjunto de datos es una configuración del lado del servidor en Platform Edge Network. La secuencia de datos garantiza que los datos entrantes en la red perimetral de Platform se enruten correctamente a las aplicaciones y servicios de Adobe Experience Cloud. Para obtener más información, consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es) o esto [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=es).

![Arquitectura](assets/architecture.png)

## Requisitos previos

Para crear una secuencia de datos, su organización debe estar aprovisionada para esta función en la interfaz de recopilación de datos (anteriormente, [!UICONTROL Launch]) y debe tener permisos de usuario para administrar y ver flujos de datos.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Saber cuándo utilizar un conjunto de datos.
* Crear un flujo de datos.
* Configuración de una secuencia de datos.

## Crear un flujo de datos

Las secuencias de datos se pueden crear en la variable [!UICONTROL Recopilación de datos] interfaz con el [!UICONTROL Datastream] herramienta de configuración. Para crear una secuencia de datos:

1. Asegúrese de que está en el entorno limitado del Experience Platform correcto, ya que los flujos de datos se definen en un nivel de entorno limitado.
1. Seleccionar **[!UICONTROL Datastreams]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Nueva secuencia de datos]**.

   ![inicio de flujos de datos](assets/datastream-new.png)

1. Proporcione un **[!UICONTROL Nombre]**, por ejemplo `Luma Mobile App` y una **[!UICONTROL Descripción]**, por ejemplo `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Recordatorio final: si va a seguir este tutorial con varias personas en una sola zona protegida o utiliza una cuenta compartida, considere la posibilidad de añadir o anteponer una identificación como parte de las convenciones de nomenclatura. Por ejemplo, en lugar de `Luma Mobile App Event Dataset`, utilice `Luma Mobile App Event Dataset - Joe Smith`. Consulte también la nota en [Información general](overview.md).

1. Seleccione el esquema que ha creado en la lección anterior en la **Esquema de evento** lista.
1. Seleccione **[!UICONTROL Guardar]**.

   ![nuevos flujos de datos](assets/datastream-name.png)


## Agregar servicios

Cuando esté pasando por el (opcional) [Analytics](analytics.md) y [Experience Platform](platform.md) En este tutorial, se explican las lecciones aprendidas al añadir servicios al conjunto de datos para garantizar que, cuando el SDK de Platform Mobile envíe datos a la red perimetral, el conjunto de datos reenvíe esos datos a los servicios configurados.

### Adobe Analytics

1. Seleccione **[!UICONTROL Agregar servicio]**.

1. Añadir **[!UICONTROL Adobe Analytics]** desde el [!UICONTROL Servicio] lista,

1. Escriba el nombre del grupo de informes que desee usar en **[!UICONTROL ID del grupo de informes]**.

1. Habilitar el servicio cambiando **[!UICONTROL Habilitado]** en.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir Adobe Analytics como servicio de flujo de datos](assets/datastream-service-aa.png)


### Adobe Experience Platform

También es posible que desee habilitar el servicio Adobe Experience Platform.

>[!IMPORTANT]
>
>Solo puede habilitar el servicio Adobe Experience Platform cuando haya creado un conjunto de datos de evento. Si aún no ha creado un conjunto de datos de evento, siga las instrucciones [aquí](platform.md).

1. Clic ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir servicio]** para agregar otro servicio.

1. Seleccione **[!UICONTROL Adobe Experience Platform]** en la lista [!UICONTROL Servicio].

1. Habilitar el servicio cambiando **[!UICONTROL Habilitado]** en.

1. Seleccione el **[!UICONTROL Conjunto de datos de evento]** que ha creado como parte de [Crear un conjunto de datos](platform.md#create-a-dataset) instrucciones, por ejemplo **Conjunto de datos de evento de aplicación móvil Luma**

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir Adobe Experience Platform como servicio de flujo de datos](assets/datastream-service-aep.png)
1. La configuración final debería tener un aspecto similar al siguiente.

   ![configuración de secuencia de datos](assets/datastream-settings.png)


>[!NOTE]
>
>Al habilitar cada uno de los servicios que utiliza su organización, se garantiza que los datos recopilados en la aplicación móvil se puedan utilizar en todas partes. Para obtener más información sobre la configuración del flujo de datos, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Al implementar el SDK de Platform Mobile en su propia aplicación, debe crear tres flujos de datos para asignarlos a sus tres entornos de etiquetas (desarrollo, fase y producción). Si utiliza el SDK móvil de Platform con aplicaciones basadas en Platform como Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, debe asegurarse de crear esos flujos de datos en los entornos limitados adecuados.

>[!SUCCESS]
>
>Ahora tiene una secuencia de datos para utilizar durante el resto del tutorial.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Configuración de etiquetas](configure-tags.md)**
