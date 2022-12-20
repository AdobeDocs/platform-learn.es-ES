---
title: Crear un flujo de datos
description: Crear un flujo de datos
exl-id: 4a33a7f3-8bd8-4d28-9ae4-a0609444485f
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Crear un flujo de datos

Los datos que envía desde su sitio web con Platform Web SDK llegan a un conjunto de servidores de Adobe llamados [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Esta red puede enviar sus datos a la [Conjunto de datos de Adobe Experience Platform que creó anteriormente](create-a-schema.md) y otros productos dentro de Adobe Experience Cloud. Estos productos de Adobe también pueden responder con datos a su página web. Por ejemplo, la red perimetral puede devolver contenido de personalización de Adobe Target.

Para configurar los productos de Adobe que Edge Network envía datos a y desde, debe crear un conjunto de datos. Cuando la red perimetral recibe datos de su página web, consulta el conjunto de datos que ha creado, lee su configuración y reenvía datos a los productos de Adobe correspondientes.

![Configuración del producto Datastream](../assets/datastream-diagram.png)

1. Para crear un conjunto de datos, primero debe navegar a la interfaz de usuario de recopilación de datos. En la esquina superior derecha de Platform, haga clic en la **[!UICONTROL Selector de aplicación]** y seleccione **[!UICONTROL Recopilación de datos]** en el menú desplegable.
   ![Menú de recopilación de datos](../assets/data-collection-menu.png)
1. Una vez que se muestra la interfaz de recopilación de datos, seleccione **[!UICONTROL Datastreams]** en el panel de navegación izquierdo y, a continuación, en la sección **[!UICONTROL Nuevo conjunto de datos]** en la esquina superior derecha.
1. Proporcione un nombre para el conjunto de datos, seleccione [el esquema que creó anteriormente](create-a-schema.md) como el **[!UICONTROL Conjunto de datos del evento]** y seleccione **[!UICONTROL Guardar]** (la asignación se cubre más adelante).
   ![Nombre y descripción del conjunto de datos](../assets/datastream-name-description.png)

## Añadir servicio al conjunto de datos

La siguiente pantalla le permite añadir qué productos y servicios de Adobe deben recibir los datos que envía desde su sitio web.

1. Seleccione el **[!UICONTROL Añadir servicio]** comando. Para los fines de este tutorial, active solo Adobe Experience Platform, seleccione [el conjunto de datos que creó anteriormente](create-a-dataset.md) y seleccione **[!UICONTROL Guardar]** en la esquina superior derecha. Se ha creado el conjunto de datos.
   ![Configuración del producto Datastream](../assets/datastream-product-configuration.png)

## Entornos de almacén de datos

Las empresas suelen tener una ruta de promoción para cualquier actualización del sitio web. Alguien de la empresa (un especialista en marketing o ingeniero, según los cambios) suele probar sus cambios en un entorno de desarrollo que solo esa persona está utilizando. Una vez que se sientan cómodos con los cambios, los cambios se convierten en un entorno de ensayo en el que reciben más pruebas. Finalmente, los cambios se publican en el sitio web de producción que ven los usuarios. Los conjuntos de datos admiten este patrón de promoción.

Si admite aplicaciones basadas en Platform como Real-Time CDP, Journey Optimizer o Customer Journey Analytics, se deben crear conjuntos de datos adicionales en los entornos limitados de Platform independientes que se correspondan con estos entornos.

Si no es cliente de Platform, puede crear varios conjuntos de datos en un solo simulador de pruebas y utilizar la función de copia del conjunto de datos para duplicar la configuración.

El servidor está totalmente configurado para recibir datos de la página web.

[Siguiente: ](../configure-the-client/whats-a-data-layer.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
