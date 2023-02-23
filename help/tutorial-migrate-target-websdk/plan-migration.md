---
title: Planificación | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo planificar la implementación de Adobe Target desde at.js 2.x al SDK web de Adobe Experience Platform.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Planificar la migración de at.js al SDK web de plataforma

Antes de actualizar al SDK web de Platform en su sitio, debe evaluar la implementación actual.

## Evaluar la implementación actual de at.js

El primer paso para una migración exitosa es tener una comprensión sólida de su implementación actual de at.js Target. Hay características, funciones y código personalizado que puede utilizar que requieren actualizaciones. Tenga en cuenta lo siguiente al evaluar:

### ¿Qué funciones se admiten?

El SDK web de la plataforma se encuentra en constante desarrollo activo y las funciones y mejoras se añaden regularmente. Al evaluar la implementación actual de at.js, consulte [casos de uso admitidos](https://github.com/orgs/adobe/projects/18/views/1) para obtener la información más reciente.

### ¿Qué funciones utiliza hoy en día?

El SDK web de plataforma es una nueva biblioteca que consolida todas las soluciones de Adobe para los sitios web en un único SDK. Esto permite una integración más estricta y permite nuevas funciones exclusivas de Adobe Experience Platform. Sin embargo, esto también significa que las funciones de at.js no son compatibles con el SDK web de Platform. Al evaluar la implementación actual, tenga en cuenta lo siguiente:

- Funciones de at.js como `getOffer()` y `applyOffer()`
- Modificaciones en la configuración global de Target
- Integración con Adobe Analytics
- Uso de un script de mitigación de parpadeo
- Uso de tokens de respuesta
- Uso de parámetros de mbox, perfil y entidad
- Código personalizado exclusivo de su implementación

### ¿Qué enfoque de migración tomará?

Una vez que haya revisado la implementación de at.js, debe determinar un enfoque de migración. Hay dos opciones:

- Migrar todas las aplicaciones de Adobe a la vez en todo el sitio
- Migrar página por página

Dado que el SDK web de Platform combina y activa varias aplicaciones de Adobe, debe coordinar la migración de Target de otras aplicaciones de Adobe, como Analytics y Audience Manager. Todas las bibliotecas de Adobe de una página determinada deben migrarse al mismo tiempo. No se admite una implementación mixta del SDK web de Platform para Target ni AppMeasurement para Analytics en una página concreta. Sin embargo, se admite una implementación mixta en diferentes páginas, por ejemplo, SDK web de plataforma en la página A y at.js con AppMeasurement en la página B.

A medida que migre, antes de lanzar el producto a producción, debe planificar el seguimiento del proceso de su empresa para probar y publicar código nuevo y usar elementos como entornos de desarrollo, control de calidad y ensayo.

>[!CAUTION]
>
>Las ofertas de redireccionamiento no se admiten en las migraciones página por página si se redirecciona de una página con una biblioteca a una página con una biblioteca diferente


A continuación, revise los detalles [comparación de at.js con el SDK web de Platform](detailed-comparison.md) para comprender mejor las diferencias técnicas e identificar las áreas que requieren un enfoque adicional.

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
