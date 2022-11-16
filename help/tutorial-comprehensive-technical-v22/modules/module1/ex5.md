---
title: 'Fundamento: Configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: Implementación de Adobe Analytics y Adobe Audience Manager'
description: 'Fundamento: Configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: Implementación de Adobe Analytics y Adobe Audience Manager'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: e3ef6534-9af9-4b8c-86d0-46f413f4ff6d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 11%

---

# 1.5: Implementar Adobe Analytics y Adobe Audience Manager

## Contexto

Ahora sabe que los datos XDM fluyen a la plataforma. Explorará más sobre qué es XDM [Módulo 2](./../module2/data-ingestion.md), así como cómo crear su propio esquema para rastrear variables personalizadas. Por ahora, se fijará en lo que sucede cuando se establece el almacén de datos para reenviar datos a Analytics y Audience Manager.

## 1.5.1 Asignación de variables en Analytics

Adobe Experience Platform [!DNL Web SDK] asigna ciertos valores automáticamente, lo que hace que una nueva implementación de Analytics mediante el SDK web sea lo más rápida posible. Se enumeran las variables asignadas automáticamente [here](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html#data-collection).

Para datos XDM a los que no se asigna automáticamente [!DNL Adobe Analytics], puede usar [datos de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=es) para que coincida con su [esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es). A continuación, se puede asignar a [!DNL Analytics] using [reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=es) para rellenar [!DNL Analytics] variables. Los datos de contexto y las reglas de procesamiento serán conceptos familiares para quienes hayan trabajado con Analytics en el pasado, pero no se preocupen por los detalles por ahora si son nuevos conceptos.

También puede utilizar un conjunto predeterminado de acciones y listas de productos para enviar o recuperar datos con AEP [!DNL Web SDK]. Para ello, consulte [Productos](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#data-collection).

### Datos de contexto

Para usar por [!DNL Analytics], los datos XDM se acoplan con notación de puntos y se ponen a disposición como `contextData`. La siguiente lista de pares de valores muestra un ejemplo de `context data`:

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

Se puede acceder a todos los datos recopilados por la red perimetral mediante [reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). En [!DNL Analytics], puede utilizar reglas de procesamiento para incorporar datos de contexto en [!DNL Analytics] variables.

## Audience Manager 1.5.2 en la red perimetral del Experience Platform

El reenvío del lado del servidor no es un concepto nuevo para el Audience Manager y se aplica el mismo proceso que antes. También puede sincronizar identidades.

## 1.5.3 Revisar el almacén de datos para enviar datos a Adobe Analytics

Si desea enviar datos recopilados por el SDK web a Adobe Analytics y Adobe Audience Manager, siga estos pasos.

Vaya a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) y vaya a **Datastreams**.

En la esquina superior derecha de la pantalla, seleccione el nombre del simulador de pruebas, que debería ser `--aepSandboxId--`. Abra el conjunto de datos específico, que lleva el nombre `--demoProfileLdap-- - Demo System Datastream`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Entonces verás esto. Para habilitar Adobe Analytics, haga clic en **+Añadir servicio**.

![AEP Debugger](./images/aa2.png)

Entonces verás esto. Seleccione el servicio **Adobe Analytics**, después de lo cual debe agregar el grupo de informes en Adobe Analytics para enviar datos a . En este tutorial, esto está fuera de ámbito. Haga clic en **Cancelar**.

![AEP Debugger](./images/aa3.png)

## 1.5.4 Revise su almacén de datos para enviar datos a Adobe Audience Manager

Entonces verás esto. Para habilitar Adobe Audience Manager, haga clic en **+Añadir servicio**.

![AEP Debugger](./images/aa2.png)

Entonces verás esto. Seleccione el servicio **Adobe Audience Manager** tras el cual puede decidir habilitar o deshabilitar destinos de cookies o URL de Adobe Audience Manager. En este tutorial, esta configuración está fuera de ámbito. Haga clic en **Cancelar**.

![AEP Debugger](./images/aam1.png)

Paso siguiente: [1.6 Implementar Adobe Target](./ex6.md)

[Volver al módulo 1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../overview.md)
