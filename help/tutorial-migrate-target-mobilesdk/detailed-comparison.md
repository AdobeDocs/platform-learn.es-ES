---
title: Comparación de la extensión de Target con la extensión de Decisioning
description: Obtenga información sobre las diferencias entre at.js 2.x y el SDK web de Platform, incluidas las funciones, la configuración y el flujo de datos.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# Comparación de la extensión de Target con la extensión de Decisioning

La biblioteca independiente at.js de Adobe Target difiere considerablemente del SDK web de Platform. Las siguientes tablas son una referencia para ayudarle a evaluar las áreas de la implementación en las que puede que tenga que centrarse durante el proceso de migración.

Después de revisar la información que aparece a continuación y evaluar su implementación técnica actual de at.js, debería poder comprender lo siguiente:

- Qué funciones de Target son compatibles con el SDK web de Platform
- Qué funciones de at.js tienen equivalentes del SDK web de Platform
- Aplicación de la configuración de Target con el SDK web de Platform
- Diferencias entre el flujo de datos de at.js y el SDK web de Platform

Si es nuevo en el SDK web de Platform, no se preocupe: los elementos siguientes se tratan con más detalle a lo largo de este tutorial.

## Comparación de características

| | Extensión de Target | Extensión de Decisioning (Target a través de Edge) | Experiencias basadas en código de AJO (SDK de mensajería) |
|---|---|---|---|
| Modo de recuperación previa | Admitido | Admitido | Admitido |
| Modo de ejecución | Admitido | No compatible | No compatible |
| Parámetros personalizados | Admitido | No se admiten parámetros por mbox | No compatible |
| Audiencias de entrada | Admitido | Admitido | Admitido mediante la configuración de audiencia de Campaign y de exclusión de experimentos |
| Segmentación de audiencias mediante métricas móviles del ciclo vital | Admitido | Compatible mediante reglas de recopilación de datos | Actualmente, la segmentación de experiencias no es compatible |
| thirdPartyId (mbox3rdPartyId) | Compatible mediante el mapa de identidad y la configuración del área de nombres en el conjunto de datos | No compatible |
| Notificaciones (mostrar, hacer clic) | Admitido | Admitido | Admitido |
| Tokens de respuesta | Admitido | Admitido | No equivalente para devolver metadatos específicos de la campaña fuera del contenido |
| Ofertas dinámicas | Admitido | Admitido | Se admite la representación de token relacionado con perfiles y elementos de decisión en el contenido |
| Analytics para Target (A4T) | Solo del lado del cliente | Lado del cliente y lado del servidor | No compatible |
| Vistas previas móviles (modo de control de calidad) | Admitido | Asistencia limitada | En curso |



## Llamadas dignas de mención

>[!NOTE]
>
>No se admite la migración de Target al SDK web de Platform mientras se mantiene una implementación de Adobe Analytics de AppMeasurement existente para una página determinada.
>
> Es posible migrar la implementación de at.js (y AppMeasurement.js) al SDK web de Platform de una en una. Si adopta este enfoque, es mejor establecer las opciones [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) y [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) en `true` con el comando `configure`.

## Funciones de extensión de Target y equivalentes de extensión de Decisioning

Muchas funciones de extensión de Target tienen un enfoque equivalente que utiliza la extensión Decisioning descrita en la tabla siguiente. Para obtener más información sobre [funciones](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulte la Guía para desarrolladores de Adobe Target.

| Extensión de Target | Extensión de Decisioning |
| --- | --- | 
| |  |

## Configuración de la extensión de Target y equivalentes de la extensión Decisioning

La extensión de Target se puede configurar y descargar con varios ajustes en la ...

| Extensión de Target | Extensión de Decisioning |
| --- | --- | 
| |  |


## Comparación del diagrama del sistema

Los siguientes diagramas le ayudarán a comprender las diferencias del flujo de datos entre una implementación de Target con at.js y una implementación con el SDK web de Platform.

### Diagrama del sistema de extensiones de Target



### Diagrama del sistema de extensiones Decisioning




>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
