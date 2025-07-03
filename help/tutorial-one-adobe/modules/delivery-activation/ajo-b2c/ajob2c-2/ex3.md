---
title: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definir acciones personalizadas'
description: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definir acciones personalizadas'
kt: 5342
doc-type: tutorial
exl-id: 92752e84-3bbe-4d11-b187-bd9fdbbee709
source-git-commit: e3d3b8e3abdea1766594eca53255df024129cb2c
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---

# 3.2.3 Definir una acción personalizada

En este ejercicio, creará una acción personalizada para enviar un mensaje a un canal de Slack.

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Ahora utilizará un canal de Slack existente y enviará mensajes a ese canal de Slack. Slack tiene una API fácil de usar y usted utilizará Adobe Journey Optimizer para almacenar en déclencheur su API.

![Demostración](./images/slack.png)

En el menú de la izquierda, desplácese hacia abajo y haga clic en **Configuraciones**. A continuación, haga clic en el botón **Administrar** en **Acciones**.

![Demostración](./images/menuactions.png)

Luego verá la lista **Acciones**. Haga clic en **Crear acción**.

![Demostración](./images/acthome.png)

Verá una ventana emergente de acción vacía.

![Demostración](./images/emptyact.png)

Como nombre de la acción, use `--aepUserLdap--TextSlack`.

Definir descripción en: `Send Message to Slack`.

Para la **configuración de URL**, use esto:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Método: **POST**

>[!NOTE]
>
>La URL anterior hace referencia a una función Lambda de AWS que reenviará la solicitud al canal de Slack como se ha mencionado anteriormente. Esto se hace para proteger el acceso a un canal de Slack propiedad de Adobe. Si tiene su propio canal de Slack, debe crear una aplicación de Slack a través de [https://api.slack.com/](https://api.slack.com/), luego debe crear un webhook entrante en esa aplicación de Slack y, a continuación, reemplazar la dirección URL anterior por la dirección URL del webhook entrante.

![Demostración](./images/slackname.png)

**Autenticación** debe establecerse en **Sin autenticación**.

![Demostración](./images/slackauth.png)

En **Cargas útiles**, debe definir qué campos se deben enviar a Slack. Lógicamente, desea que Adobe Journey Optimizer y Adobe Experience Platform sean el cerebro de la personalización, por lo que el texto que se enviará a Slack debe definirlo Adobe Journey Optimizer y luego enviarlo a Slack para su ejecución.

Para la **solicitud**, haga clic en el icono **Editar carga útil**.

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

Entonces verá esto... Haga clic en **Guardar**.

![Demostración](./images/slackmsgpopup1.png)

Desplácese hacia arriba y haga clic en **Guardar** una vez más para guardar la acción.

![Demostración](./images/slackmsgpopup3.png)

La acción personalizada ahora forma parte de la lista **Acciones**.

![Demostración](./images/slackdone.png)

Ha definido eventos y fuentes de datos y acciones externas. A continuación, combinará todo eso en un recorrido.

## Pasos siguientes

Ir a [3.2.4 Crear el recorrido y los mensajes](./ex4.md){target="_blank"}

Volver a [Adobe Journey Optimizer: fuentes de datos externas y acciones personalizadas](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
