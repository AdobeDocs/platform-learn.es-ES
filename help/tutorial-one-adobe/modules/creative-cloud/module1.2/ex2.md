---
title: Introducción a los servicios de Firefly
description: Introducción a los servicios de Firefly
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: a0c16a47372d322a7931578adca30a246b537183
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---

# 1.2.2 Uso de las API de Adobe en Workfront Fusion

## 1.2.2.1 Usar la API Texto a imagen del Firefly con Workfront Fusion

Pase el ratón sobre el segundo nodo **Set multiple variables** y haga clic en **+** para agregar otro módulo.

![WF Fusion](./images/wffusion48.png)

Busque **http** y luego seleccione **HTTP**.

![WF Fusion](./images/wffusion49.png)

Seleccione **Realizar una solicitud**.

![WF Fusion](./images/wffusion50.png)

Seleccione estas variables:

- **URL**: `https://firefly-api.adobe.io/v3/images/generate`
- **Método**: `POST`

Haga clic en **Agregar un encabezado**.

![WF Fusion](./images/wffusion51.png)

Debe introducir los siguientes encabezados:

| Clave | Valor |
|:-------------:| :---------------:| 
| `x-api-key` | su variable almacenada para `CONST_client_id` |
| `Authorization` | `Bearer ` + su variable almacenada para `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

Escriba los detalles de `x-api-key`. Haga clic en **Agregar**.

![WF Fusion](./images/wffusion52.png)

Haga clic en **Agregar un encabezado**.

![WF Fusion](./images/wffusion53.png)

Escriba los detalles de `Authorization`. Haga clic en **Agregar**.

![WF Fusion](./images/wffusion54.png)

Haga clic en **Agregar un encabezado**. Escriba los detalles de `Content-Type`. Haga clic en **Agregar**.

![WF Fusion](./images/wffusion541.png)

Haga clic en **Agregar un encabezado**. Escriba los detalles de `Accept`. Haga clic en **Agregar**.

![WF Fusion](./images/wffusion542.png)

Establezca **Body type** en **Raw**. Para **Content type**, seleccione **JSON (application/json)**.

![WF Fusion](./images/wffusion55.png)

Pegue esta carga en el campo **Solicitar contenido**.

```json
{
  "numVariations": 1,
  "size": {
    "width": 2048,
    "height": 2048
  },
  "prompt": "Horses in a field",
  "promptBiasingLocaleCode": "en-US"
}
```

Marque la casilla de verificación de **Analizar respuesta**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion56.png)

Haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffusion57.png)

Una vez ejecutado el escenario, debería ver esto.

![WF Fusion](./images/wffusion58.png)

¿Desea hacer clic en **?Icono** en el cuarto nodo, HTTP, para ver la respuesta. Debería ver un archivo de imagen en la respuesta.

![WF Fusion](./images/wffusion59.png)

Copie la dirección URL de la imagen y ábrala en una ventana del explorador. Entonces debería ver algo así:

![WF Fusion](./images/wffusion60.png)

Haga clic con el botón derecho en el objeto **HTTP** y cambie su nombre a **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

Haga clic en **Guardar** para guardar los cambios.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 Usar la API de Photoshop con Workfront Fusion

Haga clic en el icono **wrench** entre los nodos **Set Bearer Token** y **Firefly T2I**. Seleccione **Agregar un enrutador**.

![WF Fusion](./images/wffusion63.png)

Haga clic con el botón derecho en el objeto **Firefly T2I** y seleccione **Clonar**.

![WF Fusion](./images/wffusion64.png)

Arrastre y suelte el objeto clonado cerca del objeto **Router**, y se conectará automáticamente al **Router**. Entonces deberías tener esto.

![WF Fusion](./images/wffusion65.png)

Ahora tiene una copia idéntica basada en la solicitud HTTP **Firefly T2I**. Algunas de las configuraciones de la solicitud HTTP **Firefly T2I** son similares a las que necesita para interactuar con la **API de Photoshop**, que ahorra tiempo. Ahora solo necesita cambiar las variables que no son las mismas, como la dirección URL de solicitud y la carga útil.

Cambie **URL** a `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

Reemplazar **Solicitar contenido** por la siguiente carga útil:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button",
        "text": {
          "content": "Click here"
        }
      },
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Buy this stuff"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

![WF Fusion](./images/wffusion67.png)

Para que este **contenido de solicitud** funcione correctamente, faltan algunas variables:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Vuelva al primer nodo, haga clic en **Inicializar constantes** y, a continuación, seleccione **Agregar elemento** para cada una de estas variables.

![WF Fusion](./images/wffusion69.png)

| Clave | Valor de ejemplo |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Para encontrar las variables, vuelva a Postman y abra las **Variables de entorno**.

![Almacenamiento de Azure](./../module1.1/images/az105.png)

Copie estos valores en Workfront Fusion y añada un nuevo elemento para cada una de estas 4 variables.

Entonces deberías tener esto. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion68.png)

A continuación, vuelva a la solicitud HTTP clonada para actualizar **Solicitar contenido**. Observará estas variables negras en **Solicitar contenido**, que son las variables que copió desde Postman. Ahora debe cambiarlas por las variables que acaba de definir en Workfront Fusion. Reemplace cada variable una por una eliminando el texto en negro y reemplazándolo por la variable correcta.

![WF Fusion](./images/wffusion70.png)

Hay 3 cambios que hacer en la sección **input**.

![WF Fusion](./images/wffusion71.png)

También hay 3 cambios que hacer en la sección **output**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion72.png)

Haga clic con el botón derecho en el nodo clonado y seleccione **Rename**. Cambie el nombre a **Photoshop Change Text**.

![WF Fusion](./images/wffusion73.png)

Entonces deberías tener esto.

![WF Fusion](./images/wffusion74.png)

Paso siguiente: [1.2.3 ...](./ex3.md)

[Volver al módulo 1.2](./automation.md)

[Volver a todos los módulos](./../../../overview.md)
