---
title: Adobe Marketing Agent para ChatGPT Enterprise
description: Adobe Marketing Agent para ChatGPT Enterprise
kt: 5342
doc-type: tutorial
source-git-commit: 44d0e98ae4c7568411cb0e01ed8eff38b4a34137
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# 1.1.2 Adobe Marketing Agent para ChatGPT Enterprise

>[!IMPORTANT]
>
>Este laboratorio usa una función que aún no se ha lanzado. La función aún se está desarrollando, por lo que no está disponible en general todavía.

[!BADGE En desarrollo]

+++En Detalles de desarrollo
Al utilizar Adobe Marketing Agent para ChatGPT Enterprise Beta, Usted reconoce por la presente que Beta se proporciona &quot;tal cual&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o apoyar de otro modo Beta. Se recomienda tener precaución y no confiar en modo alguno en el correcto funcionamiento o rendimiento de dichos Beta y/o materiales de acompañamiento. Beta se considera información confidencial de Adobe.  Cualquier &quot;comentario&quot; (información sobre Beta, incluidos, entre otros, problemas o defectos que encuentre al utilizar Beta, sugerencias, mejoras y recomendaciones) proporcionado por usted a Adobe se asigna a Adobe, incluidos todos los derechos, el título y el interés en y para dichos comentarios.

+++

## Vídeo

En este vídeo, obtendrá una explicación y una demostración de todos los pasos involucrados en este ejercicio.

>[!VIDEO](https://video.tv.adobe.com/v/3478410?quality=12&learn=on)

## 1.1.2.1 Crear aplicación personalizada en ChatGPT Enterprise para Adobe Marketing Agent

>[!NOTE]
>
>El uso de Adobe Marketing Agent en ChatGPT requiere lo siguiente:
>- una versión de pago de ChatGPT Enterprise de OpenAI
>- uso del cliente web ChatGPT Enterprise

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

- **Nombre**: `Adobe Marketing Agent`
- **URL del servidor MCP**: consulte con su representante de Adobe
- **Autenticación**: `OAuth`

Marque la casilla de verificación de **Entiendo y deseo continuar**.

Haga clic en **Crear**.

![ChatGPT](./images/chatgpt6.png)

ChatGPT intentará conectarse a su cuenta de Adobe. Seleccione **Permitir acceso** y luego tendrá que iniciar sesión con su cuenta de Adobe.

![ChatGPT](./images/chatgpt7.png)

Una vez que haya iniciado sesión correctamente, debería ver que su Adobe Marketing Agent ahora está conectado correctamente.

![ChatGPT](./images/chatgpt8.png)

## 1.1.2.2: establecer contexto en Adobe Marketing Agent

Cierre esta ventana.

![Agent Orchestrator](./images/chatgpt9.png)

Entonces debería ver esto. Haz clic en el icono **+**, ve a **Más** y luego selecciona **Adobe Marketing Agent**.

![Agent Orchestrator](./images/chatgpt10.png)

Antes de seguir interactuando con Adobe Marketing Agent a través de ChatGPT, se debe establecer el contexto.

Para este ejercicio, el contexto debe configurarse para utilizar:

- **Espacio aislado**: **Prod - Accelerate (VA7)**

La configuración de Zona protegida ayuda a identificar qué zona protegida debe ver ChatGPT al hacer preguntas.

- **Vista de datos**: **Acelerar B2C 2026**

La configuración de Vista de datos ayuda a identificar qué vista de datos debe ver ChatGPT al hacer preguntas.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
list sandboxes
```

![Agent Orchestrator](./images/chatgpt11.png)

Debería ver una lista similar de las zonas protegidas disponibles. La zona protegida actual de este ejemplo está configurada en **prod**.

Para cambiar eso a la zona protegida que necesita usarse, ingrese el siguiente **indicador** y haga clic en el botón **enviar**.

```javascript
switch to sandbox accelerate
```

![Agent Orchestrator](./images/chatgpt12.png)

Entonces debería ver esto. Haga clic en **Establecer contexto**.

![Agent Orchestrator](./images/chatgpt13.png)

Entonces debería ver esto. Escriba el **indicador** siguiente y haga clic en el botón **enviar** para establecer la vista de datos que se va a usar.

```javascript
list dataviews
```

![Agent Orchestrator](./images/chatgpt14.png)

Debería ver una lista similar de vistas de datos disponibles.

Para establecer la vista de datos que debe usarse, ingrese el siguiente **indicador** y haga clic en el botón **enviar**.

```javascript
switch to Accelerate 2026 B2C
```

![Agent Orchestrator](./images/chatgpt15.png)

Entonces debería ver esto. Haga clic en **Establecer contexto**.

![Agent Orchestrator](./images/chatgpt16.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/chatgpt17.png)

El contexto ahora está configurado correctamente, por lo que puede empezar a enviar mensajes específicos a continuación.

## 1.1.2.3 Comience con las tendencias generales de compra para anclar el contexto y ampliar el alcance de la fibra

**Intención**

Obtenga un impulso de nivel superior sobre la demanda de categorías (móvil, fijo, Internet, TV, fibra), específicamente durante los últimos 60 días. Esto establece líneas de base para la estacionalidad, los efectos de promoción y la variación regional después del despliegue en Nueva York.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/chatgpt18.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/chatgpt19.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/chatgpt20.png)

Luego debería ver esto, que profundiza en las tendencias específicas de la fibra.

![Agent Orchestrator](./images/chatgpt21.png)

## 1.1.2.4: correlacionar pedidos con preferencias de contenido

**Intención**

Pruebe la hipótesis de que una preferencia por un género específico (por ejemplo, ciencia ficción, deportes, teatro) predice el comportamiento de actualización de banda ancha, especialmente para las necesidades de banda ancha alta.

En primer lugar, debe averiguar qué campo se utiliza para almacenar la preferencia de género.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Which field is used to store the preferred genre in the sandbox accelerate?
```

![Agent Orchestrator](./images/chatgpt22.png)

Debería ver esto, lo que muestra que el campo usado para el género es **_experienceplatform.individualCharacteristic.preferences.ferredGenre**.

![Agent Orchestrator](./images/chatgpt23.png)

Con esa información, puede empezar a explorar en profundidad los datos de compra.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/chatgpt24.png)

Entonces debería ver esto. Haga clic en **Referencia**.

![Agent Orchestrator](./images/chatgpt25.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/chatgpt26.png)

Desplácese hacia abajo para ver más información.

![Agent Orchestrator](./images/chatgpt27.png)

## 1.1.2.5 identificar Recorridos de fibra existentes

**Intención**

Descubra qué recorridos activos o finalizados recientemente incluyen &quot;Fibra&quot; en el título, por ejemplo, &quot;Actualización de fibra NYC - Septiembre&quot;, &quot;Prueba de fibra - Paquete de transmisión&quot;.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/chatgpt28.png)

Entonces debería ver esto. Haga clic en **Referencia**.

![Agent Orchestrator](./images/chatgpt29.png)

A continuación, debería ver una lista de recorridos.

![Agent Orchestrator](./images/chatgpt30.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/chatgpt31.png)

Entonces debería ver esto. Haga clic en **Referencia**.

![Agent Orchestrator](./images/chatgpt32.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/chatgpt33.png)

Desplácese hacia abajo para ver más detalles.

![Agent Orchestrator](./images/chatgpt34.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/chatgpt35.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/chatgpt36.png)

## 1.1.2.6 Validar el rendimiento del recorrido mediante el análisis de abandonos

**Intención**

Desea comprender las visitas en el orden previsto de rendimiento de la recorrido para saber si hay algún nodo o condición dentro de la recorrido que esté experimentando la pérdida de un gran porcentaje de perfiles. Esto resulta útil para saber si se necesitan ajustes adicionales en el recorrido.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/chatgpt37.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/chatgpt38.png)

Desplácese un poco hacia abajo. Ahora puede revisar la tabla inspeccionando cada nodo y sus respectivos números de entrada, números de visitas en el orden previsto y tasa de visitas en el orden previsto.

![Agent Orchestrator](./images/chatgpt39.png)

Desplácese hacia abajo un poco más para ver observaciones y recomendaciones.

![Agent Orchestrator](./images/chatgpt40.png)

Ahora has completado este laboratorio.

Volver a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}