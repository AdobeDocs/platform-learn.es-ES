---
title: 'Audience Activation de Microsoft Azure Event Hub: activar audiencia'
description: 'Audience Activation de Microsoft Azure Event Hub: activar audiencia'
kt: 5342
doc-type: tutorial
exl-id: 89cfda0e-6c5e-45ab-9506-f0f0f6211e7f
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 4%

---

# 2.4.5 Activar la audiencia

## Agregar audiencia al destino de Azure Event Hub

En este ejercicio, agregará la audiencia `--aepUserLdap-- - Interest in Plans` a su destino de Azure Event Hub `--aepUserLdap---aep-enablement`.

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

Vaya a **Destinos** y haga clic en **Examinar**. A continuación, verá todos los destinos disponibles. Busque su destino y haga clic en los 3 puntos**...** como se indica a continuación, luego haga clic en **Activar audiencias**.

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

Siguiente paso: [2.4.6 Crear su proyecto de Microsoft Azure](./ex6.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
