---
title: Foundation - Ingesta de datos
description: Foundation - Ingesta de datos
kt: 5342
doc-type: tutorial
exl-id: 0fa38179-637b-4dda-a4e4-754a4cdd61a8
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# 1.2 Ingesta de datos

En este módulo, el objetivo es aprender todo acerca de la ingesta de datos. Aprenderá a utilizar la ingesta de datos en streaming y por lotes. Implementará la ingesta de datos de flujo continuo mediante Launch, de modo que el comportamiento del cliente en el sitio web del laboratorio práctico se transmita a Adobe Experience Platform en tiempo real. Aprenderá a utilizar la ingesta de datos por lotes mediante un flujo de trabajo de Adobe Experience Platform para tomar un archivo CSV, asignarlo a un esquema XDM y, a continuación, ingerirlo en Adobe Experience Platform.

## Objetivos de aprendizaje

- Obtenga información sobre cómo crear un esquema XDM en Adobe Experience Platform
- Obtenga información sobre cómo crear conjuntos de datos en Adobe Experience Platform
- Obtenga información sobre cómo crear un extremo de flujo continuo y configurar la extensión de Adobe Experience Platform en Launch
- Obtenga información sobre cómo crear reglas en Launch para transmitir datos a Adobe Experience Platform
- Aprenda a integrar Adobe Experience Platform Launch en una página web
- Aprenda a utilizar un flujo de trabajo de Adobe Experience Platform para introducir un archivo CSV en Adobe Experience Platform

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a Adobe Experience Platform Launch: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acceso a Postman

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se hace referencia en [Instalar la extensión de Chrome para la documentación de Experience League](../../../getting-started/gettingstarted/ex1.md)

## Ejercicios

[1.2.1 Explorar el sitio web](./ex1.md)

En este ejercicio, explorará el sitio web que utilizará como parte de esta habilitación.

[1.2.2 Configuración de esquemas y definición de identificadores](./ex2.md)

En este ejercicio, configurará el esquema XDM necesario para capturar información de perfil y comportamiento del cliente. En cada esquema XDM, también debe configurar un identificador principal para vincular toda la información a.

[1.2.3 Configuración de conjuntos de datos](./ex3.md)

En este ejercicio, recuperará los conjuntos de datos necesarios para capturar y almacenar información de perfil y comportamiento del cliente.

[1.2.4 Ingesta de datos desde fuentes sin conexión](./ex4.md)

En este ejercicio, accederá al sitio web y a la aplicación móvil y se comportará como un cliente que transmite datos a Platform.

[1.2.5 Zona de aterrizaje de datos](./ex5.md)

Configure el conector Source de la zona de aterrizaje de datos con el almacenamiento del blob de Azure.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

![Perspectivas técnicas](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](./../../../../overview.md)
