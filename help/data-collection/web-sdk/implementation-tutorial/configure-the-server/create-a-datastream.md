---
title: Crear un flujo de datos
description: Crear un flujo de datos
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Crear un flujo de datos

Los datos que envía desde el sitio web llegan a un conjunto de servidores de Adobe llamados [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Esta red es capaz de enviar sus datos al [Conjunto de datos de Adobe Experience Platform que ha creado anteriormente](create-a-schema.md) y otros productos de Adobe Experience Cloud. Estos productos de Adobe también pueden responder con datos a su página web. Por ejemplo, Edge Network puede devolver contenido de personalización de Adobe Target.

Para configurar los productos de Adobe desde y hacia los que Edge Network envía datos, debe crear una secuencia de datos. Cuando Edge Network recibe datos de su página web, consulta la secuencia de datos que ha creado, lee su configuración y, a continuación, reenvía datos a los productos de Adobe adecuados.

Para crear una secuencia de datos, primero vaya a la [!UICONTROL Datastreams] ver en [!UICONTROL Recopilación de datos]. Clic [!UICONTROL Crear flujo de datos] en la esquina superior derecha. Proporcione un nombre para la secuencia de datos.

![Nombre y descripción de secuencia de datos](../../../assets/implementation-strategy/datastream-name-description.png)

La siguiente pantalla le permite configurar qué productos de Adobe deben recibir los datos enviados desde el sitio web. Para los fines de este tutorial, habilite solo Adobe Experience Platform y seleccione el conjunto de datos que creó anteriormente (que estará en el valor predeterminado [!UICONTROL Prod] y haga clic en [!UICONTROL Guardar].

![Configuración de producto de flujo de datos](../../../assets/implementation-strategy/datastream-product-configuration.png)

Se ha creado su conjunto de datos.

## Entornos de flujo de datos

Las empresas suelen tener una ruta de promoción para cualquier actualización de sitio web. Alguien de la compañía (un experto en marketing o un ingeniero, según los cambios) suele probar sus cambios en un entorno de desarrollo que solo usa esa persona. Una vez que se sientan cómodos con los cambios, estos se promocionan a un entorno de ensayo en el que reciben más pruebas. Finalmente, los cambios se publican en el sitio web de producción que ven los usuarios. Las secuencias de datos admiten este patrón de promoción.

Después de hacer clic en [!UICONTROL Guardar]Sin embargo, debería haber notado que se crearon automáticamente tres entornos de flujo de datos: [!UICONTROL Entorno de desarrollo], [!UICONTROL Entorno de ensayo], y [!UICONTROL Entorno de producción].

![Entornos de flujo de datos](../../../assets/implementation-strategy/datastream-environments.png)

Si hace clic en cada entorno de flujo de datos, notará que todos tienen la misma configuración que proporcionó. Sin embargo, estos entornos se pueden personalizar individualmente.

Si está familiarizado con las etiquetas de Adobe Experience Platform, es posible que ya se sienta cómodo con el concepto de entorno de desarrollo, ensayo y producción. Los entornos dentro de las etiquetas están relacionados con los entornos dentro de un conjunto de datos. A medida que mueve una biblioteca de etiquetas a través del flujo de trabajo de publicación de etiquetas desde el desarrollo, hasta el ensayo y la producción, el entorno de flujo de datos que se utiliza también cambiará automáticamente de [!UICONTROL Entorno de desarrollo], a [!UICONTROL Entorno de ensayo], a [!UICONTROL Entorno de producción]. Esto le permite, por ejemplo, enviar datos a un conjunto de datos mientras los cambios están en desarrollo y enviar datos a otro conjunto de datos una vez que los cambios están en producción. Esto puede mantener los datos de producción libres de cualquier dato de basura que pueda generar durante el proceso de desarrollo. Analizaremos los entornos de flujo de datos más adelante al configurar las extensiones en la propiedad de etiquetas.

El servidor está ahora completamente configurado para recibir datos de la página web.
