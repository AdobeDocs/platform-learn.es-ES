---
title: 'CDP en tiempo real: cree un segmento y realice una acción.'
description: 'CDP en tiempo real: cree un segmento y realice una acción.'
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# 6. CDP en tiempo real: cree un segmento y tome medidas

**Autor: [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Alberto de Caro](https://www.linkedin.com/in/albertodecaro/), [Benedikt Wedenik](https://www.linkedin.com/in/benedikt-wedenik/)**

En este módulo, configurará un segmento de flujo continuo y lo activará en varios destinos.

## Objetivos de aprendizaje

- Aprenda a crear un segmento y habilitarlo para la transmisión por secuencias.
- Obtenga información sobre cómo configurar un destino publicitario mediante la interfaz de usuario de Adobe Experience Platform.
- Obtenga información sobre cómo conectar un segmento a un destino y activarlo.
- Obtenga información sobre cómo utilizar los segmentos de Adobe Experience Platform en Adobe Audience Manager y cómo utilizar los segmentos de Adobe Audience Manager en Adobe Experience Platform, gracias al uso compartido bidireccional de segmentos.

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a Adobe Target
- Acceso a AWS S3

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem11.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--module11sandbox--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[6.1 Crear un segmento](./ex1.md)

Obtenga información sobre cómo crear un segmento.

[6.2 Revise cómo configurar el destino DV360 mediante destinos](./ex2.md)

Obtenga información sobre cómo configurar un destino publicitario mediante la interfaz de usuario de Real-Time CDP.

[6.3 Acción: enviar el segmento a DV360](./ex3.md)

Conecte el segmento que ha creado en el ejercicio 6.1 al DV360 de destino.

[6.4 Acción: enviar el segmento a un destino S3](./ex4.md)

Utilice el segmento que ha creado en el ejercicio 6.1 y envíelo a un destino S3, que normalmente se utiliza para los destinos de marketing por correo electrónico.

[6.5 Acción: enviar el segmento a Adobe Target](./ex5.md)

Utilice el segmento que ha creado en el ejercicio 6.1 para configurar una actividad de segmentación de experiencias en Adobe Target.

[6.6 Audiencias externas](./ex6.md)

Importar audiencias desde un sistema de origen externo a Adobe Experience Platform.

[SDK de destinos 6.7](./ex7.md)

Configure su propio destino mediante el SDK de Destinations.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
