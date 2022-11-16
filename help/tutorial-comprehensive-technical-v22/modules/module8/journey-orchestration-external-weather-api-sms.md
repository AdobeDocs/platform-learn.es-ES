---
title: 'Adobe Journey Optimizer: API de meteorología externa, acción de SMS y más'
description: 'Adobe Journey Optimizer: API de meteorología externa, acción de SMS y más'
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# 8. Adobe Journey Optimizer: Fuentes de datos externas y acciones personalizadas

**Autor: [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, utilizará Adobe Journey Optimizer para escuchar el comportamiento de los clientes, tanto en línea como sin conexión, y responder a él de forma inteligente, contextual y en tiempo real. Ya ha tenido una experiencia práctica inicial con Adobe Journey Optimizer en el módulo 6. En este ejercicio, profundizará un poco y explorará un caso de uso más avanzado mediante el cual las fuentes de datos externas se utilizan como parte de un recorrido.

## Objetivos de aprendizaje

- Obtenga información sobre cómo crear eventos, fuentes de datos externas y recorridos en Adobe Journey Optimizer
- Aprenda a consumir información meteorológica de la API de Tiempo Abierto
- Aprenda a utilizar destinos de acción personalizados como Twilio y Slack de Adobe Journey Optimizer

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a Adobe Journey Optimizer
- Acceso a la API de clima abierto

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem12.png)

## Contexto empresarial

Como marca, ha invertido mucho en personalizar experiencias en línea. Ahora, desea ser tan contextual y relevante para las experiencias sin conexión.
En este módulo, utilizará la presencia de un cliente en una tienda sin conexión para luego ofrecer una experiencia personalizada dentro de la tienda mostrando contenido relevante para ese cliente en nuestras pantallas de la tienda y, al mismo tiempo, queremos enviar un mensaje push o SMS personalizado a ese mismo cliente, todo en tiempo real.
Como marca, también comprende que el contexto afecta en gran medida al interés de un cliente, por lo que desea incorporar la información meteorológica actual de la ubicación de ese cliente para decidir qué contenido o promoción mostrar.

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--aepSandboxId--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[8.1 Definir un evento](./ex1.md)

Obtenga información sobre cómo definir un evento personalizado con Adobe Journey Optimizer.

[8.2 Definir una fuente de datos externa](./ex2.md)

Obtenga información sobre cómo configurar una fuente de datos externa mediante Adobe Journey Optimizer.

[8.3 Definir una acción personalizada](./ex3.md)

Obtenga información sobre cómo definir una acción externa mediante Adobe Journey Optimizer.

[8.4 Crear su recorrido y mensajes](./ex4.md)

Combine eventos, fuentes de datos y acciones en un recorrido inteligente y contextual.

[8.5 Déclencheur de su recorrido](./ex5.md)

Déclencheur el recorrido específico.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
