---
title: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: implementación de Adobe Analytics y Adobe Audience Manager'
description: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: implementación de Adobe Analytics y Adobe Audience Manager'
kt: 5342
doc-type: tutorial
exl-id: 9c60eef0-8ac6-45ce-96c7-19516c94a813
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# 1.1.5 Implementación de Adobe Analytics y Adobe Audience Manager

## Contexto

Ahora sabe que los datos XDM fluyen a la plataforma. Explorará más sobre qué es XDM en [Módulo 1.2](./../dc1.2/data-ingestion.md), así como sobre cómo generar su propio esquema para rastrear variables personalizadas. Por ahora, verá lo que sucede cuando establece su secuencia de datos para reenviar datos a Analytics y Audience Manager.

## Asignación de variables en Analytics

Adobe Experience Platform [!DNL Web SDK] asigna ciertos valores automáticamente, lo que hace que una nueva implementación de Analytics mediante Web SDK sea lo más rápida posible. Las variables asignadas automáticamente se enumeran [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection).

Para datos XDM que no se asignan automáticamente a Adobe Analytics, puede usar [datos de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=es) para que coincidan con su [esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es). A continuación, se puede asignar a Analytics mediante [reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) para rellenar variables de Analytics. Los datos de contexto y las reglas de procesamiento serán conceptos familiares para quienes hayan trabajado con Analytics en el pasado, pero no se preocupe por los detalles por ahora si son conceptos nuevos.

También puede utilizar un conjunto predeterminado de acciones y listas de productos para enviar o recuperar datos con AEP Web SDK. Para ello, consulte [Productos](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection).

### Datos de contexto

Para que los utilice Analytics, los datos XDM se acoplan con notación de puntos y se ponen a disposición como `contextData`. La siguiente lista de pares de valores muestra un ejemplo de `context data`:

```javascript
{
    "bh": "900",
    "bw": "1680",
    "c": "24",
    "c.a.d.key.[0]": "value1",
    "c.a.d.key.[1]": "value2",
    "c.a.d.object.key1": "value1",
    "c.a.d.object.key2.[0]": "value2",
    "c.a.x.environment.browserdetails.javascriptenabled": "true",
    "c.a.x.environment.type": "browser",
    "cust_hit_time_gmt": "1579781427",
    "g": "http://example.com/home",
    "gn": "home",
    "j": "1.8.5",
    "k": "Y",
    "s": "1680x1050",
    "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:01,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
    "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
    "v": "Y"
}
```

### Reglas de procesamiento

Se puede acceder a todos los datos recopilados por la red perimetral mediante [reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). En Analytics, puede utilizar reglas de procesamiento para incorporar datos de contexto en variables de Analytics.

## Audience Manager en Experience Platform Edge Network

El reenvío del lado del servidor no es un concepto nuevo para Audience Manager y se aplica el mismo proceso que antes. También puede sincronizar identidades.

## Revise el flujo de datos para enviar datos a Adobe Analytics

Si desea enviar datos recopilados por Web SDK a Adobe Analytics y Adobe Audience Manager, siga estos pasos.

Vaya a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) y luego a **Datastreams**.

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`. Abra la secuencia de datos específica, que se llama `--aepUserLdap-- - Demo System Datastream`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Entonces verá esto... Para habilitar Adobe Analytics, haga clic en **Agregar servicio**.

![Depurador de AEP](./images/aa2.png)

Entonces verá esto... Seleccione el servicio **Adobe Analytics**, después del cual tendrá que agregar el grupo de informes en Adobe Analytics para enviar datos a. En este tutorial, está fuera de ámbito. Haga clic en **Cancelar**.

![Depurador de AEP](./images/aa3.png)

## Revise el flujo de datos para enviar datos a Adobe Audience Manager

Entonces verá esto... Para habilitar Adobe Audience Manager, haga clic en **Agregar servicio**.

![Depurador de AEP](./images/aa2.png)

Entonces verá esto... Seleccione el servicio **Adobe Audience Manager** tras el cual puede decidir habilitar o deshabilitar destinos de cookies de Adobe Audience Manager o destinos de URL. En este tutorial, esta configuración está fuera de ámbito. Haga clic en **Cancelar**.

![Depurador de AEP](./images/aam1.png)

## Pasos siguientes

Ir a [1.1.6 Implementar Adobe Target](./ex6.md){target="_blank"}

Volver a la [configuración de la recopilación de datos de Adobe Experience Platform y la extensión de etiquetas de Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
