---
title: Instalación y configuración de la extensión de etiquetas de Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo instalar y configurar la extensión de etiquetas de Platform Web SDK en la interfaz de recopilación de datos. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK, Tags
jira: KT-15404
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 11%

---

# Instalación de la extensión de etiquetas de Adobe Experience Platform Web SDK

Obtenga información sobre cómo instalar y configurar la extensión de etiquetas de Adobe Experience Platform Web SDK. La forma más sencilla de implementar Web SDK es utilizar el administrador de etiquetas de Adobe, las etiquetas (anteriormente conocido como Launch). La extensión de etiquetas Platform Web SDK es la _única extensión de etiquetas_ necesaria para enviar datos a _todas las aplicaciones de Adobe Experience Cloud_, incluidas [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-Time Customer Data Platform y [Journey Optimizer](setup-web-channel.md).

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Creación de una propiedad de etiqueta en la interfaz de recopilación de datos
* Instalación de la extensión de etiquetas de Platform Web SDK
* Asigne el flujo de datos creado anteriormente a la extensión.

## Requisitos previos

Debe haber completado las lecciones anteriores en este tutorial:

* [Configuración de una secuencia de datos](configure-datastream.md)

### Añadir una propiedad de etiqueta

Primero debe tener una propiedad de etiqueta. Una propiedad es un contenedor para todas las JavaScript, reglas y otras funciones necesarias para recopilar detalles de una página web y enviarlos a varias ubicaciones.

Cree una nueva propiedad de etiqueta para el tutorial:

1. Abrir la [interfaz de recopilación de datos](https://experience.adobe.com/data-collection/){target="_blank"}
1. Seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo
1. Seleccione el botón **[!UICONTROL Nueva propiedad]**
   ![Agregar nueva propiedad](assets/websdk-property-addNewProperty.png)
1. Como **[!UICONTROL Nombre]**, escriba `Web SDK Course` (agregue su nombre al final, si varias personas de su compañía realizan este tutorial)
1. Como **[!UICONTROL Dominios]**, escriba `enablementadobe.com` (explicado más tarde)
1. Seleccionar **[!UICONTROL Guardar]**
   ![Detalles de la propiedad](assets/websdk-property-propertyDetails.png)

## Añadir la extensión de Web SDK

Con el esquema XDM, la secuencia de datos y la propiedad de etiqueta creados, ya puede instalar la extensión web SDK de Platform:

1. Abra la nueva propiedad de etiquetas
1. Ir a **[!UICONTROL Extensiones]** > **[!UICONTROL Catálogo]**
1. Buscar `Adobe Experience Platform Web SDK`
1. Seleccionar **[!UICONTROL Instalar]**

   ![Instalar extensión de Web SDK](assets/extension-platform-web-sdk.png)


## Vinculación de la extensión al conjunto de datos

Deje la mayoría de las configuraciones predeterminadas y actualícelas más tarde, según sea necesario. Lo único que debe hacer ahora es vincular la extensión al conjunto de datos:

1. En **[!UICONTROL Datastreams]**, seleccione el método de entrada **[!UICONTROL Choose from list]**
1. Seleccione el entorno limitado en el que ha creado el esquema, el área de nombres de identidad y el conjunto de datos
1. Seleccione la secuencia de datos que creó anteriormente, `Luma Web SDK`
1. Seleccionar **[!UICONTROL Guardar]**

   >[!NOTE]
   >
   > Si no encuentra su secuencia de datos, vaya a la lección [Configurar una secuencia de datos](configure-datastream.md) y siga los pasos para crear una

   ![Selección de secuencia de datos](assets/extension-luma-web-sdk-datastream-extension.png)

Para obtener más información sobre cada sección de la extensión, consulte [Configuración de la extensión de Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).

>[!NOTE]
>
>Aunque no configuró un CNAME en la configuración de [!UICONTROL dominio de Edge] en esta lección, Adobe recomienda utilizar un CNAME al implementar Platform Web SDK en su propio sitio web. Aunque la implementación de CNAME no proporciona ningún beneficio en términos de vida útil de las cookies, puede haber otros beneficios. Estos beneficios incluyen bloqueadores de anuncios y exploradores menos comunes que impiden que se envíen datos a dominios que clasifican como rastreadores. En estos casos, el uso de un CNAME puede impedir que la recopilación de datos se interrumpa para los usuarios que utilizan estas herramientas.

>[!NOTE]
>
>Durante este tutorial, solo debe configurar un conjunto de datos y asociarlo a todos los entornos de etiquetas (desarrollo, fase y producción). Al implementar Platform Web SDK en su propio sitio web, debe configurar un flujo de datos independiente para cada entorno y asignarlo en consecuencia en la configuración de la extensión.

Ahora que ha instalado Platform Web SDK y lo ha asociado al conjunto de datos, está listo para empezar a recopilar datos.

[Siguiente: ](create-data-elements.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Web SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
