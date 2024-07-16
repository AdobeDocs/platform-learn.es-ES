---
title: Bootcamp - Customer Journey Analytics - Visualización con Customer Journey Analytics
description: Bootcamp - Customer Journey Analytics - Visualización con Customer Journey Analytics
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: 051b5b91-56c4-414e-a4c4-74aa67219551
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 0%

---

# 4.5 Visualización con el Customer Journey Analytics

## Objetivos

- Explicación de la IU de Analysis Workspace
- Conozca algunas funciones que hacen que Analysis Workspace sea tan diferente.
- Obtenga información sobre cómo analizar en CJA mediante Analysis Workspace

## Contexto

En este ejercicio utilizará Analysis Workspace dentro de CJA para analizar vistas de productos, canales de productos, pérdidas, etc.

Usemos el proyecto que creó en [4.4 Preparación de datos en Analysis Workspace](./ex4.md), así que vaya a [https://analytics.adobe.com](https://analytics.adobe.com).

![demostración](./images/prohome.png)

Abra el proyecto `yourLastName - Omnichannel Analysis`.

Con el proyecto abierto y la vista de datos `CJA Bootcamp - Omnichannel Data View` seleccionada, está listo para empezar a crear sus primeras visualizaciones.

![demostración](./images/prodataView1.png)

## ¿Cuántas vistas de productos tenemos diariamente?

En primer lugar, es necesario seleccionar las fechas adecuadas para analizar los datos. Vaya al menú desplegable de calendario en el lado derecho del lienzo. Haga clic en él y seleccione el intervalo de fechas aplicable.

>[!IMPORTANT]
>
>Los datos más recientes disponibles se han introducido el 19/09/2022; seleccione un intervalo de fechas que incluya esta fecha.

![demostración](./images/pro1.png)

En el menú del lado izquierdo (área de componentes), busque la Métrica calculada **Vistas del producto**. Selecciónelo, arrástrelo y suéltelo en el lienzo, en la parte superior derecha de la tabla de forma libre.

![demostración](./images/pro2.png)

Automáticamente, se agregará la dimensión **Day** para crear su primera tabla. Ahora puedes ver tu pregunta respondida en el vuelo.

![demostración](./images/pro3.png)

A continuación, haga clic con el botón derecho en el resumen de la métrica.

![demostración](./images/pro4.png)

Haga clic en **Visualizar** y, a continuación, seleccione **Línea** como visualización.

![demostración](./images/pro5.png)

Verá las vistas de sus productos por día.

![demostración](./images/pro6.png)

Puede cambiar el ámbito de tiempo al día haciendo clic en **Configuración** dentro de la visualización.

![demostración](./images/pro7.png)

Haga clic en el punto al lado de **Línea** para **Administrar el Source de datos**.

![demostración](./images/pro7a.png)

A continuación, haga clic en **Bloquear selección** y seleccione **Elementos seleccionados** para bloquear esta visualización y que siempre muestre una cronología de vistas de productos.

![demostración](./images/pro7b.png)

## Principales 4 productos vistos

¿Cuáles son los 4 productos principales vistos?

Recuerde guardar el proyecto de vez en cuando.

| Sistema operativo | Método abreviado |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Comando + S |

Empecemos a encontrar los 4 productos más vistos. En el menú del lado izquierdo, busque el Dimension **Product Name** -.

![demostración](./images/pro8.png)

Ahora arrastre y suelte **Nombre de producto** para reemplazar la dimensión **Día**:

Este será el resultado

![demostración](./images/pro10a.png)

A continuación, intente desglosar uno de los productos por Nombre de marca. Busque **brandName** y arrástrelo bajo el primer nombre de producto.

![demostración](./images/pro13.png)

A continuación, realice un desglose utilizando el nivel de lealtad. Busque **Nivel de fidelidad** y arrástrelo bajo el nombre de la marca.

![demostración](./images/pro15.png)

A continuación, verá esto:

![demostración](./images/pro15a.png)

Por último, puede añadir más visualizaciones. En el lado izquierdo, debajo de visualizaciones, busque `Donut`. Tome `Donut`, arrástrelo y suéltelo en el lienzo bajo la visualización **Línea**.

![demostración](./images/pro18.png)

A continuación, en la tabla, seleccione las 3 **filas de nivel de fidelidad** del desglose que hicimos en **Google Pixel XL Black Smartphone de 32 GB** > **Citi Signal**. Mientras selecciona las 3 filas, mantenga presionado el botón **CTRL** (en Windows) o el botón **Comando** (en Mac).

![demostración](./images/pro20.png)

Verá que el gráfico de anillo ha cambiado:

![demostración](./images/pro21.png)

Incluso puede adaptar el diseño para que sea más legible, haciendo que el gráfico **Línea** y el gráfico **Anillo** sean un poco más pequeños para que puedan encajar uno junto al otro:

![demostración](./images/pro22.png)

Haz clic en el punto al lado de **Anillo** para **administrar el Source de datos**.
A continuación, haga clic en **Bloquear selección** para bloquear esta visualización y que siempre muestre una cronología de vistas de productos.

![demostración](./images/pro22b.png)

Obtenga más información acerca de las visualizaciones con Analysis Workspace aquí:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Canal de interacción de productos, desde la visualización hasta la compra

Hay muchas maneras de resolver esta pregunta. Uno de ellos es utilizar el tipo de interacción de producto y utilizarlo en una tabla de forma libre. Otra forma es usar una **Visualización de abandonos**. Usemos el último ya que queremos visualizar y analizar al mismo tiempo.

Cierre el panel actual haciendo clic aquí:

![demostración](./images/pro23.png)

Ahora agregue un nuevo panel en blanco al hacer clic en **+ Agregar panel en blanco**.

![demostración](./images/pro24.png)

Haga clic en la visualización **Abandonos**.

![demostración](./images/pro25.png)

Seleccione el mismo intervalo de fechas que en el ejercicio anterior.

![demostración](./images/pro1.png)

Entonces verá esto...

![demostración](./images/prodatefa.png)

Busque la dimensión **Tipo de evento** en los componentes del lado izquierdo:

![demostración](./images/pro26.png)

Haga clic en la flecha para abrir la dimensión:

![demostración](./images/pro27.png)

Verá todos los tipos de eventos disponibles.

![demostración](./images/pro28.png)

Seleccione el elemento **commerce.productViews** y arrástrelo y suéltelo en el campo **Agregar punto de contacto** dentro de la **Visualización de visitas en el orden previsto**.

![demostración](./images/pro29.png)

Haz lo mismo con **commerce.productListAdds** y **commerce.purchases** y suéltalos en el campo **Agregar Touchpoint** dentro de la **Visualización de abandonos**. La visualización tendrá este aspecto:

![demostración](./images/props1.png)

Puedes hacer muchas cosas aquí. Algunos ejemplos: compare con el paso del tiempo, compare cada paso por dispositivo o compare por fidelidad. Sin embargo, si queremos analizar cosas interesantes como por qué los clientes no compran después de agregar un artículo al carro de compras, podemos usar la mejor herramienta en CJA: hacer clic con el botón derecho.

Haga clic con el botón derecho en el punto de contacto **commerce.productListAdds**. Luego haz clic en **Abandonos por desglose en este punto de contacto**.

![demostración](./images/pro32.png)

Se creará una nueva tabla de forma libre para analizar qué hicieron las personas si no realizaron la compra.

![demostración](./images/pro33.png)

Cambie **Tipo de evento** por **Nombre de página**, en la nueva tabla de forma libre, para ver a qué páginas se dirigen en lugar de la página de confirmación de compra.

![demostración](./images/pro34.png)

## ¿Qué hacen las personas en el sitio antes de llegar a la página Cancelar servicio?

De nuevo, hay muchas maneras de realizar este análisis. Usemos el análisis de flujo para iniciar la parte de descubrimiento.

Cierre el panel actual haciendo clic aquí:

![demostración](./images/pro0.png)

Ahora agregue un nuevo panel en blanco al hacer clic en **+ Agregar panel en blanco**.

![demostración](./images/pro0a.png)

Haga clic en la visualización **Flujo**.

![demostración](./images/pro35.png)

A continuación, verá esto:

![demostración](./images/pro351.png)

Seleccione el mismo intervalo de fechas que en el ejercicio anterior.

![demostración](./images/pro1.png)

Busque la dimensión **Nombre de página** en los componentes del lado izquierdo:

![demostración](./images/pro36.png)

Haga clic en la flecha para abrir la dimensión:

![demostración](./images/pro37.png)

Encontrará todas las páginas vistas. Buscar el nombre de página: **Cancelar servicio**.
Arrastre y suelte **Cancelar servicio** en la visualización de flujo del campo central:

![demostración](./images/pro38.png)

A continuación, verá esto:

![demostración](./images/pro40.png)

Analicemos ahora si los clientes que visitaron la página **Cancelar servicio** en el sitio web también llamaron al centro de llamadas y cuál fue el resultado.

En las dimensiones, vuelva atrás y luego busque **Tipo de interacción de llamada**.
Arrastre y suelte **Tipo de interacción de llamada** para reemplazar la primera interacción a la derecha en **Visualización de flujo**.

![demostración](./images/pro43.png)

Ahora está viendo el ticket de asistencia de los clientes que llamaron al centro de llamadas después de visitar la página **Cancelar servicio**.

![demostración](./images/pro44.png)

A continuación, en las dimensiones, busca **Sensación de llamada**.  Arrástrela y suéltela para reemplazar la primera interacción a la derecha en **Visualización de flujo**.

![demostración](./images/pro46.png)

A continuación, verá esto:

![demostración](./images/flow.png)

Como puede ver, hemos ejecutado un análisis omnicanal utilizando la Visualización de flujo. Gracias a eso hemos encontrado que parece que algunos clientes que estaban pensando en cancelar su servicio, tuvieron una sensación positiva después de llamar al centro de llamadas. ¿Tal vez hemos cambiado de opinión con un ascenso?


## ¿Qué rendimiento tienen los clientes con un contacto del centro de llamadas positivo respecto a los KPI principales?

Primero segmentemos los datos para obtener solamente usuarios con llamadas **positivas**. En CJA, los segmentos se denominan Filtros. Vaya a los filtros dentro del área del componente (en el lado izquierdo) y haga clic en **+**.

![demostración](./images/pro58.png)

Dentro del Generador de filtros, asigne un nombre al filtro

| Nombre | Descripción |
| ----------------- |-------------| 
| Sensación de llamada: positiva | Sensación de llamada: positiva |

![demostración](./images/pro47.png)

En los componentes (dentro del Generador de filtros), busque **Sensación de llamada** y arrástrela y suéltela en la definición del Generador de filtros.

![demostración](./images/pro48.png)

Ahora seleccione **positivo** como valor para el filtro.

![demostración](./images/pro49.png)

Cambie el ámbito al nivel **Persona**.

![demostración](./images/pro50.png)

Para finalizar, simplemente haz clic en **Guardar**.

![demostración](./images/pro51.png)

Entonces volverás a estar aquí. Si aún no lo ha hecho, cierre el panel anterior.

![demostración](./images/pro0c.png)

Ahora agregue un nuevo panel en blanco al hacer clic en **+ Agregar panel en blanco**.

![demostración](./images/pro24c.png)

Seleccione el mismo intervalo de fechas que en el ejercicio anterior.

![demostración](./images/pro1.png)

Haga clic en **Tabla de forma libre**.

![demostración](./images/pro52.png)

Ahora arrastre y suelte el filtro que acaba de crear.

![demostración](./images/pro53.png)

Tiempo para añadir algunas métricas. Comience con **Vistas del producto**. Arrastre y suelte en la tabla de forma libre. También puede eliminar la métrica **Eventos**.

![demostración](./images/pro54.png)

Haz lo mismo con **Personas**, **Agregar al carro** y **Compras**. Vas a terminar con una mesa como esta.

![demostración](./images/pro55.png)

Gracias al primer análisis de flujo, surgió una nueva pregunta. Por lo tanto, decidimos crear esta tabla y comparar algunos KPI con un segmento para responder esa pregunta. Como puede ver, el tiempo para obtener información es mucho más rápido que usar SQL o usar otras soluciones de BI.

## Customer Journey Analytics y resumen de Analysis Workspace

Como ha aprendido en este laboratorio, Analysis Workspace vincula los datos de todos los canales para analizar el recorrido completo del cliente. Además, recuerde que puede incluir datos en el mismo espacio de trabajo que no esté vinculado al recorrido.
Puede resultar muy útil incluir datos desconectados en el análisis para dar contexto al recorrido. Algunos ejemplos incluyen datos NPS, encuestas, eventos de Facebook Ads o interacciones sin conexión (no identificadas).

Paso siguiente: [4.6 De las perspectivas a la acción](./ex6.md)

[Volver al flujo de usuario 4](./uc4.md)

[Volver a todos los módulos](./../../overview.md)
