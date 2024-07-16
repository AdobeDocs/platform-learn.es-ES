---
title: Configuración de una secuencia de datos para implementaciones del SDK de Platform Mobile
description: Aprenda a crear una secuencia de datos en Experience Platform.
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 6%

---

# Crear un flujo de datos

Aprenda a crear una secuencia de datos en Experience Platform.

Un conjunto de datos es una configuración del lado del servidor en Platform Edge Network. La secuencia de datos garantiza que los datos entrantes del Edge Network de Platform se enruten correctamente a las aplicaciones y servicios de Adobe Experience Cloud. Para obtener más información, consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) o este [vídeo](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=es).

![Arquitectura](assets/architecture.png)

## Requisitos previos

Para crear una secuencia de datos, su organización debe estar aprovisionada para esta característica en la interfaz de recopilación de datos (anteriormente [!UICONTROL Launch]) y debe tener permisos de usuario para administrar y ver secuencias de datos.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Saber cuándo utilizar un conjunto de datos.
* Cree una secuencia de datos.
* Configure una secuencia de datos.

## Crear un flujo de datos

Se pueden crear flujos de datos en la interfaz [!UICONTROL Recopilación de datos] con la herramienta de configuración [!UICONTROL Datastream]. Para crear una secuencia de datos:

1. Asegúrese de que está en el entorno limitado del Experience Platform correcto, ya que los flujos de datos se definen en un nivel de entorno limitado.
1. Seleccione **[!UICONTROL Datastreams]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Nueva secuencia de datos]**.

   ![inicio de flujos de datos](assets/datastream-new.png)

1. Proporcione **[!UICONTROL Nombre]**, por ejemplo `Luma Mobile App` y **[!UICONTROL Descripción]**, por ejemplo `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Recordatorio final: si va a seguir este tutorial con varias personas en una sola zona protegida o utiliza una cuenta compartida, considere la posibilidad de añadir o anteponer una identificación como parte de las convenciones de nomenclatura. Por ejemplo, en lugar de `Luma Mobile App Event Dataset`, use `Luma Mobile App Event Dataset - Joe Smith`. Consulte también la nota de [Información general](overview.md).

1. Seleccione el esquema que creó en la lección anterior de la lista **Esquema de eventos**.
1. Seleccione **[!UICONTROL Guardar]**.

   ![nuevas secuencias de datos](assets/datastream-name.png)


## Agregar servicios

Cuando se siguen las lecciones (opcionales) de [Analytics](analytics.md) y [Experience Platform](platform.md) de este tutorial, se agregan servicios a la secuencia de datos para que los datos enviados al Edge Network de Platform se reenvíen a estas aplicaciones.

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png)


### Adobe Experience Platform

You might also want to enable the Adobe Experience Platform service. 

>[!IMPORTANT]
>
>You can only enable the Adobe Experience Platform service when having created an event dataset. If you don't already have an event dataset created, follow the instructions [here](platform.md).

1. Click ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add Service]** to add another service.

1. Select **[!UICONTROL Adobe Experience Platform]** from the [!UICONTROL Service] list.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select the **[!UICONTROL Event Dataset]** that you created as part of the [Create a dataset](platform.md#create-a-dataset) instructions, for example **Luma Mobile App Event Dataset**

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png)
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png)

-->


>[!NOTE]
>
>Al habilitar cada uno de los servicios que utiliza su organización, se garantiza que los datos recopilados en la aplicación móvil se puedan utilizar en todas partes. Para obtener más información acerca de la configuración del flujo de datos, revise la documentación [aquí](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).

Al implementar el SDK de Platform Mobile en su propia aplicación, debe crear tres flujos de datos para asignarlos a sus tres entornos de etiquetas (desarrollo, fase y producción). Si utiliza el SDK móvil de Platform con aplicaciones basadas en Platform como Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, debe asegurarse de crear esos flujos de datos en los entornos limitados adecuados.

>[!SUCCESS]
>
>Ahora tiene una secuencia de datos para utilizar durante el resto del tutorial.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Configurar una propiedad de etiqueta](configure-tags.md)**
