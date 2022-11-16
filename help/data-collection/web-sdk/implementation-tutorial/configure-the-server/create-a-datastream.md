---
title: Crear un flujo de datos
description: Crear un flujo de datos
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Crear un flujo de datos

Los datos que envía desde su sitio web llegan a un conjunto de servidores de Adobe llamados [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Esta red es capaz de enviar sus datos al [Conjunto de datos de Adobe Experience Platform que creó anteriormente](create-a-schema.md) y otros productos dentro de Adobe Experience Cloud. Estos productos de Adobe también pueden responder con datos a su página web. Por ejemplo, la red perimetral puede devolver contenido de personalización de Adobe Target.

Para configurar los productos de Adobe que Edge Network envía datos a y desde, debe crear un conjunto de datos. Cuando la red perimetral recibe datos de su página web, consulta el conjunto de datos que ha creado, lee su configuración y reenvía datos a los productos de Adobe correspondientes.

Para crear un conjunto de datos, en primer lugar vaya al [!UICONTROL Datastreams] ver dentro de [!UICONTROL Recopilación de datos]. Haga clic en [!UICONTROL Crear conjunto de datos] en la esquina superior derecha. Proporcione un nombre para el conjunto de datos.

![Nombre y descripción del conjunto de datos](../../../assets/implementation-strategy/datastream-name-description.png)

La siguiente pantalla le permite configurar qué productos de Adobe deben recibir los datos enviados desde el sitio web. Para los fines de este tutorial, active solo Adobe Experience Platform, seleccione el conjunto de datos que ha creado anteriormente (que estará en el valor predeterminado [!UICONTROL Prod] entorno limitado) y haga clic en [!UICONTROL Guardar].

![Configuración del producto Datastream](../../../assets/implementation-strategy/datastream-product-configuration.png)

Se ha creado el conjunto de datos.

## Entornos de almacén de datos

Las empresas suelen tener una ruta de promoción para cualquier actualización del sitio web. Alguien de la empresa (un especialista en marketing o ingeniero, según los cambios) suele probar sus cambios en un entorno de desarrollo que solo esa persona está utilizando. Una vez que se sientan cómodos con los cambios, los cambios se convierten en un entorno de ensayo en el que reciben más pruebas. Finalmente, los cambios se publican en el sitio web de producción que ven los usuarios. Los conjuntos de datos admiten este patrón de promoción.

Después de hacer clic en [!UICONTROL Guardar], debería haber notado que se crearon automáticamente tres entornos de conjunto de datos: [!UICONTROL Entorno de desarrollo], [!UICONTROL Entorno de ensayo]y [!UICONTROL Entorno de producción].

![Entornos de almacén de datos](../../../assets/implementation-strategy/datastream-environments.png)

Si hace clic en cada entorno del conjunto de datos, verá que se les ha dado la misma configuración que usted proporcionó. Sin embargo, estos entornos se pueden personalizar individualmente.

Si está familiarizado con las etiquetas de Adobe Experience Platform, es posible que ya se sienta cómodo con el concepto de entorno de desarrollo, ensayo y producción. Los entornos dentro de Etiquetas están relacionados con entornos dentro de un conjunto de datos. A medida que mueve una biblioteca de etiquetas a través del flujo de trabajo de publicación de etiquetas desde el desarrollo, el ensayo, la producción, el entorno de flujo de datos que se utiliza cambiará automáticamente de [!UICONTROL Entorno de desarrollo], a [!UICONTROL Entorno de ensayo], a [!UICONTROL Entorno de producción]. Esto le permite, por ejemplo, enviar datos a un conjunto de datos mientras los cambios están en desarrollo y enviar datos a un conjunto de datos diferente una vez que los cambios estén en producción. Esto puede mantener los datos de producción libres de cualquier residuo que pueda generar durante el proceso de desarrollo. Más adelante analizaremos los entornos del conjunto de datos al configurar las extensiones en la propiedad de etiqueta.

El servidor está totalmente configurado para recibir datos de la página web.
