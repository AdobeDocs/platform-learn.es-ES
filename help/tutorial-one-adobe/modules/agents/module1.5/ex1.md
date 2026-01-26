---
title: CJA & ChatGPT con servidor MCP
description: CJA & ChatGPT con servidor MCP
kt: 5342
doc-type: tutorial
source-git-commit: ca2812e14a22b80b7f00066f9cc482e708b4ac6a
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 1.5.1 CJA y ChatGPT con servidor MCP

>[!IMPORTANT]
>
>Este laboratorio usa una función que aún no se ha lanzado. La función aún se está desarrollando, por lo que no está disponible en general todavía.


>[!NOTE]
>
>Este ejercicio sobre la configuración y el uso de un servidor MCP con ChatGPT para conectarse a CJA está relacionado con este ejercicio [1.1 Customer Journey Analytics: crear un tablero con Analysis Workspace sobre Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). La vista de datos y la conexión de CJA que se utilizan en el siguiente ejercicio son la vista de datos y la conexión que se configuraron en ese ejercicio. Si desea replicar los siguientes resultados, primero debe seguir esas instrucciones.

## Vídeo

En este vídeo, obtendrá una explicación y una demostración de todos los pasos involucrados en este ejercicio.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 Crear aplicación personalizada en ChatGPT para CJA

>[!NOTE]
>
>El uso de CJA en ChatGPT requiere lo siguiente:
>- una versión de pago de ChatGPT de OpenAI
>- uso del cliente web ChatGPT

Vaya a [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} e inicie sesión con los detalles de su cuenta. Una vez que haya iniciado sesión, debería ver esto. Haga clic en su nombre de usuario.

![ChatGPT](./images/chatgpt1.png)

Seleccione **Configuración**.

![ChatGPT](./images/chatgpt2.png)

Vaya a **Aplicaciones** y seleccione **Configuración avanzada**.

![ChatGPT](./images/chatgpt3.png)

Active **Modo de desarrollador** y luego haga clic en **Atrás**.

![ChatGPT](./images/chatgpt4.png)

Haga clic en **Crear aplicación**.

![ChatGPT](./images/chatgpt5.png)

Rellene los campos de esta manera:

- **Nombre**: `CJA`
- **URL del servidor MCP**: consulte con su representante de Adobe
- **Autenticación**: `OAuth`

Marque la casilla de verificación de **Entiendo y deseo continuar**.

Haga clic en **Crear**.

![ChatGPT](./images/chatgpt6.png)

Una vez que haya iniciado sesión correctamente, debería ver que la aplicación de CJA ahora está conectada correctamente.

![ChatGPT](./images/chatgpt8.png)

## 1.5.1.2: establecer contexto en CJA

Cierre esta ventana.

![ChatGPT y CJA](./images/chatgpt9.png)

Entonces debería ver esto. Haz clic en el icono **+**, ve a **Más** y luego selecciona **CJA**.

![ChatGPT y CJA](./images/chatgpt10.png)

Antes de seguir interactuando con CJA a través de ChatGPT, se debe establecer el contexto.

Para este ejercicio, el contexto debe configurarse para utilizar:

- **Vista de datos**: **—aepUserLdap— - Vista de datos omnicanal**

La configuración de Vista de datos ayuda a identificar qué vista de datos debe ver ChatGPT al hacer preguntas.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
list dataviews
```

![ChatGPT y CJA](./images/chatgpt11.png)

Debería ver una lista similar de vistas de datos disponibles.

![ChatGPT y CJA](./images/chatgpt11a.png)

Para cambiar eso a la vista de datos que necesita usarse, ingrese el siguiente **indicador** y haga clic en el botón **enviar**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT y CJA](./images/chatgpt12.png)

Entonces debería ver esto.

![ChatGPT y CJA](./images/chatgpt16.png)

El contexto ahora está configurado correctamente, por lo que puede empezar a enviar mensajes específicos a continuación.

## 1.5.1.3 Explorar la vista de datos

>[!NOTE]
>
>La vista de datos que se está usando aquí se configuró como parte del ejercicio [Crear una vista de datos](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Escriba el siguiente **Mensaje** y haga clic en el botón **enviar** para explorar qué métricas y dimensiones están disponibles para usted.

```javascript
list the available metrics and dimensions
```

![ChatGPT y CJA](./images/chatgpt101.png)

Debería ver esta respuesta, que incluye las métricas y dimensiones configuradas como parte del ejercicio [Crear una vista de datos](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![ChatGPT y CJA](./images/chatgpt102.png)

## 1.5.1.4 tabla de forma libre: vistas del producto

Ahora puede empezar a explorar los datos. Comience por escribir la siguiente solicitud y haga clic en **enviar** para enviar su solicitud de informe.

```javascript
how many product views happened on January 21?
```

![ChatGPT y CJA](./images/chatgpt103.png)

Seleccione **RunReport**.

![ChatGPT y CJA](./images/chatgpt104.png)

Entonces debería ver una respuesta como esta.

![ChatGPT y CJA](./images/chatgpt105.png)

Ahora puede desglosar la respuesta añadiendo una dimensión. Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
break down product views by product name
```

![ChatGPT y CJA](./images/chatgpt106.png)

Entonces debería ver una respuesta como esta.

![ChatGPT y CJA](./images/chatgpt107.png)

Ahora también puede crear una visualización. Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT y CJA](./images/chatgpt108.png)

Seleccione **UpsertProject**.

![ChatGPT y CJA](./images/chatgpt109.png)

Seleccione **RunReport**.

![ChatGPT y CJA](./images/chatgpt110.png)

Entonces debería ver esto.

![ChatGPT y CJA](./images/chatgpt111.png)

Desplácese hacia abajo.

![ChatGPT y CJA](./images/chatgpt112.png)

Ahora también puede descargar este gráfico de líneas. Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
export this chart to PNG
```

![ChatGPT y CJA](./images/chatgpt113.png)

Entonces debería ver esto. Haga clic en **Descargar el archivo PNG**.

![ChatGPT y CJA](./images/chatgpt114.png)

Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
can you breakdown product views by user agent?
```

![ChatGPT y CJA](./images/chatgpt115.png)

Seleccione **RunReport**.

![ChatGPT y CJA](./images/chatgpt116.png)

Entonces debería ver esto.

![ChatGPT y CJA](./images/chatgpt117.png)

## Visualización de abandonos de 1.5.1.5

Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT y CJA](./images/chatgpt118.png)

Seleccione **UpsertProject**.

![ChatGPT y CJA](./images/chatgpt119.png)

Seleccione **RunReport**.

![ChatGPT y CJA](./images/chatgpt120.png)

Entonces deberías ver algo como esto. Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT y CJA](./images/chatgpt120a.png)

Haga clic en **Descargar el archivo PNG**.

![ChatGPT y CJA](./images/chatgpt121.png)

Ahora verá la visualización del análisis de abandonos.

![ChatGPT y CJA](./images/chatgpt122.png)

Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
break down the fallout analysis at the touchpoint of the add to carts
```

![ChatGPT y CJA](./images/chatgpt123.png)

Seleccione **RunReport**.

![ChatGPT y CJA](./images/chatgpt124.png)

Volver a [Analytics y agentes](./analyticsagents.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}