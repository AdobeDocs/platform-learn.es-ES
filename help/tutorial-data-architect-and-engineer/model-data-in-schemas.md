---
title: Datos de modelo en esquemas
seo-title: Model data in schemas | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Datos de modelo en esquemas
description: En esta lección, modelará los datos de Luma en esquemas. Esta es una de las lecciones más largas del tutorial, ¡así que toma un vaso de agua y abróchate!
role: Data Architect
feature: Schemas
jira: KT-4348
thumbnail: 4348-model-data-in-schemas.jpg
exl-id: 317f1c39-7f76-4074-a246-ef19f044cb85
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 1%

---

# Datos de modelo en esquemas

<!-- 60min -->
En esta lección, modelará los datos de Luma en esquemas. Esta es una de las lecciones más largas del tutorial, ¡así que toma un vaso de agua y abróchate!

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. El modelo de datos de experiencia (XDM) es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación que se utilice para comunicarse con los servicios de Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que puede ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y expresar los atributos del cliente con fines de personalización.

XDM es el marco de trabajo básico que permite a Adobe Experience Cloud, con tecnología Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento justo. La metodología en la que se ha creado Experience Platform, **Sistema XDM**, pone en funcionamiento esquemas del Modelo de datos de experiencia para que los usen los servicios de Platform.

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

**Los arquitectos de datos** tendrán que crear esquemas fuera de este tutorial, pero **los ingenieros de datos** trabajarán de cerca con los esquemas creados por el arquitecto de datos.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre los esquemas y el modelo de datos de experiencia (XDM):
>[!VIDEO](https://video.tv.adobe.com/v/27105?learn=on&enablevpops)

>[!TIP]
>
> Para profundizar en el modelado de datos en Experience Platform, recomendamos ver la lista de reproducción [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/es/playlists/experience-platform-model-your-customer-experience-data-with-xdm), disponible de forma gratuita en Experience League.

## Permisos necesarios

En la lección [Configurar permisos](configure-permissions.md), configuró todos los controles de acceso necesarios para completar esta lección.

<!--, specifically:

* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)-->


<!--
## Luma's goals
-->

## Crear esquema de fidelización mediante la IU

En este ejercicio, crearemos un esquema para los datos de fidelidad de Luma.

1. Vaya a la interfaz de usuario de Platform y asegúrese de que la zona protegida está seleccionada.
1. Vaya a **[!UICONTROL Esquemas]** en el panel de navegación izquierdo.
1. Seleccione el botón **[!UICONTROL Crear esquema]** en la parte superior derecha.
   ![Esquema con grupo de campos OOTB](assets/schemas-loyaltyCreateSchema.png)

1. En el flujo de trabajo Crear esquema, seleccione **[!UICONTROL Perfil individual]** como clase base para su esquema, ya que modelaremos los atributos de un cliente individual (puntos, estado, etc.).
1. Seleccione **[!UICONTROL Siguiente]**.
   ![Seleccionar clase base](assets/schemas-loyaltySelectBaseClass.png)

1. Escriba `Luma Loyalty Schema` en el campo de texto **[!UICONTROL Nombre para mostrar del esquema]**. En el lienzo siguiente, también puede revisar y verificar la estructura de esquema base proporcionada por la clase elegida.
1. Seleccione **[!UICONTROL Finalizar]** para crear su esquema.
   ![Terminar de crear el esquema de fidelización](assets/schemas-loyaltyFinishSchemaCreation.png)

### Adición de grupos de campos estándar

Una vez creado el esquema, se le redirigirá al Editor de esquemas, donde puede agregar campos al esquema. Puede agregar campos individuales directamente al esquema o utilizar grupos de campos. Es importante tener en cuenta que todos los campos individuales siguen estando asociados a una clase o grupo de campos. Puede elegir entre un gran conjunto de grupos de campos estándar del sector proporcionados por Adobe o crear los suyos propios. A medida que empiece a modelar sus propios datos en Experience Platform, conviene familiarizarse con los grupos de campos estándar del sector que proporciona Adobe. Siempre que sea posible, se recomienda utilizarlos, ya que a veces alimentan servicios descendentes, como inteligencia artificial aplicada al cliente, inteligencia artificial aplicada a la atribución y Adobe Analytics.

Al trabajar con sus propios datos, un paso significativo será determinar cuáles de sus propios datos deben capturarse en Platform y cómo deben modelarse. Este gran tema se analiza con más detalle en la lista de reproducción [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/es/playlists/experience-platform-model-your-customer-experience-data-with-xdm). En este tutorial, solo le guiaré a través de la implementación de algunos esquemas predeterminados.

Para agregar grupos de campos:

1. Seleccione **[!UICONTROL Agregar]** bajo el encabezado **[!UICONTROL Grupos de campos]**.
   ![Agregar nuevo grupo de campos](assets/schemas-loyalty-addFieldGroup.png)
1. En el modal **[!UICONTROL Agregar grupos de campos]**, seleccione los siguientes grupos de campos:
   1. **[!UICONTROL Detalles demográficos]** para datos básicos de clientes como nombre y fecha de nacimiento
   1. **[!UICONTROL Datos personales de contacto]** para obtener detalles básicos como la dirección de correo electrónico y el número de teléfono
1. Puede obtener una vista previa de los campos contribuidos en el grupo de campos seleccionando el icono en el lado derecho de la fila.
   ![Seleccionar grupos de campos estándar](assets/schemas-loyalty-addFirstTwoFieldGroups.png)

1. Marque la casilla **[!UICONTROL Sector]** > **[!UICONTROL Comercio minorista]** para exponer los grupos de campos específicos del sector.
1. Seleccione **[!UICONTROL Detalles de fidelización]** para agregar los campos del programa de fidelización.
1. Seleccione **[!UICONTROL Agregar grupos de campos]** para agregar los tres grupos de campos al esquema.
   ![Agregar grupos de campos estándar al esquema de fidelidad](assets/schemas-loyalty-saveOotbMixins.png)


Ahora, dedique un tiempo a explorar el estado actual del esquema. Los grupos de campos han agregado campos estándar relacionados con una persona, sus detalles de contacto y el estado del programa de fidelización. Puede encontrar útiles estos dos grupos de campos al crear esquemas para los datos de su propia compañía. Seleccione una fila de grupo de campos específica o marque la casilla junto al nombre del grupo de campos para ver cómo cambia la visualización.

Para guardar el esquema, seleccione **[!UICONTROL Guardar]**.
![Guardar el esquema](assets/schemas-loyalty-saveSchema.png)

>[!NOTE]
>
>Es aceptable si un grupo de campos agrega un campo para un punto de datos que no recopila. Por ejemplo, &quot;faxPhone&quot; puede ser un campo para el que Luma no recopila datos. Eso está bien. El hecho de que un campo esté definido en el esquema no significa que los datos para él *deban* ingerirse más adelante. También puede quitar el campo del esquema.

### Agregar un grupo de campos personalizados

Ahora, vamos a crear un grupo de campos personalizados.

Aunque el grupo de campos de fidelidad contenía un campo `loyaltyID`, Luma desea administrar todos sus identificadores del sistema en un solo grupo para garantizar la coherencia en todos sus esquemas.

Los grupos de campos deben crearse en el flujo de trabajo del esquema. Puede:

* Agregue primero un nuevo campo personalizado al esquema y, a continuación, cree un grupo de campos personalizados, o
* Cree primero un grupo de campos personalizados y, a continuación, agréguele campos.

En este tutorial, empezamos con la creación de un grupo de campos personalizados.

Para crear el grupo de campos:

1. Seleccione **[!UICONTROL Agregar]** bajo el encabezado **[!UICONTROL Grupos de campos de esquema]**
   ![Agregar nuevo grupo de campos](assets/schemas-loyalty-addFieldGroup.png)
1. Seleccionar **[!UICONTROL Crear nuevo grupo de campos]**
1. Usar `Luma Identity profile field group` como **[!UICONTROL nombre para mostrar]**
1. Usar `system identifiers for XDM Individual Profile class` como **[!UICONTROL descripción]**
1. Seleccionar **[!UICONTROL Agregar grupos de campos]**
   ![Agregar nuevo grupo de campos](assets/schemas-loyalty-nameFieldGroup.png)

El nuevo grupo de campo vacío se agrega al esquema. Los botones **[!UICONTROL +]** se pueden usar para agregar nuevos campos a cualquier ubicación de la jerarquía. En nuestro caso, queremos añadir campos en el nivel raíz:

1. Seleccione **[!UICONTROL +]** junto al nombre del esquema. Esto agrega un nuevo campo bajo el área de nombres de ID de inquilino para administrar los conflictos entre los campos personalizados y cualquier campo estándar.
1. En la barra lateral **[!UICONTROL Propiedades del campo]**, agregue los detalles del nuevo campo:
   1. **[!UICONTROL Nombre de campo]**: `systemIdentifier`
   1. **[!UICONTROL Nombre para mostrar]**: `System Identifier`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Objeto]**
   1. En el menú desplegable **[!UICONTROL Grupo de campos]**, seleccione el **grupo de campos de perfil de identidad de Luma** que hemos creado.

      ![Agregar nuevo grupo de campos](assets/schemas-loyalty-addSystemIdentifier.png)
   1. Seleccionar **[!UICONTROL Aplicar]**

      ![Aplicar nuevas propiedades de campo](assets/schemas-loyalty-applySystemIdentifier.png)

Ahora agregue dos campos bajo el objeto `systemIdentifier`:

1. Primer campo
   1. **[!UICONTROL Nombre de campo]**: `loyaltyId`
   1. **[!UICONTROL Nombre para mostrar:]** `Loyalty Id`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Cadena]**
1. Segundo campo
   1. **[!UICONTROL Nombre de campo]**: `crmId`
   1. **[!UICONTROL Nombre para mostrar]**: `CRM Id`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Cadena]**

El nuevo grupo de campos debe tener este aspecto. Seleccione el botón **[!UICONTROL Guardar]** para guardar el esquema, pero déjelo abierto para el siguiente ejercicio.
![Grupo de campos de fidelización completado](assets/schemas-loyalty-identityFieldGroupComplete.png)

## Creación de un tipo de datos

Los grupos de campos, como su nuevo `Luma Identity profile field group`, se pueden reutilizar en otros esquemas, lo que le permite aplicar definiciones de datos estándar en varios sistemas. Pero solo se pueden reutilizar _en esquemas que comparten una clase_, en este caso la clase de perfil individual de XDM.

El tipo de datos es otra construcción de varios campos que se puede reutilizar en esquemas _en varias clases_. Vamos a convertir nuestro nuevo objeto `systemIdentifier` en un tipo de datos:

Con `Luma Loyalty Schema` todavía abierto, seleccione el objeto `systemIdentifier` y seleccione **[!UICONTROL Convertir a nuevo tipo de datos]**

![Grupo de campos de fidelización completo](assets/schemas-loyalty-convertToDataType.png)

Si **[!UICONTROL cancela]** fuera del esquema y navega a la pestaña **[!UICONTROL Tipos de datos]**, verá el tipo de datos que acaba de crear. Utilizaremos este tipo de datos más adelante en la lección.

![Grupo de campos de fidelización completo](assets/schemas-loyalty-confirmDataType.png)


## Crear esquema CRM mediante API

Ahora crearemos un esquema con la API.

>[!TIP]
>
> Si prefiere omitir el ejercicio de API, puede crear el siguiente esquema con el método de interfaz de usuario:
>
> 1. Usar la clase [!UICONTROL Perfil individual]
> 1. Asigne un nombre `Luma CRM Schema`
> 1. Utilice los siguientes grupos de campos: Detalles demográficos, detalles de contacto personal y grupo de campos del perfil de identidad de Luma

Primero creamos el esquema vacío:

1. Abrir [!DNL Postman]
1. Si no cuenta con un token de acceso, abra la solicitud **[!DNL OAuth: Request Access Token]** y seleccione **Enviar** para solicitar un nuevo token de acceso.
1. Abra las variables de entorno y cambie el valor de **CONTAINER_ID** de `global` a `tenant`. Recuerde, debe usar `tenant` siempre que desee interactuar con sus propios elementos personalizados en Platform, como crear un esquema.
1. Seleccionar **Guardar**
   ![Cambiar CONTAINER_ID a tenant](assets/schemas-crm-changeContainerId.png)
1. Abrir la solicitud **[!DNL Schema Registry API > Schemas > Create a new custom schema.]**
1. Abra la pestaña **Body**, pegue el siguiente código y seleccione **Send** para realizar la llamada de API. Esta llamada crea un nuevo esquema utilizando la misma clase base `XDM Individual Profile`:

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
   >Las referencias de área de nombres en esta y las muestras de código subsiguientes (por ejemplo `https://ns.adobe.com/xdm/context/profile`) se pueden obtener usando llamadas de API de lista con el encabezado **[!DNL CONTAINER_ID]** y aceptar establecido en los valores correctos. Algunos también son fácilmente accesibles desde la interfaz de usuario.

1. Debería obtener una respuesta de `201 Created`
1. Copie `meta:altId` del cuerpo de respuesta. Lo utilizaremos más adelante en otro ejercicio.
   ![Crear el esquema CRM](assets/schemas-crm-createSchemaCall.png)

1. El nuevo esquema debe ser visible en la interfaz de usuario, pero sin ningún grupo de campos
   ![Crear el esquema CRM](assets/schemas-loyalty-emptySchemaInTheUI.png)

>[!NOTE]
>
> El identificador de esquema `meta:altId` o también se puede obtener realizando la solicitud de API **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]** con el **[!UICONTROL CONTAINER_ID]** establecido en `tenant` y un encabezado de aceptación `application/vnd.adobe.xdm+json`.

>[!TIP]
>
> Problemas comunes con esta llamada y posibles correcciones:
>
> * Sin token de autenticación: ejecute la solicitud **OAuth: Solicitar token de acceso** para generar un nuevo token
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: actualizar la variable de entorno **CONTAINER_ID** de `global` a `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: compruebe sus permisos de usuario en Admin Console

### Adición de grupos de campos estándar

Ahora es el momento de agregar los grupos de campos al esquema:

1. En [!DNL Postman], abra la solicitud **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. En la ficha **Params**, pegue el valor `meta:altId` de la respuesta anterior como `SCHEMA_ID`
1. Abra la pestaña Cuerpo, pegue el siguiente código y seleccione **Enviar** para realizar la llamada de API. Esta llamada agrega los grupos de campos estándar a su `Luma CRM Schema`:

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

   ![Grupos de campo estándar agregados](assets/schemas-crm-addMixins.png)


### Agregar grupo de campos personalizados

Ahora vamos a agregar nuestra `Luma Identity profile field group` al esquema. En primer lugar, necesitamos encontrar el ID de nuestro nuevo grupo de campos, utilizando una API de lista:

1. Abrir la solicitud **[!DNL Schema Registry API > Field groups > Retrieve a list of field groups within the specified container.]**
1. Seleccione el botón **Send** para recuperar una lista de todos los grupos de campos personalizados de su cuenta
1. Tome el valor `$id` de `Luma Identity profile field group` (el suyo será diferente del valor de esta captura de pantalla)
   ![Recuperar la lista de grupos de campos](assets/schemas-crm-getListOfMixins.png)
1. Volver a abrir la solicitud **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. La ficha **Params** debe seguir teniendo `$id` de su esquema
1. Abra la ficha **Body** y pegue el siguiente código; reemplace el valor `$ref` por el `$id` de su propio `Luma Identity profile field group`:

   ```json
   [{
     "op": "add",
     "path": "/allOf/-",
     "value": {
       "$ref": "REPLACE_WITH_YOUR_OWN_FIELD_GROUP_ID"
     }
   }]
   ```

1. Seleccionar **Enviar**
   ![Agregando el grupo de campos de identidad](assets/schemas-crm-addIdentityMixin.png)

Compruebe que el grupo de campos se ha agregado al esquema comprobando tanto la respuesta de la API como en la interfaz.

## Crear esquema de eventos de compra sin conexión

Ahora vamos a crear un esquema basado en la clase **[!UICONTROL Experience Event]** para los datos de compra sin conexión de Luma. Dado que ahora se está familiarizando con la interfaz de usuario del editor de esquemas, reduciré el número de capturas de pantalla en las instrucciones:

1. Cree un esquema con la clase **[!UICONTROL Experience Event]**.
1. Asigne un nombre al esquema `Luma Offline Purchase Events Schema`.
1. Agregue el grupo de campos estándar **[!UICONTROL Detalles de Commerce]** para capturar detalles de pedidos comunes. Dedique unos minutos a explorar los objetos que hay dentro.
1. Busque `Luma Identity profile field group`. ¡No está disponible! Recuerde que los grupos de campos están vinculados a una clase y, como estamos utilizando una clase diferente para este esquema, no podemos utilizarla. Es necesario agregar un nuevo grupo de campos para la clase XDM ExperienceEvent que contenga los campos de identidad. Nuestro tipo de datos lo hará muy fácil.
1. Seleccione el botón de opción **[!UICONTROL Crear nuevo grupo de campos]**
1. Escriba **[!UICONTROL Display name]** como `Luma Identity ExperienceEvent field group` y seleccione el botón **[!UICONTROL Agregar grupos de campos]**
1. Seleccione **[!UICONTROL +]** junto al nombre del esquema.
1. Como **[!UICONTROL Nombre de campo]**, escriba `systemIdentifier`.
1. Como **[!UICONTROL Nombre para mostrar]**, escriba `System Identifier`.
1. Como **[!UICONTROL Tipo]**, seleccione **Identificador del sistema**, que es el tipo de datos personalizados que creó anteriormente.
1. Como **[!UICONTROL grupo de campos]**, seleccione **grupo de campos Luma Identity ExperienceEvent**.
1. Seleccione el botón **[!UICONTROL Aplicar]**.
1. Seleccione el botón **[!UICONTROL Guardar]**.

Observe cómo el tipo de datos agregó todos los campos.

![Agregar el tipo de datos al grupo de campos](assets/schemas-offlinePurchases-addDatatype.png)

Además, seleccione **[!UICONTROL XDM ExperienceEvent]** en el encabezado **[!UICONTROL Class]** e inspeccione algunos de los campos que ha contribuido esta clase. Tenga en cuenta que los campos _id y timestamp son obligatorios al utilizar la clase XDM ExperienceEvent; estos campos deben rellenarse para cada registro que introduzca al utilizar este esquema:

![Estructura base del evento de experiencia](assets/schemas-offlinePurchase-experienceEventbase.png)

## Crear esquema de eventos web

Ahora vamos a crear un esquema más para los datos del sitio web de Luma. En este punto, debería ser un experto en la creación de esquemas. Cree el siguiente esquema con estas propiedades

| Propiedad | Valor |
|---------------|-----------------|
| Clase | Evento de experiencia |
| Nombre del esquema | Esquema de eventos web de Luma |
| Grupo de campo | ExperienceEvent de SDK web de AEP |
| Grupo de campo | Evento de experiencia del consumidor |

Seleccione el grupo de campos **[!UICONTROL Evento de experiencia del consumidor]**. Este grupo de campos contiene los objetos commerce y productListItems que también estaban en [!UICONTROL Detalles de Commerce]. De hecho, [!UICONTROL Evento de experiencia del consumidor] es una combinación de otros grupos de campos estándar que también están disponibles por separado. El grupo de campos [!UICONTROL AEP Web SDK ExperienceEvent] también contiene otros grupos de campos, incluidos algunos de los mismos en [!UICONTROL Evento de experiencia del consumidor]. Afortunadamente, se mezclan sin problemas.

Observe que no se agregó `Luma Identity ExperienceEvent field group` a este esquema. Esto se debe a que Web SDK tiene una forma diferente de recopilar identidades. Si selecciona la clase **[!UICONTROL XDM ExperienceEvent]** en la sección **[!UICONTROL Composition]** del editor de esquemas, verá que uno de los campos que agrega de forma predeterminada se llama **[!UICONTROL IdentityMap]**. Varias aplicaciones de Adobe utilizan [!DNL IdentityMap] para vincularse a Platform. Verá cómo se envían las identidades a Platform a través de identityMap en la lección de ingesta de transmisión.


## Crear esquema de catálogo de productos

Mediante los grupos de campos [!UICONTROL Detalles de Commerce] y [!UICONTROL Evento de experiencia del consumidor], Luma informa de algunos detalles de eventos relacionados con el producto a través del tipo de datos estándar productListItems. Pero también tienen campos de detalles de producto adicionales que les gustaría enviar a Platform. En lugar de capturar todos estos campos en sus sistemas de punto de venta y comercio electrónico, Luma preferiría ingerirlos directamente desde su sistema de catálogo de productos. Una &quot;relación de esquema&quot; permite definir una relación entre dos esquemas para los fines de clasificación o búsquedas. Luma utilizará una relación para clasificar los detalles del producto. Comenzaremos el proceso ahora y lo completaremos al final de la siguiente lección.

>[!NOTE]
>
>Si es cliente existente de Analytics o Target, la clasificación de entidades con relaciones de esquema es análoga a las clasificaciones de SAINT o a la carga del catálogo de productos para Recommendations

En primer lugar, se debe crear un esquema para el catálogo de productos de Luma utilizando una clase personalizada:

1. Seleccione el botón **[!UICONTROL Crear esquema]**.
1. En el flujo de trabajo Crear esquema, seleccione la opción **[!UICONTROL Otros]**.
   ![Crear nuevo esquema](assets/schemas-newSchema-browseClasses.png)
1. Seleccione el botón **[!UICONTROL Crear clase]**
1. Asigne un nombre `Luma Product Catalog Class`
1. Deje **[!UICONTROL Funcionamiento]** como **[!UICONTROL Registro]**
1. Seleccione el botón **[!UICONTROL Crear]**.
   ![Crear nueva clase](assets/schemas-productClass.png)
1. La **clase de catálogo de productos Luma** que ha creado aparece en la tabla Clases a continuación. Asegúrese de que la clase esté seleccionada y, a continuación, seleccione **[!UICONTROL Siguiente]**.
   ![Nueva clase agregada](assets/schemas-productClassSelected.png)
1. Asigne un nombre al esquema `Luma Product Catalog Schema`.
1. Crear un nuevo [!UICONTROL grupo de campos] llamado `Luma Product Catalog field group` con los campos siguientes:
   1. productName: Nombre del producto: String
   1. productCategory: Categoría del producto: Cadena
   1. productColor: Product Color: String
   1. productSKU: Product SKU: String | Requerido
   1. productSize: Tamaño del producto: Cadena
   1. productPrice: Precio del producto: Doble
1. **[!UICONTROL Guardar]** el esquema

El nuevo esquema debería tener un aspecto similar al siguiente. Observe cómo el campo `productSku` aparece en la sección [!UICONTROL Campos obligatorios]:
![Esquema del producto](assets/schemas-productSchema.png)

El siguiente paso es definir la relación entre los dos esquemas de ExperienceEvent y `Luma Product Catalog Schema`; sin embargo, hay que seguir algunos pasos adicionales en la siguiente lección para poder hacerlo.


## Recursos adicionales

* [Documentación del sistema del modelo de datos de experiencia (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es)
* [API de Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/)


Ahora que tiene sus esquemas, puede [asignar identidades](map-identities.md).
