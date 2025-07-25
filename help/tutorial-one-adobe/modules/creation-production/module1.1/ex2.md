---
title: Optimizar el proceso de Firefly con Microsoft Azure y las direcciones URL prefirmadas
description: Obtenga información sobre cómo optimizar el proceso de Firefly mediante Microsoft Azure y las direcciones URL prefirmadas
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: a1da1c73cbddacde00211190a1ca3d36f7a2c329
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 1%

---

# 1.1.2 Optimizar el proceso de Firefly mediante Microsoft Azure y las direcciones URL prefirmadas

Obtenga información sobre cómo optimizar el proceso de Firefly mediante Microsoft Azure y las direcciones URL prefirmadas.

## 1.1.2.1 ¿Qué son las direcciones URL prefirmadas?

Una dirección URL prefirmada es una dirección URL que concede acceso temporal a un objeto específico en una ubicación de almacenamiento. Mediante la dirección URL, un usuario puede, por ejemplo, LEER el objeto o ESCRIBIR un objeto (o actualizar un objeto existente). La dirección URL contiene parámetros específicos que establece la aplicación.

En el contexto de la creación de automatización de la cadena de suministro de contenido, a menudo hay varias operaciones de archivo que deben realizarse para un caso de uso específico. Por ejemplo, puede que sea necesario cambiar el fondo de un archivo, el texto de varias capas, etc. No siempre es posible realizar todas las operaciones de archivo al mismo tiempo, lo que crea la necesidad de un enfoque de varios pasos. Después de cada paso intermedio, la salida es un archivo temporal necesario para ejecutar el siguiente paso. Una vez ejecutado el siguiente paso, el archivo temporal pierde valor rápidamente y, a menudo, ya no es necesario, por lo que debe eliminarse.

Actualmente, Adobe Firefly Services admite estos dominios:

- Amazon AWS: *.amazonaws.com
- Microsoft Azure: *.windows.net
- Dropbox: *.dropboxusercontent.com

El motivo por el que a menudo se utilizan soluciones de almacenamiento en la nube es que los recursos intermedios que se crean pierden valor rápidamente. El problema que se resuelve con las URL prefirmadas suele resolverse mejor con una solución de almacenamiento de productos, que suele ser uno de los servicios en la nube anteriores.

Dentro del ecosistema de Adobe también hay soluciones de almacenamiento, como Frame.io, Workfront Fusion y recursos de Adobe Experience Manager. Estas soluciones también admiten direcciones URL prefirmadas, por lo que a menudo se convierten en una opción que debe realizarse durante la implementación. La elección suele basarse en una combinación de aplicaciones ya disponibles y costes de almacenamiento.

Como tal, las direcciones URL prefirmadas se utilizan en combinación con las operaciones de Adobe Firefly Services porque:

- las organizaciones suelen necesitar procesar varios cambios en la misma imagen en pasos intermedios, y se necesita un almacenamiento intermedio para que sea posible.
- el acceso a la lectura y escritura desde ubicaciones de almacenamiento en la nube debe ser seguro y, en un entorno del lado del servidor, no es posible iniciar sesión manualmente, por lo que la seguridad debe codificarse directamente en la dirección URL.

Una URL firmada previamente utiliza tres parámetros para limitar el acceso al usuario:

- Ubicación de almacenamiento: podría ser una ubicación de bloque de AWS S3, una ubicación de cuenta de almacenamiento de Microsoft Azure con contenedor
- Nombre de archivo: el archivo específico que debe leerse, actualizarse y eliminarse.
- Query string parameter: un parámetro de cadena de consulta siempre comienza con un signo de interrogación y va seguido de una serie compleja de parámetros

Por ejemplo:

- **Amazon AWS**: `https://bucket.s3.eu-west-2.amazonaws.com/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AXXXXXXXXXX%2Feu-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250510T171315Z&X-Amz-Expires=1800&X-Amz-Signature=XXXXXXXXX&X-Amz-SignedHeaders=host`
- **Microsoft Azure**: `https://storageaccount.blob.core.windows.net/container/image.png?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=XXXXXX%3D`

## 1.1.2.2 crear una suscripción de Azure

>[!NOTE]
>
>Si ya tiene una suscripción a Azure, puede omitir este paso. Continúe con el siguiente ejercicio en ese caso.

>[!NOTE]
>
>Si está siguiendo este tutorial como parte de un taller guiado en persona o de una formación guiada bajo demanda, es probable que ya tenga acceso a una cuenta de almacenamiento de Microsoft Azure. En ese caso, no es necesario que cree su propia cuenta; utilice la cuenta que se le ha proporcionado como parte de la formación.

Vaya a [https://portal.azure.com](https://portal.azure.com){target="_blank"} e inicie sesión con su cuenta de Azure. Si no dispone de una, utilice su dirección de correo electrónico personal para crear su cuenta de Azure.

![Almacenamiento de Azure](./images/02azureportalemail.png){zoomable="yes"}

Después de iniciar sesión correctamente, debería ver la siguiente pantalla:

![Almacenamiento de Azure](./images/03azureloggedin.png){zoomable="yes"}

En el menú de la izquierda, seleccione **Todos los recursos**. Si aún no se ha suscrito, aparecerá la pantalla de suscripción de Azure.

Si no se ha suscrito, seleccione **Comenzar con una versión de prueba gratuita de Azure**.

![Almacenamiento de Azure](./images/04azurestartsubscribe.png){zoomable="yes"}

Rellene el formulario de suscripción de Azure y proporcione su teléfono móvil y tarjeta de crédito para la activación (tendrá un nivel gratuito durante 30 días y no se le cobrará, a menos que actualice).

Cuando finalice el proceso de suscripción, ya está listo para comenzar.

![Almacenamiento de Azure](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.3 Crear cuenta de almacenamiento de Azure

Busque `storage account` y luego seleccione **Cuentas de almacenamiento**.

![Almacenamiento de Azure](./images/azs1.png){zoomable="yes"}

Seleccione **+ Crear**.

![Almacenamiento de Azure](./images/azs2.png){zoomable="yes"}

Seleccione su **suscripción** y seleccione (o cree) un **grupo de recursos**.

En **nombre de cuenta de almacenamiento**, use `--aepUserLdap--`.

Seleccione **Revisar + crear**.

![Almacenamiento de Azure](./images/azs3.png){zoomable="yes"}

Seleccione **Crear**.

![Almacenamiento de Azure](./images/azs4.png){zoomable="yes"}

Después de la confirmación, seleccione **Ir al recurso**.

![Almacenamiento de Azure](./images/azs5.png){zoomable="yes"}

Su cuenta de almacenamiento de Azure ya está lista para su uso.

![Almacenamiento de Azure](./images/azs6.png){zoomable="yes"}

Seleccione **Almacenamiento de datos** y luego vaya a **Contenedores**. Seleccionar **+ Contenedor**.

![Almacenamiento de Azure](./images/azs7.png){zoomable="yes"}

Use `--aepUserLdap--` para el nombre y seleccione **Crear**.

![Almacenamiento de Azure](./images/azs8.png){zoomable="yes"}

El contenedor ya está listo para usarse.

![Almacenamiento de Azure](./images/azs9.png){zoomable="yes"}

## 1.1.2.4 Instalar Azure Storage Explorer

[Descargue Microsoft Azure Storage Explorer para administrar sus archivos](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. Seleccione la versión correcta para su sistema operativo específico, descárguela e instálela.

![Almacenamiento de Azure](./images/az10.png){zoomable="yes"}

Abra la aplicación y seleccione **Iniciar sesión con Azure**.

![Almacenamiento de Azure](./images/az11.png){zoomable="yes"}

Seleccione **Suscripción**.

![Almacenamiento de Azure](./images/az12.png){zoomable="yes"}

Seleccione **Azure** y después **Siguiente**.

![Almacenamiento de Azure](./images/az13.png){zoomable="yes"}

Seleccione su cuenta de Microsoft Azure y complete el proceso de autenticación.

![Almacenamiento de Azure](./images/az14.png){zoomable="yes"}

Después de la autenticación, aparece este mensaje.

![Almacenamiento de Azure](./images/az15.png){zoomable="yes"}

Vuelva a la aplicación Microsoft Azure Storage Explorer, seleccione su suscripción y elija **Abrir explorador**.

>[!NOTE]
>
>Si no se muestra tu cuenta, haz clic en el icono **engranaje** junto a tu dirección de correo electrónico y selecciona **Anular filtro**.

![Almacenamiento de Azure](./images/az16.png){zoomable="yes"}

Su cuenta de almacenamiento aparece en **Cuentas de almacenamiento**.

![Almacenamiento de Azure](./images/az17.png){zoomable="yes"}

Abra **Contenedores de blobs** y seleccione el contenedor que creó en el ejercicio anterior.

![Almacenamiento de Azure](./images/az18.png){zoomable="yes"}

## 1.1.2.5: carga manual de archivos y uso de un archivo de imagen como referencia de estilo

Cargue un archivo de imagen de su elección o [este archivo](./images/gradient.jpg){target="_blank"} en el contenedor.

>[!NOTE]
>
>Cuando se utilizan imágenes como referencia de estilo, referencia de composición o como imagen de máscara, se aceptan los siguientes tipos de imagen:
>- image/jpeg
>- image/png
>- image/webp

![Almacenamiento de Azure](./images/gradient.jpg)

Una vez cargado, puede verlo en su contenedor:

![Almacenamiento de Azure](./images/az19.png){zoomable="yes"}

Haga clic con el botón derecho en `gradient.jpg` y, a continuación, seleccione **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az20.png){zoomable="yes"}

En **Permisos**, solo se requiere **Leer**. Seleccione **Crear**.

![Almacenamiento de Azure](./images/az21.png){zoomable="yes"}

Copie la URL firmada previamente para este archivo de imagen para la siguiente solicitud de API a Firefly.

![Almacenamiento de Azure](./images/az22.png){zoomable="yes"}

En Postman, abra la solicitud **POST - Firefly - T2I (styleref) V3**.
Esto aparece en **Cuerpo**.

![Almacenamiento de Azure](./images/az23.png){zoomable="yes"}

Reemplace la URL del marcador de posición por la URL prefirmada para su archivo de imagen y seleccione **Enviar**.

![Almacenamiento de Azure](./images/az24.png){zoomable="yes"}

Abra la nueva imagen de Firefly Services de respuesta en el explorador.

![Almacenamiento de Azure](./images/az25.png){zoomable="yes"}

Aparece otra imagen con `horses in a field`, pero esta vez el estilo es similar al archivo de imagen proporcionado como referencia de estilo.

![Almacenamiento de Azure](./images/az26.png){zoomable="yes"}

## 1.1.2.6: carga de archivo mediante programación

Para usar la carga de archivos mediante programación con cuentas de almacenamiento de Azure, debe crear un nuevo token de **firma de acceso compartido (SAS)** con permisos que le permitan escribir un archivo.

En el Explorador de almacenamiento de Azure, haga clic con el botón secundario en el contenedor y seleccione **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az27.png){zoomable="yes"}

En **Permisos**, seleccione los siguientes permisos necesarios:

- **Leer**
- **Agregar**
- **Create**
- **Write**
- **Lista**

Seleccione **Crear**.

![Almacenamiento de Azure](./images/az28.png){zoomable="yes"}

Después de recibir tu **firma de acceso compartido**, selecciona **Copiar** para copiar la URL.

![Almacenamiento de Azure](./images/az29.png){zoomable="yes"}

Use la **URL de token SAS** para cargar un archivo en su cuenta de almacenamiento de Azure.

En Postman, selecciona la carpeta **FF - Firefly Services Tech Insiders**, luego selecciona **...** en la carpeta **Firefly** y, a continuación, selecciona **Agregar solicitud**.

![Almacenamiento de Azure](./images/az30.png){zoomable="yes"}

Cambie el nombre de la solicitud vacía a **Cargar archivo a la cuenta de almacenamiento de Azure**, cambie **Tipo de solicitud** a **PUT** y pegue la URL del token SAS en la sección URL y, a continuación, seleccione **Cuerpo**.

![Almacenamiento de Azure](./images/az31.png){zoomable="yes"}

A continuación, seleccione un archivo de su equipo local o use otro archivo de imagen ubicado [aquí](./images/gradient2-p.jpg){target="_blank"}.

![Archivo de degradación](./images/gradient2-p.jpg)

En **Cuerpo**, seleccione **binario**, a continuación **Seleccionar archivo** y, por último, seleccione **+ Nuevo archivo del equipo local**.

![Almacenamiento de Azure](./images/az32.png){zoomable="yes"}

Seleccione el archivo que desee y seleccione **Abrir**.

![Almacenamiento de Azure](./images/az33.png){zoomable="yes"}

A continuación, especifique el nombre de archivo que se utilizará en su cuenta de almacenamiento de Azure colocando el cursor delante del signo de interrogación **.** en la dirección URL de esta manera:

![Almacenamiento de Azure](./images/az34.png){zoomable="yes"}

La dirección URL tiene este aspecto, pero debe cambiarse.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

Cambie el nombre de archivo a `gradient2-p.jpg` y cambie la dirección URL para incluir el nombre de archivo de esta manera:

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Almacenamiento de Azure](./images/az34a.png){zoomable="yes"}

A continuación, ve a **Encabezados** para agregar un nuevo encabezado manualmente de esta manera:

| Clave | Valor |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Almacenamiento de Azure](./images/az35.png){zoomable="yes"}

Vaya a **Autorización** y establezca **Tipo de autenticación** en **Sin autenticación** y seleccione **Enviar**.

![Almacenamiento de Azure](./images/az36.png){zoomable="yes"}

A continuación, esta respuesta vacía aparece en Postman, lo que significa que la carga del archivo es correcta.

![Almacenamiento de Azure](./images/az37.png){zoomable="yes"}

Cuando vuelva al Explorador de almacenamiento de Azure, actualice el contenido de la carpeta y aparecerá el archivo recién cargado.

![Almacenamiento de Azure](./images/az38.png){zoomable="yes"}

## 1.1.2.7 uso de archivos de programación

Para leer archivos mediante programación de cuentas de almacenamiento de Azure a largo plazo, debe crear un nuevo token de **firma de acceso compartido (SAS)**, con permisos que le permitan leer un archivo. Técnicamente, podría utilizar el token SAS creado en el ejercicio anterior, pero se recomienda tener un token independiente con solo permisos de **Read** y un token independiente con solo permisos de **Write**.

### Token SAS de lectura a largo plazo

Vuelva al Explorador de almacenamiento de Azure, haga clic con el botón secundario en el contenedor y, a continuación, seleccione **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az27.png){zoomable="yes"}

En **Permisos**, seleccione los siguientes permisos necesarios:

- **Leer**
- **Lista**

Establezca **Tiempo de caducidad** en 1 año a partir de ahora.

Seleccione **Crear**.

![Almacenamiento de Azure](./images/az100.png){zoomable="yes"}

Copie la dirección URL y escríbala en un archivo del equipo para obtener el token SAS a largo plazo con permisos de lectura.

![Almacenamiento de Azure](./images/az101.png){zoomable="yes"}

La dirección URL debe tener este aspecto:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

Puede derivar un par de valores de la dirección URL anterior:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Token SAS de escritura a largo plazo

Vuelva al Explorador de almacenamiento de Azure, haga clic con el botón secundario en el contenedor y seleccione **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az27.png){zoomable="yes"}

En **Permisos**, seleccione los siguientes permisos necesarios:

- **Leer**
- **Lista**
- **Agregar**
- **Create**
- **Write**

Establezca el **Tiempo de caducidad** en 1 año a partir de ahora.

Seleccione **Crear**.

![Almacenamiento de Azure](./images/az102.png){zoomable="yes"}

Copie la dirección URL y escríbala en un archivo del equipo para obtener el token SAS a largo plazo con permisos de lectura y escritura.

![Almacenamiento de Azure](./images/az103.png){zoomable="yes"}

La dirección URL debe tener este aspecto:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Puede derivar un par de valores de la dirección URL anterior:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variables en Postman

Como puede ver en la sección anterior, hay algunas variables comunes en el token de lectura y en el token de escritura.

A continuación, debe crear variables en Postman que almacenen los distintos elementos de los tokens SAS anteriores. Hay algunos valores que son los mismos en ambas direcciones URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Para futuras interacciones de API, lo principal que cambia es el nombre del recurso, mientras que las variables anteriores siguen siendo las mismas. En ese caso, tiene sentido crear variables en Postman para que no necesite especificarlas manualmente cada vez.

En Postman, seleccione **Entornos**, abra **Todas las variables** y seleccione **Entorno**.

![Almacenamiento de Azure](./images/az104.png){zoomable="yes"}

Cree estas 4 variables en la tabla que se muestra y, para las columnas **Valor inicial** y **Valor actual**, introduzca sus valores personales específicos.

- `AZURE_STORAGE_URL`: su dirección URL
- `AZURE_STORAGE_CONTAINER`: su nombre de contenedor
- `AZURE_STORAGE_SAS_READ`: su token de lectura SAS
- `AZURE_STORAGE_SAS_WRITE`: su token de escritura SAS

Seleccione **Guardar**.

![Almacenamiento de Azure](./images/az105.png){zoomable="yes"}

### Variables en PostBuster

Como puede ver en la sección anterior, hay algunas variables comunes en el token de lectura y en el token de escritura.

A continuación, debe crear variables en PostBuster que almacenen los distintos elementos de los tokens SAS anteriores. Hay algunos valores que son los mismos en ambas direcciones URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Abra PostBuster. Seleccione **Entorno base** y haga clic en el icono **editar** para abrir el Entorno base.

![Almacenamiento de Azure](./images/pbbe1.png)

A continuación, verá 4 variables vacías. Introduzca los detalles de su cuenta de almacenamiento de Azure aquí.

![Almacenamiento de Azure](./images/pbbe2.png)

El archivo de entorno base debería tener un aspecto similar al siguiente. Haga clic en **Cerrar**.

![Almacenamiento de Azure](./images/pbbe3.png)

### Pruebe la configuración

En uno de los ejercicios anteriores, **Body** de su solicitud **Firefly - T2I (styleref) V3** tenía este aspecto:

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Almacenamiento de Azure](./images/az24.png){zoomable="yes"}

Cambie la dirección URL a:

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

Seleccione **Enviar** para probar los cambios que realizó.

![Almacenamiento de Azure](./images/az106.png){zoomable="yes"}

Si las variables se configuraron correctamente, se devuelve una URL de imagen.

![Almacenamiento de Azure](./images/az107.png){zoomable="yes"}

Abra la dirección URL de la imagen para comprobar la imagen.

![Almacenamiento de Azure](./images/az108.jpg)

## Pasos siguientes

Vaya a [Trabajar con las API de Photoshop](./ex3.md){target="_blank"}

Volver a [Información general de Adobe Firefly Services](./firefly-services.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}