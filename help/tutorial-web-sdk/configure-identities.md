---
title: Configuración de un área de nombres de identidad
description: Obtenga información sobre cómo configurar áreas de nombres de identidad para utilizarlas con el SDK web de Adobe Experience Platform. Esta lección forma parte del tutorial Implementar Adobe Experience Cloud con SDK web .
feature: Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 6%

---

# Configuración de un área de nombres de identidad

Obtenga información sobre cómo configurar áreas de nombres de identidad para utilizarlas con el SDK web de Adobe Experience Platform.

La variable [Servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es) establece un ID de visitante común en todas las soluciones de Adobe para impulsar las funcionalidades de Experience Cloud, como el uso compartido de audiencias entre soluciones. También puede enviar sus propios ID de cliente al servicio para permitir integraciones y segmentación entre dispositivos con otros sistemas, como el sistema de administración de la relación con los clientes (CRM).

Si el sitio web ya utiliza el servicio de ID de Experience Cloud en el sitio web (a través de la API de visitante o la extensión de etiqueta del servicio de ID de Experience Cloud) y desea continuar utilizándolo al migrar al SDK web de Adobe Experience Platform, debe utilizar la última versión de la API de visitante o la extensión de etiqueta del servicio de ID de Experience Cloud. Consulte [Migración de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) para obtener más información.

>[!NOTE]
>
> Para fines de demostración, los ejercicios de esta lección permiten capturar los detalles de identidad de un cliente ficticio que ha iniciado sesión en la [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html) utilizando las credenciales, **usuario: test@adobe.com / contraseña: prueba**. Aunque puede utilizar estos pasos para crear una identidad diferente para sus propios fines, para aprender las capacidades del mapa de identidad en la interfaz de recopilación de datos, primero se recomienda que siga para capturar la identidad de ejemplo.

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Explicación de las áreas de nombres de identidad
* Crear un área de nombres de identidad personalizada para capturar un ID de CRM interno


## Requisitos previos

Ya debe haber completado las lecciones anteriores:

* [Configuración de permisos](configure-permissions.md)
* [Configurar esquemas](configure-schemas.md)

>[!IMPORTANT]
>
>La variable [Extensión de ID de Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) no es necesario al implementar el SDK web de Adobe Experience Platform, ya que la biblioteca JavaScript del SDK web contiene la funcionalidad del servicio de ID de visitante.

## Cree un área de nombres de identidad

En este ejercicio, se crea un área de nombres de identidad para el campo de identidad personalizado de Luma, `lumaCrmId`. Las áreas de nombres de identidad desempeñan un papel fundamental en la creación de perfiles de clientes en tiempo real, ya que dos valores coincidentes en el mismo espacio de nombres permiten que dos fuentes de datos formen un gráfico de identidad.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre la identidad en Adobe Experience Platform:
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

Ahora, cree un área de nombres para el ID de Luma CRM:

1. Abra el [Interfaz de recopilación de datos](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Seleccione el simulador de pruebas que utiliza para el tutorial

   >[!NOTE]
   >
   >Si es cliente de una aplicación basada en Platform como Real-Time CDP, recomendamos utilizar un entorno limitado de desarrollo para este tutorial. Si no lo está, use el **[!UICONTROL Prod]** simulador de pruebas.

1. Select **[!UICONTROL Identidades]** en la navegación izquierda
1. Select **[!UICONTROL Examinar]**

   En la interfaz principal de la página aparece una lista de áreas de nombres de identidad que muestra sus nombres, símbolos de identidad, fecha de la última actualización y si son áreas de nombres estándar o personalizadas. El carril derecho contiene información sobre la intensidad del gráfico de identidad.

1. Select **[!UICONTROL Crear área de nombres de identidad]**

   ![Ver identidades](assets/configure-identities-screen.png)

1. Proporcione los siguientes detalles y seleccione **[!UICONTROL Crear]**.

   | Campo | Valor |
   |---------------|-----------|
   | Nombre para mostrar | ID de Luma CRM |
   | Símbolo de identidad | lumaCrmId |
   | Tipo | ID entre dispositivos |


   ![Crear espacios de nombres](assets/identities-create-namespace.png)


   El área de nombres de identidad se rellena en la variable **[!UICONTROL Identidades]** en el Navegador.

   ![Crear espacios de nombres](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> En el [Crear elementos de datos](create-data-elements.md) aprenderá a utilizar este espacio de nombres al enviar identidades a Platform Edge Network.

## Cree el área de nombres de identidad en el entorno limitado de producción

Debido a una limitación actual en la extensión del SDK web, también se deben crear áreas de nombres de identidad en el entorno limitado de producción para poder utilizar el espacio de nombres y enviar datos a un entorno limitado de desarrollo. Por lo tanto, si ha estado utilizando un entorno limitado de desarrollo para este tutorial, cree también el `Luma CRM ID` en el entorno limitado de producción.

## Recursos adicionales

* Documentación del [Servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=es)
* [API del servicio de identidad](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Ahora que las identidades están establecidas, se puede configurar el conjunto de datos.

[Siguiente: ](configure-datastream.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK web de Adobe Experience Platform. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
