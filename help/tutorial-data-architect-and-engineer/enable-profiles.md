---
title: Habilitar perfiles de cliente en tiempo real
seo-title: Enable Real-Time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Habilitar perfiles de cliente en tiempo real
description: En esta lección, debe habilitar sus esquemas y conjuntos de datos para el perfil del cliente en tiempo real.
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---

# Habilitar perfiles de cliente en tiempo real

<!-- 15min-->
En esta lección, debe habilitar sus esquemas y conjuntos de datos para el perfil del cliente en tiempo real.

Bueno, mentí cuando dije que la lección de conjuntos de datos era la lección más corta en este tutorial, ¡este debería tomar incluso menos tiempo! Literalmente, todo lo que vas a hacer es voltear un montón de toggles. Pero lo que sucede cuando se voltean estas gafas es _real_ importante, así que quería dedicarle una página entera.

Con Perfil del cliente en tiempo real, puede ver una vista completa de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar sus diferentes datos de clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

Por increíble que suene todo eso, no necesita activarse *todos sus datos* para perfil. De hecho, solo debe habilitar los datos necesarios para los casos de uso de activación. Habilite los datos que desee utilizar para casos de uso de marketing, integraciones de centros de llamadas, etc., donde necesite un acceso rápido a un perfil de cliente sólido. Si está cargando datos solo para análisis, probablemente no debería habilitarse para el perfil.

Hay [protecciones para datos del perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) que debe revisar al decidir cuál de sus propios datos debe habilitar para el perfil.

<!--is this accurate. Are there other considerations to point out? -->

**Arquitectos de datos** necesitará habilitar Perfil del cliente en tiempo real fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre el Perfil del cliente en tiempo real:
>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&learn=on)

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) , configure todos los controles de acceso necesarios para completar esta lección.


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Activación de esquemas para el perfil del cliente en tiempo real mediante la interfaz de usuario de Platform

Comencemos con la simple tarea de habilitar un esquema:

1. En la interfaz de usuario de Platform, abra el **Esquema de lealtad de Luma**
1. En **[!UICONTROL Propiedades del esquema]**, active la casilla **Perfil** switch
1. En el modo de confirmación, pulse la tecla **[!UICONTROL Habilitar]** botón para confirmar
1. Seleccione el **[!UICONTROL Guardar]** para guardar los cambios

   >[!IMPORTANT]
   >
   >Una vez que un esquema está habilitado para Perfil, no se puede deshabilitar ni eliminar. Además, los campos no se pueden eliminar del esquema después de este punto. Estas implicaciones son importantes de tener en cuenta más adelante cuando trabaje con sus propios datos en su entorno de producción. Debe utilizar un simulador para pruebas de desarrollo en este tutorial, que se puede eliminar en cualquier momento.
   >
   >En el entorno controlado de este tutorial, habilitará sus esquemas y conjuntos de datos para el perfil, _antes de ingerir datos_. Al trabajar con sus propios datos, le recomendamos que haga las cosas en el siguiente orden:
   >
   > 1. En primer lugar, incorpore algunos datos en sus conjuntos de datos.
   > 1. Solucione cualquier problema que surja durante el proceso de consumo de datos (por ejemplo, problemas de validación o asignación de datos).
   > 1. Habilitar los conjuntos de datos y esquemas para el perfil
   > 1. Reingesta de datos



   ![Alternar perfil](assets/profile-loyalty-enableSchema.png)

Fácil, ¿verdad? Repita los pasos anteriores para este otro esquema:

1. Esquema del catálogo de productos de Luma
1. Esquema de eventos de compra sin conexión de Luma
1. Esquema de eventos web de Luma (en el modal de confirmación, marque la casilla &quot;Los datos de este esquema contendrán una identidad principal en el campo identityMap&quot;).

## Activación de esquemas para el perfil del cliente en tiempo real mediante la API de plataforma

Ahora, es hora de habilitar el `Luma CRM Schema` con la API. Si desea omitir este ejercicio y habilitarlo en la interfaz de usuario, continúe.

### Obtener el meta:altId del esquema

Primero veamos el `meta:altId` del `Luma CRM Schema`:

1. Abrir [!DNL Postman]
1. Si no ha realizado una solicitud en las últimas 24 horas, es probable que los tokens de autorización hayan caducado. Abra la solicitud **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** y seleccione **Enviar** para solicitar nuevos tokens de acceso y JWT, como hizo en la [!DNL Postman] lección.
1. Abra la solicitud **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Seleccione el **Enviar** botón
1. Debe obtener una respuesta de 200
1. Busque en la respuesta para la variable `Luma CRM Schema` y copie el `meta:altId` value
   ![Copiar meta:altIid](assets/profile-crm-getMetaAltId.png)

### Habilitar el esquema

Ahora que tenemos el meta:altId del esquema, podemos habilitarlo para el perfil:

1. Abra la solicitud **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. En el **Parámetros** pegue su `meta:altId` como `SCHEMA_ID` valor de parámetro
1. En el **Cuerpo** , pegue el siguiente código

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. Seleccione el **Enviar** botón
1. Debe obtener una respuesta de 200

   ![Habilite el esquema CRM para el perfil con su meta:altIid personalizado utilizado como parámetro SCHEMA_ID](assets/profile-crm-enableProfile.png)

Debería poder ver en la interfaz de usuario que los cinco esquemas están habilitados para Perfil (es posible que necesite MAYÚS-Recargar para ver que `Luma CRM Schema` está habilitado):
![Todos los esquemas habilitados](assets/profile-allSchemasEnabled.png)


## Habilitar conjuntos de datos para el perfil del cliente en tiempo real mediante la interfaz de usuario de Platform

Los conjuntos de datos también deben habilitarse para Perfil y el proceso es aún más sencillo:

1. En la interfaz de usuario de Platform, abra el `Luma Loyalty Dataset`
1. Alternar el **[!UICONTROL Perfil]** switch
1. En el modo de confirmación, pulse la tecla **[!UICONTROL Habilitar]** botón para confirmar

   ![ Alternar perfil](assets/profile-loyalty-enableDataset.png)

Repita los pasos anteriores para estos otros conjuntos de datos:

1. Conjunto de datos del catálogo de productos de Luma
1. Conjunto de datos de eventos de compra sin conexión de Luma
1. Conjunto de datos de eventos web de Luma

>[!NOTE]
>
>A diferencia de los esquemas, puede deshabilitar los conjuntos de datos de Perfil, pero todos los datos introducidos anteriormente permanecerán en Perfil.

## Habilitar conjuntos de datos para el perfil del cliente en tiempo real mediante la API de plataforma

Ahora habilitará un conjunto de datos para Perfil mediante la API. De nuevo, si desea habilitarlo a través de la interfaz de usuario utilizando el método anterior, también está bien.

### Obtención del id del conjunto de datos

Primero tenemos que conseguir el `id` del `Luma CRM Dataset`:

1. Abrir [!DNL Postman]
1. Si no ha realizado una solicitud en las últimas 24 horas, es probable que los tokens de autorización hayan caducado. Abra la solicitud **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** y seleccione **Enviar** para solicitar nuevos tokens de acceso y JWT, como hizo en la [!DNL Postman] lección.
1. Abra la solicitud **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. Seleccione el **Enviar** botón
1. Debe obtener una respuesta de 200
1. Busque en la respuesta para la variable `Luma CRM Dataset` y copie el id:
   ![Copiar el id](assets/profile-crm-copyDatasetId.png)

### Habilitar el conjunto de datos

Ahora que tenemos el id del conjunto de datos, podemos habilitarlo para el perfil:

1. Abra la solicitud **[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. En el **Parámetros** actualice el `DATASET_ID` a su propio valor
1. En el **Cuerpo** pegue el siguiente código. Tenga en cuenta que los dos primeros valores son etiquetas preexistentes que son visibles en la respuesta anterior. Deben incluirse en el cuerpo, además de las dos nuevas etiquetas que estamos agregando:

   ```json
   {
       "tags":{
           "adobe/pqs/table":["luma_crm_dataset"],
           "adobe/siphon/table/format":["parquet"],
           "unifiedProfile":["enabled:true"],
           "unifiedIdentity":["enabled:true"]
           }
   }
   ```

1. Seleccione el **Enviar** botón
1. Debe obtener una respuesta de 200

   ![Habilite el conjunto de datos CRM para el perfil, asegurándose de usar su id de conjunto de datos personalizado como parámetro DATASET_ID](assets/profile-crm-enableDataset.png)

También puede confirmar que la interfaz de usuario muestra el conjunto de datos habilitado:
![Confirmar](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> Si incorpora datos antes de habilitar el esquema y el conjunto de datos para el perfil, tendrá que volver a introducir esos datos más adelante.

## Recursos adicionales

* [Documentación del perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=es)
* [Referencia de la API del perfil del cliente en tiempo real](https://www.adobe.io/experience-platform-apis/references/profile/)


**Ingenieros de datos** debe continuar con el [Suscripción a eventos de ingesta de datos](subscribe-to-data-ingestion-events.md) lección.
**Arquitectos de datos** _puede adelantarse_ y vaya a [lección de ingesta por lotes](ingest-batch-data.md).
