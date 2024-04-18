---
title: Instalación y configuración de la extensión de etiquetas del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo instalar y configurar la extensión de etiqueta SDK web de Platform en la interfaz de recopilación de datos. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK
exl-id: 7dedf9ea-eeda-4738-9633-b5a5a5f5f9ae
source-git-commit: fe8b92c560c9676a44935005cc558388244d6aea
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 12%

---

# Instalación de la extensión de etiquetas de SDK web de Adobe Experience Platform

Obtenga información sobre cómo instalar y configurar la extensión de etiqueta del SDK web de Platform. La forma más sencilla de implementar el SDK web es mediante el administrador de etiquetas de Adobe, las etiquetas (anteriormente conocido como Launch). La extensión de etiqueta del SDK web de Platform es la _extensión de etiqueta solamente_ necesario para enviar datos a _todas las aplicaciones de Adobe Experience Cloud_, incluido [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), REAL-TIME CUSTOMER DATA PLATFORM y [Journey Optimizer](journey-optimizer/setup-web-channel.md)!

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Creación de una propiedad de etiqueta en la interfaz de recopilación de datos
* Instalación de la extensión de etiqueta del SDK web de Platform
* Asigne el flujo de datos creado anteriormente a la extensión.

## Requisitos previos

Debe haber completado las lecciones anteriores en este tutorial:

* [Configuración de una secuencia de datos](configure-datastream.md)

## Instalación de la extensión del SDK web de Experience Platform

### Añadir una propiedad

Primero debe tener una propiedad de etiqueta. Una propiedad es un contenedor para todos los elementos JavaScript, las reglas y otras funciones necesarias para recopilar detalles de una página web y enviarlos a varias ubicaciones.

Cree una nueva propiedad de etiqueta para el tutorial:

1. Abra el [Interfaz de recopilación de datos](https://launch.adobe.com/){target="_blank"}
1. Seleccionar **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo
1. Seleccione el **[!UICONTROL Nueva propiedad]** botón
   ![Añadir una nueva propiedad](assets/websdk-property-addNewProperty.png)
1. Como el **[!UICONTROL Nombre]**, introduzca `Web SDK Course` (añada su nombre al final, si varias personas de su compañía realizan este tutorial)
1. Como el **[!UICONTROL Domains]**, introduzca `enablementadobe.com` (explicado más tarde)
1. Seleccionar **[!UICONTROL Guardar]**
   ![Detalles de la propiedad](assets/websdk-property-propertyDetails.png)

## Añadir la extensión del SDK web

Con el esquema XDM, la secuencia de datos y la propiedad de etiqueta creados, ya puede instalar la extensión del SDK web de Platform:

1. Abra la nueva propiedad de etiquetas
1. Ir a **[!UICONTROL Extensiones]** > **[!UICONTROL Catálogo]**
1. Buscar por `Adobe Experience Platform Web SDK`
1. Seleccionar **[!UICONTROL Instalar]**

   ![Instalar extensión del SDK web](assets/extension-platform-web-sdk.png)


## Vinculación del SDK web de Platform al conjunto de datos

Deje la mayoría de las configuraciones predeterminadas y actualícelas más tarde, según sea necesario. Lo único que debe hacer ahora es vincular la extensión al conjunto de datos:

1. En **[!UICONTROL Datastreams]**, seleccione la **[!UICONTROL Elegir de la lista]** método de entrada
1. Seleccione la secuencia de datos que creó anteriormente, `Luma Web SDK`
1. Seleccionar **[!UICONTROL Guardar]**

   >[!NOTE]
   >
   > Si no encuentra el conjunto de datos, vaya a la [Configuración de una secuencia de datos](configure-datastream.md) y siga los pasos para crear uno

   ![Selección de flujo de datos](assets/extension-luma-web-sdk-datastream-extension.png)

Ahora que ha instalado el SDK web de Platform y lo ha asociado al conjunto de datos, está listo para empezar a asignar elementos de datos a un objeto XDM con el esquema que ha creado.

>[!NOTE]
>
>Durante este tutorial, solo debe configurar un conjunto de datos y asociarlo a todos los entornos de etiquetas (desarrollo, fase y producción). Al implementar el SDK web de Platform en su propio sitio web, debe configurar un flujo de datos independiente para cada entorno y asignarlo a los entornos de etiquetas.

>[!NOTE]
>
>Aunque no configuró un CNAME en el [!UICONTROL Dominio de Edge] Al configurar en esta lección, Adobe recomienda utilizar un CNAME al implementar el SDK web de Platform en su propio sitio web. Aunque la implementación de CNAME no proporciona ningún beneficio en términos de vida útil de las cookies, puede haber otros beneficios. Estos beneficios incluyen bloqueadores de anuncios y exploradores menos comunes que impiden que se envíen datos a dominios que clasifican como rastreadores. En estos casos, el uso de un CNAME puede impedir que la recopilación de datos se interrumpa para los usuarios que utilizan estas herramientas.

Para obtener más información sobre cada sección de la extensión, consulte [Configuración de la extensión SDK para web de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=es)



[Siguiente: ](create-data-elements.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
