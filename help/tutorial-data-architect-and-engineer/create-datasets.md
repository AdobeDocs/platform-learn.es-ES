---
title: Crear conjuntos de datos
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Crear conjuntos de datos
description: En esta lección, creará conjuntos de datos para recibir sus datos.
role: Data Architect, Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 8%

---

# Crear conjuntos de datos

<!--15min-->

En esta lección, creará conjuntos de datos para recibir sus datos. Le encantará saber que esta es la lección más corta del tutorial.

Todos los datos que se incorporan correctamente en Adobe Experience Platform se conservan en el lago de datos como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

**Arquitectos de datos** necesitará crear conjuntos de datos fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre los conjuntos de datos:
>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) , configure todos los controles de acceso necesarios para completar esta lección.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Crear conjuntos de datos en la interfaz de usuario

En este ejercicio, crearemos conjuntos de datos en la interfaz de usuario. Empecemos con los datos de lealtad:

1. Vaya a **[!UICONTROL Conjuntos de datos]** en la navegación izquierda de la interfaz de usuario de Platform
1. Seleccione el **[!UICONTROL Crear conjunto de datos]** botón
   ![Crear un conjunto de datos](assets/datasets-createDataset.png)

1. En la siguiente pantalla, seleccione **Crear conjunto de datos a partir del esquema**
1. En la siguiente pantalla, seleccione su `Luma Loyalty Schema` y, a continuación, seleccione **[!UICONTROL Siguiente]** botón
   ![Seleccionar el conjunto de datos](assets/datasets-selectSchema.png)

1. Asigne un nombre al conjunto de datos `Luma Loyalty Dataset` y seleccione **[!UICONTROL Finalizar]** botón
   ![Asigne un nombre al conjunto de datos](assets/datasets-nameDataset.png)
1. Cuando el conjunto de datos se haya guardado, se le dirigirá a una pantalla como esta:
   ![Conjunto de datos creado](assets/datasets-created.png)

¡Ya está! Te dije que esto iba a ser rápido. Cree estos otros conjuntos de datos siguiendo los mismos pasos:

1. `Luma Offline Purchase Events Dataset` para su `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` para su `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` para su `Luma Product Catalog Schema`


## Creación de un conjunto de datos mediante API

Ahora cree el `Luma CRM Dataset` usando la API .

>[!NOTE]
>
>Si desea omitir el ejercicio de API y crear la variable `Luma CRM Dataset` en la interfaz de usuario que está bien. Asigne un nombre `Luma CRM Dataset` y utilice el `Luma CRM Schema`.

### Obtenga el id del esquema que se utilizará en el conjunto de datos

Primero tenemos que conseguir el `$id` del `Luma CRM Schema`:

1. Abrir [!DNL Postman]
1. Si no ha realizado una solicitud en las últimas 24 horas, es probable que los tokens de autorización hayan caducado. Abra la solicitud **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** y seleccione **Enviar** para solicitar nuevos tokens de acceso y JWT, como hizo en la [!DNL Postman] lección.
1. Abra la solicitud **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Seleccione el **Enviar** botón
1. Debe obtener una respuesta de 200
1. Busque en la respuesta para la variable `Luma CRM Schema` y copie el `$id` value
   ![Copiar el $id](assets/dataset-crm-getSchemaId.png)

### Crear el conjunto de datos

Ahora puede crear el conjunto de datos:

1. Descargar [API del servicio de catálogo.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) a su `Luma Tutorial Assets` carpeta.
1. Importar la colección en [!DNL Postman]
1. Seleccione la solicitud **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. Pegue lo siguiente como **Cuerpo** de la solicitud, ***sustituir el valor de id por el suyo propio***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. Seleccione el **Enviar** botón
1. Debe obtener una respuesta de 201 Created que contenga el id del nuevo conjunto de datos.
   ![Conjunto de datos creado con API, su $id personalizado utilizado en el cuerpo](assets/datasets-crm-created.png)

>[!TIP]
>
> Problemas comunes que hacen esta solicitud y posibles correcciones:
>
> * `400: There was a problem retrieving xdm schema`. Asegúrese de haber reemplazado el id en el ejemplo anterior con el id propio `Luma CRM Schema`
> * Sin token de autenticación: Ejecute el **IMS: Generación + autenticación de JWT mediante token de usuario** llamada para generar nuevos tokens
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: Actualice el **CONTAINER_ID** variable de entorno desde `global` a `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Verificar los permisos de usuario en el Admin Console



Puede volver al **[!UICONTROL Conjuntos de datos]** en la interfaz de usuario de Platform, puede verificar la creación correcta de los cinco conjuntos de datos.
![Cinco conjuntos de datos completados](assets/datasets-allComplete.png)


## Recursos adicionales

* [Documentación de conjuntos de datos](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=es)
* [Referencia de la API de conjuntos de datos (parte del servicio de catálogo)](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

Ahora que todos nuestros esquemas, identidades y conjuntos de datos están establecidos, podemos [habilitarlos para el perfil del cliente en tiempo real](enable-profiles.md).
