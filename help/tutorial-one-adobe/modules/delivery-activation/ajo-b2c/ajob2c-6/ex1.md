---
title: Tarjetas de contenido en Adobe Journey Optimizer
description: Tarjetas de contenido en Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
exl-id: df8402b8-7668-492d-9d82-e89f60fa3c05
source-git-commit: 3661655384d0034f206b6a5c44b8e69205329b2d
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 0%

---

# 3.6.1 Tarjetas de contenido

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Configuración de canal de tarjetas de contenido 3.6.1.1

En el menú de la izquierda, ve a **Canales** y luego selecciona **Configuraciones de canal**. Haga clic en **Crear configuración de canal**.

![Tarjetas de contenido](./images/contentcard1.png)

Escriba el nombre: `--aepUserLdap--_Content_Cards_Web`, seleccione el canal **Tarjetas de contenido** y, a continuación, habilite la plataforma **Web**.

![Tarjetas de contenido](./images/contentcard2.png)

Desplácese hacia abajo y asegúrese de que la opción **Una sola página** esté habilitada.

Escriba la dirección URL del sitio web creado anteriormente como parte del módulo **Introducción**, que tiene el siguiente aspecto: `https://dsn.adobe.com/web/--aepUserLdap---XXXX`. No olvides cambiar el **XXXX** por el código único de tu sitio web.

>[!IMPORTANT]
>
>La referencia anterior a la URL del sitio web de demostración de CitiSignal `https://dsn.adobe.com/web/--aepUserLdap---XXXX` debe cambiarse a la URL real. Para encontrar la dirección URL, ve a tu proyecto de sitio web en [https://dsn.adobe.com/](https://dsn.adobe.com/).

Establezca el campo **Ubicación en la página** en `CitiSignalContentCardContainer`.

![Tarjetas de contenido](./images/contentcard4.png)

Desplácese hacia arriba y haga clic en **Enviar**.

![Tarjetas de contenido](./images/contentcard5.png)

La configuración del canal ya está lista para utilizarse.

![Tarjetas de contenido](./images/contentcard6.png)

## 3.6.1.2 Configurar una campaña programada para las tarjetas de contenido

En el menú de la izquierda, ve a **Campañas** y luego haz clic en **Crear campaña**.

![EnLaAplicación](./images/contentcard7.png)

Seleccione **Programado - Marketing** y haga clic en **Crear**.

![EnLaAplicación](./images/contentcard8.png)

Escriba el nombre `--aepUserLdap-- - CitiSignal Fiber Max Content Cards` y haga clic en **Acciones**.

![EnLaAplicación](./images/contentcard9.png)

Haga clic en **+ Agregar acción** y luego seleccione **Tarjeta de contenido**.

![EnLaAplicación](./images/contentcard10.png)

Seleccione la configuración de canal de tarjetas de contenido que creó en el paso anterior, que se llama: `--aepUserLdap--_Content_Cards_Web`.

A continuación, haga clic en **Editar reglas**.

![EnLaAplicación](./images/contentcard11.png)

Haga clic en **X** para quitar la regla actual.

![EnLaAplicación](./images/contentcard11b.png)

Haga clic en **+ Agregar condición**.

![EnLaAplicación](./images/contentcard11c.png)

Seleccione la condición **Se enviaron los datos a la plataforma**. Haga clic en **Listo**

![EnLaAplicación](./images/contentcard11d.png)

Entonces debería ver esto. Haga clic en **Editar contenido**.

![EnLaAplicación](./images/contentcard11e.png)

Entonces debería ver esto.

![EnLaAplicación](./images/contentcard12.png)

Configure las siguientes opciones:

- **Título**: `CitiSignal Fiber Max`
- **Cuerpo**: `Lightning speed for gamers`
- **URL de destino**: `https://dsn.adobe.com/web/--aepUserLdap---XXXX/plans`

>[!IMPORTANT]
>
>La referencia anterior a la URL del sitio web de demostración de CitiSignal `https://dsn.adobe.com/web/--aepUserLdap---XXXX/plans` debe cambiarse a la URL real. Para encontrar la dirección URL, ve a tu proyecto de sitio web en [https://dsn.adobe.com/](https://dsn.adobe.com/).

Haga clic en el icono para cambiar la dirección URL seleccionando un recurso de los AEM Assets.

![EnLaAplicación](./images/contentcard13.png)

Vaya a la carpeta **citisignal-images** y seleccione el archivo **`neon_rabbit_banner.jpg`**. Haga clic en **Seleccionar**.

![EnLaAplicación](./images/contentcard14.png)

Entonces deberías tener esto. Haga clic en **+ botón Agregar**.

![EnLaAplicación](./images/contentcard15.png)

Configure las siguientes opciones para el botón:

- **Título de botón**: `Upgrade now!`
- **Evento de interacción**: `click`
- **Destino**: `https://dsn.adobe.com/web/--aepUserLdap---XXXX/plans`

>[!IMPORTANT]
>
>La referencia anterior a la URL del sitio web de demostración de CitiSignal `https://dsn.adobe.com/web/--aepUserLdap---XXXX/plans` debe cambiarse a la URL real. Para encontrar la dirección URL, ve a tu proyecto de sitio web en [https://dsn.adobe.com/](https://dsn.adobe.com/).

Haga clic en **Revisar para activar**.

![EnLaAplicación](./images/contentcard16.png)

Haga clic en **Activar**.

![EnLaAplicación](./images/contentcard17.png)

La campaña se activará, lo que puede tardar un par de minutos.

![EnLaAplicación](./images/contentcard18.png)

Después de un par de minutos, la campaña estará activa.

![EnLaAplicación](./images/contentcard19.png)

## 3.6.1.3 Actualizar el sitio web de DSN

Para mostrar la tarjeta de contenido en el sitio web, debe realizar un cambio en el diseño de la página principal del sitio web de demostración de CitiSignal.

Vaya a [https://dsn.adobe.com/](https://dsn.adobe.com/). Haz clic en los **3 puntos** de tu sitio web y haz clic en **Editar**.

![EnLaAplicación](./images/contentcard20.png)

Haga clic para seleccionar la página **Inicio**. Haga clic en **Editar contenido**.

![EnLaAplicación](./images/contentcard21.png)

Pase el ratón sobre la imagen a pantalla completa y haga clic en el botón **+**.

![EnLaAplicación](./images/contentcard22.png)

Vaya a **General**, seleccione **Banner** y haga clic en **Agregar**.

![EnLaAplicación](./images/contentcard23.png)

Haga clic en para seleccionar el titular recién creado. Vaya a **Estilo** e introduzca `CitiSignalContentCardContainer` en el campo **Clases CSS personalizadas**.

![EnLaAplicación](./images/contentcard24.png)

Ir a **Alineación**. Establezca el campo **Alignment** en `left` y establezca el campo **Vertical Alignment** en `middle`.

Haga clic en el icono **X** para cerrar la ventana de diálogo.

![EnLaAplicación](./images/contentcard25.png)

Se han realizado los cambios en el diseño del sitio web.

Si abre el sitio en una nueva ventana del explorador ahora, debería tener este aspecto. el área gris es el titular recién creado, pero aún no tiene ningún contenido.

![EnLaAplicación](./images/contentcard25a.png)

Para asegurarse de que el contenido se carga dinámicamente en el banner recién creado, es necesario realizar un cambio en la propiedad Etiquetas de recopilación de datos.

## 3.6.1.4: actualizar la propiedad de etiquetas de recopilación de datos

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), a **Etiquetas**. Como parte del módulo [Introducción](./../../../../modules/getting-started/gettingstarted/ex1.md), se crearon las propiedades de Etiquetas de recopilación de datos.

Ya ha estado utilizando estas propiedades de etiquetas de recopilación de datos como parte de módulos anteriores.

Haga clic para abrir la propiedad Recopilación de datos para la web.

![DSN](./images/launchprop.png)

En el menú de la izquierda, ve a **Reglas** y haz clic para abrir la regla **Vista de página**.

![EnLaAplicación](./images/contentcard101.png)

Haga clic en la acción **Enviar evento de experiencia &quot;Vista de página&quot;**.

![EnLaAplicación](./images/contentcard102.png)

Como parte de la regla **Vista de página**, es necesario solicitar las instrucciones de personalización de Edge para una superficie específica. La superficie es el titular que configuró en el paso anterior. Para ello, desplácese hacia abajo hasta **Personalization** e introduzca `web://dsn.adobe.com/web/--aepUserLdap---XXXX#CitiSignalContentCardContainer` en **Superficies**.

>[!IMPORTANT]
>
>La referencia anterior a la URL del sitio web de demostración de CitiSignal `web://dsn.adobe.com/web/--aepUserLdap---XXXX#CitiSignalContentCardContainer` debe cambiarse a la URL real. Para encontrar la dirección URL, ve a tu proyecto de sitio web en [https://dsn.adobe.com/](https://dsn.adobe.com/).

Haga clic en **Conservar cambios**.

![EnLaAplicación](./images/contentcard103.png)

Haga clic en **Guardar** o en **Guardar en biblioteca**.

![EnLaAplicación](./images/contentcard104.png)


En el menú de la izquierda, ve a **Reglas** y haz clic en **Agregar regla**.

![EnLaAplicación](./images/contentcard26.png)

Escriba el nombre: `Display AJO Content Cards`. Haga clic en **+ Agregar** para agregar un nuevo evento.

![EnLaAplicación](./images/contentcard27.png)

Seleccione la **extensión**: **Adobe Experience Platform Web SDK** y, a continuación, seleccione **Tipo de evento**: **Suscribir elementos del conjunto de reglas**.

En **Esquemas**, seleccione **Tarjeta de contenido**.

En **Superficies**, escriba `web://dsn.adobe.com/web/--aepUserLdap---XXXX#CitiSignalContentCardContainer`

>[!IMPORTANT]
>
>La referencia anterior a la URL del sitio web de demostración de CitiSignal `web://dsn.adobe.com/web/--aepUserLdap---XXXX#CitiSignalContentCardContainer` debe cambiarse a la URL real. Para encontrar la dirección URL, ve a tu proyecto de sitio web en [https://dsn.adobe.com/](https://dsn.adobe.com/).

Haga clic en **Conservar cambios**.

![EnLaAplicación](./images/contentcard28.png)

Entonces debería ver esto. Haga clic en **+ Agregar** para agregar una acción nueva.

![EnLaAplicación](./images/contentcard29.png)

Seleccione la **extensión**: **Core** y seleccione el **Tipo de acción**: **Código personalizado**.

Habilite la casilla de verificación para **Idioma**: **JavaScript** y luego haga clic en **Abrir editor**.

![EnLaAplicación](./images/contentcard30.png)

A continuación, debería ver una ventana de editor vacía.

![EnLaAplicación](./images/contentcard31.png)

Pegue el siguiente código en el editor y haga clic en **Guardar**.

```javascript
if (!Array.isArray(event.propositions)) {
  console.log("No personalization content");
  return;
}

console.log(">>> Content Card response from Edge: ", event.propositions);

event.propositions.forEach(function (payload) {
  payload.items.forEach(function (item) {
    if (!item.data || !item.data.content || item.data.content === "undefined") {
      return;
    }
    console.log(">>> Content Card response from Edge: ", item);
    const { content } = item.data;
    const { title, body, image, buttons } = content;
    const titleValue = title.content;
    const description = body.content;
    const imageUrl = image.url;
    const buttonLabel = buttons[0]?.text.content;
    const buttonLink = buttons[0]?.actionUrl;
    const html = `<div  class="Banner Banner--alignment-left Banner--verticalAlignment-left hero-banner ContentCardContainer"  oxygen-component-id="cmp-0"  oxygen-component="Banner"  role="presentation"  style="color: rgb(255, 255, 255); height: 60%;">  <div class="Image" role="presentation">    <img src="${imageUrl}" style="object-fit: cover; height: 100%"    />  </div>  <div class="Banner__content">    <div class="Title Title--alignment-left Title--textAlignment-left">      <div class="Title__content" role="presentation">        <strong class="Title__pretitle">${titleValue}</strong>        <h2>${description}</h2>      </div>    </div>    <div class="Button Button--alignment-left Button--variant-cta">              <button          class="Dniwja_spectrum-Button Dniwja_spectrum-BaseButton Dniwja_i18nFontFamily Dniwja_spectrum-FocusRing Dniwja_spectrum-FocusRing-ring"          type="button"          data-variant="accent"          data-style="fill"          onclick="window.open('${buttonLink}')"       style="color:#FFFFFF;padding: 12px 28px;font-size: 24px;font-family: adobe-clean;font-weight: bolder;" >          <span            id="react-aria5848951631-49"            class="Dniwja_spectrum-Button-label"            >${buttonLabel}</span          >        </button>            </div>  </div></div>`;
    if (document.querySelector(".CitiSignalContentCardContainer")) {
      const contentCardContainer = document.querySelector(
        ".CitiSignalContentCardContainer"
      );
      contentCardContainer.innerHTML = html;
      contentCardContainer.style.height = "60%";
    }
  });
});
```

![EnLaAplicación](./images/contentcard32.png)

Haga clic en **Conservar cambios**.

![EnLaAplicación](./images/contentcard33.png)

Haga clic en **Guardar** o en **Guardar en biblioteca**.

![EnLaAplicación](./images/contentcard34.png)

En el menú de la izquierda, ve a **Flujo de publicación** y haz clic para abrir la biblioteca **Principal**.

![EnLaAplicación](./images/contentcard35.png)

Haga clic en **Agregar todos los recursos modificados** y, a continuación, haga clic en **Guardar y generar en desarrollo**.

![EnLaAplicación](./images/contentcard36.png)

## 3.6.1.5 Probar la tarjeta de contenido en el sitio web

Vaya a [https://dsn.adobe.com](https://dsn.adobe.com). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en los 3 puntos **...** del proyecto del sitio web y, a continuación, haga clic en **Ejecutar** para abrirlo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Ahora debería ver el sitio web de CitiSignal que se está cargando, y la tarjeta de contenido que configuró debería mostrarse en lugar del área gris vacía que tenía antes.

![EnLaAplicación](./images/contentcard37.png)

## Pasos siguientes

Ir a [3.6.2 páginas de aterrizaje](./ex2.md)

Volver a [Adobe Journey Optimizer: administración de contenido](./ajocontent.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
