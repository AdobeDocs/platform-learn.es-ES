---
title: Uso de las API de Photoshop
description: Aprenda a trabajar con las API de Photoshop y los servicios de Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: d33df99e9c75e7d5feef503b68174b93860ac245
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# 1.1.3 Uso de las API de Photoshop

Aprenda a trabajar con las API de Photoshop y los servicios de Firefly.

## 1.1.3.1 Actualizar la integración de Adobe I/O

1. Vaya a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nueva integración de Adobe I/O](./images/iohome.png){zoomable="yes"}

1. Vaya a **Proyectos** y seleccione el proyecto que creó en el ejercicio anterior, que se llama `--aepUserLdap-- Firefly`.

![Almacenamiento de Azure](./images/ps1.png){zoomable="yes"}

1. Seleccione **+ Agregar al proyecto** y luego seleccione **API**.

![Almacenamiento de Azure](./images/ps2.png){zoomable="yes"}

1. Seleccione **Creative Cloud** y elija **Photoshop - Servicios de Firefly**. Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/ps3.png){zoomable="yes"}

1. Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/ps4.png){zoomable="yes"}

A continuación, debe seleccionar un perfil de producto que defina qué permisos están disponibles para esta integración.

1. Seleccione **Configuración predeterminada de Firefly Services** y **Configuración predeterminada de Creative Cloud Automation Services**.

1. Seleccione **Guardar la API configurada**.

![Almacenamiento de Azure](./images/ps5.png){zoomable="yes"}

El proyecto de Adobe I/O ahora se actualiza para que funcione con las API de Photoshop y Firefly Services.

![Almacenamiento de Azure](./images/ps6.png){zoomable="yes"}

## 1.1.3.2 Interactuar mediante programación con un archivo de PSD

>[!IMPORTANT]
>
>Si eres empleado de Adobe, sigue las instrucciones aquí para usar [PostBuster](./../../../postbuster.md).

1. Descargue [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} en su escritorio.

1. Abra **citisignal-fiber.psd** en Photoshop.

![Almacenamiento de Azure](./images/ps7.png){zoomable="yes"}

En el panel **Capas**, el diseñador del archivo ha asignado un nombre único a cada capa. Puede ver la información de la capa abriendo el archivo PSD en Photoshop, pero también puede hacerlo mediante programación.

Enviemos su primera solicitud de API a las API de Photoshop.

1. En Postman, antes de enviar solicitudes de API a Photoshop, debe autenticarse en Adobe I/O. Abra la solicitud anterior llamada **POST - Obtener token de acceso**.

1. Vaya a **Params** y compruebe que el parámetro **Scope** esté configurado correctamente. El **valor** de **ámbito** debe tener este aspecto:

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

1. Select **Send**.

![Azure Storage](./images/ps8.png){zoomable="yes"}

Now you have a valid access token to interact with Photoshop APIs.

![Almacenamiento de Azure](./images/ps9.png){zoomable="yes"}

### API de Photoshop: Hello World

Next, let&#39;s say hello to Photoshop APIs to test if all permissions and access is set correctly.

1. In the collection **Photoshop**, open the request  **Photoshop Hello (Test Auth.)**. Select **Send**.

![Azure Storage](./images/ps10.png){zoomable="yes"}

You should receive the response **Welcome to the Photoshop API!**.

![Azure Storage](./images/ps11.png){zoomable="yes"}

A continuación, para interactuar mediante programación con el archivo PSD **citisignal-fiber.psd**, debe cargarlo en su cuenta de almacenamiento. Puede hacerlo manualmente (arrastrándolo y soltándolo en el contenedor mediante el Explorador de almacenamiento de Azure), pero esta vez debe hacerlo a través de la API.

### Cargar PSD en Azure

1. En Postman, abra la solicitud **Cargar PSD a la cuenta de almacenamiento de Azure**. En el ejercicio anterior configuró estas variables de entorno en Postman, que ahora utilizará:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Como puede ver en la solicitud **Cargar PSD a la cuenta de almacenamiento de Azure**, la dirección URL está configurada para utilizar estas variables.

![Almacenamiento de Azure](./images/ps12.png){zoomable="yes"}

1. In **Body**, select the file **citisignal-fiber.psd**.

![Azure Storage](./images/ps13.png){zoomable="yes"}

1. Your screen should look like this. Select **Send**.

![Azure Storage](./images/ps14.png){zoomable="yes"}

You should get this empty response back from Azure, which means that your file is stored in your container in your Azure Storage account.

![Azure Storage](./images/ps15.png){zoomable="yes"}

If you use Azure Storage Explorer to look at your file, be sure to refresh your folder.

![Azure Storage](./images/ps16.png){zoomable="yes"}

### Photoshop API - Get manifest

Next, you need to get the manifest file of your PSD file.

1. En Postman, abra la solicitud **Photoshop - Obtener manifiesto de PSD**. Ir a **Cuerpo**.

El cuerpo debería tener un aspecto similar al siguiente:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "thumbnails": {
      "type": "image/jpeg"
    }
  }
}
```

1. Seleccione **Enviar**.

En la respuesta, ahora verá un vínculo. Como las operaciones en Photoshop a veces pueden tardar algún tiempo en completarse, Photoshop proporciona un archivo de estado como respuesta a la mayoría de las solicitudes entrantes. Para comprender lo que sucede con su solicitud, debe leer el archivo de estado.

![Almacenamiento de Azure](./images/ps17.png){zoomable="yes"}

1. Para leer el archivo de estado, abra la solicitud **Photoshop - Obtener estado de PS**. Puede ver que esta solicitud usa una variable como dirección URL, que es una variable establecida por la solicitud anterior que envió, **Photoshop - Obtener manifiesto de PSD**. Las variables se establecen en **Scripts** de cada solicitud. Seleccione **Enviar**.

![Almacenamiento de Azure](./images/ps18.png){zoomable="yes"}

La pantalla debería tener un aspecto similar al siguiente. Actualmente, el estado está establecido en **pendiente**, lo que significa que el proceso aún no ha finalizado.

![Almacenamiento de Azure](./images/ps19.png){zoomable="yes"}

1. Seleccione enviar un par de veces más en **Photoshop - Obtener estado de PS**, hasta que el estado cambie a **correcto**. Esto puede tardar un par de minutos.

Cuando la respuesta esté disponible, podrá ver que el archivo json contiene información sobre todas las capas del archivo PSD. Esta información es útil, ya que se pueden identificar cosas como el nombre o el ID de la capa.

![Almacenamiento de Azure](./images/ps20.png){zoomable="yes"}

Por ejemplo, busque el texto `2048x2048-cta`. La pantalla debería tener un aspecto similar al siguiente:

![Almacenamiento de Azure](./images/ps21.png){zoomable="yes"}

### API de Photoshop: Cambiar texto

A continuación, debe cambiar el texto de la llamada a la acción mediante las API.

1. En Postman, abra la solicitud **Photoshop - Cambiar texto** y vaya a **Cuerpo**.

La pantalla debería tener un aspecto similar al siguiente:

- primero, se especifica un archivo de entrada: `citisignal-fiber.psd`
- segundo, se especifica la capa que se va a cambiar, con el texto al que se va a cambiar
- tercero, se especifica un archivo de salida: `citisignal-fiber-changed-text.psd`

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Get Fiber now!"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

The output file has a different name, because you don&#39;t want to override the original input file.

1. Seleccione **Enviar**.

![Almacenamiento de Azure](./images/ps23.png){zoomable="yes"}

Al igual que antes, la respuesta contiene un vínculo que apunta al archivo de estado que realiza un seguimiento del progreso.

![Almacenamiento de Azure](./images/ps22.png){zoomable="yes"}

1. Para leer el archivo de estado, abre la solicitud **Photoshop - Obtener estado de PS** y selecciona **Enviar**. Si el estado no se establece en **correcto** inmediatamente, espere un par de segundos y, a continuación, seleccione **Enviar** de nuevo.

1. Select the URL to download the output file.

![Azure Storage](./images/ps24.png){zoomable="yes"}

1. Open **citisignal-fiber-changed-text.psd** after downloading the file to your computer. Debería ver que el marcador de posición de la llamada a la acción se ha reemplazado con el texto **Obtener fibra ahora!**.

![Almacenamiento de Azure](./images/ps25.png){zoomable="yes"}

También puede ver este archivo en el contenedor mediante el Explorador de almacenamiento de Azure.

![Azure Storage](./images/ps26.png){zoomable="yes"}

## Pasos siguientes

Ir a [API de modelos personalizados de Firefly](./ex4.md){target="_blank"}

Volver a [Información general sobre los servicios de Adobe Firefly](./firefly-services.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
