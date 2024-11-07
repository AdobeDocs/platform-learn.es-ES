---
title: 'Activación de segmentos en Microsoft Azure Event Hub: configure el destino RTCDP del centro de eventos en Adobe Experience Platform'
description: 'Activación de segmentos en Microsoft Azure Event Hub: configure el destino RTCDP del centro de eventos en Adobe Experience Platform'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 2.4.2 Configuración del destino de Azure Event Hub en Adobe Experience Platform

## 2.4.2.1 Identificar los parámetros de conexión de Azure necesarios

Para definir un destino de centro de eventos en Adobe Experience Platform, necesita lo siguiente:

- Área de nombres de Event Hubs
- Centro de eventos
- Nombre de clave SAS de Azure
- Clave SAS de Azure

El espacio de nombres EventHub y EventHub se definieron en el ejercicio anterior: [Ejercicio 1 - Configurar Event Hub en Azure](./ex1.md)

### Área de nombres de Event Hubs

Para buscar la información anterior en Azure Portal, vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home). Asegúrese de que está utilizando la cuenta de Azure correcta.

Seleccione **Todos los recursos** en Azure Portal:

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### Centro de eventos

Busque un recurso con el tipo de recurso **Event Hubs Namespace**; si ha seguido las convenciones de nomenclatura utilizadas en el ejercicio anterior, el espacio de nombres de Event Hubs será `--aepUserLdap---aep-enablement`. Tome nota de ello, lo necesitará en el próximo ejercicio.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

Haga clic en el nombre del área de nombres de Event Hubs para obtener los detalles:

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

Seleccione **Event Hubs** para obtener una lista de los Event Hubs definidos en el área de nombres de Event Hubs; si ha seguido las convenciones de nomenclatura utilizadas en el ejercicio anterior, encontrará un Event Hub denominado `--aepUserLdap---aep-enablement-event-hub`. Tome nota de ello, lo necesitará en el próximo ejercicio.

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### Nombre de clave SAS

Seleccione **directivas de acceso compartido** para el espacio de nombres de **Event Hubs**

![2-05-select-sas.png](./images/2-05-select-sas.png)

Verá una lista de directivas de acceso compartido. La clave SAS que estamos buscando es **RootManageSharedAccessKey**. Nombre de la clave SAS. ¡Anótalo!

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### Valor de clave SAS

Haga clic en **RootManageSharedAccessKey** para obtener el valor de la clave SAS. Y presione el icono **Copiar al portapapeles** para copiar la **clave principal**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### Resumen de valores de destino

En este punto debería haber identificado todos los valores necesarios para definir el destino de Azure Event Hub en Adobe Experience Platform Real-time CDP.

| Nombre de atributo de destino | Valor de atributo de destino | Valor de ejemplo |
|---|---|---|
| sasKeyName | Nombre de clave SAS | RootManageSharedAccessKey |
| sasKey | Valor de clave SAS | srREx9ShJG1Rv7f/... |
| namespace | Área de nombres de Event Hubs | `--aepUserLdap---aep-enablement` |
| eventHubName | Centro de eventos | `--aepUserLdap---aep-enablement-event-hub` |

## 2.4.2.2 Crear un destino de Azure Event Hub en Adobe Experience Platform

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

Vaya a **Destinos** y luego a **Catálogo**.

![Ingesta de datos](./images/sb2a.png)

Seleccione **Almacenamiento en la nube**, vaya a **Azure Event Hubs** y haga clic en **Configurar** o **Configurar**:

![2-08-list-targets.png](./images/2-08-list-destinations.png)

Rellene los valores de destino recopilados en el ejercicio anterior. A continuación, haga clic en **Conectar con destino**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

Si las credenciales son correctas, verá una confirmación: **Conectado**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

Ahora necesita escribir el nombre y la descripción con el formato `--aepUserLdap---aep-enablement`. Escriba **eventHubName** (consulte el ejercicio anterior, tiene este aspecto: `--aepUserLdap---aep-enablement-event-hub`) y haga clic en **Siguiente**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

Haga clic en **Guardar y salir**.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

El destino se habrá creado y estará disponible en Adobe Experience Platform.

![2-12-destination-created.png](./images/2-12-destination-created.png)

Paso siguiente: [2.4.3 Crear un segmento](./ex3.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
