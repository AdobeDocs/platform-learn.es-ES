---
title: Introducción a Agent Orchestrator
description: Introducción a Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: ffdc6b34a82c945c142f433f65a4f2f8d5cdcd18
workflow-type: tm+mt
source-wordcount: '1514'
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

>[!NOTE]
>
>En este laboratorio, cambiarás de contexto al moverte entre el análisis y la orquestación.

## 1.1.1.2 Comience con las tendencias generales de compra para anclar el contexto y ampliar el alcance de la fibra

**Intención**: recibe un impulso de nivel superior según la demanda de la categoría (móvil, teléfono fijo, Internet, TV, fibra), específicamente durante los últimos 60 días. Esto establece líneas de base para la estacionalidad, los efectos de promoción y la variación regional después del despliegue de NY.

**Pensando**:

&quot;¿Fiber está ganando cuota postNY? ¿Estamos viendo la canibalización de Internet de cobre/DSL? ¿Cuál es el cambio de mezcla frente a los paquetes de TV?&quot;

&quot;Esto me ayudará a dimensionar la audiencia a la que se puede dirigir en Viena y a establecer objetivos realistas&quot;.

**Lecturas procesables que el experto en marketing espera**:

Un gráfico de líneas/barras apiladas de compras por categoría principal (granulado diario/semanal).

Porcentaje de compras por categoría frente a períodos anteriores.

Picos importantes relacionados con las fechas promocionales.

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Debería ver lo siguiente:

>[!NOTE]
>
>Esté atento a la atribución retardada: los pedidos de fibra pueden capturarse en &quot;Internet&quot; en algunos esquemas heredados. Si es así, concilie la taxonomía antes de tomar decisiones.

![Agent Orchestrator](./images/ao5.png)

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Luego debería ver esto, que profundiza en las tendencias específicas de la fibra.

**Acción**: observe la curva de crecimiento y los picos regionales.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3: correlacionar pedidos con preferencias de contenido

**Intención**: Prueba la hipótesis de que la preferencia de contenido (por ejemplo, ciencia ficción, deportes, teatro) predice el comportamiento de actualización de banda ancha, especialmente para las necesidades de ancho de banda alto.

**Pensando**

&quot;Los fanáticos de ciencia ficción a menudo ven 4K y transmiten desde múltiples dispositivos; probablemente valoren la baja latencia&quot;.

&quot;Cuantifiquemos si SciFi (y tal vez Deportes) se correlaciona con pedidos recientes&quot;.

**Salidas esperadas**

Un pivote de pedidos (filtro de acumulado anual aplicado) desglosado por género preferido, limitado a los últimos 2 meses.

Clasificar géneros por tasa de conversión de pedidos y AOV (valor de pedido promedio).

Decisión: Si SciFi muestra una señal fuerte, esto se convierte en un pilar creativo principal para el lanzamiento de Fiber Max en Viena (por ejemplo, &quot;nunca más amortiguar&quot; mensajes, paquetes premium).

**Intención**

Analizar la conversión por género (por ejemplo, ciencia ficción, deportes).

**Objetivo** Validar si los fans de ciencia ficción sobreindexan las actualizaciones de fibra.

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 identificar Recorridos de fibra existentes

Haga clic en la ventana **context**.

![Agent Orchestrator](./images/ao10.png)

Establezca el contexto en:

- **Source de documentación**: **Adobe Journey Optimizer**
- **Espacio aislado**: **Acelerar**
- **Vista de datos**: **Acelerar B2C 2026**

![Agent Orchestrator](./images/ao11.png)

**Intención** Descubra qué recorridos activos o finalizados recientemente incluyen &quot;Fibra&quot; en el título, por ejemplo, &quot;Actualización de fibra NYC - Septiembre&quot;, &quot;Prueba de fibra - Paquete de transmisión&quot;.

**Pensando**

&quot;¿Cuál de estos recorridos tuvo un buen desempeño y cuáles fueron sus déclencheur?&quot;

&quot;¿Puedo reutilizar la lógica de orquestación ganadora para Viena?&quot;

**Salidas esperadas**

Lista de recorridos con estado (activo, pausado, finalizado), intervalos de fechas, segmentos de destinatario, KPI (tasa de apertura, CTR, conversión).

Siguiente movimiento: Preseleccione uno o dos recorridos de fibra exitosos para la clonación/adaptación.

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/ao13.png)

Enumere los recorridos activos o anteriores con la mensajería de fibra.

Acción: preseleccione recorridos de alto rendimiento para la clonación.

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Comprobar la semilla

**Intención**:

Comprenda la definición de la semilla del recorrido &quot;CitiSignal - Promoción de lanzamiento de Fiber Max&quot;: qué rasgos impulsaron la segmentación (por ejemplo, &quot;Preferencia de género SciFi&quot;, &quot;4+ dispositivos&quot;, &quot;flujo ≥ 300 GB/mes&quot;).

**Pensando**

&quot;Quiero combinar la creatividad de ciencia ficción probada con la mensajería de rendimiento de Fiber Max&quot;.

&quot;Si la audiencia se superpone con muchos descargadores, podemos apilar la propensión&quot;.

**Salidas esperadas**

Criterios de audiencia (inclusión/exclusión), tamaño de audiencia, filtros de región, actualización, umbrales de frecuencia.

>[!NOTE]
>
>Cambiar contexto a CJA

A partir de este punto, el experto en marketing cambia al modo de análisis para garantizar un sistema de informes adecuado.

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
What was the initial audience in the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/ao16.png)
Revise los criterios de audiencia (hábitos de streaming, recuento de dispositivos).

**Objetivo**: comprender los rasgos para las necesidades de ancho de banda alto.

## 1.1.1.6 Validar el rendimiento del recorrido mediante el análisis de abandonos

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

>[!NOTE]
>
>Cambiar contexto a CJA)

**Intención**:

Creación de un funnel paso a paso en Customer Journey Analytics

Entregado → Abierto → Se hizo clic → Aterrizó → Vista del producto → Añadir al carrito → Cierre de compra → Pedido completado

Incluya vistas de SKU relacionadas con fibra como rama.

**Pensando**:

&quot;¿Dónde estamos perdiendo personas: correo electrónico abierto, carga de página de aterrizaje, PDP, fricción de pago?&quot;

&quot;¿Los usuarios de ciencia ficción rebotan más o menos que el promedio en PDP de fibra?&quot;

**Resultados esperados**:

Una visualización de abandonos con tasas de caída en cada paso.

Superposiciones de segmentos (ciencia ficción vs deportes vs otros).

Desglose del dispositivo o explorador por fricción técnica.

**Decisiones**:

Si la pérdida de pago es alta, coordine con el producto/UX para corregir el flujo de pago.

Si la salida de PDP es alta, vuelva a trabajar para reclamar claridad (velocidades, tiempos de instalación, valor del paquete).

>[!NOTE]
>
>Cambiar contexto a TRABAJO

Ahora el experto en marketing se traslada a Adobe Journey Optimizer para las operaciones de orquestación y audiencia.

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey 
```

Generar visualización de funnel: Entregado → Abierto → Se Ha Hecho Clic → Finalizar Compra → Pedido.

**Acción**: identifique los puntos de entrega y optimice la mensajería o el UX.

## 1.1.1.7 Buscar audiencias existentes alineadas con un uso elevado

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Cambiar contexto a Adobe Journey Optimizer

**Intención**:

Busque cualquier audiencia de JO denominada con &quot;descargadores masivos&quot;, probablemente definida por umbrales de uso de datos mensuales, horas de streaming o concurrencia del dispositivo.

**Pensando**:

&quot;Si existe una audiencia como Heavy Downloaders, es perfecto para el posicionamiento de Fiber Max: velocidad, fiabilidad, niveles ilimitados&quot;.

**Resultados esperados**:

Metadatos de audiencia: criterios de definición, tamaño, última actualización, etiquetas de control, disponibilidad de región.

Localice audiencias con un uso de datos elevado.

**Objetivo**: Combínalo con la preferencia de ciencia ficción para la segmentación Fiber Max.

## 1.1.1.8 Determine si esas audiencias ya están en uso

**Intención**:

Compruebe el vínculo de audiencia a recorrido: asegúrese de que no doblamos el mensaje ni chocamos con los programas actuales.

**Pensando**:

&quot;Si Heavy Downloaders ya está en un recorrido de retención, necesitamos una lógica de supresión o un límite de frecuencia para evitar la fatiga&quot;.

**Resultados esperados**:

Asignaciones: audiencia → nombre del recorrido, estado, política de contacto, último envío, rendimiento.

**Decisión**:

Si está en uso, cree exclusiones o supresión compartida para el lanzamiento de Viena.

Si no está en uso, luz verde para recorrido nuevo.

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
Which of the above are used in a journey? 
```

Asegúrese de que no haya superposición con las campañas activas.

**Acción**: aplique la supresión si es necesario.

## 1.1.1.9 Crear nuevo Recorrido para el lanzamiento de Fiber Max

**Intención**:

Cree un nuevo recorrido dirigido a la audiencia compuesta:

Heavy Downloaders ∩ Preferencia SciFi (clave de audiencia kbaa_5207bf).

**Pensando**:

&quot;Este es el punto dulce para Fiber Max: alta tendencia + relevancia creativa&quot;.

&quot;Organizaremos una experiencia multitáctil vinculada a la disponibilidad de Viena&quot;.

**diseño de Recorrido (JO)**:

Criterios de entrada:

Audiencia: Heavy Downloaders - Ciencia ficción Preference_kbaa_5207bf

Geografía: metro de Viena (lista de código postal o polígono geográfico)

Elegibilidad: No está en la campaña activa de &quot;Actualización de fibra NYC - Septiembre&quot;; no es un suscriptor de fibra actual.

Déclencheur y tiempo:

T14 días antes del lanzamiento de Viena (enero de 2026): Previsualizar correo electrónico: &quot;Fiber Max está llegando&quot;.

Semana del lanzamiento: correo electrónico principal + banner en la aplicación + sincronización de medios de pago (a través del destino CDP).

T+3 días: división del comportamiento: si no hay clic, empuje SMS; si se hace clic pero no se ha solicitado, vuelva a emplear un CTA de disponibilidad del instalador.

T+10 días: prueba de oferta: instalación gratuita frente a descuento del primer mes (A/B).

Personalization:

Copia dinámica para los amantes de SciFi (latencia/enlaces de transmisión 4K).

Afirmaciones de velocidad/latencia adaptadas a la combinación de dispositivos (consolas de juegos, cajas de streaming).

Paquete de recomendaciones: Fiber Max + paquete de contenido premium para TV.

Gobernanza:

Límite de frecuencia: máximo 3 toques por 10 días.

Suprimir si el suscriptor de fibra actual o si el ticket existe para la instalación.

Respetar las preferencias de exclusión.

**Plan de medición (CJA)**:

Seguimiento: envío, apertura, clic, vista de PDP, inicio de cierre de compra, finalización de pedidos.

KPI: tasa de conversión a Fiber Max, aumento frente a control, tiempo de instalación.

Diagnóstico: informe de abandonos por dispositivo o segmento de género.

Cómo encaja todo esto (el modelo mental del experto en marketing)

Diagnosticar la demanda (categorías generales → fibra específicamente).

Probar contenido para señal de conversión (pedidos por género).

Mis recorridos exitosos (encontrar recorridos nombrados por Fiber y la audiencia promocional de SciFi).

Validar los puntos de fricción (abandonos de CJA en el recorrido SciFi).

Activar contra segmentos de alta tendencia (Heavy Downloaders ∩ SciFi).

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Entonces debería ver esto. Asegúrese de que se encuentra en la organización **Experience Platform International**.

Haga clic en la ventana **context**.

![Agent Orchestrator](./images/ao2.png)

Establezca el contexto en:

- **Source de documentación**: **Journey Optimizer**
- **Espacio aislado**: **Acelerar**
- **Vista de datos**: **Acelerar B2C 2026**

Haga clic en **Establecer contexto**.

![Agent Orchestrator](./images/aoea3.png)

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

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

## 1.1.1.10 experimentos

Vaya a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Entonces debería ver esto. Asegúrese de que se encuentra en la organización **Experience Platform International**.

Haga clic en la ventana **context**.

![Agent Orchestrator](./images/ao2.png)

Establezca el contexto en:

- **Source de documentación**: **Journey Optimizer**
- **Espacio aislado**: **Acelerar**
- **Vista de datos**: **Acelerar B2C 2026**

Haga clic en **Establecer contexto**.

![Agent Orchestrator](./images/aoea3.png)

Escriba el **indicador** siguiente y haga clic en el botón **generar**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Debería ver lo siguiente:

![Agent Orchestrator](./images/aoea1.png)

Haga clic en la sugerencia para comparar las tasas de conversión de cada tratamiento y luego haga clic en **generar**.

![Agent Orchestrator](./images/aoea2.png)

Entonces debería ver una comparación detallada como esta:

![Agent Orchestrator](./images/aoea4.png)

Volver a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}