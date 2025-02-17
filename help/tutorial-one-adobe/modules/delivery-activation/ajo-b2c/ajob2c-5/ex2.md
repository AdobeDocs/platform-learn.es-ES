---
title: Cree su campaña con los servicios de traducción de AJO
description: Cree su campaña con los servicios de traducción de AJO
kt: 5342
doc-type: tutorial
exl-id: 536caf45-c614-48e8-adbb-6dc67d1a9606
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# 3.5.2 Creación de la campaña

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/). Haga clic en **Journey Optimizer**.

![Traducciones](./images/ajolp1.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`.

![ACOP](./images/ajolp2.png)

>[!NOTE]
>
>Si ya ha creado los fragmentos Encabezado y Pie de página como parte del ejercicio [ejercicio 3.1.2.1](./../ajob2c-1/ex2.md) y el [ejercicio 3.1.2.2](./../ajob2c-1/ex2.md), vaya al ejercicio 3.5.2.3 Crear campaña de fibra. No vuelva a crear los fragmentos Encabezado y Pie de página.

## 3.5.2.1 Crear el fragmento de encabezado

En el menú de la izquierda, haga clic en **Fragmentos**. Un fragmento es un componente reutilizable dentro de Journey Optimizer, que evita la duplicación y facilita los cambios futuros que deberían afectar a todos los mensajes, como los cambios en un encabezado o pie de página de un mensaje de correo electrónico.

Haga clic en **Crear fragmento**.

![ACOP](./images/fragm1.png)

Escriba el nombre `--aepUserLdap-- - CitiSignal - Header` y seleccione **Tipo: Fragmento visual**. Haga clic en **Crear**.

![ACOP](./images/fragm2.png)

Entonces verá esto... En el menú de la izquierda, encontrará los componentes de estructura que puede utilizar para definir la estructura del correo electrónico (filas y columnas).

Arrastre y suelte una columna **1:1** del menú en el lienzo. Este será el marcador de posición de la imagen del logotipo.

![Journey Optimizer](./images/fragm3.png)

A continuación, puede utilizar Componentes de contenido para añadir contenido dentro de estos bloques. Arrastre y suelte un componente **Image** en la primera celda de la primera fila. Haga clic en **Examinar**.

![Journey Optimizer](./images/fragm4.png)

A continuación, verá una ventana emergente que muestra la biblioteca multimedia de AEM Assets. Vaya a la carpeta **citi-signal-images**, haga clic para seleccionar la imagen **CitiSignal-Logo-White.png** y haga clic en **Seleccionar**.

>[!NOTE]
>
>Si no ves las imágenes de Citi Signal en tu biblioteca de AEM Assets, puedes encontrarlas [aquí](./../../../../assets/ajo/CitiSignal-images.zip). Descárguelas en su escritorio, cree la carpeta **citi-signal-images** y cargue todas las imágenes de esa carpeta.

![Journey Optimizer](./images/fragm5.png)

Entonces verá esto... La imagen es blanca y aún no se muestra. Ahora debe definir un color de fondo para que la imagen se muestre correctamente. Haga clic en **Estilos** y luego haga clic en el cuadro **Color de fondo**.

![Journey Optimizer](./images/fragm6.png)

En la ventana emergente, cambie el código de color **Hex** a **#8821F4** y, a continuación, cambie el enfoque haciendo clic en el campo **100%**. Luego verá el nuevo color aplicado a la imagen.

![Journey Optimizer](./images/fragm7.png)

La imagen también es un poco demasiado grande en este momento. Cambiemos la anchura deslizando el conmutador **Width** a **40%**.

![Journey Optimizer](./images/fragm8.png)

El fragmento de encabezado ya está listo. Haz clic en **Guardar** y luego haz clic en la flecha para volver a la pantalla anterior.

![Journey Optimizer](./images/fragm9.png)

El fragmento debe publicarse para poder utilizarse. Haga clic en **Publicar**.

![Journey Optimizer](./images/fragm10.png)

Después de un par de minutos, verás que el estado de tu fragmento ha cambiado a **Activo**.
A continuación, debe crear un nuevo fragmento para el pie de página de los mensajes de correo electrónico. Haga clic en **Crear fragmento**.

![Journey Optimizer](./images/fragm11.png)

## 3.5.2.2 Crear el fragmento Pie de página

Haga clic en **Crear fragmento**.

![Journey Optimizer](./images/fragm11.png)

Escriba el nombre `--aepUserLdap-- - CitiSignal - Footer` y seleccione **Tipo: Fragmento visual**. Haga clic en **Crear**.

![Journey Optimizer](./images/fragm12.png)

Entonces verá esto... En el menú de la izquierda, encontrará los componentes de estructura que puede utilizar para definir la estructura del correo electrónico (filas y columnas).

Arrastre y suelte una columna **1:1** del menú en el lienzo. Este será el marcador de posición para el contenido del pie de página.

![Journey Optimizer](./images/fragm13.png)

A continuación, puede utilizar Componentes de contenido para añadir contenido dentro de estos bloques. Arrastre y suelte un componente **HTML** en la primera celda de la primera fila. Haga clic en el componente para seleccionarlo y, a continuación, haga clic en el icono **&lt;/>** para editar el código fuente de HTML.

![Journey Optimizer](./images/fragm14.png)

Entonces verá esto...

![Journey Optimizer](./images/fragm15.png)

Copie el siguiente fragmento de código de HTML y péguelo en la ventana **Editar HTML** de Journey Optimizer.

```html
<!--[if mso]><table cellpadding="0" cellspacing="0" border="0" width="100%"><tr><td style="text-align: center;" ><![endif]-->
<table style="width: auto; display: inline-block;">
  <tbody>
    <tr class="component-social-container">
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.facebook.com" data-component-social-icon-id="facebook">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://x.com" data-component-social-icon-id="twitter">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.instagram.com" data-component-social-icon-id="instagram">
         
        </a>
      </td>
    </tr>
  </tbody>
</table>
<!--[if mso]></td></tr></table><![endif]-->
```

Entonces, tendrás esto. En las líneas 7, 12 y 17, ahora debe insertar un archivo de imagen con los recursos de la biblioteca de AEM Assets.

![Journey Optimizer](./images/fragm16.png)

Asegúrese de que el cursor se encuentra en la línea 7 y luego haga clic en **Assets** en el menú de la izquierda. Haga clic en **Abrir selector de recursos** para seleccionar la imagen.

![Journey Optimizer](./images/fragm17.png)

Abra la carpeta **citi-signal-images** y haga clic para seleccionar la imagen **Icon_Facebook.png**. Haga clic en **Seleccionar**.

![Journey Optimizer](./images/fragm18.png)

Asegúrese de que el cursor se encuentra en la línea 12 y luego haga clic en **Abrir selector de recursos** para seleccionar la imagen.

![Journey Optimizer](./images/fragm19.png)

Abra la carpeta **citi-signal-images** y haga clic para seleccionar la imagen **Icon_X.png**. Haga clic en **Seleccionar**.

![Journey Optimizer](./images/fragm20.png)

Asegúrese de que el cursor se encuentra en la línea 17 y, a continuación, haga clic en **Abrir selector de recursos** para seleccionar la imagen.

![Journey Optimizer](./images/fragm21.png)

Abra la carpeta **citi-signal-images** y haga clic para seleccionar la imagen **Icon_Instagram.png**. Haga clic en **Seleccionar**.

![Journey Optimizer](./images/fragm22.png)

Entonces verá esto... Haga clic en **Guardar**.

![Journey Optimizer](./images/fragm23.png)

Luego volverás a estar en el editor. Los iconos aún no están visibles porque el fondo y los archivos de imagen están todos en blanco. Para cambiar el color de fondo, ve a **Estilos** y haz clic en la casilla de verificación **Color de fondo**.

![Journey Optimizer](./images/fragm24.png)

Cambie el código de color **Hex** a **#000000**.

![Journey Optimizer](./images/fragm25.png)

Cambie la alineación para que esté centrada.

![Journey Optimizer](./images/fragm26.png)

Vamos a agregar otras partes al pie de página. Arrastre y suelte un componente **Image** sobre el componente de HTML que acaba de crear. Haga clic en **Examinar**.

![Journey Optimizer](./images/fragm27.png)

Haga clic para seleccionar el archivo de imagen **`CitiSignal_Footer_Logo.png`** y haga clic en **Seleccionar**.

![Journey Optimizer](./images/fragm28.png)

Vaya a **Estilos** y haga clic en la casilla de verificación **Color de fondo**; cambiémosla a negro otra vez. Cambie el código de color **Hex** a **#000000**.

![Journey Optimizer](./images/fragm29.png)

Cambie la anchura a **20%** y compruebe que la alineación esté centrada.

![Journey Optimizer](./images/fragm30.png)

A continuación, arrastre y suelte un componente **Text** en el componente de HTML que creó. Haga clic en **Examinar**.

![Journey Optimizer](./images/fragm31.png)

Copie y pegue el texto siguiente reemplazando el texto del marcador de posición.

```
1234 N. South Street, Anywhere, US 12345

Unsubscribe

©2024 CitiSignal, Inc and its affiliates. All rights reserved.
```

Establezca la **alineación del texto** en el centro.

![Journey Optimizer](./images/fragm32.png)

Cambiar **color de fuente** a blanco, **#FFFFFF**.

![Journey Optimizer](./images/fragm33.png)

Cambiar el **color de fondo** a negro, **#000000**.

![Journey Optimizer](./images/fragm34.png)

Seleccione el texto **Cancelar la suscripción** en el pie de página y haga clic en el icono **Vínculo** de la barra de menús. Establezca **Type** en **Exclusión/baja externa** y establezca la dirección URL en **https://aepdemo.net/unsubscribe.html** (no se permite tener una dirección URL en blanco para el vínculo de cancelación de suscripción).

![Journey Optimizer](./images/fragm35.png)

Entonces, tendrás esto. El pie de página ya está listo. Haz clic en **Guardar** y luego haz clic en la flecha para volver a la página anterior.

![Journey Optimizer](./images/fragm36.png)

Haga clic en **Publicar** para publicar el pie de página y utilizarlo en un mensaje de correo electrónico.

![Journey Optimizer](./images/fragm37.png)

Después de un par de minutos, verás que el estado del pie de página ha cambiado a **Activo**.

![Journey Optimizer](./images/fragm38.png)

## 3.5.2.3 Creación de una campaña de fibra

Ahora creará una campaña. A diferencia del recorrido basado en eventos del ejercicio anterior, que se basa en eventos de experiencia entrantes o entradas o salidas de audiencia para almacenar en déclencheur un recorrido para un cliente específico, las campañas se dirigen a una audiencia completa una vez con contenido único como boletines informativos, promociones únicas o información genérica, o periódicamente con contenido similar enviado de forma regular como, por ejemplo, campañas de cumpleaños y recordatorios.

En el menú, ve a **Campañas** y haz clic en **Crear campaña**.

![Journey Optimizer](./images/oc43.png)

Seleccione **Programado - Marketing** y haga clic en **Crear**.

![Journey Optimizer](./images/campaign1.png)

En la pantalla de creación de campañas, configure lo siguiente:

- **Nombre**: `--aepUserLdap-- - CitiSignal Fiber`.
- **Descripción**: campaña de fibra
- **Tipo de identidad**: cambiar a Correo electrónico

![Journey Optimizer](./images/campaign2.png)

Desplácese hacia abajo hasta **Acción**. Para la **acción**, seleccione **correo electrónico**.

![Journey Optimizer](./images/campaign3.png)

A continuación, seleccione una **configuración de correo electrónico** existente. Editará el contenido en un par de minutos.

![Journey Optimizer](./images/campaign3a.png)

Desplácese hasta **Audiencia**. Haga clic en **Seleccionar audiencia**.

![Journey Optimizer](./images/campaign2b.png)

Para la **audiencia**, seleccione la audiencia que creó en [1.3.3 Crear una composición federada](./../../datacollection/dc1.3/ex3.md), que se denomina `--aepUserLdap-- - CitiSignal Eligible for Fiber`. Haga clic en **Guardar**.

![Journey Optimizer](./images/campaign2a.png)

Desplácese hacia abajo hasta **Programar**. Para el **horario**, elige **En una fecha y hora específicas** y establece una hora de elección.

![Journey Optimizer](./images/campaign4.png)

Ahora puede empezar a crear el propio mensaje de correo electrónico. Desplácese hacia arriba y haga clic en **Editar contenido**.

![Journey Optimizer](./images/campaign5.png)

Entonces verá esto... Para la **línea de asunto**, use esto:

```
{{profile.person.name.firstName}}, here's your Fiber offer!
```

A continuación, haga clic en **Editar cuerpo del correo electrónico**.

![Journey Optimizer](./images/campaign6.png)

Elija **Diseño desde cero**.

![Journey Optimizer](./images/campaign7.png)

Entonces verá esto... En el menú de la izquierda, encontrará los componentes de estructura que puede utilizar para definir la estructura del correo electrónico (filas y columnas).

Arrastrar y soltar 4 veces una columna **1:1** en el lienzo, lo que debería proporcionarle esta estructura:

![Journey Optimizer](./images/campaign8.png)

En el menú de la izquierda, ve a **Fragmentos**. Arrastre el encabezado que creó anteriormente al primer componente del lienzo. Arrastre el pie de página creado anteriormente hasta el último componente del lienzo.

![Journey Optimizer](./images/campaign9.png)

Haga clic en el icono **+** en el menú de la izquierda. Vaya a **Contenido** para empezar a agregar contenido al lienzo.

![Journey Optimizer](./images/campaign10.png)

Arrastre y suelte un componente **Text** en la segunda fila.

![Journey Optimizer](./images/campaign11.png)

Seleccione el texto predeterminado en ese componente **Escriba el texto aquí.** y reemplácelo por el siguiente texto. Cambie la alineación a **Alineación central**.

```javascript
Hi {{profile.person.name.firstName}}

As a CitiSignal customer, you're in pole position to discover our new Fiber offering. Have a look at the below offer and update your contract!

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

Arrastre y suelte un componente **Image** en la tercera fila. Haga clic en **Examinar**.

![Journey Optimizer](./images/campaign13.png)

Seleccione el repositorio de AEM Assets que creó como parte de módulos anteriores. Ese repositorio debe llamarse `--aepUserLdap-- - Citi Signal dev`. Haga clic para abrir la carpeta `--aepUserLdap-- - Workfront Assets`.

![Journey Optimizer](./images/campaign15a.png)

Haga clic para seleccionar la imagen **2048x2048_buynow.png** y luego haga clic en **Seleccionar**.

![Journey Optimizer](./images/campaign14.png)

El correo electrónico básico de la newsletter ya está listo. Haga clic en **Guardar**.

![Journey Optimizer](./images/ready.png)

Vuelva al panel de campañas haciendo clic en la **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/campaign19.png)

Haga clic en **Revisar para activar**.

![Journey Optimizer](./images/campaign20.png)

Entonces puede obtener este error. Si es así, es posible que tenga que esperar hasta 24 horas hasta que se haya evaluado la audiencia y luego intentar activar la campaña de nuevo. También es posible que tenga que actualizar la programación de la campaña para que se ejecute más adelante.

![Journey Optimizer](./images/campaign21a.png)

Haga clic en **Activar**.

![Journey Optimizer](./images/campaign21.png)

Una vez activada, la campaña se programará para ejecutarse.

![Journey Optimizer](./images/campaign22.png)

Ha terminado este ejercicio.

## Pasos siguientes

Ir a [3.5.3 Agregar idiomas a tu correo electrónico](./ex3.md)

Volver a [Adobe Journey Optimizer: servicios de traducción](./ajotranslationsvcs.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
