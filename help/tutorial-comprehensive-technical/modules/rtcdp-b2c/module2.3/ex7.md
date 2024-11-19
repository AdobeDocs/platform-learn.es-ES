---
title: 'Real-time CDP: SDK de destinos'
description: 'Real-time CDP: SDK de destinos'
kt: 5342
doc-type: tutorial
exl-id: 5606ca2f-85ce-41b3-80f9-3c137f66a8c0
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 6%

---

# 2.3.7 SDK de destinos

## Configuración del proyecto de Adobe I/O

En este ejercicio volverá a utilizar Adobe I/O para consultar las API de Adobe Experience Platform. Si aún no ha configurado el proyecto de Adobe I/O, vuelva al [Ejercicio 3 en el Módulo 2.1](../module2.1/ex3.md) y siga las instrucciones que se indican a continuación.

## Autenticación de Postman en el Adobe I/O

En este ejercicio volverá a utilizar Postman para consultar las API de Adobe Experience Platform. Si aún no configuró la aplicación de Postman, vuelva al [Ejercicio 3 del módulo 2.1](../module2.1/ex3.md) y siga las instrucciones que se indican a continuación.

## Definir punto final y formato

Para este ejercicio, necesitará un punto final que configurar para que cuando un segmento se califique, el evento de calificación se pueda transmitir a ese punto final. En este ejercicio, usará un extremo de ejemplo con [https://webhook.site/](https://webhook.site/). Vaya a [https://webhook.site/](https://webhook.site/), donde verá algo similar a esto. Haga clic en **Copiar al portapapeles** para copiar la dirección URL. Deberá especificar esta dirección URL en el siguiente ejercicio. La dirección URL de este ejemplo es `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`.

![Ingesta de datos](./images/webhook1.png)

En cuanto al formato, utilizaremos una plantilla estándar que transmitirá las clasificaciones o desclasificaciones de segmentos junto con metadatos como identificadores de cliente. Las plantillas se pueden personalizar para satisfacer las expectativas de puntos finales específicos, pero en este ejercicio reutilizaremos una plantilla estándar, lo que dará como resultado una carga útil como esta que se transmitirá al punto final.

```json
{
  "profiles": [
    {
      "identities": [
        {
          "type": "ecid",
          "id": "64626768309422151580190219823409897678"
        }
      ],
      "AdobeExperiencePlatformSegments": {
        "add": [
          "f58c723c-f1e5-40dd-8c79-7bb4ab47f041"
        ],
        "remove": []
      }
    }
  ]
}
```

## Creación de una configuración de servidor y plantilla

El primer paso para crear su propio destino en Adobe Experience Platform es crear una configuración de servidor y plantilla.

Para ello, vaya a la **API de creación de destinos**, a **plantillas y servidores de destino** y haga clic para abrir el POST de solicitud **Crear una configuración de servidor de destino**. Entonces verá esto... En **Encabezados**, debe actualizar manualmente el valor de la clave **x-sandbox-name** y establecerlo en `--aepSandboxName--`. Seleccione el valor **{{SANDBOX_NAME}}**.

![Ingesta de datos](./images/sdkpm1.png)

Reemplazar por `--aepSandboxName--`.

![Ingesta de datos](./images/sdkpm2.png)

A continuación, vaya a **Cuerpo**. seleccione el marcador de posición **{{body}}**.

![Ingesta de datos](./images/sdkpm3.png)

Ahora necesita reemplazar el marcador de posición **{{body}}** por el siguiente código:

```json
{
    "name": "Custom HTTP Destination",
    "destinationServerType": "URL_BASED",
    "urlBasedDestination": {
        "url": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "yourURL"
        }
    },
    "httpTemplate": {
        "httpMethod": "POST",
        "requestBody": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{\n    \"profiles\": [\n    {%- for profile in input.profiles %}\n        {\n            \"identities\": [\n            {%- for idMapEntry in profile.identityMap -%}\n            {%- set namespace = idMapEntry.key -%}\n                {%- for identity in idMapEntry.value %}\n                {\n                    \"type\": \"{{ namespace }}\",\n                    \"id\": \"{{ identity.id }}\"\n                }{%- if not loop.last -%},{%- endif -%}\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\n            {% endfor %}\n            ],\n            \"AdobeExperiencePlatformSegments\": {\n                \"add\": [\n                {%- for segment in profile.segmentMembership.ups | added %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ],\n                \"remove\": [\n                {#- Alternative syntax for filtering segments by status: -#}\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ]\n            }\n        }{%- if not loop.last -%},{%- endif -%}\n    {% endfor %}\n    ]\n}"
        },
        "contentType": "application/json"
    }
}
```

Después de pegar el código anterior, debe actualizar manualmente el campo **urlBasedDestination.url.value** y establecerlo en la dirección URL del webhook que creó en el paso anterior, que era `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a` en este ejemplo.

![Ingesta de datos](./images/sdkpm4.png)

Después de actualizar el campo **urlBasedDestination.url.value**, debería tener este aspecto. Haga clic en **Enviar**.

![Ingesta de datos](./images/sdkpm5.png)

Después de hacer clic en **Enviar**, se creará la plantilla de servidor y, como parte de la respuesta, verá un campo denominado **instanceId**. Escríbelo, ya que lo necesitará en el siguiente paso. En este ejemplo, **instanceId** es
`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`.

![Ingesta de datos](./images/sdkpm6.png)

## Cree la configuración de destino

En Postman, en **API de creación de destino**, vaya a **Configuraciones de destino** y haga clic para abrir el POST de solicitud **Crear una configuración de destino**. Entonces verá esto... En **Encabezados**, debe actualizar manualmente el valor de la clave **x-sandbox-name** y establecerlo en `--aepSandboxName--`. Seleccione el valor **{{SANDBOX_NAME}}**.

![Ingesta de datos](./images/sdkpm7.png)

Reemplazar por `--aepSandboxName--`.

![Ingesta de datos](./images/sdkpm8.png)

A continuación, vaya a **Cuerpo**. seleccione el marcador de posición **{{body}}**.

![Ingesta de datos](./images/sdkpm9.png)

Ahora necesita reemplazar el marcador de posición **{{body}}** por el siguiente código:

```json
{
    "name": "--aepUserLdap-- - Webhook",
    "description": "Exports segment qualifications and identities to a custom webhook via Destination SDK.",
    "status": "TEST",
    "customerAuthenticationConfigurations": [
        {
            "authType": "BEARER"
        }
    ],
    "customerDataFields": [
        {
            "name": "endpointsInstance",
            "type": "string",
            "title": "Select Endpoint",
            "description": "We could manage several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
            "isRequired": true,
            "enum": [
                "US",
                "EU",
                "APAC",
                "NZ"
            ]
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en",
        "category": "streaming",
        "connectionType": "Server-to-server",
        "frequency": "Streaming"
    },
    "identityNamespaces": {
        "ecid": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": false
        }
    },
    "segmentMappingConfig": {
        "mapExperiencePlatformSegmentName": true,
        "mapExperiencePlatformSegmentId": true,
        "mapUserInput": false
    },
    "aggregation": {
        "aggregationType": "BEST_EFFORT",
        "bestEffortAggregation": {
            "maxUsersPerRequest": "1000",
            "splitUserById": false
        }
    },
    "schemaConfig": {
        "profileRequired": false,
        "segmentRequired": true,
        "identityRequired": true
    },
    "destinationDelivery": [
        {
            "authenticationRule": "NONE",
            "destinationServerId": "yourTemplateInstanceID"
        }
    ]
}
```

![Ingesta de datos](./images/sdkpm11.png)

Después de pegar el código anterior, debe actualizar manualmente el campo **destinationDelivery. destinationServerId** y debe establecerlo en **instanceId** de la plantilla de servidor de destino que creó en el paso anterior, que era `eb0f436f-dcf5-4993-a82d-0fcc09a6b36c` en este ejemplo. A continuación, haga clic en **Enviar**.

![Ingesta de datos](./images/sdkpm10.png)

A continuación, verá esta respuesta.

![Ingesta de datos](./images/sdkpm12.png)

El destino se creará en Adobe Experience Platform. Vamos allí y vamos a comprobarlo.

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Destinos**, haz clic en **Catálogo** y desplázate hacia abajo hasta la categoría **Transmisión**. Ahora verá su destino disponible allí.

![Ingesta de datos](./images/destsdk1.png)

## Vincule el segmento a su destino

En **Destinos** > **Catálogo**, haga clic en **Configurar** en su destino para empezar a agregar segmentos a su nuevo destino.

![Ingesta de datos](./images/destsdk2.png)

Escriba un token de portador ficticio, como **1234**. Haga clic en **Conectar con destino**.

![Ingesta de datos](./images/destsdk3.png)

Entonces verá esto... Como nombre de destino, use `--aepUserLdap-- - Webhook`. Seleccione un punto final de su elección, en este ejemplo **EU**. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk4.png)

Si lo desea, puede seleccionar una política de control de datos. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk5.png)

Seleccione el segmento que creó anteriormente, que se llama `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk6.png)

Entonces verá esto... Asegúrese de asignar **SOURCE FIELD** `--aepTenantId--.identification.core.ecid` al campo `Identity: ecid`. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk7.png)

Haga clic en **Finalizar**.

![Ingesta de datos](./images/destsdk8.png)

Su destino ya está activo, las nuevas cualificaciones del segmento se transmitirán ahora a su webhook personalizado.

![Ingesta de datos](./images/destsdk9.png)

## Pruebe la activación del segmento

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Ahora puede seguir el siguiente flujo para acceder al sitio web. Haga clic en **Integraciones**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

En la página **Integraciones**, debe seleccionar la propiedad de recopilación de datos que se creó en el ejercicio 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada demostración, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

En la página de inicio de **Luma**, ve a **Hombres** y haz clic en el producto **PROTEUS FITNESS JACKSHIRT**.

![Ingesta de datos](./images/homenadia.png)

Ahora ha visitado la página de productos de **PROTEUS FITNESS JACKSHIRT**, lo que significa que ahora calificará para el segmento que creó anteriormente en este ejercicio.

![Ingesta de datos](./images/homenadiapp.png)

Cuando abra el Visor de perfiles y vaya a **Segmentos**, verá que el segmento cumple los requisitos.

![Ingesta de datos](./images/homenadiapppb.png)

Ahora, vuelva al gancho web abierto en [https://webhook.site/](https://webhook.site/), donde debería ver una nueva solicitud entrante, que se origina desde Adobe Experience Platform y que contiene el evento de calificación de segmentos.

![Ingesta de datos](./images/destsdk10.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../../overview.md)
