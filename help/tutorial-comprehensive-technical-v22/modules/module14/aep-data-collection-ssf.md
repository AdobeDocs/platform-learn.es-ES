---
title: Recopilación de datos de Adobe Experience Platform y reenvío de servidor en tiempo real
description: En este módulo, utilizará los conjuntos de datos, esquemas y la propiedad del servidor de recopilación de datos de Adobe Experience Platform configurados anteriormente para recopilar datos y, a continuación, reenviar esos datos del lado del servidor a un punto final de su elección.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c157ca52-c84f-4398-a658-2b6067e41707
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 14. Conexiones de Real-Time CDP: Reenvío de eventos

**Autor: [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Clement Delalande](https://www.linkedin.com/in/clement-delalande/)**

En este módulo, utilizará los conjuntos de datos, esquemas y la propiedad del cliente de recopilación de datos de Adobe Experience Platform configurados anteriormente para recopilar datos y, a continuación, reenviar esos datos del lado del servidor a un punto final de su elección.

En este módulo, debe:

- Crear una propiedad de Adobe Experience Platform Data Collection Server
- Instalación y uso de la extensión del conector de Adobe Cloud en la recopilación de datos de Adobe Experience Platform
- Crear un extremo de función de Google y transmitir datos a él
- Crear un extremo de AWS y transmitir datos a él

Vea este vídeo para comprender el valor, el recorrido del cliente y el proceso de configuración:

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## Objetivos de aprendizaje

- Familiarícese con las propiedades del servidor de recopilación de datos de Adobe Experience Platform y la nueva extensión del conector de Adobe Cloud
- Obtenga información sobre cómo reutilizar datos del SDK web de Adobe Experience Platform en soluciones de terceros como Google y AWS
- Comprenda la arquitectura subyacente a la recopilación de datos de Adobe Experience Platform y al reenvío del lado del servidor.

## Requisitos previos

- Acceso a la recopilación de datos de Adobe Experience Platform y Adobe Experience Platform
- Explicación de los conjuntos de datos de Adobe Experience Platform y XDM

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem21.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--aepSandboxId--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[14.1 Crear una propiedad de reenvío de eventos de recopilación de datos](./ex1.md)

En este ejercicio, debe crear la propiedad Adobe Experience Platform Data Collection Event Forwarding .

[14.2 Actualice el almacén de datos para que los datos estén disponibles en la propiedad Reenvío de eventos de recopilación de datos](./ex2.md)

En este ejercicio, actualizará el almacén de datos existente para que los datos recopilados por la propiedad del cliente de recopilación de datos de Adobe Experience Platform estén disponibles para la propiedad del servidor de recopilación de datos de Adobe Experience Platform.

[14.3 Crear y configurar un vínculo web personalizado](./ex3.md)

En este ejercicio, creará y configurará un enlace web personalizado y comenzará a reenviar los datos recopilados por el SDK web a ese vínculo web personalizado.

[14.4 Crear y configurar una función de nube de Google](./ex4.md)

En este ejercicio, creará y configurará una función de Google Cloud y comenzará a reenviar datos recopilados por el SDK web a Google.

[14.5 Avanzar hacia el ecosistema de AWS](./ex5.md)

En este ejercicio, puede configurar el entorno de AWS mediante la puerta de enlace de la API de AWS, AWS Kinesis, AWS Firefox y AWS S3, tras lo cual comenzará a reenviar los datos de evento recopilados por el SDK web.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
