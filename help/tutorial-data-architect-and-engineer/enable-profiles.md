---
title: Activar perfiles de cliente en tiempo real
seo-title: Enable Real-Time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Activar perfiles de cliente en tiempo real
description: En esta lección, debe habilitar los esquemas y conjuntos de datos para el Perfil del cliente en tiempo real.
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 0%

---

# Activar perfiles de cliente en tiempo real

<!-- 15min-->
En esta lección, debe habilitar los esquemas y conjuntos de datos para el Perfil del cliente en tiempo real.

Vale, mentí cuando dije que la lección de los conjuntos de datos era la lección más corta de este tutorial: ¡esta debería tardar aún menos tiempo! Literalmente, todo lo que vas a hacer es dar la vuelta a un montón de toggles. Pero lo que pasa cuando cambias estos toggles es _de verdad_ importante, por lo que quería dedicarle una página entera.

Con el Perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los distintos datos de clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

Tan increíble como todo lo que suena, no es necesario activar *todos los datos* para el perfil. De hecho, solo debe habilitar los datos que necesite para casos de uso de activación. Habilite los datos que desee utilizar para casos de uso de marketing, integraciones de centros de llamadas, etc., en los que necesite un acceso rápido a un perfil de cliente sólido. Si solo carga datos para su análisis, probablemente no debería habilitarse para el perfil.

Hay cosas importantes [protecciones para datos del perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) que debe revisar al decidir cuál de sus propios datos debe habilitar para el perfil.

<!--is this accurate. Are there other considerations to point out? -->

**Arquitectos de datos** Necesitará habilitar el Perfil del cliente en tiempo real fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información acerca del Perfil del cliente en tiempo real:
>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&learn=on)

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) Esta lección, ha configurado todos los controles de acceso necesarios para completar esta lección.


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Activación de esquemas para el perfil del cliente en tiempo real mediante la interfaz de usuario de Platform

Empecemos con la sencilla tarea de habilitar un esquema:

1. En la interfaz de usuario de Platform, abra **Esquema de fidelización de Luma**
1. Entrada **[!UICONTROL Propiedades del esquema]**, cambie el **Perfil** cambiar
1. En el modal de confirmación, pulse la tecla **[!UICONTROL Activar]** para confirmar
1. Seleccione el **[!UICONTROL Guardar]** para guardar los cambios

   >[!IMPORTANT]
   >
   >Una vez que un esquema está habilitado para el perfil, no se puede deshabilitar ni eliminar. Además, los campos no se pueden eliminar del esquema después de este punto. Estas implicaciones son importantes que se deben tener en cuenta más adelante cuando trabaje con sus propios datos en el entorno de producción. Debe utilizar una zona protegida de desarrollo en este tutorial, que se puede eliminar en cualquier momento.
   >
   >En el entorno controlado de este tutorial, habilitará los esquemas y conjuntos de datos para el perfil, _antes de ingerir datos_. Al trabajar con sus propios datos, le recomendamos que haga las cosas en el siguiente orden:
   >
   > 1. En primer lugar, introduzca algunos datos en los conjuntos de datos.
   > 1. Solucionar cualquier problema que surja durante el proceso de ingesta de datos (por ejemplo, problemas de validación o asignación de datos).
   > 1. Habilitar los conjuntos de datos y esquemas para el perfil
   > 1. Reingesta de datos


   ![Alternancia de perfil](assets/profile-loyalty-enableSchema.png)

Fácil, ¿verdad? Repita los pasos anteriores para este otro esquema:

1. Esquema del catálogo de productos Luma
1. Esquema de eventos de compra sin conexión de Luma
1. Esquema de eventos web de Luma (en el modal de confirmación, marque la casilla &quot;Los datos de este esquema contendrán una identidad principal en el campo identityMap&quot;).

## Habilitar esquemas para el perfil del cliente en tiempo real mediante la API de Platform

Ahora, es el momento de habilitar el `Luma CRM Schema` con la API de. Si desea omitir este ejercicio y simplemente habilitarlo en la interfaz de usuario, continúe.

### Obtener el meta:altId del esquema

Primero vamos a por el `meta:altId` de la `Luma CRM Schema`:

1. Abrir [!DNL Postman]
1. Si no tiene un token de acceso, abra la solicitud **[!DNL OAuth: Request Access Token]** y seleccione **Enviar** para solicitar un nuevo token de acceso, como hizo en el [!DNL Postman] lección.
1. Abrir la solicitud **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Seleccione el **Enviar** botón
1. Deberías obtener una respuesta de 200
1. Busque en la respuesta de `Luma CRM Schema` y copie el `meta:altId` valor
   ![Copie el meta:altId](assets/profile-crm-getMetaAltId.png)

### Habilitar el esquema

Ahora que tenemos el meta:altId del esquema, podemos habilitarlo para el perfil:

1. Abrir la solicitud **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. En el **Parámetros** pegue su `meta:altId` valor como `SCHEMA_ID` valor de parámetro
1. En el **Cuerpo** , pegue el siguiente código

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. Seleccione el **Enviar** botón
1. Deberías obtener una respuesta de 200

   ![Habilite el esquema CRM para el perfil con el meta:altId personalizado utilizado como parámetro SCHEMA_ID](assets/profile-crm-enableProfile.png)

Debería poder ver en la interfaz de usuario que los cinco esquemas están habilitados para el perfil (es posible que tenga que MAYÚS-Recargar para verlo) `Luma CRM Schema` está activada):
![Todos los esquemas habilitados](assets/profile-allSchemasEnabled.png)


## Habilitar conjuntos de datos para el perfil del cliente en tiempo real mediante la interfaz de usuario de Platform

Los conjuntos de datos también deben habilitarse para el perfil y el proceso es aún más sencillo:

1. En la interfaz de usuario de Platform, abra `Luma Loyalty Dataset`
1. Alternar el **[!UICONTROL Perfil]** cambiar
1. En el modal de confirmación, pulse la tecla **[!UICONTROL Activar]** para confirmar

   ![ Alternancia de perfil](assets/profile-loyalty-enableDataset.png)

Repita los pasos anteriores para estos otros conjuntos de datos:

1. Conjunto de datos del catálogo de productos Luma
1. Conjunto de datos de eventos de compra sin conexión de Luma
1. Conjunto de datos de eventos web de Luma

>[!NOTE]
>
>A diferencia de los esquemas, puede deshabilitar los conjuntos de datos del perfil, aunque todos los datos ingeridos anteriormente permanecerán en el perfil.

## Habilitar conjuntos de datos para el perfil del cliente en tiempo real mediante la API de Platform

Ahora habilitará un conjunto de datos para el perfil mediante la API. De nuevo, si desea habilitarlo a través de la interfaz de usuario con el método anterior, también está bien.

### Obtener el ID del conjunto de datos

Primero tenemos que conseguir el `id` de la `Luma CRM Dataset`:

1. Abrir [!DNL Postman]
1. Si no tiene un token de acceso, abra la solicitud **[!DNL OAuth: Request Access Token]** y seleccione **Enviar** para solicitar un nuevo token de acceso, como hizo en el [!DNL Postman] lección.
1. Abrir la solicitud **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. Seleccione el **Enviar** botón
1. Deberías obtener una respuesta de 200
1. Busque en la respuesta de `Luma CRM Dataset` y copie el id:
   ![Copiar el ID](assets/profile-crm-copyDatasetId.png)

### Habilitar el conjunto de datos

Ahora que tenemos el ID del conjunto de datos, podemos habilitarlo para el perfil:

1. Abrir la solicitud **[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. En el **Parámetros** actualice el `DATASET_ID` valor para los suyos propios
1. En el **Cuerpo** , pegue el siguiente código. Tenga en cuenta que los dos primeros valores son etiquetas preexistentes visibles en la respuesta anterior. Deben incluirse en el cuerpo, además de las dos nuevas etiquetas que estamos añadiendo:

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
1. Deberías obtener una respuesta de 200

   ![Habilite el conjunto de datos CRM para el perfil, asegurándose de utilizar su ID de conjunto de datos personalizado como parámetro DATASET_ID](assets/profile-crm-enableDataset.png)

También puede confirmar que la interfaz de usuario muestra el conjunto de datos habilitado:
![Confirmar](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> Si introduce datos antes de habilitar el esquema y el conjunto de datos para el perfil, deberá volver a introducir esos datos más tarde.

## Recursos adicionales

* [Documentación del Perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=es)
* [Referencia de la API del perfil del cliente en tiempo real](https://www.adobe.io/experience-platform-apis/references/profile/)


**Ingenieros de datos** debe continuar a la [Suscripción a eventos de ingesta de datos](subscribe-to-data-ingestion-events.md) lección.
**Arquitectos de datos** _puede saltarse adelante_ y vaya a la [lección de ingesta por lotes](ingest-batch-data.md).
