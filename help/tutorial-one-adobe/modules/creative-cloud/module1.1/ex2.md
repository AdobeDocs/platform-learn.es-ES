---
title: Introducción a los servicios de Firefly
description: Introducción a los servicios de Firefly
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: ea06ca2d05195efa57643d45d7e50d3d914081d3
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---

# 1.1.2 Optimizar el proceso de Firefly mediante Microsoft Azure y las direcciones URL prefirmadas

## 1.1.2.1 Crear una suscripción de Azure

>[!NOTE]
>
>Si ya tiene una suscripción a Azure, puede omitir este paso. Continúe con el siguiente ejercicio en ese caso.

Vaya a [https://portal.azure.com](https://portal.azure.com) e inicie sesión con su cuenta de Azure. Si no dispone de una, utilice su dirección de correo electrónico personal para crear su cuenta de Azure.

![Almacenamiento de Azure](./images/02azureportalemail.png)

Después de iniciar sesión correctamente, verá la siguiente pantalla:

![Almacenamiento de Azure](./images/03azureloggedin.png)

Haga clic en el menú de la izquierda y seleccione **Todos los recursos**. Si aún no se ha suscrito, aparecerá la pantalla de suscripción de Azure. En ese caso, seleccione **Iniciar con una versión de prueba gratuita de Azure**.

![Almacenamiento de Azure](./images/04azurestartsubscribe.png)

Rellene el formulario de suscripción de Azure, proporcione su teléfono móvil y tarjeta de crédito para la activación (tendrá un nivel gratuito durante 30 días y no se le cobrará, a menos que actualice).

Cuando finalice el proceso de suscripción, ya está listo para comenzar:

![Almacenamiento de Azure](./images/06azuresubscriptionok.png)

## 1.1.2.2 Crear cuenta de almacenamiento de Azure

Busque `storage account` y haga clic en **Cuentas de almacenamiento**.

![Almacenamiento de Azure](./images/azs1.png)

Haga clic en **+ Crear**.

![Almacenamiento de Azure](./images/azs2.png)

Complete los siguientes detalles:

- Seleccione su **suscripción**
- Seleccione (o cree) un **grupo de recursos**
- **Nombre de cuenta de almacenamiento**: use `--aepUserLdap--`

Haga clic en **Revisar + crear**.

![Almacenamiento de Azure](./images/azs3.png)

Haga clic en **Crear**.

![Almacenamiento de Azure](./images/azs4.png)

A continuación, obtendrá una confirmación similar. Haga clic en **Ir al recurso**.

![Almacenamiento de Azure](./images/azs5.png)

Su cuenta de almacenamiento de Azure ya está lista para su uso.

![Almacenamiento de Azure](./images/azs6.png)

Haga clic en **Almacenamiento de datos** y luego vaya a **Contenedores**. Haga clic en **+ contenedor**.

![Almacenamiento de Azure](./images/azs7.png)

Para el nombre, use `--aepUserLdap--`. Haga clic en **Crear**.

![Almacenamiento de Azure](./images/azs8.png)

El contenedor ya está listo para usarse.

![Almacenamiento de Azure](./images/azs9.png)

## 1.1.2.3 Instalar Azure Storage Explorer

Utilizará el Explorador de almacenamiento de Microsoft Azure para administrar los archivos. Puede descargarlo a través de [este enlace](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4). Seleccione la versión correcta para su sistema operativo específico, descárguela e instálela.

![Almacenamiento de Azure](./images/az10.png)

Una vez instalada la aplicación, ábrala. Verá algo similar a esto. Haga clic en **Iniciar sesión con Azure**.

![Almacenamiento de Azure](./images/az11.png)

Haga clic en **Suscripción**.

![Almacenamiento de Azure](./images/az12.png)

Seleccione **Azure** y haga clic en **Siguiente**.

![Almacenamiento de Azure](./images/az13.png)

Seleccione su cuenta de Microsoft Azure y complete el proceso de autenticación.

![Almacenamiento de Azure](./images/az14.png)

Una vez autenticado, verá un mensaje como este.

![Almacenamiento de Azure](./images/az15.png)

Vuelva a la aplicación del Explorador de almacenamiento de Microsoft Azure. Seleccione su suscripción y haga clic en **Abrir explorador**.

![Almacenamiento de Azure](./images/az16.png)

Encontrará su cuenta de almacenamiento en **Cuentas de almacenamiento**.

![Almacenamiento de Azure](./images/az17.png)

Abra **Contenedores de blob** y haga clic en el contenedor que creó en el ejercicio anterior.

![Almacenamiento de Azure](./images/az18.png)

## 1.1.2.4 Carga manual de archivos y uso de un archivo de degradado como referencia de estilo

Ahora debe cargar un archivo de degradado de su elección en el contenedor. Puedes usar cualquier archivo de degradado que desees o [este archivo](./images/gradient.jpg) descargándolo en tu equipo.

![Almacenamiento de Azure](./images/gradient.jpg)

Coloque el archivo de degradado en el contenedor en el Explorador de almacenamiento de Azure.

Una vez cargado, lo verá en su contenedor:

![Almacenamiento de Azure](./images/az19.png)

Haga clic con el botón secundario en el archivo `gradient.jpg` y, a continuación, haga clic en **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az20.png)

En **Permisos**, solo se requiere **Leer**. Haga clic en **Crear**.

![Almacenamiento de Azure](./images/az21.png)

A continuación, verá la dirección URL firmada previamente para este archivo de imagen. Cópielo como lo necesite para la siguiente solicitud de API al Firefly.

![Almacenamiento de Azure](./images/az22.png)

Vuelva a Postman. Abra la solicitud **POST - Firefly - T2I (styleref) V3**. Verá esto en **Cuerpo**.

![Almacenamiento de Azure](./images/az23.png)

Reemplace la dirección URL del marcador de posición por la dirección URL prefirmada del archivo de degradado que copió del Explorador de almacenamiento de Azure. Entonces, tendrás esto. Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/az24.png)

Recibirá una respuesta de Servicios de Firefly de nuevo, con una imagen nueva. Abra el archivo de imagen en el explorador.

![Almacenamiento de Azure](./images/az25.png)

Verá otra imagen con `horses in a field`, pero esta vez el estilo será similar al archivo de degradado proporcionado como referencia de estilo.

![Almacenamiento de Azure](./images/az26.png)

## 1.1.2.5 Carga programática de archivos

Para usar la carga de archivos mediante programación con cuentas de almacenamiento de Azure, deberá crear un nuevo token de **firma de acceso compartido (SAS)**, con permisos que le permitan escribir un archivo.

Para ello, vuelva al Explorador de almacenamiento de Azure. Haga clic con el botón secundario en el contenedor y, a continuación, haga clic en **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az27.png)

En **Permisos**, se requieren los siguientes permisos:

- **Leer**
- **Agregar**
- **Create**
- **Write**
- **Lista**

Haga clic en **Crear**.

![Almacenamiento de Azure](./images/az28.png)

Luego obtendrá su **token SAS**. Haga clic en **Copiar**.

![Almacenamiento de Azure](./images/az29.png)

Ahora puede usar este **token SAS** para cargar un archivo en su cuenta de almacenamiento de Azure. Vuelva a Postman para hacerlo.

Haga clic para seleccionar la carpeta **FF - Firefly Services Tech Insiders**, luego haga clic en los 3 puntos **...** de la carpeta **Firefly** y, a continuación, haga clic en **Agregar solicitud**.

![Almacenamiento de Azure](./images/az30.png)

A continuación, tendrá una solicitud vacía. Cambie el nombre de la solicitud a **Cargar archivo a la cuenta de almacenamiento de Azure**, cambie **Tipo de solicitud** a **PUT** y pegue la URL del token SAS en la sección URL.

A continuación, haga clic en **Cuerpo**.

![Almacenamiento de Azure](./images/az31.png)

Ahora tendrá que seleccionar un archivo del equipo local. Puede usar un nuevo archivo de imagen o usar otro archivo de degradado que encuentre [aquí](./images/gradient2-p.jpg).

![Archivo de degradación](./images/gradient2-p.jpg)

En **Cuerpo**, seleccione **binario**, haga clic en **Seleccionar archivo** y, a continuación, haga clic en **+ Nuevo archivo del equipo local**.

![Almacenamiento de Azure](./images/az32.png)

Seleccione el archivo que desee y haga clic en **Abrir**.

![Almacenamiento de Azure](./images/az33.png)

Entonces verá esto... Lo siguiente que debe hacer es especificar el nombre de archivo que se utilizará en su cuenta de almacenamiento de Azure. Para ello, ¿necesita poner sus cursos delante del signo de interrogación **?** en la dirección URL. Actualmente puede ver esto allí:

![Almacenamiento de Azure](./images/az34.png)

La dirección URL tiene este aspecto, pero debe cambiarse.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

El nombre de archivo que se va a usar es `gradient2-p.jpg`, lo que significa que la dirección URL debe cambiar para incluir el nombre de archivo, de esta manera:

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Almacenamiento de Azure](./images/az34a.png)

A continuación, ve a **Encabezados** donde debes agregar un nuevo encabezado manualmente. Utilice esto:

x-ms-blob-type BlockBlob

![Almacenamiento de Azure](./images/az35.png)

Vaya a **Autorización** y establezca **Tipo de autenticación** en **Sin autenticación**. Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/az36.png)

Verá esta respuesta vacía en Postman, lo que significa que la carga del archivo se realizó correctamente.

![Almacenamiento de Azure](./images/az37.png)

Si vuelve al Explorador de almacenamiento de Azure y actualiza el contenido de la carpeta, ahora encontrará allí el archivo recién cargado.

![Almacenamiento de Azure](./images/az38.png)

Paso siguiente: [1.1.3 ...](./ex3.md)

[Volver al módulo 1.1](./firefly-services.md)

[Volver a todos los módulos](./../../../overview.md)
