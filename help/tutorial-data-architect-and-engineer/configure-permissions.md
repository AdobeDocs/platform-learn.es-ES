---
title: Configure los permisos
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configure los permisos
description: En esta lección, debe configurar los permisos de usuario de Adobe Experience Platform mediante el Admin Console de Adobe.
role: Data Architect, Data Engineer
feature: Access Control
jira: KT-4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 2%

---

# Configure los permisos

<!--30min-->

En esta lección, debe configurar los permisos de usuario de Adobe Experience Platform mediante [!DNL Adobe's Admin Console] y la pantalla [!UICONTROL Permisos] en la interfaz de Platform.

El control de acceso es una función clave de privacidad en Experience Platform y se recomienda limitar los permisos al mínimo requerido para que las personas realicen sus funciones laborales. Consulte la [documentación de control de acceso](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=es) para obtener más información.

Los arquitectos y los ingenieros de datos son usuarios avanzados de Adobe Experience Platform y necesitará muchos permisos para completar este tutorial y, posteriormente, su trabajo diario. Es probable que los arquitectos de datos estén involucrados en la administración de *otros usuarios de Platform* en su compañía, como especialistas en marketing, analistas y científicos de datos. A medida que complete esta lección, piense en cómo puede utilizar estas funciones para administrar otros usuarios de su compañía.

**Los arquitectos de datos** suelen configurar permisos para otros usuarios fuera de este tutorial.

>[!IMPORTANT]
>
>Un administrador del sistema de productos de Adobe Experience Cloud debe completar algunos de los pasos de esta lección, que se indican en los encabezados de sección. Si no es administrador del sistema, póngase en contacto con uno de sus empleados de la empresa y pídale que realice estas tareas. También hay que completar una tarea durante la lección [Configurar Developer Console y Postman](set-up-developer-console-and-postman.md).

## Acerca del Admin Console

[!DNL Admin Console] es la interfaz utilizada para administrar el acceso de usuario a todos los productos de Adobe Experience Cloud. Para acceder a Platform, se debe añadir un usuario o un usuario en el Admin Console y, a continuación, todos sus elementos de permisos granulares se administran en la pantalla Permisos de Adobe Experience Platform.


Este es un breve resumen de las funciones que existen para Platform:

* **Los usuarios** de un perfil de producto pueden completar tareas en la interfaz de usuario de Platform según los permisos asignados en el perfil de producto.
* **Los desarrolladores** pueden crear proyectos y credenciales de API en Adobe Developer Console para empezar a usar la API de Experience Platform
* **Administradores de productos** pueden agregar usuarios y desarrolladores al producto Adobe Experience Platform en Adobe Admin Console, así como administrar el acceso granular de usuarios en la pantalla Permisos de la interfaz de Platform.
* **Los administradores del sistema** pueden agregar administradores de productos y administrar prácticamente cualquier permiso para todos los productos de Adobe Experience Cloud.

## Agregar un usuario y un desarrollador al perfil de producto `AEP-Default-All-Users` (requiere un administrador del sistema o un administrador de productos)

En este ejercicio, usted, un administrador del sistema o un administrador de productos le añadirán como usuario y desarrollador al producto Adobe Experience Platform de Adobe Admin Console.

>[!NOTE]
>
>Si es administrador del sistema y ayuda a un compañero a seguir este tutorial, considere la posibilidad de añadir a su compañero como *administrador de productos* para Adobe Experience Platform. Como administrador de productos, podría completar estos pasos por su cuenta y administrar a otros usuarios de Experience Platform en el futuro.

Para agregar al participante del tutorial como [!UICONTROL Usuario] y [!UICONTROL Desarrollador]:

1. Iniciar sesión en [Adobe Admin Console](https://adminconsole.adobe.com)
1. Seleccione **[!UICONTROL Productos]** en la barra de navegación superior
1. Seleccionar **Adobe Experience Platform**
   ![Seleccionar Adobe Experience Platform](assets/adminconsole-experiencePlatform.png)
1. Es posible que ya tenga varios perfiles en la instancia de Experience Platform. Seleccionar el perfil `AEP-Default-All-Users`
   ![Seleccionar Agregar Nuevo Perfil](assets/adminconsole-newProfile.png)

1. Vaya a la ficha **[!UICONTROL Usuarios]**
1. Seleccione el botón **[!UICONTROL Agregar usuario]**
   ![Seleccionar Agregar usuario](assets/adminconsole-addUser.png)
1. Complete el flujo de trabajo para añadir al participante del tutorial como usuario al perfil del producto

1. Vaya a la ficha **[!UICONTROL Desarrolladores]**
1. Seleccione el botón **[!UICONTROL Agregar desarrollador]**
   ![Seleccionar Agregar usuario](assets/adminconsole-addDeveloper.png)
1. Complete el flujo de trabajo para añadir al participante del tutorial como desarrollador al perfil del producto


## Agregar una función en Adobe Experience Platform (requiere un administrador del sistema o un administrador de productos)

Los permisos granulares para el Experience Platform se administran en la pantalla Permisos de la interfaz de Platform. Solo los administradores de sistemas y productos tienen acceso a esta pantalla, por lo que si no tiene privilegios de administrador, necesitará la asistencia de alguien que sí lo tenga.

Los permisos se administran en Funciones. Cree una función para el tutorial:

1. Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com)
1. Seleccione **[!UICONTROL Permisos]** en el panel de navegación izquierdo para acceder a la pantalla de [!UICONTROL Roles]
1. Seleccionar **[!UICONTROL Crear rol]**

   ![Crear un rol en Experience Platform](assets/permissions-addRole.png)
1. Asigne un nombre al rol `Luma Tutorial Platform` (añada el nombre del participante del tutorial al final, si varias personas de su compañía toman este tutorial) y seleccione **[!UICONTROL Confirmar]**

   ![Crear un rol en Experience Platform](assets/permissions-nameRole.png)


1. Agregue todos los elementos de permiso para los siguientes recursos usando **[!UICONTROL +]** y **[!UICONTROL Agregar todos]**:

   1. Modelado de datos
   1. Administración de datos
   1. Administración de perfiles
   1. Identity Management
   1. Administración de zona protegida
   1. Servicio de consultas
   1. Recopilación de datos
   1. Control de datos
   1. Paneles
   1. Alertas

      ![Agregar elementos de permiso](assets/permissions-addPermissionItems.png)

1. En Ingesta de datos, agregue los elementos de permiso Administrar fuentes y Ver fuentes.

1. Después de agregar todos los elementos de permiso, asegúrese de seleccionar el botón Guardar
   ![Guardar elementos de permiso](assets/permissions-savePermissions.png)

Hará algunas pequeñas actualizaciones de esta función después de las lecciones de [Crear una zona protegida](create-a-sandbox.md) y [Configurar Developer Console y Postman](set-up-developer-console-and-postman.md).

## Crear un perfil de producto de recopilación de datos (requiere un administrador del sistema o de productos)

En este ejercicio, usted o un administrador del sistema de su empresa crearán un perfil de producto para la recopilación de datos (anteriormente conocido como Adobe Experience Platform Launch) y lo añadirán como administrador de perfil de producto.

>[!NOTE]
>
>Si es administrador del sistema y ayuda a un compañero con este tutorial, considere la posibilidad de agregarlo como *administrador de productos* para la recopilación de datos. Como administrador de productos, podrá completar estos pasos por su cuenta y administrar a otros usuarios de la recopilación de datos en el futuro.

Para crear el perfil de producto:

1. En [!DNL Adobe Admin Console], vaya al producto Recopilación de datos de Adobe Experience Platform
1. Agregue un nuevo perfil denominado `Luma Tutorial Data Collection` (agregue el nombre del participante del tutorial al final, si varias personas de su compañía están siguiendo este tutorial)
1. Desactivar la configuración de **[!UICONTROL Propiedades]** > **[!UICONTROL Inclusión automática]**
1. No asignar propiedades ni permisos en este momento
1. Añadir el participante del tutorial como administrador de este perfil

Después de completar estos pasos, debería ver que el perfil `Luma Tutorial Data Collection` está configurado con un administrador.
![Perfil de recopilación de datos creado](assets/adminconsole-dc-profileCreated.png)

## Configuración del perfil de producto de recopilación de datos

Ahora que es administrador del perfil de producto `Luma Tutorial Data Collection`, puede configurar los permisos y las funciones que necesitará para completar el tutorial.

### Adición de permisos

Ahora agregará los elementos de permiso individuales al perfil:

1. En [Adobe Admin Console](https://adminconsole.adobe.com), vaya a **[!UICONTROL Productos]** > **[!UICONTROL Recopilación de datos]**
1. Abrir el perfil `Luma Tutorial Data Collection`
1. Vaya a la ficha **[!UICONTROL Permisos]**
1. Abrir **[!UICONTROL Plataformas]**
1. Asegúrese de que todas las plataformas disponibles estén seleccionadas (puede ver diferentes opciones según la licencia)
1. **[!UICONTROL Guardar]** cambios
   ![Agregar plataformas](assets/adminconsole-launch-addPlatforms.png)
1. Abrir **[!UICONTROL propiedades]**
1. Asegúrese de que la opción **[!UICONTROL Incluir automáticamente]** esté Desactivada para que no tenga acceso a ninguna propiedad (agregaremos una más tarde)
1. **[!UICONTROL Guardar]** cambios
   ![Quitar propiedades](assets/adminconsole-launch-removeProperties.png)
1. Abrir **[!UICONTROL derechos de propiedad]**
1. Seleccione **[!UICONTROL Agregar todos]** para agregar todos los permisos de propiedad
1. **[!UICONTROL Guardar]**
   ![Quitar propiedades](assets/adminconsole-launch-addPropertyRights.png)
1. Abrir **[!UICONTROL derechos de compañía]**
1. Agregar **[!UICONTROL Administrar propiedades]**
1. Seleccionar **[!UICONTROL Guardar]**
   ![Quitar propiedades](assets/adminconsole-launch-companyRights.png)


### Añádase como usuario

Ahora añádase como usuario al perfil de recopilación de datos:

1. Vaya a la ficha **[!UICONTROL Usuarios]**
1. Seleccione el botón **[!UICONTROL Agregar usuario]**
   ![Seleccionar Agregar usuario](assets/adminconsole-launch-addUser.png)
1. Complete el flujo de trabajo para añadirse como usuario al perfil del producto

No es necesario que se incorpore como desarrollador para la recopilación de datos.

Ahora tiene casi todos los permisos necesarios para completar el tutorial. ¡Solo habrá dos ajustes más que harás dentro de [!DNL Adobe Admin Console], incluido uno después de [crear una zona protegida](create-a-sandbox.md)!
