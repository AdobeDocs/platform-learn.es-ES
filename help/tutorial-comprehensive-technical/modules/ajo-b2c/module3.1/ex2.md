---
title: Journey Optimizer Cree su recorrido y mensaje de correo electrónico
description: Journey Optimizer Cree su mensaje de correo electrónico
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# 3.1.2 Crear el recorrido y el mensaje de correo electrónico

En este ejercicio, configurará el recorrido y el mensaje que debe activarse cuando alguien cree una cuenta en el sitio web de demostración.

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Para cambiar de una zona protegida a otra, haga clic en **PRODUCTION Prod (VA7)** y seleccione la zona protegida en la lista. En este ejemplo, la zona protegida se denomina **Habilitación de AEP para el año fiscal 22**. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

## 3.1.2.1 Creación de un recorrido

En el menú de la izquierda, haga clic en **Recorridos**. A continuación, haga clic en **Crear Recorrido** para crear un nuevo recorrido.

![ACOP](./images/createjourney.png)

A continuación, verá una pantalla de recorrido vacía.

![ACOP](./images/journeyempty.png)

En el ejercicio anterior creó un nuevo **evento**. Le puso este nombre `ldapAccountCreationEvent` y reemplazó `ldap` por su LDAP. Este fue el resultado de la creación del Evento:

![ACOP](./images/eventdone.png)

Ahora debe tomar este evento como inicio de este Recorrido. Para ello, vaya al lado izquierdo de la pantalla y busque el evento en la lista de eventos.

![ACOP](./images/eventlist.png)

Seleccione el evento, arrástrelo y suéltelo en el lienzo de Recorrido. El Recorrido ahora tiene este aspecto:

![ACOP](./images/journeyevent.png)

Como segundo paso en el recorrido, debe agregar un breve paso **Wait**. Vaya al lado izquierdo de la pantalla a la sección **Orchestration** para encontrarlo. Utilizará atributos de perfil y debe asegurarse de que se rellenan en el Perfil del cliente en tiempo real.

![ACOP](./images/journeywait.png)

Su recorrido ahora tiene este aspecto. En el lado derecho de la pantalla debe configurar el tiempo de espera. Configúrelo en 1 minuto. Esto le dará tiempo suficiente para que los atributos de perfil estén disponibles después de que se active el evento.

![ACOP](./images/journeywait1.png)

Haga clic en **Aceptar** para guardar los cambios.

Como tercer paso del recorrido, debes agregar una acción **Correo electrónico**. Vaya al lado izquierdo de la pantalla a **Actions**, seleccione la acción **Email** y arrástrela y suéltela en el segundo nodo del recorrido. Ahora puede ver esto.

![ACOP](./images/journeyactions.png)

Defina **Category** en **Marketing** y seleccione una superficie de correo electrónico que le permita enviar correo electrónico. En este caso, la superficie de correo electrónico que se va a seleccionar es **Correo electrónico**. Asegúrese de que las casillas de verificación de **Clics en el correo electrónico** y **aperturas del correo electrónico** estén habilitadas.

![ACOP](./images/journeyactions1.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

## 3.1.2.2 Crear el mensaje

Para crear tu mensaje, haz clic en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

Ahora puede ver esto.

![ACOP](./images/journeyactions3.png)

Haga clic en el campo de texto **Línea de asunto**.

![Journey Optimizer](./images/msg5.png)

Empiece a escribir **Hola** en el área de texto

![Journey Optimizer](./images/msg6.png)

La línea de asunto aún no ha finalizado. A continuación, debe traer el token de personalización para el campo **Nombre** que se almacena en `profile.person.name.firstName`. En el menú de la izquierda, desplácese hacia abajo para encontrar el elemento **Person** y haga clic en la flecha para ir un nivel más profundo.

![Journey Optimizer](./images/msg7.png)

Ahora encuentra el elemento **Nombre completo** y haz clic en la flecha para ir un nivel más profundo.

![Journey Optimizer](./images/msg8.png)

Finalmente, busque el campo **Nombre** y haga clic en el signo **+** que está al lado. A continuación, verá aparecer el token de personalización en el campo de texto.

![Journey Optimizer](./images/msg9.png)

A continuación, agregue el texto **, ¡gracias por registrarse!**. Haga clic en **Guardar**.

![Journey Optimizer](./images/msg10.png)

Entonces volverás a estar aquí. Haga clic en **Enviar correo electrónico a Designer** para crear el contenido del correo electrónico.

![Journey Optimizer](./images/msg11.png)

En la siguiente pantalla, se le solicitarán tres métodos diferentes para proporcionar el contenido del correo electrónico:

- **Diseñe desde cero**: Comience con un lienzo en blanco y utilice el editor de WYSIWYG para arrastrar y soltar los componentes de estructura y contenido y así crear visualmente el contenido del correo electrónico.
- **Codifique su propia**: cree su propia plantilla de correo electrónico codificándola con el HTML
- **HTML de importación**: importe una plantilla de HTML existente que podrá editar.

Haga clic en **Diseñar desde cero**.

![Journey Optimizer](./images/msg12.png)

En el menú de la izquierda, encontrará los componentes de estructura que puede utilizar para definir la estructura del correo electrónico (filas y columnas).

![Journey Optimizer](./images/msg13.png)

Arrastre y suelte una columna **1:2 Left** del menú en el lienzo. Este será el marcador de posición de la imagen del logotipo.

![Journey Optimizer](./images/msg14.png)

Arrastre y suelte una columna **1:1** debajo del componente anterior. Este será el bloque de banner.

![Journey Optimizer](./images/msg15.png)

Arrastre y suelte una columna **1:2 Left** debajo del componente anterior. Este será el contenido real con una imagen en el lado izquierdo y texto en el lado derecho.

![Journey Optimizer](./images/msg16.png)

A continuación, arrastre y suelte una columna **1:1** debajo del componente anterior. Este será el pie de página del correo electrónico. El lienzo debería tener un aspecto similar al siguiente:

![Journey Optimizer](./images/msg17.png)

A continuación, vamos a utilizar los componentes de contenido para añadir contenido dentro de estos bloques. Haga clic en el elemento de menú **Componentes de contenido**

![Journey Optimizer](./images/msg18.png)

Arrastre y suelte un componente **Image** en la primera celda de la primera fila. Haga clic en **Examinar**.

![Journey Optimizer](./images/msg19.png)

Entonces verá esto... Vaya a la carpeta **enablement-assets** y seleccione el archivo **luma-logo.png**. Haga clic en **Seleccionar**.

![Journey Optimizer](./images/msg21.png)

Ahora estás de vuelta aquí:

![Journey Optimizer](./images/msg25.png)

Vaya a **Componentes de contenido** y arrastre y suelte un componente **Imagen** en la primera celda de la primera fila. Haga clic en **Examinar**.

![Journey Optimizer](./images/msg26.png)

En la ventana emergente **Assets**, ve a la carpeta **enablement-assets**. En esta carpeta encontrará todos los recursos preparados y cargados previamente por el equipo creativo. Seleccione **module23-thank-you-new.png** y haga clic en **Seleccionar**.

![Journey Optimizer](./images/msg28.png)

A continuación, tendrá esto:

![Journey Optimizer](./images/msg30.png)

Seleccione la imagen y, en el menú de la derecha, desplácese hacia abajo hasta que vea el componente deslizador de anchura **Size**. Utilice el regulador para cambiar la anchura a f.i. **60 %**.

![Journey Optimizer](./images/msg31.png)

A continuación, vaya a **Componentes de contenido** y arrastre y suelte un componente **Texto** en el componente de estructura en la cuarta fila.

![Journey Optimizer](./images/msg33.png)

Seleccione el texto predeterminado **Escriba el texto aquí.** como lo haría con cualquier editor de texto. Escriba **Estimado** en su lugar. Observe la barra de herramientas de texto que se muestra cuando está en modo de texto.

![Journey Optimizer](./images/msg34.png)

En la barra de herramientas, haga clic en el icono **Agregar personalización**.

![Journey Optimizer](./images/msg35.png)

A continuación, debe traer el token de personalización **First name** que se almacena en `profile.person.name.firstName`. En el menú, busque el elemento **Person**, explore en profundidad el elemento **Nombre completo** y, a continuación, haga clic en el icono **+** para agregar el campo Nombre al editor de expresiones.

Haga clic en **Guardar**.

![Journey Optimizer](./images/msg36.png)

Ahora notará cómo se ha agregado el campo de personalización al texto.

![Journey Optimizer](./images/msg37.png)

En el mismo campo de texto, presione **Entrar** dos veces para agregar dos líneas y escriba **Gracias por crear su cuenta con Luma!**.

![Journey Optimizer](./images/msg38.png)

La última comprobación que debes realizar para asegurarte de que el correo electrónico esté listo es previsualizarlo, haz clic en el botón **Simular contenido**.

![Journey Optimizer](./images/msg50.png)

Comience por identificar qué perfil desea utilizar para la vista previa. Seleccione el área de nombres **email** haciendo clic en el icono situado junto al campo **Introducir área de nombres de identidad**.

En la lista de áreas de nombres de identidad, seleccione el área de nombres **Email**.

En el campo **Valor de identidad**, escriba la dirección de correo electrónico de un perfil de demostración anterior que ya esté almacenado en el Perfil del cliente en tiempo real. Por ejemplo **woutervangeluwe+06022022-01@gmail.com** y haga clic en el botón **Buscar perfil de prueba**

![Journey Optimizer](./images/msg53.png)

Una vez que el perfil aparezca en la tabla, haga clic en la ficha **Vista previa** para obtener acceso a la pantalla de vista previa.

Cuando la vista previa esté lista, compruebe que la personalización es correcta en la línea de asunto, el texto del cuerpo y el vínculo de baja se resaltan como un hipervínculo.

Haga clic en **Cerrar** para cerrar la vista previa.

![Journey Optimizer](./images/msg54.png)

Haz clic en **Guardar** para guardar el mensaje.

![Journey Optimizer](./images/msg55.png)

Vuelva al panel de mensajes haciendo clic en la **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/msg56.png)

Ha completado la creación del correo electrónico de registro. Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/msg57.png)

Haga clic en **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 3.1.2.3 Publish su recorrido

Aún necesita darle un Nombre a su recorrido. Para ello, haga clic en el icono **Propiedades** en la parte superior derecha de la pantalla.

![ACOP](./images/journeyname.png)

A continuación, puede introducir el nombre del recorrido aquí. Use `--aepUserLdap-- - Account Creation Journey`. Haga clic en **Aceptar** para guardar los cambios.

![ACOP](./images/journeyname1.png)

Ahora puede publicar su recorrido haciendo clic en **Publish**.

![ACOP](./images/publishjourney.png)

Vuelva a hacer clic en **Publish**.

![ACOP](./images/publish1.png)

A continuación, verá una barra de confirmación verde que indica que el recorrido se ha publicado.

![ACOP](./images/published.png)

Ya ha terminado este ejercicio.

Paso siguiente: [3.1.3 Actualice la propiedad de recopilación de datos y pruebe su recorrido](./ex3.md)

[Volver al módulo 3.1](./journey-orchestration-create-account.md)

[Volver a todos los módulos](../../../overview.md)
