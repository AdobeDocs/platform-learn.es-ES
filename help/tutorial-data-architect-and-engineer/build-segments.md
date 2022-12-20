---
title: Generación de segmentos
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Generación de segmentos
description: En esta lección, generaremos algunos segmentos basados en los datos de perfil que hemos introducido en las lecciones anteriores.
role: Data Architect
feature: Data Governance
kt: 4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# Generación de segmentos

<!-- 30 min-->
En esta lección, generaremos algunos segmentos basados en los datos de perfil que ingerimos en las lecciones anteriores.

Una vez que tenga Perfiles de cliente en tiempo real, puede crear segmentos de individuos que compartan características similares y que puedan responder de manera similar a las estrategias de marketing. Los componentes básicos de estos segmentos son los campos XDM que creó anteriormente.

**Arquitectos de datos** necesitará crear segmentos fuera de este tutorial y admitir a sus colegas con esta tarea.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre la creación de segmentos:
>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)


## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) Para completar esta lección, debe configurar todos los controles de acceso necesarios:

* Elementos de permiso **[!UICONTROL Administración de perfiles]** > **[!UICONTROL Administrar segmentos]**, **[!UICONTROL Ver segmentos]** y **[!UICONTROL Exportar segmento de audiencia]**
* Elementos de permiso **[!UICONTROL Administración de perfiles]** > **[!UICONTROL Ver perfiles]** y **[!UICONTROL Administrar perfiles]**
* Elemento de permiso **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* Acceso de rol de usuario a la variable `Luma Tutorial Platform` perfil de producto
* Acceso de rol de desarrollador a la variable `Luma Tutorial Platform` perfil de producto (para API)

## Crear un segmento básico

Vamos a crear un segmento simple para los clientes de programas de fidelidad con un estado oro o platino

1. En la interfaz de usuario de Platform, vaya a **[!UICONTROL Segmentos]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Crear segmento]** botón
1. A la izquierda del generador de esquemas hay tres fichas para Atributos (Datos de registro), Eventos (Datos de series temporales) y Audiencias
1. Seleccione el icono de engranaje para observar cómo el generador de segmentos toma como valor predeterminado mostrar solo los campos con datos y le permite cambiar la política de combinación
1. En la pestaña Atributos , vaya a la **Perfil individual XDM > Fidelidad** carpeta (también puede buscar &quot;lealtad&quot;)
1. Arrastrar y soltar, `Tier` desde el menú de campos de atributo al lienzo del generador de segmentos
1. Select `Tier` es igual que `Gold` o `Platinum`
1. Select **[!UICONTROL Actualizar estimación]** para ver cuántos perfiles cumplen los requisitos para su segmento
1. Como **[!UICONTROL Nombre]**, introduzca `Luma customers with level Gold or Above`
1. Seleccione **[!UICONTROL Guardar]**
   ![Segmento](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Creación de un segmento dinámico

En este ejercicio, crearemos un segmento para los clientes que hayan comprado el mismo producto dos veces en un plazo de 30 días. Los segmentos dinámicos le permiten escalar la segmentación mediante el uso de campos como variables.

1. Vaya a **[!UICONTROL Segmentos]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Crear segmento]** botón
1. Seleccione el **[!UICONTROL Eventos]** ficha
1. Filtre la lista a `purchases`
1. Arrastre el **[!UICONTROL Compras]** tipo de evento en el lienzo _dos veces separadas_
1. Seleccione el icono del reloj entre las dos **[!UICONTROL Compras]** y elija &quot;en un plazo de 30 días&quot;
1. Confirme que su definición de segmento en este punto dice **&quot;Incluya la audiencia que tenga al menos 1 evento de compras y, en un plazo de 30 días, tenga al menos 1 evento de compras&quot;**

   ![Dos compras en un plazo de 30 días](assets/segment-twoPurchases.png)
1. Ahora cambie el filtro de evento a `sku`
1. Arrastre el campo SKU al segundo evento de compra
   ![Dos compras en un plazo de 30 días con SKU](assets/segment-twoPurchases-addSku.png)
1. Ahora borre el filtro de eventos
1. Debería ver en el **[!UICONTROL Examinar variables]** , hay carpetas para los dos eventos de compra. Haga clic para explorar **[!UICONTROL Compras 1]**\
   ![Dos compras en un plazo de 30 días con SKU, examine la primera compra](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Desplácese hacia abajo hasta el **[!UICONTROL Elementos de la lista de productos]** carpeta, seleccione **[!UICONTROL SKU]** y arrástrela a la derecha del **[!UICONTROL es igual que]** operando. Cuando pase el ratón por encima del área, suéltela en la sección &quot;Agregar para comparar operandos&quot;
1. Asigne un nombre al segmento `Bought same product within 30 days`
1. Confirme que su definición de audiencia sea **&quot;Incluya la audiencia que tenga al menos 1 evento de compras y, en un plazo de 30 días, tenga al menos 1 evento de compras donde (SKU igual a compras1 SKU)&quot;**
1. Seleccione el botón **[!UICONTROL Guardar]**

   ![Compró el mismo producto en el segmento de los últimos 30 días](assets/segment-boughtSameProduct.png)

## Generar un segmento de varias entidades

Recuerde cómo creamos la relación entre las variables `Luma Offline Purchase Events Schema` y `Luma Product Catalog Schema` en lecciones anteriores? Lo hicimos para poder usar la relación en nuestro esquema mediante la segmentación multientidad.

Con la función avanzada de segmentación multientidad, puede crear segmentos utilizando varias clases XDM para ampliar los esquemas. Como resultado, el generador de segmentos puede acceder a campos adicionales como si fueran nativos del almacén de datos de perfil

Creará el siguiente segmento aplicando la relación que creó entre sus `Luma Product Catalog Schema` y `Luma Offline Purchase Events Schema`.

1. Vaya a **[!UICONTROL Segmentos]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Crear segmento]** botón
1. Seleccione el **[!UICONTROL Eventos]** ficha
1. Filtre la lista a `purchases`
1. Arrastre el **[!UICONTROL Compras]** tipo de evento en el lienzo
1. Seleccione el menú desplegable del reloj situado encima del evento y elija **[!UICONTROL en los últimos 30 días]**
1. Filtre el **[!UICONTROL Eventos]** a `category` y, a continuación, arrastre el **[!UICONTROL Categoría del producto]** field to **[!UICONTROL Compras]**
1. Cambie el operador a **[!UICONTROL comienza con]** y escriba `men` en el cuadro de texto
1. Como **[!UICONTROL Nombre]**, introduzca `Purchased a Men's product in the last 30 days`
1. Confirmar la definición de la audiencia `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Seleccione el botón **[!UICONTROL Guardar]**

   ![Compró el mismo producto en el segmento de los últimos 30 días](assets/segment-purchasedMens.png)

## Segmentación por lotes y flujos

Haga clic en **[!UICONTROL Segmentos]** en la navegación de la izquierda y dediquemos un momento a revisar nuestros tres segmentos:

* Dos de nuestros segmentos son segmentos por lotes y uno es un segmento de flujo continuo.
* La plataforma establece de forma predeterminada la segmentación de flujo continuo siempre que sea posible, lo que califica al cliente para un segmento en cuanto cumpla los criterios. Cuando las definiciones de segmentos son demasiado complejas para la transmisión por secuencias, se convierten automáticamente en lotes. En este caso, los dos segmentos tomaron el valor predeterminado por lotes porque la ventana retrospectiva de los eventos de compra fue buena a siete días. Para obtener una lista completa y actual de las limitaciones de flujo continuo, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* Los trabajos por lotes se ejecutan en un programa diario, que se puede desactivar.

![Compró el mismo producto en el segmento de los últimos 30 días](assets/segment-review.png)

## Recursos adicionales

* [Documentación del servicio de segmentación](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [Referencia de la API del servicio de segmentación](https://www.adobe.io/experience-platform-apis/references/segmentation/)

Hay más en la segmentación, especialmente al activar segmentos. Estos temas se tratarán en otro tutorial.

¡Lo has hecho a través de todos los ejercicios! Continúe con el [Conclusión](conclusion.md).
