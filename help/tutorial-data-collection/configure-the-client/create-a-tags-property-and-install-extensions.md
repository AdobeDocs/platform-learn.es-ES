---
title: Creación de una propiedad de etiqueta de Adobe Experience Platform e instalación de extensiones
description: Creación de una propiedad de etiqueta de Adobe Experience Platform e instalación de extensiones
exl-id: d0fe82b5-a036-4e13-bae1-d1fee78d0084
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Crear una Adobe Experience Platform [!DNL Tags] propiedades e instalar extensiones

Ahora que el código en la página está insertando datos y eventos en la capa de datos, es hora de que el especialista en marketing lea los datos de la capa de datos y envíe estos datos a Adobe Experience Platform. Esto generalmente requeriría dos bibliotecas JavaScript:

* Capa de datos del cliente de Adobe: En pasos anteriores, se creó una matriz de capa de datos y se insertaron objetos en ella. Para acceder a estos datos, debe cargar la biblioteca JavaScript de la capa de datos del cliente de Adobe. Esta biblioteca proporciona notificaciones para eventos y cambios en la capa de datos, así como acceso sencillo a los datos.
* SDK web de Adobe Experience Platform: Esta biblioteca JavaScript se comunica con la [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). El SDK gestiona la identidad, el consentimiento, la recopilación de datos, la personalización, las audiencias y mucho más.

Aunque puede cargar estas bibliotecas individuales en su sitio web y utilizarlas directamente, le recomendamos que utilice [Etiquetas de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es). Con Etiquetas, puede incrustar un solo script en el HTML y utilizar la interfaz de usuario Etiquetas para implementar tanto la capa de datos del cliente de Adobe como el SDK web de Adobe Experience Platform. Las etiquetas también permiten crear reglas para enviar datos, entre otras cosas. Este tutorial utiliza Etiquetas para este fin y supone que dispone de conocimientos básicos sobre el funcionamiento de las etiquetas.

## Crear una propiedad en Etiquetas

1. [Crear una propiedad en etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Instalación de la extensión de la capa de datos del cliente de Adobe

Instale la extensión de la capa de datos del cliente de Adobe:

1. Select **[!UICONTROL Extensiones]** en la navegación de la izquierda, en la propiedad Tag que está utilizando para este tutorial.
1. Seleccione el **[!UICONTROL Catálogo]** vínculo en la parte superior y, a continuación, busque &quot;capa de datos&quot;.
1. Una vez que la capa de datos del cliente de Adobe se muestre en los resultados, haga clic en el **[!UICONTROL Instalar]** botón. Debería ver una pantalla de configuración. Para este tutorial, no es necesario cambiar los valores predeterminados.
1. Haga clic en **[!UICONTROL Guardar]**.
   ![Instalación de la extensión de capa de datos del cliente de Adobe](../assets/acdl-extension-installation.png)


## Instalación de la extensión del SDK web de Adobe Experience Platform

A continuación, instale la extensión del SDK web de Adobe Experience Platform:

1. Busque la extensión en el catálogo de extensiones y haga clic en las **[!UICONTROL Instalar]** botón. Debería ver la pantalla de configuración:
   ![Instalación de la extensión del SDK web de Adobe Experience Platform](../assets/web-sdk-extension-installation.png)
1. En el [!UICONTROL Datastream] , seleccione el conjunto de datos que ha creado anteriormente. Se le presentan los mismos entornos de conjunto de datos que se vieron en [Crear un conjunto de datos](../configure-the-server/create-a-datastream.md).
   ![Selección del conjunto de datos](../assets/web-sdk-datastream-selection.png)
1. Más adelante en la pantalla de configuración, busque y desmarque **[!UICONTROL Habilitar la recopilación de datos de clic]**. De forma predeterminada, el SDK rastrea automáticamente los vínculos. Sin embargo, en este tutorial se muestra cómo puede rastrear sus propios clics en vínculos mediante información de vínculos personalizados.
1. Haga clic en el **[!UICONTROL Guardar]** para finalizar la instalación de la extensión web SDK de Adobe Experience Platform.

>[!TIP]
>
>Los entornos de conjuntos de datos tienen una relación con los entornos de etiquetas. Supongamos que completa la instalación de la extensión del SDK web de Adobe Experience Platform, crea una biblioteca de etiquetas que incluya la extensión y, a continuación, publica la biblioteca en un entorno de desarrollo de etiquetas. Cuando la biblioteca de etiquetas se carga en la página web y la extensión del SDK web de Adobe Experience Platform realiza una solicitud a Edge Network, la extensión incluye [!UICONTROL Entorno de desarrollo] ID de entorno de datastream. La red perimetral, a su vez, utiliza ese ID para leer la configuración de la variable [!UICONTROL Entorno de desarrollo] entorno de flujo de datos y reenviar datos a los productos de Adobe correspondientes.
>
>En este momento, solo tiene un entorno de conjunto de datos de desarrollo, un entorno de conjunto de datos de ensayo y un entorno de flujo de datos de producción. Es posible crear varios entornos de desarrollo de conjuntos de datos (uno para usted y otro para su compañero, tal vez) mediante la interfaz de usuario del conjunto de datos. Si tiene varios entornos de conjuntos de datos de desarrollo, puede seleccionar cuál desea utilizar para esta propiedad de etiqueta.


Se han instalado las extensiones adecuadas. Es hora de crear reglas y elementos de datos.

[Siguiente: ](create-rules-for-tracking-page-view-and-commerce-events.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
