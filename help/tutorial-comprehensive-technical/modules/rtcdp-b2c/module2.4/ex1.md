---
title: 'Activación de segmentos en Microsoft Azure Event Hub: configure Event Hub en Azure'
description: 'Activación de segmentos en Microsoft Azure Event Hub: configure Event Hub en Azure'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# 2.4.1 Configuración del entorno de Microsoft Azure EventHub

Azure Event Hubs es un servicio de suscripción de publicación con gran capacidad de adaptación que puede introducir millones de eventos por segundo y transmitirlos a varias aplicaciones. Esto le permite procesar y analizar las grandes cantidades de datos producidos por sus dispositivos y aplicaciones conectados.

## 2.4.1.1 ¿Qué es Azure Event Hubs?

Azure Event Hubs es una plataforma de transmisión de datos masivos y un servicio de ingesta de eventos. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un centro de eventos se pueden transformar y almacenar mediante cualquier proveedor de análisis en tiempo real o adaptador de almacenamiento/agrupamiento.

Event Hubs representa la **puerta principal** de una canalización de eventos, a menudo denominada ingestor de eventos en las arquitecturas de soluciones. Un ingestor de eventos es un componente o servicio que se encuentra entre los editores de eventos (como Adobe Experience Platform RTCDP) y los consumidores de eventos para desvincular la producción de un flujo de evento del consumo de esos eventos. Event Hubs proporciona una plataforma de streaming unificada con búfer de retención de tiempo, lo que desvincula a los productores de eventos de los consumidores de eventos.

## 2.4.1.2 Crear un área de nombres de Event Hubs

Vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home) y seleccione **Crear un recurso**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

En la pantalla del recurso, escribe **Event** en la barra de búsqueda y selecciona **Event Hubs** de la lista desplegable:

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Haga clic en **Crear**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Si es la primera vez que crea un recurso en Azure, deberá crear un nuevo **grupo de recursos**. Si ya tiene un grupo de recursos, puede seleccionarlo (o crear uno nuevo).

Seleccione **Crear nuevo**, asigne un nombre al grupo `--aepUserLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

Complete la prueba de los campos como se indica:

- Área de nombres: defina su área de nombres, debe ser única, use el siguiente patrón `--aepUserLdap---aep-enablement`
- Ubicación: **Europa occidental** se refiere al centro de datos de Azure en Ámsterdam
- Nivel de precios: **Básico**
- Unidades de rendimiento: **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

Haga clic en **Revisar + crear**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Haga clic en **Crear**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

La implementación del grupo de recursos puede tardar entre 1 y 2 minutos. Si se realiza correctamente, verá la siguiente pantalla:

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 2.4.1.3 Configurar el centro de eventos en Azure

Vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home) y seleccione **Todos los recursos**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

En la lista de recursos, seleccione su área de nombres `--aepUserLdap---aep-enablement`:

![1-10-list-resources.png](./images/1-10-list-resources.png)

En la pantalla de detalles de `--aepUserLdap---aep-enablement`, seleccione **Event Hubs**:

![1-11-eventhub-namespace.png](./images/1-11-eventhub-namespace.png)

Haga clic en **+ Centro de eventos**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

Use `--aepUserLdap---aep-enablement-event-hub` como nombre y haga clic en **Crear**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

Haga clic en **Event Hubs** en el área de nombres del centro de eventos. Ahora debería ver su **Centro de eventos** en la lista. En ese caso, puede pasar al siguiente ejercicio.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 2.4.1.4 Configurar su cuenta de almacenamiento de Azure

Para depurar la función de Azure Event Hub en ejercicios posteriores, deberá proporcionar una cuenta de almacenamiento de Azure como parte de la configuración del proyecto de código de Visual Studio. Ahora creará esa cuenta de almacenamiento de Azure.

Vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home) y seleccione **Crear un recurso**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Escriba **storage** en la búsqueda y seleccione **Storage Account** de la lista.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

Seleccione **Crear**.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

Especifique su **grupo de recursos** (creado al principio de este ejercicio), use `--aepUserLdap--aepstorage` como nombre de su cuenta de almacenamiento y seleccione **Almacenamiento redundante localmente (LRS)**; a continuación, haga clic en **Revisar + crear**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

Haga clic en **Crear**.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

La creación de su cuenta de almacenamiento tardará un par de segundos:

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

Cuando finalice, la pantalla mostrará el botón **Ir al recurso**.

Haga clic en **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

Su cuenta de almacenamiento ahora está visible en **Recursos recientes**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

Paso siguiente: [2.4.2 Configuración del destino de Azure Event Hub en Adobe Experience Platform](./ex2.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
