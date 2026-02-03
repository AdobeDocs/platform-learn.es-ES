---
title: Adobe Analytics & Claude.ai con servidor MCP
description: Adobe Analytics & Claude.ai con servidor MCP
kt: 5342
doc-type: tutorial
source-git-commit: 44559d6278da4bed8a864d0faf092352b8370398
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 1.5.3 Adobe Analytics y Claude.ai con servidor MCP

[!BADGE Alpha]

+++Detalles de Alpha
Al utilizar CJA &amp; Claude.ai con el servidor MCP Alpha, por la presente reconoce que el Alpha se proporciona &quot;tal cual&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o apoyar de otro modo Alpha. Se recomienda tener precaución y no confiar en modo alguno en el correcto funcionamiento o rendimiento de dichos Alpha y/o materiales de acompañamiento. Alpha se considera información confidencial de Adobe. Cualquier &quot;comentario&quot; (información sobre Alpha, incluidos, entre otros, problemas o defectos que encuentre al utilizar Alpha, sugerencias, mejoras y recomendaciones) proporcionado por usted a Adobe se asigna a Adobe, incluidos todos los derechos, el título y el interés en y para dichos comentarios.

+++

## Vídeo

En este vídeo, obtendrá una explicación y una demostración de todos los pasos involucrados en este ejercicio.

>[!VIDEO](https://video.tv.adobe.com/v/3479562?quality=12&learn=on)

## 1.5.3.1 Crear aplicación personalizada en Claude.ai para Adobe Analytics

>[!NOTE]
>
>El uso de Adobe Analytics en Claude.ai requiere lo siguiente:
>- una versión de pago de Claude.ai
>- uso del cliente web Claude.ai

Vaya a [https://claude.ai/](https://claude.ai/){target="_blank"} e inicie sesión con los detalles de su cuenta. Una vez que haya iniciado sesión, debería ver esto. Haga clic en el icono **+**.

![Claude.ai](./images/claudeaa1.png)

Seleccione **Agregar conectores**.

![Claude.ai](./images/claudeaa2.png)

Haga clic en **agregar uno personalizado**.

![Claude.ai](./images/claudeaa3.png)

Rellene los campos de esta manera:

- **Nombre**: `CJA`
- **URL del servidor MCP**: consulte con su representante de Adobe

Haga clic en **Agregar**.

![Claude.ai](./images/claudeaa4.png)

Entonces debería ver esto. Haga clic en **Conectar**.

![Claude.ai](./images/claudeaa5.png)

Una vez que se haya autenticado correctamente, debería ver esto. Haga clic en el icono **+** para iniciar una nueva conversación.

![Claude.ai](./images/claudeaa6.png)

Vaya a **+**, a **Conectores** y debería ver que el conector **Adobe Analytics** ya está habilitado.

![Claude.ai](./images/claudeaa7.png)

Ya está listo para iniciar el análisis de datos.

![Claude.ai](./images/claudeaa8.png)

## 1.5.3.2: establecer contexto en Adobe Analytics

Antes de seguir interactuando con CJA a través de Claude.ai, es necesario establecer el contexto.

Para este ejercicio, el contexto debe configurarse para utilizar:

- **Grupo de informes**: **CID - Datos de demostración**

La configuración del grupo de informes ayuda a identificar qué datos debe ver Claude.ai al hacer preguntas.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
list report suites
```

![Claude.ai](./images/claudeaa9.png)

Seleccionar **Permitir siempre**.

![Claude.ai](./images/claudeaa10.png)

Seleccionar **Permitir siempre**.

![Claude.ai](./images/claudeaa11.png)

Entonces deberías ver algo como esto.

![Claude.ai](./images/claudeaa12.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
use report suite CID Demo Data
```

![Claude.ai](./images/claudeaa13.png)

Seleccionar **Permitir siempre**.

![Claude.ai](./images/claudeaa14.png)

Se ha seleccionado el grupo de informes.

![Claude.ai](./images/claudeaa15.png)

## 1.5.2.3 Explorar el grupo de informes

Escriba el siguiente **Mensaje** y haga clic en el botón **enviar** para explorar qué métricas y dimensiones están disponibles para usted.

```javascript
list the available metrics and dimensions
```

![Claude.ai y CJA](./images/claudeaa101.png)

Seleccionar **Permitir siempre**.

![Claude.ai y CJA](./images/claudeaa102.png)

Seleccione **Permitir siempre** de nuevo.

![Claude.ai y CJA](./images/claudeaa103.png)

Debería ver esta respuesta, que incluye las métricas y dimensiones configuradas en este grupo de informes.

![Claude.ai y CJA](./images/claudeaa104.png)

## 1.5.2.4 informes

Ahora puede empezar a explorar los datos. Comience por escribir la siguiente solicitud y haga clic en **enviar** para enviar su solicitud de informe.

```javascript
show me pageviews for Feb 2?
```

![Claude.ai y CJA](./images/claudeaa105.png)

Entonces deberías ver algo como esto.

![Claude.ai y CJA](./images/claudeaa106.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
break down pageviews by page name
```

![Claude.ai y CJA](./images/claudeaa107.png)

Entonces debería ver esto.

![Claude.ai y CJA](./images/claudeaa108.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
give me an overview of page names, page views by marketing channel
```

![Claude.ai y CJA](./images/claudeaa109.png)

Entonces deberías ver algo como esto.

![Claude.ai y CJA](./images/claudeaa110.png)

Desplácese un poco hacia abajo para ver el análisis.

![Claude.ai y CJA](./images/claudeaa111.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Analyze different metrics by marketing channel
```

![Claude.ai y CJA](./images/claudeaa112.png)

Entonces deberías ver algo como esto.

![Claude.ai y CJA](./images/claudeaa113.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
which tracking codes drove the most visits and purchases?
```

![Claude.ai y CJA](./images/claudeaa114.png)

Debería ver algo similar a esto: primero se muestran **códigos de seguimiento principales por visitas**.

![Claude.ai y CJA](./images/claudeaa115.png)

Puedes ver los códigos de seguimiento que más compras condujeron en el informe **Códigos de seguimiento principales por pedidos (compras)**.

![Claude.ai y CJA](./images/claudeaa116.png)

Y luego encuentras información adicional proporcionada por Claude.ai en función de los datos procedentes de Adobe Analytics.

![Claude.ai y CJA](./images/claudeaa117.png)

Ya ha terminado este ejercicio.

Volver a [Analytics y agentes](./analyticsagents.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}