---
title: Introducción a Agent Orchestrator
description: Introducción a Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: dee5b0855eeeb455bf22f511d11cd13f7e904889
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# 1.1.1 Introducción a Agent Orchestrator

## 1.1.1.1 establecer contexto en Agent Orchestrator

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Entonces debería ver esto. Asegúrese de que se encuentra en la organización **Experience Platform International**.

![Agent Orchestrator](./images/ao1.png)

Haga clic en la ventana **context**.

![Agent Orchestrator](./images/ao2.png)

Establezca el contexto en:

- **Source de documentación**: **Customer Journey Analytics**
- **Espacio aislado**: **Acelerar**
- **Vista de datos**: **Acelerar B2C 2026**

Haga clic en **Establecer contexto**.

![Agent Orchestrator](./images/ao3.png)

## 1.1.1.2 Comience con las tendencias generales de compra para anclar el contexto y ampliar el alcance de la fibra

**Intención**

Obtenga un impulso de nivel superior sobre la demanda de categorías (móvil, fijo, Internet, TV, fibra), específicamente durante los últimos 60 días. Esto establece líneas de base para la estacionalidad, los efectos de promoción y la variación regional después del despliegue en Nueva York.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/ao5.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Luego debería ver esto, que profundiza en las tendencias específicas de la fibra.

**Acción**: observe la curva de crecimiento y los picos regionales.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3: correlacionar pedidos con preferencias de contenido

**Intención**

Pruebe la hipótesis de que la preferencia de contenido (por ejemplo, ciencia ficción, deportes, teatro) predice el comportamiento de actualización de banda ancha, especialmente para necesidades de banda ancha alta.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 identificar Recorridos de fibra existentes

**Intención**

Descubra qué recorridos activos o finalizados recientemente incluyen &quot;Fibra&quot; en el título, por ejemplo, &quot;Actualización de fibra NYC - Septiembre&quot;, &quot;Prueba de fibra - Paquete de transmisión&quot;.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/ao13.png)

Enumere los recorridos activos o anteriores con la mensajería de fibra.

Acción: preseleccione recorridos de alto rendimiento para la clonación.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Comprobar la semilla

**Intención**:

Comprenda la definición de la semilla del recorrido &quot;CitiSignal - Promoción de lanzamiento de Fiber Max&quot;: qué rasgos impulsaron la segmentación (por ejemplo, &quot;Preferencia de género SciFi&quot;, &quot;4+ dispositivos&quot;, &quot;flujo ≥ 300 GB/mes&quot;).

Escriba el **indicador** siguiente y, a continuación, escriba **+CitiSignal fib** para habilitar el completado automático. Seleccione el recorrido **CitiSignal - Promoción de lanzamiento de Fiber Max**.

```javascript
What was the initial audience in the journey named 
```

![Agent Orchestrator](./images/ao16.png)

Entonces debería ver esto. Haga clic en el botón **enviar**.

![Agent Orchestrator](./images/ao17.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validar el rendimiento del recorrido mediante el análisis de abandonos

**Intención**

Creación de un funnel paso a paso en Customer Journey Analytics

Entregado → Abierto → Se hizo clic → Aterrizó → Vista del producto → Añadir al carrito → Cierre de compra → Pedido completado

Incluya vistas de SKU relacionadas con fibra como rama.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

## 1.1.1.7 Crear una audiencia nueva

**Intención**

En base a los hallazgos anteriores, existe una correlación entre los clientes que consumen muchos datos y que tienen un género preferido de ciencia ficción o fantasía. Ahora combinará estos atributos en una audiencia.

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

>[!NOTE]
>
>Compruebe que el contexto del asistente señala a la zona protegida **Accelerate** y a la vista de datos **Accelerate 2026 B2C**

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Revise el plan. Escriba `yes` y haga clic en **enviar**.

![Agent Orchestrator](./images/ao33.png)

Revise la expresión de consulta del segmento. Escriba `yes` y haga clic en el botón **enviar**.

![Agent Orchestrator](./images/ao34.png)

Revise la estimación del tamaño del segmento. Escriba `yes` y haga clic en el botón **enviar**.

![Agent Orchestrator](./images/ao35.png)

Haga clic en **Revisar**.

![Agent Orchestrator](./images/ao36.png)

Revise la definición del segmento. Haga clic en **Crear**.

![Agent Orchestrator](./images/ao37.png)

Se ha creado la audiencia.

![Agent Orchestrator](./images/ao38.png)

>[!NOTE]
>
>Cuando se crea una audiencia nueva, el asistente tarda 24 horas en estar disponible para su uso posterior.

## 1.1.1.8 Busque audiencias existentes alineadas con un uso elevado y compruebe si están en uso

**Intención**:

Busque cualquier audiencia denominada con &quot;descargadores masivos&quot;, definida por los umbrales mensuales de uso de datos.

>[!NOTE]
>
>En la versión anterior creó una nueva audiencia, recuerde que el asistente tardará 24 horas en estar disponible para su uso posterior. Ahora debería usar otra audiencia que ya exista en su lugar.

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Entonces debería ver esto. Asegúrese de que se encuentra en la organización **Experience Platform International**.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

>[!NOTE]
>
>Compruebe que el contexto del asistente señala a la zona protegida **Accelerate** y a la vista de datos **Accelerate 2026 B2C**

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/ao31.png)

Ya existen algunas audiencias para &quot;descargadores pesados&quot;. Vamos a ver si ya están en uso.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

Entonces debería ver algo similar a esto.

![Agent Orchestrator](./images/ao51.png)

Ahora debería comprobar si ese recorrido está activo. Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao52.png)

Entonces debería ver algo similar a esto. Ese recorrido no está corriendo en este momento.

![Agent Orchestrator](./images/ao53.png)

Para el próximo lanzamiento de Fiber Max, debería crear un nuevo recorrido.

## 1.1.1.9 Crear nuevo Recorrido para el lanzamiento de Fiber Max

**Intención**:

Cree un nuevo recorrido dirigido a la audiencia compuesta:

Heavy Downloaders ∩ Preferencia SciFi (clave de audiencia kbaa_5207bf).

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Entonces debería ver esto. Asegúrese de que se encuentra en la organización **Experience Platform International**.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

>[!NOTE]
>
>Compruebe que el contexto del asistente señala a la zona protegida **Accelerate** y a la vista de datos **Accelerate 2026 B2C**

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Entonces debería ver esto. Escriba `yes` y haga clic en generar.

![Agent Orchestrator](./images/aocj2.png)

Entonces debería ver esto. Escriba `yes` y haga clic en generar.

![Agent Orchestrator](./images/aocj3.png)

Entonces debería ver esto. Escriba `The first one` y haga clic en generar.

![Agent Orchestrator](./images/aocj4.png)

Entonces debería ver esto. Escriba `yes` y haga clic en generar.

![Agent Orchestrator](./images/aocj5.png)

Revise la respuesta. Escriba `yes` y haga clic en generar.

![Agent Orchestrator](./images/aocj6.png)

Haga clic en **Revisar**.

![Agent Orchestrator](./images/aocj7.png)

Actualice el nombre del recorrido con su LDAP para que sea único. Haga clic en **Guardar**.

![Agent Orchestrator](./images/aocj8.png)

El recorrido se ha creado en modo de borrador.

![Agent Orchestrator](./images/aocj9.png)

## 1.1.1.10 administración de conflictos de Recorrido

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Entonces debería ver esto. Asegúrese de que se encuentra en la organización **Experience Platform International**.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

>[!NOTE]
>
>Compruebe que el contexto del asistente apunta a la fuente de documentación **Journey Optimizer**, la zona protegida **Accelerate** y la vista de datos **Accelerate 2026 B2C**

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

Revise la información.

![Agent Orchestrator](./images/aocj81.png)

Desplácese hacia abajo y seleccione **Fuentes** para comprobar que la información procede de Experience League.

![Agent Orchestrator](./images/aocj82.png)

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
List any conflicts for "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aocj70.png)

Revise la información de conflictos de recorrido.

![Agent Orchestrator](./images/aocj71.png)

Desplácese hacia abajo para ver más detalles sobre conflictos de recorrido.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11 experimentos

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Entonces debería ver esto. Asegúrese de que se encuentra en la organización **Experience Platform International**.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

>[!NOTE]
>
>Compruebe que el contexto del asistente señala a la zona protegida **Accelerate** y a la vista de datos **Accelerate 2026 B2C**

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/aoea1.png)

Haga clic en la sugerencia para comparar las tasas de conversión de cada tratamiento y luego haga clic en **enviar**.

![Agent Orchestrator](./images/aoea2.png)

Entonces debería ver una comparación detallada como esta:

![Agent Orchestrator](./images/aoea4.png)

Volver a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}