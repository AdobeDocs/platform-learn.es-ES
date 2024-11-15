---
title: Activación de segmentos en Microsoft Azure Event Hub
description: Activación de segmentos en Microsoft Azure Event Hub
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 2.4 Real-Time CDP: Activación de segmentos en Microsoft Azure Event Hub

**Autores: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, configurará un destino de Microsoft Azure EventHub como un destino en tiempo real para Adobe Experience Platform Real-time CDP. También configurará e implementará una función de Azure que se activará en tiempo real cada vez que Adobe Experience Platform envíe una carga útil de segmento a su destino de Azure EventHub. La función de Azure que almacenará en déclencheur mostrará el mecanismo de las capacidades de activación de Adobe Experience Platform Real-time CDP.

Como parte de este módulo, también comprenderá qué déclencheur necesita CDP en tiempo real para entregar una carga útil a un destino especificado. También analizaremos el estado de la calificación de un segmento y cómo se relaciona con la activación.

Adobe Experience Platform Real-time CDP admite la activación de datos en destinos de almacenamiento de nube de streaming, lo que le permite exportar datos y eventos de audiencia en tiempo real a estos destinos en formato JSON. A continuación, puede describir la lógica empresarial además de estos eventos en sus destinos

Microsoft Azure Event Hubs es un servicio de ingesta de datos en tiempo real totalmente administrado que es sencillo, fiable y escalable. Transmita millones de eventos por segundo desde cualquier fuente para crear canalizaciones de datos dinámicas y responder inmediatamente a los desafíos empresariales.

## Objetivos de aprendizaje

- Familiarícese con los centros de eventos de Microsoft Azure
- Configure un destino RTCDP en su Microsoft Azure Event Hub
- Comprenda cuándo se activa Real-time CDP y cómo es la carga útil de activación
- Configure Visual Studio Code para desarrollar, probar e implementar su proyecto de Azure
- Cree e implemente una función de Azure que consuma segmentos y cualificaciones entregados en tiempo real por RTCDP

## Requisitos previos

- Acceso a [Adobe Experience Platform](https://experience.adobe.com/platform)
- Familiaridad con el entorno del sitio web de demostración de AEP
- Obtenga información sobre cómo definir, utilizar y activar segmentos de streaming en Adobe Experience Platform

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se hace referencia en [Instalar la extensión de Chrome para la documentación del Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Ejercicios

[2.4.0 Configuración del entorno](./ex0.md)

En este ejercicio, configurará el entorno de Microsoft Azure.

[2.4.1 Configuración del entorno de Microsoft Azure EventHub](./ex1.md)

En este ejercicio configurará el entorno de Microsoft Azure EventHub.

[2.4.2 Configuración del destino de Azure Event Hub en Adobe Experience Platform](./ex2.md)

En este ejercicio configurará la conexión de destino de Real-time CDP que enviará segmentos en tiempo real al EventHub que ha configurado en el ejercicio anterior.

[2.4.3 Crear un segmento](./ex3.md)

En este ejercicio creará un segmento de flujo continuo en Adobe Experience Platform

[2.4.4 Activar segmento](./ex4.md)

En este ejercicio, activará el segmento de streaming en su destino de Real-time CDP EventHub.

[2.4.5 Crear su proyecto de Microsoft Azure](./ex5.md)

En este ejercicio creará una función de Azure que se activará en tiempo real cuando Adobe Experience Platform active las cualificaciones de segmento en el destino correspondiente de Azure Event Hub.

[2.4.6 Escenario de extremo a extremo](./ex6.md)

En este punto, todo está configurado. Ahora puede navegar por el sitio web de demostración de AEP y recibir las cualificaciones de los segmentos en su función de Déclencheur de Microsoft Azure EventHub.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](../../../overview.md)
