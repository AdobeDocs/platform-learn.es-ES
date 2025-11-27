---
title: Introducción a Agent Orchestrator
description: Introducción a Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: bb31fe8a36f1c9ee9d212500e2e58e01be1129b8
workflow-type: tm+mt
source-wordcount: '1375'
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

- **Source de documentación**: **Journey Optimizer**

La configuración de Source de documentación ayuda a dar preferencia a qué conjunto de documentos de Experience League comprobar si hay preguntas relacionadas con el conocimiento del producto o Experience League.

- **Espacio aislado**: **Prod - Accelerate (VA7)**

La configuración de la zona protegida ayuda a identificar qué simulador de pruebas debe consultar el asistente al hacer preguntas.

- **Vista de datos**: **Acelerar B2C 2026**

La configuración de vista de datos ayuda a identificar qué vista de datos debe ver el asistente de IA al hacer preguntas.

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

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3: correlacionar pedidos con preferencias de contenido

**Intención**

Pruebe la hipótesis de que una preferencia por un género específico (por ejemplo, ciencia ficción, deportes, teatro) predice el comportamiento de actualización de banda ancha, especialmente para las necesidades de banda ancha alta.

En primer lugar, debe averiguar qué campo se utiliza para almacenar la preferencia de género.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Which field is used to store the preferred genre?
```

![Agent Orchestrator](./images/ao7a.png)

Debería ver esto, lo que muestra que el campo usado para el género es **_experienceplatform.individualCharacteristic.preferences.ferredGenre**.

![Agent Orchestrator](./images/ao7b.png)

Con esa información, puede empezar a explorar en profundidad los datos de compra.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Entonces debería ver esto. Haga clic en el icono en el bloque **Razonamiento completado** para comprender lo que sucede en Agent Orchestrator entre bastidores.

![Agent Orchestrator](./images/ao9.png)

Debería ver una explicación similar.

![Agent Orchestrator](./images/ao10.png)

## 1.1.1.4 identificar Recorridos de fibra existentes

**Intención**

Descubra qué recorridos activos o finalizados recientemente incluyen &quot;Fibra&quot; en el título, por ejemplo, &quot;Actualización de fibra NYC - Septiembre&quot;, &quot;Prueba de fibra - Paquete de transmisión&quot;.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Entonces debería ver esto. Haga clic en **Mostrar más**.

![Agent Orchestrator](./images/ao13.png)

A continuación, debería ver una lista más amplia de recorridos activos o pasados. Haga clic en el icono **descargar** para descargar una lista de estos recorridos.

![Agent Orchestrator](./images/ao13a.png)

Esto generará un archivo CSV para usted que contiene todos los resultados del asistente de IA.

![Agent Orchestrator](./images/ao13b.png)

Haga clic en para cerrar el panel derecho. Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Entonces debería ver esto. Haga clic en el vínculo de uno de los recorridos y seleccione **Detalles del Recorrido**.

![Agent Orchestrator](./images/ao15.png)

Se abrirá una nueva ventana y se le redirigirá inmediatamente a la descripción general de Detalles del Recorrido.

![Agent Orchestrator](./images/ao15a.png)

## 1.1.1.5 Comprobar qué audiencia se utiliza

**Intención**:

Comprenda la definición de la semilla del recorrido &quot;CitiSignal - Promoción de lanzamiento de Fiber Max&quot;: qué rasgos impulsaron la segmentación (por ejemplo, &quot;Preferencia de género SciFi&quot;, &quot;4+ dispositivos&quot;, &quot;flujo ≥ 300 GB/mes&quot;).

Escriba el **indicador** siguiente:

```javascript
What was the initial audience in the journey named 
```

A continuación, escriba manualmente `+CitiSignal fib` para habilitar el completado automático. Seleccione el recorrido **CitiSignal - Promoción de lanzamiento de Fiber Max**.

![Agent Orchestrator](./images/ao16.png)

Entonces debería ver esto. Haga clic en el botón **enviar**.

![Agent Orchestrator](./images/ao17.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Validar el rendimiento del recorrido mediante el análisis de abandonos

**Intención**

Desea comprender las visitas en el orden previsto de rendimiento de la recorrido para saber si hay algún nodo o condición dentro de la recorrido que esté experimentando la pérdida de un gran porcentaje de perfiles. Esto resulta útil para saber si se necesitan ajustes adicionales en el recorrido.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

Entonces debería ver esto.

![Agent Orchestrator](./images/ao20.png)

Desplácese un poco hacia abajo. Ahora puede revisar la tabla inspeccionando cada nodo y sus respectivos números de entrada, números de visitas en el orden previsto y tasa de visitas en el orden previsto.

AI Assistant le ofrece observaciones y recomendaciones.

Haga clic en la frase **Así es como obtuve los resultados**.

![Agent Orchestrator](./images/ao21.png)

A continuación, puede ver los pasos seguidos por AI Assistant para llegar a los resultados.

![Agent Orchestrator](./images/ao22.png)

## 1.1.1.7 Crear una audiencia nueva

**Intención**

En base a los hallazgos e investigaciones anteriores, existe una correlación entre los clientes que consumen muchos datos y que tienen un género preferido de ciencia ficción o fantasía. Ahora combinará estos atributos en una audiencia.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Revise el plan. Escriba `yes` y haga clic en **enviar**.

>[!NOTE]
>
>Este plan se genera en función de una guía de referencia del sistema. Los clientes podrán personalizar planes y añadir sus propios planes, pero por ahora son estáticos.

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
>Al crear una audiencia nueva, pasarán 24 horas antes de que la audiencia esté disponible para que el asistente de IA la utilice más.

## 1.1.1.8 Busque audiencias existentes alineadas con un uso elevado y compruebe si están en uso

**Intención**:

Busque cualquier audiencia denominada con &quot;descargadores masivos&quot;, definida por los umbrales mensuales de uso de datos.

>[!NOTE]
>
>En el paso anterior creó una nueva audiencia, recuerde que pasarán 24 horas antes de que la audiencia esté disponible para el asistente de IA para un uso posterior. Ahora debería usar otra audiencia que ya exista en su lugar.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Entonces debería ver esto. Ahora desea ver todas sus audiencias y cuánto han cambiado en los últimos días.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
List how much these audiences changed over the last few days.
```

![Agent Orchestrator](./images/ao31.png)

Entonces debería ver esto. Haga clic en **Mostrar más**.

![Agent Orchestrator](./images/ao31a.png)

Entonces debería ver esto. Haga clic en para cerrar el panel derecho.

![Agent Orchestrator](./images/ao31b.png)

Desplácese un poco hacia abajo para revisar los pasos realizados por el Asistente de IA.

![Agent Orchestrator](./images/ao31c.png)

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
Are these journeys active? 
```

![Agent Orchestrator](./images/ao52.png)

Entonces debería ver algo similar a esto. Ninguno de estos recorridos se está ejecutando actualmente.

![Agent Orchestrator](./images/ao53.png)

Para el próximo lanzamiento de Fiber Max, debería crear un nuevo recorrido.

## 1.1.1.9 Crear nuevo Recorrido para el lanzamiento de Fiber Max

**Intención**:

Cree un nuevo recorrido dirigido a la audiencia compuesta:

Heavy Downloaders ∩ Preferencia de ciencia ficción.

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Entonces debería ver esto. Escriba `yes` y haga clic en generar.

![Agent Orchestrator](./images/aocj2.png)

Entonces debería ver esto. Escriba `yes` y haga clic en generar.

![Agent Orchestrator](./images/aocj3.png)

Entonces debería ver esto. Escriba `The first one` y haga clic en enviar.

![Agent Orchestrator](./images/aocj4.png)

Entonces debería ver esto. Escriba `yes` y haga clic en enviar.

![Agent Orchestrator](./images/aocj5.png)

Revise la respuesta. Escriba `yes` y haga clic en enviar.

![Agent Orchestrator](./images/aocj6.png)

Haga clic en **Revisar**.

![Agent Orchestrator](./images/aocj7.png)

Actualice el nombre del recorrido con su LDAP para que sea único. Haga clic en **Guardar**.

![Agent Orchestrator](./images/aocj8.png)

El recorrido se ha creado en modo de borrador.

![Agent Orchestrator](./images/aocj9.png)

## 1.1.1.10 administración de conflictos de Recorrido

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

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
List any conflicts for the journey +CitiSignal Fiber Max
```

A continuación, seleccione manualmente el recorrido **CitiSignal - Fiber Max Launch Promotion** de la lista.

![Agent Orchestrator](./images/aocj70.png)

Entonces debería ver esto. Haga clic en **enviar**.

![Agent Orchestrator](./images/aocj70a.png)

Revise la información de conflictos de recorrido.

![Agent Orchestrator](./images/aocj71.png)

Desplácese hacia abajo para ver más detalles sobre conflictos de recorrido.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11 experimentos

Escriba el **indicador** siguiente y haga clic en el botón **enviar**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/aoea1.png)

Desplácese hacia abajo y haga clic en una de las sugerencias. Haga clic en **enviar**.

>[!NOTE]
>
>Las sugerencias son dinámicas, por lo que debería ver sugerencias diferentes cada vez que se genere una respuesta. Es probable que sus sugerencias sean diferentes a las que se muestran en esta captura de pantalla.

![Agent Orchestrator](./images/aoea2.png)

Debería ver una respuesta detallada relacionada con la sugerencia elegida.

![Agent Orchestrator](./images/aoea4.png)

Ahora has completado este laboratorio.

Volver a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}