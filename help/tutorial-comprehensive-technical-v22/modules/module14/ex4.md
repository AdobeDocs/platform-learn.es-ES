---
title: 'Recopilación de datos y reenvío del lado del servidor en tiempo real: creación y configuración de una función de Google Cloud'
description: Creación y configuración de una función de Google Cloud
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: d3678a30-6df9-44aa-a2fa-970127f75f59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 0%

---

# 14.4 Crear y configurar una función de nube de Google

## 14.4.1 Crear la función de nube de Google

Vaya a [https://console.cloud.google.com/](https://console.cloud.google.com/). Vaya a **Funciones de nube**.

![GCP](./images/gcp1.png)

Entonces verás esto. Haga clic en **CREAR FUNCIÓN**.

![GCP](./images/gcp2.png)

Entonces verás esto.

![GCP](./images/gcp6.png)

Realice las siguientes opciones:

- **Nombre de función**: `--demoProfileLdap---event-forwarding`
- **Región**: seleccionar cualquier región
- **Tipo de déclencheur**: select **HTTP**
- **Autenticación**: select **Permitir invocaciones no autenticadas**

Ahora deberías tener esto. Haga clic en **GUARDAR**.

![GCP](./images/gcp7.png)

Haga clic en **SIGUIENTE**.

![GCP](./images/gcp8.png)

Verá esto:

![GCP](./images/gcp9.png)

Realice las siguientes opciones:

- **Tiempo de ejecución**: select **Node.js 16** (o más reciente)
- **Punto de entrada**: enter **helloAEP**

Haga clic en **HABILITAR API** para habilitar **API de compilación en la nube**. A continuación, verá una nueva ventana. En esa nueva ventana, haga clic en **HABILITAR** de nuevo.

![GCP](./images/gcp10.png)

Entonces verás esto. Haga clic en **Habilitar**.

![GCP](./images/gcp11.png)

Una vez **API de compilación en la nube** se ha habilitado, verá esto.

![GCP](./images/gcp12.png)

Vuelva a su **Función en la nube**.
En el Editor en línea de funciones de Cloud, asegúrese de que tiene el siguiente código:

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

A continuación, haga clic en **IMPLEMENTACIÓN**.

![GCP](./images/gcp13.png)

Entonces verás esto. Se está creando la función de nube. Esto puede tardar un par de minutos.

![GCP](./images/gcp14.png)

Una vez que la función se haya creado y ejecutado, lo verá. Haga clic en el nombre de la función para abrirla.

![GCP](./images/gcp15.png)

Entonces verás esto. Vaya a **DÉCLENCHEUR**. Verá el **URL de déclencheur** que es lo que utilizará para definir el punto final en el servidor de Launch.

![GCP](./images/gcp16.png)

Copie la dirección URL del Déclencheur, que tiene este aspecto: **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**.

En los pasos siguientes, configurará el servidor de recopilación de datos de Adobe Experience Platform para transmitir información específica sobre **Vistas de páginas** a su función de Google Cloud. En lugar de reenviar la carga útil completa tal cual, solo enviará cosas como **ECID**, **timestamp** y **Nombre de la página** a su función de Google Cloud.

Este es un ejemplo de carga útil que debe analizar para filtrar las variables mencionadas anteriormente:

```json
{
  "events": [
    {
      "xdm": {
        "eventType": "web.webpagedetails.pageViews",
        "web": {
          "webPageDetails": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC",
            "name": "vangeluw-OCUC",
            "viewName": "vangeluw-OCUC",
            "pageViews": {
              "value": 1
            }
          },
          "webReferrer": {
            "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/equipment"
          }
        },
        "device": {
          "screenHeight": 1080,
          "screenWidth": 1920,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1920,
            "viewportHeight": 451
          }
        },
        "placeContext": {
          "localTime": "2022-02-23T06:51:07.140+01:00",
          "localTimezoneOffset": -60
        },
        "timestamp": "2022-02-23T05:51:07.140Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy/reactor",
          "version": "2.8.0+2.9.0",
          "environment": "browser"
        },
        "_experienceplatform": {
          "identification": {
            "core": {
              "ecid": "08346969856929444850590365495949561249"
            }
          },
          "demoEnvironment": {
            "brandName": "vangeluw-OCUC"
          },
          "interactionDetails": {
            "core": {
              "channel": "web"
            }
          }
        }
      },
      "query": {
        "personalization": {
          "schemas": [
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
          ],
          "decisionScopes": [
            "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0YzA1MjM4MmUxYjY1MDUiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTRiZjA5ZGM0MTkwZWJiYSJ9",
            "__view__"
          ]
        }
      }
    }
  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  },
  "meta": {
    "state": {
      "domain": "adobedemo.com",
      "cookiesEnabled": true,
      "entries": [
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_identity",
          "value": "CiYwODM0Njk2OTg1NjkyOTQ0NDg1MDU5MDM2NTQ5NTk0OTU2MTI0OVIPCPn66KfyLxgBKgRJUkwx8AH5-uin8i8="
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent_check",
          "value": "1"
        },
        {
          "key": "kndctr_907075E95BF479EC0A495C73_AdobeOrg_consent",
          "value": "general=in"
        }
      ]
    }
  }
}
```

Estos son los campos que contienen la información que debe analizarse:

- ECID: **events.xdm._experienceplatform.identification.core.ecid**
- timestamp: **timestamp**
- Nombre de página: **events.xdm.web.webPageDetails.name**

Ahora vamos al servidor de recopilación de datos de Adobe Experience Platform para configurar los elementos de datos y hacerlo posible.

## 14.4.2 Actualice la propiedad Event Forwarding: Elementos de datos

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) y vaya a **Reenvío de eventos**. Busque la propiedad Event Forwarding y haga clic en ella para abrirla.

![SSF de recopilación de datos de Adobe Experience Platform](./images/prop1.png)

En el menú de la izquierda, vaya a **Elementos de datos**. Haga clic en **Añadir elemento de datos**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/de1gcp.png)

A continuación, verá un nuevo elemento de datos para configurar.

![SSF de recopilación de datos de Adobe Experience Platform](./images/de2gcp.png)

Realice la siguiente selección:

- Como **Nombre**, introduzca **customerECID**.
- Como **Extensión**, seleccione **Principal**.
- Como **Tipo de elemento de datos**, seleccione **Ruta**.
- Como **Ruta**, introduzca `arc.event.xdm.--aepTenantId--.identification.core.ecid`. Al introducir esta ruta, se filtrará el campo **ecid** desde la carga útil de evento que envía el sitio web o la aplicación móvil a Adobe Edge.

>[!NOTE]
>
>En las rutas arriba y abajo, se hace referencia a **arc**. **arc** representa Contexto de Recursos de Adobe y **arc** representa siempre el objeto más alto disponible que está disponible en el contexto del servidor. Los enriquecimientos y transformaciones pueden añadirse a los **arc** mediante las funciones del servidor de recopilación de datos de Adobe Experience Platform.
>
>En las rutas arriba y abajo, se hace referencia a **evento**. **evento** significa un evento único y Adobe Experience Platform Data Collection Server siempre evaluará cada evento individualmente. A veces, es posible que vea una referencia a **events** en la carga útil que envía el cliente del SDK web, pero en el servidor de recopilación de datos de Adobe Experience Platform, cada evento se evalúa individualmente.

Ahora tendrás esto. Haga clic en **Guardar**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/gcdpde1.png)

Haga clic en **Añadir elemento de datos**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/addde.png)

A continuación, verá un nuevo elemento de datos para configurar.

![SSF de recopilación de datos de Adobe Experience Platform](./images/de2gcp.png)

Realice la siguiente selección:

- Como **Nombre**, introduzca **eventTimestamp**.
- Como **Extensión**, seleccione **Principal**.
- Como **Tipo de elemento de datos**, seleccione **Ruta**.
- Como **Ruta**, introduzca **arc.event.xdm.timestamp**. Al introducir esta ruta, se filtrará el campo **timestamp** desde la carga útil de evento que envía el sitio web o la aplicación móvil a Adobe Edge.

Ahora tendrás esto. Haga clic en **Guardar**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/gcdpde2.png)

Haga clic en **Añadir elemento de datos**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/addde.png)

A continuación, verá un nuevo elemento de datos para configurar.

![SSF de recopilación de datos de Adobe Experience Platform](./images/de2gcp.png)

Realice la siguiente selección:

- Como **Nombre**, introduzca **pageName**.
- Como **Extensión**, seleccione **Principal**.
- Como **Tipo de elemento de datos**, seleccione **Ruta**.
- Como **Ruta**, introduzca **arc.event.xdm.web.webPageDetails.name**. Al introducir esta ruta, se filtrará el campo **name** desde la carga útil de evento que envía el sitio web o la aplicación móvil a Adobe Edge.

Ahora tendrás esto. Haga clic en **Guardar**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/gcdpde3.png)

Ahora tiene estos elementos de datos creados:

![SSF de recopilación de datos de Adobe Experience Platform](./images/de3gcp.png)

## 14.4.3 Actualice la propiedad Event Forwarding : Actualizar una regla

En el menú de la izquierda, vaya a **Reglas**. En el ejercicio anterior, creó la regla **Todas las páginas**. Haga clic en esa regla para abrirla.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl1gcp.png)

Entonces lo harás. Haga clic en el **+** icono bajo **Acciones** para agregar una nueva acción.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl2gcp.png)

Entonces verás esto.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl4gcp.png)

Realice la siguiente selección:

- Seleccione el **Extensión**: **Conector de Adobe Cloud**.
- Seleccione el **Tipo de acción**: **Llamada de recuperación**.

Eso debería darte esto **Nombre**: **Conector de Adobe Cloud: Realizar llamada de recuperación**. Ahora debería ver esto:

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl5gcp.png)

A continuación, configure lo siguiente:

- Cambie el protocolo de solicitud de GET a **POST**
- Introduzca la URL de la función de nube de Google que ha creado en uno de los pasos anteriores con este aspecto: **https://europe-west1-dazzling-pillar-273812.cloudfunctions.net/vangeluw-event-forwarding**

Ahora deberías tener esto. A continuación, vaya a **Cuerpo**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl6gcp.png)

Entonces verás esto. Haga clic en el botón de opción para **JSON**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl7gcp.png)

Configure las variables **Cuerpo** de la siguiente manera:

| CLAVE | VALOR |
|--- |--- |
| customerECID | {{customerECID}} |
| pageName | {{pageName}} |
| eventTimestamp | {{eventTimestamp}} |

Entonces verás esto. Haga clic en **Mantener cambios**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl9gcp.png)

Entonces verás esto. Haga clic en **Guardar**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl10gcp.png)

Ahora ha actualizado la regla existente en una propiedad del servidor de recopilación de datos de Adobe Experience Platform. Vaya a **Flujo de publicación** para publicar los cambios. Abra la biblioteca de desarrollo. **Principal** haciendo clic en **Editar** como se indica.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl12gcp.png)

Haga clic en el **Agregar todos los recursos modificados** , después de lo cual verá su Regla y el Elemento de datos en esta biblioteca. A continuación, haga clic en **Guardar y generar para desarrollo**. Los cambios se están implementando.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl13gcp.png)

Después de un par de minutos, verá que la implementación ha finalizado y está lista para probarse.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl14.png)

## 14.3.4 Probar la configuración

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../module0/images/web8.png)

Ahora puede seguir el flujo siguiente para acceder al sitio web. Haga clic en **Integraciones**.

![DSN](../module0/images/web1.png)

En el **Integraciones** , debe seleccionar la propiedad Recopilación de datos que se creó en el ejercicio 0.1.

![DSN](../module0/images/web2.png)

Verá que su sitio web de demostración se abre. Seleccione la dirección URL y cópiela en el portapapeles.

![DSN](../module0/images/web3.png)

Abra una nueva ventana del explorador incógnito.

![DSN](../module0/images/web4.png)

Pegue la dirección URL del sitio web de la demostración, que copió en el paso anterior. A continuación, se le pedirá que inicie sesión con su Adobe ID.

![DSN](../module0/images/web5.png)

Seleccione su tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../module0/images/web6.png)

Verá su sitio web cargado en una ventana del navegador incógnito. Para cada demostración, tendrá que usar una ventana nueva del explorador incógnito para cargar la URL de su sitio web de demostración.

![DSN](../module0/images/web7.png)

Cuando abra la vista del desarrollador del explorador, podrá inspeccionar las solicitudes de red como se indica a continuación. Al utilizar el filtro **interactuar**, verá las solicitudes de red que envía el cliente de recopilación de datos de Adobe Experience Platform a Adobe Edge.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook1.png)

Cambie la vista a la función de Google Cloud y vaya a **REGISTROS**. Ahora debería tener una vista similar a esta, con una serie de entradas de registro mostradas. Cada vez que ve **Ejecución de la función iniciada**, significa que el tráfico entrante se recibió en su función de Google Cloud.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook3gcp.png)

Actualicemos un poco su función para trabajar con los datos entrantes y mostrar la información recibida del servidor de recopilación de datos de Adobe Experience Platform. Vaya a **FUENTE** y haga clic en **EDITAR**.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook4gcp.png)

En la siguiente pantalla, haga clic en **SIGUIENTE**.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/gcf1.png)

Actualice el código de esta manera:

```javascript
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloAEP = (req, res) => {
  console.log('>>>>> Function has started. The following information was received from Event Forwarding:');
  console.log(req.body);

  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
```

Entonces tendrás esto. Haga clic en **IMPLEMENTACIÓN**.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/gcf2.png)

Después de un par de minutos, la función se volverá a implementar. Haga clic en el nombre de la función para abrirla.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/gcf3.png)

En el sitio web de demostración, vaya a un producto, como por ejemplo **CAPRI DE ENCABEZADO RELAJADO**.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/gcf3a.png)

Cambie la vista a la función de Google Cloud y vaya a **REGISTROS**. Ahora debería tener una vista similar a esta, con una serie de entradas de registro mostradas.

Ahora, por cada vista de página en su sitio web de demostración, debería ver una nueva entrada de registro en los registros de su función de nube de Google, que muestran la información recibida.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/gcf4.png)

Ahora ha enviado correctamente los datos recopilados por la recopilación de datos de Adobe Experience Platform, en tiempo real, a un extremo de la función de Google Cloud. Desde allí, cualquier aplicación de Google Cloud Platform, como BigQuery, puede utilizar esos datos para el almacenamiento y la elaboración de informes, o para casos de uso de aprendizaje automático.

Paso siguiente: [14.5 Avanzar hacia el ecosistema de AWS](./ex5.md)

[Volver al módulo 14](./aep-data-collection-ssf.md)

[Volver a todos los módulos](./../../overview.md)
