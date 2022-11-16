---
title: 'Activación de segmentos en el centro de eventos de Microsoft Azure: Activar segmento'
description: 'Activación de segmentos en el centro de eventos de Microsoft Azure: Activar segmento'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 250f8536-b6bd-4c64-a552-80d5c6fb6358
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 2%

---

# 13.4 Activar segmento

## 13.4.1 Añadir segmento al destino del centro de eventos de Azure

En este ejercicio, agregará su segmento `--demoProfileLdap-- - Interest in Equipment` a su `--demoProfileLdap---aep-enablement` Destino de Azure Event Hub.

Inicie sesión en Adobe Experience Platform accediendo a esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepSandboxId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar el simulador para pruebas apropiado, verá el cambio de pantalla y ahora estará en su simulador para pruebas dedicado.

![Ingesta de datos](../module2/images/sb1.png)

Vaya a **Destinos** y haga clic en **Examinar**. A continuación, verá todos los destinos disponibles. Busque el destino y haga clic en el botón **+** como se indica a continuación.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Entonces verás esto. Busque su segmento utilizando su LDAP y seleccione `--demoProfileLdap-- - Interest in Equipment` de la lista de segmentos.

Haga clic en **Siguiente**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

CDP en tiempo real de Adobe Experience Platform puede entregar una carga útil a dos tipos de destinos, destinos de segmento y destinos de perfil.

Los destinos de segmento recibirán una carga útil de calificación de segmento predefinida que se analizará más adelante. Esta carga útil contiene **all** cualificaciones del segmento para un perfil específico. Incluso para segmentos que no están en la lista de activación de destino. Un ejemplo de este destino de segmento es **Centros de eventos de Azure** y **AWS Kinesis**.

Los destinos basados en perfiles permiten elegir cualquier atributo (firstName, lastName, ...) del esquema de unión de perfiles XDM e incluirlo en la carga útil de activación. Un ejemplo de este destino es el **Marketing por correo electrónico**.

Como su destino de Azure Event Hub es un **segmento** destino, seleccione, por ejemplo, el campo `--aepTenantId--.identification.core.ecid`.

Haga clic en **Añadir nuevo campo**, haga clic en examinar esquema y seleccione el campo `--aepTenantId--identification.core.ecid` (elimine cualquier otro campo que se muestre automáticamente).

Haga clic en **Siguiente**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Haga clic en **Finalizar**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

El segmento ahora se activa para el destino de Microsoft Event Hub.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Paso siguiente: [13.5 Crear su proyecto de Microsoft Azure](./ex5.md)

[Volver al módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../overview.md)
