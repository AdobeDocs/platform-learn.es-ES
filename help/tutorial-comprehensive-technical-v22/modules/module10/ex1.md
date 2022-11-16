---
title: 'Adobe Journey Optimizer: Configurar un recorrido basado en déclencheur: confirmación de pedido'
description: 'En esta sección puede configurar un recorrido basado en déclencheur: Confirmación de pedidos'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 69bb9eca-3942-4c31-a3d2-0b218143e1eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 9%

---

# 10.1 Configuración de un recorrido basado en déclencheur: confirmación de pedido

Inicie sesión en Adobe Journey Optimizer desde [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Se le redirigirá al **Página principal**  en Journey Optimizer. En primer lugar, asegúrese de que está utilizando el simulador para pruebas correcto. El entorno limitado que se va a usar se denomina `--aepSandboxId--`. Para cambiar de un simulador de pruebas a otro, haga clic en **PRODUCCIÓN (VA7)** y seleccione el simulador de pruebas de la lista. En este ejemplo, el simulador de pruebas recibe el nombre **Habilitación de AEP para el año fiscal 22**. Entonces estará en el **Página principal** vista del entorno limitado `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.1.1 Crear el evento

En el menú , vaya a **Configuraciones** y haga clic en **Administrar** under **Eventos**.

![Journey Optimizer](./images/oc30.png)

En el **Eventos** , verá una vista similar a esta. Haga clic en **Crear evento**.

![Journey Optimizer](./images/oc31.png)

A continuación, verá una configuración de evento vacía.

![Journey Optimizer](./images/oc32.png)

En primer lugar, asigne un nombre al evento de esta manera: `--demoProfileLdap--PurchaseEvent`y añada una descripción como esta: `Purchase Event`.

![Journey Optimizer](./images/oc34.png)

A continuación, se muestra la variable **Tipo de evento** selección. Select **Unitario**.

![Journey Optimizer](./images/eventidtype1.png)

A continuación, se muestra la variable **Tipo de ID de evento** selección. Select **Sistema generado**

![Journey Optimizer](./images/eventidtype.png)

A continuación, se muestra la selección de Esquema. Se preparó un esquema para este ejercicio. Utilice el esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![Journey Optimizer](./images/oc35.png)

Después de seleccionar el esquema, verá una serie de campos seleccionados en el **Carga útil** para obtener más información. Haga clic en el **Editar/Lápiz** para añadir campos adicionales a este evento.

![Journey Optimizer](./images/oc36.png)

Verá esta ventana emergente. Ahora debe marcar casillas de verificación adicionales para acceder a datos adicionales cuando se active este evento.

![Journey Optimizer](./images/oc37.png)

En primer lugar, marque la casilla de la línea . `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

A continuación, desplácese hacia abajo y marque la casilla de verificación en la línea `productListItems`.

![Journey Optimizer](./images/oc39.png)

A continuación, desplácese hacia abajo y marque la casilla de verificación en la línea `commerce`.

![Journey Optimizer](./images/oc391.png)

A continuación, haga clic en **Ok**.

A continuación, verá que se han añadido campos adicionales al evento. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc40.png)

El nuevo evento se comparte y el evento se ve en la lista de eventos disponibles ahora.

Haga clic en el evento de nuevo para abrir el **Editar evento** de nuevo.
Pase el ratón sobre la **Carga útil** para volver a ver los 3 iconos. Haga clic en el **Ver carga útil** icono.

![Journey Optimizer](./images/oc41.png)

Ahora verá un ejemplo de la carga útil esperada. Su evento tiene un eventID de orquestación único que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

El ID de evento es lo que se debe enviar a Adobe Journey Optimizer para almacenar en déclencheur el recorrido que se creará en el siguiente paso. Escriba este eventID, ya que lo necesitará en uno de los pasos siguientes.
`"eventID": "ef6dd943c94fe1b4763c098ccd1772344662f2a9f614513106cb5ada8be36857"`

Haga clic en **Ok**, seguido de **Cancelar**.

El evento está configurado y listo para utilizarse.

## 10.1.2 Crear su recorrido

En el menú , vaya a **Recorridos** y haga clic en **Crear Recorrido**.

![Journey Optimizer](./images/oc43.png)

Entonces verás esto. Póngale un nombre a tu recorrido. En su lugar, utilice `--demoProfileLdap-- - Order Confirmation journey`. Haga clic en **Aceptar**.

![Journey Optimizer](./images/oc45.png)

En primer lugar, debe añadir el evento como punto de partida del recorrido. Busque su evento `--demoProfileLdap--PurchaseEvent` y arrástrelo y suéltelo en el lienzo. Haga clic en **Aceptar**.

![Journey Optimizer](./images/oc46.png)

A continuación, en **Acciones**, busque la variable **Correo electrónico** y añádalo al lienzo.

![Journey Optimizer](./images/oc47.png)

Configure las variables **Categoría** a **Marketing** y seleccione una superficie de correo electrónico que le permita enviar correos electrónicos. En este caso, la superficie de correo electrónico que se va a seleccionar es **Correo electrónico**. Asegúrese de que las casillas de verificación de **Clics en correos electrónicos** y **aperturas por correo electrónico** están activadas.

![ACOP](./images/journeyactions1.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

Ahora ven esto. Haga clic en el **Línea de asunto** campo de texto.

![ACOP](./images/journeyactions3.png)

En el área de texto empiece a escribir **Gracias por tu pedido,**

![Journey Optimizer](./images/oc5.png)

La línea de asunto aún no ha finalizado. A continuación, debe introducir el token de personalización para el campo **Nombre** que se almacenan en `profile.person.name.firstName`. En el menú de la izquierda, desplácese hacia abajo para encontrar la variable **Persona** > **Nombre completo** >  **Nombre** y haga clic en el botón **+** para añadir el token de personalización a la línea de asunto. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc6.png)

Volverás aquí. Haga clic en **Diseñador de correo electrónico** para crear el contenido del correo electrónico.

![Journey Optimizer](./images/oc7.png)

En la siguiente pantalla, haga clic en **Diseño desde cero**.

![Journey Optimizer](./images/oc8.png)

En el menú de la izquierda, encontrará los componentes de estructura que puede utilizar para definir la estructura del correo electrónico (filas y columnas).

Arrastre y suelte 8 veces al **Columna 1:1** en el lienzo, que debería darle lo siguiente:

![Journey Optimizer](./images/oc9.png)

Vaya a **Componentes de contenido**.

![Journey Optimizer](./images/oc10.png)

Arrastre y suelte una **Imagen** en la primera fila. Haga clic en **Examinar**.

![Journey Optimizer](./images/oc11.png)

Vaya a la carpeta **enablement-assets**, seleccione el archivo **luma-logo.png** y haga clic en **Select**.

![Journey Optimizer](./images/oc12.png)

Ahora estás aquí de vuelta. Haga clic en la imagen para seleccionarla y, a continuación, utilice la variable **Tamaño** control deslizante para que la imagen del logotipo sea un poco más pequeña.

![Journey Optimizer](./images/oc13.png)

Vaya a **Componentes de contenido** y arrastre y suelte una **Imagen** en la segunda fila. Seleccione el **Componente de imagen** pero NO haga clic en Examinar.

![Journey Optimizer](./images/oc15.png)

Pegar esta URL de imagen en el campo **Fuente**: `https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/29043bedcde632a9cbe8a02a164189c9_preparing.png`. Esta imagen está alojada fuera del Adobe.

![Journey Optimizer](./images/oc14.png)

Al cambiar el ámbito a otro campo, se representa la imagen y verá esto:

![Journey Optimizer](./images/oc16.png)

A continuación, vaya a **Componentes de contenido** y arrastre y suelte un **Texto** en la tercera fila.

![Journey Optimizer](./images/oc17.png)

Seleccionar el texto predeterminado de ese componente **Escriba el texto aquí.** y sustitúyalo por el texto siguiente:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Coloque el cursor junto al texto **Hi** y haga clic en **Añadir personalización**.

![Journey Optimizer](./images/oc19.png)

Vaya a la **Persona** > **Nombre completo** > **Nombre** y haga clic en el botón **+** para añadir el token de personalización a la línea de asunto. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc20.png)

Verá esto:

![Journey Optimizer](./images/oc21.png)

A continuación, vaya a **Componentes de contenido** y arrastre y suelte un **Texto** en la cuarta fila.

![Journey Optimizer](./images/oc22.png)

Seleccionar el texto predeterminado de ese componente **Escriba el texto aquí.** y sustitúyalo por el texto siguiente:

`Order Information`

Cambie el tamaño de fuente a **26px** y centrar el texto en esta celda. Entonces tendrá esto:

![Journey Optimizer](./images/oc23.png)

A continuación, vaya a **Componentes de contenido** y arrastre y suelte una **HTML** en la quinta fila. Haga clic en el componente HTML y, a continuación, haga clic en **Mostrar el código fuente**.

![Journey Optimizer](./images/oc24.png)

En el **Editar HTML** , pegue este HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Haga clic en **Guardar**.

![Journey Optimizer](./images/oc25.png)

Entonces tendrás esto. Haga clic en **Guardar** para guardar el progreso.

![Journey Optimizer](./images/oc26.png)

Vaya a **Componentes de contenido** y arrastre y suelte una **HTML** en la sexta fila. Haga clic en el componente HTML y, a continuación, haga clic en **Mostrar el código fuente**.

![Journey Optimizer](./images/oc57.png)

En el **Editar HTML** , pegue este HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

Entonces tendrá esto:

![Journey Optimizer](./images/oc58.png)

Ahora tiene que reemplazar **xxx** por referencia al objeto productListItems que forma parte del suceso que déclencheur el recorrido.

![Journey Optimizer](./images/oc59.png)

Primero, elimine **xxx** en su código de HTML primero.

![Journey Optimizer](./images/oc60.png)

En el menú de la izquierda, haga clic en **Atributos contextuales**. Este contexto se pasa al mensaje desde el recorrido.

![Journey Optimizer](./images/oc601.png)

Entonces verás esto. Haga clic en la flecha situada junto a **Journey Orchestration** para profundizar.

![Journey Optimizer](./images/oc61.png)

Haga clic en la flecha situada junto a **Eventos** para profundizar.

![Journey Optimizer](./images/oc62.png)

Haga clic en la flecha situada junto a `--demoProfileLdap--PurchaseEvent` para profundizar.

![Journey Optimizer](./images/oc63.png)

Haga clic en la flecha situada junto a **productListItems** para profundizar.

![Journey Optimizer](./images/oc64.png)

Haga clic en el **+** junto a **Nombre** para agregarlo al lienzo. Entonces tendrás esto. Ahora debe seleccionar  **.name** como se indica en la captura de pantalla siguiente, y luego debe eliminar **.name**.

![Journey Optimizer](./images/oc65.png)

Entonces tendrás esto. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc66.png)

Volverá al Diseñador de correo electrónico ahora. Haga clic en **Guardar** para guardar el progreso.

![Journey Optimizer](./images/oc67.png)

A continuación, vaya a **Componentes de contenido** y arrastre y suelte una **HTML** en la séptima fila. Haga clic en el componente HTML y, a continuación, haga clic en **Mostrar el código fuente**.

![Journey Optimizer](./images/oc68.png)

En el **Editar HTML** , pegue este HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Hay 2 referencias de **xxx** en este código de HTML. Ahora tiene que reemplazar cada **xxx** por referencia al objeto productListItems que forma parte del suceso que déclencheur el recorrido.

![Journey Optimizer](./images/oc69.png)

En primer lugar, elimine la primera **xxx** en su código de HTML.

![Journey Optimizer](./images/oc71.png)

En el menú de la izquierda, haga clic en **Atributos contextuales**.

![Journey Optimizer](./images/oc711.png)

Haga clic en la flecha situada junto a **Journey Orchestration** para profundizar.

![Journey Optimizer](./images/oc72.png)

Haga clic en la flecha situada junto a **Eventos** para profundizar.

![Journey Optimizer](./images/oc722.png)

Haga clic en la flecha situada junto a `--demoProfileLdap--PurchaseEvent` para profundizar.

![Journey Optimizer](./images/oc73.png)

Haga clic en la flecha situada junto a **Comercio** para profundizar.

![Journey Optimizer](./images/oc733.png)

Haga clic en la flecha situada junto a **Pedido** para profundizar.

![Journey Optimizer](./images/oc74.png)

Haga clic en el **+** junto a **Precio total** para agregarlo al lienzo.

![Journey Optimizer](./images/oc75.png)

Entonces tendrás esto. Ahora elimine el segundo **xxx** en su código de HTML.

![Journey Optimizer](./images/oc76.png)

Haga clic en el **+** junto a **Precio total** para agregarlo al lienzo.

![Journey Optimizer](./images/oc77.png)

También puede añadir el campo **Moneda** desde el **Pedido** en el lienzo, como puede ver aquí.
Cuando haya terminado, haga clic en **Guardar** para guardar los cambios.

![Journey Optimizer](./images/oc771.png)

A continuación, volverá al Diseñador de correo electrónico. Haga clic en **Guardar** de nuevo.

![Journey Optimizer](./images/oc78.png)

Vuelva al panel de mensajes haciendo clic en el **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/oc79.png)

Haga clic en la flecha situada en la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/oc79a.png)

Haga clic en **Ok** para cerrar la acción del correo electrónico.

![Journey Optimizer](./images/oc79b.png)

Haga clic en **Publicación** para publicar el recorrido.

![Journey Optimizer](./images/oc511.png)

Haga clic en **Publicación** de nuevo.

![Journey Optimizer](./images/oc512.png)

El recorrido ya está publicado.

![Journey Optimizer](./images/oc513.png)

## 10.1.5 Actualizar la propiedad del cliente de recopilación de datos de Adobe Experience Platform

Vaya a [Recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/launch/) y seleccione **Etiquetas**.

Esta es la página Propiedades de la recopilación de datos de Adobe Experience Platform que vio anteriormente.

![Página de Properties](../module1/images/launch1.png)

En el módulo 0, Sistema de demostración creó dos propiedades de cliente para usted: uno para el sitio web y otro para la aplicación móvil. Para encontrarlos, busque `--demoProfileLdap--` en el **[!UICONTROL Buscar]** en la ventana Haga clic en para abrir el **Web** propiedad.

![Cuadro de búsqueda](../module1/images/property6.png)

Vaya a **Elementos de datos**. Buscar y abrir el elemento de datos **XDM - Compra**.

![Journey Optimizer](./images/oc91.png)

Entonces verás esto. Navegar al campo **_experience.campaign.orchestration.eventID** y complete su eventID aquí. El eventID que se debe rellenar aquí es el eventID que creó como parte del ejercicio 10.1.2. Haga clic en **Guardar** o **Guardar en biblioteca**.

![Journey Optimizer](./images/oc92.png)

Guarde los cambios en la propiedad Client y, a continuación, publique los cambios actualizando la biblioteca de desarrollo.

![Journey Optimizer](./images/oc93.png)

Los cambios ya están implementados y se pueden probar.

## 10.1.6 Pruebe el correo electrónico de confirmación de pedido mediante el sitio web de demostración

Probemos el recorrido actualizado comprando un producto en el sitio web de demostración.

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../module0/images/web8.png)

En el **Pantallas** página, haga clic en **Ejecutar**.

![DSN](../module1/images/web2.png)

Verá que su sitio web de demostración se abre. Seleccione la dirección URL y cópiela en el portapapeles.

![DSN](../module0/images/web3.png)

Abra una nueva ventana del explorador incógnito.

![DSN](../module0/images/web4.png)

Pegue la dirección URL del sitio web de la demostración, que copió en el paso anterior. A continuación, se le pedirá que inicie sesión con su Adobe ID.

![DSN](../module0/images/web5.png)

Seleccione su tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../module0/images/web6.png)

Verá su sitio web cargado en una ventana del navegador incógnito. Para cada demostración, tendrá que usar una ventana nueva del explorador incógnito para cargar la URL de su sitio web de demostración.

![DSN](../module0/images/web7.png)

Haga clic en el icono del logotipo de Adobe en la esquina superior izquierda de la pantalla para abrir el Visor de perfiles.

![Demostración](../module2/images/pv1.png)

Consulte el panel Visualizador de perfiles y el perfil del cliente en tiempo real con el **ID de Experience Cloud** como identificador principal para este cliente actualmente desconocido.

![Demostración](../module2/images/pv2.png)

Vaya a la página Registro/Inicio de sesión . Haga clic en **CREAR UNA CUENTA**.

![Demostración](../module2/images/pv9.png)

Complete los detalles y haga clic en **Registro** después de lo cual, se le redirigirá a la página anterior.

![Demostración](../module2/images/pv10.png)

Agregue cualquier producto al carro de compras y vaya a la sección **Carro de compras** página. Haga clic en **Continúe con el cierre de compra**.

![Journey Optimizer](./images/cart1.png)

A continuación, compruebe los campos en la página de cierre de compra y haga clic en **Cierre de compra**.

![Journey Optimizer](./images/cart2.png)

A continuación, recibirá su correo electrónico de confirmación de pedido en cuestión de segundos.

![Journey Optimizer](./images/oc98.png)

Ha terminado este ejercicio.

Paso siguiente: [10.2 Configuración de un recorrido de newsletter basado en lotes](./ex2.md)

[Volver al módulo 10](./journeyoptimizer.md)

[Volver a todos los módulos](../../overview.md)
