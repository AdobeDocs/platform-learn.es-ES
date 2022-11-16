---
title: 'Activación de segmentos en el centro de eventos de Microsoft Azure: resumen y beneficios'
description: 'Activación de segmentos en el centro de eventos de Microsoft Azure: resumen y beneficios'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2174ac52-b5dd-4bc8-ab5f-4d84ae9ef19b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# Resumen y beneficios

¡Felicitaciones y gracias por invertir su tiempo en aprender sobre Microsoft Azure Event Hub y Adobe Experience Platform!
En este módulo, ha aprendido a configurar una instancia de Azure Event Hub y a conectarla a Adobe Experience Platform.

## Ventajas

Destacemos las ventajas de integrar Adobe Experience Platform con el Centro de eventos de Microsoft Azure:

- Los centros de eventos de Microsoft Azure como destino de Adobe Experience Platform le permiten capturar la calificación de segmentos en tiempo real y procesarlos mediante una función de Azure Event Hub. Con esta función de Azure Event Hub, puede crear cualquier tipo de controlador de activación de segmentos personalizado y, como tal, integrar cualquier tipo de destino de terceros.

- Aunque los destinos solo se activan mediante segmentos especificados, la carga útil de activación incluye todos los segmentos para los que se califica el perfil dado.

- Un segmento solo déclencheur una activación cuando su estado cambia. Por ejemplo, un perfil que se califica cuatro veces para un segmento en un periodo de tres meses, solo se activarán los dos primeros. El primero es un cambio de estado de a **realizado**, la segunda se activa mediante un cambio de estado de **realizado** a **existente**.

- Al activar segmentos para perfiles conocidos, se incluye un mapa de identidad completo en la carga útil de activación. La función de Azure puede utilizar cualquiera de las identidades disponibles para asignar los segmentos a un perfil administrado en una aplicación de terceros, mientras utiliza el identificador de cliente de la aplicación.

- En este módulo, la función de centro de eventos se implementó localmente (modo de depuración en código de Visual Studio), lo que le ofrece muchas opciones de solución de problemas y depuración.

## Consulte esto

- N/A

[Volver al módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../overview.md)
