---
title: Configuración de un flujo de datos para implementaciones de Platform Mobile SDK
description: Aprenda a crear una secuencia de datos en Experience Platform.
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Crear un flujo de datos

Aprenda a crear una secuencia de datos en Experience Platform.

Un conjunto de datos es una configuración del lado del servidor en Platform Edge Network. La secuencia de datos garantiza que los datos entrantes en Platform Edge Network se enruten correctamente a las aplicaciones y servicios de Adobe Experience Cloud. Para obtener más información, consulte la [documentación](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) o este [vídeo](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/edge-network/configure-datastreams).

![Arquitectura](assets/architecture.png){zoomable="yes"}

## Requisitos previos

Para crear una secuencia de datos, su organización debe estar aprovisionada para esta característica en la interfaz de recopilación de datos (anteriormente [!UICONTROL Launch]) y debe tener permisos de usuario para administrar y ver secuencias de datos.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Saber cuándo utilizar un conjunto de datos.
* Cree una secuencia de datos.
* Configure una secuencia de datos.

## Crear un flujo de datos

Se pueden crear flujos de datos en la interfaz [!UICONTROL Recopilación de datos] con la herramienta de configuración [!UICONTROL Datastream]. Para crear una secuencia de datos:

1. Asegúrese de que está en el entorno limitado de Experience Platform correcto, ya que los flujos de datos se definen en un nivel de entorno limitado.
1. Seleccione **[!UICONTROL Datastreams]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Nueva secuencia de datos]**.

   ![inicio de flujos de datos](assets/datastream-new.png){zoomable="yes"}

1. Proporcione **[!UICONTROL Nombre]**, por ejemplo `Luma Mobile App` y **[!UICONTROL Descripción]**, por ejemplo `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Recordatorio final: si va a seguir este tutorial con varias personas en una sola zona protegida o utiliza una cuenta compartida, considere la posibilidad de añadir o anteponer una identificación como parte de las convenciones de nomenclatura. Por ejemplo, en lugar de `Luma Mobile App Event Dataset`, use `Luma Mobile App Event Dataset - Joe Smith`. Consulte también la nota de [Información general](overview.md).

1. Seleccione el esquema que creó en la lección anterior de la lista **Esquema de eventos**.
1. Seleccione **[!UICONTROL Guardar]**.

   ![nuevas secuencias de datos](assets/datastream-name.png){zoomable="yes"}


## Agregar servicios

Cuando se siguen las lecciones (opcionales) de [Analytics](analytics.md) y [Experience Platform](platform.md) de este tutorial, se agregan servicios a la secuencia de datos para que los datos enviados a Platform Edge Network se reenvíen a estas aplicaciones.

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png){zoomable="yes"}


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

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png){zoomable="yes"}
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png){zoomable="yes"}

-->


>[!NOTE]
>
>Al habilitar cada uno de los servicios que utiliza su organización, se garantiza que los datos recopilados en la aplicación móvil se puedan utilizar en todas partes. Consulte [configuración de secuencia de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) para obtener más información.

Al implementar Platform Mobile SDK en su propia aplicación, debe crear tres flujos de datos para asignarlos a sus tres entornos de etiquetas (desarrollo, fase y producción). Si utiliza Platform Mobile SDK con aplicaciones basadas en Platform, como Adobe Real-Time Customer Data Platform o Adobe Journey Optimizer, debe asegurarse de crear esas secuencias de datos en los entornos limitados adecuados.

>[!SUCCESS]
>
>Ahora tiene una secuencia de datos para utilizar durante el resto del tutorial.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Configurar una propiedad de etiqueta](configure-tags.md)**
