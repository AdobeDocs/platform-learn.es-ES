---
title: 'Adobe Journey Optimizer: API de meteorología externa, acción de SMS y más: Definir acciones personalizadas'
description: 'Adobe Journey Optimizer: API de meteorología externa, acción de SMS y más: Definir acciones personalizadas'
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7ee5aee9-3740-4eee-9f53-a44fdb564a00
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 8.3 Definir una acción personalizada

En este ejercicio, creará dos acciones personalizadas utilizando Adobe Journey Optimizer en combinación.

Inicie sesión en Adobe Journey Optimizer desde [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Se le redirigirá al **Página principal**  en Journey Optimizer. En primer lugar, asegúrese de que está utilizando el simulador para pruebas correcto. El entorno limitado que se va a usar se denomina `--aepSandboxId--`. Para cambiar de un simulador de pruebas a otro, haga clic en **PRODUCCIÓN (VA7)** y seleccione el simulador de pruebas de la lista. En este ejemplo, el simulador de pruebas recibe el nombre **Habilitación de AEP para el año fiscal 22**. Entonces estará en el **Página principal** vista del entorno limitado `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

En el menú de la izquierda, desplácese hacia abajo y haga clic en **Configuraciones**. A continuación, haga clic en el **Administrar** botón debajo de **Acciones**.

![Demostración](./images/menuactions.png)

Verá el **Acciones** lista.

![Demostración](./images/acthome.png)

Defina una acción que envíe un texto a un canal de Slack.

## 8.3.1 Acción: Enviar texto al canal del Slack

Ahora utilizará un canal de Slack existente y enviará mensajes a ese canal de Slack. Slack tiene una API fácil de usar y utilizaremos Adobe Journey Optimizer para almacenar en déclencheur su API.

![Demostración](./images/slack.png)

Haga clic en **Crear acción** para empezar a agregar una nueva acción.

![Demostración](./images/adda.png)

Verá una ventana emergente de acción vacía.

![Demostración](./images/emptyact.png)

Como nombre de la acción, utilice `--demoProfileLdap--TextSlack`. En este ejemplo, el Nombre de la acción es `vangeluwTextSlack`.

Establecer descripción como: `Send Text to Slack`.

![Demostración](./images/slackname.png)

Para la variable **Configuración de URL**, utilice esto:

- Dirección URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Método: **POST**

>[!NOTE]
>
>La URL anterior hace referencia a una función de AWS Lambda que reenviará la solicitud al canal del Slack como se mencionó anteriormente. Esto se hace para proteger el acceso a un canal de Slack propiedad del Adobe. Si tiene su propio canal de Slack, debe crear una aplicación Slack a través de [https://api.slack.com/](https://api.slack.com/), debe crear un vínculo web entrante en esa aplicación Slack y, a continuación, reemplazar la URL anterior por la URL de vínculo web entrante.

No es necesario cambiar los campos del encabezado.

![Demostración](./images/slackurl.png)

**Autenticación** debe configurarse como **Sin autenticación**.

![Demostración](./images/slackauth.png)

Para la variable **Parámetros de acción**, debe definir qué campos se deben enviar al Slack. Lógicamente, queremos que Adobe Journey Optimizer y Adobe Experience Platform sean el cerebro de la personalización, por lo que el texto que se envía al Slack debe definirse por Adobe Journey Optimizer y luego enviarse al Slack para su ejecución.

Así que para la **Parámetros de acción**, haga clic en **Editar carga útil** icono.

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

I.F.: al especificar los campos siguientes, se podrá acceder a estos campos desde el Recorrido del cliente y se podrán rellenar dinámicamente desde el Recorrido:

**&quot;toBeMapped&quot;: true,**

**&quot;dataType&quot;: &quot;string&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

Verá esto:

![Demostración](./images/slackmsgpopup1.png)

Haga clic en **Guardar**.

![Demostración](./images/twiliomsgpopup2.png)

Desplácese hacia arriba y haga clic en **Guardar** una vez más para guardar la acción personalizada.

![Demostración](./images/slackmsgpopup3.png)

La acción personalizada ahora forma parte del **Acciones** lista.

![Demostración](./images/slackdone.png)

Ha definido eventos, fuentes de datos externas y acciones. Ahora consolidemos todo eso en un recorrido.

Paso siguiente: [8.4 Crear su recorrido y mensajes](./ex4.md)

[Volver al módulo 8](journey-orchestration-external-weather-api-sms.md)

[Volver a todos los módulos](../../overview.md)
