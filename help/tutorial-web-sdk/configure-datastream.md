---
title: Configuración de una secuencia de datos para el SDK web de Platform
description: Obtenga información sobre cómo habilitar un flujo de datos y configurar soluciones de Experience Cloud. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Datastreams
jira: KT-15399
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 8%

---

# Configuración de una secuencia de datos

Obtenga información sobre cómo configurar una secuencia de datos para el SDK web de Adobe Experience Platform.

[Datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) indica al Edge Network de Adobe Experience Platform dónde enviar los datos recopilados por el SDK web de Platform. En la configuración de flujos de datos, se habilitan las aplicaciones de Experience Cloud, la cuenta de Experience Platform y el reenvío de eventos.

![SDK web, flujos de datos y diagrama de Edge Network](assets/dc-websdk-datastreams.png)

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Crear un flujo de datos
* Introducción a las anulaciones de flujos de datos

## Requisitos previos

Antes de configurar la secuencia de datos, debe haber completado las siguientes lecciones:

* [Configuración de un esquema](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)

## Crear un flujo de datos

Ahora puede crear un flujo de datos para indicar a Platform Edge Network dónde enviar los datos recopilados por el SDK web.

**Para crear una secuencia de datos:**

1. Abrir la [interfaz de recopilación de datos](https://launch.adobe.com/){target="_blank"}
1. Asegúrese de que está en la zona protegida correcta

   >[!NOTE]
   >
   >Si es cliente de una aplicación basada en Platform como Real-Time CDP o Journey Optimizer, le recomendamos que utilice una zona protegida de desarrollo para este tutorial. Si no lo está, use la zona protegida **[!UICONTROL Prod]**.

1. Vaya a **[!UICONTROL Datastreams]** en el panel de navegación izquierdo
1. Seleccionar **[!UICONTROL Nueva secuencia de datos]**
1. Escriba `Luma Web SDK: Development Environment` como **[!UICONTROL Nombre]**. Se hace referencia a este nombre más adelante al configurar la extensión del SDK web en la propiedad de etiquetas.
1. Seleccionar **[!UICONTROL Guardar]**

   ![Crear la secuencia de datos](assets/datastream-create-new-datastream.png)

   >[!NOTE]
   >
   >No es necesario que seleccione un esquema. La selección de esquemas solo es necesaria si usa la característica [Preparación de datos para la recopilación de datos](/help/data-collection/edge/data-prep.md).

En la siguiente pantalla, puede agregar servicios como aplicaciones de Adobe al conjunto de datos, pero no agregará ningún servicio en este punto. Lo hará más adelante en las lecciones [Configurar Experience Platform](setup-experience-platform.md), [Configurar Analytics](setup-analytics.md), [Configurar Audience Manager](setup-audience-manager.md), [Configurar destino](setup-target.md) o [Reenvío de eventos](setup-event-forwarding.md).

>[!NOTE]
>
>Al implementar el SDK web de Platform en su propio sitio web, debe crear tres flujos de datos para asignarlos a sus tres entornos de etiquetas (desarrollo, fase y producción). Si utiliza el SDK web de Platform con aplicaciones basadas en Platform como Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, debe asegurarse de crear esas secuencias de datos en los entornos limitados de Platform correspondientes.

## Anular una secuencia de datos

[Anulaciones de secuencia de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides) le permiten definir configuraciones adicionales para su secuencia de datos y luego anular la configuración predeterminada en ciertas condiciones.

La anulación de la configuración del flujo de datos es un proceso de dos pasos:

1. En primer lugar, defina las anulaciones de flujos de datos en la configuración del servicio de flujos de datos. Por ejemplo, puede definir grupos de informes de Analytics, espacios de trabajo de Target o conjuntos de datos de Platform alternativos para utilizarlos como invalidaciones.
1. A continuación, envíe las invalidaciones al Edge Network mediante una acción de evento de envío del SDK web o mediante una configuración en la extensión de etiqueta del SDK web.

En la lección [Configurar Adobe Analytics](setup-analytics.md), reemplaza el grupo de informes de una página mediante la acción Enviar evento del SDK web de Platform.

Ya está listo para instalar la extensión del SDK web de Platform en su propiedad de etiquetas.

[Siguiente: ](install-web-sdk.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
