---
title: Creación de elementos de datos para Platform Web SDK
description: Obtenga información sobre cómo crear un objeto XDM y asignarle elementos de datos en etiquetas. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
jira: KT-15401
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 1feddab414a8a7e49f04b8886c275d06516d0114
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 2%

---

# Creación de elementos de datos

Aprenda a crear elementos de datos en etiquetas para datos de contenido, comercio e identidad en el [sitio de demostración de Luma](https://newluma.enablementadobe.com). A continuación, rellene los campos del esquema XDM con el tipo de elemento de datos Variable de la extensión Adobe Experience Platform Web SDK.



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
* [Extensión web SDK instalada en la propiedad tag](install-web-sdk.md)


>[!IMPORTANT]
>
>Los datos de esta lección provienen de la capa de datos `[!UICONTROL adobeDataLayer]` del sitio de Luma. Para ver la capa de datos, abra la consola de desarrollador y escriba `[!UICONTROL adobeDataLayer]` para ver la capa de datos completa disponible.![capa de datos adobeDataLayer](assets/data-element-data-layer-new.png)


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

+++Ejemplo de XDM en la capa de datos

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
            "URL":"https://newluma.enablementadobe.com/",
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

Antes de crear el objeto XDM, cree el siguiente conjunto de elementos de datos para la capa de datos [Luma demo site](https://newluma.enablementadobe.com){target="_blank"}:

1. Vaya a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Agregar elemento de datos]** (o **[!UICONTROL Crear nuevo elemento de datos]** si no hay elementos de datos existentes en la propiedad de etiqueta)

   ![Crear elemento de datos](assets/data-element-create.png)

1. Asigne un nombre al elemento de datos `Page Name`.
1. Utilice la **[!UICONTROL variable de JavaScript]** **[!UICONTROL tipo de elemento de datos]** para señalar a un valor de la capa de datos de Luma: `adobeDataLayer.0.page.name`

1. Marque las casillas de **[!UICONTROL Forzar valor en minúsculas]** y **[!UICONTROL Limpiar texto]** para estandarizar el caso y eliminar espacios superfluos

1. Deje `None` como la configuración de **[!UICONTROL Duración del almacenamiento]**, ya que este valor es diferente en cada página

1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos Page Name](assets/data-element-pageName.png)

Cree estos elementos de datos adicionales siguiendo los mismos pasos:

* **`User Id`** asignado a
  `adobeDataLayer.0.user.id`

* **`User Logged In`** asignado a
  `adobeDataLayer.0.user.loggedIn`

* **`Ecommerce Product Id`** se asignó a `adobeDataLayer.0.ecommerce.detail.products.0.id`
* **`Ecommerce Product Name`** se asignó a `adobeDataLayer.0.ecommerce.detail.products.0.name`
* **`Ecommerce Purchase Id`** se asignó a `adobeDataLayer.0.ecommerce.purchase.actionField.id`
* **`Ecommerce Product Category`** usa el **[!UICONTROL código personalizado]** **[!UICONTROL tipo de elemento de datos]** y el siguiente código personalizado:

  ```javascript
  return adobeDataLayer[0].ecommerce.detail.products[0].category+":"+adobeDataLayer[0].ecommerce.detail.products[0].subcategory;
  ```

* **`Ecommerce Cart Products`** con el siguiente código personalizado:

  ```javascript
  const cartProducts = adobeDataLayer
  .flatMap(evt => Array.isArray(evt?.ecommerce?.cart?.items) ? evt.ecommerce.cart.items : [])
  .filter(item => item && item.id && item.name && item.brand)
  .map(({ id, name, brand }) => ({ id, name, brand }));
  
  return cartProducts;
  ```

* **`Ecommerce Checkout Products`** con el siguiente código personalizado:

  ```javascript
  const checkoutProducts = adobeDataLayer
  .flatMap(evt => Array.isArray(evt?.ecommerce?.checkout?.products) ? evt.ecommerce.checkout.products : [])
  .filter(item => item && item.id && item.name && item.brand)
  .map(({ id, name, brand }) => ({ id, name, brand }));
  
  return checkoutProducts;
  ```


>[!CAUTION]
>
>El tipo de elemento de datos [!UICONTROL JavaScript variable] trata las referencias de matriz como puntos en lugar de corchetes, por lo que hacer referencia al elemento de datos de nombre de usuario como `adobeDataLayer[0].page.name` **no funcionará**.

## Creación de elementos de datos variables para XDM y objetos de datos

Los elementos de datos que acaba de crear se utilizarán para crear un objeto XDM (para aplicaciones de Platform) y un objeto de datos (para Analytics, Target y Audience Manager). Estos objetos tienen sus propios elementos de datos especiales llamados **[!UICONTROL Variable]**, que son muy fáciles de crear.

Para crear el elemento de datos Variable para XDM, vincúlelo al esquema que creó en la lección [Configurar un esquema](configure-schemas.md):

1. Seleccionar **[!UICONTROL Agregar elemento de datos]**
1. Asigne un nombre al elemento de datos `XDM Variable`. Se recomienda añadir el prefijo &quot;xdm&quot; a los elementos de datos específicos de XDM para organizar mejor la propiedad de etiqueta
1. Seleccione **[!UICONTROL Adobe Experience Platform Web SDK]** como **[!UICONTROL extensión]**
1. Seleccione la **[!UICONTROL variable]** como **[!UICONTROL tipo de elemento de datos]**
1. Seleccione **[!UICONTROL XDM]** como **[!UICONTROL propiedad]**
1. Seleccione la **[!UICONTROL zona protegida]** en la que creó el esquema
1. Seleccione el **[!UICONTROL esquema]** apropiado, en este caso `Luma Web Event Data`
1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos variable para XDM](assets/analytics-tags-data-element-xdm-variable.png)

A continuación, cree el elemento de datos Variable para el objeto de datos:

1. Seleccionar **[!UICONTROL Agregar elemento de datos]**
1. Asigne un nombre al elemento de datos `Data Variable`.
1. Seleccione **[!UICONTROL Adobe Experience Platform Web SDK]** como **[!UICONTROL extensión]**
1. Seleccione la **[!UICONTROL variable]** como **[!UICONTROL tipo de elemento de datos]**
1. Seleccione **[!UICONTROL datos]** como **[!UICONTROL propiedad]**
1. Seleccione las soluciones de Experience Cloud que desee implementar como parte de este tutorial
1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos de variable para el objeto de datos](assets/data-element-data-variable.png)


Al final de estos pasos, debe tener los siguientes elementos de datos creados:

| Elementos de datos de la extensión principal | Elementos de datos de la extensión Platform Web SDK |
-----------------------------|-------------------------------
| `Ecommerce Cart Products` | `Data Variable` |
| `Ecommerce Checkout Products` | `XDM Variable` |
| `Ecommerce Checkout Products` | |
| `Ecommerce Product Category` | |
| `Ecommerce Product Id` | |
| `Ecommerce Product Name` | |
| `Ecommerce Purchase Id` | |
| `Page Name` | |
| `User Id` | |
| `User Logged In` | |

Con estos elementos de datos en su lugar, está listo para empezar a enviar datos a Platform Edge Network con una regla de etiquetas. Pero primero, aprenda a recopilar identidades con Web SDK.

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Web SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848)
