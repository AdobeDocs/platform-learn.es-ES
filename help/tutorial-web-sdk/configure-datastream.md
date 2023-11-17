---
title: Configuración de una secuencia de datos
description: Obtenga información sobre cómo habilitar un flujo de datos y configurar soluciones de Experience Cloud. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Tags,Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 10%

---

# Configuración de una secuencia de datos

Obtenga información sobre cómo habilitar un flujo de datos y configurar soluciones de Experience Cloud.

Las secuencias de datos indican a Adobe Experience Platform Edge Network dónde enviar los datos recopilados por el SDK web de Platform. En la configuración de flujos de datos, se habilitan las aplicaciones de Experience Cloud, la cuenta de Experience Platform y el reenvío de eventos. Consulte la [Aspectos básicos de configuración de una secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es) para obtener información más detallada.

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Crear un flujo de datos
* Habilitar las aplicaciones de Experience Cloud
* Habilitar Experience Platform

## Requisitos previos

Antes de configurar la secuencia de datos, debe haber completado las siguientes lecciones:

* [Configure los permisos](configure-permissions.md)
* [Configuración de un esquema](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)

## Crear un flujo de datos

Ahora puede crear una secuencia de datos para indicar a Platform Edge Network dónde enviar los datos recopilados por el SDK web.

**Para crear una secuencia de datos:**

1. Abra el [Interfaz de recopilación de datos](https://launch.adobe.com/){target="_blank"}
1. Asegúrese de que está en la zona protegida correcta

   >[!NOTE]
   >
   >Si es cliente de una aplicación basada en Platform como Real-Time CDP, le recomendamos que utilice una zona protegida de desarrollo para este tutorial. Si no lo está, use el **[!UICONTROL Prod]** zona protegida.

1. Ir a **[!UICONTROL Datastreams]** en el panel de navegación izquierdo
1. Seleccionar **[!UICONTROL Nueva secuencia de datos]** en el lado derecho de la pantalla.
1. Escriba `Luma Web SDK` como **[!UICONTROL nombre]**. Se hace referencia a este nombre más adelante al configurar la extensión del SDK web en la propiedad de etiquetas.
1. Seleccione su `Luma Web Event Data` como el **[!UICONTROL Esquema de evento]**
1. Seleccione **[!UICONTROL Guardar]**

   ![Creación de la secuencia de datos](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >La función de asignación se incorporará a este tutorial más adelante.




En la siguiente pantalla, puede añadir servicios como aplicaciones de Adobe al conjunto de datos, pero no agregará ningún servicio en este punto del tutorial. Lo hará más adelante en las lecciones [Configurar Experience Platform](setup-experience-platform.md), [Configuración de Analytics](setup-analytics.md), [Configurar Audience Manager](setup-audience-manager.md), [Configurar Target](setup-target.md), o [Reenvío de eventos](setup-event-forwarding.md).

>[!NOTE]
>
>Al implementar el SDK web de Platform en su propio sitio web, debe crear tres flujos de datos para asignarlos a sus tres entornos de etiquetas (desarrollo, fase y producción). Si utiliza el SDK web de Platform con aplicaciones basadas en Platform como Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, debe asegurarse de crear esas secuencias de datos en los entornos limitados de Platform correspondientes.

Ya está listo para instalar la extensión del SDK web de Platform en su propiedad de etiquetas.

[Siguiente: ](install-web-sdk.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
