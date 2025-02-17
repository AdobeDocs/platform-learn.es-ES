---
title: Asignación de identidades
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Asignación de identidades
description: En esta lección, crearemos áreas de nombres de identidad y agregaremos campos de identidad a nuestros esquemas.
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 6%

---

# Asignación de identidades

<!-- 30 min-->

En esta lección, crearemos áreas de nombres de identidad y agregaremos campos de identidad a nuestros esquemas. Después de hacerlo, también podremos completar las relaciones de esquema de la lección anterior.

El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de sus clientes y sus comportamientos al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real. Los campos de identidad y las áreas de nombres son el pegamento que une diferentes fuentes de datos para crear un perfil de cliente en tiempo real de 360 grados.

**Los arquitectos de datos** deberán asignar identidades fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre la identidad en Adobe Experience Platform:
>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on&enablevpops)

>[!NOTE]
>
>Los campos de identidad solo son necesarios si crea perfiles de clientes en tiempo real. No son necesarios si solo está introduciendo datos en el lago de datos.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## Permisos necesarios

En la lección [Configurar permisos](configure-permissions.md), configuró todos los controles de acceso necesarios para completar esta lección.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Crear área de nombres de identidad

En este ejercicio, crearemos áreas de nombres de identidad para los campos de identidad personalizados de Luma: `loyaltyId`, `crmId` y `productSku`. Las áreas de nombres de identidad desempeñan un papel esencial en la creación de perfiles de clientes en tiempo real, ya que dos valores coincidentes en la misma área de nombres permiten que dos fuentes de datos formen un gráfico de identidad.


### Creación de áreas de nombres en la IU

Empecemos creando un área de nombres para el esquema de fidelidad de Luma:

1. En la interfaz de usuario de Platform, vaya a **[!UICONTROL Identities]** en el panel de navegación izquierdo
1. Observará que hay varias áreas de nombres de identidad listas para usar. Seleccione el botón **[!UICONTROL Crear área de nombres de identidad]**
1. Proporcione los siguientes detalles

   | Campo | Valor |
   |---------------|-----------|
   | Nombre para mostrar | ID de fidelización de Luma |
   | Símbolo de identidad | lumaLoyaltyId |
   | Tipo | Entre Dispositivos |

1. Seleccionar **[!UICONTROL Crear]**

   ![Crear áreas de nombres](assets/identity-createNamespace.png)

Ahora configure otra área de nombres para el esquema del catálogo de productos de Luma con los siguientes detalles:

| Campo | Valor |
|---------------|-----------|
| Nombre para mostrar | SKU del producto de Luma |
| Símbolo de identidad | lumaProductSKU |
| Tipo | Identificador de no personas |



## Crear área de nombres de identidad mediante API

Crearemos nuestro área de nombres de CRM mediante API.

>[!NOTE]
>
>Si prefiere omitir los ejercicios de la API, no dude en crear el área de nombres de CRM a través del método de interfaz de usuario que utilizó con los siguientes detalles:
>
> 1. Como **[!UICONTROL nombre para mostrar]**, use `Luma CRM Id`
> 1. Como **[!UICONTROL símbolo de identidad]**, use `lumaCrmId`
> 1. Como **[!UICONTROL Type]**, utilice Cross-Device

Vamos a crear el área de nombres de identidad `Luma CRM Id`:

1. Descargar [servicio de identidad.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) en la carpeta `Luma Tutorial Assets`
1. Importar la colección en [!DNL Postman]
1. Si no cuenta con un token de acceso, abra la solicitud **[!DNL OAuth: Request Access Token]** y seleccione **Enviar** para solicitar un nuevo token de acceso.
1. Seleccione la solicitud **[!UICONTROL Servicio de identidad] > [!UICONTROL Área de nombres de identidad] > [!UICONTROL Crear un nuevo área de nombres de identidad].**
1. Pegue lo siguiente como [!DNL Body] de la solicitud:

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. Presione el botón **Send** y debería obtener una respuesta de **200 OK**:

   ![Área de nombres de identidad](assets/identity-createUsingApi.png)

Si vuelve a la interfaz de usuario, debería ver las tres nuevas áreas de nombres personalizadas:
![Área de nombres de identidad ](assets/identity-newIdentities.png)


## Campos de identidad de etiqueta en esquemas

Ahora que tenemos nuestras áreas de nombres, el siguiente paso es actualizar nuestros esquemas para etiquetar nuestros campos de identidad.


### Etiquetar campos XDM para la identidad principal

Es necesario especificar una identidad principal para cada esquema utilizado con el perfil del cliente en tiempo real. Y cada registro introducido debe tener un valor para ese campo.

Vamos a agregar una identidad principal a `Luma Loyalty Schema`:

1. Abrir `Luma Loyalty Schema`
1. Seleccione el(la) `Luma Identity profile field group`
1. Seleccione el campo `loyaltyId`
1. Marque la casilla **[!UICONTROL Identidad]**
1. Marque también la casilla **[!UICONTROL Identidad principal]**
1. Seleccione el área de nombres `Luma Loyalty Id` de la lista desplegable **[!UICONTROL Áreas de nombres de identidad]**
1. Seleccionar **[!UICONTROL Aplicar]**
1. Seleccionar **[!UICONTROL Guardar]**

   ![Identidad principal ](assets/identity-loyalty-primary.png)

Repita el proceso para alguno de los demás esquemas:

1. En `Luma CRM Schema`, etiquete el campo `crmId` como la identidad principal mediante el área de nombres `Luma CRM Id`
1. En `Luma Offline Purchase Events Schema`, etiquete el campo `loyaltyId` como la identidad principal mediante el área de nombres `Luma Loyalty Id`
1. En `Luma Product Catalog Schema`, etiquete el campo `productSku` como la identidad principal mediante el área de nombres `Luma Product SKU`

>[!NOTE]
>
>Los datos recopilados con Web SDK son una excepción a la práctica habitual de etiquetar campos de identidad en el esquema. Web SDK usa el mapa de identidad para etiquetar identidades *en el lado de la implementación* y, por lo tanto, determinaremos las identidades de `Luma Web Events Schema` cuando implementemos Web SDK en el sitio web de Luma. En esa lección posterior, recopilaremos el ID del visitante de Experience Cloud (ECID) como ID principal y el crmId como ID secundario.

Con nuestra selección de identidades principales, es claro ver cómo `Luma CRM Schema` puede conectarse a `Luma Offline Purchase Events Schema`, ya que ambos utilizan `loyaltyId` como identificador. Pero, ¿cómo podemos conectar nuestras compras sin conexión con el comportamiento en línea? ¿Cómo podemos clasificar los productos comprados con nuestro catálogo de productos? Utilizaremos campos de identidad y relaciones de esquema adicionales.

<!--use a visual-->

### Etiquetar campos XDM para la identidad secundaria

Se pueden añadir varios campos de identidad a un esquema. Las identidades no principales suelen denominarse identidades secundarias. Para conectar las compras sin conexión con el comportamiento en línea, agregaremos el crmId como identificador secundario a `Luma Loyalty Schema` y, posteriormente, a los datos de eventos web. Vamos a actualizar `Luma Loyalty Schema`:

1. Abrir `Luma Loyalty Schema`
1. Seleccionar `Luma Identity Profile Field group`
1. Seleccionar campo `crmId`
1. Marque la casilla **[!UICONTROL Identidad]**
1. Seleccione el área de nombres `Luma CRM Id` de la lista desplegable **[!UICONTROL Áreas de nombres de identidad]**
1. Seleccione **[!UICONTROL Aplicar]** y, a continuación, seleccione el botón **[!UICONTROL Guardar]** para guardar los cambios

   ![Identidad secundaria](assets/identity-loyalty-secondaryId.png)

## Completar las relaciones de esquema

Ahora que tenemos los campos de identidad etiquetados, podemos completar la configuración de las relaciones de esquema entre el catálogo de productos de Luma y los esquemas de eventos:

1. Abrir `Luma Offline Purchase Events Schema`
1. Seleccionar **[!UICONTROL detalles de Commerce]** grupo de campos
1. Seleccione el campo **[!UICONTROL productListItems]** > **[!UICONTROL SKU]**
1. Marque la casilla **[!UICONTROL Relación]**
1. Seleccione `Luma Product Catalog Schema` como **[!UICONTROL esquema de referencia]**
1. `Luma Product SKU` debe rellenarse automáticamente como **[!UICONTROL área de nombres de identidad de referencia]**
1. Seleccionar **[!UICONTROL Aplicar]**
1. Seleccionar **[!UICONTROL Guardar]**

   ![Campo de referencia](assets/identity-offlinePurchase-relationship.png)

Repita este proceso para crear una relación entre `Luma Web Events Schema` y `Luma Product Catalog Schema`.

Tenga en cuenta que después de definir la relación, se indica en las secciones **[!UICONTROL Composition]** y **[!UICONTROL Structure]** del editor de esquemas.

![Visualización de relaciones en el editor de esquemas](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## Recursos adicionales

* [Documentación del servicio de identidad](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=es)
* [API del servicio de identidad](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Ahora que nuestras identidades están establecidas, ¡podemos [crear nuestros conjuntos de datos](create-datasets.md)!
