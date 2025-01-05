---
title: 'Adobe Journey Optimizer: Configuración de un recorrido basado en déclencheur: confirmación de pedido'
description: 'En esta sección configurará un recorrido basado en déclencheur: confirmación de pedido'
kt: 5342
doc-type: tutorial
exl-id: b9d9b357-08d1-4f65-9e0b-46224d035602
source-git-commit: 9865b5697abe2d344fb530636a1afc3f152a9e8f
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 1%

---

# 3.4.1 Configuración de un recorrido basado en déclencheur: confirmación de pedido

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.1.1 Creación de un evento

En el menú, ve a **Configuraciones** y haz clic en **Administrar** en **Eventos**.

![Journey Optimizer](./images/oc30.png)

En la pantalla **Eventos**, verá una vista similar a esta. Haga clic en **Crear evento**.

![Journey Optimizer](./images/oc31.png)

A continuación, verá una configuración de evento vacía.

En primer lugar, asigne al evento un nombre como este: `--aepUserLdap--PurchaseEvent` y agregue una descripción como esta: `Purchase Event`.

Para **Type**, seleccione **Unitary**.
Para **Tipo de ID de evento**, seleccione **Sistema generado**.

![Journey Optimizer](./images/eventidtype.png)

A continuación se muestra la selección Esquema. Se ha preparado un esquema para este ejercicio. Use el esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

Después de seleccionar el esquema, verá una serie de campos seleccionados en la sección **Carga útil**. Haga clic en el icono **Editar/Lápiz** para agregar campos adicionales a este evento.

![Journey Optimizer](./images/oc36.png)

Entonces verá esta ventana emergente. Ahora debe marcar casillas de verificación adicionales para acceder a datos adicionales cuando se active este evento.

![Journey Optimizer](./images/oc37.png)

En primer lugar, marque la casilla en la línea `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

A continuación, desplácese hacia abajo y marque la casilla de verificación en la línea `commerce`.

![Journey Optimizer](./images/oc391.png)

A continuación, desplácese hacia abajo y marque la casilla de verificación en la línea `productListItems`. Haga clic en **Ok**.

![Journey Optimizer](./images/oc39.png)

Luego verá que se han agregado campos adicionales al evento. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc40.png)

El nuevo evento se guarda y ahora verá el evento en la lista de eventos disponibles.

Vuelve a hacer clic en el evento para abrir de nuevo la pantalla **Editar evento**.
Pase el ratón sobre el campo **Carga útil** de nuevo para ver los 3 iconos. Haz clic en el icono **Ver carga**.

![Journey Optimizer](./images/oc41.png)

Ahora verá un ejemplo de la carga útil esperada. El evento tiene un identificador de evento de orquestación único, que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

El ID de evento es lo que debe enviarse a Adobe Journey Optimizer para almacenar en déclencheur el recorrido que va a generar en el siguiente paso. Anote este eventID, ya que lo necesitará en uno de los pasos siguientes.
`"eventID": "1c8148a8ab1993537d0ba4e6ac293dd4f2a88d80b2ca7be6293c3b28d4ff5ae6"`

Haga clic en **Aceptar**, seguido de **Cancelar**.

El evento está ahora configurado y listo para utilizarse.

## 3.4.1.2 Crear el recorrido

En el menú, ve a **Recorridos** y haz clic en **Crear Recorrido**.

![Journey Optimizer](./images/oc43.png)

Entonces verá esto... Dé un nombre a su recorrido. Usar `--aepUserLdap-- - Order Confirmation journey`. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc45.png)

En primer lugar, debe agregar el evento como punto de partida del recorrido. Busque el evento `--aepUserLdap--PurchaseEvent`, arrástrelo y suéltelo en el lienzo. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc46.png)

A continuación, en **Acciones**, busque la acción **Correo electrónico** y agréguela al lienzo.

![Journey Optimizer](./images/oc47.png)

Defina **Category** en **Marketing** y seleccione una superficie de correo electrónico que le permita enviar correo electrónico. En este caso, la superficie de correo electrónico que se va a seleccionar es **Correo electrónico**. Asegúrese de que las casillas de verificación de **Clics en el correo electrónico** y **aperturas del correo electrónico** estén habilitadas.

![ACOP](./images/journeyactions1.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

Ahora puede ver esto. Haga clic en el campo de texto **Línea de asunto**.

![ACOP](./images/journeyactions3.png)

En el área de texto empieza a escribir **Gracias por tu pedido,** y haz clic en el icono **Personalization**.

![Journey Optimizer](./images/oc5.png)

La línea de asunto aún no ha finalizado. A continuación, debe traer el token de personalización para el campo **Nombre** que se almacena en `profile.person.name.firstName`. En el menú de la izquierda, desplácese hacia abajo para encontrar el campo **Persona** > **Nombre completo** > **Nombre** y haga clic en el icono **+** para agregar el token de personalización a la línea de asunto. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc6.png)

Entonces volverás a estar aquí. Haga clic en **Editar cuerpo del correo electrónico** para crear el contenido del correo electrónico.

![Journey Optimizer](./images/oc7.png)

En la siguiente pantalla, haz clic en **Diseñar desde cero**.

![Journey Optimizer](./images/oc8.png)

En el menú de la izquierda, encontrará los componentes de estructura que puede utilizar para definir la estructura del correo electrónico (filas y columnas).

Arrastrar y soltar 8 veces una columna **1:1** en el lienzo, lo que debería proporcionarle lo siguiente:

![Journey Optimizer](./images/oc9.png)

En el menú de la izquierda, ve a **Fragmentos**. Arrastre el encabezado que creó anteriormente en [ejercicio 3.1.2.1](./../module3.1/ex2.md) al primer componente del lienzo. Arrastre el pie de página creado anteriormente en [ejercicio 3.1.2.2](./../module3.1/ex2.md) al último componente del lienzo.

![Journey Optimizer](./images/fragm1.png)

Haga clic en el icono **+** en el menú de la izquierda. Vaya a **Contenido** para empezar a agregar contenido al lienzo.

![Journey Optimizer](./images/oc10.png)

Vaya a **Contenido** y arrastre y suelte un componente **Imagen** en la segunda fila. Haga clic en **Examinar**.

![Journey Optimizer](./images/oc15.png)

Abra la carpeta **citi-signal-images**, haga clic para seleccionar la imagen **citisignal-preparation.png** y haga clic en **Seleccionar**.

![Journey Optimizer](./images/oc14.png)

En **Estilos**, cambie el ancho a **40%**.

![Journey Optimizer](./images/oc14a.png)

A continuación, vaya a **Contenido** y arrastre y suelte un componente **Texto** en la tercera fila.

![Journey Optimizer](./images/oc17.png)

Seleccione el texto predeterminado en ese componente **Escriba el texto aquí.** y reemplácelo por el siguiente texto:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Coloque el cursor junto al texto **Hi** y haga clic en **Agregar Personalization**.

![Journey Optimizer](./images/oc19.png)

Vaya al campo **Persona** > **Nombre completo** > **Nombre** y haga clic en el icono **+** para agregar el token de personalización a la línea de asunto. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc20.png)

A continuación, verá esto:

![Journey Optimizer](./images/oc21.png)

A continuación, vaya a **Contenido** y arrastre y suelte un componente **Texto** en la cuarta fila.

![Journey Optimizer](./images/oc22.png)

Seleccione el texto predeterminado en ese componente **Escriba el texto aquí.** y reemplácelo por el siguiente texto:

`Order Information`

Cambie el tamaño de la fuente a **26px** y centre el texto en esta celda. A continuación, tendrá esto:

![Journey Optimizer](./images/oc23.png)

A continuación, ve a **Contenido** y arrastra y suelta un componente **HTML** en la quinta fila. Haga clic en el componente HTML y, a continuación, en **Mostrar el código fuente**.

![Journey Optimizer](./images/oc24.png)

En la ventana emergente **Editar HTML**, pegue este HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Haga clic en **Guardar**.

![Journey Optimizer](./images/oc25.png)

Entonces, tendrás esto. Haga clic en **Guardar** para guardar el progreso.

![Journey Optimizer](./images/oc26.png)

Vaya a **Contenido** y arrastre y suelte un componente **HTML** en la sexta fila. Haga clic en el componente HTML y, a continuación, en **Mostrar el código fuente**.

![Journey Optimizer](./images/oc57.png)

En la ventana emergente **Editar HTML**, pegue este HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

A continuación, tendrá esto:

![Journey Optimizer](./images/oc58.png)

Ahora tiene que reemplazar **xxx** por una referencia al objeto productListItems que forma parte del evento que almacena en déclencheur el recorrido.

![Journey Optimizer](./images/oc59.png)

Primero, elimine **xxx** en el código de HTML.

![Journey Optimizer](./images/oc60.png)

En el menú de la izquierda, haga clic en **Atributos contextuales**. Este contexto se pasa al mensaje desde el recorrido.

Entonces verá esto... Haga clic en la flecha situada junto a **Journey Orchestration** para explorar en profundidad.

![Journey Optimizer](./images/oc601.png)

Haga clic en la flecha situada junto a **Eventos** para explorar en profundidad.

![Journey Optimizer](./images/oc62.png)

Haga clic en la flecha situada junto a `--aepUserLdap--PurchaseEvent` para explorar en profundidad.

![Journey Optimizer](./images/oc63.png)

Haga clic en la flecha situada junto a **productListItems** para explorar en profundidad.

![Journey Optimizer](./images/oc64.png)

Haga clic en el icono **+** junto a **Nombre** para agregarlo al lienzo. Entonces, tendrás esto. Ahora necesita seleccionar **.nombre** como se indica en la siguiente captura de pantalla, y luego debe eliminar **.nombre**.

![Journey Optimizer](./images/oc65.png)

Entonces, tendrás esto. Haga clic en **Guardar**.

![Journey Optimizer](./images/oc66.png)

Ahora volverá a la Designer de correo electrónico. Haga clic en **Guardar** para guardar el progreso.

![Journey Optimizer](./images/oc67.png)

A continuación, ve a **Contenido** y arrastra y suelta un componente **HTML** en la séptima fila. Haga clic en el componente HTML y, a continuación, en **Mostrar el código fuente**.

![Journey Optimizer](./images/oc68.png)

En la ventana emergente **Editar HTML**, pegue este HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Hay 2 referencias de **xxx** en este código de HTML. Ahora tiene que reemplazar cada **xxx** por una referencia al objeto productListItems que forma parte del evento que almacena en déclencheur el recorrido.

![Journey Optimizer](./images/oc69.png)

Primero, elimine el primer **xxx** de su código de HTML.

![Journey Optimizer](./images/oc71.png)

En el menú de la izquierda, haga clic en **Atributos contextuales**.
Haga clic en la flecha situada junto a **Journey Orchestration** para explorar en profundidad.

![Journey Optimizer](./images/oc72.png)

Haga clic en la flecha situada junto a **Eventos** para explorar en profundidad.

![Journey Optimizer](./images/oc722.png)

Haga clic en la flecha situada junto a `--aepUserLdap--PurchaseEvent` para explorar en profundidad.

![Journey Optimizer](./images/oc73.png)

Haga clic en la flecha situada junto a **Commerce** para explorar en profundidad.

![Journey Optimizer](./images/oc733.png)

Haga clic en la flecha situada junto a **Pedido** para explorar en profundidad.

![Journey Optimizer](./images/oc74.png)

Haga clic en el icono **+** junto a **Precio total** para agregarlo al lienzo.

![Journey Optimizer](./images/oc75.png)

Entonces, tendrás esto. Ahora elimina el segundo **xxx** de tu código de HTML.

![Journey Optimizer](./images/oc76.png)

Vuelva a hacer clic en el icono **+** junto a **Precio total** para agregarlo al lienzo.
También puede agregar el campo **Currency** desde el objeto **Order** al lienzo, como puede ver aquí.
Cuando hayas terminado, haz clic en **Guardar** para guardar los cambios.

![Journey Optimizer](./images/oc77.png)

A continuación, volverá a la Designer de correo electrónico. Vuelva a hacer clic en **Guardar**.

![Journey Optimizer](./images/oc78.png)

Vuelva al panel de mensajes haciendo clic en la **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/oc79.png)

Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/oc79a.png)

Haz clic en **Guardar** para cerrar la acción de correo electrónico.

![Journey Optimizer](./images/oc79b.png)

Haga clic en **Publish** para publicar el recorrido.

![Journey Optimizer](./images/oc511.png)

Vuelva a hacer clic en **Publish**.

![Journey Optimizer](./images/oc512.png)

El recorrido se ha publicado.

![Journey Optimizer](./images/oc513.png)

## 3.4.1.5 Actualizar la propiedad de cliente de recopilación de datos de Adobe Experience Platform

Vaya a [Recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/launch/) y seleccione **Etiquetas**.

Esta es la página de Propiedades de recopilación de datos de Adobe Experience Platform que vio antes.

![Página de propiedades](./../../../modules/datacollection/module1.1/images/launch1.png)

En **Introducción**, Demo System creó dos propiedades de cliente para usted: una para el sitio web y otra para la aplicación móvil. Encuéntralos buscando `--aepUserLdap--` en el cuadro **[!UICONTROL Buscar]**. Haga clic para abrir la propiedad **Web**.

![Cuadro de búsqueda](./../../../modules/datacollection/module1.1/images/property6.png)

Vaya a **Elementos de datos**. Busque y abra el elemento de datos **XDM - Purchase**.

![Journey Optimizer](./images/oc91.png)

Entonces verá esto... Vaya al campo **_experience.campaign.orchestration.eventID** y rellene su eventID aquí. El eventID que se va a rellenar aquí es el eventID que creó como parte del ejercicio 3.4.1.1 Haga clic en **Guardar** o en **Guardar en biblioteca**.

![Journey Optimizer](./images/oc92.png)

Guarde los cambios en la propiedad y, a continuación, publique los cambios actualizando la biblioteca de desarrollo.

![Journey Optimizer](./images/oc93.png)

Los cambios se han implementado y se pueden probar.

## 3.4.1.6 Pruebe el correo electrónico de confirmación de pedido en el sitio web de demostración

Probemos el recorrido actualizado comprando un producto en el sitio web de demostración.

Vaya a [https://dsn.adobe.com](https://dsn.adobe.com). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en los 3 puntos **...** del proyecto del sitio web y, a continuación, haga clic en **Ejecutar** para abrirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada ejercicio, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Eche un vistazo al panel Visor de perfiles y al Perfil del cliente en tiempo real con el **ID de Experience Cloud** como identificador principal de este cliente actualmente desconocido.

![Demostración](./../../../modules/datacollection/module1.2/images/pv2.png)

Vaya a la página Registrar/Iniciar sesión. Haga clic en **CREAR UNA CUENTA**.

![Demostración](./../../../modules/datacollection/module1.2/images/pv9.png)

Complete sus detalles y haga clic en **Registrarse** después de lo cual se le redirigirá a la página anterior.

![Demostración](./../../../modules/datacollection/module1.2/images/pv10.png)

Añadir cualquier producto al carro de compras

![Journey Optimizer](./images/cart1a.png)

Vaya a la página **Carro**. Haga clic en **Finalizar compra**.

![Journey Optimizer](./images/cart1.png)

A continuación, compruebe los campos y complete si es necesario. Haga clic en **Continuar**.

![Journey Optimizer](./images/cart2.png)

Haga clic en **Confirmar pedido**.

![Journey Optimizer](./images/cart2a.png)

Su pedido se ha confirmado.

![Journey Optimizer](./images/cart2b.png)

Recibirá el correo electrónico de confirmación del pedido en cuestión de segundos.

![Journey Optimizer](./images/oc98.png)

Ha terminado este ejercicio.

Siguiente paso: [3.4.2 Configuración de un recorrido de boletín basado en lotes](./ex2.md)

[Volver al módulo 3.4](./journeyoptimizer.md)

[Volver a todos los módulos](../../../overview.md)
