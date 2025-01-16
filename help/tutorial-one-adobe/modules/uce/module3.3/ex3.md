---
title: 'Offer decisioning: Pruebe la decisión'
description: 'Offer decisioning: Pruebe la decisión'
kt: 5342
doc-type: tutorial
source-git-commit: a1cba79313a651c929d76008943c1c5f8a64a9f7
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---

# 3.3.3 Preparar la propiedad del cliente de recopilación de datos de Adobe Experience Platform y la configuración de Web SDK para el Offer decisioning

## 3.3.3.1 Actualizar la secuencia de datos

En [Introducción](./../../../modules/getting-started/gettingstarted/ex2.md), creó su propia **secuencia de datos**. Luego usó el nombre `--aepUserLdap-- - Demo System Datastream`.

En este ejercicio, debe configurar ese **conjunto de datos** para que funcione con el **Offer decisioning**.

Para ello, vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Entonces verá esto... Haga clic en **Flujo de datos**.

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Busque su **secuencia de datos**, que se llama `--aepUserLdap-- - Demo System Datastream`. Haga clic en **Flujo de datos** para abrirlo.

![SDK web](./images/websdk1.png)

Entonces verá esto... Haga clic en **...** junto a **Adobe Experience Platform** y, a continuación, haga clic en **Editar**.

![SDK web](./images/websdk3.png)

Para habilitar **Offer decisioning**, marque la casilla de **Offer decisioning**. Haga clic en **Guardar**.

![SDK web](./images/websdk5.png)

Su **secuencia de datos** ya está listo para trabajar con **Offer decisioning**.

![SDK web](./images/websdk4.png)

## 3.3.3.2 Configuración de la propiedad de cliente de recopilación de datos de Adobe Experience Platform para solicitar ofertas personalizadas

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), a **Etiquetas**. Busque las propiedades de recopilación de datos, que se denominan `--aepUserLdap-- - Demo System (DD/MM/YYYY)`. Abra la propiedad de cliente de recopilación de datos para la web.

![SDK web](./images/launch1.png)

En su propiedad, vaya a **Reglas** y abra la regla **Vista de página**.

![SDK web](./images/launch2.png)

Haga clic para abrir el evento de experiencia de acción **Enviar &quot;Vista de página&quot;**.

![SDK web](./images/launch3.png)

Entonces verá esto... En **Personalization**, notará la opción de **ámbitos**.

![SDK web](./images/launch4.png)

Por cada solicitud enviada al perímetro de y a Adobe Experience Platform, es posible proporcionar uno o más **ámbitos de decisión**. Un **ámbito de decisión** es una combinación de dos elementos:

- ID de decisión
- ID de ubicación

Primero echemos un vistazo a dónde se pueden encontrar esos dos elementos.

### 3.3.3.2.1 Recuperación del ID de ubicación

El ID de ubicación identifica la ubicación y el tipo de recurso necesario. Por ejemplo, la imagen a pantalla completa de la página de inicio del sitio web de CitiSignal corresponde al ID de colocación Web - Imagen.

>[!NOTE]
>
>Como parte del ejercicio 2.3.5, ya ha configurado una actividad de segmentación de experiencias de Adobe Target que cambiará la imagen de la ubicación a pantalla completa en la página principal, como puede ver en la captura de pantalla. Para este ejercicio, ahora hará que sus ofertas aparezcan en la imagen debajo de la imagen a pantalla completa como se indica en la captura de pantalla.

![SDK web](./images/launch5.png)

Para encontrar el ID de ubicación de la imagen en la web, ve a Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

A continuación, vaya a Componentes y luego a Ubicaciones. Haga clic en la ubicación **Web - Imagen** para ver sus detalles.

![SDK web](./images/launch6.png)

Como puede ver en la imagen anterior, en este ejemplo el ID de ubicación es `dps:offer-placement:1a08a14ccfe533b6`. Escriba el ID de ubicación de la ubicación para Web - Imagen tal como la necesitará en el siguiente ejercicio.

### 3.3.3.2.2 Recuperar el ID de decisión de oferta

El **ID de decisión de oferta** identifica qué combinación de ofertas personalizadas y oferta de reserva desea utilizar. En el ejercicio anterior creó su propia Decisión y le asignó el nombre `--aepUserLdap-- - CitiSignal Decision`.

Para encontrar el ID de decisión de oferta de su `--aepUserLdap-- - CitiSignal Decision`, vaya a Ofertas y luego a Decisiones. Haga clic para seleccionar la decisión, que se denomina `--aepUserLdap-- - CitiSignal Decision`.

![SDK web](./images/launch7.png)

Como puede ver en la imagen anterior, en este ejemplo el identificador de decisión es `dps:offer-activity:1a08ba4b529b2fb2`. Anote el ID de decisión de oferta para la decisión `--aepUserLdap-- - CitiSignal Decision`, ya que lo necesitará en el próximo ejercicio.

Ahora que ha recuperado los dos elementos que necesita para crear un **ámbito de decisión**, puede continuar con el siguiente paso, que implica codificar el ámbito de decisión.

### 3.3.3.2.3 Codificación BASE64

El **ámbito de decisión** que debe especificar es una cadena codificada en BASE64. Esta cadena codificada en BASE64 es una combinación del ID de ubicación y el ID de decisión, como puede ver a continuación:

```json
{
  "xdm:activityId": "dps:offer-activity:1a08ba4b529b2fb2",
  "xdm:placementId": "dps:offer-placement:1a08a14ccfe533b6"
}
```

Puede recuperar la cadena codificada en BASE64 desde Adobe Experience Platform. Vaya a Decisiones y haga clic para abrir la Decisión, que se llama `--aepUserLdap-- - CitiSignal Decision`.

![SDK web](./images/launch9.png)

Después de abrir `--aepUserLdap-- - CitiSignal Decision`, verá esto. Busque la ubicación Web - Imagen y haga clic en el botón **Copiar**. A continuación, haga clic en **Ámbito de decisión codificado**. **Ámbito de decisión** se ha copiado en el portapapeles.

![SDK web](./images/launch10.png)

A continuación, vuelva a Launch, a la acción **AEP Web SDK - Enviar evento**.

![SDK web](./images/launch4.png)

Pegue el ámbito de decisión codificado en el campo de entrada. Guarde los cambios en la acción **AEP Web SDK - Enviar evento** haciendo clic en **[!UICONTROL Conservar cambios]**.

![SDK web](./images/launch11.png)

A continuación, haga clic en **[!UICONTROL Guardar]**.

![SDK web](./images/launch12.png)

En Recopilación de datos de Adobe Experience Platform, vaya a **[!UICONTROL Flujo de publicación]** y abra su **[!UICONTROL Biblioteca de desarrollo]**, que se llama **[!UICONTROL Principal]**. Haga clic en **[!UICONTROL + Agregar todos los recursos modificados]** y luego haga clic en **[!UICONTROL Guardar y generar para desarrollo]**. Los cambios se publicarán en el sitio web de demostración.

![SDK web](./images/launch13.png)

Cada vez que esté cargando una **Página general** ahora, como por ejemplo la página principal del sitio web de demostración, el Offer decisioning evaluará cuál es la oferta aplicable y devolverá una respuesta al sitio web con los detalles de la oferta que se va a mostrar. La visualización de la oferta en el sitio web requiere una configuración adicional, que se explica en el siguiente paso.

## 3.3.3.3 Configuración de la propiedad del cliente de recopilación de datos de Adobe Experience Platform para recibir y aplicar ofertas personalizadas

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), para **[!UICONTROL Propiedades]**. Busque las propiedades de recopilación de datos, que se denominan `--aepUserLdap-- - Demo System (DD/MM/YYYY)`. Abra la propiedad de recopilación de datos para la web.

![SDK web](./images/launch1.png)

En su propiedad, vaya a **Reglas**. Busque y abra la regla **Mostrar oferta (Offer decisioning)**.

![SDK web](./images/decrec2.png)

Entonces verá esto... Abra la acción **Mostrar la oferta en la página**.

![SDK web](./images/decrec6a.png)

Haga clic en **[!UICONTROL Abrir editor]**

![SDK web](./images/decrec6.png)

Sobrescriba el código pegando el siguiente código en el editor.

```javascript
if (!Array.isArray(event.decisions)) {
  console.log("No personalization decisions");
  return;
}

console.log("Received response from Offer Decisioning", event.decisions);

event.decisions.forEach(function (payload) {
  payload.items.forEach(function (item) {
    console.log("Offer", item.data.deliveryURL);

    if (!item.data || item.data?.deliveryURL==null) {
      return;
    }
    console.log("item.data.deliveryURL", item.data.deliveryURL)
    //document.querySelector(".TopRibbon").innerHTML = item.data.content;
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2)").innerHTML = "<img style='max-width:100%;' src='"+item.data.deliveryURL+"'/>";
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2) > img").style.backgroundRepeat="no-repeat";
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2) > img").style.backgroundPosition="center center";
    document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div:nth-child(2) > img").style.backgroundSize = "contain";
  });
});
```

Las líneas 17 aplicarán la imagen que devuelve el Offer decisioning al sitio web. Haga clic en **[!UICONTROL Guardar]**.

![SDK web](./images/decrec7.png)

Haga clic en **[!UICONTROL Conservar cambios]**.

![SDK web](./images/keepchanges1dd.png)

A continuación, haga clic en **[!UICONTROL Guardar]**.

![SDK web](./images/decrec8.png)

En Recopilación de datos de Adobe Experience Platform, vaya a **[!UICONTROL Flujo de publicación]** y abra su **[!UICONTROL Biblioteca de desarrollo]**, que se llama **[!UICONTROL Principal]**. Haga clic en **[!UICONTROL + Agregar todos los recursos modificados]** y luego haga clic en **[!UICONTROL Guardar y generar para desarrollo]**. Los cambios se publicarán en el sitio web de demostración.

![SDK web](./images/decrec9.png)

Con este cambio, esta regla de la recopilación de datos de Adobe Experience Platform ahora escucha la respuesta del Offer decisioning que forma parte de la respuesta de Web SDK y, cuando se recibe la respuesta, la imagen de la oferta se muestra en la página principal.

Al ver el sitio web de demostración, verá que esta imagen se reemplazará ahora. En lugar de las imágenes predeterminadas del sitio web de CitiSignal, ahora verá una oferta como esta. En este caso, se muestra la oferta de reserva.

![SDK web](./images/decrec10.png)

Ahora ha configurado dos tipos de personalización:

- 1 Actividad de segmentación de experiencias con Adobe Target en el ejercicio 2.3.5
- 1 Implementación del Offer decisioning con la propiedad de recopilación de datos

En el siguiente ejercicio verá cómo puede combinar sus ofertas y decisiones creadas en Adobe Journey Optimizer con una actividad de segmentación de experiencias de Adobe Target.

Siguiente paso: [3.3.4 Combinar Adobe Target y el Offer decisioning](./ex4.md)

[Volver al módulo 3.3](./offer-decisioning.md)

[Volver a todos los módulos](./../../../overview.md)
