---
title: 'Activación de segmentos en Microsoft Azure Event Hub: activar segmento'
description: 'Activación de segmentos en Microsoft Azure Event Hub: activar segmento'
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 3%

---

# 2.4.4 Activar segmento

## 2.4.4.1 Agregar segmento al destino de Azure Event Hub

En este ejercicio, agregará el segmento `--aepUserLdap-- - Interest in Equipment` a su destino de Azure Event Hub `--aepUserLdap---aep-enablement`.

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

Vaya a **Destinos** y haga clic en **Examinar**. A continuación, verá todos los destinos disponibles. Busque su destino y haga clic en el icono **+** como se indica a continuación.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Entonces verá esto... Busque el segmento con el LDAP y seleccione `--aepUserLdap-- - Interest in Equipment` en la lista de segmentos.

Haga clic en **Next**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform Real-time CDP puede entregar una carga útil a dos tipos de destinos, destinos de segmento y destinos de perfil.

Los destinos de segmento recibirán una carga útil de calificación de segmentos predefinida que se analizará más adelante. Esta carga útil contiene **todas** las clasificaciones de segmento para un perfil específico. Incluso para segmentos que no están en la lista de activación del destino. Un ejemplo de este destino de segmento son **Azure Event Hubs** y **AWS Kinesis**.

Los destinos basados en perfiles le permiten elegir cualquier atributo (firstName, lastName, ...) del esquema de unión de perfiles XDM e incluirlo en la carga útil de activación. Un ejemplo de este destino es **Email Marketing**.

Dado que el destino de Azure Event Hub es un destino de **segmento**, seleccione, por ejemplo, el campo `--aepTenantId--.identification.core.ecid`.

Haga clic en **Agregar nuevo campo**, haga clic en Examinar esquema y seleccione el campo `--aepTenantId--identification.core.ecid` (elimine cualquier otro campo que se mostraría automáticamente).

Haga clic en **Next**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Haga clic en **Finalizar**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

El segmento ahora está activado para el destino del centro de eventos de Microsoft.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Paso siguiente: [2.4.5 Cree su proyecto de Microsoft Azure](./ex5.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
