---
title: 'Planning: Migrar Target de at.js 2.x al SDK web'
description: Obtenga información sobre cómo planificar la implementación de Adobe Target desde at.js 2.x al SDK web de Adobe Experience Platform.
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Planifique la migración de at.js al SDK web de Platform

Antes de actualizar al SDK web de Platform en el sitio, debe evaluar la implementación actual.

## Evaluar la implementación actual de at.js

El primer paso para una migración exitosa es tener una comprensión firme de su implementación actual de at.js Target. Hay funciones, características y código personalizado que puede utilizar que requieren actualizaciones. Tenga en cuenta lo siguiente al evaluar:

### ¿Qué funciones se admiten?

El SDK web de Platform se encuentra en continuo desarrollo activo y las funciones y mejoras se añaden regularmente. A medida que evalúe su implementación actual de at.js, consulte la página [casos de uso admitidos](https://github.com/orgs/adobe/projects/18/views/1) para obtener la información más reciente.

### ¿Qué funciones utiliza hoy en día?

El SDK web de Platform es una nueva biblioteca que consolida todas las soluciones de Adobe para los sitios web en un único SDK. Esto permite una integración más estrecha y permite nuevas funciones exclusivas de Adobe Experience Platform. Sin embargo, esto también significa que las funciones de at.js no son compatibles con versiones anteriores del SDK web de Platform. A medida que evalúe la implementación actual, tenga en cuenta lo siguiente:

- Funciones de at.js como `getOffer()` y `applyOffer()`
- Modificaciones en la configuración global de Target
- Integración con Adobe Analytics
- Uso de un script de mitigación de parpadeo
- Uso de tokens de respuesta
- Uso de parámetros de mbox, perfil y entidad
- Código personalizado exclusivo de la implementación

### ¿Qué enfoque de migración adoptará?

Una vez que haya revisado la implementación de at.js, debe determinar un método de migración. Hay dos opciones:

- Migrar todas las aplicaciones de Adobe a la vez en todo el sitio
- Migrar página por página (Migrate on a page)

Dado que el SDK web de Platform combina y habilita varias aplicaciones de Adobe, debe coordinar la migración de Target de otras aplicaciones de Adobe como Analytics y Audience Manager. Todas las bibliotecas de Adobe de una página determinada deben migrarse al mismo tiempo. No se admite una implementación mixta del SDK web de Platform para Target y AppMeasurement para Analytics en una página concreta. Sin embargo, se admite una implementación mixta en diferentes páginas, por ejemplo, el SDK web de Platform en la página A y at.js con AppMeasurement en la página B.

A medida que migre, debe planificar el seguimiento del proceso de su empresa para probar y lanzar nuevo código y utilizar elementos como entornos de desarrollo, control de calidad y ensayo antes de realizar el lanzamiento en producción.

>[!CAUTION]
>
>Las ofertas de redireccionamiento no son compatibles con las migraciones página por página si se redirige desde una página con una biblioteca a una página con una biblioteca diferente


A continuación, revise la [comparación detallada de at.js con el SDK web de Platform](detailed-comparison.md) para comprender mejor las diferencias técnicas e identificar las áreas que requieren un enfoque adicional.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
