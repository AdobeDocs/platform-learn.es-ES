---
title: Bootcamp - Customer Journey Analytics - De perspectivas a acción
description: Bootcamp - Customer Journey Analytics - De perspectivas a acción
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: e5c2ad88967d7f6a45d3a5cc09ca4c9bc9a62a08
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 4.6 De perspectivas a acciones

## Objetivos

- Obtenga información sobre cómo crear una audiencia basada en una vista recopilada en el Customer Journey Analytics
- Usar esta audiencia en Real-Time CDP y Adobe Journey Optimizer

## 4.6.1 Crear una audiencia y publicarla

En el proyecto, ha creado un filtro llamado **Sentimientos de llamada** y pudieron ver el número de usuarios que tuvieron sus llamadas al centro de llamadas clasificadas como **positive**. Ahora podrá crear un segmento con estos usuarios y activarlo en recorridos o canales de comunicación.

El primer paso es: En el panel creado en el último ejercicio, seleccione línea **1. Sentimiento de llamada - Positivo**, haga clic con el botón derecho y seleccione la **Crear audiencia a partir de una selección** opción:

![demostración](./images/aud1.png)

A continuación, asigne un nombre a la audiencia según el modelo **yourLastName - Llamada de audiencia CJA que se siente positiva**:

![demostración](./images/aud2.png)

Tenga en cuenta que es posible tener una vista previa de la audiencia que se está creando:

![demostración](./images/aud3.png)

Finalmente, haga clic en **Publicación**.

![demostración](./images/aud4.png)

## 4.6.2 Usar la audiencia como parte de un segmento

Vuelva a Adobe Experience Platform y vaya a **Segmentos > Examinar** y podrá ver el segmento creado en CJA listo y disponible para usar en sus activaciones y recorridos.

![demostración](./images/aud5.png)

Ahora vamos a usar este segmento en una activación de Facebook y en un recorrido de clientes.

## 4.6.3 Utilizar su segmento en Real-Time CDP en tiempo real

En Adobe Experience Platform, vaya a **Segmentos > Examinar** y busque la audiencia que ha creado en CJA:

![demostración](./images/aud6.png)

Haga clic en el segmento y, a continuación, haga clic en **Activar en destino**:

![demostración](./images/aud7.png)

Seleccione el destino denominado **bootcamp-facebook** y, a continuación, haga clic en **Siguiente**.

![demostración](./images/aud8.png)

Haga clic en **Siguiente** de nuevo.

![demostración](./images/aud9.png)

Seleccione el **Origen de la audiencia** y configúrela en **Directamente de los clientes**, haga clic en **Siguiente**.

![demostración](./images/aud10.png)

Haga clic en **Finalizar**.

![demostración](./images/aud11.png)

El segmento ahora está conectado a Audiencias personalizadas de Facebook. Ahora usemos el mismo segmento en Adobe Journey Optimizer.

## 4.6.4 Usar su segmento en Adobe Journey Optimizer

En Adobe Experience Platform, haga clic en **Journey Optimizer** y, a continuación, en el menú de la izquierda, haga clic en **Recorridos** y empiece a crear un recorrido haciendo clic en **Crear Recorrido**.

![demostración](./images/aud20.png)

![demostración](./images/aud21.png)

![demostración](./images/aud22.png)

A continuación, en el menú de la izquierda, debajo de **Eventos**, seleccione **Clasificación del segmento** y arrástrela al recorrido:

![demostración](./images/aud23.png)

En Segmento, haga clic en **Editar** para seleccionar un segmento:

![demostración](./images/aud24.png)

Seleccione la audiencia que creó anteriormente en CJA y haga clic en  **Guardar**.

![demostración](./images/aud25.png)

¡Listo! Desde aquí puede crear un recorrido para los clientes que cumplen los requisitos para este segmento.

[Volver al flujo de usuario 4](./uc4.md)

[Voltar para todos módulos](./../../overview.md)
