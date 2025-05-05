---
title: 'Audience Activation a Microsoft Azure Event Hub: activar audiencia'
description: 'Audience Activation a Microsoft Azure Event Hub: activar audiencia'
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 5%

---

# 2.4.5 Activar la audiencia

## Agregar audiencia al destino de Azure Event Hub

En este ejercicio, agregará la audiencia `--aepUserLdap-- - Interest in Plans` a su destino de Azure Event Hub `--aepUserLdap---aep-enablement`.

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Vaya a **Destinos** y haga clic en **Examinar**. A continuación, verá todos los destinos disponibles. Busque su destino y haga clic en los 3 puntos&#x200B;**...** como se indica a continuación, luego haga clic en **Activar audiencias**.

![5-01-select-destination.png](./images/501selectdestination.png)

Entonces verá esto... Busque su audiencia con su ldap y seleccione `--aepUserLdap-- - Interest in Plans` de la lista de audiencias.

Haga clic en **Next**.

![5-04-select-segment.png](./images/504selectsegment.png)

Haga clic en **Agregar nuevo campo**, haga clic en Examinar esquema y seleccione el campo `--aepTenantId--identification.core.ecid` (elimine cualquier otro campo que se mostraría automáticamente).

Haga clic en **Next**.

![5-05-select-attributes.png](./images/505selectattributes.png)

Haga clic en **Finalizar**.

![5-06-destination-finish.png](./images/506destinationfinish.png)

La audiencia ahora está activada en el destino del centro de eventos de Microsoft.

![5-07-destination-segment-added.png](./images/507destinationsegmentadded.png)

## Pasos siguientes

Vaya a [2.4.6 y cree su proyecto de Microsoft Azure](./ex6.md){target="_blank"}

Volver a [Real-Time CDP: Audience Activation a Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
