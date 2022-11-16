---
title: Servicios inteligentes
description: Servicios inteligentes
kt: 5342
audience: Data Engineer, Data Architect, Data Scientist
doc-type: tutorial
activity: develop
exl-id: 99b56722-95bf-4c51-b4d6-8b5a8e5fd936
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 5. Servicios inteligentes

**Autores: [Diptiman Badajena](https://www.linkedin.com/in/diptiman-badajena-1b178019/), [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, aprenderá a configurar, configurar y utilizar los servicios inteligentes de Adobe Experience Platform.

## Objetivos de aprendizaje

- Familiarícese con Adobe Experience Platform
- Configuración del esquema/conjunto de datos para su uso con servicios inteligentes
- Crear una nueva instancia de Customer AI
- Panel de valoración y segmentación

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem5.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--module10sandbox--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[5.1 AI del cliente: preparación de datos (ingesta)](./ex1.md)

Los datos del cliente se incorporan y transforman con el Experience Data Model (XDM) en Adobe Experience Platform. Específicamente, todos los conjuntos de datos que se utilizan en Servicios inteligentes deben cumplir el esquema XDM de Consumer ExperienceEvent (CEE).

[5.2 Customer AI: crear una nueva instancia (configurar)](./ex2.md)

El analista de marketing configura las predicciones deseadas especificando reglas comerciales e identificando datos relevantes. Después de configurar el modelo, programe las ejecuciones y revise las puntuaciones.

[5.3 AI del cliente: panel de puntuación y segmentación (Predecir y tomar medidas)](./ex3.md)

Una vez que los modelos han terminado la formación y la puntuación, las puntuaciones se vuelven a escribir en Platform. Puede decidir qué acciones realizar con las predicciones, como definir segmentos, crear tableros personalizados, etc.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
