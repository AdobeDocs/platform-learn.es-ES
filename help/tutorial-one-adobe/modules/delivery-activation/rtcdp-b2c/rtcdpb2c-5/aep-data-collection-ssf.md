---
title: Recopilación de datos de Adobe Experience Platform y reenvío del lado del servidor en tiempo real
description: En este módulo, se utilizarán los conjuntos de datos, esquemas y la propiedad del servidor de recopilación de datos de Adobe Experience Platform configurados previamente para recopilar datos y, a continuación, reenviar esos datos del lado del servidor a un extremo de su elección.
kt: 5342
doc-type: tutorial
exl-id: dbf5e995-9c2e-4f72-b336-e942cb22cde5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# Conexiones Real-Time CDP 2.5: Reenvío de eventos

En este módulo, se utilizarán los conjuntos de datos, esquemas y la propiedad del cliente de recopilación de datos de Adobe Experience Platform configurados previamente para recopilar datos y, a continuación, reenviar esos datos del lado del servidor a un extremo de su elección.

En este módulo, deberá hacer lo siguiente:

- Crear una propiedad de servidor de recopilación de datos de Adobe Experience Platform
- Instalación y uso de la extensión Adobe Cloud Connector en la recopilación de datos de Adobe Experience Platform
- Crear un extremo de función de Google y transmitir datos a él
- Crear un extremo de AWS y transmitir datos a él

## Objetivos de aprendizaje

- Familiarícese con las propiedades del servidor de recopilación de datos de Adobe Experience Platform y con la nueva extensión del conector de Adobe Cloud
- Aprenda a reutilizar datos de Adobe Experience Platform Web SDK en soluciones de terceros como Google y AWS
- Comprenda la arquitectura detrás de la recopilación de datos de Adobe Experience Platform y el reenvío del lado del servidor.

## Requisitos previos

- Acceso a la recopilación de datos de Adobe Experience Platform y Adobe Experience Platform
- Comprensión de los conjuntos de datos de Adobe Experience Platform y XDM

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se hace referencia en [Instalar la extensión de Chrome para la documentación de Experience League](../../../getting-started/gettingstarted/ex1.md)

## Ejercicios

[2.5.1 Crear una propiedad de reenvío de eventos de recopilación de datos](./ex1.md)

En este ejercicio, creará su propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform.

[2.5.2 Actualizar el flujo de datos para que los datos estén disponibles para la propiedad de reenvío de eventos de recopilación de datos](./ex2.md)

En este ejercicio, actualizará el flujo de datos existente para que los datos recopilados por la propiedad de cliente de recopilación de datos de Adobe Experience Platform estén disponibles para la propiedad de servidor de recopilación de datos de Adobe Experience Platform.

[2.5.3 Crear y configurar un webhook personalizado](./ex3.md)

En este ejercicio, creará y configurará un webhook personalizado y empezará a reenviar los datos recopilados por Web SDK a dicho webhook personalizado.

[2.5.4 Reenviar eventos a GCP Pub/Sub](./ex4.md)

En este ejercicio, creará y configurará una función de nube de Google y empezará a reenviar los datos recopilados por Web SDK a Google.

[2.5.5 Reenviar eventos a AWS Kinesis y AWS S3](./ex5.md)

En este ejercicio, configurará el entorno de AWS mediante AWS IAM, AWS Kinesis, AWS Firefox y AWS S3, después de lo cual empezará a reenviar los datos de evento recopilados por Web SDK.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

![Perspectivas técnicas](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](./../../../../overview.md)
