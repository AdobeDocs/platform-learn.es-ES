---
title: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definir acciones personalizadas'
description: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definir acciones personalizadas'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 3%

---

# 3.2.3 Definir una acción personalizada

En este ejercicio, creará dos acciones personalizadas utilizando Adobe Journey Optimizer en combinación.

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Para cambiar de una zona protegida a otra, haga clic en **PRODUCTION Prod (VA7)** y seleccione la zona protegida en la lista. En este ejemplo, la zona protegida se denomina **Habilitación de AEP para el año fiscal 22**. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

En el menú de la izquierda, desplácese hacia abajo y haga clic en **Configuraciones**. A continuación, haga clic en el botón **Administrar** en **Acciones**.

![Demostración](./images/menuactions.png)

Luego verá la lista **Acciones**.

![Demostración](./images/acthome.png)

Definirá una acción que enviará un texto a un canal de Slack.

## 3.2.3.1 Acción: enviar texto al canal del Slack

Ahora utilizará un canal de Slack existente y enviará mensajes a ese canal de Slack. Slack tiene una API fácil de usar y utilizaremos Adobe Journey Optimizer para almacenar en déclencheur su API.

![Demostración](./images/slack.png)

Haga clic en **Crear acción** para empezar a agregar una acción nueva.

![Demostración](./images/adda.png)

Verá una ventana emergente de acción vacía.

![Demostración](./images/emptyact.png)

Como nombre de la acción, use `--aepUserLdap--TextSlack`. En este ejemplo, el nombre de la acción es `vangeluwTextSlack`.

Definir descripción en: `Send Text to Slack`.

![Demostración](./images/slackname.png)

Para la **configuración de URL**, use esto:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Método: **POST**

>[!NOTE]
>
>La URL anterior hace referencia a una función Lambda de AWS que reenvía la solicitud al canal del Slack como se ha mencionado anteriormente. Esto se hace para proteger el acceso a un canal de Slack propiedad del Adobe. Si tiene su propio canal de Slack, debe crear una aplicación de Slack a través de [https://api.slack.com/](https://api.slack.com/), luego debe crear un webhook entrante en esa aplicación de Slack y luego reemplazar la dirección URL anterior por la dirección URL del webhook entrante.

No es necesario cambiar los campos de encabezado.

![Demostración](./images/slackurl.png)

**Autenticación** debe establecerse en **Sin autenticación**.

![Demostración](./images/slackauth.png)

Para los **parámetros de acción**, debe definir qué campos deben enviarse al Slack. Lógicamente, queremos que Adobe Journey Optimizer y Adobe Experience Platform sean el cerebro de la personalización, por lo que el texto que se enviará al Slack debe definirlo Adobe Journey Optimizer y luego enviarlo al Slack para que lo ejecute.

Por lo tanto, para los **parámetros de acción**, haga clic en el icono **Editar carga útil**.

![Demostración](./images/slackmsgp.png)

A continuación, verá una ventana emergente vacía.

![Demostración](./images/slackmsgpopup.png)

Copie el texto siguiente y péguelo en la ventana emergente vacía.

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

Información: al especificar los campos siguientes, se podrá acceder a estos campos desde el Recorrido del cliente y se podrán rellenar de forma dinámica desde el Recorrido:

**&quot;toBeMapped&quot;: true,**

**&quot;dataType&quot;: &quot;string&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

A continuación, verá esto:

![Demostración](./images/slackmsgpopup1.png)

Haga clic en **Guardar**.

![Demostración](./images/twiliomsgpopup2.png)

Desplácese hacia arriba y haga clic en **Guardar** una vez más para guardar la acción personalizada.

![Demostración](./images/slackmsgpopup3.png)

La acción personalizada ahora forma parte de la lista **Acciones**.

![Demostración](./images/slackdone.png)

Ha definido eventos y fuentes de datos y acciones externas. Ahora vamos a consolidar todo eso en un recorrido.

Paso siguiente: [3.2.4 Crear el recorrido y los mensajes](./ex4.md)

[Volver al módulo 8](journey-orchestration-external-weather-api-sms.md)

[Volver a todos los módulos](../../../overview.md)
