---
title: Comparación de la extensión de Target con la extensión de Decisioning
description: Obtenga información sobre las diferencias entre la extensión de Target y la extensión Decisioning, incluidas las funciones, la configuración y el flujo de datos.
source-git-commit: c907ccb9163ace8272f6881638a41362090bf3e5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 4%

---

# Comparación de la extensión de Target con la extensión de Decisioning

La extensión de Adobe Journey Optimizer - Decisioning difiere de la extensión de Adobe Target para aplicaciones móviles. Las siguientes tablas son una referencia para ayudarle a evaluar las áreas de la implementación en las que puede que tenga que centrarse durante el proceso de migración.

Después de revisar la información siguiente y evaluar la implementación técnica actual de la extensión de Target, debería poder comprender lo siguiente:

- Qué funciones de Target son compatibles con Adobe Journey Optimizer: Decisioning
- Qué funciones de extensión de Adobe Target tienen equivalentes en Adobe Journey Optimizer y Decisioning
- Aplicación de la configuración de Target con Adobe Journey Optimizer: decisiones
- Diferencias entre el flujo de datos de la extensión de Adobe Target y la extensión de Adobe Journey Optimizer - Decisioning

Si es nuevo en el SDK web de Platform, no se preocupe: los elementos siguientes se tratan con más detalle a lo largo de este tutorial.

## Comparación de características

| Función | Extensión de Target | Extensión de Decisioning (Target a través de Edge) |
|---|---|---|
| Modo de recuperación previa | Admitido | Admitido |
| Modo de ejecución | Admitido | No compatible |
| Parámetros personalizados | Admitido | No se admiten parámetros por mbox |
| Audiencias de entrada | Admitido | Admitido |
| Segmentación de audiencias mediante métricas móviles del ciclo vital | Admitido | Compatible mediante reglas de recopilación de datos |
| thirdPartyId (mbox3rdPartyId) | Admitido | Compatible mediante el mapa de identidad y la configuración del área de nombres en el conjunto de datos |
| Notificaciones (mostrar, hacer clic) | Admitido | Admitido |
| Tokens de respuesta | Admitido | Admitido |
| Ofertas dinámicas | Admitido | Admitido |
| Analytics para Target (A4T) | Solo del lado del cliente | Lado del cliente y lado del servidor |
| Vistas previas móviles (modo de control de calidad) | Admitido | Asistencia limitada |



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

Los siguientes diagramas le ayudarán a comprender las diferencias del flujo de datos entre una implementación de Target con la extensión Adobe Journey Optimizer - Decisioning y una implementación con la extensión Adobe Target.

### Diagrama del sistema de extensiones de Target



### Diagrama del sistema de extensión de Decisioning




>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
