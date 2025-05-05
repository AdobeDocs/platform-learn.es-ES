---
title: Ingesta de datos por lotes
seo-title: Ingest batch data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Ingesta de datos por lotes
description: En esta lección, debe introducir datos por lotes en Experience Platform mediante varios métodos.
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-batch-data.jpg
exl-id: fc7db637-e191-4cc7-9eec-29f4922ae127
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '2446'
ht-degree: 0%

---

# Ingesta de datos por lotes

<!-- 1hr-->
En esta lección, debe introducir datos por lotes en Experience Platform mediante varios métodos.

La ingesta de datos por lotes le permite introducir una gran cantidad de datos en Adobe Experience Platform a la vez. Puede introducir datos por lotes de una sola vez y cargarlos en la interfaz de Platform o mediante la API. También puede configurar cargas por lotes programadas regularmente desde servicios de terceros, como los servicios de almacenamiento en la nube, mediante los conectores de Source.

**Los ingenieros de datos** deberán ingerir datos por lotes fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre la ingesta de datos:

>[!VIDEO](https://video.tv.adobe.com/v/27106?learn=on&enablevpops)


## Permisos necesarios

En la lección [Configurar permisos](configure-permissions.md), configuró todos los controles de acceso necesarios para completar esta lección.

<!--
* Permission item **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]**, **[!UICONTROL Manage Datasets]** and **[!UICONTROL Data Monitoring]**
* Permission items **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

Necesitará acceso a un servidor (S)FTP o a una solución de almacenamiento en la nube para el ejercicio Fuentes. Si no dispone de una solución alternativa.

## Ingesta de datos por lotes con la interfaz de usuario de Platform

Los datos se pueden cargar directamente en un conjunto de datos en la pantalla de conjuntos de datos en los formatos JSON y parquet. Esta es una buena manera de probar la ingesta de algunos de los datos después de crear una

### Descargue y prepare los datos

En primer lugar, obtenga los datos de ejemplo y personalícelos para su inquilino:

>[!NOTE]
>
>Los datos contenidos en el archivo [luma-data.zip](assets/luma-data.zip) son ficticios y solo se deben usar con fines de demostración.

1. Descargue [luma-data.zip](assets/luma-data.zip) en su carpeta de **Tutorial de Luma de Assets**.
1. Descomprima el archivo y cree una carpeta llamada `luma-data` que contenga los cuatro archivos de datos que usaremos en esta lección
1. Abra `luma-loyalty.json` en un editor de texto y reemplace todas las instancias de `_techmarketingdemos` con su propio id. de inquilino de guion bajo, tal como se ve en sus propios esquemas:
   ![Id. de inquilino de guion bajo](assets/ingestion-underscoreTenant.png)

1. Guarde el archivo actualizado

### Ingesta de datos

1. En la interfaz de usuario de Platform, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo
1. Abra su `Luma Loyalty Dataset`
1. Desplácese hacia abajo hasta que vea la sección **[!UICONTROL Agregar datos]** en la columna derecha
1. Cargar el archivo `luma-loyalty.json`.
1. Una vez cargado el archivo, aparecerá una fila para el lote
1. Si vuelve a cargar la página después de unos minutos, verá que el lote se ha cargado correctamente con 1000 registros y 1000 fragmentos de perfil.

   ![Ingesta](assets/ingestion-loyalty-uploadJson.png)
   <!--do i need to explain error diagnostics and partial ingestion-->

>[!NOTE]
>
>Hay algunas opciones, **[!UICONTROL Diagnóstico de errores]** e **[!UICONTROL Ingesta parcial]**, que verá en varias pantallas en esta lección. Estas opciones no se tratan en el tutorial. Información rápida:
>
>* Al habilitar los diagnósticos de error, se generan datos sobre la ingesta de sus datos, que puede revisar mediante la API de acceso a datos. Obtenga más información al respecto en [la documentación](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=es).
>* La ingesta parcial permite introducir datos que contienen errores, hasta un determinado umbral que puede especificar. Obtenga más información al respecto en [la documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/partial.html?lang=es)

### Validación de los datos

Existen varias formas de confirmar que los datos se han introducido correctamente.

#### Validación en la interfaz de usuario de Platform

Para confirmar que los datos se han introducido en el conjunto de datos:

1. En la misma página donde ha introducido los datos, seleccione el botón **[!UICONTROL Vista previa del conjunto de datos]** en la parte superior derecha
1. Seleccione el botón **Vista previa** para poder ver algunos de los datos ingeridos.

   ![Vista previa del conjunto de datos correcto](assets/ingestion-loyalty-preview.png)


Para confirmar que los datos han aterrizado en el perfil (los datos pueden tardar unos minutos en aterrizar):

1. Vaya a **[!UICONTROL Perfiles]** en el panel de navegación izquierdo
1. Seleccione el icono junto al campo **[!UICONTROL Seleccionar área de nombres de identidad]** para abrir el modal
1. Seleccione su área de nombres `Luma Loyalty Id`
1. A continuación, introduzca uno de los valores `loyaltyId` del conjunto de datos, `5625458`
1. Seleccionar **[!UICONTROL vista]**
   ![Confirmar un perfil del conjunto de datos](assets/ingestion-loyalty-profile.png)

#### Validación con eventos de ingesta de datos

Si se ha suscrito a los eventos de ingesta de datos de la lección anterior, compruebe la dirección URL única de webhook.site. Debería ver tres solicitudes que aparecen en el siguiente orden, con un tiempo entre ellas, con los siguientes `eventCode` valores:

1. `ing_load_success`: el lote como ingerido
1. `ig_load_success`: el lote se incorporó al gráfico de identidades
1. `ps_load_success`: el lote se incorporó al servicio de perfil

![webhook de ingesta de datos](assets/ingestion-loyalty-webhook.png)

Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html?lang=es#available-status-notification-events) para obtener más información sobre las notificaciones.

## Ingesta de datos por lotes con la API de Platform

Ahora vamos a cargar datos mediante la API.

>[!NOTE]
>
>Los arquitectos de datos pueden cargar los datos de CRM mediante el método de interfaz de usuario.

### Descargue y prepare los datos

1. Ya debería haber descargado y descomprimido [luma-data.zip](assets/luma-data.zip) en su carpeta `Luma Tutorial Assets`.
2. Abra `luma-crm.json` en un editor de texto y reemplace todas las instancias de `_techmarketingdemos` con su propio id. de inquilino de guion bajo, tal como se ve en los esquemas
3. Guarde el archivo actualizado

### Obtención del ID del conjunto de datos

Primero vamos a obtener el ID del conjunto de datos en el que queremos introducir los datos:

1. Abrir [!DNL Postman]
1. Si no tiene un token de acceso, abra la solicitud **[!DNL OAuth: Request Access Token]** y seleccione **Enviar** para solicitar un nuevo token de acceso, tal como lo hizo en la lección [!DNL Postman].
1. Abra las variables de entorno y asegúrese de que el valor de **CONTAINER_ID** sigue siendo `tenant`
1. Abra la solicitud **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]** y seleccione **Enviar**
1. Debería obtener una respuesta de `200 OK`
1. Copie el ID de `Luma CRM Dataset` del cuerpo de respuesta
   ![Obtener el ID del conjunto de datos](assets/ingestion-crm-getDatasetId.png)

### Crear el lote

Ahora podemos crear un lote en el conjunto de datos:

1. Descargar [API de ingesta de datos.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json) en la carpeta `Luma Tutorial Assets`
1. Importar la colección en [!DNL Postman]
1. Seleccionar la solicitud **[!DNL Data Ingestion API > Batch Ingestion > Create a new batch in Catalog Service.]**
1. Pegue lo siguiente como **Cuerpo** de la solicitud, ***reemplazando el valor datasetId por el suyo propio***:

   ```json
   {
       "datasetId":"REPLACE_WITH_YOUR_OWN_DATASETID",
       "inputFormat": {
           "format": "json"
       }
   }
   ```

1. Seleccione el botón **Enviar**
1. Debe obtener una respuesta 201 Created que contenga el ID del nuevo lote.
1. Copiar `id` del nuevo lote
   ![Lote Creado](assets/ingestion-crm-createBatch.png)

### Ingesta de datos

Ahora podemos cargar los datos en el lote:

1. Seleccionar la solicitud **[!DNL Data Ingestion API > Batch Ingestion > Upload a file to a dataset in a batch.]**
1. En la pestaña **Params**, introduzca la ID del conjunto de datos y la ID de lote en sus campos respectivos
1. En la ficha **Params**, escriba `luma-crm.json` como **rutaDeAccesoDeArchivo**
1. En la ficha **Cuerpo**, seleccione la opción **binario**
1. Seleccione el(a) `luma-crm.json` descargado(a) de su carpeta `Luma Tutorial Assets` local
1. Seleccione **Send** y debería obtener una respuesta de 200 OK con &#39;1&#39; en el cuerpo de la respuesta

   ![Datos cargados](assets/ingestion-crm-uploadFile.png)

En este punto, si observa el lote en la interfaz de usuario de Platform, verá que está en estado &quot;[!UICONTROL Cargando]&quot;:
![Carga por lotes](assets/ingestion-crm-loading.png)

Dado que la API por lotes se utiliza a menudo para cargar varios archivos, debe informar a Platform cuando se complete un lote, lo que haremos en el siguiente paso.

### Completar el lote

Para completar el lote:

1. Seleccionar la solicitud **[!DNL Data Ingestion API > Batch Ingestion > Finish uploading a file to a dataset in a batch.]**
1. En la ficha **Parámetros**, escriba `COMPLETE` como **acción**
1. En la pestaña **Params**, ingrese su ID de lote. No se preocupe por el ID del conjunto de datos o la ruta de archivo, si están presentes.
1. Asegúrese de que la dirección URL de la publicación sea `https://platform.adobe.io/data/foundation/import/batches/:batchId?action=COMPLETE` y de que no haya referencias innecesarias a `datasetId` o `filePath`
1. Seleccione **Send** y debería obtener una respuesta de 200 OK con &#39;1&#39; en el cuerpo de la respuesta

   ![Lote completado](assets/ingestion-crm-complete.png)

### Validación de los datos

#### Validación en la interfaz de usuario de Platform

Valide que los datos hayan aterrizado en la interfaz de usuario de Platform como lo hizo para el conjunto de datos de Fidelidad.

En primer lugar, confirme que el lote muestra que se han introducido 1000 registros:

![Éxito en lote](assets/ingestion-crm-success.png)

A continuación, confirme el lote mediante Vista previa del conjunto de datos:

![Vista previa por lotes](assets/ingestion-crm-preview.png)

Por último, confirme que uno de sus perfiles se ha creado buscando uno en el área de nombres `Luma CRM Id`, por ejemplo `112ca06ed53d3db37e4cea49cc45b71e`

![Perfil ingerido](assets/ingestion-crm-profile.png)

Hay una cosa interesante que acaba de pasar que quiero señalar. Abra ese perfil `Danny Wright`. El perfil tiene `Lumacrmid` y `Lumaloyaltyid`. Recuerde que `Luma Loyalty Schema` contenía dos campos de identidad, ID de fidelidad de Luma e ID de CRM. Ahora que hemos cargado ambos conjuntos de datos, se han combinado en un solo perfil. Los datos de fidelización tenían `Daniel` como nombre y &quot;Ciudad de Nueva York&quot; como dirección particular, mientras que los datos de CRM tenían `Danny` como nombre y `Portland` como dirección particular del cliente con el mismo ID de fidelización. Volveremos a explicar por qué el nombre muestra `Danny` en la lección sobre las políticas de combinación.

¡Enhorabuena, acaba de combinar perfiles!

![Perfil combinado ](assets/ingestion-crm-profileLinkedIdentities.png)

#### Validación con eventos de ingesta de datos

Si se ha suscrito a los eventos de ingesta de datos de la lección anterior, compruebe la dirección URL única de webhook.site. Debería ver tres solicitudes, igual que con los datos de fidelidad:

![webhook de ingesta de datos](assets/ingestion-crm-webhook.png)

Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html?lang=es#available-status-notification-events) para obtener más información sobre las notificaciones.

## Ingesta de datos con flujos de trabajo

Veamos otra forma de cargar los datos. La función de flujos de trabajo permite introducir datos CSV que aún no están modelados en XDM.

### Descargue y prepare los datos

1. Ya debería haber descargado y descomprimido [luma-data.zip](assets/luma-data.zip) en su carpeta `Luma Tutorial Assets`.
1. Confirme que tiene `luma-products.csv`

### Creación de un flujo de trabajo

Ahora vamos a configurar el flujo de trabajo:

1. Vaya a **[!UICONTROL Flujos de trabajo]** en el panel de navegación izquierdo
1. Seleccione **[!UICONTROL Asignar CSV al esquema XDM]** y seleccione el botón **[!UICONTROL Iniciar]**
   ![Iniciar el flujo de trabajo](assets/ingestion-products-launchWorkflow.png)
1. Seleccione su `Luma Product Catalog Dataset` y seleccione el botón **[!UICONTROL Siguiente]**
   ![Seleccione su conjunto de datos](assets/ingestion-products-selectDataset.png)
1. Agregue el archivo `luma-products.csv` que descargó y seleccione el botón **[!UICONTROL Siguiente]**
   ![Seleccione su conjunto de datos](assets/ingestion-products-selectData.png)
1. Ahora se encuentra en la interfaz del asignador, en la que puede asignar un campo desde los datos de origen (uno de los nombres de columna del archivo `luma-products.csv`) a los campos XDM del esquema de destino. En nuestro ejemplo, los nombres de columna están lo suficientemente cerca de los nombres de campo de esquema que el asignador puede detectar automáticamente la asignación correcta. Si el asignador no pudiera detectar automáticamente el campo derecho, seleccionaría el icono a la derecha del campo de destino para seleccionar el campo XDM correcto. Además, si no desea introducir una de las columnas del CSV, puede eliminar la fila del asignador. No dude en jugar y cambiar los encabezados de columna en `luma-products.csv` para familiarizarse con el funcionamiento del asignador.
1. Seleccione el botón **[!UICONTROL Finalizar]**
   ![Seleccione su conjunto de datos](assets/ingestion-products-mapper.png)

### Validación de los datos

Cuando se haya cargado el lote, compruebe la carga previsualizando el conjunto de datos.

Dado que `Luma Product SKU` es un área de nombres que no es de personas, no veremos ningún perfil para los códigos de artículo del producto.

Debería ver las tres visitas a su webhook.

## Ingesta de datos con orígenes

Bien, hiciste las cosas de la manera difícil. ¡Ahora pasemos a la tierra prometida de la ingesta por lotes de _automated_! Cuando digo: &quot;¡PONLO!&quot; tú dices: &quot;¡OLVÍDALO!&quot; &quot;¡PONLO!&quot; &quot;¡OLVÍDALO!&quot; &quot;¡PONLO!&quot; &quot;¡OLVÍDALO!&quot; Solo bromeaba, ¡nunca harías algo así! Ok, de vuelta al trabajo. Ya casi has terminado.

Vaya a **[!UICONTROL Sources]** en el panel de navegación izquierdo para abrir el catálogo de Sources. Aquí verá varias integraciones listas para usar con los proveedores de datos y almacenamiento líderes en el sector.

![catálogo de Source](assets/ingestion-offline-sourceCatalog.png)

Bien, vamos a ingerir datos usando un conector de origen.

Este ejercicio será elegir-su-propio-estilo de aventura. Voy a mostrar el flujo de trabajo mediante el conector de origen FTP. Puede utilizar un conector de origen de Cloud Storage diferente que utilice en su empresa o cargar el archivo json mediante la interfaz de usuario del conjunto de datos, como hicimos con los datos de fidelidad.

Muchos de los orígenes tienen un flujo de trabajo de configuración similar, en el que:

1. Introduzca los detalles de autenticación
1. Seleccione los datos que desea introducir
1. Seleccione el conjunto de datos de Platform en el que desea introducirlo
1. Asignar los campos al esquema XDM
1. Elija la frecuencia con la que desea volver a ingerir datos desde esa ubicación

>[!NOTE]
>
>Los datos de compra sin conexión que utilizaremos en este ejercicio contienen datos de fecha y hora. Los datos de fecha y hora deben estar en [cadenas con formato ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) o Tiempo Unix formateado en milisegundos (1531263959000) y se convierten en el momento de la ingesta al tipo XDM de destino. Para obtener más información sobre la conversión de datos y otras restricciones, consulte [la documentación de la API de ingesta por lotes](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/api-overview.html?lang=es#types).

### Descargue, prepare y cargue los datos a su proveedor de almacenamiento en la nube preferido

1. Ya debería haber descargado y descomprimido [luma-data.zip](assets/luma-data.zip) en su carpeta `Luma Tutorial Assets`.
1. Abra `luma-offline-purchases.json` en un editor de texto y reemplace todas las instancias de `_techmarketingdemos` con su propio id. de inquilino de guion bajo, tal como se ve en los esquemas
1. Actualice todas las marcas de tiempo para que los eventos se produzcan en el último mes (por ejemplo, busque `"timestamp":"2022-06` y reemplace el año y el mes)
1. Elija su proveedor de almacenamiento en la nube preferido, asegurándose de que esté disponible en el catálogo [!UICONTROL Sources]
1. Cargue `luma-offline-purchases.json` a una ubicación de su proveedor de almacenamiento en la nube preferido

### Ingeste los datos en su ubicación de almacenamiento en la nube preferida

1. En la interfaz de usuario de Platform, filtre el catálogo [!UICONTROL Sources] a **[!UICONTROL Cloud Storage]**
1. Tenga en cuenta que hay vínculos prácticos a la documentación en `...`
1. En el cuadro de su proveedor de almacenamiento de nube preferido, seleccione el botón **[!UICONTROL Configurar]**
   ![Seleccionar configuración](assets/ingestion-offline-selectFTP.png)
1. **[!UICONTROL Autenticación]** es el primer paso. Escriba el nombre de su cuenta, por ejemplo `Luma's FTP Account` y los detalles de autenticación. Este paso debería ser bastante similar para todas las fuentes de almacenamiento en la nube, aunque los campos pueden variar ligeramente. Una vez que haya especificado los detalles de autenticación de una cuenta, puede reutilizarlos para otras conexiones de origen que podrían estar enviando datos diferentes en programaciones diferentes de otros archivos de la misma cuenta
1. Seleccione el **[!UICONTROL botón Conectar a origen]**
1. Cuando Platform se haya conectado correctamente a Source, seleccione el botón **[!UICONTROL Siguiente]**
   ![Autenticar con el origen](assets/ingestion-offline-authentication.png)

1. En el paso **[!UICONTROL Seleccionar datos]**, la interfaz de usuario usará sus credenciales para abrir la carpeta en su solución de almacenamiento en la nube
1. Seleccione los archivos que desea introducir, por ejemplo `luma-offline-purchases.json`
1. Como **[!UICONTROL formato de datos]**, seleccione `XDM JSON`
1. A continuación, puede obtener una vista previa de la estructura json y de los datos de ejemplo en el archivo
1. Seleccione el botón **[!UICONTROL Siguiente]**
   ![Seleccione sus archivos de datos](assets/ingestion-offline-selectData.png)

1. En el paso **[!UICONTROL Asignación]**, seleccione su `Luma Offline Purchase Events Dataset` y seleccione el botón **[!UICONTROL Siguiente]**. Tenga en cuenta en el mensaje que, como los datos que estamos ingiriendo son un archivo JSON, no hay ningún paso de asignación en el que asignemos el campo de origen al campo de destino. Los datos JSON ya deben estar en XDM. Si estuviera introduciendo un CSV, vería la interfaz de usuario de asignación completa en este paso:
   ![Seleccione su conjunto de datos](assets/ingestion-offline-mapping.png)
1. En el paso **[!UICONTROL Programación]**, elija la frecuencia con la que desea volver a ingerir datos desde Source. Dedique un momento a ver las opciones. Solo vamos a hacer una ingesta única, así que deja la **[!UICONTROL Frecuencia]** en **[!UICONTROL Una vez]** y selecciona el botón **[!UICONTROL Siguiente]**:
   ![Programar el flujo de datos](assets/ingestion-offline-scheduling.png)
1. En el paso **[!UICONTROL Detalle del flujo de datos]**, puede elegir un nombre para el flujo de datos, escribir una descripción opcional, activar los diagnósticos de error y la ingesta parcial. Deje la configuración tal cual y seleccione el botón **[!UICONTROL Siguiente]**:
   ![Editar detalles de su flujo de datos](assets/ingestion-offline-detail.png)
1. En el paso **[!UICONTROL Revisar]**, puedes revisar todos tus ajustes juntos y editarlos o seleccionar el botón **[!UICONTROL Finalizar]**
1. Después de guardar, aterrizará en una pantalla como esta:
   ![Completado](assets/ingestion-offline-complete.png)

### Validación de los datos

Cuando se haya cargado el lote, compruebe la carga previsualizando el conjunto de datos.

Debería ver las tres visitas a su webhook.

Vuelva a buscar el perfil con valor `5625458` en el área de nombres `loyaltyId` para ver si hay algún evento de compra en su perfil. Debería ver una compra. Para ver los detalles de la compra, selecciona **[!UICONTROL Ver JSON]**:

![Evento de compra en el perfil](assets/ingestion-offline-eventInProfile.png)

## Herramientas de ETL

Adobe se asocia con varios proveedores de ETL para admitir la ingesta de datos en Experience Platform. Debido a la variedad de proveedores externos, ETL no se trata en este tutorial, aunque puede revisar algunos de estos recursos:

* [Desarrollar integraciones de ETL para Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/etl/home.html?lang=es)
* [[!DNL Snaplogic] Paquete de instantáneas de Adobe Experience Platform](https://www.snaplogic.com/resources/videos/august-2020-aep)

## Recursos adicionales

* [Documentación de ingesta por lotes](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=es)
* [Referencia de API de ingesta por lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)

Ahora vamos a [transmitir datos usando Web SDK](ingest-streaming-data.md)
