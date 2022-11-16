---
title: Configure los permisos
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configure los permisos
description: En esta lección, debe configurar los permisos de usuario de Adobe Experience Platform mediante el Admin Console de Adobe.
role: Data Architect, Data Engineer
feature: Access Control
kt: 4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 3%

---

# Configure los permisos

<!--30min-->

En esta lección, debe configurar los permisos de usuario de Adobe Experience Platform mediante [!DNL Adobe's Admin Console].

El control de acceso es una función de privacidad clave en Experience Platform y recomendamos limitar los permisos al mínimo necesario para que las personas realicen sus funciones de trabajo. Consulte la [Documentación de control de acceso](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=es) para obtener más información.

Los arquitectos de datos y los ingenieros de datos son usuarios potentes de Adobe Experience Platform y necesitará muchos permisos para completar este tutorial y, posteriormente, su trabajo diario. Es probable que los arquitectos de datos participen en la administración de *otros usuarios de Platform* en su empresa, como especialistas en marketing, analistas y científicos de datos. Cuando complete esta lección, piense en cómo puede usar estas funciones para administrar otros usuarios en su empresa.

**Arquitectos de datos** a menudo, configure permisos para otros usuarios fuera de este tutorial.

>[!IMPORTANT]
>
>Un administrador del sistema de productos de Adobe Experience Cloud debe completar algunos de los pasos de esta lección, que se describen en los encabezados de sección. Si no es administrador del sistema, póngase en contacto con uno de su empresa y pídale que complete estas tareas.

## Acerca del Admin Console

La variable [!DNL Admin Console] es la interfaz que se utiliza para administrar el acceso de los usuarios a todos los productos de Adobe Experience Cloud. Consulte [Documentación de Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para obtener información más detallada. Aquí hay algunas claves [!DNL Admin Console] conceptos:

* A **perfil de producto** es una combinación de permisos, funciones y entornos de simulación de pruebas asociados a un producto de Adobe específico. Se pueden crear varios perfiles de producto para un único producto de Adobe. Por ejemplo, un perfil &quot;experto en marketing&quot; podría limitar los permisos a lo que un especialista en marketing típico necesitaría para completar tareas clave en el entorno de la plataforma de producción, mientras que un perfil &quot;arquitecto de datos&quot; podría utilizarse para conceder permisos diferentes en varios entornos de la plataforma. En esta lección, debe crear un perfil de producto &quot;Tutorial de Luma&quot; con todos los permisos que un arquitecto de datos y un ingeniero de datos necesitarían para completar este tutorial en un entorno limitado.
* Un **integración** es una conexión a un *proyecto* en la consola de Adobe Developer. La consola de Adobe Developer es el corazón de la autenticación y la configuración de las API de Adobe. Configurará una integración en Developer Console y [!DNL Postman] lección.

A continuación, se muestra un breve resumen de las funciones que existen para Platform:

* **Usuarios** de un perfil de producto puede completar tareas en la interfaz de usuario de Platform según los permisos asignados en el perfil de producto.
* **Desarrolladores** de un perfil de producto puede completar tareas utilizando la API de Platform según los permisos del perfil de producto.
* **Administradores de perfil de producto** puede editar *de ese perfil específico* permisos y agregar usuarios, desarrolladores y administradores de perfil adicionales.
* **Administradores de producto** administrar *todos los perfiles de producto* para Platform y agregue nuevos perfiles de producto.
* **Administradores del sistema** puede agregar administradores de productos y administrar prácticamente cualquier permiso para todos los productos de Adobe Experience Cloud.

## Crear un perfil de producto de Experience Platform (requiere un administrador del sistema o un administrador del producto)

En este ejercicio, usted o un administrador del sistema de su empresa crearán un perfil de producto para Adobe Experience Platform y lo agregarán como administrador para ese perfil de producto.

>[!NOTE]
>
>Si es administrador del sistema y está asistiendo a un colega en la realización de este tutorial, considere la posibilidad de agregar su colega como *Administrador de productos* para Adobe Experience Platform. Como administrador de productos, podrían completar estos pasos por su cuenta y administrar otros usuarios de Experience Platform en el futuro.

Para crear el perfil de producto:

1. Inicie sesión en el [Adobe Admin Console](https://adminconsole.adobe.com)
1. Select **[!UICONTROL Productos]** en la barra de navegación superior
1. Select **[!UICONTROL Adobe Experience Platform]** en el panel de navegación izquierdo (es posible que necesite expandir el **[!UICONTROL Experience Cloud]** sección)
1. Es posible que ya tenga varios perfiles en la instancia de Experience Platform. Seleccione el **[!UICONTROL Nuevo perfil]** para agregar otro
   ![Seleccionar Agregar nuevo perfil](assets/adminconsole-newProfile.png)
1. Asigne un nombre al perfil. `Luma Tutorial Platform` (añada el nombre del participante del tutorial al final, si varias personas de su empresa están tomando este tutorial) y seleccione la opción **[!UICONTROL Siguiente]** botón
   ![Asigne un nombre al perfil de la plataforma de tutoriales de Luma](assets/adminconsole-nameProfile.png)
1. Dependiendo de los detalles de su licencia de producto, puede que vea o no este segundo **[!UICONTROL Servicios]** en el Navegador. No se utilizará ninguno de estos servicios en este tutorial, por lo que desmarque **[!UICONTROL Habilitar todos los servicios]** a *remove* todos los servicios y seleccione **[!UICONTROL Guardar]**.
   ![Desactivar servicios](assets/adminconsole-createProfile-services.png)

Ahora, añada el participante del tutorial como administrador del perfil de producto recién creado. If *you* son los participantes en el tutorial, vaya a [Configuración del perfil de producto del Experience Platform](#configure-experience-platform-product-profile):

1. Seleccione el `Luma Tutorial Platform` perfil de producto:

   ![Abrir el perfil](assets/adminconsole-newProfileInList.png)

1. Seleccione el **[!UICONTROL Administradores]** y, a continuación, seleccione **[!UICONTROL Agregar administrador]** botón:

   ![Vaya a la ficha Administradores y seleccione Agregar administrador .](assets/adminconsole-addAdmin.png)

1. Complete el flujo de trabajo para añadir el participante del tutorial como administrador.

Después de completar estos pasos, debe ver que la variable `Luma Tutorial Platform` perfil se configura con un administrador.
![Perfil de plataforma creado](assets/adminconsole-platform-profileCreated.png)

## Configuración del perfil de producto del Experience Platform

Ahora que es administrador de `Luma Tutorial Platform` perfil de producto, puede configurar los permisos y las funciones que necesitará para completar el tutorial.

### Adición de permisos

Ahora agregará los elementos de permiso individuales al perfil:

1. Abra el `Luma Tutorial Platform` perfil de producto
1. Seleccione la pestaña **[!UICONTROL Permisos]**
1. En **[!UICONTROL Sandboxes]**, añada la variable **[!UICONTROL Prod]** entorno limitado al perfil. Es necesario tener acceso al [!DNL Prod] simulador de pruebas para crear entornos limitados adicionales. Una vez que añadamos el simulador de pruebas en la siguiente lección, eliminaremos el [!DNL Prod] simulador de pruebas del perfil del producto.
1. En [!UICONTROL Ingesta de datos], añada la variable [!UICONTROL Administrar fuentes] y [!UICONTROL Ver fuentes] elementos de permiso.
1. Agregue todos los elementos de permiso para:
   1. [!UICONTROL Modelado de datos]
   1. [!UICONTROL Administración de datos]
   1. [!UICONTROL Administración de perfiles]
   1. [!UICONTROL Administración de identidades]
   1. [!UICONTROL Administración de Simuladores para pruebas]
   1. [!UICONTROL Servicio de consultas]
   1. [!UICONTROL Recopilación de datos]
   1. [!UICONTROL Gobierno de datos]
   1. [!UICONTROL Tableros]
   1. [!UICONTROL Alertas]

1. Después de agregar todos los elementos de permiso, asegúrese de seleccionar la variable **[!UICONTROL Guardar]** botón

### Añádese como usuario

En este punto, si `Luma Tutorial Platform` era tu *only* perfil de producto de Experience Platform, aún no podría iniciar sesión en la interfaz de usuario de Experience Platform. Para ello, debe ser un *usuario* en el perfil de producto. Afortunadamente, ya que eres un *admin* de un perfil de producto, puede agregarse como *usuario*!

1. Vaya a la **[!UICONTROL Usuarios]** ficha
1. Seleccione el **[!UICONTROL Agregar usuario]** botón
   ![Seleccionar Agregar usuario](assets/adminconsole-addUser.png)
1. Complete el flujo de trabajo para añadirse como usuario al perfil del producto

### Añádese como desarrollador

Para utilizar la API de Platform, agréguese como desarrollador:

1. Vaya a la **[!UICONTROL Desarrolladores]** ficha
1. Seleccione el **[!UICONTROL Agregar desarrollador]** botón
   ![Seleccionar Agregar usuario](assets/adminconsole-addDeveloper.png)
1. Complete el flujo de trabajo para añadirse como desarrollador al perfil del producto

## Crear un perfil de producto de recopilación de datos (requiere un administrador del sistema o un administrador de productos)

En este ejercicio, usted o un administrador del sistema de su empresa crearán un perfil de producto para la recopilación de datos (anteriormente conocido como Adobe Experience Platform Launch) y lo añadirán como administrador de perfiles de producto.

>[!NOTE]
>
>Si es administrador del sistema y asiste a un colega en este tutorial, considere la posibilidad de agregarlos como *Administrador de productos* para la recopilación de datos. Como administrador de productos, podrán completar estos pasos por su cuenta y administrar otros usuarios de la recopilación de datos en el futuro.

Para crear el perfil de producto:

1. En el [!DNL Adobe Admin Console] vaya al producto de recopilación de datos de Adobe Experience Platform
1. Añadir un perfil nuevo con el nombre `Luma Tutorial Data Collection` (añada el nombre del participante del tutorial al final, si varias personas de su empresa están tomando este tutorial)
1. Desactive el **[!UICONTROL Propiedades]** > **[!UICONTROL Inclusión automática]** configuración
1. No asignar propiedades o permisos en este momento
1. Añadir el participante del tutorial como administrador de este perfil

Después de completar estos pasos, debe ver que la variable `Luma Tutorial Data Collection` perfil se configura con un administrador.
![Perfil de recopilación de datos creado](assets/adminconsole-dc-profileCreated.png)

## Configuración del perfil de producto de la recopilación de datos

Ahora que es administrador de `Luma Tutorial Data Collection` perfil de producto, puede configurar los permisos y las funciones que necesitará para completar el tutorial.

### Adición de permisos

Ahora agregará los elementos de permiso individuales al perfil:

1. En el [Adobe Admin Console](https://adminconsole.adobe.com), vaya a **[!UICONTROL Productos]** > **[!UICONTROL Recopilación de datos]**
1. Abra el `Luma Tutorial Data Collection` perfil
1. Vaya a la **[!UICONTROL Permisos]** ficha
1. Apertura **[!UICONTROL Plataformas]**
1. Asegúrese de que todas las plataformas disponibles estén seleccionadas (puede que vea diferentes opciones en función de su licencia)
1. **[!UICONTROL Guardar]** cualquier cambio
   ![Agregar plataformas](assets/adminconsole-launch-addPlatforms.png)
1. Apertura **[!UICONTROL Propiedades]**
1. Asegúrese de que la variable **[!UICONTROL Inclusión automática]** la opción está desactivada para que no tenga acceso a ninguna propiedad (la agregaremos más adelante)
1. **[!UICONTROL Guardar]** cualquier cambio
   ![Eliminación de propiedades](assets/adminconsole-launch-removeProperties.png)
1. Apertura **[!UICONTROL Derechos de propiedad]**
1. Select **[!UICONTROL Agregar todo]** para agregar todos los permisos de propiedad
1. **[!UICONTROL Guardar]**
   ![Eliminación de propiedades](assets/adminconsole-launch-addPropertyRights.png)
1. Apertura **[!UICONTROL Derechos de compañía]**
1. Agregar **[!UICONTROL Administrar propiedades]**
1. Seleccione **[!UICONTROL Guardar]**

   ![Eliminación de propiedades](assets/adminconsole-launch-companyRights.png)


### Añádese como usuario

A continuación, agréguese como usuario al perfil de recopilación de datos:

1. Vaya a la **[!UICONTROL Usuarios]** ficha
1. Seleccione el **[!UICONTROL Agregar usuario]** botón
   ![Seleccionar Agregar usuario](assets/adminconsole-launch-addUser.png)
1. Complete el flujo de trabajo para añadirse como usuario al perfil del producto

No es necesario que se añada como desarrollador para la recopilación de datos.

Ahora tiene casi todos los permisos necesarios para completar el tutorial. Solo habrá dos ajustes más que se harán dentro de la variable [!DNL Adobe Admin Console], incluido uno después de [crear un entorno limitado](create-a-sandbox.md)!
