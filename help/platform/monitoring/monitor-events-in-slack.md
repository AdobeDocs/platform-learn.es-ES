---
title: Monitorización de eventos en Slack
description: Obtenga información sobre cómo recibir notificaciones de Experience Platform en Slack mediante la integración con un proxy de gancho web de Adobe App Builder.
feature: Monitoring
role: Developer, Admin
level: Intermediate
duration: 519
last-substantial-update: 2026-02-24T00:00:00Z
jira: KT-20339
exl-id: 6d4a072c-9eef-4a38-9459-9e1cbd66bfb5
source-git-commit: 4ec7a800ef963f9b1257e2f246428abff32e9b94
workflow-type: tm+mt
source-wordcount: '1539'
ht-degree: 0%

---

# Monitorización de eventos de Experience Platform en Slack

Obtenga información sobre cómo recibir notificaciones de Experience Platform en Slack mediante la integración con un proxy de gancho web de Adobe App Builder. Es posible que los ingenieros y administradores de datos deseen recibir notificaciones proactivas en Slack desde Adobe Experience Platform para monitorizar el estado de sus implementaciones de Platform. Este tutorial describe la arquitectura y los pasos de implementación para conectar Adobe I/O Events a Slack mediante Adobe App Builder.


>[!VIDEO](https://video.tv.adobe.com/v/3480183?learn=on)

## ¿Por qué un proxy webhook?

La conexión directa de Adobe I/O Events a un webhook entrante de Slack no es posible debido a una discrepancia de protocolos en el proceso de verificación.

* **El desafío**: Al registrar un webhook con Adobe I/O Events, Adobe enviará una solicitud de &quot;desafío&quot; (ya sea un `GET` o un `POST`) a su extremo. El punto de conexión debe procesar correctamente este desafío y devolver el valor específico para confirmar la propiedad.

* **La limitación**: Los webhooks entrantes de Slack están diseñados únicamente para introducir cargas JSON para la mensajería. No tienen lógica para reconocer o responder al protocolo de enlace del desafío de verificación de Adobe.

* **La solución**: implemente un proxy de gancho web intermedio mediante Adobe App Builder. Este proxy se encuentra entre Adobe y Slack para lo siguiente:
   1. Interceptar la solicitud de Adobe y responder al desafío de verificación.
   1. Formatee la carga útil en un mensaje compatible con Slack y reenvíelo a Slack.

* **Método de envío**: acciones de tiempo de ejecución.  Las acciones de tiempo de ejecución se incluyen en Adobe App Builder. Cuando se utiliza una acción en tiempo de ejecución (acción no web) como controlador de eventos, Adobe I/O Events administra automáticamente la verificación de firmas y las respuestas de desafío. Las acciones en tiempo de ejecución son el enfoque recomendado, ya que requieren menos código y proporcionan seguridad integrada.

## Descripción general de arquitectura

### ¿Qué es Adobe Developer Console?

Adobe Developer Console es el portal central para administrar sus proyectos, API y credenciales de Adobe. Es donde crea el proyecto, configura la autenticación y registra los webhooks.

### ¿Qué es App Builder?

Adobe App Builder es un marco de trabajo completo que permite a los desarrolladores empresariales crear aplicaciones nativas de la nube.

* **Aprovisionamiento**: App Builder no está habilitado de forma predeterminada; debe aprovisionarse para su organización como característica. Asegúrese de que su organización tenga el derecho de **[!DNL App Builder]**.

* **Plantilla de proyecto**: los proyectos de App Builder se crean específicamente con la plantilla **[!UICONTROL App Builder]** en [!DNL Developer Console] ([!UICONTROL Proyecto a partir de la plantilla] > [!UICONTROL App Builder]). La plantilla configura automáticamente los espacios de trabajo y los entornos de tiempo de ejecución necesarios.

* **Guía de introducción de App Builder**: consulte la documentación [para aprovisionar y crear su primer proyecto a partir de la plantilla](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app){target=_blank}.

### ¿Qué es Adobe I/O Runtime?

Adobe I/O Runtime es la plataforma sin servidor que alimenta App Builder. Permite a los desarrolladores implementar código (Funciones como servicio) que se ejecuta en respuesta a solicitudes HTTP sin administrar la infraestructura del servidor.

En esta implementación, utilizamos una **Acción**. Una acción es una función sin estado (escrita en Node.js) que se ejecuta en Adobe I/O Runtime. Nuestra acción sirve como punto final HTTP público con el que Adobe I/O Events habla.

Para obtener más información, consulte la [documentación de Adobe I/O Runtime](https://developer.adobe.com/runtime/){target=_blank}.

## Guía de implementación

### Requisitos previos

Antes de empezar, asegúrese de que dispone de lo siguiente:

* **Acceso a Adobe Developer Console**: debe tener acceso a un administrador del sistema o a [rol de desarrollador](../admin/add-developers.md) dentro de una organización que tenga App Builder habilitado.

  >[!TIP]
  > Para comprobar el aprovisionamiento de App Builder, inicie sesión en [Adobe Developer Console](https://developer.adobe.com/console/){target=_blank}, asegúrese de que se encuentra en la organización deseada, seleccione **[!UICONTROL Crear proyecto a partir de la plantilla]** y compruebe que la plantilla de App Builder está disponible. Si no es así, consulte la sección de preguntas frecuentes sobre App Builder &quot;[Cómo obtener App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/faq#how-to-get-app-builder){target=_blank}&quot;


* **Node.js y npm**: Este proyecto requiere Node.js, que incluye NPM (Administrador de paquetes de nodos). NPM se utiliza para instalar la CLI de Adobe y administrar las dependencias del proyecto.

   * [Descargar Node.js (versión LTS recomendada)](https://nodejs.org/){target=_blank}
   * [npm Guía de introducción](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm){target=_blank}: Una guía sobre cómo comprobar la instalación.

* **`aio CLI`**: instalado a través de su terminal: `npm install -g @adobe/aio-cli`
* **Configuración de la aplicación Slack**: necesita configurar una aplicación Slack en su área de trabajo con un **webhook entrante** activado.

   * [Crear una aplicación de Slack](https://api.slack.com/apps){target=_blank}
   * [Guía de webhooks entrantes de Slack](https://docs.slack.dev/messaging/sending-messages-using-incoming-webhooks/){target=_blank}: siga esta guía para crear su aplicación y generar la URL del webhook (comienza con `https://hooks.slack.com/`...).

### Paso 1: Crear un proyecto en Adobe Developer Console

En primer lugar, cree un proyecto con la plantilla App Builder en Adobe Developer Console:

1. Iniciar sesión en [Adobe Developer Console](https://developer.adobe.com/console)
1. Seleccione **[!UICONTROL Crear proyecto a partir de la plantilla]**
1. Seleccione la plantilla de App Builder
1. Escriba un Título de proyecto, por ejemplo `Slack webhook integration`
1. Seleccionar **[!UICONTROL Guardar]**

### Inicializar el entorno de tiempo de ejecución

Ejecute los siguientes comandos en el terminal para crear la estructura del proyecto:

#### Iniciar sesión en `aio`

```
aio login
```

#### Paso 2: Inicializar un nuevo proyecto de App Builder

```
aio app init slack-webhook-proxy
```

1. Seleccione su organización y pulse **Intro**
1. Seleccione el proyecto que creó en el paso anterior (por ejemplo, `Slack webhook integration`) y presione **Entrar**
1. Seleccione la opción **[!UICONTROL Solo las plantillas admitidas por mi organización]**
1. Omitir la sección de muestra presionando **Intro**
1. Cuando se le solicite, asegúrese de que los siguientes componentes están seleccionados (el círculo debe rellenarse) y presione **Intro**:
   1. **[!UICONTROL Acciones: Implementar acciones en tiempo de ejecución]**
   1. **[!UICONTROL Eventos: publicar en Adobe I/O Events]**
   1. **[!UICONTROL Web Assets: implementar en recursos estáticos hospedados]**
1. Con las flechas &quot;Arriba&quot; y &quot;Abajo&quot;, navega por la lista entrante, elige **[!UICONTROL Adobe Experience Platform: Perfil del cliente en tiempo real]** y pulsa **Intro**
1. Las acciones **[!UICONTROL genéricas]** se generan automáticamente
1. Elija **[!UICONTROL Pure HTML/JS]** para la interfaz de usuario y presione **Intro**
1. Mantenga **[!UICONTROL generic]** como acción de ejemplo para mostrar cómo acceder a un nombre de API externo y presione **Entrar**
1. Mantenga **[!UICONTROL publish-events]** como nombre de la acción de ejemplo para crear mensajes en formato de eventos de nube y presione **Entrar**

Se debe completar la inicialización de la aplicación.

#### Vaya al directorio del proyecto

```
cd slack-webhook-proxy
```

#### Añadir la acción web

```
aio app add action
```

1. Elija **[!UICONTROL Solo Plantillas Compatibles Con Mi Organización]** y presione **Entrar**
2. Vea la acción **[!UICONTROL publish-events]** en la tabla que se presenta; presione **Space** para seleccionar la acción. Si el círculo al lado del nombre está relleno como se muestra en el tutorial de vídeo, presione **Entrar**
3. Asigne un nombre a la acción `webhook-proxy`

### Paso 3: Actualizar el código de acción de proxy

En un IDE o editor de texto, cree o modifique el archivo `actions/webhook-proxy/index.js` con el siguiente código. Esta implementación reenvía eventos a Slack. La verificación de firma y la gestión de desafíos son automáticas al utilizar el registro de acciones en tiempo de ejecución.

```javascript
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("webhook-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### Paso 4: Configurar la acción

La configuración de la acción en `app.config.yaml` es crítica. Utilice web: no para crear una acción no web que se pueda registrar como Acción de tiempo de ejecución en Developer Console.

```yaml
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

#### Por qué `web: no?`

Cuando se utiliza una acción que no es de web y se registra mediante la opción &quot;Acción de tiempo de ejecución&quot; en Developer Console, Adobe I/O Events hace lo siguiente automáticamente:

* Controla la verificación por desafío (tanto `GET` como `POST`)
* Comprueba las firmas digitales antes de invocar la acción
* Encadena una acción de validador de firmas delante de la acción

Esto significa que el código solo necesita gestionar la lógica empresarial (reenvío a Slack).

### Paso 4: Actualizar las variables de entorno

Para administrar credenciales de forma segura, utilizamos variables de entorno. Cree o modifique el archivo `.env` en la raíz del proyecto para agregar la URL del webhook de Slack. Asegúrese de mostrar los archivos ocultos en el sistema si no ve el archivo `.env`:

```
# ... other .env file content ...
 
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Paso 5: Implementar la acción

Una vez configuradas las variables de entorno, implemente la acción. Asegúrese de estar en la raíz del proyecto, concretamente `slack-webhook-proxy`, al ejecutar este comando en el terminal.

```
aio app deploy
```

La acción se implementará en Adobe I/O Runtime y estará disponible en Developer Console para registrarse.

### Paso 6: Registrar la acción en Adobe Developer Console

Ahora que la acción está implementada, regístrela como destino para los eventos de Adobe.

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console){target=_blank} y abra su proyecto de App Builder.
1. Elige tu **[!UICONTROL Workspace]**
1. Seleccione **[!UICONTROL Agregar servicio]** y seleccione **[!UICONTROL Evento]**.
1. Seleccione **[!UICONTROL Adobe Experience Platform]** como producto.
1. Seleccione **[!UICONTROL Notificaciones de plataforma]** como tipo de eventos.
1. Seleccione los eventos específicos (o todos) de los que desea recibir una notificación en Slack y seleccione **[!UICONTROL Siguiente]**.
1. Seleccione o [cree su credencial de OAuth](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/api/platform-api-authentication){target=_blank}.
1. Configurar **[!UICONTROL detalles de registro de eventos]**:
   1. **[!UICONTROL Nombre de registro]**: asigne un nombre descriptivo al registro.
   1. **[!UICONTROL Descripción del registro]**: asegúrese de que esto sea explícito para que otros colaboradores puedan saber lo que hace.
   1. Seleccionar **[!UICONTROL Siguiente]**
   1. **[!UICONTROL Método de envío]**: seleccione **[!UICONTROL Acción en tiempo de ejecución]** (no &quot;webhook&quot;).
   1. **[!UICONTROL Acción en tiempo de ejecución]**: elija `webhook-proxy` en el menú desplegable (actualice la página si no la ve).
1. Seleccione **[!UICONTROL Guardar eventos configurados]**.


### Paso 7: Validar con un evento de ejemplo

Puede probar todo el flujo de extremo a extremo haciendo clic en el icono &quot;Enviar evento de muestra&quot; junto a cualquier evento configurado.

El evento de muestra se envía en el canal que ha configurado al crear la aplicación de Slack y el webhook; debería ver algo similar a esto:

![Ejemplo de un evento de supervisión en Slack](../assets/slack-monitor.png)

¡Felicidades, ha integrado correctamente Slack con los eventos de Experience Platform!

### Problemas comunes

Estos son algunos problemas que puede encontrar al configurar el proxy y algunas formas potenciales de solucionarlos.

* **No se pueden ver las organizaciones de IMS**: Si no ve su lista de organizaciones IMS al ejecutar `aio app init`, intente lo siguiente. Ejecute `aio logout` en el terminal, cierre la sesión de Experience Cloud en el explorador web predeterminado y vuelva a ejecutar `aio login`.
* **La acción no aparece en el menú desplegable**: Asegúrate de que `web: no` esté establecido en `app.config.yaml`. En el menú desplegable Acción de tiempo de ejecución solo aparecen las acciones que no son web. Actualice la página de Developer Console después de implementar.
* **Error en la verificación de firma**: si ve esto en los registros de activación, significa que el validador integrado de Adobe rechazó la solicitud. Esto no debería suceder para eventos Adobe legítimos. Compruebe que el registro de eventos esté configurado correctamente.
* **Slack no recibe mensajes**: Compruebe que `SLACK_WEBHOOK_URL` esté configurado correctamente en el archivo `.env` y que la aplicación de Slack tenga habilitado el webhook entrante.
* **Tiempo de espera de acción**: Las acciones de tiempo de ejecución tienen un tiempo de espera de 60 segundos. Si la acción tarda más, considere la posibilidad de utilizar el método del diario en su lugar.
