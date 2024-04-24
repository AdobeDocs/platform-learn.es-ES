---
title: Configuración de un área de nombres de identidad
description: Obtenga información sobre cómo configurar áreas de nombres de identidad para utilizarlas con el SDK web de Adobe Experience Platform. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 7%

---

# Configuración de un área de nombres de identidad

Obtenga información sobre cómo configurar áreas de nombres de identidad para utilizarlas con el SDK web de Adobe Experience Platform.

El [Servicio de identidad de Adobe Experience Cloud](https://experienceleague.adobe.com/en/docs/id-service/using/home) establece un ID de visitante común (el ECID) en todas las aplicaciones de Adobe basadas en SDK para potenciar las funciones de Experience Cloud, como el uso compartido de audiencias entre aplicaciones. También puede enviar sus propios ID de cliente al servicio para permitir integraciones y segmentaciones en todos los dispositivos con otros sistemas, como el sistema de administración de la relación con los clientes (CRM).

El [Servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) (sí, ¡hay dos!) utiliza los ECID y los ID de cliente para generar gráficos de identidad, lo que le permite combinar atributos y comportamientos en los perfiles de cliente en tiempo real.

>[!NOTE]
>
> Con fines de demostración, los ejercicios de esta lección le permiten capturar los detalles de identidad de un cliente ficticio que ha iniciado sesión en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) uso de las credenciales, **usuario: `test@adobe.com` / password: prueba**.

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Comprender las áreas de nombres de identidad
* Cree un área de nombres de identidad personalizada para capturar un ID de CRM interno


## Requisitos previos

Ya debe haber completado las lecciones anteriores:

* [Configuración de esquemas](configure-schemas.md)

>[!IMPORTANT]
>
>El [Extensión de ID de Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) no es necesario al implementar el SDK web de Adobe Experience Platform, ya que la biblioteca JavaScript del SDK web contiene la funcionalidad del servicio de ID de visitante.
>
> Si su sitio web ya utiliza el servicio de ID de Experience Cloud en su sitio web (a través de la API de visitante o la extensión de etiqueta del servicio de ID de Experience Cloud) y desea seguir utilizándolo al migrar al SDK web de Adobe Experience Platform, debe utilizar la última versión de la API de visitante o la extensión de etiqueta del servicio de ID de Experience Cloud. Consulte [Migración de ID](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview) para obtener más información.

## Crear un área de nombres de identidad

En este ejercicio, se crea un área de nombres de identidad para el campo de identidad personalizado de Luma, `lumaCrmId`. Las áreas de nombres de identidad desempeñan un papel esencial en la creación de perfiles de clientes en tiempo real, ya que dos valores coincidentes en la misma área de nombres permiten que dos fuentes de datos formen un gráfico de identidad.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre la identidad en Adobe Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

Ahora, cree un área de nombres para el ID de Luma CRM:

1. Abra el [Interfaz de recopilación de datos](https://launch.adobe.com/){target="_blank"}
1. Seleccione la zona protegida que está utilizando para el tutorial.

   >[!NOTE]
   >
   >Si es cliente de una aplicación basada en Platform como Real-Time CDP o Journey Optimizer, le recomendamos que utilice una zona protegida de desarrollo para este tutorial. Si no lo está, use el **[!UICONTROL Prod]** zona protegida.

1. Seleccionar **[!UICONTROL Identidades]** en el panel de navegación izquierdo
1. Seleccionar **[!UICONTROL Examinar]**

   Aparece una lista de áreas de nombres de identidad en la interfaz principal de la página, con sus nombres, símbolos de identidad, fecha de última actualización y si son áreas de nombres estándar o personalizadas. El carril derecho contiene información sobre [!UICONTROL Intensidad del gráfico de identidad].

1. Seleccionar **[!UICONTROL Crear área de nombres de identidad]**

   ![Ver identidades](assets/configure-identities-screen.png)

1. Proporcione los siguientes detalles y seleccione **[!UICONTROL Crear]**.

   | Campo | Valor |
   |---------------|-----------|
   | Nombre para mostrar | ID de Luma CRM |
   | Símbolo de identidad | lumaCrmId |
   | Tipo | ID individual entre dispositivos |


   ![Crear áreas de nombres](assets/identities-create-namespace.png)


   El área de nombres de identidad se rellena en **[!UICONTROL Identidades]** pantalla.

   ![Crear áreas de nombres](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> En el [Crear identidades](create-identities.md) En esta lección, aprenderá a utilizar esta área de nombres al enviar identidades a Platform Edge Network.

## Cree el área de nombres de identidad en la zona protegida de producción

Debido a una limitación actual en la extensión del SDK web, también se deben crear áreas de nombres de identidad en el entorno limitado de producción para utilizar el área de nombres y enviar datos a un entorno limitado de desarrollo. Por lo tanto, si ha estado utilizando una zona protegida de desarrollo para este tutorial, cree también el `Luma CRM ID` en la zona protegida de producción.

Ahora que las identidades están configuradas, se puede configurar el conjunto de datos.

[Siguiente: ](configure-datastream.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
