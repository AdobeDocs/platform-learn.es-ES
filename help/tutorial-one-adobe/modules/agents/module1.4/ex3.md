---
title: Implementación de Brand Concierge mediante etiquetas de recopilación de datos
description: Implementación de Brand Concierge mediante etiquetas de recopilación de datos
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# 1.4.3 Implementar Brand Concierge mediante etiquetas de recopilación de datos

>[!IMPORTANT]
>
>Este ejercicio se está trabajando en él y aún no ha finalizado.

## Propiedad de etiquetas de recopilación de datos

Brand Concierge necesita enviar datos a Adobe Experience Platform. Para ello, es necesario implementar Web SDK (o alloy.js) en el sitio web.

Para que sea posible, ahora debe crear una propiedad Etiquetas de recopilación de datos.

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Recopilación de datos**.

![Brand Concierge](./images/aep101.png)

Haga clic en **Nueva propiedad**.

![Brand Concierge](./images/aep102.png)

Escriba el nombre: `--aepUserLdap-- - CitiSignal Website + Brand Concierge` y también el dominio del sitio web.

Haga clic en **Guardar**.

![Brand Concierge](./images/aep103.png)

Busque su propiedad y, a continuación, ábrala.

![Brand Concierge](./images/aep104.png)

Vaya a **Extensiones** y luego a **Catálogo**.

![Brand Concierge](./images/aep105.png)

Busque `web sdk` y, a continuación, haga clic en la extensión **Adobe Experience Platform Web SDK**. Haga clic en **Instalar**.

![Brand Concierge](./images/aep106.png)

Entonces debería ver esto. Aquí solo debe proporcionar los detalles de su conjunto de datos. Para ello, desplácese un poco hacia abajo.

![Brand Concierge](./images/aep107.png)

Para los 3 entornos **Production**, **Staging** y **Development**, seleccione lo siguiente:

- **Espacio aislado**: `--aepUserLdap-- - bc`
- **Flujo de datos**: `--aepUserLdap-- - Brand Concierge`

Haga clic en **Guardar**.

![Brand Concierge](./images/aep108.png)

Entonces debería ver esto. Ir a **Reglas**.

![Brand Concierge](./images/aep108a.png)

Haga clic en **Crear nueva regla**.

![Brand Concierge](./images/aep109.png)

Escriba el nombre: `Homepage`. A continuación, haga clic en **+ Agregar** en **EVENTOS**.

![Brand Concierge](./images/aep110.png)

Seleccione las siguientes opciones:

- **Extensión**: **Principal**
- **Tipo de evento**: **Biblioteca cargada (Principio de página)**

Haga clic en **Conservar cambios**.

![Brand Concierge](./images/aep111.png)

Entonces debería ver esto. Haga clic en **+ Agregar** en **CONDICIONES**.

![Brand Concierge](./images/aep112.png)

Seleccione las siguientes opciones:

- **Tipo de lógica**: **Normal**
- **Extensión**: **Principal**
- **Tipo De Condición**: **Ruta Sin Cadena De Consulta**
- **ruta igual a...**: introduzca el dominio del sitio web, en este caso `https://vangeluw.adobedemosystem.com/`

Haga clic en **Conservar cambios**.

![Brand Concierge](./images/aep113.png)

Entonces debería ver esto. Haga clic en **+ Agregar** en **ACCIONES**.

![Brand Concierge](./images/aep114.png)

Seleccione las siguientes opciones:

- **Extensión**: **Principal**
- **Tipo de acción**: **Código personalizado**
- **Idioma**: **JavaScript**

Haga clic en **Abrir editor**.

![Brand Concierge](./images/aep115.png)

Pegue el siguiente código:

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

Haga clic en **Guardar**.

![Brand Concierge](./images/aep116.png)

Entonces debería ver esto. Haga clic en **Conservar cambios**.

![Brand Concierge](./images/aep117.png)

Entonces debería ver esto. Haga clic en **Guardar**.

![Brand Concierge](./images/aep118.png)

Vaya a **Flujo de publicación**. Haga clic en **Agregar biblioteca**.

![Brand Concierge](./images/aep119.png)

Escriba el nombre: `Dev`, seleccione **Desarrollo (desarrollo)** para el entorno y haga clic en **Agregar todos los recursos modificados**.

Haga clic en **Guardar y crear para desarrollo**.

![Brand Concierge](./images/aep120.png)

Después de un par de minutos, se creará su biblioteca. Espera a ver el **punto verde** al lado de **Dev**. A continuación, vaya a **Entornos**.

![Brand Concierge](./images/aep121.png)

Haga clic en el icono **Instalar** para el entorno **Desarrollo**.

![Brand Concierge](./images/aep122.png)

Entonces debería ver esto. Haga clic en el botón **copiar** para copiar la ruta de la biblioteca. Deberá implementar esto en su sitio web.

La ruta de la biblioteca debe ser similar a la siguiente:
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

Volver a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}