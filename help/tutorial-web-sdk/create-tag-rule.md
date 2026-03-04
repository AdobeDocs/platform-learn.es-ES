---
title: Creación de reglas de etiquetas para Platform Web SDK
description: Obtenga información sobre cómo enviar un evento a Platform Edge Network mediante reglas de etiquetas. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
jira: KT-15403
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: d15ce3b51424dba51b5b621b6d92eff85edd5b27
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 1%

---

# Creación de reglas de etiquetas

Obtenga información sobre cómo enviar eventos al Edge Network de Adobe Experience Platform mediante reglas de etiquetas. Una regla de etiqueta es una combinación de eventos, condiciones y acciones que indica a la propiedad de etiqueta que haga algo. Con Platform Web SDK, las reglas se utilizan para enviar eventos a Platform Edge Network con los datos adecuados.



## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Utilice una convención de nombres para administrar reglas dentro de las etiquetas
* Envío de un evento con campos XDM mediante las acciones Actualizar variable y Enviar evento
* Apilar varios conjuntos de campos XDM en varias reglas
* Asignar elementos de datos de matriz individuales o completos al objeto XDM
* Publicación de una regla de etiqueta en una biblioteca de desarrollo


## Requisitos previos

Está familiarizado con las etiquetas de recopilación de datos y con el [sitio de demostración de Luma](https://luma.enablementadobe.com), y ha completado las lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Instalar extensión de SDK web](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)
* [Captura de identidades](create-identities.md)

## Convenciones de nomenclatura

Para administrar reglas en etiquetas, se recomienda seguir una convención de nombres estándar. Este tutorial utiliza una convención de nombres de cuatro partes:

* [**ubicación**] - [**evento**] - [**propósito**] - [**pedido**]

donde;

1. **ubicación** es la página o páginas del sitio donde se activa la regla
1. **event** es el déclencheur de la regla
1. **propósito** es la acción principal realizada por la regla
1. **order** es el orden en el que la regla debe activarse en relación con otras reglas que comparten el mismo evento
<!-- minor update -->

## Añadir la extensión de capa de datos del cliente Adobe

El sitio web de Luma utiliza una capa de datos impulsada por evento denominada capa de datos del cliente de Adobe (ACDL). Cada vez que se produce un evento de capa de datos, se inserta en la matriz `adobeDataLayer`. Este tutorial utiliza una extensión de etiquetas denominada Capa de datos del cliente de Adobe para aprovechar convenientemente estos eventos para construir nuestras reglas.

Para añadir la extensión:

1. Ir a **[!UICONTROL Extensiones]**
1. Filtrar a **[!UICONTROL capa de datos del cliente de Adobe]**
1. Seleccionar **[!UICONTROL Instalar]**

   ![Agregar extensión de capa de datos del cliente de Adobe](assets/rules-acdl-extension.png)

1. Mantener la configuración predeterminada
1. Seleccionar **[!UICONTROL Guardar]**

>[!NOTE]
>
> No es necesario utilizar la capa de datos del cliente de Adobe para implementar Experience Platform Web SDK. Muchos otros tipos de eventos se utilizan normalmente en implementaciones de etiquetas (Library Loaded, DOM Ready, Window Loaded, etc.) para activar reglas.

## Creación de reglas de etiquetas

En las etiquetas, las reglas se utilizan para ejecutar acciones como configurar variables y activar llamadas de red bajo diversas condiciones. La extensión de etiquetas Experience Platform Web SDK incluye dos acciones que se utilizan en las reglas:

* **[!UICONTROL Variable de actualización]** asigna elementos de datos a sus variables de datos o XDM
* **[!UICONTROL Enviar evento]** realiza la llamada de red para enviar datos a Experience Platform Edge Network

En el resto de esta lección:

1. Utilice la acción **[!UICONTROL Actualizar variable]** para definir una &quot;configuración global&quot; de los campos XDM.

1. Use de nuevo la acción **[!UICONTROL Actualizar variable]** para anular la &quot;configuración global&quot; y contribuir con campos XDM adicionales en ciertas condiciones (por ejemplo, al agregar detalles del producto en páginas de productos).

1. Use la acción **[!UICONTROL Enviar evento]** para enviar los datos a Adobe Experience Platform Edge Network.

Todas estas reglas se secuenciarán correctamente usando la opción &quot;[!UICONTROL order]&quot;.

Este vídeo ofrece información general del proceso:

>[!VIDEO](https://video.tv.adobe.com/v/3427710/?learn=on&enablevpops)

### Campos de configuración global

Para crear una regla de etiqueta para los campos XDM globales:

1. Abra la propiedad de etiqueta que está utilizando para este tutorial.

1. Vaya a **[!UICONTROL Reglas]** en el panel de navegación izquierdo

1. Seleccione el botón **[!UICONTROL Crear nueva regla]**

   ![Crear una regla](assets/rules-create.png)

1. Asigne un nombre a la regla `all pages - adobeDataLayer push - set global variables - 1`.

1. En la sección **[!UICONTROL Eventos]**, seleccione **[!UICONTROL Agregar]**

   ![Asigne un nombre a la regla y agregue un evento](assets/rule-name-new.png)

1. Utilice la extensión **[!UICONTROL Adobe Client Data Layer]** y seleccione **[!UICONTROL Datos insertados]** como **[!UICONTROL Tipo de evento]**

1. Seleccione el menú desplegable **[!UICONTROL Avanzado]** e introduzca `1` como **[!UICONTROL Pedido]**

   >[!NOTE]
   >
   > Cuanto más bajo sea el número de pedido, más pronto se ejecutará. Por lo tanto, le damos a nuestra &quot;configuración global&quot; un número de pedido bajo.

1. Escuchar **[!UICONTROL Todos los eventos]**
1. Seleccione **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal
   ![Seleccionar Déclencheur de biblioteca cargado](assets/create-tag-rule-trigger-loaded.png)

1. En la sección **[!UICONTROL Acciones]**, seleccione **[!UICONTROL Agregar]**

1. Como la **[!UICONTROL extensión]**, seleccione **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Como **[!UICONTROL Tipo de acción]**, seleccione **[!UICONTROL Actualizar variable]**

1. Como **[!UICONTROL elemento de datos]**, seleccione `XDM Variable` que creó en la lección [Crear elementos de datos](create-data-elements.md)

   ![Actualizar esquema de variable](assets/create-rule-update-variable.png)

1. Ahora, especifique los campos XDM asignándolos a los valores adecuados:

   | Campo XDM | Mapa a |
   |---|---|
   | `eventType` | `Web Webpagedetails Page Views` (empiece a escribir para ver los valores sugeridos) |
   | `identityMap` | `Identity Map` elemento de datos |
   | `web.webPageDetails.name` | `Page Name` elemento de datos |
   | `web.webPageDetails.pageViews.value` | `1` |


   >[!TIP]
   >
   > Los campos XDM no se incluirán en la solicitud de red si el elemento de datos es nulo. Por lo tanto, cuando el usuario no está autenticado y el elemento de datos `Identity Map` es nulo, no se enviará el objeto `identityMap`. Por eso podemos definirlo con seguridad en nuestra &quot;configuración global&quot;.

   >[!TIP]
   >
   > La configuración `web.webPageDetails.pageViews.value` proporciona una forma estándar de indicar una vista de página para otras aplicaciones de flujo descendente. No es necesario que Adobe Analytics procese una llamada de red como una vista de página.

1. Cuando haya terminado, su `XDM Variable` tendrá este aspecto. Observe cómo los campos rellenados y parcialmente rellenados se indican con los círculos azules:
   ![Variable XDM](assets/rule-xdm-variable.png)
1. Seleccione **[!UICONTROL Conservar cambios]** y luego **[!UICONTROL Guardar]** la regla



### Campos de página de producto

Ahora, empiece a usar **[!UICONTROL Actualizar variable]** en reglas adicionales secuenciadas para enriquecer el objeto XDM antes de enviarlo a [!UICONTROL Platform Edge Network].

>[!TIP]
>
>El orden de las reglas determina qué regla se ejecuta primero cuando se activa un evento. Si dos reglas tienen el mismo tipo de evento, se ejecuta primero la regla con el número de orden más bajo.
> 

Comience por rastrear las vistas de productos en la página de detalles del producto de Luma:

1. Seleccionar **[!UICONTROL Agregar regla]**
1. Asigne un nombre [!UICONTROL `product detail pages - adobeDataLayer push - set product details variables - 20`]
1. Seleccione el ![+ símbolo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en Evento para agregar un nuevo déclencheur
1. En **[!UICONTROL Extensión]**, seleccione **[!UICONTROL Capa de datos del cliente de Adobe]**
1. En **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL Datos insertados]**
1. Seleccione para abrir **[!UICONTROL Opciones avanzadas]**, escriba `20`. Este valor de orden garantiza que la regla se ejecute _después de_ la regla de variables globales.
1. Escuchar un **[!UICONTROL evento específico]**
1. Escriba `productView` como **[!UICONTROL evento/clave para registrarse en]**
1. Seleccionar **[!UICONTROL Conservar cambios]**

   ![Reglas XDM de Analytics](assets/rule-pdp-event.png)


1. En **[!UICONTROL Acciones]**, seleccione **[!UICONTROL Agregar]**
1. Seleccione la extensión **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleccione **[!UICONTROL Tipo de acción]** como **[!UICONTROL variable de actualización]**
1. Seleccione `XDM Variable` como **[!UICONTROL elemento de datos]**
1. Asigne estos campos XDM a los valores adecuados:

   | Campo XDM | Mapa a |
   |---|---|
   | `eventType` | `Commerce Product Views` (empiece a escribir para ver los valores sugeridos) |
   | `commerce.productViews.value` | `1` |
   | `productListItems.name` | `Ecommerce Product Name` elemento de datos (seleccione **[!UICONTROL Proporcionar elementos individuales]** y **[!UICONTROL Agregar elemento]** primero ) |
   | `productListItems.sku` | `Ecommerce Product Id` elemento de datos |

1. Seleccionar **[!UICONTROL Conservar cambios]**

1. Seleccione **[!UICONTROL Guardar]** para guardar la regla

   >[!NOTE]
   >
   >Debido a que esta regla tiene un orden superior, sobrescribirá el conjunto `eventType` en la regla de &quot;configuración global&quot;. `eventType` solo puede contener un valor y se recomienda configurarlo con el evento más valioso.

   >[!TIP]
   >
   >La configuración de commerce.productViews.value=1 en XDM se asigna automáticamente al evento `prodView` en Analytics


### Campos del carro de compras

Puede asignar toda la matriz a un objeto XDM, siempre que la matriz coincida con el formato del esquema XDM. El elemento de datos de código personalizado `Ecommerce Cart Products` que creó anteriormente recorre el objeto de capa de datos `adobeDataLayer.ecommerce.cart.items` del sitio web de Luma y lo traduce al formato requerido del objeto `productListItems` del esquema XDM.

Para ilustrarlo, consulte la comparación a continuación de la capa de datos del sitio de Luma (izquierda) con el elemento de datos traducido (derecha):

![Formato de matriz de objeto XDM](assets/data-element-xdm-array.png)


Comparar el elemento de datos con la estructura de `productListItems` (sugerencia, debe coincidir).

>[!NOTE]
>
> No podrá ejecutar `_satellite.getVar('Ecommerce Cart Products')` en este punto del tutorial.

>[!IMPORTANT]
>
>Al asignar campos de la capa de datos al XDM, asegúrese de que los campos coincidan con el tipo de datos del campo XDM. En el ejemplo anterior `quantity` y `priceTotal` deben ser enteros, de lo contrario el registro no se introducirá en Platform.
> ![Tipo de datos de esquema XDM &#x200B;](assets/set-up-analytics-quantity-integer.png)

Ahora, asignemos la matriz al objeto XDM:


1. Cree una nueva regla con el nombre `cart page - adobeDataLayer push - set cart variables - 20`
1. Seleccione el ![+ símbolo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en Evento para agregar un nuevo déclencheur
1. En **[!UICONTROL Extensión]**, seleccione **[!UICONTROL Capa de datos del cliente de Adobe]**
1. En **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL Datos insertados]**
1. Seleccione para abrir **[!UICONTROL Opciones avanzadas]**, escriba `20`. Este valor de orden garantiza que la regla se ejecute _después de_ la regla de variables globales.
1. Escuchar un **[!UICONTROL evento específico]**
1. Escriba `cartView` como **[!UICONTROL evento/clave para registrarse en]**
1. Seleccionar **[!UICONTROL Conservar cambios]**


   ![Evento para la regla del carro de compras](assets/rule-cart-event.png)

1. En **[!UICONTROL Acciones]**, seleccione **[!UICONTROL Agregar]**
1. Seleccione la extensión **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleccione **[!UICONTROL Tipo de acción]** como **[!UICONTROL variable de actualización]**
1. Seleccione `XDM Variable` como **[!UICONTROL elemento de datos]**
1. Asigne estos campos XDM a los valores adecuados:

   | Campo XDM | Mapa a |
   |---|---|
   | `eventType` | `Commerce Product List (Cart) Views` (empiece a escribir para ver los valores sugeridos) |
   | `commerce.productListViews.value` | `1` |
   | `productListItems` | `Ecommerce Cart Products` elemento de datos (seleccione **[!UICONTROL Proporcionar toda la matriz]** primero ) |

   >[!TIP]
   >
   >La configuración de commerce.productListViews.value=1 en XDM se asigna automáticamente al evento `scView` en Analytics

1. Seleccionar **[!UICONTROL Conservar cambios]**

1. Seleccione **[!UICONTROL Guardar]** para guardar la regla


### Campos de confirmación de pedido

Cree otra regla para los eventos de compra:

1. Cree una nueva regla con el nombre `order confirmation - adobeDataLayer push - set purchase variables -  20`
1. Seleccione el ![+ símbolo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en Evento para agregar un nuevo déclencheur
1. En **[!UICONTROL Extensión]**, seleccione **[!UICONTROL Capa de datos del cliente de Adobe]**
1. En **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL Datos insertados]**
1. Seleccione para abrir **[!UICONTROL Opciones avanzadas]**, escriba `20`. Este valor de orden garantiza que la regla se ejecute _después de_ la regla de variables globales.
1. Escuchar un **[!UICONTROL evento específico]**
1. Escriba `purchase` como **[!UICONTROL evento/clave para registrarse en]**
1. Seleccionar **[!UICONTROL Conservar cambios]**
1. En **[!UICONTROL Acciones]**, seleccione **[!UICONTROL Agregar]**
1. Seleccione la extensión **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleccione **[!UICONTROL Tipo de acción]** como **[!UICONTROL variable de actualización]**
1. Seleccione `XDM Variable` como **[!UICONTROL elemento de datos]**
1. Asigne estos campos XDM a los valores adecuados:

   | Campo XDM | Mapa a |
   |---|---|
   | `eventType` | `Commerce Purchases` (empiece a escribir para ver los valores sugeridos) |
   | `commerce.productListViews.value` | `1` |
   | `commerce.order.purchaseID` | `Ecommerce Purchase Id` elemento de datos |
   | `commerce.order.currencyCode` | `USD` |
   | `productListItems` | `Ecommerce Cart Products` elemento de datos (seleccione **[!UICONTROL Proporcionar toda la matriz]** primero ) |

   >[!TIP]
   >
   >Si se establece `commerce.productListViews.value` en `1`, `commerce.order.purchaseID` y `commerce.order.currencyCode` en XDM, se asignará automáticamente a las variables `purchase`, `s.purchaseID` y `s.currencyCode` en Analytics, respectivamente.


1. Seleccionar **[!UICONTROL Conservar cambios]**
1. Seleccionar **[!UICONTROL Guardar]**


### Enviar regla de evento

Ahora que ha establecido las variables, puede crear la regla para enviar el objeto XDM completo a Platform Edge Network con la acción **[!UICONTROL Enviar evento]**.


1. Cree una nueva regla con el nombre `all pages - adobeDataLayer push - send event - 50`
1. Seleccione el ![+ símbolo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en Evento para agregar un nuevo déclencheur
1. En **[!UICONTROL Extensión]**, seleccione **[!UICONTROL Capa de datos del cliente de Adobe]**
1. En **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL Datos insertados]**
1. Seleccione para abrir **[!UICONTROL Opciones avanzadas]**, escriba `50` (que es probablemente el valor predeterminado). Este valor de orden garantiza que la regla se ejecute _después de_ las reglas de configuración de variables.
1. Escuchar **[!UICONTROL Todos los eventos]**
1. Seleccionar **[!UICONTROL Conservar cambios]**
1. En **[!UICONTROL Acciones]**, seleccione **[!UICONTROL Agregar]**
1. Seleccione la extensión **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleccione **[!UICONTROL Tipo de acción]** como **[!UICONTROL Enviar variable de evento]**



1. Como **[!UICONTROL Tipo de acción]**, seleccione **[!UICONTROL Enviar evento]**

1. Como **[!UICONTROL XDM]**, seleccione el elemento de datos `XDM Variable` creado en la lección anterior

1. Seleccione **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal

   ![Agregar la acción Enviar evento](assets/create-rule-send-event-action.png)
1. Seleccione **[!UICONTROL Guardar]** para guardar la regla

   ![Guarde la regla](assets/create-rule-save-rule.png)

Debe tener las siguientes reglas en la propiedad:

    ![Comprobar lista de reglas](assets/create-rule-list-of-rules.png)

## Publicación de las reglas en una biblioteca

A continuación, publique la regla en el entorno de desarrollo para poder verificar si funciona.

Para crear una biblioteca:

1. Vaya a **[!UICONTROL Flujo de publicación]** en el panel de navegación izquierdo

1. Seleccionar **[!UICONTROL Agregar biblioteca]**

   ![Seleccionar Agregar biblioteca](assets/rule-publish-library.png)
1. Para **[!UICONTROL Name]**, escriba `Luma Web SDK Tutorial`
1. Para el **[!UICONTROL entorno]**, seleccione `Development`
1. Seleccionar **[!UICONTROL Añadir todos los recursos modificados]**

   >[!NOTE]
   >
   >    Debería ver todos los componentes de etiquetas creados en lecciones anteriores. La extensión Core contiene la JavaScript base requerida por todas las propiedades de etiquetas web.

1. Seleccione **[!UICONTROL Guardar y generar para desarrollo]**

   ![Crear y compilar la biblioteca](assets/create-tag-rule-library-changes.png)

La biblioteca puede tardar unos minutos en crearse y, cuando se completa, muestra un punto verde a la izquierda del nombre de la biblioteca:

![Compilación completa](assets/create-rule-development-success.png)

Como puede ver en la pantalla [!UICONTROL Flujo de publicación], hay mucho más en el proceso de publicación, que está fuera del ámbito de este tutorial. Este tutorial solo utiliza una biblioteca en el entorno de desarrollo.

Ahora está listo para validar los datos de la solicitud mediante Adobe Experience Platform Debugger.

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Web SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848?profile.language=es)
