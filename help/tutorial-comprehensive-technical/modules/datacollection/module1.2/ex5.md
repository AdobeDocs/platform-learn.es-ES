---
title: Foundation - Ingesta de datos - Ingesta de datos desde fuentes sin conexión
description: Foundation - Ingesta de datos - Ingesta de datos desde fuentes sin conexión
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---

# 1.2.5 Zona de aterrizaje de datos

En este ejercicio, el objetivo es configurar el conector Source de la zona de aterrizaje de datos con el almacenamiento del blob de Azure.

La zona de aterrizaje de datos es una interfaz de almacenamiento del blob de Azure proporcionada por Adobe Experience Platform, que le permite acceder a una función de almacenamiento de archivos segura y basada en la nube para introducir archivos en Platform. La zona de aterrizaje de datos admite la autenticación basada en SAS y sus datos están protegidos con mecanismos de seguridad de almacenamiento del blob de Azure estándar en reposo y en tránsito. La autenticación basada en SAS le permite acceder de forma segura a su contenedor de zona de aterrizaje de datos a través de una conexión pública a Internet.

>[!NOTE]
>
> Adobe Experience Platform **aplica un tiempo de vida (TTL) estricto de siete días** a todos los archivos cargados en un contenedor de zona de aterrizaje de datos. Todos los archivos se eliminan a los siete días.


## 1.2.5.1 Requisitos previos

Para copiar blobs o archivos en la zona de aterrizaje de datos de Adobe Experience Platform, utilizará AzCopy, una utilidad de línea de comandos. Puede descargar una versión para su sistema operativo a través de [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Descomprima el archivo descargado

![dlz-install-az-copy.png](./images/dlz1.png)

- Descargue el archivo de datos de ejemplo global-context-websiteinteractions.csv, que contiene interacciones de sitio web de ejemplo y guárdelo en la carpeta en la que descomprimió **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Abra una ventana de terminal y vaya a la carpeta en su escritorio, debería ver el siguiente contenido (azcopy y global-context-websiteinteractions.csv), por ejemplo en OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 1.2.5.2 Conexión de la zona de aterrizaje de datos a Adobe Experience Platform

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--module2sandbox--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, ve a **Fuentes**. En el catálogo de fuentes, busque **aterrizaje de datos**. En la tarjeta **Zona de aterrizaje de datos**, haga clic en **...** y seleccione **Ver credenciales**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Haga clic en Copiar **SASUri**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 1.2.5.3 Copie el archivo CSV en la zona de aterrizaje de datos de AEP

Ahora, ingerirá datos en Adobe Experience Platform mediante las herramientas de línea de comandos de Azure con AZCopy.

Abra un terminal en la ubicación de su ubicación de instalación de AEP y ejecute el siguiente comando para copiar un archivo en la zona de aterrizaje de datos de AEP:

``./azcopy copy <your-local-file> <your SASUri>``

Asegúrate de rodear tu SASUri con comillas dobles. Reemplace `<your-local-file>` por la ruta a su copia local del archivo **global-context-websiteinteractions.csv** en el directorio azcopy, y reemplace `<your SASUri>` por el valor **SASUri** que copió de la interfaz de usuario de Adobe Experience Platform. El comando debería tener un aspecto similar al siguiente:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Después de ejecutar el comando anterior en el terminal, verá lo siguiente:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 1.2.5.4 Busque su archivo en la zona de aterrizaje de datos

Vaya a la zona de aterrizaje de datos en Adobe Experience Platform.

Seleccione **Orígenes**, busque **aterrizaje de datos** y haga clic en el botón **Configurar**.

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Se abrirá la zona de aterrizaje de datos. Verá el archivo que acaba de cargar en el panel **seleccionar datos** de la zona de aterrizaje de datos.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 1.2.5.5 Procesar el archivo

Seleccione su archivo y seleccione **Delimitado** como formato de datos. A continuación, verá una vista previa de los datos. Haga clic en **Next**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Ahora puede empezar a asignar los datos cargados para que coincidan con el esquema XDM del conjunto de datos.

Seleccione **Conjunto de datos existente** y seleccione el conjunto de datos **Sistema de demostración - Conjunto de datos de evento para el sitio web (Global v1.1)**. Haga clic en **Next**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Ahora está listo para asignar los datos de origen entrantes del archivo csv a los campos de destino desde el esquema XDM del conjunto de datos.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> No le importan los posibles errores con la asignación. Corrija la asignación en el siguiente paso.

## 1.2.5.6 Asignación de campos

En primer lugar, haga clic en el botón **Borrar todas las asignaciones**. A continuación, puede empezar con una asignación limpia.

![dlz-clear-mappings.png](./images/mappings1.png)

A continuación, haga clic en **Nuevo tipo de campo** y seleccione **Agregar nuevo campo**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Para asignar el campo de origen **ecid**, seleccione el campo **identities.ecid** y haga clic en **Seleccionar**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

A continuación, haga clic en **Asignar campo de destino**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Seleccione el campo ``--aepTenantId--``.identification.core.ecid en la estructura de esquema.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Debe asignar otros campos, haga clic en **+ Nuevo tipo de campo** seguido de **Agregar nuevo campo** y agregue campos para esta asignación

| origen | destino |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| timestamp | timestamp |
| timestamp | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

Cuando termine, la pantalla debería tener el aspecto siguiente. Haga clic en **Next**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Haga clic en **Next**.

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

Haga clic en **Finalizar**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 1.2.5.7 Monitorización del flujo de datos

Para supervisar su flujo de datos, vaya a **Orígenes**, **Flujos de datos** y haga clic en su flujo de datos:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

La carga de los datos puede tardar un par de minutos. Si se realiza correctamente, verá un estado de **Éxito**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 1.2](./data-ingestion.md)

[Volver a todos los módulos](../../../overview.md)
