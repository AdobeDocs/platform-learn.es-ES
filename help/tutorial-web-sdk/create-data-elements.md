---
title: Creación de elementos de datos para el SDK web de Platform
description: Obtenga información sobre cómo crear un objeto XDM y asignarle elementos de datos en etiquetas. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
jira: KT-15401
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 2%

---

# Creación de elementos de datos

Aprenda a crear elementos de datos en etiquetas para datos de contenido, comercio e identidad en el [sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). A continuación, rellene los campos del esquema XDM con la extensión del SDK web de Adobe Experience Platform Variable data element type.

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
>Los datos de esta lección provienen de la capa de datos `[!UICONTROL digitalData]` del sitio de Luma. Para ver la capa de datos, abra la consola de desarrollador y escriba `[!UICONTROL digitalData]` para ver la capa de datos completa disponible.![capa de datos digitalData](assets/data-element-data-layer.png)


## Enfoques de capa de datos

Existen varias formas de asignar datos de la capa de datos al XDM mediante la funcionalidad de etiquetas de Adobe Experience Platform. A continuación se presentan algunas ventajas y desventajas de tres enfoques diferentes. Si lo desea, es posible combinar los siguientes enfoques:

1. Implementación de XDM en la capa de datos
1. Asignación a XDM en etiquetas
1. Asignar a XDM en el conjunto de datos

>[!NOTE]
>
>Los ejemplos de este tutorial siguen el método Asignar a XDM en etiquetas.


### Implementación de XDM en la capa de datos

Este método implica utilizar el objeto XDM completamente definido como estructura para la capa de datos. A continuación, asigne toda la capa de datos a un elemento de datos de objeto XDM en las etiquetas. Si la implementación no utiliza un administrador de etiquetas, este método puede ser ideal porque puede enviar datos a XDM directamente desde la aplicación mediante el [comando XDM sendEvent](https://experienceleague.adobe.com/en/docs/experience-platform/edge/fundamentals/tracking-events#sending-xdm-data). Si utiliza etiquetas, puede crear un elemento de datos de código personalizado que capture toda la capa de datos como un objeto JSON de paso al XDM. A continuación, asigne el JSON de paso a través al campo de objeto XDM en la acción Enviar evento.

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
* Puede ser más rápido de implementar si su equipo de desarrollo web también posee el comportamiento digital de etiquetado

Contras

* Dependencia total del equipo de desarrollo y el ciclo de desarrollo para actualizar qué datos se transfieren a XDM
* Flexibilidad limitada, ya que XDM recibe la carga útil exacta de la capa de datos
* No se pueden utilizar las características de etiquetas integradas, como raspado, persistencia o características para implementaciones rápidas
* Es más difícil usar la capa de datos para píxeles de terceros (pero quizá quieras mover estos píxeles a [reenvío de eventos](setup-event-forwarding.md)!
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
> Si su organización ya utiliza Google Analytics y tiene el objeto dataLayer tradicional de Google en su sitio web, puede utilizar la [extensión de capa de datos de Google](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/google-data-layer/overview) en las etiquetas. Esto le permite implementar la tecnología de Adobe más rápido sin tener que solicitar asistencia a su equipo de TI. La asignación de la capa de datos de Google a XDM seguiría los mismos pasos que se describen arriba.

### Asignar a XDM en el conjunto de datos

Este método usa funcionalidad integrada en la configuración del flujo de datos llamada [Preparación de datos para la recopilación de datos](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/data-prep) y omite la asignación de variables de capa de datos a XDM en las etiquetas.

#### Pros

* Flexible, ya que puede asignar variables individuales al XDM
* Capacidad para [calcular nuevos valores](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/functions) o [transformar tipos de datos](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/data-handling) de una capa de datos antes de que pase a XDM
* Aproveche una [IU de asignación](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/data-prep#create-mapping) para asignar campos de los datos de origen a XDM con una IU de apuntar y hacer clic

#### Contras

* No se pueden usar variables de capa de datos como elementos de datos para píxeles de terceros del lado del cliente, pero se pueden usar con el reenvío de eventos
* No se puede utilizar la funcionalidad de raspado de la función de etiquetas de Adobe Experience Platform
* La complejidad del mantenimiento aumenta si se asigna la capa de datos tanto en etiquetas como en flujos de datos



>[!IMPORTANT]
>
>Como se ha indicado anteriormente, los ejemplos de este tutorial siguen el enfoque Asignar a XDM en etiquetas.

## Creación de elementos de datos para capturar la capa de datos

Antes de crear el objeto XDM, cree el siguiente conjunto de elementos de datos para la capa de datos [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Vaya a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Agregar elemento de datos]** (o **[!UICONTROL Crear nuevo elemento de datos]** si no hay elementos de datos existentes en la propiedad de etiqueta)

   ![Crear elemento de datos](assets/data-element-create.png)

1. Asigne un nombre al elemento de datos `page.pageInfo.pageName`.
1. Utilice la **[!UICONTROL variable de JavaScript]** **[!UICONTROL tipo de elemento de datos]** para señalar a un valor de la capa de datos de Luma: `digitalData.page.pageInfo.pageName`

1. Marque las casillas de **[!UICONTROL Forzar valor en minúsculas]** y **[!UICONTROL Limpiar texto]** para estandarizar el caso y eliminar espacios superfluos

1. Deje `None` como la configuración de **[!UICONTROL Duración del almacenamiento]**, ya que este valor es diferente en cada página

1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos Page Name](assets/data-element-pageName.png)

Cree estos elementos de datos adicionales siguiendo los mismos pasos:

* **`page.pageInfo.server`** asignado a
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`** asignado a
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`** asignado a
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** asignado a
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`product.productInfo.sku`** se asignó a `digitalData.product.0.productInfo.sku`
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
* **`product.productInfo.title`** se asignó a `digitalData.product.0.productInfo.title`
* **`cart.orderId`** se asignó a `digitalData.cart.orderId`
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
* **`product.category`** usa el **[!UICONTROL código personalizado]** **[!UICONTROL tipo de elemento de datos]** y el siguiente código personalizado para analizar la dirección URL del sitio para la categoría de nivel superior:

  ```javascript
  var cat = location.pathname.split(/[/.]+/);
  if (cat[5] == 'products') {
     return (cat[6]);
  } else if (cat[5] != 'html') { 
     return (cat[5]);
  }
  ```

* **`cart.productInfo`** con el siguiente código personalizado:

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

* **`cart.productInfo.purchase`** con el siguiente código personalizado:

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
>El tipo de elemento de datos [!UICONTROL JavaScript variable] trata las referencias de matriz como puntos en lugar de corchetes, por lo que hacer referencia al elemento de datos de nombre de usuario como `digitalData.user[0].profile[0].attributes.username` **no funcionará**.

## Creación de elementos de datos variables para XDM y objetos de datos

Los elementos de datos que acaba de crear se utilizarán para crear un objeto XDM (para aplicaciones de Platform) y un objeto de datos (para Analytics, Target y Audience Manager). Estos objetos tienen sus propios elementos de datos especiales llamados **[!UICONTROL Variable]**, que son muy fáciles de crear.

Para crear el elemento de datos Variable para XDM, vincúlelo al esquema que creó en la lección [Configurar un esquema](configure-schemas.md):

1. Seleccionar **[!UICONTROL Agregar elemento de datos]**
1. Asigne un nombre al elemento de datos `xdm.variable.content`. Se recomienda añadir el prefijo &quot;xdm&quot; a los elementos de datos específicos de XDM para organizar mejor la propiedad de etiqueta
1. Seleccione **[!UICONTROL Adobe Experience Platform Web SDK]** como **[!UICONTROL extensión]**
1. Seleccione la **[!UICONTROL variable]** como **[!UICONTROL tipo de elemento de datos]**
1. Seleccione **[!UICONTROL XDM]** como **[!UICONTROL propiedad]**
1. Seleccione la **[!UICONTROL zona protegida]** en la que creó el esquema
1. Seleccione el **[!UICONTROL esquema]** apropiado, en este caso `Luma Web Event Data`
1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos variable para XDM](assets/analytics-tags-data-element-xdm-variable.png)

A continuación, cree el elemento de datos Variable para el objeto de datos:

1. Seleccionar **[!UICONTROL Agregar elemento de datos]**
1. Asigne un nombre al elemento de datos `data.variable`. Se recomienda incluir el prefijo &quot;data&quot; en los elementos de datos específicos del objeto de datos para organizar mejor la propiedad de etiqueta
1. Seleccione **[!UICONTROL Adobe Experience Platform Web SDK]** como **[!UICONTROL extensión]**
1. Seleccione la **[!UICONTROL variable]** como **[!UICONTROL tipo de elemento de datos]**
1. Seleccione **[!UICONTROL datos]** como **[!UICONTROL propiedad]**
1. Seleccione las soluciones de Experience Cloud que desee implementar como parte de este tutorial
1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos de variable para el objeto de datos](assets/data-element-data-variable.png.png)


Al final de estos pasos, debe tener los siguientes elementos de datos creados:

| Elementos de datos de la extensión principal | Elementos de datos de la extensión SDK para web de Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `xdm.variable.content` |
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
>En una lección futura de [Crear reglas de etiquetas](create-tag-rule.md), aprenderá cómo los elementos de datos de **[!UICONTROL Variable]** le permiten apilar varias reglas en etiquetas utilizando **[!UICONTROL Actualizar tipo de acción de variable]**.

Con estos elementos de datos en su lugar, está listo para empezar a enviar datos al Edge Network de Platform con una regla de etiquetas. Pero primero, aprenda a recopilar identidades con el SDK web.

[Siguiente: ](create-identities.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
