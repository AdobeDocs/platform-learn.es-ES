---
title: 'Experience Decisioning: Experience Decisioning 101'
description: 'Experience Decisioning: Experience Decisioning 101'
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 3.7.1 Experience Decisioning 101

## Terminología de 3.7.1.1

Para comprender mejor Experience Decisioning, le recomendamos encarecidamente que lea la [descripción general](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=es) sobre cómo funciona el servicio de aplicaciones de Offer Decisioning con Adobe Experience Platform.

Al trabajar con Offer Decisioning, debe comprender los siguientes conceptos:

| Término | Explicación |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Oferta** | Una oferta es un mensaje de marketing que puede tener reglas asociadas que especifican quién puede ver la oferta. Una oferta tiene un estado: borrador, aprobado o archivado. |
| **Ubicación** | La combinación de ubicación (o tipo de canal) y contexto (o tipo de contenido) en el que aparece una oferta para un usuario final. En la práctica, es la combinación de texto, HTML, imagen, JSON en canales móviles, web, sociales, de mensajería instantánea y no digitales. |
| **Regla** | La lógica que define y controla la idoneidad de los usuarios finales para una oferta. |
| **Oferta personalizada** | Un mensaje de marketing personalizable basado en reglas de elegibilidad y restricciones. |
| **Oferta de reserva** | La oferta predeterminada se muestra cuando un usuario final no cumple los requisitos para ninguna de las ofertas de la colección utilizada. |
| **Límite** | Se utiliza en una definición de oferta para definir cuántas veces se puede presentar una oferta en total y a un usuario específico. |
| **Prioridad** | Level para determinar la clasificación de prioridad a partir de un conjunto de resultados de ofertas. |
| **Colección** | Se utiliza para filtrar un subconjunto de ofertas de la lista de ofertas personalizadas para acelerar el proceso de toma de decisiones de oferta. |
| **Decisión** | Una combinación de un conjunto de ofertas, ubicación y perfil para la que el experto en marketing desea que el motor de decisión proporcione la mejor oferta. |
| **AEM Assets Essentials** | Una experiencia universal y centralizada para almacenar, buscar y seleccionar recursos en las soluciones de Adobe Experience Cloud y Adobe Experience Platform. |

{style="table-layout:auto"}

## 3.7.1.2 Experience Decisioning

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

En el siguiente ejercicio, configurará sus propias ofertas y decisiones.

## Pasos siguientes

Vaya a [3.7.2 Configurar sus ofertas y decisión](./ex2.md){target="_blank"}

Volver a [Experience Decisioning](ajo-decisioning.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
