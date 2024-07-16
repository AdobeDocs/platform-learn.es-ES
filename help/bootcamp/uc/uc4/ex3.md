---
title: Bootcamp - Customer Journey Analytics - Crear una vista de datos
description: Customer Journey Analytics - Crear una vista de datos
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: e634876c-2b1c-4f7f-99e5-1940f6c87d80
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 2%

---

# 4.3 Crear una vista de datos

## Objetivos

- Información sobre la IU de vista de datos
- Comprender la configuración básica de la definición de visita
- Explicación de la atribución y la persistencia en una vista de datos

## 4.3.1 Vista de datos

Con la conexión terminada, ahora puede progresar para influir en la visualización de. Una diferencia entre Adobe Analytics y CJA es que CJA necesita una vista de datos para limpiar y preparar los datos antes de la visualización.

Una vista de datos es similar al concepto de Grupos de informes virtuales en Adobe Analytics, donde define definiciones de visitas según el contexto, filtros y también cómo se llaman los componentes.

Necesitará un mínimo de una vista de datos por conexión. Sin embargo, en algunos casos de uso, es recomendable tener varias vistas de datos para la misma conexión, con el objetivo de proporcionar perspectivas diferentes a equipos diferentes.
Si quiere que su empresa se base en los datos, debe adaptar cómo se ven los datos en cada equipo. Algunos ejemplos:

- Métricas de UX solo para el equipo de diseño de UX
- Utilice los mismos nombres para los KPI y las métricas para los Google Analytics que para los Customer Journey Analytics, de modo que el equipo de análisis digital solo pueda hablar un idioma.
- Vista de datos filtrada para mostrar, por ejemplo, datos de un solo mercado, de una marca o solo de dispositivos móviles.

En la pantalla **Conexiones**, marque la casilla de verificación que aparece delante de la conexión que acaba de crear. Haga clic en **Crear vista de datos**.

![demostración](./images/exta.png)

Se le redirigirá al flujo de trabajo **Crear vista de datos**.

![demostración](./images/0-v2.png)

## 4.3.2 Definición de vista de datos

Ahora puede configurar las definiciones básicas para la vista de datos.

![demostración](./images/0-v2.png)

La **conexión** que creó en el ejercicio anterior ya está seleccionada. Su conexión se llama `yourLastName – Omnichannel Data Connection`.

![demostración](./images/ext5.png)

A continuación, asigne un nombre a la vista de datos según esta convención de nomenclatura: `yourLastName – Omnichannel Data View`.

Escriba el mismo valor para la descripción: `yourLastName – Omnichannel Data View`.

| Nombre | Descripción |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![demostración](./images/1-v2.png)

Para la **Zona horaria**, seleccione la zona horaria **Berlín, Estocolmo, Roma, Berna, Bruselas, Viena, Ámsterdam GMT+01:00**. Este es un entorno realmente interesante, ya que algunas empresas operan en diferentes países y regiones geográficas. Asignar el huso horario adecuado para cada país evitará errores típicos en los datos, como creer que, por ejemplo, en Perú, la mayoría de la gente compra camisetas a las 4:00 a.m.

![demostración](./images/ext7.png)

También puede modificar la nomenclatura de las métricas principales (Persona, Sesión y Evento). Esto no es obligatorio, pero a algunos clientes les gusta utilizar Personas, Visitas y Visitas individuales en lugar de Persona, Sesión y Eventos (convención de nomenclatura predeterminada de Customer Journey Analytics).

Ahora debe tener configurada la siguiente configuración:

![demostración](./images/1-v2.png)

Haga clic en **Guardar y continuar**.

![demostración](./images/12-v2.png)

## 4.3.3 Componentes de vista de datos

En este ejercicio, configurará los componentes que necesita para analizar los datos y visualizarlos con Analysis Workspace. En esta interfaz de usuario, hay tres áreas principales:

- Izquierda: componentes disponibles de los conjuntos de datos seleccionados
- Medio: componentes añadidos a la vista de datos
- Lado derecho: Configuración de componentes

![demostración](./images/2-v2.png)

>[!IMPORTANT]
>
>Si no encuentra una métrica o dimensión específica, compruebe si el campo `Contains data` se ha eliminado de la vista de datos. Si no es así, elimine ese campo.
>
>![demostración](./images/2-v2a.png)

Ahora tiene que arrastrar y soltar los componentes que necesita para el análisis en **Componentes agregados**. Para ello, debe seleccionar los componentes en el menú de la izquierda y arrastrarlos y soltarlos en el lienzo en el centro.

Empecemos con el primer componente: **Nombre (web.webPageDetails.name)**. Busque este componente y, a continuación, arrástrelo y suéltelo en el lienzo.

![demostración](./images/3-v2.png)

Este componente es el nombre de página, tal como se puede derivar de la lectura del campo de esquema `(web.webPageDetails.name)`.

Sin embargo, usar **Name** como nombre no es la mejor convención de nombres para que un usuario empresarial entienda rápidamente esta dimensión.

Cambiemos el nombre a **Nombre de página**. Haga clic en el componente y cambie su nombre en el área **Configuración de componentes**.

![demostración](./images/3-0-v2.png)

Algo muy importante es la **configuración de persistencia**. El concepto de evars y prop no existe en CJA, pero la configuración de Persistencia hace posible un comportamiento similar.

![demostración](./images/3-0-v21.png)

Si no cambia esta configuración, CJA interpretará la dimensión como **Prop** (nivel de visita individual). Además, podemos cambiar la Persistencia para que la dimensión sea un **eVar** (persista el valor a través del recorrido).

Si no está familiarizado con eVars y Props, puede [leer más sobre ellos en la documentación](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html).

Dejemos el nombre de página como una prop. Por lo tanto, no es necesario que cambie ninguna **Configuración de persistencia**.

| Nombre del componente a buscar | Nuevo nombre | Configuración de persistencia |
| ----------------- |-------------| --------------------| 
| Nombre (web.webPageDetails.name) | Nombre de página |          |

A continuación, elija la dimensión **phoneNumber** y suéltela en el lienzo. El nuevo nombre debe ser **Número de teléfono**.

![demostración](./images/3-1-v2.png)

Por último, vamos a cambiar la configuración de Persistencia, ya que el Número móvil debe persistir en el nivel de usuario.

Para cambiar la Persistencia, desplácese hacia abajo en el menú derecho y abra la pestaña **Persistencia**:

![demostración](./images/5-v2.png)

Marque la casilla de verificación para modificar la configuración de persistencia. Seleccione **Más reciente** y el ámbito **Persona (ventana de informes)**, ya que solo nos importa el último número de móvil de esa persona. Si el cliente no rellena el móvil en visitas futuras, aún verá rellenado este valor.

![demostración](./images/6-v2.png)

| Nombre del componente a buscar | Nuevo nombre | Configuración de persistencia |
| ----------------- |-------------| --------------------| 
| phoneNumber | Número de teléfono | Más reciente, persona (ventana de informes) |

El siguiente componente es `web.webPageDetails.pageViews.value`.

En el menú del lado izquierdo, busque `web.webPageDetails.pageViews.value`. Arrastre y suelte esta métrica en el lienzo.

Cambie el nombre a **Vistas de página** en la **configuración de componentes**.

| Nombre del componente a buscar | Nuevo nombre | Configuración de atribución |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |         |

![demostración](./images/7-v2.png)

Para la configuración de atribución, lo dejaremos vacío.

Nota: La configuración de persistencia en las métricas también se puede cambiar en Analysis Workspace. En algunos casos, puede optar por configurarlo aquí para evitar que los usuarios empresariales tengan que pensar cuál es el mejor modelo de persistencia.

A continuación, tendrá que configurar muchos Dimension y métricas, tal como se indica en la tabla siguiente.

### DIMENSION


| Nombre del componente a buscar | Nuevo nombre | Configuración de persistencia |
| ----------------- |-------------| --------------------| 
| brandName | Nombre de marca | Más reciente, sesión |
| sensación de llamada | Sensación de llamada |          |
| ID de llamada | Tipo de interacción de llamada |          |
| callTopic | Tema de llamada | Más reciente, sesión |
| ecid | ECID | Más reciente, persona (ventana de informes) |
| email | ID de correo electrónico | Más reciente, persona (ventana de informes) |
| Tipo de pago | Tipo de pago |          |
| Método de adición de producto | Método de adición de producto | Más reciente, sesión |
| Tipo de evento | Tipo de evento |         |
| Nombre (productListItems.name) | Nombre de producto |         |
| SKU | SKU (sesión) | Más reciente, sesión |
| El ID de transacción | El ID de transacción |         |
| URL (web.webPageDetails.URL) | URL |         |
| Agente de usuario | Agente de usuario | Más reciente, sesión |
| nivel | Nivel de fidelización |          |
| puntos | Valor de duración del cliente |          |

### MÉTRICAS

| Nombre del componente a buscar | Nuevo nombre | Configuración de atribución |
| ----------------- |-------------| --------------------| 
| Cantidad | Cantidad |          |
| commerce.order.priceTotal | Ingresos |         |

La configuración debería tener este aspecto:

![demostración](./images/11-v2.png)

No olvides **guardar** tu vista de datos. Así que haga clic en **Guardar** ahora.

![demostración](./images/12-v2s.png)

## 4.3.4 Métricas calculadas

Aunque hemos organizado todos los componentes de la vista de datos, aún necesita adaptar algunos de ellos para que los usuarios empresariales estén listos para iniciar el análisis.

Si recuerda que no hemos introducido específicamente métricas como Agregar al carro de compras, Vista de producto o Compras en la Vista de datos.
Sin embargo, tenemos una dimensión llamada: **Tipo de evento**. Así que derivemos estos tipos de interacción creando 3 métricas calculadas.

Empecemos con la primera métrica: **Vistas del producto**.

En el lado izquierdo, busque **Tipo de evento** y seleccione la dimensión. A continuación, arrástrelo y suéltelo en el lienzo **Componentes incluidos**.

![demostración](./images/calcmetr1.png)

Haga clic para seleccionar la nueva métrica **Tipo de evento**.

![demostración](./images/calcmetr2.png)

Ahora cambie el nombre y la descripción del componente a los siguientes valores:

| Nombre del componente | Descripción del componente |
| ----------------- |-------------| 
| Vistas del producto | Vistas del producto |

![demostración](./images/calcmetr3.png)

Ahora contemos solamente **eventos de vistas del producto**. Para ello, desplácese hacia abajo en **Configuración de componentes** hasta que vea **Incluir valores de exclusión**. Asegúrese de habilitar la opción **Establecer valores de inclusión/exclusión**.

![demostración](./images/calcmetr4.png)

Como solo queremos contar **vistas del producto**, especifique **commerce.productViews** con los criterios.

![demostración](./images/calcmetr5.png)

La métrica calculada ya está lista.

A continuación, repite el mismo proceso para los eventos **Agregar al carro de compras** y **Comprar**.

### Añadir al carro

Primero arrastre y suelte la misma dimensión **Tipo de evento**.

![demostración](./images/calcmetr1.png)

Verá una ventana emergente que alerta de un campo duplicado, ya que estamos utilizando la misma variable. Haz clic en **Agregar de todos modos**:

![demostración](./images/calcmetr6.png)

Ahora, siga el mismo proceso que hemos seguido para las vistas de producto de la métrica:
- Cambie primero el nombre y la descripción.
- Finalmente, agregue **commerce.productListAdds** como criterios para contar solo Agregar al carro de compras

| Nombre | Descripción | Criterios |
| ----------------- |-------------| -------------|
| Añadir al carro | Añadir al carro | commerce.productListAdds |

![demostración](./images/calcmetr6a.png)

### Compras

Primero, arrastre y suelte la misma dimensión **Tipo de evento** que hicimos para las dos métricas anteriores.

![demostración](./images/calcmetr1.png)

Verá una ventana emergente que alerta de un campo duplicado, ya que estamos utilizando la misma variable. Haz clic en **Agregar de todos modos**:

![demostración](./images/calcmetr7.png)

Ahora, siga el mismo proceso que para las métricas Vistas del producto y Agregar al carro de compras:
- Cambie primero el nombre y la descripción.
- Finalmente, agregue **commerce.purchases** como criterio para contar solo las compras

| Nombre | Descripción | Criterios |
| ----------------- |-------------| -------------|
| Compras | Compras | commerce.purchases |

![demostración](./images/calcmetr7a.png)

La configuración final debería ser similar a esta. Haz clic en **Guardar y continuar**.

![demostración](./images/calcmetr8.png)

## 4.3.5 Configuración de vista de datos

Se le debe redirigir a esta pantalla:

![demostración](./images/8-v2.png)

En esta pestaña, puede modificar algunas configuraciones importantes para cambiar la forma en que se procesan los datos. Empecemos por establecer **Tiempo de espera de sesión** en 30 minutos. Gracias a la marca de tiempo de cada evento de experiencia, puede ampliar el concepto de sesión a todos los canales. Por ejemplo, ¿qué sucede si un cliente llama al centro de llamadas después de visitar el sitio web? Al usar los Tiempos de espera de sesión personalizados, tiene mucha flexibilidad para decidir qué es una sesión y cómo combinará los datos esa sesión.

![demostración](./images/ext8.png)

En esta pestaña puede modificar otras cosas como filtrar los datos mediante un segmento o filtro. No tendrá que hacer eso en este ejercicio.

![demostración](./images/10-v2.png)

Una vez finalizado, haga clic en **Guardar y finalizar**.

![demostración](./images/13-v2.png)

>[!NOTE]
>
>Puede volver a esta vista de datos posteriormente y cambiar la configuración y los componentes en cualquier momento. Los cambios afectarán a la forma en que se muestran los datos históricos.

Ahora puede continuar con la parte de visualización y análisis.

Paso siguiente: [4.4 Preparación de datos en el Customer Journey Analytics](./ex4.md)

[Volver al flujo de usuario 4](./uc4.md)

[Volver a todos los módulos](./../../overview.md)
