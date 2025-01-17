---
title: Uso de las API de Photoshop
description: Uso de las API de Photoshop
kt: 5342
doc-type: tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: 2fe7d2528132301f559f9d51faa9ad128f5d890f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# 1.1.3 Uso de las API de Photoshop

## 1.1.3.1 Actualizar la integración de Adobe I/O

Vaya a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nueva integración de Adobe I/O](./images/iohome.png)

Vaya a **Proyectos** y haga clic para abrir el proyecto que creó en el ejercicio anterior, que se llama `--aepUserLdap-- Firefly`.

![Almacenamiento de Azure](./images/ps1.png)

Haga clic en **+ Agregar al proyecto** y, a continuación, haga clic en **API**.

![Almacenamiento de Azure](./images/ps2.png)

Seleccione **Creative Cloud** y haga clic en **Photoshop - Servicios de Firefly**. Haga clic en **Next**.

![Almacenamiento de Azure](./images/ps3.png)

Haga clic en **Next**.

![Almacenamiento de Azure](./images/ps4.png)

A continuación, debe seleccionar un perfil de producto que defina qué permisos están disponibles para esta integración.

Seleccione el perfil **Configuración predeterminada de servicios de Firefly** y **Configuración predeterminada de servicios de automatización de Creative Cloud**.

Haga clic en **Guardar API configurada**.

![Almacenamiento de Azure](./images/ps5.png)

El proyecto de Adobe I/O ahora se ha actualizado para que funcione con las API de Photoshop y servicios de Firefly.

![Almacenamiento de Azure](./images/ps6.png)

## 1.1.3.2 Interactuar mediante programación con un archivo de PSD

Descarga el archivo Ve a [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} a tu escritorio.

Abra el archivo **citisignal-fiber.psd** en Photoshop. Entonces deberías tener esto.

![Almacenamiento de Azure](./images/ps7.png)

En el panel **Capas**, verá que el diseñador del archivo ha asignado un nombre único a cada capa. Puede ver la información de la capa abriendo el archivo PSD en Photoshop, pero también puede hacerlo mediante programación.

Enviemos su primera solicitud de API a las API de Photoshop.

Vaya a Postman. Antes de enviar solicitudes de API a Photoshop, debe autenticarse en el Adobe I/O. Abra la solicitud que usó anteriormente con el nombre **POST - Obtener token de acceso**.

Vaya a **Params** y compruebe que el parámetro **Scope** esté configurado correctamente. El **valor** de **ámbito** debe tener este aspecto:

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

A continuación, haga clic en **Enviar**.

![Almacenamiento de Azure](./images/ps8.png)

Luego tiene un token de acceso válido para interactuar con las API de Photoshop.

![Almacenamiento de Azure](./images/ps9.png)

### API de Photoshop 1.1.3.2.1: Hello World

A continuación, saludemos a las API de Photoshop para comprobar si todos los permisos y accesos están correctamente configurados. En la colección **Photoshop**, abra la solicitud con el nombre **Photoshop Hello (Test Auth.)**. Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/ps10.png)

Debería recibir esta respuesta: **Bienvenido a la API de Photoshop!**.

![Almacenamiento de Azure](./images/ps11.png)

A continuación, para interactuar mediante programación con el archivo PSD **citisignal-fiber.psd**, debe cargarlo en su cuenta de almacenamiento. Puede hacerlo manualmente, arrastrándolo y soltándolo en el contenedor mediante el Explorador de almacenamiento de Azure, pero esta vez debe hacerlo a través de la API.

### 1.1.3.2.2 PSD de carga en Azure

En Postman, abra la solicitud **Cargar PSD a la cuenta de almacenamiento de Azure**. En el ejercicio anterior configuró estas variables de entorno en Postman, que ahora utilizará:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Como puede ver en la solicitud **Cargar PSD a la cuenta de almacenamiento de Azure**, la dirección URL está configurada para utilizar estas variables.

![Almacenamiento de Azure](./images/ps12.png)

En **Cuerpo**, ahora debería agregar y seleccionar el archivo **citisignal-fiber.psd**.

![Almacenamiento de Azure](./images/ps13.png)

Entonces deberías tener esto. Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/ps14.png)

A continuación, debería recuperar esta respuesta vacía de Azure, lo que significa que el archivo se almacena en el contenedor de su cuenta de almacenamiento de Azure.

![Almacenamiento de Azure](./images/ps15.png)

Si usa el Explorador de almacenamiento de Azure para echar un vistazo, verá el archivo después de actualizar la carpeta.

![Almacenamiento de Azure](./images/ps16.png)

### API de Photoshop 1.1.3.2.3: Obtener manifiesto

A continuación, debe obtener el archivo de manifiesto del archivo de PSD. En Postman, abra la solicitud **Photoshop - Obtener manifiesto del PSD**. Ir a **Cuerpo**.

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

Haga clic en **Enviar**.

En la respuesta, ahora verá un vínculo. Como las operaciones en Photoshop a veces pueden tardar algún tiempo en completarse, Photoshop proporciona un archivo de estado como respuesta a la mayoría de las solicitudes entrantes. Para comprender lo que sucede con su solicitud, debe leer el archivo de estado.

![Almacenamiento de Azure](./images/ps17.png)

Para leer el archivo de estado, abra la solicitud **Photoshop - Obtener estado de PS**. A continuación, verá que esta solicitud está usando una variable como dirección URL, que es una variable establecida por la solicitud anterior que envió, **Photoshop - Obtener manifiesto del PSD**. Las variables se establecen en **Scripts** de cada solicitud.

Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/ps18.png)

Entonces debería ver esto. Actualmente, el estado está establecido en **pendiente**, lo que significa que el proceso aún no ha finalizado.

![Almacenamiento de Azure](./images/ps19.png)

Puede hacer clic en enviar un par de veces más en la solicitud **Photoshop - Obtener estado de PS**, hasta que el estado cambie a **correcto**. Esto puede tardar un par de minutos.

Cuando la respuesta esté disponible, aparecerá un archivo json que contiene información sobre todas las capas del archivo PSD. Esta información es útil, ya que elementos como el nombre o el ID de la capa se pueden ver aquí.

![Almacenamiento de Azure](./images/ps20.png)

Por ejemplo, busque el texto `2048x2048-cta`. Entonces debería ver esto.

![Almacenamiento de Azure](./images/ps21.png)

### API de Photoshop 1.1.3.2.4: Cambiar texto

A continuación, debe cambiar el texto de la llamada a la acción mediante las API. En Postman, abra la solicitud **Photoshop - Cambiar texto** y vaya a **Cuerpo**.

Entonces debería ver esto. Se puede ver lo siguiente:

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

El nombre del archivo de salida es distinto, ya que no se desea anular el archivo de entrada original.

Haga clic en **Enviar**.

![Almacenamiento de Azure](./images/ps23.png)

Al igual que antes, la respuesta contiene un vínculo que apunta al archivo de estado que realiza un seguimiento del progreso.

![Almacenamiento de Azure](./images/ps22.png)

Para leer el archivo de estado, vuelve a abrir la solicitud **Photoshop - Obtener estado de PS** y haz clic en **Enviar**. Si el estado no se establece en **correcto** inmediatamente, espere un par de segundos y vuelva a hacer clic en **Enviar**.

Una vez que el estado se establezca en **correcto**, debería ver esto. En la ruta de acceso `outputs[0]._links.renditions[0].href`, debería ver la dirección URL del archivo de salida que creó Photoshop y que contiene el texto modificado.

Haga clic en la dirección URL para descargar el archivo de salida.

![Almacenamiento de Azure](./images/ps24.png)

El archivo **citisignal-fiber-changed-text.psd** se descargará en el equipo, después de lo cual podrá abrirlo. Entonces debería ver que el marcador de posición de la llamada a la acción se ha reemplazado con el texto **Obtener fibra ahora!**.

![Almacenamiento de Azure](./images/ps25.png)

Por último, también verá ese archivo en el contenedor mediante el Explorador de almacenamiento de Azure.

![Almacenamiento de Azure](./images/ps26.png)

Ahora ha completado este ejercicio.

Siguiente Paso: [1.1.4 Modelos Personalizados De Firefly](./ex4.md){target="_blank"}

[Volver al módulo 1.1](./firefly-services.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
