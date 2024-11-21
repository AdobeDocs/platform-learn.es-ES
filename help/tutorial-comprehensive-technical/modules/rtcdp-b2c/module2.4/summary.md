---
title: 'Audience Activation de Microsoft Azure Event Hub: resumen y ventajas'
description: 'Audience Activation de Microsoft Azure Event Hub: resumen y ventajas'
kt: 5342
doc-type: tutorial
exl-id: 3b598ffc-875e-468d-b91c-882062e8203f
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# Resumen y ventajas

¡Felicidades y gracias por dedicar su tiempo a conocer Microsoft Azure Event Hub y Adobe Experience Platform!
En este módulo, ha aprendido a configurar una instancia de Azure Event Hub y a conectarla a Adobe Experience Platform.

## Ventajas

Vamos a destacar las ventajas de integrar Adobe Experience Platform con el centro de eventos de Microsoft Azure:

- Microsoft Azure Event Hubs as a Adobe Experience Platform Destination le permite capturar la calificación de audiencias en tiempo real y procesarlas con una función de Azure Event Hub. Con una función de Azure Event Hub de este tipo, puede crear cualquier tipo de controlador de activación de audiencia personalizado y, como tal, integrar cualquier tipo de destino de terceros.

- Aunque los destinos solo se activan para audiencias especificadas, la carga útil de activación incluirá todas las audiencias para las que el perfil dado cumple los requisitos.

- Una audiencia solo almacena en déclencheur una activación cuando cambia su estado. Por ejemplo, un perfil que cumpla cuatro veces los requisitos de una audiencia en un periodo de tres meses, solo se activarán los dos primeros. El primero es un cambio de estado de a **realizado**, el segundo se activa por un cambio de estado de **realizado** a **existente**.

- Al activar audiencias para perfiles conocidos, se incluye un mapa de identidad completo en la carga útil de activación. La función de Azure puede utilizar cualquiera de las identidades disponibles para asignar las audiencias a un perfil administrado en una aplicación de terceros, mientras utiliza el identificador de cliente de la aplicación.

- En este módulo, la función de concentrador de eventos se implementó localmente (modo de depuración en código de Visual Studio), lo que ofrece numerosas opciones de solución de problemas y depuración.

## Eche un vistazo a esto

- N/A

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
