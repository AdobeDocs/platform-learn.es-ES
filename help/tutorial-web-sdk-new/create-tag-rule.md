---
title: Creación de reglas de etiquetas
description: Obtenga información sobre cómo enviar un evento a la red perimetral de Platform con el objeto XDM mediante una regla de etiqueta. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
source-git-commit: 367789cfb0800fee7d020303629f57112e52464f
workflow-type: tm+mt
source-wordcount: '2005'
ht-degree: 1%

---

# Creación de reglas de etiquetas

Obtenga información sobre cómo enviar eventos a la red perimetral de Platform con el objeto XDM mediante reglas de etiqueta. Una regla de etiqueta es una combinación de eventos, condiciones y acciones que indica a la propiedad de etiqueta que haga algo.

>[!NOTE]
>
> Para fines de demostración, los ejercicios de esta lección se basan en el ejemplo utilizado durante la [Creación de identidades](create-identities.md) paso; envío de una acción de evento de XDM para capturar contenido e identidades de usuarios en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Utilice una convención de nombres para administrar reglas dentro de las etiquetas
* Envío de un evento XDM mediante los tipos de acción Actualizar variable y Enviar evento en una regla de etiqueta
* Publicación de una regla de etiqueta en una biblioteca de desarrollo


## Requisitos previos

Está familiarizado con las etiquetas de recopilación de datos y las [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html)y debe haber completado las siguientes lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)
* [Creación de identidades](create-identities.md)

## Convenciones de nomenclatura

Para administrar mejor las reglas en las etiquetas, se recomienda seguir una convención de nombres estándar. Este tutorial utiliza una convención de nombres de tres partes:

* [**ubicación**] - [**evento**] - [**herramienta**] (**Secuencia**)

donde;

1. **ubicación** es la página o páginas del sitio donde se activa la regla
1. **evento** es el déclencheur de la regla
1. **herramienta** es la aplicación o aplicaciones específicas utilizadas en el paso de acción para esa regla
1. **Secuencia** es el orden en que la regla debe activarse en relación con otras reglas
<!-- minor update -->

## Creación de reglas de etiquetas

En las etiquetas, las reglas se utilizan para ejecutar acciones (llamadas de activación) bajo varias condiciones. La extensión de etiquetas del SDK web de Platform incluye dos acciones que se utilizarán en esta lección:

* **[!UICONTROL Actualizar variable]** asigna elementos de datos a campos XDM
* **[!UICONTROL Enviar evento]** envía el objeto XDM a Experience Platform Edge Network

Primero definimos una regla con el **[!UICONTROL Actualizar variable]** acción, que define una &quot;configuración global&quot; de campos XDM que queremos enviar en cada página del sitio (por ejemplo, el nombre de página).

A continuación, podemos definir reglas adicionales con **[!UICONTROL Actualizar variable]** acción que complementará los campos XDM globales con campos adicionales que solo están disponibles bajo ciertas condiciones (por ejemplo, añadir detalles del producto en páginas de productos).

Finalmente, utilizaremos otra regla con el **[!UICONTROL Enviar evento]** acción que enviará el objeto XDM completo a Adobe Experience Platform Edge Network.


### Actualizar reglas de variables

#### Campos globales

Para crear una regla de etiqueta para los campos XDM globales:

1. Abra la propiedad de etiqueta que está utilizando para este tutorial.

1. Ir a **[!UICONTROL Reglas]** en el panel de navegación izquierdo

1. Seleccione el **[!UICONTROL Crear nueva regla]** botón

   ![Creación de una regla](assets/rules-create.png)

1. Asigne un nombre a la regla `all pages global content variables - library loaded - AA (order 1)`.

1. En el **[!UICONTROL Eventos]** , seleccione **[!UICONTROL Añadir]**

   ![Asignar un nombre a la regla y añadir un evento](assets/rule-name-new.png)

1. Utilice el **[!UICONTROL Extensión principal]** y seleccione `Page Bottom` como el **[!UICONTROL Tipo de evento]**

1. En el **[!UICONTROL Nombre]** , asígnele un nombre `Core - Page Bottom - order 1`. Esto le ayuda a describir el déclencheur con un nombre significativo.

1. Seleccionar **[!UICONTROL Avanzadas]** desplegable e introduzca `1` in **[!UICONTROL Pedido]**

   >[!NOTE]
   >
   > Cuanto mayor sea el número introducido, más adelante en el orden general de las operaciones que déclencheur.

1. Seleccionar **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal
   ![Seleccionar Déclencheur inferior de la página](assets/create-tag-rule-trigger-bottom.png)

1. En el **[!UICONTROL Acciones]** , seleccione **[!UICONTROL Añadir]**

1. Como el **[!UICONTROL Extensión]**, seleccione **[!UICONTROL SDK web de Adobe Experience Platform]**

1. Como el **[!UICONTROL Tipo de acción]**, seleccione **[!UICONTROL Actualizar variable]**

1. Como el **[!UICONTROL Elemento de datos]**, seleccione la `xdm.variable.content` que creó en la [Creación de elementos de datos](create-data-elements.md) lección

   ![Actualizar esquema de variables](assets/create-rule-update-variable.png)

Ahora, asigne los [!UICONTROL elementos de datos] a la [!UICONTROL esquema] utilizado por el objeto XDM.

>[!NOTE]
> 
> Puede asignar a propiedades individuales u objetos completos. En este ejemplo, se asigna a propiedades individuales.


1. Desplácese hacia abajo hasta que llegue al **`web`** objeto

1. Seleccione para abrirlo

1. Asigne los siguientes elementos de datos al correspondiente `web` Variables XDM

   * **`web.webPageDetials.name`** hasta `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** hasta `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** hasta `%page.pageInfo.hierarchie1%`

1. Configure `web.webPageDetials.pageViews.value` como `1`.

   ![Actualización del contenido de variables](assets/create-rule-xdm-variable-content.png)

1. A continuación, busque la `identityMap` en el esquema y selecciónelo

1. Mapa a `identityMap.loginID` elemento de datos

   ![Actualizar mapa de identidad variable](assets/create-rule-variable-identityMap.png)

1. A continuación, busque el campo eventType y selecciónelo

1. Introduzca el valor `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > Este menú desplegable rellena el **`xdm.eventType`** en el objeto XDM. Aunque también puede escribir etiquetas de forma libre en este campo, es muy recomendable que **no** ya que tiene efectos adversos con Platform.

   >[!TIP]
   >
   > Para comprender qué valores se rellenan en `eventType` , debe ir a la página de esquema y seleccionar el campo `eventType` para ver los valores sugeridos en el carril derecho.

   >[!TIP]
   >
   > Mientras que ninguno `web.webPageDetials.pageViews.value` ni `eventType` establezca en `web.webpagedetails.pageViews` son necesarios para que Adobe Analytics procese una señalización como vista de página, resulta útil disponer de una forma estándar de indicar una vista de página para otras aplicaciones de flujo descendente.

   ![Actualizar mapa de identidad variable](assets/create-tag-rule-eventType.png)


1. Seleccionar **[!UICONTROL Conservar cambios]** y luego **[!UICONTROL Guardar]** la regla de la siguiente pantalla para terminar de crearla


#### Enriquezca el objeto XDM con reglas adicionales con la acción Actualizar variable

Puede utilizar **[!UICONTROL Actualizar variable]**  en varias reglas secuenciadas para enriquecer el objeto XDM antes de enviarlo a [!UICONTROL Red perimetral de plataforma].

>[!TIP]
>
>El orden de las reglas determina qué regla se ejecuta primero cuando se activa un evento. Si dos reglas tienen el mismo tipo de evento, se ejecuta primero la que tenga el número más bajo.
> 
>![orden de reglas](assets/set-up-analytics-sequencing.png)

##### Campos de página de producto

Comience por rastrear las vistas de productos en la página de detalles del producto de Luma:

1. Seleccionar **[!UICONTROL Agregar regla]**
1. Asígnele un nombre  [!UICONTROL `ecommerce - pdp library loaded - AA (order 20)`]
1. Seleccione el ![símbolo +](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en Evento para añadir un nuevo déclencheur
1. En **[!UICONTROL Extensión]**, seleccione **[!UICONTROL Núcleo]**
1. En **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL Page Bottom]**
1. Asígnele un nombre `Core - Page Bottom - order 20`
1. Seleccionar para abrir **[!UICONTROL Opciones avanzadas]**, escriba `20`. Esto garantiza que la regla se ejecute después de que `all pages global content variables - library loaded - AA (order 1)` que establece las variables de contenido global, pero antes de la variable `all pages send event - library loaded - AA (order 50)` que envía el evento XDM.

   ![Reglas XDM de Analytics](assets/set-up-analytics-pdp.png)

1. En **[!UICONTROL Condiciones]**, seleccione para **[!UICONTROL Añadir]**
1. Salir **[!UICONTROL Tipo de lógica]** as **[!UICONTROL Normal]**
1. Salir **[!UICONTROL Extensiones]** as **[!UICONTROL Núcleo]**
1. Seleccionar **[!UICONTROL Tipo de condición]** as **[!UICONTROL Ruta sin cadena de consulta]**
1. A la derecha, habilite la **[!UICONTROL Regex]** alternar
1. En **[!UICONTROL ruta igual a]** set `/products/`. Para el sitio de demostración de Luma, garantiza que la regla solo incluya déclencheur en las páginas de productos
1. Seleccionar **[!UICONTROL Conservar cambios]**

   ![Reglas XDM de Analytics](assets/set-up-analytics-product-condition.png)

1. En **[!UICONTROL Acciones]** select **[!UICONTROL Añadir]**
1. Seleccionar **[!UICONTROL SDK web de Adobe Experience Platform]** extensión
1. Seleccionar **[!UICONTROL Tipo de acción]** as **[!UICONTROL Actualizar variable]**
1. Desplácese hacia abajo hasta el `commerce` y seleccione para abrirlo.
1. Abra el **[!UICONTROL productViews]** objeto y conjunto **[!UICONTROL valor]** hasta `1`

   ![configurar vista de producto](assets/set-up-analytics-prodView.png)

   >[!TIP]
   >
   >La configuración de commerce.productViews.value=1 en XDM se asigna automáticamente al `prodView` evento en Analytics


1. Desplácese hacia abajo hasta y seleccione `productListItems` matriz
1. Seleccionar **[!UICONTROL Proporcionar elementos individuales]**
1. Seleccionar **[!UICONTROL Agregar elemento]**

   ![Estableciendo evento de vista de producto](assets/set-up-analytics-xdm-individual.png)

   >[!CAUTION]
   >
   >El **`productListItems`** es un `array` tipo de datos, de modo que espera que los datos se incluyan como una colección de elementos. Debido a la estructura de capas de datos del sitio de demostración de Luma y a que solo es posible ver un producto a la vez en el sitio de Luma, los elementos se agregan de forma individual. Al implementar en su propio sitio web, en función de la estructura de la capa de datos, puede proporcionar una matriz completa.

1. Seleccionar para abrir **[!UICONTROL Elemento 1]**
1. Mapa **`productListItems.item1.SKU`** a `%product.productInfo.sku%`

   ![Variable del objeto XDM de SKU del producto](assets/set-up-analytics-sku.png)

1. Buscar `eventType` y configúrelo en `commerce.productViews`

1. Seleccionar **[!UICONTROL Conservar cambios]**

1. Seleccionar **[!UICONTROL Guardar]** para guardar la regla




### Campos del carro de compras

Puede asignar toda la matriz a un objeto XDM, siempre que la matriz coincida con el formato del esquema XDM. El elemento de datos de código personalizado `cart.productInfo` ha creado bucles anteriores a través de `digitalData.cart.cartEntries` objeto de capa de datos en Luma y lo traduce al formato requerido del `productListItems` del esquema XDM.

Para ilustrarlo, consulte la comparación a continuación de la capa de datos del sitio de Luma (izquierda) con el elemento de datos traducido (derecha):

![Formato de matriz de objeto XDM](assets/data-element-xdm-array.png)

Comparar el elemento de datos con `productListItems` estructura (sugerencia, debe coincidir).

>[!IMPORTANT]
>
>Observe cómo se traducen las variables numéricas, con valores de cadena en la capa de datos como `price` y `qty` se ha cambiado el formato a números en el elemento de datos. Estos requisitos de formato son importantes para la integridad de los datos en Platform y se determinan durante la [configuración de esquemas](configure-schemas.md) paso. En el ejemplo, **[!UICONTROL cantidad]** utiliza el **[!UICONTROL Entero]** tipo de datos.
> ![Tipo de datos del esquema XDM](assets/set-up-analytics-quantity-integer.png)

Ahora, asignemos la matriz al objeto XDM&quot;.


1. Cree una nueva regla con el nombre `ecommerce - cart library loaded - AA (order 20)`
1. Seleccione el ![símbolo +](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en Evento para añadir un nuevo déclencheur
1. En **[!UICONTROL Extensión]**, seleccione **[!UICONTROL Núcleo]**
1. En **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL Page Bottom]**
1. Asígnele un nombre `Core - Page Bottom - order 20`
1. Seleccionar para abrir **[!UICONTROL Opciones avanzadas]**, escriba `20`
1. Seleccionar **[!UICONTROL Conservar cambios]**

   ![Reglas XDM de Analytics](assets/set-up-analytics-cart-sequence.png)

1. En **[!UICONTROL Condiciones]**, seleccione para **[!UICONTROL Añadir]**
1. Salir **[!UICONTROL Tipo de lógica]** as **[!UICONTROL Normal]**
1. Salir **[!UICONTROL Extensiones]** as **[!UICONTROL Núcleo]**
1. Seleccionar **[!UICONTROL Tipo de condición]** as **[!UICONTROL Ruta sin cadena de consulta]**
1. A la derecha, **no** habilite el **[!UICONTROL Regex]** alternar
1. En **[!UICONTROL ruta igual a]** set `/content/luma/us/en/user/cart.html`. Para el sitio de demostración de Luma, garantiza que la regla solo contenga déclencheur en la página del carro de compras
1. Seleccionar **[!UICONTROL Conservar cambios]**

   ![Reglas XDM de Analytics](assets/set-up-analytics-cart-condition.png)

1. En **[!UICONTROL Acciones]** select **[!UICONTROL Añadir]**
1. Seleccionar **[!UICONTROL SDK web de Adobe Experience Platform]** extensión
1. Seleccionar **[!UICONTROL Tipo de acción]** as **[!UICONTROL Actualizar variable]**
1. Desplácese hacia abajo hasta el `commerce` y seleccione para abrirlo.
1. Abra el **[!UICONTROL productListViews]** objeto y conjunto **[!UICONTROL valor]** hasta `1`

   ![configurar vista de producto](assets/set-up-analytics-cart-view.png)

   >[!TIP]
   >
   >La configuración de commerce.productListViews.value=1 en XDM se asigna automáticamente al `scView` evento en Analytics



1. Desplácese hacia abajo hasta y seleccione **[!UICONTROL productListItems]** matriz

1. Seleccionar **[!UICONTROL Proporcionar toda la matriz]**

1. Mapa a **`cart.productInfo`** elemento de datos

1. Seleccionar `eventType` y se establece en `commerce.productListViews`

1. Seleccionar **[!UICONTROL Conservar cambios]**

1. Seleccionar **[!UICONTROL Guardar]** para guardar la regla

Cree otras dos reglas para el cierre de compra y la compra siguiendo el mismo patrón con las siguientes diferencias:

**Nombre de regla**: `ecommerce - checkout library loaded - AA (order 20)`

* **[!UICONTROL Condición]**: /content/luma/us/en/user/checkout.html
* Configure `eventType` como `commerce.checkouts`.
* Establecer **Evento de comercio de XDM**: commerce.checkout.value a `1`

  >[!TIP]
  >
  >Esto equivale a configurar `scCheckout` evento en Analytics

**Nombre de regla**: `ecommerce - purchase library loaded - AA (order 20)`

* **[!UICONTROL Condición]**: /content/luma/us/en/user/checkout/order/thank-you.html
* Configure `eventType` como `commerce.purchases`.
* Establecer **Evento de comercio de XDM**: commerce.purchases.value a `1`

  >[!TIP]
  >
  >Esto equivale a configurar `purchase` evento en Analytics

Hay pasos adicionales para capturar todos los datos necesarios `purchase` variables de evento:

1. Abrir **[!UICONTROL comercio]** objeto
1. Abra el **[!UICONTROL pedido]** objeto
1. Mapa **[!UICONTROL purchaseID]** a la `cart.orderId` elemento de datos
1. Establecer **[!UICONTROL currencyCode]** al valor codificado `USD`

   ![Estableciendo purchaseID para Analytics](assets/set-up-analytics-purchase.png)

   >[!TIP]
   >
   >Esto equivale a configurar `s.purchaseID` y `s.currencyCode` variables en Analytics


1. Desplácese hacia abajo hasta y seleccione **[!UICONTROL productListItems]** matriz
1. Seleccionar **[!UICONTROL Proporcionar toda la matriz]**
1. Mapa a **`cart.productInfo.purchase`** elemento de datos
1. Seleccionar **[!UICONTROL Guardar]**

Cuando haya terminado, debería ver las siguientes reglas creadas.

![Reglas XDM de Analytics](assets/set-up-analytics-rules.png)


### Enviar evento

Ahora que ha establecido las variables, puede crear la segunda regla para enviar el objeto XDM a Platform Edge Network con la variable **[!UICONTROL Enviar evento]** tipo de acción.

1. A la derecha, seleccione para **[!UICONTROL Agregar regla]** para crear otra regla

1. Asigne un nombre a la regla `all pages send event - library loaded - AA (order 50)`.

1. En el **[!UICONTROL Eventos]** , seleccione **[!UICONTROL Añadir]**

1. Utilice el **[!UICONTROL Extensión principal]** y seleccione `Page Bottom` como el **[!UICONTROL Tipo de evento]**

1. En el **[!UICONTROL Nombre]** , asígnele un nombre `Core - Page Bottom - order 50`. Esto le ayuda a describir el déclencheur con un nombre significativo.

1. Seleccionar **[!UICONTROL Avanzadas]** desplegable e introduzca `50` in **[!UICONTROL Pedido]**. Esto garantizará que el segundo déclencheur de regla sea posterior al primero que configure como déclencheur `1`.

1. Seleccionar **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal
   ![Seleccionar Déclencheur inferior de la página](assets/create-tag-rule-trigger-bottom-send.png)

1. En el **[!UICONTROL Acciones]** , seleccione **[!UICONTROL Añadir]**

1. Como el **[!UICONTROL Extensión]**, seleccione  **[!UICONTROL SDK web de Adobe Experience Platform]**

1. Como el  **[!UICONTROL Tipo de acción]**, seleccione  **[!UICONTROL Enviar evento]**

1. Como el **[!UICONTROL XDM]**, seleccione la `xdm.variable.content` elemento de datos creado en la lección anterior

1. Seleccionar **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal

   ![Añadir la acción Enviar evento](assets/create-rule-send-event-action.png)
1. Seleccionar **[!UICONTROL Guardar]** para guardar la regla

   ![Guarde la regla](assets/create-rule-save-rule.png)

## Publicación de la regla en una biblioteca

A continuación, publique la regla en el entorno de desarrollo para poder verificar si funciona.

Para crear una biblioteca:

1. Ir a **[!UICONTROL Flujo de publicación]** en el panel de navegación izquierdo

1. Seleccionar **[!UICONTROL Añadir biblioteca]**

   ![Seleccione Añadir biblioteca.](assets/rule-publish-library.png)
1. Para el **[!UICONTROL Nombre]**, introduzca `Luma Web SDK Tutorial`
1. Para el **[!UICONTROL Entorno]**, seleccione `Development`
1. Seleccionar  **[!UICONTROL Añadir todos los recursos modificados]**

   >[!NOTE]
   >
   >    Además de la extensión SDK para web de Adobe Experience Platform y la `all pages global content variables - library loaded - AA (order 50)` , verá los componentes de etiquetas creados en lecciones anteriores. La extensión Core contiene el JavaScript base requerido por todas las propiedades de etiquetas web.

1. Seleccionar **[!UICONTROL Guardar y generar para desarrollo]**

   ![Crear y crear la biblioteca](assets/create-tag-rule-library-changes.png)

La biblioteca puede tardar unos minutos en crearse y, cuando se completa, muestra un punto verde a la izquierda del nombre de la biblioteca:

![Compilación completa](assets/create-rule-development-success.png)

Como puede ver en el [!UICONTROL Flujo de publicación] En la pantalla de, hay mucho más en el proceso de publicación que está fuera del ámbito de este tutorial. Este tutorial solo utiliza una biblioteca en el entorno de desarrollo.

Ahora está listo para validar los datos en la solicitud utilizando el Adobe Experience Platform Debugger.

[Siguiente ](validate-with-debugger.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
