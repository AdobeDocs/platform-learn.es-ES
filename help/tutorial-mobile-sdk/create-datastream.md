---
title: Configurar una secuencia de datos
description: Obtenga información sobre cómo crear una secuencia de datos en Experience Platform.
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 9%

---

# Crear un flujo de datos

Obtenga información sobre cómo crear una secuencia de datos en Experience Platform.

Un conjunto de datos es una configuración del lado del servidor en Platform Edge Network.  La secuencia de datos garantiza que los datos entrantes en la red perimetral de Platform se enruten correctamente a las aplicaciones y servicios de Adobe Experience Cloud. Para obtener más información, consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es) o esto [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=es).

## Requisitos previos

Para crear una secuencia de datos, su organización debe estar aprovisionada para esta función en la interfaz de recopilación de datos (anteriormente, [!UICONTROL Launch]) y debe tener permisos de usuario para [!UICONTROL Experience Platform] > [!UICONTROL Recopilación de datos] > **[!UICONTROL Administrar flujos de datos]** y **[!UICONTROL Ver flujos de datos]**.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Saber cuándo utilizar un conjunto de datos.
* Crear un flujo de datos.
* Configurar una secuencia de datos.

## Crear un flujo de datos

Las secuencias de datos se pueden crear en la variable [!UICONTROL Recopilación de datos] interfaz con el [!UICONTROL Datastream] herramienta de configuración. Para crear una secuencia de datos:

1. Asegúrese de que está en la zona protegida de Platform correcta.
1. Seleccione **[!UICONTROL Nueva secuencia de datos]**.

   ![inicio de flujos de datos](assets/mobile-datastream-new.png)

1. Proporcione un nombre, por ejemplo `Luma App`.
1. Seleccione el esquema que ha creado en la lección anterior.
1. Seleccione **[!UICONTROL Guardar]**.

   ![nuevos flujos de datos](assets/mobile-datastream-name.png)


## Agregar servicios

A continuación, puede conectar los servicios de Experience Cloud a su conjunto de datos. Cuando el SDK de Platform Mobile envía datos a Edge Network, el conjunto de datos envía los datos a estos servicios:

1. Añadir **[!UICONTROL Adobe Analytics]** y proporcionan un grupo de informes.

1. Activar **[!UICONTROL Adobe Audience Manager]** (opcional).

1. Activar **[!UICONTROL Adobe Experience Platform]** y proporcionar un **[!UICONTROL conjunto de datos]** (opcional).
   * Si aún no ha creado un conjunto de datos, siga las instrucciones [aquí](platform.md).

1. La configuración final debería tener un aspecto similar al siguiente.
   ![configuración de secuencia de datos](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>Al habilitar cada uno de los servicios que utiliza su organización, se garantiza que los datos recopilados en la aplicación móvil se puedan utilizar en todas partes. Para obtener más información sobre la configuración del flujo de datos, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Al implementar el SDK de Platform Mobile en su propio sitio web, debe crear tres flujos de datos para asignarlos a sus tres entornos de etiquetas (desarrollo, fase y producción). Si utiliza el SDK de Platform Mobile con aplicaciones basadas en Platform, como Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, debe asegurarse de crear dichos flujos de datos en los entornos limitados de Platform correspondientes.

Siguiente: **[Configuración de etiquetas](configure-tags.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
