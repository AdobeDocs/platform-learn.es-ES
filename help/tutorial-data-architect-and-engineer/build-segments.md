---
title: Generación de segmentos
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Generación de segmentos
description: En esta lección, generaremos algunos segmentos basados en los datos de perfil que hemos ingerido en las lecciones anteriores.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# Generación de segmentos

<!-- 30 min-->
En esta lección, generaremos algunos segmentos basados en los datos de perfil que ingerimos en las lecciones anteriores.

Una vez que tenga Perfiles de clientes en tiempo real, puede crear segmentos de individuos que compartan características similares y que puedan responder de manera similar a las estrategias de marketing. Los componentes básicos de estos segmentos son los campos XDM que ha creado anteriormente.

**Arquitectos de datos** Necesitará crear segmentos fuera de este tutorial y ayudar a sus compañeros con esta tarea.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre la creación de segmentos:
>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)


## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) Esta lección, ha configurado todos los controles de acceso necesarios para completar esta lección, en concreto:

* Elementos de permisos **[!UICONTROL Administración de perfiles]** > **[!UICONTROL Administrar segmentos]**, **[!UICONTROL Ver segmentos]**, y **[!UICONTROL Exportar segmento de audiencia]**
* Elementos de permisos **[!UICONTROL Administración de perfiles]** > **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Administrar perfiles]**
* Elemento de permiso **[!UICONTROL Zonas protegidas]** > `Luma Tutorial`
* Acceso de función de usuario a `Luma Tutorial Platform` perfil de producto
* Acceso con función de desarrollador a `Luma Tutorial Platform` perfil de producto (para API)

## Crear un segmento básico

Vamos a crear un segmento simple para los clientes del programa de fidelidad con un estado oro o platino

1. En la interfaz de usuario de Platform, vaya a **[!UICONTROL Segmentos]** en el panel de navegación izquierdo
1. Seleccione el **[!UICONTROL Crear segmento]** botón
1. A la izquierda del generador de esquemas hay tres pestañas para Atributos (Datos de registro), Eventos (Datos de series temporales) y Audiencias
1. Seleccione el icono de engranaje para anotar cómo el generador de segmentos muestra solo los campos con datos de forma predeterminada y le permite cambiar la política de combinación
1. En la pestaña Atributos, vaya a **Perfil individual de XDM > Lealtad** carpeta (también puede buscar &quot;lealtad&quot;)
1. Arrastrar y soltar, `Tier` del menú campos de atributos al lienzo del generador de segmentos
1. Seleccionar `Tier` igual a `Gold` o `Platinum`
1. Seleccionar **[!UICONTROL Actualizar estimación]** para ver cuántos perfiles cumplen los requisitos para su segmento
1. Como el **[!UICONTROL Nombre]**, introduzca `Luma customers with level Gold or Above`
1. Seleccione **[!UICONTROL Guardar]**
   ![Segmento](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Creación de un segmento dinámico

En este ejercicio, crearemos un segmento para los clientes que hayan comprado el mismo producto dos veces en un plazo de 30 días. Los segmentos dinámicos le permiten escalar la segmentación utilizando campos como variables.

1. Ir a **[!UICONTROL Segmentos]** en el panel de navegación izquierdo
1. Seleccione el **[!UICONTROL Crear segmento]** botón
1. Seleccione el **[!UICONTROL Eventos]** pestaña
1. Filtrar la lista a `purchases`
1. Arrastre el **[!UICONTROL Compras]** tipo de evento en el lienzo _dos veces distintas_
1. Seleccione el icono de reloj entre los dos **[!UICONTROL Compras]** y elija &quot;en un plazo de 30 días&quot;
1. Confirme que su definición de segmento en este punto dice **&quot;Incluir a la audiencia que tiene al menos 1 evento de Compras y luego dentro de los 30 días tiene al menos 1 evento de Compras&quot;**
   ![Dos compras en 30 días](assets/segment-twoPurchases.png)
1. Ahora, cambie el filtro de eventos a `sku`
1. Arrastre el campo SKU al segundo evento de compra
   ![Dos compras en 30 días con SKU](assets/segment-twoPurchases-addSku.png)
1. Ahora, borre el filtro de eventos
1. Debería ver en el **[!UICONTROL Examinar variables]** , hay carpetas para los dos eventos de compra. Haga clic para explorar **[!UICONTROL Compras 1]**\
   ![Dos compras en un plazo de 30 días con SKU; busque la primera compra](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Explore en profundidad la **[!UICONTROL Elementos de lista de productos]** carpeta, seleccione la **[!UICONTROL SKU]** y arrástrelo a la derecha del campo. **[!UICONTROL igual a]** operando. Cuando esté pasando el ratón por encima del área, suéltela en la sección &quot;Agregar para comparar operandos&quot;
1. Asigne un nombre al segmento `Bought same product within 30 days`
1. Confirme que la definición de audiencia es **&quot;Incluir audiencia que tenga al menos 1 evento de compras y luego dentro de los 30 días tenga al menos 1 evento de compras donde (SKU es igual a SKU de compras1)&quot;**
1. Seleccione el botón **[!UICONTROL Guardar]**

   ![Se ha comprado el mismo producto en el segmento de los últimos 30 días](assets/segment-boughtSameProduct.png)

## Creación de un segmento de varias entidades

Recuerde cómo creamos la relación entre las `Luma Offline Purchase Events Schema` y el `Luma Product Catalog Schema` ¿en lecciones anteriores? Lo hicimos para poder usar la relación en nuestro esquema usando segmentación de varias entidades.

Con la función avanzada de segmentación de varias entidades, puede crear segmentos utilizando varias clases XDM para ampliar los esquemas. Como resultado, el generador de segmentos puede acceder a campos adicionales como si fueran nativos del almacén de datos de perfil

Creará el siguiente segmento aplicando la relación que ha creado entre sus `Luma Product Catalog Schema` y su `Luma Offline Purchase Events Schema`.

1. Ir a **[!UICONTROL Segmentos]** en el panel de navegación izquierdo
1. Seleccione el **[!UICONTROL Crear segmento]** botón
1. Seleccione el **[!UICONTROL Eventos]** pestaña
1. Filtrar la lista a `purchases`
1. Arrastre el **[!UICONTROL Compras]** tipo de evento en el lienzo
1. Seleccione el menú desplegable de reloj situado encima del evento y elija **[!UICONTROL en los últimos 30 días]**
1. Filtrar el **[!UICONTROL Eventos]** lista para `category` y luego arrastre el **[!UICONTROL Categoría de productos]** field en **[!UICONTROL Compras]**
1. Cambie el operador a **[!UICONTROL empieza por]** y escriba `men` en el cuadro de texto
1. Como el **[!UICONTROL Nombre]**, introduzca `Purchased a Men's product in the last 30 days`
1. Confirmar la definición de audiencia `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Seleccione el botón **[!UICONTROL Guardar]**

   ![Se ha comprado el mismo producto en el segmento de los últimos 30 días](assets/segment-purchasedMens.png)

## Segmentación por lotes y streaming

Haga clic en **[!UICONTROL Segmentos]** en la navegación de la izquierda y vamos a dedicar un momento a revisar nuestros tres segmentos:

* Dos de nuestros segmentos son segmentos por lotes y uno es un segmento de flujo continuo.
* Platform usa la segmentación por secuencias siempre que es posible y califica al cliente para un segmento en cuanto cumple los criterios. Cuando las definiciones de segmentos son demasiado complejas para la transmisión, se convierten automáticamente en lote. En este caso, los dos segmentos tomaron por defecto el lote porque la ventana retrospectiva de los eventos de compra era buena en más de siete días. Para ver una lista completa y actual de las limitaciones de flujo continuo, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* Los trabajos por lotes se ejecutan en una programación diaria, que se puede desactivar.

![Se ha comprado el mismo producto en el segmento de los últimos 30 días](assets/segment-review.png)

## Recursos adicionales

* [Documentación del Servicio de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Referencia de API del servicio de segmentación](https://www.adobe.io/experience-platform-apis/references/segmentation/)

La segmentación ofrece más ventajas, especialmente con la activación de segmentos. Estos temas se tratarán en otro tutorial.

¡Lo has hecho a través de todos los ejercicios! Continúe con el [conclusión](conclusion.md).
