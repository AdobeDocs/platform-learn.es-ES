---
title: Configuración de Developer Console y Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configuración de Developer Console y Postman
description: En esta lección, configurará un proyecto en Adobe Developer Console y le proporcionará  [!DNL Postman] colecciones para que pueda empezar a usar las API de Platform.
role: Data Architect, Data Engineer
feature: API
jira: KT-4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 0%

---

# Configurar Developer Console y [!DNL Postman]

<!--30min-->

En esta lección, debe configurar un proyecto en Adobe Developer Console y descargar [!DNL Postman] colecciones para poder empezar a usar las API de Platform.

Para completar los ejercicios de API de este tutorial, [descargue la aplicación de Postman para su sistema operativo.](https://www.postman.com/downloads/) Aunque no es necesario para usar las API de Experience Platform, Postman facilita los flujos de trabajo de las API y Adobe Experience Platform proporciona docenas de colecciones de Postman para ayudarle a ejecutar llamadas de API y aprender cómo funcionan. El resto de este tutorial supone algunos conocimientos prácticos de Postman. Para obtener ayuda, consulte la [documentación de Postman](https://learning.postman.com/).

Platform se crea primero según la API. Aunque también existen opciones de interfaz para todas las tareas principales, es posible que desee utilizar la API de Platform en algún momento. Por ejemplo, para introducir datos, mover elementos entre entornos limitados, automatizar tareas rutinarias o utilizar nuevas funciones de Platform antes de crear la interfaz de usuario.

Es posible que **los arquitectos de datos** y **los ingenieros de datos** tengan que usar la API de Platform fuera de este tutorial.

## Permisos necesarios

En la lección [Configurar permisos](configure-permissions.md), configuró todos los controles de acceso necesarios para completar esta lección.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Configuración de Adobe Developer Console

Adobe Developer Console es el destino del desarrollador para acceder a las API y SDK de Adobe, escuchar eventos casi en tiempo real, ejecutar funciones en tiempo de ejecución o crear complementos o aplicaciones de App Builder. Lo utilizará para acceder a la API de Experience Platform. Para obtener más información, consulte la [documentación de Adobe Developer Console](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. Cree una carpeta en su equipo local llamada `Luma Tutorial Assets` para los archivos utilizados en el tutorial.

1. Abrir [Adobe Developer Console](https://console.adobe.io){target="_blank"}

1. Inicie sesión y confirme que se encuentra en la organización correcta

1. Seleccione **[!UICONTROL Crear nuevo proyecto]** en el menú de [!UICONTROL Inicio rápido].

   ![Crear nuevo proyecto](assets/adobeio-createNewProject.png)


1. En el proyecto recién creado, seleccione el botón **[!UICONTROL Editar proyecto]**
1. Cambie **[!UICONTROL Project Title]** a `Luma Tutorial API Project` (agregue su nombre al final, si varias personas de su compañía realizan este tutorial)
1. Seleccionar **[!UICONTROL Guardar]**

   ![Configuración de la API del proyecto Adobe Developer Console](assets/adobeio-renameProject.png)


1. Seleccionar **[!UICONTROL Agregar API]**

   ![Configuración de la API del proyecto Adobe Developer Console](assets/adobeio-addAPI.png)

1. Filtre la lista seleccionando **[!UICONTROL Adobe Experience Platform]**

1. En la lista de API disponibles, seleccione **[!UICONTROL API de Experience Platform]** y seleccione **[!UICONTROL Siguiente]**.

   ![Configuración de la API del proyecto Adobe Developer Console](assets/adobeio-AEPAPI.png)

1. Seleccione **[!UICONTROL Servidor a servidor OAuth]** como credencial y seleccione **[!UICONTROL Siguiente]**.
   ![Seleccionar servidor a servidor OAuth](assets/adobeio-choose-auth.png)

1. Seleccione el perfil de producto `AEP-Default-All-Users` y seleccione **[!UICONTROL Guardar la API configurada]**

   ![Seleccionar perfil de producto](assets/adobeio-selectProductProfile.png)

1. Ahora se ha creado su proyecto de Developer Console.

1. En la sección **[!UICONTROL Probar]** de la página, seleccione **[!UICONTROL Descargar para Postman]** y, a continuación, seleccione **[!UICONTROL Servidor a servidor OAuth]** para descargar el archivo json del entorno [!DNL Postman]. Guarde `oauth_server_to_server.postman_environment.json` en la carpeta `Luma Tutorial Assets`.


   ![Configuración de la API del proyecto Adobe Developer Console](assets/adobeio-io-api.png)

## Pida a un administrador del sistema que añada la credencial de la API a la función

Para utilizar la credencial de la API e interactuar con el Experience Platform, un administrador del sistema deberá asignar las credenciales de la API a la función creada en la lección anterior.  Si no es administrador del sistema, envíeles lo siguiente:

1. El [!UICONTROL Nombre] de su credencial de API (`Credential in Luma Tutorial API Project`)
1. El [!UICONTROL correo electrónico técnico de la cuenta] de su credencial (esto ayudará al administrador del sistema a encontrar la credencial)

   ![[!UICONTROL Nombre] y [!UICONTROL Correo electrónico de cuenta técnica] de sus credenciales](assets/postman-credentialDetails.png)

Estas son las instrucciones para el administrador del sistema:

1. Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com)
1. Seleccione **[!UICONTROL Permisos]** en el panel de navegación izquierdo para acceder a la pantalla de [!UICONTROL Roles]
1. Abrir el rol `Luma Tutorial Platform`
   ![Abrir el rol](assets/postman-openRole.png)
1. Seleccione la ficha **[!UICONTROL Credenciales de API]**
1. Seleccionar **[!UICONTROL Agregar credenciales de API]**
   ![Agregar credencial](assets/postman-addCredential.png)
1. Busque la credencial `Credential in Luma Tutorial API Project`, filtrando con el [!UICONTROL correo electrónico de cuenta técnica] proporcionado por el participante del tutorial, si la lista es larga
1. Seleccione la credencial
1. Seleccionar **[!UICONTROL Guardar]**


   ![Agregar credencial](assets/postman-findCredential.png)

## Configuración de Postman

>[!CAUTION]
>
>La interfaz de Postman se actualiza regularmente. Las capturas de pantalla de este tutorial se tomaron con Postman v10.15.1 para Mac, pero las opciones de la interfaz pueden haber cambiado.


1. Descargar e instalar [[!DNL Postman]](https://www.postman.com/downloads/)
1. Abrir [!DNL Postman] y crear un área de trabajo
   ![Importar entorno](assets/postman-createWorkspace.png)

1. Importar el archivo de entorno json descargado, `oauth_server_to_server.postman_environment.json`
   ![Importar entorno](assets/postman-importEnvironment.png)
1. En [!DNL Postman], seleccione su entorno en la lista desplegable

1. Seleccione el icono para ver las variables de entorno:

   ![Cambiar entorno](assets/postman-changeEnvironment.png)


### Añadir el nombre y el ID de inquilino de la zona protegida

Las variables `SANDBOX_NAME`, `TENANT_ID` y `CONTAINER_ID` no se incluyen en la exportación de Adobe Developer Console, por lo que se agregan manualmente:

1. En [!DNL Postman], abra **Variables de entorno**
1. Seleccione el vínculo **Editar** a la derecha del nombre del entorno
1. En el **campo Agregar nueva variable**, escriba `SANDBOX_NAME`
1. En ambos campos de valor, escriba `luma-tutorial`, el nombre que le dimos a nuestra zona protegida en la lección anterior. Si ha utilizado un nombre diferente para la zona protegida, por ejemplo, luma-tutorial-ignatiusjreilly, asegúrese de utilizar ese valor.
1. En el **campo Agregar nueva variable**, escriba `TENANT_ID`
1. Cambie a su explorador web y busque el id de inquilino de su compañía en la interfaz de Experience Platform y extraiga la parte de la URL *después del signo @*. Por ejemplo, mi id. de inquilino es `techmarketingdemos`, pero el suyo es diferente:

   ![Obteniendo el id. de inquilino de la URL de la interfaz de Platform](assets/postman-getTenantId.png)

1. Copie este valor y vuelva a la pantalla Administrar entornos de [!DNL Postman]
1. Pegue su ID de inquilino en ambos campos de valor
1. En el **campo Agregar nueva variable**, escriba `CONTAINER_ID`
1. Escriba `global` en ambos campos de valor

   >[!NOTE]
   >
   >`CONTAINER_ID` es un campo cuyo valor cambiamos varias veces durante el tutorial. Cuando se usa `global`, la API interactúa con los elementos proporcionados por el Adobe en su cuenta de Platform. Cuando se usa `tenant`, la API interactúa con sus propios elementos personalizados.

1. Seleccionar **Guardar**

   ![Se agregaron los campos SANDBOX_NAME, TENANT_ID y CONTAINER_ID como variables de entorno](assets/postman-addEnvFields.png)



## Realizar llamadas de API

### Recuperación de un token de acceso

Adobe proporciona un completo conjunto de [!DNL Postman] colecciones para ayudarle a explorar la API de Experience Platform. Estas colecciones están en el [repositorio GitHub de muestras de Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples). Debe marcar este repositorio, ya que lo utilizará varias veces a lo largo de este tutorial y más tarde al implementar Experience Platform para su propia compañía.

La primera colección funciona con las API del servicio Identity Management de Adobe (IMS). Es una forma cómoda de recuperar un token de acceso desde Postman.

Para generar el token de acceso:

1. Descargue la [colección de API del servicio Identity Management](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) en su carpeta `Luma Tutorial Assets`
1. Importar la colección en [!DNL Postman]
1. Seleccione la solicitud **oAuth: Solicitar token de acceso** y seleccione **Enviar**
1. Debe obtener una respuesta `200 OK` con un token de acceso en la respuesta

   ![Solicitar los tokens](assets/postman-requestToken.png)

1. El token de acceso debe almacenarse automáticamente como la variable de entorno **ACCESS_TOKEN** de su entorno [!DNL Postman].

   ![Postman](assets/postman-config.png)


### Interacción con una API de Platform

Ahora vamos a hacer una llamada a la API de Platform para confirmar que hemos configurado todo correctamente.

Abra las [colecciones de Experience Platform [!DNL Postman] en GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Hay muchas colecciones en esta página para varias API de plataforma. Recomiendo encarecidamente marcarlo como favorito.

Ahora, vamos a hacer nuestra primera llamada de API:

1. Descargue la [colección de API de Registro de esquemas](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) en su carpeta `Luma Tutorial Assets`
1. Importarlo en [!DNL Postman]
1. Abra **API de Registro de esquemas > Esquemas > Enumerar esquemas**
1. Observe las pestañas **Params** y **Headers** y observe cómo incluyen algunas de las variables de entorno que ingresamos anteriormente.
1. Observe que el campo **Encabezados > Aceptar valor** está establecido en `application/vnd.adobe.xed-id+json`. Las API de Registro de esquemas requieren uno de estos [valores de encabezado Aceptar especificados](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=es#accept) que proporcionan formatos diferentes en la respuesta.
1. Seleccione **Enviar** para realizar su primera llamada a la API de Platform.

Esperamos que haya obtenido una respuesta correcta `200 OK` que contenga una lista de los esquemas XDM disponibles proporcionados por el Adobe en su zona protegida, como se muestra a continuación.

![Primera llamada API en Postman](assets/postman-firstAPICall.png)

Si la llamada no se realizó correctamente, dedique un momento a la depuración utilizando los detalles de respuesta de error de la llamada de API y revise los pasos anteriores. Si se queda atascado, solicite ayuda en el [Foro de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community?profile.language=es) o use el enlace que se encuentra en la parte derecha de esta página para &quot;Registrar un problema&quot;.

Con los permisos de plataforma, la zona protegida y [!DNL Postman] configurados, está listo para [modelar datos en esquemas](model-data-in-schemas.md).
