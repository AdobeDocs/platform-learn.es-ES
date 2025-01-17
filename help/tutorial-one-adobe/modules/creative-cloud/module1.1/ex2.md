---
title: Optimizar el proceso de Firefly con Microsoft Azure y las direcciones URL prefirmadas
description: Optimizar el proceso de Firefly con Microsoft Azure y las direcciones URL prefirmadas
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: f1f70a0e4ea3f59b5b121275e7db633caf953df9
workflow-type: tm+mt
source-wordcount: '1527'
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

>[!NOTE]
>
>Si no se muestra tu cuenta, haz clic en el icono **engranaje** junto a tu dirección de correo electrónico y selecciona **Anular filtro**.

![Almacenamiento de Azure](./images/az16.png)

Encontrará su cuenta de almacenamiento en **Cuentas de almacenamiento**.

![Almacenamiento de Azure](./images/az17.png)

Abra **Contenedores de blob** y haga clic en el contenedor que creó en el ejercicio anterior.

![Almacenamiento de Azure](./images/az18.png)

## 1.1.2.4 Carga manual de archivos y uso de un archivo de imagen como referencia de estilo

Ahora debe cargar un archivo de imagen de su elección en el contenedor. Puedes usar cualquier archivo de imagen que desees o [este archivo](./images/gradient.jpg) descargándolo en tu equipo.

![Almacenamiento de Azure](./images/gradient.jpg)

Coloque el archivo de imagen en el contenedor en el Explorador de almacenamiento de Azure.

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

Reemplace la URL del marcador de posición por la URL prefirmada para el archivo de imagen que copió del Explorador de almacenamiento de Azure. Entonces, tendrás esto. Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/az24.png)

Recibirá una respuesta de Servicios de Firefly de nuevo, con una imagen nueva. Abra el archivo de imagen en el explorador.

![Almacenamiento de Azure](./images/az25.png)

Verá otra imagen con `horses in a field`, pero esta vez el estilo será similar al archivo de imagen que proporcionó como referencia de estilo.

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

Ahora tendrá que seleccionar un archivo del equipo local. Puede usar un nuevo archivo de imagen que elija, o bien otro archivo de imagen que encuentre [aquí](./images/gradient2-p.jpg).

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

| Clave | Valor |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Almacenamiento de Azure](./images/az35.png)

Vaya a **Autorización** y establezca **Tipo de autenticación** en **Sin autenticación**. Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/az36.png)

Verá esta respuesta vacía en Postman, lo que significa que la carga del archivo se realizó correctamente.

![Almacenamiento de Azure](./images/az37.png)

Si vuelve al Explorador de almacenamiento de Azure y actualiza el contenido de la carpeta, ahora encontrará allí el archivo recién cargado.

![Almacenamiento de Azure](./images/az38.png)

## 1.1.2.6 Uso de archivos programáticos

Para poder usar archivos leídos mediante programación desde cuentas de almacenamiento de Azure a largo plazo, deberá crear un nuevo token de **firma de acceso compartido (SAS)**, con permisos que le permitan leer un archivo. Técnicamente, puede utilizar el token SAS que creó en el ejercicio anterior, pero se recomienda tener un token independiente con solo permisos de **Read** y un token independiente con solo permisos de **Write**.

### Token SAS de lectura a largo plazo

Para ello, vuelva al Explorador de almacenamiento de Azure. Haga clic con el botón secundario en el contenedor y, a continuación, haga clic en **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az27.png)

En **Permisos**, se requieren los siguientes permisos:

- **Leer**
- **Lista**

Establezca el **Tiempo de caducidad** en 1 año a partir de ahora.

Haga clic en **Crear**.

![Almacenamiento de Azure](./images/az100.png)

A continuación, obtendrá el token SAS a largo plazo con permisos de lectura. Copie la dirección URL y escríbala en un archivo del equipo.

![Almacenamiento de Azure](./images/az101.png)

La dirección URL tendrá este aspecto:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

Puede derivar un par de valores de la dirección URL anterior:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Token SAS de escritura a largo plazo

Para ello, vuelva al Explorador de almacenamiento de Azure. Haga clic con el botón secundario en el contenedor y, a continuación, haga clic en **Obtener firma de acceso compartido**.

![Almacenamiento de Azure](./images/az27.png)

En **Permisos**, se requieren los siguientes permisos:

- **Agregar**
- **Create**
- **Write**

Establezca el **Tiempo de caducidad** en 1 año a partir de ahora.

Haga clic en **Crear**.

![Almacenamiento de Azure](./images/az102.png)

A continuación, obtendrá el token SAS a largo plazo con permisos de lectura. Copie la dirección URL y escríbala en un archivo del equipo.

![Almacenamiento de Azure](./images/az103.png)

La dirección URL tendrá este aspecto:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Una vez más, puede derivar un par de valores de la URL anterior:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variables en Postman

Como puede ver en la sección anterior, hay algunas variables comunes en el token de lectura y en el token de escritura.

Ahora debe crear variables en Postman que almacenarán los distintos elementos de los tokens SAS anteriores.
Hay algunos valores que son los mismos en ambas direcciones URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Para futuras interacciones de API, lo principal que cambiará es el nombre del recurso, mientras que las variables anteriores permanecerán igual. En ese caso, tiene sentido crear variables en Postman para que no necesite especificarlas manualmente cada vez.

Para ello, abra Postman. Haga clic en el icono **Entornos**, abra el menú **Todas las variables** y haga clic en **Entorno**.

![Almacenamiento de Azure](./images/az104.png)

Entonces verá esto. Cree estas 4 variables en la tabla que se muestra y, para las columnas **Valor inicial** y **Valor actual**, introduzca sus valores personales específicos.

- `AZURE_STORAGE_URL`: su dirección URL
- `AZURE_STORAGE_CONTAINER`: su nombre de contenedor
- `AZURE_STORAGE_SAS_READ`: su token de lectura SAS
- `AZURE_STORAGE_SAS_WRITE`: su token de escritura SAS

Haga clic en **Guardar**.

![Almacenamiento de Azure](./images/az105.png)

En uno de los ejercicios anteriores, el **Cuerpo** de su solicitud **Firefly - T2I (styleref) V3** tenía este aspecto:

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Almacenamiento de Azure](./images/az24.png)

Ahora puede cambiar la dirección URL a:

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

Haga clic en **Enviar** para probar los cambios que realizó.

![Almacenamiento de Azure](./images/az106.png)

Si las variables se configuraron correctamente, verá que se devuelve una dirección URL de imagen.

![Almacenamiento de Azure](./images/az107.png)

Abra la dirección URL de la imagen para comprobar la imagen.

![Almacenamiento de Azure](./images/az108.jpg)

Siguiente paso: [1.1.3 Adobe Firefly y Adobe Photoshop](./ex3.md)

[Volver al módulo 1.1](./firefly-services.md)

[Volver a todos los módulos](./../../../overview.md)
