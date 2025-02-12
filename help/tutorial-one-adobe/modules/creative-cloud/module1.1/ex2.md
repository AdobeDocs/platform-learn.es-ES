---
title: Optimizar el proceso de Firefly con Microsoft Azure y las direcciones URL prefirmadas
description: Obtenga información sobre cómo optimizar el proceso de Firefly mediante Microsoft Azure y las direcciones URL prefirmadas
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: c29fb7908ee9a16a265f96d8181dca93fd9256cc
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 1%

---

# 1.1.2 Optimizar el proceso de Firefly mediante Microsoft Azure y las direcciones URL prefirmadas

Obtenga información sobre cómo optimizar el proceso de Firefly mediante Microsoft Azure y las direcciones URL prefirmadas.

## 1.1.2.1 Crear una suscripción de Azure

>[!NOTE]
>
>Si ya tiene una suscripción a Azure, puede omitir este paso. Continúe con el siguiente ejercicio en ese caso.

1. Vaya a [https://portal.azure.com](https://portal.azure.com){target="_blank"} e inicie sesión con su cuenta de Azure. Si no dispone de una, utilice su dirección de correo electrónico personal para crear su cuenta de Azure.

   ![Almacenamiento de Azure](./images/02azureportalemail.png){zoomable="yes"}

   Después de iniciar sesión correctamente, debería ver la siguiente pantalla:

   ![Almacenamiento de Azure](./images/03azureloggedin.png){zoomable="yes"}

1. En el menú de la izquierda, seleccione **Todos los recursos**. Si aún no se ha suscrito, aparecerá la pantalla de suscripción de Azure.

1. Si no se ha suscrito, seleccione **Comenzar con una versión de prueba gratuita de Azure**.

   ![Almacenamiento de Azure](./images/04azurestartsubscribe.png){zoomable="yes"}

1. Rellene el formulario de suscripción de Azure y proporcione su teléfono móvil y tarjeta de crédito para la activación (tendrá un nivel gratuito durante 30 días y no se le cobrará, a menos que actualice).

   Cuando finalice el proceso de suscripción, ya está listo para comenzar.

   ![Almacenamiento de Azure](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.2 Crear cuenta de almacenamiento de Azure

1. Busque `storage account` y luego seleccione **Cuentas de almacenamiento**.

   ![Almacenamiento de Azure](./images/azs1.png){zoomable="yes"}

1. Seleccione **+ Crear**.

   ![Almacenamiento de Azure](./images/azs2.png){zoomable="yes"}

1. Seleccione su **suscripción** y seleccione (o cree) un **grupo de recursos**.

1. En **nombre de cuenta de almacenamiento**, use `--aepUserLdap--`.

1. Seleccione **Revisar + crear**.

   ![Almacenamiento de Azure](./images/azs3.png){zoomable="yes"}

1. Seleccione **Crear**.

   ![Almacenamiento de Azure](./images/azs4.png){zoomable="yes"}

1. Después de la confirmación, seleccione **Ir al recurso**.

   ![Almacenamiento de Azure](./images/azs5.png){zoomable="yes"}

   Su cuenta de almacenamiento de Azure ya está lista para su uso.

   ![Almacenamiento de Azure](./images/azs6.png){zoomable="yes"}

1. Seleccione **Almacenamiento de datos** y luego vaya a **Contenedores**. Seleccionar **+ Contenedor**.

   ![Almacenamiento de Azure](./images/azs7.png){zoomable="yes"}

1. Use `--aepUserLdap--` para el nombre y seleccione **Crear**.

   ![Almacenamiento de Azure](./images/azs8.png){zoomable="yes"}

   El contenedor ya está listo para usarse.

   ![Almacenamiento de Azure](./images/azs9.png){zoomable="yes"}

## 1.1.2.3 Instalar Azure Storage Explorer

1. [Descargue Microsoft Azure Storage Explorer para administrar sus archivos](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. Seleccione la versión correcta para su sistema operativo específico, descárguela e instálela.

   ![Almacenamiento de Azure](./images/az10.png){zoomable="yes"}

1. Abra la aplicación y seleccione **Iniciar sesión con Azure**.

   ![Almacenamiento de Azure](./images/az11.png){zoomable="yes"}

1. Seleccione **Suscripción**.

   ![Almacenamiento de Azure](./images/az12.png){zoomable="yes"}

1. Seleccione **Azure** y después **Siguiente**.

   ![Almacenamiento de Azure](./images/az13.png){zoomable="yes"}

1. Seleccione su cuenta de Microsoft Azure y complete el proceso de autenticación.

   ![Almacenamiento de Azure](./images/az14.png){zoomable="yes"}

   Después de la autenticación, aparece este mensaje.

   ![Almacenamiento de Azure](./images/az15.png){zoomable="yes"}

1. Vuelva a la aplicación Microsoft Azure Storage Explorer, seleccione su suscripción y elija **Abrir explorador**.

   >[!NOTE]
   >
   >Si no se muestra tu cuenta, haz clic en el icono **engranaje** junto a tu dirección de correo electrónico y selecciona **Anular filtro**.

   ![Almacenamiento de Azure](./images/az16.png){zoomable="yes"}

   Su cuenta de almacenamiento aparece en **Cuentas de almacenamiento**.

   ![Almacenamiento de Azure](./images/az17.png){zoomable="yes"}

1. Abra **Contenedores de blobs** y seleccione el contenedor que creó en el ejercicio anterior.

   ![Almacenamiento de Azure](./images/az18.png){zoomable="yes"}

## 1.1.2.4 Carga manual de archivos y uso de un archivo de imagen como referencia de estilo

1. Cargue un archivo de imagen de su elección o [este archivo](./images/gradient.jpg){target="_blank"} en el contenedor.

   ![Almacenamiento de Azure](./images/gradient.jpg)

   Una vez cargado, puede verlo en su contenedor:

   ![Almacenamiento de Azure](./images/az19.png){zoomable="yes"}

1. Haga clic con el botón derecho en `gradient.jpg` y, a continuación, seleccione **Obtener firma de acceso compartido**.

   ![Almacenamiento de Azure](./images/az20.png){zoomable="yes"}

1. En **Permisos**, solo se requiere **Leer**. Seleccione **Crear**.

   ![Almacenamiento de Azure](./images/az21.png){zoomable="yes"}

1. Copie la URL firmada previamente para este archivo de imagen para la siguiente solicitud de API a Firefly.

   ![Almacenamiento de Azure](./images/az22.png){zoomable="yes"}

1. En Postman, abra la solicitud **POST - Firefly - T2I (styleref) V3**.
Esto aparece en **Cuerpo**.

   ![Almacenamiento de Azure](./images/az23.png){zoomable="yes"}

1. Reemplace la URL del marcador de posición por la URL prefirmada para su archivo de imagen y seleccione **Enviar**.

   ![Almacenamiento de Azure](./images/az24.png){zoomable="yes"}

1. Abra la imagen nueva de la respuesta de los servicios de Firefly en el explorador.

   ![Almacenamiento de Azure](./images/az25.png){zoomable="yes"}

   Aparece otra imagen con `horses in a field`, pero esta vez el estilo es similar al archivo de imagen proporcionado como referencia de estilo.

   ![Almacenamiento de Azure](./images/az26.png){zoomable="yes"}

## 1.1.2.5 Carga programática de archivos

Para usar la carga de archivos mediante programación con cuentas de almacenamiento de Azure, debe crear un nuevo token de **firma de acceso compartido (SAS)** con permisos que le permitan escribir un archivo.

1. En el Explorador de almacenamiento de Azure, haga clic con el botón secundario en el contenedor y seleccione **Obtener firma de acceso compartido**.

   ![Almacenamiento de Azure](./images/az27.png){zoomable="yes"}

1. En **Permisos**, seleccione los siguientes permisos necesarios:

   - **Leer**
   - **Agregar**
   - **Create**
   - **Write**
   - **Lista**

1. Seleccione **Crear**.

   ![Almacenamiento de Azure](./images/az28.png){zoomable="yes"}

1. Después de recibir tu **token SAS**, selecciona **Copiar**.

   ![Almacenamiento de Azure](./images/az29.png){zoomable="yes"}

   Use el **token SAS** para cargar un archivo en su cuenta de almacenamiento de Azure.

1. En Postman, selecciona la carpeta **FF - Firefly Services Tech Insiders**, luego selecciona **...** en la carpeta **Firefly** y, a continuación, selecciona **Agregar solicitud**.

   ![Almacenamiento de Azure](./images/az30.png){zoomable="yes"}

1. Cambie el nombre de la solicitud vacía a **Cargar archivo a la cuenta de almacenamiento de Azure**, cambie **Tipo de solicitud** a **PUT** y pegue la URL del token SAS en la sección URL y, a continuación, seleccione **Cuerpo**.

   ![Almacenamiento de Azure](./images/az31.png){zoomable="yes"}

1. A continuación, seleccione un archivo de su equipo local o use otro archivo de imagen ubicado [aquí](./images/gradient2-p.jpg){target="_blank"}.

   ![Archivo de degradación](./images/gradient2-p.jpg)

1. En **Cuerpo**, seleccione **binario**, a continuación **Seleccionar archivo** y, por último, seleccione **+ Nuevo archivo del equipo local**.

   ![Almacenamiento de Azure](./images/az32.png){zoomable="yes"}

1. Seleccione el archivo que desee y seleccione **Abrir**.

   ![Almacenamiento de Azure](./images/az33.png){zoomable="yes"}

1. A continuación, especifique el nombre de archivo que se utilizará en su cuenta de almacenamiento de Azure colocando el cursor delante del signo de interrogación **.** en la dirección URL de esta manera:

   ![Almacenamiento de Azure](./images/az34.png){zoomable="yes"}

   La dirección URL tiene este aspecto, pero debe cambiarse.

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

1. Cambie el nombre de archivo a `gradient2-p.jpg` y cambie la dirección URL para incluir el nombre de archivo de esta manera:

   `https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

   ![Almacenamiento de Azure](./images/az34a.png){zoomable="yes"}

1. A continuación, ve a **Encabezados** para agregar un nuevo encabezado manualmente de esta manera:

   | Clave | Valor |
   |:-------------:| :---------------:| 
   | `x-ms-blob-type` | `BlockBlob` |


   ![Almacenamiento de Azure](./images/az35.png){zoomable="yes"}

1. Vaya a **Autorización** y establezca **Tipo de autenticación** en **Sin autenticación** y seleccione **Enviar**.

   ![Almacenamiento de Azure](./images/az36.png){zoomable="yes"}

1. A continuación, esta respuesta vacía aparece en Postman, lo que significa que la carga del archivo es correcta.

   ![Almacenamiento de Azure](./images/az37.png){zoomable="yes"}

1. Cuando vuelva al Explorador de almacenamiento de Azure, actualice el contenido de la carpeta y aparecerá el archivo recién cargado.

   ![Almacenamiento de Azure](./images/az38.png){zoomable="yes"}

## 1.1.2.6 Uso de archivos programáticos

Para leer archivos mediante programación de cuentas de almacenamiento de Azure a largo plazo, debe crear un nuevo token de **firma de acceso compartido (SAS)**, con permisos que le permitan leer un archivo. Técnicamente, podría utilizar el token SAS creado en el ejercicio anterior, pero se recomienda tener un token independiente con solo permisos de **Read** y un token independiente con solo permisos de **Write**.

### Token SAS de lectura a largo plazo

1. Vuelva al Explorador de almacenamiento de Azure, haga clic con el botón secundario en el contenedor y, a continuación, seleccione **Obtener firma de acceso compartido**.

   ![Almacenamiento de Azure](./images/az27.png){zoomable="yes"}

1. En **Permisos**, seleccione los siguientes permisos necesarios:

   - **Leer**
   - **Lista**

1. Establezca **Tiempo de caducidad** en 1 año a partir de ahora.

1. Seleccione **Crear**.

   ![Almacenamiento de Azure](./images/az100.png){zoomable="yes"}

1. Copie la dirección URL y escríbala en un archivo del equipo para obtener el token SAS a largo plazo con permisos de lectura.

   ![Almacenamiento de Azure](./images/az101.png){zoomable="yes"}

   La dirección URL debe tener este aspecto:

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

   Puede derivar un par de valores de la dirección URL anterior:

   - `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
   - `AZURE_STORAGE_CONTAINER`: `vangeluw`
   - `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Token SAS de escritura a largo plazo

1. Vuelva al Explorador de almacenamiento de Azure, haga clic con el botón secundario en el contenedor y seleccione **Obtener firma de acceso compartido**.

   ![Almacenamiento de Azure](./images/az27.png){zoomable="yes"}

1. En **Permisos**, seleccione los siguientes permisos necesarios:

   - **Agregar**
   - **Create**
   - **Write**

1. Establezca el **Tiempo de caducidad** en 1 año a partir de ahora.

1. Seleccione **Crear**.

   ![Almacenamiento de Azure](./images/az102.png){zoomable="yes"}

1. Copie la dirección URL y escríbala en un archivo del equipo para obtener el token SAS a largo plazo con permisos de lectura.

   ![Almacenamiento de Azure](./images/az103.png){zoomable="yes"}

   La dirección URL debe tener este aspecto:

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

   Puede derivar un par de valores de la dirección URL anterior:

   - `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
   - `AZURE_STORAGE_CONTAINER`: `vangeluw`
   - `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
   - `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variables en Postman

>[!IMPORTANT]
>
>Si eres empleado de Adobe, sigue las instrucciones aquí para usar [PostBuster](./../../../postbuster.md).

Como puede ver en la sección anterior, hay algunas variables comunes en el token de lectura y en el token de escritura.

A continuación, debe crear variables en Postman que almacenen los distintos elementos de los tokens SAS anteriores. Hay algunos valores que son los mismos en ambas direcciones URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Para futuras interacciones de API, lo principal que cambia es el nombre del recurso, mientras que las variables anteriores siguen siendo las mismas. En ese caso, tiene sentido crear variables en Postman para que no tenga que especificarlas manualmente cada vez.

1. En Postman, seleccione **Entornos**, abra **Todas las variables** y seleccione **Entorno**.

   ![Almacenamiento de Azure](./images/az104.png){zoomable="yes"}

1. Cree estas 4 variables en la tabla que se muestra y, para las columnas **Valor inicial** y **Valor actual**, introduzca sus valores personales específicos.

   - `AZURE_STORAGE_URL`: su dirección URL
   - `AZURE_STORAGE_CONTAINER`: su nombre de contenedor
   - `AZURE_STORAGE_SAS_READ`: su token de lectura SAS
   - `AZURE_STORAGE_SAS_WRITE`: su token de escritura SAS

1. Seleccione **Guardar**.

   ![Almacenamiento de Azure](./images/az105.png){zoomable="yes"}

   En uno de los ejercicios anteriores, **Body** de su solicitud **Firefly - T2I (styleref) V3** tenía este aspecto:

   `"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

   ![Almacenamiento de Azure](./images/az24.png){zoomable="yes"}

1. Cambie la dirección URL a:

   `"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

1. Seleccione **Enviar** para probar los cambios que realizó.

   ![Almacenamiento de Azure](./images/az106.png){zoomable="yes"}

   Si las variables se configuraron correctamente, se devuelve una URL de imagen.

   ![Almacenamiento de Azure](./images/az107.png){zoomable="yes"}

1. Abra la dirección URL de la imagen para comprobar la imagen.

   ![Almacenamiento de Azure](./images/az108.jpg)

## Pasos siguientes

Vaya a [Trabajar con las API de Photoshop](./ex3.md){target="_blank"}

Volver a [Información general sobre los servicios de Adobe Firefly](./firefly-services.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
