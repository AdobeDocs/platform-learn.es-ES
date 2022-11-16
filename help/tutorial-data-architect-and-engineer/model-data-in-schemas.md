---
title: Datos de modelo en esquemas
seo-title: Model data in schemas | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Datos de modelo en esquemas
description: En esta lección, modelará los datos de Luma en esquemas. Esta es una de las lecciones más largas del tutorial, por lo que hay que tomar un vaso de agua y ponerte una hebilla.
role: Data Architect
feature: Schemas
kt: 4348
thumbnail: 4348-model-data-in-schemas.jpg
exl-id: 317f1c39-7f76-4074-a246-ef19f044cb85
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2497'
ht-degree: 1%

---

# Datos de modelo en esquemas

<!-- 60min -->
En esta lección, modelará los datos de Luma en esquemas. Esta es una de las lecciones más largas del tutorial, por lo que hay que tomar un vaso de agua y ponerte una hebilla.

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. Experience Data Model (XDM) es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación que se pueda utilizar para comunicarse con los servicios de Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente pueden incorporarse a una representación común que puede proporcionar perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y expresar atributos del cliente con fines de personalización.

XDM es el marco fundamental que permite a Adobe Experience Cloud, con tecnología de Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, exactamente en el momento adecuado. La metodología en la que se basa el Experience Platform, **Sistema XDM**, operacionaliza los esquemas del Modelo de datos de Experience para su uso en los servicios de plataforma.

<!--
This seems too lengthy. The video should suffice

Key terms:

* **Schema**: a representation of your data. A schema is comprised of a class and optional field groups and is used to create datasets. A schema includes behavioral attributes, timestamp, identity, attribute definitions, and relationships.
* **XDM Profile Class**: a common schema class used to represent record data
* **XDM ExperienceEvent Class**: a common schema class used to represent time-series data
* **Field group**: allows users to extend reusable fields that contain variables defining one or more attribute intended to be included in a schema or added to a class.
* **Standard Field group**: an open-source Field group built to conform to common industry standards, used to accelerate implementation and support repeatable services operating on the data
* **Data type**: a reusable object with properties in a hierarchical representation. These can be standard types or custom-defined defined types to describe your own data in your own way (for example, a collection of fields that you use to describe your products). Unlike Field groups, data types can be used in schemas regardless of the class.
* **Field**: a field is the lowest level element of a schema. Each field has a name for referencing and a type to identify the type of data that it contains. Field types can include, integer, number, string, Boolean and schema.
-->

**Arquitectos de datos** necesitará crear esquemas fuera de este tutorial, pero **Ingenieros de datos** trabajará de cerca con los esquemas creados por el arquitecto de datos.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre los esquemas y el modelo de datos de experiencia (XDM):
>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

>[!TIP]
>
> Para profundizar en el modelado de datos en Experience Platform, recomendamos tomar el curso [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm), disponible de forma gratuita en Experience League!

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) , configure todos los controles de acceso necesarios para completar esta lección.

<!--, specifically:

* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)-->


<!--
## Luma's goals
-->

## Crear esquema de fidelidad mediante la interfaz de usuario

En este ejercicio, crearemos un esquema para los datos de lealtad de Luma.

1. Vaya a la interfaz de usuario de Platform y asegúrese de que el simulador de pruebas está seleccionado.
1. Vaya a **[!UICONTROL Esquemas]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Crear esquema]** en la parte superior derecha
1. En el menú desplegable, seleccione **[!UICONTROL Perfil individual XDM]**, ya que modelaremos los atributos de un cliente individual (puntos, estado, etc.).
   ![Esquema con grupo de campos OOTB](assets/schemas-loyaltyCreateSchema.png)

### Agregar grupos de campos estándar

A continuación, se le pedirá que añada grupos de campos al esquema. Todos los campos deben agregarse a esquemas mediante grupos. Puede elegir entre un gran conjunto de grupos de campos estándar del sector proporcionados por Adobe o crear los suyos propios. A medida que empiece a modelar sus propios datos en Experience Platform, es bueno familiarizarse con los grupos de campos estándar del sector que proporciona Adobe. Siempre que sea posible, se recomienda utilizarlos, ya que a veces impulsan servicios descendentes, como Customer AI, Attribution AI y Adobe Analytics.

Al trabajar con sus propios datos, un paso importante será determinar cuál de sus propios datos debe capturarse en Platform y cómo debe modelarse. Este tema tan grande se discute en profundidad en el curso [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm). En este tutorial, solo le guiaré a través de la implementación de algunos esquemas predeterminados.

Para agregar grupos de campos:

1. En el **[!UICONTROL Agregar grupos de campos]** modal, seleccione los siguientes grupos de campos:
   1. **[!UICONTROL Detalles demográficos]** para datos básicos del cliente como nombre y fecha de nacimiento
   1. **[!UICONTROL Detalles de contacto personal]** para detalles de contacto básicos como la dirección de correo electrónico y el número de teléfono
1. Puede obtener una vista previa de los campos contribuidos en el grupo de campos seleccionando el icono en el lado derecho de la fila.
   ![Seleccionar grupos de campos estándar](assets/schemas-loyalty-addFirstTwoFieldGroups.png)

1. Marque la **[!UICONTROL Industria]** > **[!UICONTROL Comercial]** para exponer grupos de campos específicos del sector.
1. Select **[!UICONTROL Fidelidad]** para añadir los campos del programa de fidelidad.
1. Select **[!UICONTROL Agregar grupo de campos]** para agregar los tres grupos de campos al esquema.
   ![Añadir grupos de campos estándar al esquema de lealtad](assets/schemas-loyalty-saveOotbMixins.png)


Ahora, dedique algún tiempo a explorar el estado actual del esquema. Los grupos de campos han agregado campos estándar relacionados con una persona, sus detalles de contacto y el estado del programa de fidelidad. Puede que estos dos grupos de campos resulten útiles al crear esquemas para los datos de su propia empresa. Seleccione una fila de grupo de campos específica o marque la casilla junto al nombre del grupo de campos para ver cómo cambia la visualización.

Para guardar el esquema:

1. Seleccione el nodo superior del esquema.
1. Entrar `Luma Loyalty Schema` como el **[!UICONTROL Nombre para mostrar]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![Asigne un nombre al esquema y guárdelo](assets/schemas-loyalty-nameAndSave.png)

>[!NOTE]
>
>No está mal si un grupo de campos agrega un campo para un punto de datos que no recopila. Por ejemplo, &quot;faxPhone&quot; puede ser un campo para el que Luma no recopila datos. Está bien. Solo porque un campo esté definido en el esquema no significa que los datos para él *must* más adelante.

### Agregar un grupo de campos personalizados

Ahora vamos a crear un grupo de campos personalizado.

Mientras que el grupo de campos de lealtad contenía un `loyaltyID` , Luma desea administrar todos sus identificadores de sistema en un solo grupo para ayudar a garantizar la coherencia en sus esquemas.

Los grupos de campos deben crearse en el flujo de trabajo del esquema. Para crear el grupo de campos:

1. Select **[!UICONTROL Agregar]** en el **[!UICONTROL Grupos de campos de esquema]** encabezado
   ![Añadir un nuevo grupo de campos](assets/schemas-loyalty-addFieldGroup.png)
1. Select **[!UICONTROL Crear nuevo grupo de campos]**
1. Uso `Luma Identity profile field group` como el **[!UICONTROL Nombre para mostrar]**
1. Uso `system identifiers for XDM Individual Profile class` como el **[!UICONTROL Descripción]**
1. Select **[!UICONTROL Agregar grupos de campos]**

   ![Añadir un nuevo grupo de campos](assets/schemas-loyalty-nameFieldGroup.png)

El nuevo grupo de campos vacío se agrega al esquema . La variable **[!UICONTROL +]** para agregar campos nuevos a cualquier ubicación de la jerarquía. En nuestro caso, queremos añadir campos en el nivel raíz:

1. Select **[!UICONTROL +]** junto al nombre del esquema. Esto agrega un nuevo campo en el espacio de nombres del ID del inquilino para administrar los conflictos entre los campos personalizados y cualquier campo estándar.
1. En el **[!UICONTROL Propiedades del campo]** barra lateral añada los detalles del nuevo campo:
   1. **[!UICONTROL Nombre del campo]**: `systemIdentifier`
   1. **[!UICONTROL Nombre para mostrar]**: `System Identifier`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Objeto]**
   1. Select **[!UICONTROL Aplicar]**

   ![Añadir un nuevo grupo de campos](assets/schemas-loyalty-addSystemIdentifier.png)

Ahora agregue dos campos debajo de la variable `systemIdentifier` objeto:

1. Primer campo
   1. **[!UICONTROL Nombre del campo]**: `loyaltyId`
   1. **[!UICONTROL Nombre para mostrar:]** `Loyalty Id`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Cadena]**
1. Segundo campo
   1. **[!UICONTROL Nombre del campo]**: `crmId`
   1. **[!UICONTROL Nombre para mostrar]**: `CRM Id`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Cadena]**

El nuevo grupo de campos debería tener este aspecto. Seleccione el **[!UICONTROL Guardar]** para guardar el esquema, pero deje el esquema abierto para el siguiente ejercicio.
![Finalización del grupo de campos Lealtad](assets/schemas-loyalty-identityFieldGroupComplete.png)

## Crear un tipo de datos

Grupos de campos, como el nuevo `Luma Identity profile field group`, se puede reutilizar en otros esquemas, lo que permite aplicar definiciones de datos estándar en varios sistemas. Pero solo pueden reutilizarse _en esquemas que comparten una clase_, en este caso la clase de perfil individual XDM .

El tipo de datos es otra construcción de varios campos que se puede reutilizar en esquemas _en varias clases_. Vamos a convertir nuestra nueva `systemIdentifier` en un tipo de datos:

Con la variable `Luma Loyalty Schema` aún abierto, seleccione la opción `systemIdentifier` y seleccione  **[!UICONTROL Convertir en nuevo tipo de datos]**

![Finalización del grupo de campos Lealtad](assets/schemas-loyalty-convertToDataType.png)

Si **[!UICONTROL Cancelar]** fuera del esquema y vaya a la **[!UICONTROL Tipos de datos]** , verá el tipo de datos recién creado. Utilizaremos este tipo de datos más adelante en la lección.

![Finalización del grupo de campos Lealtad](assets/schemas-loyalty-confirmDataType.png)


## Crear esquema de CRM mediante API

Ahora crearemos un esquema con la API.

>[!TIP]
>
> Si prefiere omitir el ejercicio API, puede crear el esquema siguiente mediante el método de interfaz de usuario:
>
> 1. Utilice la variable [!UICONTROL Perfil individual XDM] class
> 1. Asigne un nombre `Luma CRM Schema`
> 1. Utilice los siguientes grupos de campos: Detalles demográficos, detalles de contacto personal y grupo de campos de perfil de identidad de Luma


Primero creamos el esquema vacío:

1. Abrir [!DNL Postman]
1. Si no ha realizado una solicitud en las últimas 24 horas, es probable que los tokens de autorización hayan caducado. Abra la solicitud **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** y seleccione **Enviar** para solicitar nuevos tokens de acceso y JWT.
1. Abra las variables de entorno y cambie el valor de **CONTAINER_ID** from `global` a `tenant`. Recuerde que debe usar `tenant` siempre que desee interactuar con sus propios elementos personalizados en Platform, como crear un esquema.
1. Seleccione **Guardar**
   ![Cambiar CONTAINER_ID a inquilino](assets/schemas-crm-changeContainerId.png)
1. Abra la solicitud **[!DNL Schema Registry API > Schemas > Create a new custom schema.]**
1. Abra el **Cuerpo** , pegue el siguiente código y seleccione **Enviar** para realizar la llamada de API. Esta llamada crea un nuevo esquema con el mismo `XDM Individual Profile` clase base:

   ```json
   {
     "type": "object",
     "title": "Luma CRM Schema",
     "description": "Schema for CRM data of Luma Retail ",
     "allOf": [{
       "$ref": "https://ns.adobe.com/xdm/context/profile"
     }]
   }
   ```

   >[!NOTE]
   >
   >El espacio de nombres hace referencia en este y los ejemplos de código posteriores (por ejemplo `https://ns.adobe.com/xdm/context/profile`), se puede obtener utilizando listas de llamadas API con el **[!DNL CONTAINER_ID]** y aceptar el encabezado configurado con los valores correctos. Algunos también son fácilmente accesibles desde la interfaz de usuario.

1. Debería obtener un `201 Created` response
1. Copiar `meta:altId` del cuerpo de respuesta. Lo usaremos más adelante en otro ejercicio.
   ![Creación del esquema CRM](assets/schemas-crm-createSchemaCall.png)

1. El nuevo esquema debe ser visible en la interfaz de usuario, pero sin grupos de campos
   ![Creación del esquema CRM](assets/schemas-loyalty-emptySchemaInTheUI.png)

>[!NOTE]
>
> La variable `meta:altId` o id de esquema también se puede obtener realizando la solicitud de API **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]** con la variable **[!UICONTROL CONTAINER_ID]** configure como `tenant` y un encabezado de aceptación `application/vnd.adobe.xdm+json`.

>[!TIP]
>
> Problemas comunes con esta llamada y posibles correcciones:
>
> * Sin token de autenticación: Ejecute el **IMS: Generación + autenticación de JWT mediante token de usuario** llamada para generar nuevos tokens
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: Actualice el **CONTAINER_ID** variable de entorno desde `global` a `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Verificar los permisos de usuario en el Admin Console


### Agregar grupos de campos estándar

Ahora es el momento de agregar los grupos de campos al esquema:

1. En [!DNL Postman], Abra la solicitud **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. En el **Parámetros** , pegue el `meta:altId` de la respuesta anterior como el valor `SCHEMA_ID`
1. Abra la pestaña Body , pegue el código siguiente y seleccione **Enviar** para realizar la llamada de API. Esta llamada agrega los grupos de campos estándar al `Luma CRM Schema`:

   ```json
   [{
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
       }
     },
     {
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
       }
     }
   ]
   ```

1. Debe obtener un estado 200 OK para la respuesta y los grupos de campos deben ser visibles como parte del esquema en la interfaz de usuario

   ![Se han añadido grupos de campos estándar](assets/schemas-crm-addMixins.png)


### Agregar grupo de campos personalizado

Ahora vamos a agregar nuestra `Luma Identity profile field group` al esquema. En primer lugar, es necesario encontrar el id de nuestro nuevo grupo de campos mediante una API de lista:

1. Abra la solicitud **[!DNL Schema Registry API > Field groups > Retrieve a list of field groups within the specified container.]**
1. Seleccione el **Enviar** para recuperar una lista de todos los grupos de campos personalizados de la cuenta
1. Tome el `$id` del `Luma Identity profile field group` (el suyo será diferente del valor de esta captura de pantalla)
   ![Recuperar la lista de grupos de campos](assets/schemas-crm-getListOfMixins.png)
1. Abra la solicitud **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]** again
1. La variable **Parámetros** debe tener la variable `$id` del esquema
1. Abra el **Cuerpo** y pegue el siguiente código, reemplazando el `$ref` con la variable `$id` de su propia `Luma Identity profile field group`:

   ```json
   [{
     "op": "add",
     "path": "/allOf/-",
     "value": {
       "$ref": "REPLACE_WITH_YOUR_OWN_FIELD_GROUP_ID"
     }
   }]
   ```

1. Select **Enviar**

   ![Adición del grupo Campo de identidad](assets/schemas-crm-addIdentityMixin.png)

Compruebe que el grupo de campos se ha agregado al esquema comprobando tanto la respuesta de API como en la interfaz de .

## Crear esquema de eventos de compra sin conexión

Ahora vamos a crear un esquema basado en el **[!UICONTROL XDM ExperienceEvent]** para los datos de compra sin conexión de Luma. Dado que ahora se está familiarizando con la interfaz de usuario del editor de esquemas, reduciré el número de capturas de pantalla en las instrucciones:

1. Cree un esquema con la variable **[!UICONTROL XDM ExperienceEvent]** class
1. Añadir el grupo de campos estándar **[!UICONTROL Detalles del comercio]** para capturar detalles de pedidos comunes. Dedique unos minutos a explorar los objetos que hay dentro.
1. Buscar `Luma Identity profile field group`. ¡No está disponible! Recuerde que los grupos de campos están vinculados a una clase y, como estamos utilizando una clase diferente para este esquema, no podemos utilizarla. Necesitamos añadir un nuevo grupo de campos para la clase XDM ExperienceEvent que contenga los campos de identidad. Nuestro tipo de datos lo hará muy fácil.
1. Seleccione el **[!UICONTROL Crear nuevo grupo de campos]** botón de radio
1. Introduzca la variable **[!UICONTROL Nombre para mostrar]** como `Luma Identity ExperienceEvent field group` y seleccione **[!UICONTROL Agregar grupos de campos]** botón
1. Asegúrese de que la variable **[!UICONTROL +]** los botones aparecen en la sección **[!UICONTROL Estructura]** para añadir campos nuevos
1. En **[!UICONTROL Estructura]** , seleccione **[!UICONTROL +]** en el nivel superior del esquema
1. Como **[!UICONTROL Nombre del campo]**, introduzca `systemIdentifier`
1. Como **[!UICONTROL Nombre para mostrar]**, introduzca `System Identifier`
1. Como **[!UICONTROL Tipo]**, seleccione **Identificador del sistema** que es el tipo de datos personalizado que creó anteriormente
1. Seleccione el **[!UICONTROL Aplicar]** botón
1. Asigne un nombre al esquema `Luma Offline Purchase Events Schema`
1. Seleccione el botón **[!UICONTROL Guardar]**

Observe cómo el tipo de datos ha agregado todos los campos.

![Añadir el tipo de datos al grupo de campos](assets/schemas-offlinePurchases-addDatatype.png)

También, seleccione **[!UICONTROL XDM ExperienceEvent]** en el **[!UICONTROL Clase]** e inspeccione algunos de los campos contribuidos por esta clase. Tenga en cuenta que los campos _id y timestamp son obligatorios al utilizar la clase XDM ExperienceEvent; estos campos deben rellenarse para cada registro que ingrese al utilizar este esquema:

![Estructura base del evento de experiencia](assets/schemas-offlinePurchase-experienceEventbase.png)

## Crear esquema de eventos web

Ahora vamos a crear un esquema más para los datos del sitio web de Luma. A partir de este momento, debe ser un experto en la creación de esquemas. Cree el esquema siguiente con estas propiedades

| Propiedad | Valor |
|---------------|-----------------|
| Clase | XDM ExperienceEvent |
| Grupo de campos | Mezcla de ExperienceEvent del SDK web de AEP |
| Grupo de campos | Evento de experiencia del consumidor |
| Nombre del esquema | Esquema de eventos web de Luma |

Seleccione el **[!UICONTROL Evento de experiencia del consumidor]** grupo de campos. Este grupo de campos contiene los objetos commerce y productListItems que también estaban en [!UICONTROL Detalles del comercio]. De hecho [!UICONTROL Evento de experiencia del consumidor] es una combinación de varios otros grupos de campos estándar que también están disponibles por separado. [!UICONTROL Mezcla de ExperienceEvent del SDK web de AEP] el grupo de campos también contiene otros grupos de campos, incluidos algunos de los mismos en [!UICONTROL Evento de experiencia del consumidor]. Afortunadamente, se mezclan sin problemas.

Tenga en cuenta que no agregamos la variable `Luma Identity ExperienceEvent field group` a este esquema. Esto se debe a que el SDK web tiene una forma diferente de recopilar identidades. Si selecciona la opción **[!UICONTROL XDM ExperienceEvent]** en la **[!UICONTROL Composición]** del editor de esquemas, verá que uno de los campos que agrega de forma predeterminada se llama **[!UICONTROL Mapa de identidades]**. [!DNL IdentityMap] se utiliza en varias aplicaciones de Adobe para vincular a Platform. Verá cómo se envían las identidades a Platform a través de identityMap en la lección de ingesta de flujo continuo.


## Crear esquema de catálogo de productos

Usando la variable  [!UICONTROL Detalles del comercio] y [!UICONTROL Evento de experiencia del consumidor] grupos de campos, Luma informa de algunos detalles de eventos relacionados con el producto a través del tipo de datos productListItems estándar. Pero también tienen campos de detalles de productos adicionales que les gustaría enviar a Platform. En lugar de capturar todos estos campos en sus sistemas de puntos de venta y comercio electrónico, Luma preferiría ingerirlos directamente desde su sistema de catálogo de productos. Una &quot;relación de esquema&quot; permite definir una relación entre dos esquemas para fines de clasificación o búsquedas. Luma utilizará una relación para clasificar los detalles del producto. Comenzaremos el proceso ahora y lo completaremos al final de la siguiente lección.

>[!NOTE]
>
>Si ya es cliente de Analytics o Target, clasificar entidades con relaciones de esquema es similar a clasificaciones de SAINT o cargar el catálogo de productos para Recommendations

Primero, debemos crear un esquema para el catálogo de productos de Luma mediante una clase personalizada:

1. Seleccione el **[!UICONTROL Crear esquema]** y seleccione **[!UICONTROL Examinar]** en la lista desplegable
   ![Crear nuevo esquema](assets/schemas-newSchema-browseClasses.png)
1. Seleccione el **[!UICONTROL Crear nueva clase]** botón de radio
1. Asigne un nombre `Luma Product Catalog Class`
1. Deje el **[!UICONTROL Comportamiento]** como **[!UICONTROL Registro]**
1. Seleccione el **[!UICONTROL Asignar clase]** botón
   ![Crear nueva clase](assets/schemas-productClass.png)
1. Cree una nueva [!UICONTROL grupo de campos] llamado `Luma Product Catalog field group` con los campos siguientes:
   1. productName: Nombre del producto: Cadena
   1. productCategory: Categoría del producto: Cadena
   1. productColor: Color del producto: Cadena
   1. productSku: SKU de producto: Cadena | Requerido
   1. productSize: Tamaño del producto: Cadena
   1. productPrice: Precio del producto: Duplicado
1. Asigne un nombre al esquema `Luma Product Catalog Schema` (asegúrese de actualizar el campo correcto y no actualizar el nombre de la clase)
1. **[!UICONTROL Guardar]** el esquema

El nuevo esquema debería tener este aspecto. Observe cómo la variable `productSku` se muestra en la [!UICONTROL Campos requeridos] sección:
![Esquema de producto](assets/schemas-productSchema.png)

El siguiente paso es definir la relación entre los dos esquemas de ExperienceEvent y el `Luma Product Catalog Schema`Sin embargo, hay algunos pasos adicionales que debemos seguir en la siguiente lección antes de poder hacerlo.


## Recursos adicionales

* [Documentación del sistema del Modelo de datos de experiencia (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es)
* [API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/)


Ahora que tiene sus esquemas puede [identidades del mapa](map-identities.md)!
