---
title: Bootcamp - Customer Journey Analytics - De las perspectivas a la acción
description: Bootcamp - Customer Journey Analytics - De las perspectivas a la acción
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 7a38a0a4-46e4-41f2-9a75-316dfde7128f
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 4.6 De la información a la acción

## Metas

- Obtenga información sobre cómo crear una audiencia basada en una vista recopilada en Customer Journey Analytics
- Utilice esta audiencia en Real-Time CDP y Adobe Journey Optimizer

## 4.6.1 Crear una audiencia y publicarla

En su proyecto, creó un filtro llamado **Llamadas** y pudo ver el número de usuarios que tuvieron sus llamadas al centro de llamadas clasificadas como **positivas**. Ahora podrá crear un segmento con estos usuarios y activarlos en recorridos o canales de comunicación.

El primer paso es: en el panel creado en el último ejercicio, seleccione la línea **1. Sensación de llamada - Positiva**, haga clic con el botón derecho y seleccione la opción **Crear audiencia a partir de la selección**:

![demostración](./images/aud1.png)

A continuación, asigne un nombre a la audiencia siguiendo el modelo **yourLastName - CJA audience call sintiéndose positivo**:

![demostración](./images/aud2.png)

Tenga en cuenta que es posible tener una previsualización de la audiencia que se está creando:

![demostración](./images/aud3.png)

Finalmente, haga clic en **Publish**.

![demostración](./images/aud4.png)

## 4.6.2 Usar la audiencia como parte de un segmento

Vuelva a Adobe Experience Platform, vaya a **Segmentos > Examinar** y podrá ver el segmento creado en CJA listo y disponible para usar en sus activaciones y recorridos.

![demostración](./images/aud5.png)

Ahora vamos a utilizar este segmento en una activación de Facebook y en un recorrido del cliente.

## 4.6.3 Uso del segmento en Real-Time CDP en tiempo real

En Adobe Experience Platform, vaya a **Segmentos > Examinar** y busque la audiencia que ha creado en CJA:

![demostración](./images/aud6.png)

Haga clic en el segmento y, a continuación, en **Activar en destino**:

![demostración](./images/aud7.png)

Seleccione el destino **bootcamp-facebook** y haga clic en **Siguiente**.

![demostración](./images/aud8.png)

Vuelva a hacer clic en **Siguiente**.

![demostración](./images/aud9.png)

Seleccione la opción **Origen de la audiencia** y configúrela en **Directamente de los clientes**; a continuación, haga clic en **Siguiente**.

![demostración](./images/aud10.png)

Haga clic en **Finalizar**.

![demostración](./images/aud11.png)

El segmento ahora está conectado a las audiencias personalizadas de Facebook. Ahora usemos ese mismo segmento en Adobe Journey Optimizer.

## 4.6.4 Uso del segmento en Adobe Journey Optimizer

En Adobe Experience Platform, haz clic en **Journey Optimizer** y, a continuación, en el menú del lado izquierdo, haz clic en **Recorridos** y comienza a crear un recorrido haciendo clic en **Crear Recorrido**.

![demostración](./images/aud20.png)

![demostración](./images/aud21.png)

![demostración](./images/aud22.png)

A continuación, en el menú de la izquierda, en **Eventos**, seleccione **Calificación de segmentos** y arrástrela al recorrido:

![demostración](./images/aud23.png)

En Segmento, haga clic en **Editar** para seleccionar un segmento:

![demostración](./images/aud24.png)

Seleccione la audiencia que creó anteriormente en CJA y haga clic en **Guardar**.

![demostración](./images/aud25.png)

¡Listo! Desde aquí puede crear un recorrido para los clientes que cumplen los requisitos de este segmento.

[Volver al flujo de usuario 4](./uc4.md)

[Voltar para todos los tiempos](./../../overview.md)
