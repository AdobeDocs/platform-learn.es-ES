---
title: 'Recopilación de datos y reenvío del lado del servidor en tiempo real: creación y configuración de una función de nube de Google'
description: Creación y configuración de una función de nube de Google
kt: 5342
doc-type: tutorial
exl-id: bdee5a9b-2f1a-467e-9edc-a2e10a263694
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---

# 2.5.4 Reenviar eventos a GCP Pub/Sub

>[!NOTE]
>
>Para este ejercicio, necesita acceder a un entorno de Google Cloud Platform. Si todavía no tiene acceso a GCP, cree una nueva cuenta con su dirección de correo electrónico personal.

## Cree su Pub/Subtema de Google Cloud

Vaya a [https://console.cloud.google.com/](https://console.cloud.google.com/). En la barra de búsqueda, escriba `pub/sub`. Haga clic en el resultado de búsqueda **Pub/Sub - Global real-time messaging**.

![GCP](./images/gcp1.png)

Entonces verá esto... Haga clic en **CREAR TEMA**.

![GCP](./images/gcp2.png)

Entonces verá esto... Para el identificador de tema, use `--aepUserLdap---event-forwarding`. Haga clic en **Crear**.

![GCP](./images/gcp6.png)

Se creará el tema. Haga clic en **ID de suscripción** del tema.

![GCP](./images/gcp7.png)

Entonces verá esto... Copie el **nombre del tema** en el portapapeles y guárdelo, tal como lo necesitará en los próximos ejercicios.

![GCP](./images/gcp8.png)

Ahora vamos al reenvío de eventos de recopilación de datos de Adobe Experience Platform para actualizar la propiedad de reenvío de eventos y comenzar a reenviar eventos a Pub/Sub.


## Actualice la propiedad del reenvío de eventos: Secrets

Los **secretos** de las propiedades de reenvío de eventos se usan para almacenar credenciales que se usarán para autenticarse en las API externas. En este ejemplo, debe configurar un secreto para almacenar el token OAuth de Google Cloud Platform, que se utilizará para autenticar al utilizar Pub/Sub para transmitir datos hacia GCP.

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) y luego a **Secretos**. Haga clic en **Crear nuevo secreto**.

![Recopilación de datos Adobe Experience Platform SSF](./images/secret1.png)

Entonces verá esto... Siga estas instrucciones:

- Nombre: use `--aepUserLdap---gcp-secret`
- Entorno de destino: seleccionar **Desarrollo**
- Tipo: **Google OAuth 2**
- Marque la casilla de verificación de **Pub/Sub**

Haga clic en **Crear secreto**.

![Recopilación de datos Adobe Experience Platform SSF](./images/secret2.png)

Después de hacer clic en **Crear secreto**, verá una ventana emergente para configurar la autenticación entre el secreto de la propiedad de reenvío de eventos y Google. Haga clic en **Crear y autorizar secreto `--aepUserLdap---gcp-secret` con Google**.

![Recopilación de datos Adobe Experience Platform SSF](./images/secret3.png)

Haga clic en para seleccionar su cuenta de Google.

![Recopilación de datos Adobe Experience Platform SSF](./images/secret4.png)

Haga clic en **Continuar**.

>[!NOTE]
>
>El mensaje emergente puede variar. Autorice o permita el acceso solicitado para continuar con el ejercicio.

![Recopilación de datos Adobe Experience Platform SSF](./images/secret5.png)

Después de autenticarse correctamente, verá esto.

![Recopilación de datos Adobe Experience Platform SSF](./images/secret6.png)

El secreto se ha configurado correctamente y se puede utilizar en un elemento de datos.

## Actualice la propiedad de reenvío de eventos: elemento de datos

Para utilizar el secreto en la propiedad de reenvío de eventos, debe crear un elemento de datos que almacene el valor del secreto.

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) y luego a **Reenvío de eventos**. Busque la propiedad Reenvío de eventos y haga clic en ella para abrirla.

![Recopilación de datos Adobe Experience Platform SSF](./images/prop1.png)

En el menú de la izquierda, vaya a **Elementos de datos**. Haga clic en **Agregar elemento de datos**.

![Recopilación de datos Adobe Experience Platform SSF](./images/de1gcp.png)

Configure el elemento de datos de esta manera:

- Nombre: **Secreto de GCP**
- Extensión: **Core**
- Tipo de elemento de datos: **Secreto**
- Secreto de desarrollo: seleccione el secreto que creó, que se llama `--aepUserLdap---gcp-secret`

Haga clic en **Guardar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/secret7.png)

## Actualice la propiedad de reenvío de eventos: Extensión

Con el Secreto y el Elemento de datos configurados, ahora puede configurar la extensión para Google Cloud Platform en la propiedad Reenvío de eventos.

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), vaya a **Reenvío de eventos** y abra su propiedad de Reenvío de eventos.

![Recopilación de datos Adobe Experience Platform SSF](./images/prop1.png)

A continuación, vaya a **Extensions**, para **Catalog**. Haga clic en la extensión **Google Cloud Platform** y luego en **Instalar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/gext2.png)

Entonces verá esto... Haga clic en el icono Elemento de datos.

![Recopilación de datos Adobe Experience Platform SSF](./images/gext3.png)

Seleccione el elemento de datos que creó en el ejercicio anterior, que se llama **Secreto GCP**. Haga clic en **Seleccionar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/gext4.png)

Entonces verá esto... Haga clic en **Guardar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/gext5.png)

## Actualizar la propiedad de reenvío de eventos: Actualizar una regla

Ahora que la extensión de Google Cloud Platform está configurada, puede definir una regla para comenzar a reenviar datos de evento a su tema de publicación/subtema. Para ello, deberá actualizar la regla **Todas las páginas** que creó en uno de los ejercicios anteriores.

En el menú de la izquierda, ve a **Reglas**. En el ejercicio anterior creó la regla **Todas las páginas**. Haga clic en esa regla para abrirla.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl1gcp.png)

Entonces vas a hacer esto. Haga clic en el icono **+** debajo de **Acciones** para agregar una acción nueva.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl2gcp.png)

Entonces verá esto... Realice la siguiente selección:

- Seleccione la **extensión**: **Google Cloud Platform**.
- Seleccione **Tipo de acción**: **Enviar datos a Cloud Pub/Sub**.

Esto debería darle este **Nombre**: **Google Cloud Platform - Enviar datos a Cloud Pub/Sub**. Ahora debería ver esto:

![Recopilación de datos Adobe Experience Platform SSF](./images/rl5gcp.png)

Ahora debe configurar el tema Pub/Sub que creó anteriormente.

Puede encontrar el **nombre del tema** aquí, cópielo.

![GCP](./images/gcp8.png)

Pegue **Topic name** en la configuración de regla. A continuación, haga clic en el icono Elemento de datos junto al campo **Datos (obligatorios)**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl6gcp.png)

Seleccione **Evento XDM** y haga clic en **Seleccionar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl7gcp.png)

Entonces verá esto... Haga clic en **Conservar cambios**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl8gcp.png)

Haga clic en **Guardar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl9gcp.png)

Entonces verá esto...

![Recopilación de datos Adobe Experience Platform SSF](./images/rl10gcp.png)

## Publicación de los cambios

La configuración ha finalizado. Vaya a **Flujo de publicación** para publicar los cambios. Abra la biblioteca de desarrollo **Main** haciendo clic en **Editar** como se indica.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl12gcp.png)

Haga clic en el botón **Agregar todos los recursos modificados**, tras lo cual verá que la regla y el elemento de datos aparecen en esta biblioteca. A continuación, haga clic en **Guardar y generar para desarrollo**. Los cambios se están implementando.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl13gcp.png)

Después de un par de minutos, verá que la implementación está completa y lista para probarse.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl14.png)

## Pruebe la configuración

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

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada ejercicio, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Cambie la vista a su Google Cloud Pub/Sub y vaya a **MESSAGES**. Haz clic en **EXTRAER** y después de unos segundos verás algunos mensajes en la lista. Haga clic en un mensaje para visualizar su contenido.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook3gcp.png)

Ahora puede ver la carga útil XDM del evento en Google Pub/Sub. Ahora ha enviado correctamente los datos recopilados por la recopilación de datos de Adobe Experience Platform, en tiempo real, a un extremo Pub/Sub de Google Cloud. A partir de ahí, esos datos se pueden utilizar en cualquier aplicación de Google Cloud Platform, como BigQuery para almacenamiento y creación de informes o para casos de uso de aprendizaje automático.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook4gcp.png)

## Pasos siguientes

Ir a [2.5.5 Reenviar eventos a AWS Kinesis y AWS S3](./ex5.md){target="_blank"}

Volver a [Conexiones de Real-Time CDP: reenvío de eventos](./aep-data-collection-ssf.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
