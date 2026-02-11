---
title: Utilice el cursor para desarrollar el proyecto
description: Utilice el cursor para desarrollar el proyecto
kt: 5342
doc-type: tutorial
exl-id: c73498b6-5e08-41b5-81a9-c0a76a6e2792
source-git-commit: 25901342e8d9c46b0edce3b2092b9f1d66ba5849
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# 1.7.2 Use el cursor para desarrollar su proyecto

## 1.7.2.1 Configurar el directorio y las herramientas

En el escritorio, cree un nuevo directorio con el nombre `--aepUserLdap---commerce`

![Commerce y Agentic](./images/cursorai1.png)

Haga clic con el botón derecho en la carpeta y seleccione **Nuevo terminal en la carpeta**.

![Commerce y Agentic](./images/cursorai2.png)

Entonces debería ver esto.

![Commerce y Agentic](./images/cursorai3.png)

Ahora necesita clonar un repositorio de Github existente, que puede ver [https://github.com/adobe/commerce-integration-starter-kit](https://github.com/adobe/commerce-integration-starter-kit).

Este repositorio es el Starter Kit de Adobe que utiliza Adobe Developer App Builder para mejorar la fiabilidad de las conexiones en tiempo real y reducir el tiempo de salida al mercado de las integraciones entre Adobe Commerce y otros sistemas de back-office, como ERP, CRM y PIM.

![Commerce y Agentic](./images/cursorai4.png)

Existen varias formas de clonar este repositorio; en este ejemplo se utiliza Terminal.

Introduzca el siguiente comando en la ventana de terminal y ejecútelo.

`git clone https://github.com/adobe/commerce-integration-starter-kit`

![Commerce y Agentic](./images/cursorai5.png)

Después de un par de segundos, debería ver este resultado.

![Commerce y Agentic](./images/cursorai6.png)

A continuación, debe navegar a la carpeta que acaba de crear. Introduzca el siguiente comando y, a continuación, ejecútelo.

`cd commerce-integration-starter-kit`

![Commerce y Agentic](./images/cursorai7.png)

Entonces debería ver esto.

![Commerce y Agentic](./images/cursorai8.png)

A continuación, debe configurar las herramientas de extensibilidad de Commerce para Cursor. Introduzca el siguiente comando y, a continuación, ejecútelo.

`aio commerce extensibility tools-setup`

![Commerce y Agentic](./images/cursorai9.png)

Seleccione **directorio actual**.

![Commerce y Agentic](./images/cursorai10.png)

Seleccionar **Cursor**.

![Commerce y Agentic](./images/cursorai11.png)

Seleccione **npm**.

![Commerce y Agentic](./images/cursorai12.png)

Después de un par de minutos, deberías ver esto.

![Commerce y Agentic](./images/cursorai13.png)

Al instalar las herramientas de extensibilidad de Commerce para Cursor, ahora hay un servidor MCP disponible como parte del entorno Cursor. En los próximos ejercicios, utilizará ese servidor MCP para ayudarle a desarrollar e implementar el proyecto del creador de aplicaciones.

## 1.7.2.2 Configurar su webhook

Para este ejercicio, necesitará un webhook que necesite configurarse para que cuando se cree un pedido, el evento de pedido se pueda transmitir a ese webhook. En este ejercicio, usará un extremo de ejemplo con [https://pipedream.com/requestbin](https://pipedream.com/requestbin).

Vaya a [https://pipedream.com/requestbin](https://pipedream.com/requestbin), cree una cuenta y luego un área de trabajo. Una vez creado el espacio de trabajo, verá algo similar a esto.

Haga clic en **copiar** para copiar la dirección URL. Deberá especificar esta dirección URL en el siguiente ejercicio. La dirección URL de este ejemplo es `https://eodts05snjmjz67.m.pipedream.net`.

![Cursor + Commerce](./images/webhook1.png)

## 1.7.2.3 Crear aplicación con cursor

Abra el cursor. Haga clic en **Abrir proyecto**.

![Cursor + Commerce](./images/cursorai14.png)

Vaya a la carpeta que creó, que debería llamarse `--aepUserLdap---commerce`. En esa carpeta, seleccione la carpeta que se llama `commerce-integration-starter-kit`. Haga clic en **Abrir**.

![Cursor + Commerce](./images/cursorai15.png)

Entonces debería ver esto. Antes de continuar, asegúrese de que la carpeta de nivel superior que se abre en el cursor es `commerce-integration-starter-kit`.

![Cursor + Commerce](./images/cursorai16.png)

Utilice el método abreviado de teclado `Cmd + Shift + J` para abrir la configuración del cursor. Entonces debería ver esto. Vaya a **Herramientas y MCP**.

![Cursor + Commerce](./images/cursorai17.png)

Habilite el servidor MCP **commerce-extensibility**. Una vez hecho esto, haga clic en **X** para cerrar la ventana.

![Cursor + Commerce](./images/cursorai18.png)

Copie la siguiente solicitud y péguela en el cursor. A continuación, haga clic en el botón **enviar**.

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

![Cursor + Commerce](./images/cursorai19.png)

El cursor empezará a razonar y a ejecutarse. El cursor le pedirá confirmación un par de veces. Cuando esto suceda, haga clic en **Ejecutar**. Esto puede suceder de 5 a 10 veces, según el razonamiento y la configuración.

![Cursor + Commerce](./images/cursorai20.png)

Después de un par de minutos, deberías ver algo así.

![Cursor + Commerce](./images/cursorai21.png)

El siguiente paso, tal como lo indica Cursor, es crear un archivo con el nombre `.env` y proporcionar las variables necesarias.

## 1.7.2.4: cree su archivo .env

Seleccione el archivo **env.dist**. Escriba el comando `Cmd + C` y después el comando `Cmd + V`.

![Cursor + Commerce](./images/cursorai22.png)

Cambie el nombre del archivo recién creado a `.env`.

![Cursor + Commerce](./images/cursorai23.png)

A continuación, debe proporcionar los valores para todas las variables del archivo **.env**.

![Cursor + Commerce](./images/cursorai24.png)

Aquí es donde puede encontrar toda la información necesaria.

### Extremos de Commerce

Puede encontrar estas variables en [https://experience.adobe.com](https://experience.adobe.com). Haga clic en **Commerce**.

![Cursor + Commerce](./images/cursorai25.png)

Entonces debería ver esto. Haga clic en el icono **información** junto a su entorno ACCS, que debe llamarse `--aepUserLdap-- - ACCS`. Copie los valores del extremo REST y del extremo GraphQL.

En este ejemplo, estos son los valores que se van a copiar. Péguelas junto a las siguientes variables en el archivo **.env**, en las líneas 6 y 7.


- **COMMERCE_BASE_URL** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/
- **COMMERCE_GRAPHQL_ENDPOINT** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/graphql

![Cursor + Commerce](./images/cursorai26.png)

Entonces debería tener esto en el archivo **.env**.

![Cursor + Commerce](./images/cursorai26a.png)

### Variables de proyecto de Adobe I/O

Puede encontrar estas variables en [https://developer.adobe.com/console](https://developer.adobe.com/console). Vaya a **Proyectos** y haga clic para abrir el proyecto de Adobe I/O que creó en el ejercicio anterior, que debería llamarse `--aepUserLdap-- Commerce Events`.

![Cursor + Commerce](./images/cursorai27.png)

Ir a **Producción**.

![Cursor + Commerce](./images/cursorai28.png)

Vaya a **OAuth Server-to-Server**. Entonces debería ver esto.

![Cursor + Commerce](./images/cursorai29.png)

Copie los valores de los campos **ID de cliente**, **Secreto de cliente**, **ID de cuenta técnica**, **Correo electrónico de cuenta técnica** y **ID de organización** y péguelos junto a las siguientes variables en el archivo **.env** en las líneas 13-17.

- **OAUTH_CLIENT_ID**= **ID de cliente**
- **OAUTH_CLIENT_SECRET**= **Secreto de cliente**
- **OAUTH_TECHNICAL_ACCOUNT_ID**= **ID de cuenta técnica**
- **OAUTH_TECHNICAL_ACCOUNT_EMAIL**= **Correo electrónico de cuenta técnica**
- **OAUTH_ORG_ID**= **ID de organización**

Entonces debería tener esto en el archivo **.env**.

![Cursor + Commerce](./images/cursorai29a.png)

### COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID

Para el campo **COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID=**, escriba el valor `--aepUserLdap--_commerce_events` en la línea 34 del archivo **.env**.

Entonces debería tener esto en el archivo **.env**.

![Cursor + Commerce](./images/cursorai30.png)

### Configuraciones de Workspace

Para recuperar estas variables, vuelva al proyecto de Adobe I/O y haga clic en **Información general de Workspace**.

Después de ir a la **descripción general de Workspace**, eche un vistazo a la dirección URL, que debería tener este aspecto: **https://developer.adobe.com/console/projects/133309/4566206088345586770/workspaces/4566206088345619105/details**.

El primer número de este ejemplo, 133309, es el valor que se va a usar para el campo **IO_CONSUMER_ID**.
El segundo número de este ejemplo, 4566206088345586770, es el valor que se va a utilizar para el campo **IO_PROJECT_ID**.
El tercer número de este ejemplo, 4566206088345619105, es el valor que se debe usar para el campo **IO_WORKSPACE_ID**.

![Cursor + Commerce](./images/cursorai31.png)

- **IO_CONSUMER_ID**= 133309
- **IO_PROJECT_ID**= 4566206088345586770
- **IO_WORKSPACE_ID**= 4566206088345619105

Copie estos valores y péguelos junto a las siguientes variables en el archivo **.env**, en las líneas 42-44.

![Cursor + Commerce](./images/cursorai32.png)

### EVENT_PREFIX

Para el campo **EVENT_PREFIX =**, escriba el valor `--aepUserLdap--_` en la línea 47 del archivo **.env**.

Entonces debería tener esto en el archivo **.env**.

![Cursor + Commerce](./images/cursorai33.png)

### Webhook

Para el campo **ORDER_WEBHOOK_URL**, debe pegar la dirección URL del webhook que creó anteriormente en este ejercicio, que debería tener este aspecto: `https://eodts05snjmjz67.m.pipedream.net`.

Entonces debería tener esto en el archivo **.env**.

![Cursor + Commerce](./images/cursorai34.png)

### Credenciales de App Builder

Debe actualizar las siguientes variables en el archivo **.env** en las líneas 54-55:

- **AIO_RUNTIME_NAMESPACE**=
- **AIO_RUNTIME_AUTH**=

Puede recuperar los valores de estas variables volviendo al proyecto de Adobe I/O. Vaya a **Información general de Workspace** y haga clic en **Descargar todo**.

![Cursor + Commerce](./images/cursorai35.png)

A continuación, se descargará un archivo como este. Abra ese archivo con un editor de texto.

![Cursor + Commerce](./images/cursorai36.png)

Desplácese hacia la derecha hasta que vea **runtime**. Debería ver el campo **name**, que contiene el valor de **AIO_RUNTIME_NAMESPACE**.

![Cursor + Commerce](./images/cursorai37.png)

Desplácese más hacia la derecha hasta que vea **auth**, que contiene el valor de **AIO_RUNTIME_AUTH**.

![Cursor + Commerce](./images/cursorai38.png)

Pegue ambos valores en el archivo **.env** en las líneas 54-55, debería tener esto.

![Cursor + Commerce](./images/cursorai39.png)

El archivo **.env** está ahora completamente configurado.

## 1.7.2.5 workspace.json

En el paso anterior descargó un archivo como este desde el proyecto de Adobe I/O.

![Cursor + Commerce](./images/cursorai36.png)

Cambie el nombre de ese archivo y use el nombre `workspace.json`.

![Cursor + Commerce](./images/cursorai40.png)

Copie el archivo en el directorio **scripts**>**incorporación**>**config**.

![Cursor + Commerce](./images/cursorai41.png)

## 1.7.2.6 inicio de sesión en Adobe I/O

Vuelva a la ventana de terminal que había utilizado anteriormente. Escriba el comando `aio login`.

![Cursor + Commerce](./images/cursorai44.png)

Debería ver esto después de iniciar sesión en el explorador.

![Cursor + Commerce](./images/cursorai45.png)

## 1.7.2.7 está listo para implementarse

Copie la siguiente solicitud y péguela en el cursor. A continuación, haga clic en el botón **enviar**.

`Please deploy this code to Adobe I/O`

![Cursor + Commerce](./images/cursorai42.png)

Haga clic en **Ejecutar** para permitir la acción. El cursor puede pedirle varias veces que confirme una acción.

![Cursor + Commerce](./images/cursorai43.png)

La implementación finalizará después de un par de minutos.

![Cursor + Commerce](./images/cursorai46.png)

Copie la siguiente solicitud y péguela en el cursor. A continuación, haga clic en el botón **enviar**.

`run the onboarding to commerce`

![Cursor + Commerce](./images/cursorai50.png)

Después de un par de minutos, deberías ver esto.

![Cursor + Commerce](./images/cursorai51.png)

Copie la siguiente solicitud y péguela en el cursor. A continuación, haga clic en el botón **enviar**.

`subscribe to commerce events`

![Cursor + Commerce](./images/cursorai47.png)

Después de un par de minutos, deberías ver esto.

![Cursor + Commerce](./images/cursorai49.png)

## 1.7.2.8 Verificar configuración en Adobe Commerce as a Cloud Service

Vaya a [https://experience.adobe.com](https://experience.adobe.com). Haga clic en **Commerce**.

![Cursor + Commerce](./images/cursorai60.png)

Haga clic en el entorno de as a Cloud Service de Adobe Commerce para abrirlo y, a continuación, iniciar sesión.

![Cursor + Commerce](./images/cursorai61.png)

Vaya a **Sistema** y luego a **Suscripciones de eventos**.

![Cursor + Commerce](./images/cursorai62.png)

Debería ver esta lista de suscripciones a eventos.

![Cursor + Commerce](./images/cursorai63.png)

Vaya a **Tiendas** y luego a **Configuración**.

![Cursor + Commerce](./images/cursorai64.png)

Vaya a **Servicios de Adobe** y seleccione **Adobe I/O Events**. Debería ver que el campo **Configuración de Adobe I/O Workspace** tiene un valor de un par de asteriscos y que el campo **ID de comerciante** también debe tener un valor como `--aepUserLdap--_commerce_events`.

![Cursor + Commerce](./images/cursorai65.png)

Con esta configuración configurada, ahora puede probar la configuración de.

## 1.7.2.9 Probar el escenario

Abra el sitio web.

![Cursor + Commerce](./images/cursorai101.png)

Vaya a **Relojes** y haga clic en cualquier producto.

![Cursor + Commerce](./images/cursorai102.png)

Configure el producto y haga clic en **Agregar al carro**.

![Cursor + Commerce](./images/cursorai103.png)

Haga clic en el icono **Carro** y seleccione **Finalizar compra**.

![Cursor + Commerce](./images/cursorai104.png)

Complete sus datos y haga clic en **Realizar pedido**.

![Cursor + Commerce](./images/cursorai105.png)

A continuación, debería ver una confirmación de pedido.

![Cursor + Commerce](./images/cursorai106.png)

Cambie a la aplicación de webhook. Ahora debería ver un evento entrante para el pedido que acaba de confirmarse.

![Cursor + Commerce](./images/cursorai107.png)

## 1.7.2.10 depuración de Adobe I/O

Vuelva al proyecto de Adobe I/O. Vaya a **Información general de Workspace**. Debería ver algo similar a esto. Desplácese un poco hacia abajo.

![Cursor + Commerce](./images/cursorai108.png)

Haga clic para abrir **Commerce Order Sync**.

![Cursor + Commerce](./images/cursorai109.png)

Ir a **Seguimiento de depuración**. Puede encontrar los últimos eventos entrantes allí, junto con su carga útil. Esto resulta útil para comprender qué eventos se han procesado y si se han procesado correctamente.

![Cursor + Commerce](./images/cursorai110.png)

## Pasos siguientes

Volver a [Herramientas inteligentes para desarrolladores para Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
