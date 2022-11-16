---
title: Activación de segmentos en el centro de eventos de Microsoft Azure
description: Activación de segmentos en el centro de eventos de Microsoft Azure
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73c2576d-0a69-4d56-a671-9ae1f75580b9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---

# 13. Real-Time CDP: Activación de segmentos en el centro de eventos de Microsoft Azure

**Autores: [Métricas de Marc](https://www.linkedin.com/in/marcmeewis/), [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, configurará un destino de Microsoft Azure EventHub como destino en tiempo real para CDP en tiempo real de Adobe Experience Platform. También configurará e implementará una función de Azure que se activará en tiempo real cada vez que Adobe Experience Platform envíe una carga útil de segmento a su destino de Azure EventHub. La función de Azure que va a almacenar en déclencheur mostrará el mecanismo de las funciones de activación de CDP en tiempo real de Adobe Experience Platform.

Como parte de este módulo, también obtendrá una comprensión de los déclencheur de CDP en tiempo real para proporcionar una carga útil a un destino especificado. También analizaremos el estado de una calificación de segmento y cómo se relaciona con la activación.

CDP en tiempo real de Adobe Experience Platform admite la activación de datos en destinos de almacenamiento en la nube de flujo continuo, lo que le permite exportar datos y eventos de audiencia en tiempo real a estos destinos en formato JSON. A continuación, puede describir la lógica empresarial además de estos eventos en los destinos

Los centros de eventos de Microsoft Azure son un servicio de ingesta de datos en tiempo real completamente administrado que es sencillo, fiable y escalable. Transfiera millones de eventos por segundo desde cualquier fuente para crear canalizaciones de datos dinámicas y responder inmediatamente a los desafíos del negocio.

## Objetivos de aprendizaje

- Familiarícese con los centros de eventos de Microsoft Azure
- Configuración de un destino RTCDP en Microsoft Azure Event Hub
- Comprenda cuándo se activa CDP en tiempo real y cómo se ve la carga útil de activación
- Configuración del código de Visual Studio para desarrollar, probar e implementar su proyecto de Azure
- Cree e implemente una función de Azure que consuma cualificaciones de segmentos entregadas en tiempo real por RTCDP

## Requisitos previos

- Acceso a [Adobe Experience Platform](https://experience.adobe.com/platform)
- Familiaridad con el entorno del sitio web de la demostración de AEP
- Definición, uso y activación de segmentos de flujo continuo en Adobe Experience Platform

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem18.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--module18sandbox--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[13.0 Configurar su entorno](./ex0.md)

En este ejercicio, configurará su entorno de Microsoft Azure.

[13.1 Configurar el entorno de Microsoft Azure EventHub](./ex1.md)

En este ejercicio configurará su entorno de Microsoft Azure EventHub.

[13.2 Configurar el destino del centro de eventos de Azure en Adobe Experience Platform](./ex2.md)

En este ejercicio, configurará su conexión de destino CDP en tiempo real que enviará segmentos en tiempo real a EventHub que configuró en el ejercicio anterior.

[13.3 Crear un segmento](./ex3.md)

En este ejercicio, creará un segmento de flujo continuo en Adobe Experience Platform

[13.4 Activar segmento](./ex4.md)

En este ejercicio, activará su segmento de flujo continuo en su destino de CDP EventHub en tiempo real.

[13.5 Crear su proyecto de Microsoft Azure](./ex5.md)

En este ejercicio creará una función de Azure que se activará en tiempo real cuando Adobe Experience Platform active las cualificaciones de segmentos al destino correspondiente de Azure Event Hub.

[13.6 Situación de extremo a extremo](./ex6.md)

En este punto, todo está configurado. Ahora puede navegar por su sitio web de demostración de AEP y obtener las cualificaciones de los segmentos que se entregan a su función de Déclencheur de Microsoft Azure EventHub.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
