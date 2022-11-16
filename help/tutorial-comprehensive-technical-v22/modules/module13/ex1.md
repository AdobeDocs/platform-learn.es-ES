---
title: 'Activación de segmentos en el Centro de eventos de Microsoft Azure: Centro de eventos de configuración en Azure'
description: 'Activación de segmentos en el Centro de eventos de Microsoft Azure: Centro de eventos de configuración en Azure'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 9434ac83-5554-48bf-838c-7346d571efbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# 13.1 Configurar el entorno de Microsoft Azure EventHub

Azure Event Hubs es un servicio de suscripción de publicación altamente escalable que puede ingerir millones de eventos por segundo y transmitirlos a varias aplicaciones. Esto le permite procesar y analizar las cantidades masivas de datos que producen sus aplicaciones y dispositivos conectados.

## 13.1.1 ¿Qué son los centros de eventos de Azure?

Los centros de eventos de Azure son una plataforma de transmisión de datos y un servicio de ingesta de eventos. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un centro de eventos se pueden transformar y almacenar utilizando cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento/lotes.

Los centros de eventos representan la variable **puerta delantera** para una canalización de eventos, denominada a menudo ingestor de eventos en arquitecturas de soluciones. Un ingestor de eventos es un componente o servicio que se encuentra entre editores de eventos (como Adobe Experience Platform RTCDP) y consumidores de eventos para desvincular la producción de un flujo de eventos del consumo de esos eventos. Los centros de eventos proporcionan una plataforma de transmisión unificada con búfer de retención de tiempo, lo que desvincula a los productores de eventos de los consumidores de eventos.

## 13.1.2 Crear un espacio de nombres de Hubs de eventos

Vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home) y seleccione **Crear un recurso**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

En la pantalla del recurso, introduzca **Evento** en la barra de búsqueda y seleccione **Centros de eventos** en el menú desplegable:

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Haga clic en **Crear**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Si es la primera vez que crea un recurso en Azure, deberá crear un nuevo **Grupo de recursos**. Si ya tiene un grupo de recursos, puede seleccionarlo (o crear uno nuevo).

Select **Crear nuevo**, asigne un nombre al grupo `--demoProfileLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

Complete la prueba de los campos como se indica:

- Espacio de nombres : Defina su área de nombres, debe ser única, utilice el siguiente patrón `--demoProfileLdap---aep-enablement`
- Ubicación: **Europa Occidental** hace referencia al centro de datos de Azure en Ámsterdam
- Nivel de precios: **Básico**
- Unidades de rendimiento: **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

Haga clic en **Revisar + crear**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Haga clic en **Crear**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

La implementación de su grupo de recursos puede tardar entre 1 y 2 minutos, cuando se realice correctamente, verá la siguiente pantalla:

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 13.1.3 Configurar el centro de eventos en Azure

Vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home) y seleccione **Todos los recursos**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

En la lista de recursos, seleccione su `--demoProfileLdap---aep-enablement` namespace:

![1-10-list-resources.png](./images/1-10-list-resources.png)

En `--demoProfileLdap---aep-enablement` pantalla de detalles, seleccione **Centros de eventos**:

![1-11-eventhub-namespace.png](./images/1-11-eventhub-namespace.png)

Haga clic en **+ Centro de eventos**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

Uso `--demoProfileLdap---aep-enablement-event-hub` como nombre y haga clic en **Crear**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

Haga clic en **Centros de eventos** en el espacio de nombres del centro de eventos. Ahora debería ver su **Centro de eventos** en la lista. Si ese es el caso, puede pasar al siguiente ejercicio.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 13.1.4 Configurar su cuenta de almacenamiento de Azure

Para depurar la función de Azure Event Hub en ejercicios posteriores, debe proporcionar una cuenta de almacenamiento de Azure como parte de la configuración del proyecto de código de Visual Studio. Ahora creará esa cuenta de almacenamiento de Azure.

Vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home) y seleccione **Crear un recurso**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Entrar **almacenamiento** en la búsqueda y seleccione **Cuenta de almacenamiento** de la lista.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

Seleccione **Crear**.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

Especifique la **Grupo de recursos** (creado al principio de este ejercicio), utilice `--demoProfileLdap--aepstorage` como nombre de cuenta de almacenamiento y seleccione **Almacenamiento redundante local (LRS)** y haga clic en **Revisar + crear**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

Haga clic en **Crear**.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

La creación de su cuenta de almacenamiento tardará un par de segundos:

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

Cuando termine, la pantalla mostrará la variable **Ir al recurso** botón.

Haga clic en **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

Su cuenta de almacenamiento ahora está visible en **Recursos recientes**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

Paso siguiente: [13.2 Configurar el destino del centro de eventos de Azure en Adobe Experience Platform](./ex2.md)

[Volver al módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../overview.md)
