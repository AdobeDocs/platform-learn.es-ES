---
title: Configuración de Developer Console y Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configuración de Developer Console y Postman
description: En esta lección, debe configurar un proyecto en la consola de Adobe Developer y proporcionarle lo siguiente [!DNL Postman] Colecciones para que pueda empezar a utilizar las API de Platform.
role: Data Architect, Data Engineer
feature: API
kt: 4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 35242a037bc79f18e90399c47e47064634d26a37
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# Configurar Developer Console y [!DNL Postman]

<!--30min-->

En esta lección, debe configurar un proyecto en la consola de Adobe Developer y descargar [!DNL Postman] para que pueda empezar a utilizar las API de Platform.

Para completar los ejercicios de API de este tutorial, haga lo siguiente: [descargue la aplicación de Postman para su sistema operativo.](https://www.postman.com/downloads/) Aunque no es necesario para utilizar las API de Experience Platform, Postman facilita los flujos de trabajo de las API y Adobe Experience Platform proporciona decenas de colecciones de Postman para ayudarle a ejecutar llamadas de API y aprender cómo funcionan. El resto de este tutorial supone algunos conocimientos prácticos de Postman. Para obtener ayuda, consulte la [Documentación de Postman](https://learning.postman.com/).

Platform se crea primero según la API. Aunque también existen opciones de interfaz para todas las tareas principales, es posible que desee utilizar la API de Platform en algún momento. Por ejemplo, para introducir datos, mover elementos entre entornos limitados, automatizar tareas rutinarias o utilizar nuevas funciones de Platform antes de crear la interfaz de usuario.

**Arquitectos de datos** y **Ingenieros de datos** puede que necesite utilizar la API de Platform fuera de este tutorial.

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) Esta lección, ha configurado todos los controles de acceso necesarios para completar esta lección.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Configuración de la consola de Adobe Developer

La consola de Adobe Developer es el destino del desarrollador para acceder a las API y SDK de Adobe, escuchar eventos casi en tiempo real, ejecutar funciones en tiempo de ejecución o crear complementos o aplicaciones de App Builder. Lo utilizará para acceder a la API de Experience Platform. Para obtener más información, consulte la [Documentación de la consola Adobe Developer](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. Cree una carpeta en el equipo local con el nombre `Luma Tutorial Assets` para archivos utilizados en el tutorial.

1. Abra el [Consola de Adobe Developer](https://console.adobe.io){target="_blank"}

1. Inicie sesión y confirme que se encuentra en la organización correcta

1. Seleccionar **[!UICONTROL Crear nuevo proyecto]** in [!UICONTROL Inicio rápido] menú.

   ![Crear nuevo proyecto](assets/adobeio-createNewProject.png)


1. En el proyecto recién creado, seleccione **[!UICONTROL Editar proyecto]** botón
1. Cambie el **[!UICONTROL Título del proyecto]** hasta `Luma Tutorial API Project` (añada su nombre al final, si varias personas de su compañía realizan este tutorial)
1. Seleccione **[!UICONTROL Guardar]**

   ![Configuración de API del proyecto de la consola Adobe Developer](assets/adobeio-renameProject.png)


1. Seleccionar **[!UICONTROL Añadir API]**

   ![Configuración de API del proyecto de la consola Adobe Developer](assets/adobeio-addAPI.png)

1. Filtre la lista seleccionando **[!UICONTROL Adobe Experience Platform]**

1. En la lista de API disponibles, seleccione **[!UICONTROL API de Experience Platform]** y seleccione **[!UICONTROL Siguiente]**.

   ![Configuración de API del proyecto de la consola Adobe Developer](assets/adobeio-AEPAPI.png)

1. Seleccionar **[!UICONTROL Servidor a servidor OAuth]** como credencial y seleccione **[!UICONTROL Siguiente]**.
   ![Seleccionar servidor a servidor OAuth](assets/adobeio-choose-auth.png)

1. Seleccione el `AEP-Default-All-Users` perfil de producto y seleccione **[!UICONTROL Guardar API configurada]**

   ![Seleccionar perfil de producto](assets/adobeio-selectProductProfile.png)

1. Ahora se ha creado su proyecto de Developer Console.

1. En el **[!UICONTROL Pruébelo.]** de la página, seleccione **[!UICONTROL Descargar para Postman]** y luego seleccione **[!UICONTROL Servidor a servidor OAuth]** para descargar [!DNL Postman] archivo json de entorno. Guarde el `oauth_server_to_server.postman_environment.json` en su `Luma Tutorial Assets` carpeta.


   ![Configuración de API del proyecto de la consola Adobe Developer](assets/adobeio-io-api.png)

## Pida a un administrador del sistema que añada la credencial de la API a la función

Para utilizar la credencial de la API e interactuar con el Experience Platform, un administrador del sistema deberá asignar las credenciales de la API a la función creada en la lección anterior.  Si no es administrador del sistema, envíeles lo siguiente:

1. El [!UICONTROL Nombre] de su credencial de API (`Credential in Luma Tutorial API Project`)
1. El [!UICONTROL Correo electrónico de cuenta técnica] de sus credenciales (esto ayudará al administrador del sistema a encontrar las credenciales)

   ![[!UICONTROL Nombre] y [!UICONTROL Correo electrónico de cuenta técnica] de su credencial](assets/postman-credentialDetails.png)

Estas son las instrucciones para el administrador del sistema:

1. Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com)
1. Seleccionar **[!UICONTROL Permisos]** en la navegación de la izquierda, que le llevará a la [!UICONTROL Funciones] pantalla
1. Abra el `Luma Tutorial Platform` función
   ![Abra la función](assets/postman-openRole.png)
1. Seleccione el **[!UICONTROL Credenciales de API]** pestaña
1. Seleccionar **[!UICONTROL Añadir credenciales de API]**
   ![Añadir credencial](assets/postman-addCredential.png)
1. Busque el `Credential in Luma Tutorial API Project` credencial, filtrar con la variable [!UICONTROL Correo electrónico de cuenta técnica] proporcionada por el participante del tutorial, si la lista es larga
1. Seleccione la credencial
1. Seleccione **[!UICONTROL Guardar]**


   ![Añadir credencial](assets/postman-findCredential.png)

## Configuración de Postman

>[!CAUTION]
>
>La interfaz de Postman se actualiza regularmente. Las capturas de pantalla de este tutorial se tomaron con Postman v10.15.1 para Mac, pero las opciones de la interfaz pueden haber cambiado.


1. Descargar e instalar [[!DNL Postman]](https://www.postman.com/downloads/)
1. Abrir [!DNL Postman] y cree un espacio de trabajo
   ![Importar entorno](assets/postman-createWorkspace.png)

1. Importe el archivo de entorno json descargado, `oauth_server_to_server.postman_environment.json`
   ![Importar entorno](assets/postman-importEnvironment.png)
1. Entrada [!DNL Postman], seleccione su entorno en la lista desplegable

1. Seleccione el icono para ver las variables de entorno:

   ![Cambiar entorno](assets/postman-changeEnvironment.png)


### Añadir el nombre y el ID de inquilino de la zona protegida

El `SANDBOX_NAME` y `TENANT_ID` y `CONTAINER_ID` Las variables de no se incluyen en la exportación de la consola de Adobe Developer, por lo que se añaden manualmente:

1. Entrada [!DNL Postman], abra el **Variables de entorno**
1. Seleccione el **Editar** vínculo a la derecha del nombre del entorno
1. En el **Agregar nuevo campo de variable**, introduzca `SANDBOX_NAME`
1. En ambos campos de valor, introduzca `luma-tutorial`, el nombre que le dimos a nuestra zona protegida en la lección anterior. Si ha utilizado un nombre diferente para la zona protegida, por ejemplo, luma-tutorial-ignatiusjreilly, asegúrese de utilizar ese valor.
1. En el **Agregar nuevo campo de variable**, introduzca `TENANT_ID`
1. Cambie al explorador web y busque el ID de inquilino de su empresa en la interfaz de Experience Platform y extraiga la parte de la dirección URL *después del signo @*. Por ejemplo, mi ID de inquilino es `techmarketingdemos` pero el tuyo es diferente:

   ![Obtención del ID de inquilino desde la URL de la interfaz de Platform](assets/postman-getTenantId.png)

1. Copie este valor y vuelva a la [!DNL Postman] Pantalla Administrar entornos
1. Pegue su ID de inquilino en ambos campos de valor
1. En el **Agregar nuevo campo de variable**, introduzca `CONTAINER_ID`
1. Entrar `global` en ambos campos de valor

   >[!NOTE]
   >
   >`CONTAINER_ID` es un campo cuyo valor cambiamos varias veces durante el tutorial. Cuándo `global` , la API interactúa con los elementos proporcionados por el Adobe en su cuenta de Platform. Cuándo `tenant` , la API interactúa con sus propios elementos personalizados.

1. Seleccione **Guardar**

   ![Los campos SANDBOX_NAME, TENANT_ID y CONTAINER_ID se han añadido como variables de entorno](assets/postman-addEnvFields.png)



## Realizar llamadas de API

### Recuperación de un token de acceso

El Adobe proporciona un conjunto completo de [!DNL Postman] colecciones para ayudarle a explorar la API de Experience Platform. Estas colecciones se encuentran en la [Adobe Experience Platform Postman Ejemplos Repositorio de GitHub](https://github.com/adobe/experience-platform-postman-samples). Debe marcar este repositorio, ya que lo utilizará varias veces a lo largo de este tutorial y más tarde al implementar Experience Platform para su propia compañía.

La primera colección funciona con las API del servicio Identity Management de Adobe (IMS). Es una forma cómoda de recuperar un token de acceso desde Postman.

Para generar el token de acceso:

1. Descargue la [Recopilación de API del servicio Identity Management](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) a su `Luma Tutorial Assets` carpeta
1. Importe la colección en [!DNL Postman]
1. Seleccione la solicitud **oAuth: Solicitar token de acceso** solicitar y seleccionar **Enviar**
1. Usted debe conseguir una `200 OK` respuesta con un token de acceso en la respuesta

   ![Solicitar los tokens](assets/postman-requestToken.png)

1. El token de acceso debe almacenarse automáticamente como **ACCESS_TOKEN** variable de entorno de su [!DNL Postman] entorno.

   ![Postman](assets/postman-config.png)


### Interacción con una API de Platform

Ahora vamos a hacer una llamada a la API de Platform para confirmar que hemos configurado todo correctamente.

Abra el [Experience Platform [!DNL Postman] colecciones en GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Hay muchas colecciones en esta página para varias API de plataforma. Recomiendo encarecidamente marcarlo como favorito.

Ahora, vamos a hacer nuestra primera llamada de API:

1. Descargue la [Colección de API de Registro de esquemas](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) a su `Luma Tutorial Assets` carpeta
1. Importarlo en [!DNL Postman]
1. Abrir **API de Registro de Esquemas > Esquemas > Enumerar esquemas**
1. Consulte la **Parámetros** y **Encabezados** y observe cómo incluyen algunas de las variables de entorno que ingresamos anteriormente.
1. Tenga en cuenta que la variable **Encabezados > Aceptar campo de valor** se establece en `application/vnd.adobe.xed-id+json`. Las API de Registro de esquemas requieren uno de estos elementos [valores de encabezado Aceptar especificados](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) que proporcionan diferentes formatos en la respuesta.
1. Seleccionar **Enviar** para realizar su primera llamada a la API de Platform.

Espero que tengas éxito `200 OK` Respuesta que contiene una lista de los esquemas XDM disponibles proporcionados por el Adobe en la zona protegida, como se muestra a continuación.

![Primera llamada de API en Postman](assets/postman-firstAPICall.png)

Si la llamada no se realizó correctamente, dedique un momento a la depuración utilizando los detalles de respuesta de error de la llamada de API y revise los pasos anteriores. Si se queda atascado, por favor solicite ayuda en el [Foro de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community?profile.language=es) o utilice el enlace de la derecha de esta página para &quot;Registrar un problema&quot;.

Con los permisos de Platform, la zona protegida y [!DNL Postman] configurado, está listo para [datos de modelo en esquemas](model-data-in-schemas.md)!
