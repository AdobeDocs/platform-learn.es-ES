---
title: Foundation - Ingesta de datos - Ingesta de datos desde fuentes sin conexión
description: Foundation - Ingesta de datos - Ingesta de datos desde fuentes sin conexión
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 93d9f4ef-9cbd-4310-879e-d69106b70404
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 3%

---

# 2.5 Zona de aterrizaje de datos

En este ejercicio, el objetivo es configurar el conector de origen de la zona de aterrizaje de datos con el almacenamiento del blob de Azure.

La zona de aterrizaje de datos es una interfaz de almacenamiento del blob de Azure aprovisionada por Adobe Experience Platform, que le concede acceso a una instalación de almacenamiento de archivos segura y basada en la nube para introducir archivos en Platform. La zona de aterrizaje de datos admite la autenticación basada en SAS y sus datos están protegidos con mecanismos de seguridad de almacenamiento Azure Blob estándar en reposo y en tránsito. La autenticación basada en SAS le permite acceder de forma segura a su contenedor de zona de aterrizaje de datos mediante una conexión pública a Internet.

>[!NOTE]
>
> Adobe Experience Platform **exige un tiempo de vida estricto de siete días (TTL)** en todos los archivos cargados en un contenedor de zona de aterrizaje de datos. Todos los archivos se eliminan al cabo de siete días.


## 2.5.1 Requisitos previos

Para copiar blobs o archivos a su zona de aterrizaje de datos de Adobe Experience Platform, utilizará AzCopy, una utilidad de línea de comandos. Puede descargar una versión para su sistema operativo a través de [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/es-es/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Descomprimir el archivo de descarga

![dlz-install-az-copy.png](./images/dlz1.png)

- Descargar el archivo de datos de ejemplo [global-context-websiteinteractions.csv](../../assets/csv/data-ingestion/global-context-websiteinteractions.csv), que contiene interacciones de sitio web de ejemplo y las guarda en la carpeta en la que ha descomprimido. **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Abra una ventana de terminal y vaya a la carpeta de su escritorio. Debería ver el siguiente contenido (azcopy y global-context-websiteinteractions.csv), por ejemplo en OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 2.5.2 Conexión de la zona de aterrizaje de datos a Adobe Experience Platform

Inicie sesión en Adobe Experience Platform accediendo a esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--module2sandbox--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar el simulador para pruebas apropiado, verá el cambio de pantalla y ahora estará en su simulador para pruebas dedicado.

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, vaya a **Fuentes**. En el catálogo de fuentes, busque **aterrizaje de datos**. En el **Zona de aterrizaje de datos** tarjeta, haga clic en **...** y seleccione **Ver credenciales**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Haga clic en Copiar **SASUri**.

![dlz-copy-sas-uri-png](./images/dlz-copy-sas-uri.png)

## 2.5.3 Copie su archivo csv en su zona de aterrizaje de datos de AEP

Ahora ingerirá datos en Adobe Experience Platform mediante las herramientas de línea de comandos de Azure mediante AZCopy.

Abra un terminal en la ubicación de la instalación de azcopy y ejecute el siguiente comando para copiar un archivo en la zona de aterrizaje de datos de AEP:

``./azcopy copy <your-local-file> <your SASUri>``

Asegúrese de rodear su SASUri con comillas dobles. Reemplazar `<your-local-file>` por la ruta de acceso a la copia local del archivo **global-context-websiteinteractions.csv** en el directorio azcopy y reemplace `<your SASUri>` por **SASUri** que ha copiado desde la interfaz de usuario de Adobe Experience Platform. El comando debería tener este aspecto:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Después de ejecutar el comando anterior en su terminal, verá esto:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 2.5.4 Busque su archivo en la zona de aterrizaje de datos

Vaya a la zona de aterrizaje de datos en Adobe Experience Platform.

Select **Fuentes**, busque **aterrizaje de datos** y haga clic en el botón **Configuración** botón.

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Se abrirá la zona de aterrizaje de datos. Verá el archivo que acaba de cargar en el informe **seleccionar datos** panel.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 2.5.5 Procesar el archivo

Seleccione el archivo y seleccione **Delimitado** como formato de datos. A continuación, verá una vista previa de sus datos. Haga clic en **Siguiente**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Ahora puede empezar a asignar los datos cargados para que coincidan con el esquema XDM del conjunto de datos.

Select **Conjunto de datos existente** y seleccione el conjunto de datos **Sistema de demostración: conjunto de datos de evento para sitio web (Global v1.1)**. Haga clic en **Siguiente**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Ya está listo para asignar los datos de origen entrantes del archivo csv a los campos de destino del esquema XDM del conjunto de datos.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> No importa los posibles errores con la asignación. Corrija la asignación en el siguiente paso.

## 2.5.6 Campos de asignación

En primer lugar, haga clic en el **Borrar todas las asignaciones** botón. A continuación, puede empezar con una asignación limpia.

![dlz-clear-mappings.png](./images/mappings1.png)

A continuación, haga clic en **Nuevo tipo de campo** y, a continuación, seleccione **Añadir nuevo campo**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Para asignar la variable **ecid** campo de origen, seleccione el campo **identities.ecid** y haga clic en **Select**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

A continuación, haga clic en **Asignar campo de destino**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Seleccione el campo ``--aepTenantId--``.identification.core.ecid en la estructura del esquema.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Debe asignar un par de campos más, haga clic en **+ Nuevo tipo de campo** seguido de **Añadir nuevo campo** y agregar campos para esta asignación

| source | Target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| timestamp | timestamp |
| timestamp | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

Cuando termine, la pantalla que aparece a continuación. Haga clic en **Siguiente**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Haga clic en **Siguiente**.

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

Haga clic en **Finalizar**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 2.5.7 Monitorización del flujo de datos

Para monitorizar el flujo de datos, vaya a **Fuentes**, **Flujos de datos** y haga clic en su flujo de datos:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

La carga de los datos puede tardar un par de minutos; si se realiza correctamente, verá un estado de **Correcto**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 2](./data-ingestion.md)

[Volver a todos los módulos](../../overview.md)
