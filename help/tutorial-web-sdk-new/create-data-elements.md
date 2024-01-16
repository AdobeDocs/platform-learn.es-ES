---
title: Creación de elementos de datos
description: Obtenga información sobre cómo crear un objeto XDM y asignarle elementos de datos en etiquetas. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 1%

---

# Creación de elementos de datos

Obtenga información sobre cómo crear los elementos de datos esenciales necesarios para capturar datos con el SDK web de Experience Platform. Recopilar datos de contenido e identidad en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Aprenda a utilizar el esquema XDM creado anteriormente para recopilar datos mediante el tipo de elemento de datos del SDK web de Platform denominado Variable.

>[!NOTE]
>
> Para fines de demostración, los ejercicios de esta lección se basan en el ejemplo utilizado durante [Configuración de un esquema](configure-schemas.md) paso; creación de objetos XDM de ejemplo que capturan el contenido visualizado y las identidades de los usuarios en la [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>Los datos de esta lección provienen de `[!UICONTROL digitalData]` en el sitio de Luma. Para ver la capa de datos, abra la consola de desarrollador y escriba `[!UICONTROL digitalData]` para ver la capa de datos completa disponible.![capa de datos digitalData](assets/data-element-data-layer.png)


Independientemente del SDK web de Platform, debe seguir creando elementos de datos dentro de la propiedad de etiquetas que se asignen a variables de recopilación de datos de su sitio web, como una capa de datos, un atributo de HTML, etc. Una vez creados esos elementos de datos, debe asignarlos al esquema XDM creado durante la [configuración de esquemas](configure-schemas.md) lección. Por lo tanto, la creación de elementos de datos consta de dos acciones:

1. Asignación de variables de sitio web a elementos de datos y
1. Asignación de esos elementos de datos a un objeto XDM

Para el paso 1, siga asignando la capa de datos a los elementos de datos del modo en que lo hace actualmente, utilizando cualquiera de los tipos de elementos de datos de la extensión de etiqueta principal. Para el paso 2, la extensión del SDK web de Platform tiene disponibles los siguientes tipos de elementos de datos:

* ID de combinación de eventos
* Mapa de identidad
* Variable
* Objeto XDM

Esta lección se centra en el tipo de elemento de datos Variable. Puede crear un elemento de datos para capturar la actividad de los visitantes de Luma en función de la capa de datos disponible en el sitio de Luma. En la siguiente lección, aprenderá sobre el mapa de identidad.

>[!NOTE]
>
> Los tipos de elementos de datos ID de combinación de eventos y objeto XDM rara vez se utilizan en casos puntuales.

## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Comprender diferentes enfoques para asignar una capa de datos a XDM
* Crear elementos de datos para capturar datos de contenido
* Asignar elementos de datos a un elemento de datos de objeto XDM


## Requisitos previos

Comprenderá qué es una capa de datos y se familiarizará con el [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} capa de datos y cómo hacer referencia a elementos de datos en etiquetas. Debe haber completado los siguientes pasos anteriores en el tutorial.

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)

>[!IMPORTANT]
>
>El [Extensión del servicio de ID de Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) no es necesaria al implementar el SDK web de Adobe Experience Platform, ya que la funcionalidad del servicio de ID está integrada en el SDK web de Platform.

## Enfoques de capa de datos

Existen varias formas de asignar datos de la capa de datos al XDM mediante la funcionalidad de etiquetas de Adobe Experience Platform. A continuación se presentan algunas ventajas y desventajas de tres enfoques diferentes:

* [Implementación de XDM en la capa de datos](create-data-elements.md#implement-xdm-in-the-data-layer)
* [Asignar a XDM en el conjunto de datos](create-data-elements.md#map-to-xdm-in-the-datastream)
* [Asignación a XDM en etiquetas](create-data-elements.md#map-data-layer-in-tags)

>[!NOTE]
>
>Los ejemplos de este tutorial siguen el método Asignar a XDM en etiquetas.


### Implementación de XDM en la capa de datos

Este método implica utilizar el objeto XDM completamente definido como estructura para la capa de datos. A continuación, asigne toda la capa de datos a un elemento de datos de objeto XDM en Etiquetas de Adobe. Si la implementación no utiliza un administrador de etiquetas, este método puede ser ideal porque puede enviar datos a XDM directamente desde la aplicación utilizando [Comando sendEvent de XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#sending-xdm-data). Si utiliza etiquetas de Adobe, puede crear un elemento de datos de código personalizado que capture toda la capa de datos como un objeto JSON de paso al XDM. A continuación, asigne el JSON de paso a través al campo de objeto XDM en la acción Enviar evento.

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

* Omite los pasos para asignar variables de capa de datos individuales al XDM
* Puede ser más rápido de implementar si su equipo de desarrollo posee un comportamiento digital de etiquetado

Contras

* Dependencia total del equipo de desarrollo y el ciclo de desarrollo para actualizar qué datos se transfieren a XDM
* Flexibilidad limitada, ya que XDM recibe la carga útil exacta de la capa de datos
* No se pueden utilizar las funciones integradas de etiquetas, como raspado, persistencia o características para implementaciones rápidas
* No se puede usar la capa de datos para píxeles de terceros
* No es posible transformar los datos entre la capa de datos y XDM

### Asignar a XDM en el conjunto de datos

Este método utiliza la funcionalidad integrada en la configuración de flujo de datos denominada [Preparación de datos para la recopilación de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html) y omite la asignación de variables de capa de datos a XDM en etiquetas.

Pros

* Flexible, ya que puede asignar variables individuales al XDM
* Capacidad para [calcular nuevos valores](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html?lang=es) o [transformar tipos de datos](https://experienceleague.adobe.com/docs/experience-platform/data-prep/data-handling.html) de una capa de datos antes de pasar a XDM
* Aproveche una [IU de asignación](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html#create-mapping) para asignar campos en los datos de origen a XDM con una IU de apuntar y hacer clic

Contras

* No se pueden usar variables de capa de datos como elementos de datos para píxeles de terceros del lado del cliente, pero se pueden usar con etiquetas de Adobe para el reenvío de eventos
* No se puede utilizar la funcionalidad de raspado de la función de etiquetas de Adobe Experience Platform
* La complejidad del mantenimiento aumenta si se asigna la capa de datos tanto en etiquetas como en flujos de datos

### Asignación de capas de datos en etiquetas

Este método implica la asignación de variables de capa de datos individuales U objetos de capa de datos a elementos de datos en etiquetas y, finalmente, a XDM. Este es el enfoque tradicional para la implementación mediante un sistema de administración de etiquetas.

Pros

* El enfoque más flexible, ya que puede controlar variables individuales y transformar datos antes de que llegue a XDM
* Puede utilizar déclencheur de etiquetas de Adobe y la funcionalidad de raspado para pasar datos a XDM
* Puede asignar elementos de datos a píxeles de terceros del lado del cliente

Contras

* Puede tardar más en implementarse

>[!TIP]
>
> Capa de datos de Google
> 
> Si su organización ya utiliza Google Analytics y tiene el objeto dataLayer tradicional de Google en su sitio web, puede utilizar el complemento [Extensión de capa de datos Google](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/google-data-layer/overview.html?lang=en) en Etiquetas de Adobe. Esto le permite implementar la tecnología de Adobe más rápido sin tener que solicitar asistencia a su equipo de TI. La asignación de la capa de datos de Google a XDM seguiría los mismos pasos que se describen arriba.

>[!IMPORTANT]
>
>Como se ha indicado anteriormente, los ejemplos de este tutorial siguen el enfoque Asignar a XDM en etiquetas.

## Creación de elementos de datos para capturar la capa de datos

Antes de crear el objeto XDM, cree el siguiente conjunto de elementos de datos para [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} capa de datos:

1. Ir a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Añadir elemento de datos]** (o **[!UICONTROL Crear nuevo elemento de datos]** si no hay elementos de datos existentes en la propiedad etiqueta )

   ![Crear elemento de datos](assets/data-element-create.jpg)

1. Asigne un nombre al elemento de datos `page.pageInfo.pageName`.
1. Utilice el **[!UICONTROL Variable JavaScript]** **[!UICONTROL Tipo de elemento de datos]** para señalar a un valor de la capa de datos de Luma: `digitalData.page.pageInfo.pageName`

1. Marque las casillas de **[!UICONTROL Forzar valor de minúsculas]** y **[!UICONTROL Limpiar texto]** para estandarizar el caso y eliminar espacios superfluos

1. Salir `None` como el **[!UICONTROL Duración del almacenamiento]** ya que este valor es diferente en cada página

1. Seleccionar **[!UICONTROL Guardar]**

   ![Elemento de datos Nombre de página](assets/data-element-pageName.jpg)

Cree estos cuatro elementos de datos adicionales siguiendo los mismos pasos:

* **`page.pageInfo.server`**  asignado a
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  asignado a
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  asignado a
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** asignado a
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** asignado a `digitalData.cart.orderId` (utilice esta opción durante la [Análisis de configuración](setup-analytics.md) lección)


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

<!-- There are different ways to map data elements to XDM object fields. You can map individual data elements to individual XDM fields or map data elements to entire XDM objects as long as your data element matches the exact key-value pair schema present in the XDM object. In this lesson, you will capture content data by mapping to individual fields. You will learn how to [map a data element to an entire XDM object](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) in the [Setup Analytics](setup-analytics.md) lesson. 

Create an XDM object to capture content data:

1. In the left navigation, select **[!UICONTROL Data Elements]**
1. Select **[!UICONTROL Add Data Element]**
1. **[!UICONTROL Name]** the data element **`xdm.content`**
1. As the **[!UICONTROL Extension]** select `Adobe Experience Platform Web SDK`
1. As the **[!UICONTROL Data Element Type]** select `XDM object`
1. Select the Platform **[!UICONTROL Sandbox]** in which you created the XDM schema in during the [Configure an XDM Schema](configure-schemas.md) lesson, in this example `DEVELOPMENT Mobile and Web SDK Courses`
1. As the **[!UICONTROL Schema]**, select your `Luma Web Event Data` schema:

    ![XDM object](assets/data-element-xdm.content-fields.png)

    >[!NOTE]
    >
    >The sandbox corresponds to the Experience Platform sandbox in which you created the schema. There can be multiple sandboxes available in your Experience Platform instance, so make sure to select the right one. Always work in development first, then production.

1. Scroll down until you reach the **`web`** object
1. Select to open it

    ![Web Object](assets/data-element-pageviews-xdm-object.png)


1. Map the following web XDM variables to data elements

    * **`web.webPageDetials.name`** to `%page.pageInfo.pageName%`
    * **`web.webPageDetials.server`** to `%page.pageInfo.server%`
    * **`web.webPageDetials.siteSection`** to `%page.pageInfo.hierarchie1%`

    ![XDM object](assets/data-element-xdm.content.png)

1. Next, find the `identityMap` object in the schema and select it
 
1. Map to the `identityMap.loginID` data element

1. Select **[!UICONTROL Save]**

   ![Data Collection interface](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)

-->

Al final de estos pasos, debe tener los siguientes elementos de datos creados:

| Elementos de datos de la extensión CORE | Elementos de datos del SDK web de Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |


>[!TIP]
>
>En un futuro [Creación de una regla de etiqueta](create-tag-rule.md) lección, aprenderá cómo **[!UICONTROL Variable]** elemento de datos permite apilar varias reglas en etiquetas utilizando **[!UICONTROL Actualizar tipo de acción de variable]**. A continuación, puede enviar de forma independiente el objeto XDM a Adobe Experience Platform Edge Network mediante un **[!UICONTROL Tipo de acción Enviar evento]**.

Con estos elementos de datos en su lugar, está listo para empezar a enviar datos a Platform Edge Network con una regla de etiquetas. Pero primero, aprenda a recopilar identidades con el SDK web.

[Siguiente: ](create-identities.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
