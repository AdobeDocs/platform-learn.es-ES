---
title: 1. Configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web
description: 'Fundamento: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 86da7132-cb06-4be3-b6b8-ea3ab937e6dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 1. Fundamento: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web

**Autor: [Matthew Joseph Woolley](https://www.linkedin.com/in/matthewjwoolley/), [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Este módulo básico le presenta la visión de recopilación de datos de Adobe y explica cómo obtener datos de un sitio web y una aplicación móvil en Adobe Experience Platform y otras aplicaciones a través de la recopilación de datos de Adobe Experience Platform, los SDK de Adobe Experience Platform y la red perimetral de Adobe Experience Platform. Este módulo presenta algunos conceptos y tecnologías que tienen un impacto fuera del ámbito de un tutorial técnico de Adobe Experience Platform. Debe quedar claro qué partes de estos ejercicios son fundamentales para el resto del tutorial completo, que le enseña más sobre Experience Edge y sus capacidades, y a dónde ir para obtener más información y tutoriales.

## Objetivos de aprendizaje

- Descubra cómo una marca utiliza la recopilación de datos de Adobe Experience Platform como su sistema Tag Management (TMS).
- Conozca los flujos de datos que utiliza una marca para introducir datos en sus productos de Adobe.
- Obtenga información sobre cómo enviar datos a Adobe Experience Platform y otros productos a través de Adobe Experience Platform Edge Network.
- Aprenda a crear elementos de datos y reglas que recopilen datos de web y móvil.
- Obtenga información sobre los eventos de seguimiento del SDK web y cómo depurar su contenido.
- Descubra qué es una capa de datos y qué Adobe recomienda al implementar una.
- Descubra cuáles son los pasos para implementar el SDK web desde cero.
- Conozca la diferencia entre una implementación web y una implementación móvil.

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a la recopilación de datos de Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acceso al sitio web de demostración

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem1.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--aepSandboxId--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[1.1 Explicación de la recopilación de datos de Adobe Experience Platform](./ex1.md)

En este ejercicio, explore la interfaz de usuario de la recopilación de datos de Adobe Experience Platform y conozca sus funcionalidades.

[1.2 Recopilación de datos del servidor, conjuntos de datos y redes perimetrales](./ex2.md)

En este ejercicio, aprenderá a reenviar datos a productos de Adobe en la interfaz de recopilación de datos de Adobe Experience Platform e investigar los flujos de datos utilizados por el sitio web de demostración.

[1.3 Introducción a la recopilación de datos de Adobe Experience Platform](./ex3.md)

En este ejercicio, aprenderá a configurar una extensión, crear elementos de datos y reglas y publicarlos en la web.

[1.4 Recopilación de datos web del lado del cliente](./ex4.md)

En este ejercicio, depure el SDK web que se ha instalado para comprender cómo funciona y qué datos se utilizarán en ejercicios futuros.

[1.5 Implementar Adobe Analytics y Adobe Audience Manager](./ex5.md)

En este ejercicio, consulte y utilice datos web recopilados con el SDK web en Adobe Analytics y Adobe Audience Manager.

[1.6 Implementar Adobe Target](./ex6.md)

En este ejercicio, configure una actividad en Adobe Target, implementada mediante el SDK web.

[Requisitos del esquema XDM 1.7 en Adobe Experience Platform](./ex7.md)

Para garantizar que el SDK web y alloy.js puedan introducir datos en Adobe Experience Platform, es necesario que una mezcla XDM específica forme parte del esquema XDM en Adobe Experience Platform.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
