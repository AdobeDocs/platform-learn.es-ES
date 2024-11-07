---
title: 'Recopilación de datos y reenvío de eventos: reenvío de eventos hacia el ecosistema de AWS'
description: Reenviar eventos hacia el ecosistema de AWS
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 2%

---

# 2.5.5 Avanzar eventos hacia el ecosistema de AWS

>[!IMPORTANT]
>
>La finalización de este ejercicio es opcional y conlleva un coste utilizar AWS Kinesis. Aunque AWS proporciona una cuenta de nivel gratuita que le permite probar y configurar muchos servicios sin coste, AWS Kinesis no forma parte de esa cuenta de nivel gratuito. Por lo tanto, para implementar y probar este ejercicio, se tendrá en cuenta un coste para utilizar AWS Kinesis.

## Es bueno saber

Adobe Experience Platform admite varios servicios de Amazon como destino.
Kinesis y S3 son [destinos de exportación de perfiles](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en) y se pueden usar como parte de Real-Time CDP de Adobe Experience Platform.
Puede incorporar fácilmente eventos de segmentos de alto valor y atributos de perfil asociados a sus sistemas de elección.

En esta nota, aprenderá a configurar su propio flujo de Kinesis de Amazon para transmitir datos de evento procedentes del ecosistema de Edge de Adobe Experience Platform a un destino de almacenamiento en la nube, como Amazon S3. Esto resulta útil en caso de que desee recopilar eventos de experiencia de propiedades web y móviles e insertarlos en el conjunto de datos para su análisis e informes operativos. Por lo general, los conjuntos de datos consumen datos por lotes con grandes importaciones diarias de archivos, y no exponen puntos finales http públicos que podrían utilizarse junto con el reenvío de eventos.

El soporte de los casos de uso anteriores implica que los datos transmitidos deben almacenarse en búfer o colocarse en cola antes de escribirse en un archivo. Se debe tener cuidado de no abrir el archivo para tener acceso de escritura en varios procesos. Delegar esta tarea en un sistema específico es ideal para escalar bien y, al mismo tiempo, garantizar un gran nivel de servicio. Aquí es donde Kinesis acude en rescate.

Amazon Kinesis Data Streams se centra en la ingesta y el almacenamiento de flujos de datos. Kinesis Data Firefox se centra en ofrecer flujos de datos a destinos seleccionados, como bloques de S3.

Como parte de este ejercicio, usted...

- Realizar una configuración básica de un flujo de datos de Kinesis
- Cree un flujo de entrega de Firefox y utilice el compartimento S3 como destino
- Configure la puerta de enlace de la API de Amazon como extremo de la API REST para recibir los datos de evento
- Reenviar datos de evento sin procesar del Edge de Adobe al flujo de Kinesis

## 2.5.5.1 Configuración del contenedor de AWS S3

Vaya a [https://console.aws.amazon.com](https://console.aws.amazon.com) e inicie sesión con la cuenta de Amazon que creó anteriormente.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awshome.png)

Después de iniciar sesión, se le redirigirá a **AWS Management Console**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awsconsole.png)

En el menú **Buscar servicios**, busque **s3**. Haga clic en el primer resultado de búsqueda: **S3 - Almacenamiento escalable en la nube**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awsconsoles3.png)

Luego verá la página principal de **Amazon S3**. Haga clic en **Crear cubo**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/s3home.png)

En la pantalla **Crear cubo**, debe configurar dos cosas:

- Nombre: use el nombre `eventforwarding---aepUserLdap--`. Por ejemplo, en este ejercicio el nombre del contenedor es **aepmodulertcdpvangeluw**
- Región: use la región **EU (Frankfurt) eu-central-1**

![ETL](./images/bucketname.png)

Mantenga el resto de configuraciones predeterminadas tal cual. Desplácese hacia abajo y haga clic en **Crear cubo**.

![ETL](./images/createbucket.png)

A continuación, verá que se está creando su contenedor y se redirigirá a la página principal de Amazon S3.

![ETL](./images/S3homeb.png)

## 2.5.5.2 Configuración del flujo de datos de AWS Kinesis

En el menú **Buscar servicios**, busque **kinesis**. Haga clic en el primer resultado de búsqueda: **Kinesis - Trabajar con datos de flujo en tiempo real**.

![ETL](./images/kinesis1.png)

Seleccione **Transmisiones de datos de Kinesis**. Haga clic en **Crear flujo de datos**.

![ETL](./images/kinesis2.png)

Para el **nombre de secuencia de datos**, use `--aepUserLdap---datastream`.

![ETL](./images/kinesis3.png)

No es necesario cambiar ninguna de las otras opciones de configuración. Desplácese hacia abajo y haga clic en **Crear flujo de datos**.

![ETL](./images/kinesis4.png)

Entonces verá esto... Una vez que el flujo de datos se haya creado correctamente, puede pasar al siguiente ejercicio.

![ETL](./images/kinesis5.png)

## 2.5.5.3 Configuración del flujo de entrega de AWS Firefox

En el menú **Buscar servicios**, busque **kinesis**. Haga clic en **Kinesis Data Firehouse**.

![ETL](./images/kinesis6.png)

Haga clic en **Crear flujo de entrega**.

![ETL](./images/kinesis7.png)

Para **Source**, seleccione **Amazon Kinesis Data Streams**. Para **Destino**, seleccione **Amazon S3**. Haga clic en **Examinar** para seleccionar el flujo de datos.

![ETL](./images/kinesis8.png)

Seleccione el flujo de datos. Haga clic en **Elegir**.

![ETL](./images/kinesis9.png)

Entonces verá esto... Recuerde el **nombre de flujo de entrega**, ya que lo necesitará más adelante.

![ETL](./images/kinesis10.png)

Desplácese hacia abajo hasta que vea **Configuración de destino**. Haga clic en **Examinar** para seleccionar el espacio de S3.

![ETL](./images/kinesis11.png)

Seleccione su compartimento de S3 y haga clic en **Elegir**.

![ETL](./images/kinesis12.png)

Entonces verás algo como esto. Actualice la siguiente configuración:

- Partición dinámica: establecer en **Enabled**
- Desagregación de varios registros: establecer en **Deshabilitado**
- Nuevo delimitador de línea: establecer en **Habilitado**
- Análisis en línea para JSON: establecido en **Enabled**

![ETL](./images/kinesis13.png)

Desplácese un poco hacia abajo y verá esto. Actualice la siguiente configuración:

- Claves de partición dinámica
   - Nombre de clave: **dynamicPartitioningKey**
   - Expresión JQ: **.dynamicPartitioningKey**
- Prefijo del contenedor S3: añada el siguiente código:

```bash
!{partitionKeyFromQuery:dynamicPartitioningKey}/!{timestamp:yyyy}/!{timestamp:MM}/!{timestamp:dd}/!{timestamp:HH}/}
```

- Prefijo de salida de error de contenedor S3: establecido en **error**

![ETL](./images/kinesis14.png)

Finalmente, desplácese un poco más hacia abajo y haga clic en **Crear flujo de entrega**

![ETL](./images/kinesis15.png)

Después de un par de minutos, su flujo de entrega no se creará y **Activo**.

![ETL](./images/kinesis16.png)

## 2.5.5.4 Configuración de la función de AWS IAM

En el menú **Buscar servicios**, busque **iam**. Haga clic en **puerta de enlace de API**.

![ETL](./images/iam1.png)

Haga clic en **Roles**.

![ETL](./images/iam2.png)

Busque su rol **KinesisFirehouse**. Haga clic en él para abrirlo.

![ETL](./images/iam3.png)

Haga clic en el nombre de la directiva de permisos para abrirla.

![ETL](./images/iam4.png)

En la nueva pantalla que se abre, haga clic en **Editar directiva**.

![ETL](./images/iam5.png)

En **Kinesis** - **Acciones**, asegúrese de que los permisos de **Escritura** para **PutRecord** estén habilitados. Haga clic en **Revisar directiva**.

![ETL](./images/iam6.png)

Haga clic en **Guardar cambios**.

![ETL](./images/iam7.png)

Entonces volverás a estar aquí. Haga clic en **Roles**.

![ETL](./images/iam8.png)

Busque su rol **KinesisFirehouse**. Haga clic en él para abrirlo.

![ETL](./images/iam3.png)

Vaya a **Relaciones de confianza** y haga clic en **Editar directiva de confianza**.

![ETL](./images/iam9.png)

Sobrescriba la directiva de confianza actual pegando este código para reemplazar el código existente:

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"Service": [
                    "firehose.amazonaws.com",
                    "kinesis.amazonaws.com",
                    "apigateway.amazonaws.com"
                ]
			},
			"Action": "sts:AssumeRole"
		}
	]
}
```

Haga clic en **Actualizar directiva**

![ETL](./images/iam10.png)

Entonces verá esto... Deberá especificar **ARN** para este rol en el siguiente paso.

![ETL](./images/iam11.png)

## 2.5.5.5 Configuración de la puerta de enlace de la API de AWS

Amazon API Gateway es un servicio de AWS para crear, publicar, mantener, supervisar y proteger las API de REST, HTTP y WebSocket a cualquier escala. Los desarrolladores de API pueden crear API que accedan a AWS u otros servicios web, así como datos almacenados en AWS Cloud.

Ahora expondrá el flujo de datos de Kinesis a Internet a través de un punto de conexión HTTPS que luego pueden consumir directamente los servicios de Adobe, como el reenvío de eventos.

En el menú **Buscar servicios**, busque **puerta de enlace de API**. Haga clic en **puerta de enlace de API**.

![ETL](./images/kinesis17.png)

Entonces verás algo como esto. Haga clic en **Crear API**.

![ETL](./images/kinesis18.png)

Haga clic en **Generar** en la tarjeta **API REST**.

![ETL](./images/kinesis19.png)

Entonces verá esto... Complete la configuración de esta manera:

- Elija el protocolo: seleccione **REST**
- Crear nueva API: seleccionar **Nueva API**
- Configuración:
   - Nombre de API: usar `--aepUserLdap---eventforwarding`
   - Tipo de extremo: seleccionar **Regional**

Haga clic en **Crear API**.

![ETL](./images/kinesis20.png)

Entonces verá esto... Haga clic en **Acciones** y, a continuación, haga clic en **Crear recurso**.

![ETL](./images/kinesis21.png)

Entonces verá esto... Establezca **Nombre del recurso** en **stream**. Haga clic en **Crear recurso**.

![ETL](./images/kinesis22.png)

Entonces verá esto... Haga clic en **Acciones** y, a continuación, haga clic en **Crear método**.

![ETL](./images/kinesis23.png)

En el menú desplegable, seleccione **POST** y haga clic en el botón **v**.

![ETL](./images/kinesis24.png)

Entonces verá esto... Complete la configuración de esta manera:

- Tipo de integración: **Servicio AWS**
- Región de AWS: seleccione la región que usa el flujo de datos de Kinesis, en este caso: **us-west-2**
- Servicio AWS: seleccione **Kinesis**
- Subdominio de AWS: dejar vacío
- Método HTTP: seleccione **POST**
- Tipo de acción: seleccionar **Usar nombre de acción**
- Acción: ingresar **PutRecord**
- Rol de ejecución: pegue el **ARN** del rol de ejecución que usa su Kinesis Data Firefox, tal como se le indicó en el ejercicio anterior
- Administración de contenido: seleccionar **Pasar**
- Usar tiempo de espera predeterminado: activar la casilla de verificación

Haga clic en **Guardar**.

![ETL](./images/kinesis25.png)

Entonces verá esto... Haga clic en **Solicitud de integración**.

![ETL](./images/kinesis27.png)

Haga clic en **encabezados HTTP**.

![ETL](./images/kinesis28.png)

Desplácese un poco hacia abajo y haga clic en **Agregar encabezado**.

![ETL](./images/kinesis29.png)

Establezca **Name** en **Content-Type**, establezca **Asignado desde** a `'application/x-amz-json-1.1'`. Haga clic en el icono **v** para guardar los cambios.

![ETL](./images/kinesis30.png)

Entonces verá esto... Para **solicitar el paso del cuerpo**, seleccione **Cuando no haya plantillas definidas (recomendado)**. A continuación, haga clic en **Agregar plantilla de asignación**.

![ETL](./images/kinesis31.png)

En **Content-Type**, escriba **application/json**. Haga clic en el icono **v** para guardar los cambios.

![ETL](./images/kinesis32.png)

Desplácese hacia abajo para buscar una ventana del editor de código. Pegue el siguiente código allí:

```json
{
  "StreamName": "$input.path('StreamName')",
  "Data": "$util.base64Encode($input.json('$.Data'))",
  "PartitionKey": "$input.path('$.PartitionKey')"
}
```

Haga clic en **Guardar**.

![ETL](./images/kinesis33.png)

A continuación, desplácese hacia arriba y haga clic en **&lt;- Method Execution** para volver.

![ETL](./images/kinesis34.png)

Haga clic en **PRUEBA**.

![ETL](./images/kinesis35.png)

Desplácese hacia abajo y pegue este código en **Solicitar cuerpo**. Haga clic en **Prueba**.

```json
{
  "Data": {
    "message": "Hello World",
    "dynamicPartitioningKey": "v2"
  },
  "PartitionKey": "1",
  "StreamName": "--aepUserLdap---datastream"
}
```

![ETL](./images/kinesis36.png)

A continuación, verá un resultado similar:

![ETL](./images/kinesis37.png)

Entonces verá esto... Haga clic en **Acciones** y, a continuación, haga clic en **Implementar API**.

![ETL](./images/kinesis38.png)

Para **Fase de implementación**, seleccione **Nueva fase**. Como **nombre de escenario**, escriba **prod**. Haga clic en **Implementar**.

![ETL](./images/kinesis39.png)

Entonces verá esto... Haga clic en **Guardar cambios**. Información: la dirección URL de la imagen es la dirección URL que se utiliza para enviar datos a (en este ejemplo: https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod).

![ETL](./images/kinesis40.png)

Puede probar la configuración utilizando la siguiente solicitud cURL, solo tiene que reemplazar la siguiente URL por la suya, `https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod` en este ejemplo y agregar `/stream` al final de la dirección URL.

```json
curl --location --request POST 'https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod/stream' \
--header 'Content-Type: application/json' \
--data-raw '{
    "Data": {
        "userid": "--aepUserLdap--@adobe.com",
        "firstName":"--aepUserLdap--",
        "offerName":"10% off on outdoor gears",
        "offerCode": "10OFF-SPRING",
        "dynamicPartitioningKey": "campaign"
    },
    "PartitionKey": "1",
    "StreamName": "--aepUserLdap---datastream"
}'
```

Pegue el código actualizado anterior en una ventana de terminal y pulse Intro. A continuación, verá esta respuesta, similar a la respuesta que pudo ver al realizar pruebas anteriormente.

![ETL](./images/kinesis41.png)

## 2.5.5.6 Actualizar la propiedad de reenvío de eventos

Ahora puede activarlo en el flujo de datos de Kinesis de AWS a través de la puerta de enlace de la API de AWS, de modo que ahora puede enviar los eventos de experiencia sin procesar al ecosistema de AWS. Con Conexiones Real-Time CDP y Reenvío de eventos, ahora puede habilitar fácilmente el reenvío de eventos a su punto final de puerta de enlace de API de AWS recién creado.

### 2.5.5.6.1 Actualizar la propiedad de reenvío de eventos: Crear un elemento de datos

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) y luego a **Reenvío de eventos**. Busque la propiedad Reenvío de eventos y haga clic en ella para abrirla.

![Recopilación de datos Adobe Experience Platform SSF](./images/prop1.png)

En el menú de la izquierda, vaya a **Elementos de datos**. Haga clic en **Agregar elemento de datos**.

![Recopilación de datos Adobe Experience Platform SSF](./images/deaws1.png)

A continuación, verá un nuevo elemento de datos para configurar.

![Recopilación de datos Adobe Experience Platform SSF](./images/de2.png)

Realice la siguiente selección:

- Como **Nombre**, escriba **awsDataObject**.
- Como la **extensión**, seleccione **Principal**.
- Como **Tipo de elemento de datos**, seleccione **Código personalizado**.

Ahora vas a tener esto. Haga clic en **&lt;/> Abrir editor**.

![Recopilación de datos Adobe Experience Platform SSF](./images/deaws3.png)

En el Editor, pegue el siguiente código en la línea 3. Haga clic en **Guardar**.

```javascript
const newObj = {...arc.event.xdm, dynamicPartitioningKey: "event_forwarding"}
return JSON.stringify(newObj);
```

![Recopilación de datos Adobe Experience Platform SSF](./images/deaws4.png)

>[!NOTE]
>
>En la ruta anterior, se hace referencia a **arc**. **arc** significa Contexto de recursos de Adobe y **arc** siempre representa el objeto más alto disponible en el contexto del lado del servidor. Se pueden agregar enriquecimientos y transformaciones a ese objeto **arc** mediante las funciones del servidor de recopilación de datos de Adobe Experience Platform.
>
>En la ruta anterior, se hace referencia a **event**. **event** significa un evento único y el servidor de recopilación de datos de Adobe Experience Platform siempre evaluará cada evento de forma individual. A veces, es posible que vea una referencia a **events** en la carga útil enviada por el lado del cliente del SDK web, pero en el reenvío de eventos de recopilación de datos de Adobe Experience Platform, cada evento se evalúa individualmente.

Entonces volverás a estar aquí. Haga clic en **Guardar** o en **Guardar en biblioteca**.

![Recopilación de datos Adobe Experience Platform SSF](./images/deaws5.png)

### 2.5.5.6.2 Actualizar la propiedad de Adobe Experience Platform Data Collection Server: Actualizar la regla

En el menú de la izquierda, ve a **Reglas**. Haga clic para abrir la regla **Todas las páginas** que creó en uno de los ejercicios anteriores.

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws1.png)

Entonces verá esto... Haga clic en el icono **+** para agregar una acción nueva.

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws2.png)

Entonces verá esto... Realice la siguiente selección:

- Seleccione la **extensión**: **Conector de nube de Adobe**.
- Seleccione el **Tipo de acción**: **Realizar llamada de recuperación**.

Esto debería proporcionarle este **Nombre**: **Conector de nube de Adobe - Realizar llamada de búsqueda**. Ahora debería ver esto:

![Recopilación de datos Adobe Experience Platform SSF](./images/rl4.png)

A continuación, configure lo siguiente:

- Cambiar el método de solicitud de GET a **POST**
- Escriba la dirección URL del extremo de puerta de enlace de API de AWS que creó en uno de los pasos anteriores, con el siguiente aspecto: `https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod/stream`

Ahora debería tener esto. A continuación, vaya a **Encabezados**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws5.png)

Bajo los encabezados, agregue un nuevo encabezado con la clave **Content-Type** y el valor **application/json**. A continuación, vaya a **Cuerpo**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws5a.png)

Entonces verá esto... Pegue el siguiente código en el campo **Cuerpo (sin procesar)**. Haga clic en **Conservar cambios**.

```json
{
    "Data":{{awsDataObject}},
    "PartitionKey": "1",
    "StreamName": "--aepUserLdap---datastream"
}
```

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws7.png)

Entonces verás que estás de vuelta aquí. Haga clic en **Guardar** o en **Guardar en biblioteca**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws10.png)

Ahora ha configurado la primera regla en una propiedad de reenvío de eventos. Vaya a **Flujo de publicación** para publicar los cambios.
Abra la biblioteca de desarrollo haciendo clic en **Principal**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws11.png)

Haga clic en el botón **Agregar todos los recursos modificados**, tras lo cual verá que los cambios de reglas y elementos de datos aparecen en esta biblioteca. A continuación, haga clic en **Guardar y generar para desarrollo**. Los cambios se están implementando.

![Recopilación de datos Adobe Experience Platform SSF](./images/rlaws13.png)

Después de un par de minutos, verá que la implementación está completa y lista para probarse.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl14.png)

## 2.5.5.7 Prueba de la configuración

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Ahora puede seguir el siguiente flujo para acceder al sitio web. Haga clic en **Integraciones**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

En la página **Integraciones**, debe seleccionar la propiedad de recopilación de datos que se creó en el ejercicio 0.1.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada demostración, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

Cuando abra la Vista de desarrollador del explorador, puede inspeccionar las Solicitudes de red como se indica a continuación. Cuando use el filtro **interaction**, verá las solicitudes de red que envía el cliente de recopilación de datos de Adobe Experience Platform a Adobe Edge.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook1.png)

Si selecciona la carga útil sin procesar, vaya a [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) y pegue la carga útil. Haga clic en **Hacer bonito**. Verá la carga útil JSON, el objeto **events** y el objeto **xdm**. En uno de los pasos anteriores, al definir el elemento de datos, utilizó la referencia **arc.event.xdm**, que le permitirá analizar el objeto **xdm** de esta carga.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook2.png)

Cambia tu vista a **AWS**. Al abrir el flujo de datos y entrar en la ficha **Supervisión**, ahora verá tráfico entrante.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hookaws3.png)

Cuando abra el flujo de entrega y vaya a la pestaña **Supervisión**, también verá tráfico entrante.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hookaws4.png)

Por último, cuando eche un vistazo al compartimento de S3, verá que se están creando archivos como consecuencia de la ingesta de datos.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hookaws5.png)

Al descargar un archivo de este tipo y abrirlo con un editor de texto, verá que contiene la carga útil XDM de los eventos reenviados.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hookaws6.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 2.5](./aep-data-collection-ssf.md)

[Volver a todos los módulos](./../../../overview.md)
