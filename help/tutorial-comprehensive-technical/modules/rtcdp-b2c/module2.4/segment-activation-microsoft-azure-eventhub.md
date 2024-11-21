---
title: Audience Activation de Microsoft Azure Event Hub
description: Audience Activation de Microsoft Azure Event Hub
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 2.4 Real-Time CDP: Audience Activation de Microsoft Azure Event Hub

En este módulo, configurará un destino de Microsoft Azure EventHub como un destino en tiempo real para Adobe Experience Platform Real-time CDP. También configurará e implementará una función de Azure que se activará en tiempo real cada vez que Adobe Experience Platform envíe una carga útil de audiencia a su destino de Azure EventHub. La función de Azure que almacenará en déclencheur mostrará el mecanismo de las capacidades de activación de Adobe Experience Platform Real-time CDP.

Como parte de este módulo, también comprenderá qué déclencheur necesita CDP en tiempo real para entregar una carga útil a un destino especificado. También analizaremos el estado de una calificación de audiencia y cómo se relaciona con la activación.

Adobe Experience Platform Real-time CDP admite la activación de datos en destinos de almacenamiento de nube de streaming, lo que le permite exportar datos y eventos de audiencia en tiempo real a estos destinos en formato JSON. A continuación, puede describir la lógica empresarial además de estos eventos en sus destinos

Microsoft Azure Event Hubs es un servicio de ingesta de datos en tiempo real totalmente administrado que es sencillo, fiable y escalable. Transmita millones de eventos por segundo desde cualquier fuente para crear canalizaciones de datos dinámicas y responder inmediatamente a los desafíos empresariales.

## Objetivos de aprendizaje

- Familiarícese con los centros de eventos de Microsoft Azure
- Configure un destino RTCDP en su Microsoft Azure Event Hub
- Comprenda cuándo se activa Real-time CDP y cómo es la carga útil de activación
- Configure Visual Studio Code para desarrollar, probar e implementar su proyecto de Azure
- Cree e implemente una función de Azure que consuma cualificaciones de audiencia suministradas en tiempo real por RTCDP

## Requisitos previos

- Acceso a [Adobe Experience Platform](https://experience.adobe.com/platform)
- Obtenga información sobre cómo definir, utilizar y activar audiencias en Adobe Experience Platform

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se hace referencia en [Instalar la extensión de Chrome para la documentación del Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Ejercicios

[2.4.1 Configuración del entorno](./ex1.md)

En este ejercicio, configurará el entorno de Microsoft Azure.

[2.4.2 Configuración del entorno de Microsoft Azure EventHub](./ex2.md)

En este ejercicio configurará el entorno de Microsoft Azure EventHub.

[2.4.3 Configuración del destino de Azure Event Hub en Adobe Experience Platform](./ex3.md)

En este ejercicio configurará la conexión de destino de Real-time CDP que entregará audiencias en tiempo real a la instancia de Event Hub que configuró en el ejercicio anterior.

[2.4.4 Crear una audiencia](./ex4.md)

En este ejercicio creará una audiencia en Adobe Experience Platform

[2.4.5 Activar la audiencia](./ex5.md)

En este ejercicio, activará la audiencia en el destino de EventHub.

[2.4.6 Crear su proyecto de Microsoft Azure](./ex6.md)

En este ejercicio creará una función de Azure que se activará en tiempo real cuando Adobe Experience Platform envíe cualificaciones de audiencia al destino correspondiente de Azure Event Hub.

[2.4.7 Escenario de extremo a extremo](./ex7.md)

En este punto, todo está configurado. Ahora puede navegar por el sitio web de demostración y obtener las cualificaciones de audiencia que se entregan a la función de Déclencheur de Microsoft Azure Event Hub.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](../../../overview.md)
