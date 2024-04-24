---
title: Creación de elementos de datos
description: Obtenga información sobre cómo crear un objeto XDM y asignarle elementos de datos en etiquetas. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 100a6a9ac8d580b68beb7811f99abcdc0ddefd1a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 1%

---

# Creación de elementos de datos

Obtenga información sobre cómo crear elementos de datos en etiquetas para contenido, comercio y datos de identidad en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). A continuación, rellene los campos del esquema XDM con la extensión del SDK web de Platform Tipo de elemento de datos variable.

## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Comprender diferentes enfoques para asignar una capa de datos a XDM
* Creación de elementos de datos para capturar datos
* Asignación de elementos de datos a un objeto XDM


## Requisitos previos

Tiene una comprensión de lo que es una capa de datos y ha completado las lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)


>[!IMPORTANT]
>
>Los datos de esta lección provienen de `[!UICONTROL digitalData]` en el sitio de Luma. Para ver la capa de datos, abra la consola de desarrollador y escriba `[!UICONTROL digitalData]` para ver la capa de datos completa disponible.![capa de datos digitalData](assets/data-element-data-layer.png)


## Enfoques de capa de datos

Existen varias formas de asignar datos de la capa de datos al XDM mediante la funcionalidad de etiquetas de Adobe Experience Platform. A continuación se presentan algunas ventajas y desventajas de tres enfoques diferentes. Si lo desea, es posible combinar los siguientes enfoques:

1. Implementación de XDM en la capa de datos
1. Asignación a XDM en etiquetas
1. Asignar a XDM en el conjunto de datos

>[!NOTE]
>
>Los ejemplos de este tutorial siguen el método Asignar a XDM en etiquetas.


### Implementación de XDM en la capa de datos

Este método implica utilizar el objeto XDM completamente definido como estructura para la capa de datos. A continuación, asigne toda la capa de datos a un elemento de datos de objeto XDM en las etiquetas. Si la implementación no utiliza un administrador de etiquetas, este método puede ser ideal porque puede enviar datos a XDM directamente desde la aplicación utilizando [Comando sendEvent de XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#sending-xdm-data). Si utiliza etiquetas, puede crear un elemento de datos de código personalizado que capture toda la capa de datos como un objeto JSON de paso al XDM. A continuación, asigne el JSON de paso a través al campo de objeto XDM en la acción Enviar evento.

A continuación se muestra un ejemplo del aspecto que tendría la capa de datos al utilizar el formato de capa de datos del cliente de Adobe:

Ejemplo de +++XDM en la capa de datos

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://luma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

Pros

* Elimina los pasos adicionales para reasignar a variables de capa de datos a XDM
* Puede ser más rápido de implementar si su equipo de desarrollo posee un comportamiento digital de etiquetado

Contras

* Dependencia total del equipo de desarrollo y el ciclo de desarrollo para actualizar qué datos se transfieren a XDM
* Flexibilidad limitada, ya que XDM recibe la carga útil exacta de la capa de datos
* No se pueden utilizar las características de etiquetas integradas, como raspado, persistencia o características para implementaciones rápidas
* No se puede usar la capa de datos para píxeles de terceros
* No es posible transformar los datos entre la capa de datos y XDM

### Asignación de capas de datos en etiquetas

Este método implica la asignación de variables de capa de datos individuales U objetos de capa de datos a elementos de datos en etiquetas y, finalmente, a XDM. Este es el enfoque tradicional para la implementación mediante un sistema de administración de etiquetas.

#### Pros

* El enfoque más flexible, ya que puede controlar variables individuales y transformar datos antes de que llegue a XDM
* Puede utilizar déclencheur de etiquetas de Adobe y la funcionalidad de raspado para pasar datos a XDM
* Puede asignar elementos de datos a píxeles de terceros del lado del cliente

#### Contras

* Se tarda tiempo en reconstruir la capa de datos como elementos de datos


>[!TIP]
>
> Capa de datos de Google
> 
> Si su organización ya utiliza Google Analytics y tiene el objeto dataLayer tradicional de Google en su sitio web, puede utilizar el complemento [Extensión de capa de datos Google](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/google-data-layer/overview.html?lang=en) en etiquetas. Esto le permite implementar la tecnología de Adobe más rápido sin tener que solicitar asistencia a su equipo de TI. La asignación de la capa de datos de Google a XDM seguiría los mismos pasos que se describen arriba.

### Asignar a XDM en el conjunto de datos

Este método utiliza la funcionalidad integrada en la configuración de flujo de datos denominada [Preparación de datos para la recopilación de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html) y omite la asignación de variables de capa de datos a XDM en etiquetas.

#### Pros

* Flexible, ya que puede asignar variables individuales al XDM
* Capacidad para [calcular nuevos valores](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html?lang=es) o [transformar tipos de datos](https://experienceleague.adobe.com/docs/experience-platform/data-prep/data-handling.html) de una capa de datos antes de pasar a XDM
* Aproveche una [IU de asignación](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html#create-mapping) para asignar campos en los datos de origen a XDM con una IU de apuntar y hacer clic

#### Contras

* No se pueden usar variables de capa de datos como elementos de datos para píxeles de terceros del lado del cliente, pero se pueden usar con el reenvío de eventos
* No se puede utilizar la funcionalidad de raspado de la función de etiquetas de Adobe Experience Platform
* La complejidad del mantenimiento aumenta si se asigna la capa de datos tanto en etiquetas como en flujos de datos



>[!IMPORTANT]
>
>Como se ha indicado anteriormente, los ejemplos de este tutorial siguen el enfoque Asignar a XDM en etiquetas.

## Creación de elementos de datos para capturar la capa de datos

Antes de crear el objeto XDM, cree el siguiente conjunto de elementos de datos para [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} capa de datos:

1. Ir a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Añadir elemento de datos]** (o **[!UICONTROL Crear nuevo elemento de datos]** si no hay elementos de datos existentes en la propiedad etiqueta )

   ![Crear elemento de datos](assets/data-element-create.png)

1. Asigne un nombre al elemento de datos `page.pageInfo.pageName`.
1. Utilice el **[!UICONTROL Variable JavaScript]** **[!UICONTROL Tipo de elemento de datos]** para señalar a un valor de la capa de datos de Luma: `digitalData.page.pageInfo.pageName`

1. Marque las casillas de **[!UICONTROL Forzar valor de minúsculas]** y **[!UICONTROL Limpiar texto]** para estandarizar el caso y eliminar espacios superfluos

1. Salir `None` como el **[!UICONTROL Duración del almacenamiento]** ya que este valor es diferente en cada página

1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos Nombre de página](assets/data-element-pageName.png)

Cree estos elementos de datos adicionales siguiendo los mismos pasos:

* **`page.pageInfo.server`**  asignado a
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  asignado a
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  asignado a
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** asignado a
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`product.productInfo.sku`** asignado a `digitalData.product.0.productInfo.sku`
<!--digitalData.product.0.productInfo.sku
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.sku;
    });
    return cartItem;
    ```
    -->
* **`product.productInfo.title`** asignado a `digitalData.product.0.productInfo.title`
* **`cart.orderId`** asignado a `digitalData.cart.orderId`
<!--
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.title;
    });
    return cartItem;
    ```
    -->
* **`product.category`** uso del **[!UICONTROL Código personalizado]** **[!UICONTROL Tipo de elemento de datos]** y el siguiente código personalizado para analizar la dirección URL del sitio para la categoría de nivel superior:

  ```javascript
  var cat = location.pathname.split(/[/.]+/);
  if (cat[5] == 'products') {
     return (cat[6]);
  } else if (cat[5] != 'html') { 
     return (cat[5]);
  }
  ```

* **`cart.productInfo`** mediante el siguiente código personalizado:

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  cartItem.push({
  "SKU": item.sku
  });
  });
  return cartItem; 
  ```

* **`cart.productInfo.purchase`** mediante el siguiente código personalizado:

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  var qty = parseInt(item.qty);
  var price = parseInt(item.price);
  cartItem.push({
  "SKU": item.sku,
  "quantity": qty,
  "priceTotal": price
  });
  });
  return cartItem; 
  ```



>[!CAUTION]
>
>El [!UICONTROL Variable JavaScript] el tipo de elemento de datos trata las referencias de matriz como puntos en lugar de corchetes, por lo que hacer referencia al elemento de datos username como `digitalData.user[0].profile[0].attributes.username` **no funcionará**.

## Crear elemento de datos variable

Después de crear los elementos de datos, asígnelos al XDM mediante el **[!UICONTROL Variable]** elemento de datos que define el esquema utilizado para el objeto XDM. Este objeto debe ajustarse al esquema XDM creado durante la [Configuración de un esquema](configure-schemas.md) lección.

Para crear el elemento de datos Variable:

1. Seleccionar **[!UICONTROL Añadir elemento de datos]**
1. Asigne un nombre al elemento de datos `xdm.variable.content`. Se recomienda añadir el prefijo &quot;xdm&quot; a los elementos de datos específicos de XDM para organizar mejor la propiedad de etiqueta
1. Seleccione el **[!UICONTROL SDK web de Adobe Experience Platform]** como el **[!UICONTROL Extensión]**
1. Seleccione el **[!UICONTROL Variable]** como el **[!UICONTROL Tipo de elemento de datos]**
1. Seleccione el Experience Platform adecuado **[!UICONTROL Sandbox]**
1. Seleccione el adecuado **[!UICONTROL Esquema]**, en este caso `Luma Web Event Data`
1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos variable](assets/analytics-tags-data-element-xdm-variable.png)


Al final de estos pasos, debe tener los siguientes elementos de datos creados:

| Elementos de datos de la extensión principal | Elementos de datos de la extensión SDK para web de Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `xdm.variable.content` |
| `cart.productInfo` | |
| `cart.productInfo.purchase` | |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

>[!TIP]
>
>En un futuro [Creación de reglas de etiquetas](create-tag-rule.md) lección, aprenderá cómo **[!UICONTROL Variable]** elemento de datos permite apilar varias reglas en etiquetas utilizando **[!UICONTROL Actualizar tipo de acción de variable]**.

Con estos elementos de datos en su lugar, está listo para empezar a enviar datos al Edge Network de Platform con una regla de etiquetas. Pero primero, aprenda a recopilar identidades con el SDK web.

[Siguiente: ](create-identities.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
