---
title: 'Base: ingesta de datos'
description: 'Base: ingesta de datos'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# 2. Base: ingesta de datos

**Autor: [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, el objetivo es aprender todo sobre la ingesta de datos. Aprenderá sobre la ingesta de datos en Streaming y Batch. Implementará la ingesta de datos de flujo continuo mediante Launch, de modo que el comportamiento del cliente en el sitio web de Hands-On Lab se transmita a Adobe Experience Platform en tiempo real. Aprenderá sobre la ingesta de datos por lotes utilizando un flujo de trabajo de Adobe Experience Platform para tomar un archivo CSV, asignarlo a un esquema XDM y, a continuación, ingerirlo en Adobe Experience Platform.

## Objetivos de aprendizaje

- Obtenga información sobre cómo crear un esquema XDM en Adobe Experience Platform
- Obtenga información sobre cómo crear conjuntos de datos en Adobe Experience Platform
- Obtenga información sobre cómo crear un extremo de flujo continuo y configurar la extensión de Adobe Experience Platform en Launch
- Obtenga información sobre cómo crear reglas en Launch para transmitir datos a Adobe Experience Platform
- Aprenda a integrar Adobe Experience Platform Launch en una página web
- Aprenda a utilizar un flujo de trabajo de Adobe Experience Platform para ingerir un archivo CSV en Adobe Experience Platform

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a Adobe Experience Platform Launch: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acceso a [https://public.aepdemo.net](https://public.aepdemo.net)
- Acceso a Postman

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem2.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--module2sandbox--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[2.1 Explorar el sitio web](./ex1.md)

En este ejercicio, explorará el sitio web que utilizará como parte de esta habilitación.

[2.2 Configurar esquemas y definir identificadores](./ex2.md)

En este ejercicio, debe configurar los esquemas XDM necesarios para capturar la información de perfil y el comportamiento del cliente. En cada esquema XDM, también tendrá que configurar un identificador principal para vincular toda la información.

[2.3 Configurar conjuntos de datos](./ex3.md)

En este ejercicio, recuperará los conjuntos de datos necesarios para capturar y almacenar información de perfil y comportamiento del cliente.

[2.4 Ingesta de datos de fuentes sin conexión](./ex4.md)

En este ejercicio, accederá al sitio web y a la aplicación móvil y se comportará como un cliente, transmitiendo datos a Platform.

[2.5 Zona de aterrizaje de datos](./ex5.md)

Configure el conector de origen de la zona de aterrizaje de datos con el almacenamiento de Azure Blob.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
