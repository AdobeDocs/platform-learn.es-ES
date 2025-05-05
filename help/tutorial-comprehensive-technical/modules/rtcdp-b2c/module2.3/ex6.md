---
title: 'Real-time CDP: destinos SDK'
description: 'Real-time CDP: destinos SDK'
kt: 5342
doc-type: tutorial
exl-id: 5606ca2f-85ce-41b3-80f9-3c137f66a8c0
source-git-commit: c49b41e1b033573dbebc9ced3a3f4071bf94d04e
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 5%

---

# 2.3.6 Destinos SDK

## Configuración del proyecto de Adobe I/O

En este ejercicio volverá a utilizar Adobe I/O para consultar las API de Adobe Experience Platform. Si aún no ha configurado el proyecto de Adobe I/O, vuelva al [Ejercicio 3 en el Módulo 2.1](../module2.1/ex3.md) y siga las instrucciones que se indican a continuación.

>[!IMPORTANT]
>
>Si eres un empleado de Adobe, sigue las instrucciones aquí para usar [PostBuster](./../../../postbuster.md).

## Autenticación en el Adobe I/O

En este ejercicio volverá a utilizar Postman para consultar las API de Adobe Experience Platform. Si aún no configuró la aplicación Postman, vuelva al [Ejercicio 3 del módulo 2.1](../module2.1/ex3.md) y siga las instrucciones que se indican a continuación.

>[!IMPORTANT]
>
>Si eres un empleado de Adobe, sigue las instrucciones aquí para usar [PostBuster](./../../../postbuster.md).

## Definir punto final y formato

Para este ejercicio, necesitará un punto final que configurar para que cuando una audiencia se califique, el evento de calificación se pueda transmitir a ese punto final. En este ejercicio, usará un extremo de ejemplo con [https://pipedream.com/requestbin](https://pipedream.com/requestbin). Vaya a [https://pipedream.com/requestbin](https://pipedream.com/requestbin), cree una cuenta y luego un área de trabajo. Una vez creado el espacio de trabajo, verá algo similar a esto.

Haga clic en **copiar** para copiar la dirección URL. Deberá especificar esta dirección URL en el siguiente ejercicio. La dirección URL de este ejemplo es `https://eodts05snjmjz67.m.pipedream.net`.

![Ingesta de datos](./images/webhook1.png)

En cuanto al formato, se utiliza una plantilla estándar que transmite las cualificaciones o descualificaciones de la audiencia junto con metadatos como los identificadores de cliente. Las plantillas se pueden personalizar para satisfacer las expectativas de puntos finales específicos, pero en este ejercicio reutilizaremos una plantilla estándar, lo que dará como resultado una carga útil como esta que se transmitirá al punto final.

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

El primer paso para crear su propio destino en Adobe Experience Platform es crear una configuración de servidor y plantilla con Postman.

Para ello, abra su aplicación de Postman, vaya a la **API de creación de destinos**, a **plantillas y servidores de destino** y haga clic para abrir la solicitud **POST: cree una configuración de servidor de destino**.

>[!NOTE]
>
>Si no tiene esa colección de Postman, vuelva a [Ejercicio 3 en el módulo 2.1](../module2.1/ex3.md) y siga las instrucciones para configurar Postman con las colecciones de Postman proporcionadas.

Entonces verá esto... En **Encabezados**, debe actualizar manualmente el valor de la clave **x-sandbox-name** y establecerlo en `--aepSandboxName--`. Seleccione el valor **{{SANDBOX_NAME}}**.

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

Después de pegar el código anterior, debe actualizar manualmente el campo **urlBasedDestination.url.value** y establecerlo en la dirección URL del webhook que creó en el paso anterior, que era `https://eodts05snjmjz67.m.pipedream.net` en este ejemplo.

![Ingesta de datos](./images/sdkpm4.png)

Después de actualizar el campo **urlBasedDestination.url.value**, debería tener este aspecto. Haga clic en **Enviar**.

![Ingesta de datos](./images/sdkpm5.png)

>[!NOTE]
>
>Recuerde que antes de enviar una solicitud al Adobe I/O, necesita tener un(a) `access_token` válido(a). Para obtener un `access_token` válido, ejecute el POST de solicitud **Obtener token de acceso** en la colección **E/S de Adobe - OAuth**.

Después de hacer clic en **Enviar**, se creará la plantilla de servidor y, como parte de la respuesta, verá un campo denominado **instanceId**. Escríbelo, ya que lo necesitará en el siguiente paso. En este ejemplo, **instanceId** es
`52482c90-8a1e-42fc-b729-7f0252e5cebd`.

![Ingesta de datos](./images/sdkpm6.png)

## Cree la configuración de destino

En Postman, en **API de creación de destino**, vaya a **Configuraciones de destino** y haga clic para abrir el POST de solicitud **Crear una configuración de destino**. Entonces verá esto... En **Encabezados**, debe actualizar manualmente el valor de la clave **x-sandbox-name** y establecerlo en `--aepSandboxName--`. Seleccione el valor **{{SANDBOX_NAME}}** y reemplácelo por `--aepSandboxName--`.

![Ingesta de datos](./images/sdkpm7.png)

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
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=es",
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

Después de pegar el código anterior, debe actualizar manualmente el campo **destinationDelivery. destinationServerId** y debe establecerlo en **instanceId** de la plantilla de servidor de destino que creó en el paso anterior, que era `52482c90-8a1e-42fc-b729-7f0252e5cebd` en este ejemplo. A continuación, haga clic en **Enviar**.

![Ingesta de datos](./images/sdkpm10.png)

A continuación, verá esta respuesta.

![Ingesta de datos](./images/sdkpm12.png)

El destino se creará en Adobe Experience Platform. Vamos allí y vamos a comprobarlo.

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Destinos**, haz clic en **Catálogo** y desplázate hacia abajo hasta la categoría **Transmisión**. Ahora verá su destino disponible allí.

![Ingesta de datos](./images/destsdk1.png)

## Vincule la audiencia al destino

En **Destinos** > **Catálogo**, haga clic en **Configurar** en el destino para empezar a agregar audiencias al nuevo destino.

![Ingesta de datos](./images/destsdk2.png)

Escriba un valor aleatorio para **token de portador**, como **1234**. Haga clic en **Conectar con destino**.

![Ingesta de datos](./images/destsdk3.png)

Entonces verá esto... Como nombre de destino, use `--aepUserLdap-- - Webhook`. Seleccione un punto final de su elección, en este ejemplo **EU**. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk4.png)

Si lo desea, puede seleccionar una política de control de datos. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk5.png)

Seleccione la audiencia que creó anteriormente, que se llama `--aepUserLdap-- - Interest in Galaxy S24`. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk6.png)

Entonces verá esto... Asegúrese de asignar **SOURCE FIELD** `--aepTenantId--.identification.core.ecid` al campo `Identity: ecid`. Haga clic en **Next**.

![Ingesta de datos](./images/destsdk7.png)

Haga clic en **Finalizar**.

![Ingesta de datos](./images/destsdk8.png)

El destino ya está activo. Las nuevas cualificaciones de audiencia se transmitirán ahora al webhook personalizado.

![Ingesta de datos](./images/destsdk9.png)

## Prueba de la activación de audiencia

Vaya a [https://dsn.adobe.com](https://dsn.adobe.com). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en los 3 puntos **...** del proyecto del sitio web y, a continuación, haga clic en **Ejecutar** para abrirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada ejercicio, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

En este ejemplo, desea responder a un cliente específico que ve un producto específico.
En la página de inicio de **Citi Signal**, ve a **Teléfonos y dispositivos** y haz clic en el producto **Galaxy S24**.

![Ingesta de datos](./images/homegalaxy.png)

Ya se ha visto la página de productos del Galaxy S24, por lo que su audiencia podrá acceder a su perfil en los minutos siguientes.

![Ingesta de datos](./images/homegalaxy1.png)

Cuando abra el Visor de perfiles y vaya a **Audiencias**, verá que la audiencia cumple los requisitos.

![Ingesta de datos](./images/homegalaxydsdk.png)

Ahora, vuelva al gancho web abierto en [https://eodts05snjmjz67.m.pipedream.net](https://eodts05snjmjz67.m.pipedream.net), donde debería ver una nueva solicitud entrante, que se origina en Adobe Experience Platform y que contiene el evento de calificación de audiencia.

![Ingesta de datos](./images/destsdk10.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../../overview.md)
