---
title: CJA & Claude.ai con servidor MCP
description: CJA & Claude.ai con servidor MCP
kt: 5342
doc-type: tutorial
source-git-commit: 5eb5432251ee7193909ed4ec7decd0d94d0843a2
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# 1.5.2 CJA y Claude.ai con servidor MCP

[!BADGE Alpha]

+++Detalles de Alpha
Al utilizar CJA &amp; Claude.ai con el servidor MCP Alpha, por la presente reconoce que el Alpha se proporciona &quot;tal cual&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o apoyar de otro modo Alpha. Se recomienda tener precaución y no confiar en modo alguno en el correcto funcionamiento o rendimiento de dichos Alpha y/o materiales de acompañamiento. Alpha se considera información confidencial de Adobe. Cualquier &quot;comentario&quot; (información sobre Alpha, incluidos, entre otros, problemas o defectos que encuentre al utilizar Alpha, sugerencias, mejoras y recomendaciones) proporcionado por usted a Adobe se asigna a Adobe, incluidos todos los derechos, el título y el interés en y para dichos comentarios.

+++


>[!NOTE]
>
>Este ejercicio sobre la configuración y el uso de un servidor MCP con Claude.ai para conectarse a CJA está relacionado con este ejercicio [1.1 Customer Journey Analytics: crear un tablero con Analysis Workspace sobre Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). La vista de datos y la conexión de CJA que se utilizan en el siguiente ejercicio son la vista de datos y la conexión que se configuraron en ese ejercicio. Si desea replicar los siguientes resultados, primero debe seguir esas instrucciones.

## Vídeo

En este vídeo, obtendrá una explicación y una demostración de todos los pasos involucrados en este ejercicio.

>[!VIDEO](https://video.tv.adobe.com/v/3479561?quality=12&learn=on)

## 1.5.2.1 Crear aplicación personalizada en Claude.ai para CJA

>[!NOTE]
>
>El uso de CJA en Claude.ai requiere lo siguiente:
>- una versión de pago de Claude.ai
>- uso del cliente web Claude.ai

Vaya a [https://claude.ai/](https://claude.ai/){target="_blank"} e inicie sesión con los detalles de su cuenta. Una vez que haya iniciado sesión, debería ver esto. Haga clic en el icono **+**.

![Claude.ai](./images/claude1.png)

Seleccione **Agregar conectores**.

![Claude.ai](./images/claude2.png)

Haga clic en **agregar uno personalizado**.

![Claude.ai](./images/claude3.png)

Rellene los campos de esta manera:

- **Nombre**: `CJA`
- **URL del servidor MCP**: consulte con su representante de Adobe

Haga clic en **Agregar**.

![Claude.ai](./images/claude4.png)

Entonces debería ver esto. Haga clic en **Conectar**.

![Claude.ai](./images/claude5.png)

Una vez que se haya autenticado correctamente, debería ver esto. Haga clic en el icono **+** para iniciar una nueva conversación.

![Claude.ai](./images/claude6.png)

Vaya a **+**, a **Conectores** y debería ver que el conector **CJA** ya está habilitado.

![Claude.ai](./images/claude8.png)

Ya está listo para iniciar el análisis de datos.

![Claude.ai](./images/claude7.png)

## 1.5.2.2: establecer contexto en CJA

Antes de seguir interactuando con CJA a través de Claude.ai, es necesario establecer el contexto.

Para este ejercicio, el contexto debe configurarse para utilizar:

- **Vista de datos**: **—aepUserLdap— - Vista de datos omnicanal**

La configuración de vista de datos ayuda a identificar qué vista de datos debe ver Claude.ai al hacer preguntas.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
list dataviews
```

![Claude.ai y CJA](./images/claude9.png)

Seleccionar **Permitir siempre**.

![Claude.ai y CJA](./images/claude10.png)

Debería ver una lista similar de vistas de datos disponibles.

![Claude.ai y CJA](./images/claude11.png)

Para cambiar eso a la vista de datos que necesita usarse, ingrese el siguiente **indicador** y haga clic en el botón **enviar**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![Claude.ai y CJA](./images/claude11a.png)

Seleccionar **Permitir siempre**.

![Claude.ai y CJA](./images/claude12.png)

Entonces debería ver esto.

![Claude.ai y CJA](./images/claude16.png)

El contexto ahora está configurado correctamente, por lo que puede empezar a enviar mensajes específicos a continuación.

## 1.5.2.3 Explorar la vista de datos

>[!NOTE]
>
>La vista de datos que se está usando aquí se configuró como parte del ejercicio [Crear una vista de datos](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Escriba el siguiente **Mensaje** y haga clic en el botón **enviar** para explorar qué métricas y dimensiones están disponibles para usted.

```javascript
list the available metrics and dimensions
```

![Claude.ai y CJA](./images/claude101.png)

Seleccione **Permitir siempre** dos veces, una para recuperar **métricas** y otra para recuperar **dimensiones**.

![Claude.ai y CJA](./images/claude101a.png)

Debería ver esta respuesta, que incluye las métricas y dimensiones configuradas como parte del ejercicio [Crear una vista de datos](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![Claude.ai y CJA](./images/claude102.png)

## 1.5.2.4 tabla de forma libre: vistas del producto

Ahora puede empezar a explorar los datos. Comience por escribir la siguiente solicitud y haga clic en **enviar** para enviar su solicitud de informe.

```javascript
how many product views happened on January 21, 2026?
```

![Claude.ai y CJA](./images/claude103.png)

Seleccionar **Permitir siempre**.

![Claude.ai y CJA](./images/claude104.png)

Entonces debería ver una respuesta como esta.

![Claude.ai y CJA](./images/claude105.png)

Ahora puede desglosar la respuesta añadiendo una dimensión. Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
break down product views by product name
```

![Claude.ai y CJA](./images/claude106.png)

Entonces debería ver una respuesta como esta.

![Claude.ai y CJA](./images/claude107.png)

Ahora también puede crear una visualización. Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
create a line visualization by hour for product views on January 21
```

![Claude.ai y CJA](./images/claude108.png)

Entonces debería ver esto.

![Claude.ai y CJA](./images/claude109.png)

Ahora también puede descargar este gráfico de líneas. Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
export this chart to PNG
```

![Claude.ai y CJA](./images/claude113.png)

Entonces debería ver esto. Haga clic en **Descargar**.

![Claude.ai y CJA](./images/claude114.png)

A continuación, puede abrir el PNG descargado y utilizarlo en otros documentos.

![Claude.ai y CJA](./images/claude114a.png)

Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
can you breakdown product views by user agent?
```

![Claude.ai y CJA](./images/claude115.png)

Entonces debería ver esto.

![Claude.ai y CJA](./images/claude117.png)

## Visualización de abandonos de 1.5.2.5

Escriba el **prompt** siguiente y haga clic en el botón **enviar**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![Claude.ai y CJA](./images/claude118.png)

Debería ver algo similar a esto, que incluye una visualización generada por Claude.ai basada en los datos proporcionados por Customer Journey Analytics.

![Claude.ai y CJA](./images/claude119.png)

Siguiente paso: [Adobe Analytics y Claude.ai con servidor MCP](./ex3.md){target="_blank"}

Volver a [Analytics y agentes](./analyticsagents.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}