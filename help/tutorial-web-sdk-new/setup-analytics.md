---
title: Configuración de Adobe Analytics mediante el SDK web de Experience Platform
description: Obtenga información sobre cómo configurar Adobe Analytics mediante el SDK web de Experience Platform. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
solution: Data Collection, Analytics
source-git-commit: fd366a4848c2dd9e01b727782e2f26005a440725
workflow-type: tm+mt
source-wordcount: '3078'
ht-degree: 0%

---

# Configuración de Adobe Analytics con el SDK web de Platform

Obtenga información sobre cómo configurar Adobe Analytics mediante [SDK web de Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html), cree reglas de etiquetas para enviar datos a Adobe Analytics y valide que Analytics está capturando los datos según lo esperado.

[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics.html?lang=es) es una aplicación líder del sector que le permite comprender a sus clientes como personas y dirigir su negocio con inteligencia de clientes.

![Diagrama del SDK web a Adobe Analytics](assets/dc-websdk-aa.png)

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Configuración de un esquema XDM para Adobe Analytics
* Comprenda la diferencia entre las variables XDM asignadas automáticamente y manualmente para Analytics
* Configuración de una secuencia de datos para habilitar Adobe Analytics
* Anular una secuencia de datos para enviar datos a otro grupo de informes de Adobe Analytics
* Asignar elementos de datos de matriz individuales o completos al objeto XDM
* Utilice el tipo de acción Actualizar regla de variable para apilar varias reglas en un evento XDM
* Captura de vistas de página en Adobe Analytics con el objeto XDM
* Captura de datos de comercio electrónico con el objeto XDM para la cadena de producto de Adobe Analytics
* Definición de un eVar de comercialización de sintaxis de producto mediante XDM
* Validar si las variables de Adobe Analytics se establecen con el objeto XDM mediante Experience Platform Debugger
* Usar reglas de procesamiento de Adobe Analytics para establecer variables personalizadas
* Adobe Analytics captura los datos con Adobe Experience Platform Assurance
* Adobe Analytics captura los datos validados mediante informes en tiempo real

## Requisitos previos

Para completar esta lección, primero debe:

* Estar familiarizado con Adobe Analytics y tener acceso a él.

* Tener al menos un ID de grupo de informes de prueba o desarrollo. Si no dispone de un grupo de informes de prueba o desarrollo que pueda utilizar para este tutorial, [cree uno](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=es).

* Complete las lecciones anteriores de las secciones Configuración inicial y Configuración de etiquetas de este tutorial.

## Configuración de la secuencia de datos

El SDK web de Platform envía datos del sitio web a Platform Edge Network. A continuación, la secuencia de datos indica a Platform Edge Network a qué grupos de informes de Adobe Analytics deben reenviarse los datos.

1. Ir a [Recopilación de datos](https://experience.adobe.com/#/data-collection){target="blank"} interfaz
1. En el panel de navegación izquierdo, seleccione **[!UICONTROL Datastreams]**
1. Seleccione el creado anteriormente `Luma Web SDK: Development Environment` secuencia de datos

   ![Seleccione la secuencia de datos del SDK web de Luma](assets/datastream-luma-web-sdk-development.png)

1. Seleccionar **[!UICONTROL Añadir servicio]**
   ![Añadir un servicio al conjunto de datos](assets/datastream-analytics-addService.png)
1. Seleccionar **[!UICONTROL Adobe Analytics]** como el **[!UICONTROL Servicio]**
1. Introduzca el  **[!UICONTROL ID del grupo de informes]** del grupo de informes de desarrollo
1. Seleccionar **[!UICONTROL Guardar]**

   ![Análisis de guardado de flujo de datos](assets/datastream-add-analytics.png)

   >[!TIP]
   >
   >Agregar más grupos de informes seleccionando **[!UICONTROL Agregar grupo de informes]** es equivalente al etiquetado de grupos múltiples.

>[!WARNING]
>
>En este tutorial, solo puede configurar el grupo de informes de Adobe Analytics para su entorno de desarrollo. Al crear flujos de datos para su propio sitio web, crearía flujos de datos y grupos de informes adicionales para los entornos de ensayo y producción.

## Esquemas XDM y variables de Analytics

¡Felicidades! Ya ha configurado un esquema compatible con Adobe Analytics en la [Configuración de un esquema](configure-schemas.md) ¡lección!

Pero tal vez se pregunten, ¿cómo configuro todas mis props, evars y eventos?

Existen varios métodos que se pueden utilizar simultáneamente:

1. Establezca campos XDM estándar y algunos se asignarán automáticamente a variables de Analytics.
1. Asigne campos XDM adicionales a variables de Analytics en reglas de procesamiento de Analytics.
1. Asigne a variables de Analytics directamente en el esquema XDM.

<!-- Implementing Platform Web SDK should be as product-agnostic as possible. For Adobe Analytics, mapping eVars, props, and events doesn't occur during schema creation, nor during the tag rules configuration as it has been done traditionally. Instead, every XDM key-value pair becomes a Context Data Variable that maps to an Analytics variable in one of two ways: 

1. Automatically mapped variables using reserved XDM fields
1. Manually mapped variables using Analytics Processing Rules

To understand what XDM variables are auto-mapped to Adobe Analytics, please see [Variables automatically mapped in Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en). Any variable that is not auto-mapped must be manually mapped. 

 1. **Product-agnostic XDM**: maintain a semantic key-value pair XDM schema and use [Adobe Analytics Processing Rules](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.html) to map the XDM fields to eVars, props, and so on. By a semantic XDM schema, we mean that the field names themselves have meaning. For example, the field name `web.webPageDetails.pageName` has more meaning than say `prop1` or `evar3`.


 1. **Analytics-specific XDM**: Use a purpose-built Adobe Analytics field group in the XDM schema called `Adobe Analytics ExperienceEvent Template`
 
The approach Adobe has seen customers prefer is the **Analytics-specific XDM**, because it skips the mapping step in the Adobe Analytics Processing Rules interface. The steps in this lesson use the **Analytics-specific XDM** approach.
-->

### Campos asignados automáticamente

Muchos campos XDM se asignan automáticamente a variables de Analytics.

El esquema creado en [Configuración de un esquema](configure-schemas.md) Esta lección contiene algunas variables asignadas automáticamente a Analytics, como se describe en esta tabla:

| Variables asignadas automáticamente de XDM a Analytics | variable de Adobe Analytics |
|-------|---------|
| `identitymap.ecid.[0].id` | mid |
| `web.webPageDetails.name` | s.pageName |
| `web.webPageDetails.server` | s.server |
| `web.webPageDetails.siteSection` | s.channel |
| `commerce.productViews.value` | prodView |
| `commerce.productListViews.value` | scView |
| `commerce.checkouts.value` | scCheckout |
| `commerce.purchases.value` | compra |
| `commerce.order.currencyCode` | s.currencyCode |
| `commerce.order.purchaseID` | s.purchaseID |
| `productListItems[].SKU` | s.products=;product name;;;; (primary; consulte la nota más abajo) |
| `productListItems[].name` | s.products=;product name;;;; (reserva: consulte la nota más abajo) |
| `productListItems[].quantity` | s.products=;;product quantity;;; |
| `productListItems[].priceTotal` | s.product=;;;product price;; |

Las secciones individuales de la cadena de producto de Analytics se configuran mediante diferentes variables XDM en la variable `productListItems` objeto.
>El 18 de agosto de 2022, `productListItems[].SKU` tiene prioridad para la asignación al nombre del producto en la variable s.products.
>El valor establecido en `productListItems[].name` se asigna al nombre del producto solo si `productListItems[].SKU` no existe. De lo contrario, no está asignado y disponible en los datos de contexto.
>No establezca una cadena vacía o nulo como  `productListItems[].SKU`. Esto tiene el efecto no deseado de asignar al nombre del producto en la variable s.products.

Para obtener la lista más actualizada de asignaciones, consulte [Asignación de variables de Analytics en Adobe Experience Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=es).


### Asignación con reglas de procesamiento de Analytics

Todos los campos del esquema XDM pasan a estar disponibles para Adobe Analytics como variables de datos de contexto con el siguiente prefijo `a.x.`. Por ejemplo, `a.x.web.webinteraction.region`

En este ejercicio, se asigna una variable XDM a una prop. Siga estos mismos pasos para cualquier asignación personalizada que deba realizar para cualquier `eVar`, `prop`, `event`, o variable accesible a través de Reglas de procesamiento.

1. Vaya a la interfaz de Analytics.
1. Ir a [!UICONTROL Administrador] > [!UICONTROL Herramientas de administración] > [!UICONTROL Grupos de informes]
1. Seleccione el grupo de informes de desarrollo/prueba que está utilizando para el tutorial > [!UICONTROL Editar configuración] > [!UICONTROL General] > [!UICONTROL Reglas de procesamiento]

   ![Compra de Analytics](assets/analytics-process-rules.png)

1. Cree una regla para **[!UICONTROL Sobrescribir el valor de]** `[!UICONTROL Product SKU (prop1)]` hasta `a.x.productlistitems.0.sku`. Recuerde agregar una nota sobre por qué está creando la regla y asigne un nombre al título de la misma. Seleccionar **[!UICONTROL Guardar]**

   ![Compra de Analytics](assets/analytics-set-processing-rule.png)

   >[!IMPORTANT]
   >
   >La primera vez que se asigna a una regla de procesamiento, la interfaz de usuario no muestra las variables de datos de contexto del objeto XDM. Para corregir que, seleccione cualquier valor, haga clic en Guardar y vuelva a editar. Ahora deberían aparecer todas las variables XDM.

### Asignar a variables de Analytics en el esquema XDM

Una alternativa a las reglas de procesamiento es asignar a variables de Analytics en el esquema XDM mediante `Adobe Analytics ExperienceEvent Template` grupo de campos. Este enfoque ha ganado popularidad porque a muchos usuarios les resulta más sencillo que configurar reglas de procesamiento, sin embargo, al aumentar el tamaño de la carga útil XDM, podría aumentar el tamaño del perfil en otras aplicaciones como Real-Time CDP.

Para añadir el `Adobe Analytics ExperienceEvent Template` grupo de campos al esquema:

1. Abra el [Recopilación de datos](https://experience.adobe.com/#/data-collection){target="blank"} interfaz
1. Seleccionar **[!UICONTROL Esquemas]** desde la navegación izquierda
1. Asegúrese de que está en la zona protegida que está utilizando en el tutorial.
1. Abra su `Luma Web Event Data` esquema
1. En el **[!UICONTROL Grupos de campos]** , seleccione **[!UICONTROL Añadir]**
1. Busque el `Adobe Analytics ExperienceEvent Template` grupo de campos y agréguelo al esquema


Ahora establezca un eVar de comercialización en la cadena de producto. Con el `Adobe Analytics ExperienceEvent Template` , puede asignar variables a eVars de comercialización o eventos dentro de la cadena de producto. Esto también se conoce como configuración **Comercialización de sintaxis del producto**.

1. Vuelva a la propiedad de etiquetas

1. Abra la regla `ecommerce - library loaded - set product details variables - 20`

1. Abra el **[!UICONTROL Establecer variable]** acción

1. Seleccionar para abrir `_experience > analytics > customDimensions > eVars > eVar1`

1. Configure las variables **[!UICONTROL Valor]** hasta `%product.productInfo.title%`

1. Seleccionar **[!UICONTROL Conservar cambios]**

   ![Variable del objeto XDM de SKU del producto](assets/set-up-analytics-product-merchandising.png)

1. Seleccionar **[!UICONTROL Guardar]** para guardar la regla

Como acaba de ver, básicamente todas las variables de Analytics se pueden configurar en la variable `Adobe Analytics ExperienceEvent Template` grupo de campos.

>[!NOTE]
>
> Observe el `_experience` objeto bajo `productListItems` > `Item 1`. Configuración de cualquier variable en esto [!UICONTROL objeto] establece eVars o eventos de sintaxis del producto.


### Envío de datos a otro grupo de informes

Es posible que desee cambiar a qué grupos de informes de Adobe Analytics se envían los datos cuando los visitantes se encuentran en determinadas páginas. Esto requiere una configuración tanto en el conjunto de datos como en una regla.

#### Configurar una anulación del grupo de informes de secuencia de datos

Para configurar la configuración de anulación de grupos de informes de Adobe Analytics en el conjunto de datos:

1. Abra su secuencia de datos
1. Edite el **[!UICONTROL Adobe Analytics]** mediante la apertura de la ![más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, seleccione **[!UICONTROL Editar]**

   ![Sobrescribir la secuencia de datos](assets/datastream-edit-analytics.png)

1. Seleccione el **[!UICONTROL Opciones avanzadas]** para abrir **[!UICONTROL Anulaciones de grupos de informes]**

1. Seleccione los grupos de informes que desee anular. En este caso, `Web SDK Course Dev` y `Web SDK Course Stg`

1. Seleccione Guardar

   ![Sobrescribir la secuencia de datos](assets/analytics-datastreams-edit-adobe-analytics-configurations-report-suites.png)


#### Envíe una vista de página a otro grupo de informes con anulación de secuencia de datos

Vamos a crear una regla para enviar una llamada de vista de página adicional a un grupo de informes diferente. Utilice la función de anulación de la secuencia de datos para cambiar el grupo de informes de una página mediante **[!UICONTROL Enviar evento]** Acción.

1. Cree una nueva regla y asígnele el nombre `homepage - library loaded - AA report suite override - 51`

1. Seleccione el signo más debajo de **[!UICONTROL Evento]** para añadir un nuevo déclencheur

1. En **[!UICONTROL Extensión]**, seleccione **[!UICONTROL Núcleo]**

1. En **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL biblioteca cargada]**

1. Seleccionar para abrir **[!UICONTROL Opciones avanzadas]**, escriba `51`. Esto garantiza que la regla se ejecute después de que `all pages - library loaded - send event - 50` que establece el XDM de línea base con el **[!UICONTROL Actualizar variable]** tipo de acción.

   ![Anulación de grupo de informes de Analytics](assets/set-up-analytics-rs-override.png)

1. En **[!UICONTROL Condiciones]**, seleccione para **[!UICONTROL Añadir]**

1. Salir **[!UICONTROL Tipo de lógica]** as **[!UICONTROL Normal]**

1. Salir **[!UICONTROL Extensiones]** as **[!UICONTROL Núcleo]**

1. Seleccionar **[!UICONTROL Tipo de condición]** as **[!UICONTROL Ruta sin cadena de consulta]**

1. A la derecha, deje el **[!UICONTROL Regex]** alternancia deshabilitada

1. En **[!UICONTROL ruta igual a]** set `/content/luma/us/en.html`. Para el sitio de demostración de Luma, garantiza que la regla solo contenga déclencheur en la página de inicio

1. Seleccionar **[!UICONTROL Conservar cambios]**

   ![Condición de anulación de grupo de informes de Analytics](assets/set-up-analytics-override-condition.png)

1. En **[!UICONTROL Acciones]** select **[!UICONTROL Añadir]**

1. Como el **[!UICONTROL Extensión]**, seleccione **[!UICONTROL SDK web de Adobe Experience Platform]**

1. Como el **[!UICONTROL Tipo de acción]**, seleccione **[!UICONTROL Enviar evento]**

1. Como el **[!UICONTROL Tipo]**, seleccione `web.webpagedetails.pageViews`

1. Como el **[!UICONTROL Datos XDM]**, seleccione la `xdm.variable.content` que creó en la [Creación de elementos de datos](create-data-elements.md) lección

   ![Anulación de flujo de datos de Analytics](assets/set-up-analytics-datastream-override-1.png)

1. Desplácese hacia abajo hasta el **[!UICONTROL Anulaciones de configuraciones de flujo de datos]** sección

1. Deje el **[!UICONTROL Desarrollo]** pestaña seleccionada.

   >[!TIP]
   >
   >    Esta pestaña determina en qué entorno de etiquetas se produce la anulación. Para este ejercicio, solo debe especificar el entorno de desarrollo, pero cuando implemente esto en producción, recuerde hacerlo también en **[!UICONTROL Producción]** entorno.


1. Seleccione el **[!UICONTROL Datastream]**, en este caso `Luma Web SDK: Development Environment`

1. En **[!UICONTROL Grupos de informes]**, seleccione el grupo de informes para el que desee anular la selección. En este caso, `tmd-websdk-course-stg`.

1. Seleccionar **[!UICONTROL Conservar cambios]**

1. Y **[!UICONTROL Guardar]** su regla

   ![Anulación de flujo de datos de Analytics](assets/analytics-tags-report-suite-override.png)



## Cree su entorno de desarrollo

Añada los nuevos elementos de datos y reglas a su `Luma Web SDK Tutorial` y reconstruya su entorno de desarrollo.

¡Felicidades! El siguiente paso es validar la implementación de Adobe Analytics mediante el SDK web de Experience Platform.

## Validar Adobe Analytics para el SDK web de Platform

En el [Depurador](validate-with-debugger.md) En esta lección, ha aprendido a inspeccionar la solicitud XDM del lado del cliente con Platform Debugger y la consola de desarrollador del explorador, que es similar a cómo depurar un `AppMeasurement.js` Implementación de Analytics. También ha aprendido a validar las solicitudes del lado del servidor de Platform Edge Network enviadas a aplicaciones de Adobe y a ver una carga útil completamente procesada mediante Assurance.

Para validar que Analytics captura correctamente los datos mediante el SDK web de Experience Platform, debe ir dos pasos más allá para:

1. Valide cómo procesa los datos el objeto XDM en la red perimetral de Platform, utilizando la función de seguimiento de Edge de Experience Platform Debugger
1. Validar cómo Analytics procesa los datos mediante reglas de procesamiento e informes en tiempo real
1. Validar cómo Analytics procesa completamente los datos mediante Adobe Experience Platform Assurance

### Usar seguimiento de borde

Obtenga información sobre cómo validar que Adobe Analytics está capturando el ECID, las vistas de página, la cadena de producto y los eventos de comercio electrónico con la función Edge Trace de Experience Platform Debugger.

### Validación de ID de Experience Cloud

1. Vaya a la [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}
1. Seleccione el botón de inicio de sesión en la parte superior derecha y utilice las credenciales u: test@adobe.com p: test para autenticarse
1. Abra Experience Platform Debugger y [cambie la propiedad de etiquetas del sitio a su propia propiedad de desarrollo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)


1. Para habilitar el seguimiento de Edge, vaya a Experience Platform Debugger, en el panel de navegación izquierdo, seleccione **[!UICONTROL Registros]**, luego seleccione la **[!UICONTROL Edge]** y seleccione. **[!UICONTROL Connect]**

   ![Conectar seguimiento de Edge](assets/analytics-debugger-edgeTrace.png)

1. Estará vacío por ahora

   ![Seguimiento de Edge conectado](assets/analytics-debugger-edge-connected.png)

1. Actualice la página de Luma y vuelva a comprobar Experience Platform Debugger. Debería ver los datos que llegan. La fila que empieza por **[!UICONTROL Asignación automática de Analytics]** es la señalización de Adobe Analytics
1. Seleccione para abrir ambos `[!UICONTROL mappedQueryParams]` y la segunda lista desplegable para ver las variables de Analytics

   ![Seguimiento de Edge de señalizaciones de Analytics](assets/analytics-debugger-edge-analytics.png)

   >[!TIP]
   >
   >La segunda lista desplegable corresponde al ID del grupo de informes de Analytics al que está enviando los datos. Debe coincidir con su propio grupo de informes, no con el de la captura de pantalla.

1. Desplazarse hacia abajo para buscar `[!UICONTROL c.a.x.identitymap.ecid.[0].id]`. Es una variable de datos de contexto que captura el ECID
1. Desplácese hacia abajo hasta que vea el informe de Analytics. `[!UICONTROL mid]` variable. Ambos ID coinciden con el Experience Cloud ID del dispositivo.
1. En el sitio de Luma,

   ![Analytics ECID](assets/analytics-debugger-ecid.png)

   >[!NOTE]
   >
   >Como ha iniciado sesión, dedique un momento a validar el ID autenticado `112ca06ed53d3db37e4cea49cc45b71e` para el usuario **`test@adobe.com`** también se captura en el `[!UICONTROL c.a.x.identitymap.lumacrmid.[0].id]`

### Anulaciones de grupos de informes

Arriba configuró una anulación de secuencia de datos para el [Página principal de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).  Para validar esta configuración

1. Busque una fila con **[!UICONTROL Configuración de flujo de datos después de aplicar el reemplazo]**. Aquí encontrará el grupo de informes principal y los grupos de informes adicionales que se configuraron para las anulaciones del grupo de informes.

   ![Validación de lista de anulación de grupos de informes de Analytics](assets/aep-debugger-datastream-override.png)

1. Desplácese hacia abajo hasta la fila que comience por **[!UICONTROL Asignación automática de Analytics]**  y compruebe que la variable `[!UICONTROL reportSuiteIds]` muestra el grupo de informes que especificó en las configuraciones de anulación

   ![Validación de llamada de anulación de grupo de informes de Analytics](assets/aep-debugger-analytics-report-suite-override.png)

### Vistas de página de contenido

Vaya a una página de producto como la [Página de productos de Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02).  Compruebe que Analytics captura las vistas de páginas de contenido.

1. Buscar: `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`.
1. Desplácese hacia abajo para ver el `[!UICONTROL gn]` variable. Es la sintaxis dinámica de Analytics para `[!UICONTROL s.pageName]` variable. Captura el nombre de página de la capa de datos.

   ![Cadena de producto de Analytics](assets/analytics-debugger-edge-page-view.png)

### Eventos de cadena de producto y comercio electrónico

Dado que ya se encuentra en una página de producto, este ejercicio sigue utilizando el mismo seguimiento de Edge para validar que Analytics capture los datos del producto. Tanto la cadena de producto como los eventos de comercio electrónico se asignan automáticamente a variables XDM de Analytics. Siempre y cuando haya asignado a la aplicación adecuada `productListItem` Variable XDM al [configuración de un esquema XDM para Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics), la red perimetral de plataforma se encarga de asignar los datos a las variables de análisis adecuadas.

**En primer lugar, valide que la variable `Product String` se ha establecido**

1. Buscar: `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. La variable captura el valor del elemento de datos asignado al `productListItems.item1.sku` anteriormente en esta lección
1. Busque también. `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL _experience.analytics.customdimensions.evars.evar1]`. La variable captura el valor del elemento de datos asignado `productListItems.item1._experience.analytics.customdimensions.evars.evar1`
1. Desplácese hacia abajo para ver el `[!UICONTROL pl]` variable. Es la sintaxis dinámica de la variable de cadena de producto de Analytics
1. Tenga en cuenta que el nombre del producto de la capa de datos está asignado tanto a la variable `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]` y el `[!UICONTROL product]` parámetro de la cadena de products.  Además, el título de producto de la capa de datos se asigna a la evar1 de comercialización en la cadena de productos.

   ![Cadena de producto de Analytics](assets/analytics-debugger-prodstring.png)

   El seguimiento de Edge trata `commerce` eventos de forma ligeramente diferente a `productList` dimensiones. No ve una variable de datos de contexto asignada de la misma manera que ve el nombre del producto asignado a `[!UICONTROL c.a.x.productlistitem.[0].name]` arriba. En su lugar, el seguimiento de Edge muestra la asignación automática del evento final en Analytics `event` variable. Platform Edge Network lo asigna en consecuencia, siempre y cuando se asigne al XDM adecuado `commerce` mientras que [configuración del esquema para Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics); en este caso, la variable `commerce.productViews.value=1`.

1. Vuelva a la ventana de Experience Platform Debugger y desplácese hacia abajo hasta el `[!UICONTROL events]` se establece en. `[!UICONTROL prodView]`

1. Tenga en cuenta también `[!UICONTROL c.a.x.eventType]` se establece en `commerce.productViews` ya que se encuentra en una página de producto.

   >[!TIP]
   >
   > El `ecommerce - pdp library loaded - AA (order 20)` La regla de sobrescribe el valor de `eventType` configurado por el `all pages global content variables - library loaded - AA (order 1)` regla tal como se establece en déclencheur más adelante en la secuencia


   ![Vista de producto de Analytics](assets/analytics-debugger-prodView.png)

**Validar el resto de los eventos de comercio electrónico y las cadenas de producto establecidas para Analytics.**

1. Añadir [Reloj Didi Sport](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) al carro
1. Vaya a la [Página de carrito](https://luma.enablementadobe.com/content/luma/us/en/user/cart.html), compruebe el seguimiento de Edge para

   * `eventType` establezca en `commerce.productListViews`
   * `[!UICONTROL events: "scView"]`, y
   * se establece la cadena de producto

   ![Vista de carro de Analytics](assets/analytics-debugger-cartView.png)

1. Continúe con el cierre de compra, compruebe el seguimiento de Edge para

   * `eventType` establezca en `commerce.checkouts`
   * `[!UICONTROL events: "scCheckout"]`, y
   * se establece la cadena de producto

   ![Cierre de Analytics](assets/analytics-debugger-checkout.png)

1. Rellene solo el **Nombre** y **Apellidos** en el formulario de envío y seleccione **Continuar**. En la página siguiente, seleccione **Realizar pedido**
1. En la página de confirmación, marque Rastro de Edge para

   * `eventType` establezca en `commerce.purchases`
   * Evento de compra configurado `[!UICONTROL events: "purchase"]`
   * Variable de código de moneda establecida `[!UICONTROL cc: "USD"]`
   * ID de compra configurado en `[!UICONTROL pi]`
   * Cadena de producto `[!UICONTROL pl]` definición del nombre, cantidad y precio del producto

   ![Compra de Analytics](assets/analytics-debugger-purchase.png)



## Validar Adobe Analytics con Adobe Experience Platform Assurance

Adobe Experience Platform Assurance es un producto de Adobe Experience Cloud que le ayuda a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias con su sitio web y aplicación móvil.

Arriba ha validado que Adobe Analytics está capturando el ECID, las vistas de página, la cadena de producto y los eventos de comercio electrónico con la función Edge Trace de Experience Platform Debugger.  También ha validado esa asignación de prop1 mediante reglas de procesamiento e informes en tiempo real.  A continuación, valide esos mismos eventos con Adobe Experience Platform Assurance.

>[!NOTE]
>
>Para validar los datos de Adobe Analytics con Adobe Experience Platform Assurance, debe [Habilitar el acceso de los usuarios a Adobe Experience Platform Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html)

### Acceso a Adobe Experience Platform Assurance

Hay varias formas de acceder a Assurance:

1. A través de la interfaz Adobe Experience Platform
1. A través de la interfaz de recopilación de datos Adobe Experience Platform
1. Mediante registros dentro del Adobe Experience Platform Debugger (recomendado)

Para acceder a Assurance a través de Adobe Experience Platform, desplácese hacia abajo y seleccione **[!UICONTROL Assurance]** en la navegación del carril izquierdo debajo de **[!UICONTROL RECOPILACIÓN DE DATOS]**.  Seleccione el **[!UICONTROL &quot;Tutorial 3 de SDK web&quot;]** sesión para acceder a los eventos generados en la sección anterior.
![Assurance mediante Adobe Experience Platform](assets/assurance-open-aep.png)

Para acceder a Assurance a través de la recopilación de datos de Adobe Experience Platform, seleccione **[!UICONTROL Assurance]** en la navegación del carril izquierdo debajo de **[!UICONTROL RECOPILACIÓN DE DATOS]**.  Seleccione el **[!UICONTROL &quot;Tutorial 3 de SDK web&quot;]** sesión para acceder a los eventos generados en la sección anterior.\
![Assurance mediante la recopilación de datos de Adobe Experience Platform](assets/assurance-open-data-collection.png)

Para acceder a Assurance a través del Adobe Experience Platform Debugger, vaya a Experience Platform Debugger, en el panel de navegación izquierdo, seleccione **[!UICONTROL Registros]**, luego seleccione la **[!UICONTROL Edge]** y seleccione. **[!UICONTROL Connect]**.  Una vez establecida la conexión a la red perimetral, seleccione el icono de vínculo externo. Se recomienda acceder a Assurance a través de Debugger, ya que las sesiones web se deben iniciar desde Debugger.
![Assurance mediante la recopilación de datos de Adobe Experience Platform](assets/assurance-open-aep-debugger.png)

Dentro de **[!UICONTROL &quot;Tutorial 3 de SDK web&quot;]** Centro de sesión de Assurance **[!UICONTROL &quot;hitdebugger&quot;]** en la barra de búsqueda de eventos para filtrar los resultados a los datos posteriores al procesamiento de Adobe Analytics.
![Datos posteriores al procesamiento de Assurance Adobe Analytics](assets/assurance-hitdebugger.png)

### Validación de ID de Experience Cloud con Assurance

Para validar que Adobe Analytics está capturando el ECID, seleccione una señalización y abra la carga útil.  El proveedor de esta señalización debe ser **[!UICONTROL com.adobe.analytics.hitdebugger]**
![Validación de Adobe Analytics con Assurance](assets/assurance-hitdebugger-payload.png)

Luego desplácese hacia abajo hasta **[!UICONTROL mcvisId]** para validar que el ECID se captura correctamente
![Validación de ID de Experience Cloud con Assurance](assets/assurance-hitdebugger-mcvisId.png)

### Validación de vistas de página de contenido con Assurance

Con la misma señalización, compruebe que las vistas de página de contenido estén asignadas a la variable de Adobe Analytics correcta.
Desplácese hacia abajo hasta **[!UICONTROL pageName]** para validar que la variable `Page Name` se captura correctamente
![Validación del nombre de página con Assurance](assets/assurance-hitdebugger-content-pagename.png)

### Validación de eventos de cadena de producto y comercio electrónico con Assurance

Siguiendo los mismos casos de uso de validación utilizados al validar con Experience Platform Debugger anteriormente, siga utilizando la misma señalización para validar el `Ecommerce Events` y el `Product String`.

1. Busque la carga útil en la que **[!UICONTROL eventos]** contain `prodView`
   ![Validación de cadenas de producto con Assurance](assets/assurance-hitdebugger-prodView-event.png)
1. Desplácese hacia abajo hasta **[!UICONTROL product-string]** para validar el `Product String`.
   * Tenga en cuenta `Product SKU` y `Merchandizing eVar1`.
1. Desplácese hacia abajo y valide que `prop1`, que configuró con reglas de procesamiento en la sección anterior, contiene el `Product SKU`\
   ![Cadena de producto con validación de variables de comercialización con Assurance](assets/assurance-hitdebugger-prodView-productString-merchVar.png)

Siga validando la implementación revisando el carro de compras, el cierre de compra y los eventos de compra.

1. Busque la carga útil en la que **[!UICONTROL eventos]** contain `scView` y valide la cadena de producto.
   ![Validación de cadenas de producto con Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Busque la carga útil en la que **[!UICONTROL eventos]** contain `scCheckout` y valide la cadena de producto.
   ![Validación de cadenas de producto con Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Busque la carga útil en la que **[!UICONTROL eventos]** contain `purchase`
   ![Validación de cadenas de producto con Assurance](assets/assurance-hitdebugger-purchase-event.png)
1. Al validar el `purchase` evento, tenga en cuenta que la variable `Product String` debe contener el `Product SKU`, `Product Quantity` , y `Product Total Price`.
1. Además, para el `purchase` validar que la variable `purchase-id` y/o `purchaseId` están configuradas


¡Felicidades! ¡Tú lo hiciste! Este es el final de la lección y ahora está listo para implementar Adobe Analytics con el SDK web de Platform para su propio sitio web.

[Siguiente: ](setup-audience-manager.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
