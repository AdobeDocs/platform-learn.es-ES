---
title: Introducción a los servicios de Firefly
description: Introducción a los servicios de Firefly
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: c5d015fee3650d9c5a154f0b1374d27b20d2ea42
workflow-type: tm+mt
source-wordcount: '1759'
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

Haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffusion75.png)

Haga clic en el icono **search** del nodo **Photoshop Change Text** para ver la respuesta. Debe tener una respuesta similar a esta, con un vínculo a un archivo de estado.

![WF Fusion](./images/wffusion76.png)

Antes de continuar con las interacciones de la API de Photoshop, deshabilitemos la ruta al nodo **Firefly T2I** para no enviar llamadas de API innecesarias a ese extremo de API. Haga clic en el icono **llave inglesa** y, a continuación, seleccione **Deshabilitar ruta**.

![WF Fusion](./images/wffusion77.png)

Entonces deberías tener esto.

![WF Fusion](./images/wffusion78.png)

A continuación, agregue otro nodo **Set multiple variables**.

![WF Fusion](./images/wffusion79.png)

Colóquelo después del nodo **Photoshop Change Text**.

![WF Fusion](./images/wffusion80.png)

Haga clic en el nodo **Set multiple variables** y seleccione **Add item**. Seleccione el valor de la variable de la respuesta de la solicitud anterior.

| Nombre de variable | Valor variable |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

Haga clic en **Agregar**.

![WF Fusion](./images/wffusion81.png)

Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion82.png)

Haga clic con el botón derecho en el nodo **Photoshop Change Text** y seleccione **Clone**.

![WF Fusion](./images/wffusion83.png)

Arrastre la solicitud HTTP clonada después del nodo **Set multiple variables** que acaba de crear.

![WF Fusion](./images/wffusion83.png)

Haga clic con el botón derecho en la solicitud HTTP clonada, seleccione **Rename** y cambie el nombre a **Photoshop Check Status**.

![WF Fusion](./images/wffusion84.png)

Haga clic en para abrir la solicitud HTTP. Cambie la dirección URL de modo que haga referencia a la variable que creó en el paso anterior y establezca el **Método** en **GET**.

![WF Fusion](./images/wffusion85.png)

Elimine **Body** seleccionando la opción vacía.

![WF Fusion](./images/wffusion86.png)

Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion87.png)

Haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffusion88.png)

Entonces debería obtener una respuesta que contenga el campo **status**, con el estado establecido en **running**. Photoshop tarda un par de segundos en completar el proceso.

![WF Fusion](./images/wffusion89.png)

Ahora que sabe que la respuesta necesita un poco más de tiempo para completarse, puede ser una buena idea agregar un temporizador delante de esta solicitud HTTP para que no se ejecute de inmediato.

Haga clic en el nodo **Herramientas** y, a continuación, seleccione **Suspensión**.

![WF Fusion](./images/wffusion90.png)

Coloque el nodo **Sleep** entre **Establecer varias variables** y **Comprobar el estado de Photoshop**. Establezca **Delay** en **5** segundos. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion91.png)

Entonces, tendrás esto. El desafío con la siguiente configuración es que 5 segundos de espera pueden ser suficientes, pero tal vez no sean suficientes. En realidad, sería mejor tener una solución más inteligente como un bucle do...while que compruebe el estado cada 5 segundos hasta que el estado sea igual a **succeeded**. Ahora implementará una táctica de este tipo en los pasos siguientes.

![WF Fusion](./images/wffusion92.png)

Haga clic en el icono **llave inglesa** que hay entre **Establecer varias variables** y **Suspender**. Seleccione **Agregar módulo**.

![WF Fusion](./images/wffusion93.png)

Busque `flow` y luego seleccione **Control de flujo**.

![WF Fusion](./images/wffusion94.png)

Seleccione **Repetidor**.

![WF Fusion](./images/wffusion95.png)

Establezca **Repeats** en **20**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion96.png)

A continuación, haga clic en **+** en **Photoshop Comprobar estado** para agregar otro módulo.

![WF Fusion](./images/wffusion97.png)

Busque **flow** y seleccione **Flow Control**.

![WF Fusion](./images/wffusion98.png)

Seleccione **Agregador de matrices**.

![WF Fusion](./images/wffusion99.png)

Definir **Módulo Source** en **Repetidor**. Seleccionar **Aceptar**.

![WF Fusion](./images/wffusion100.png)

Entonces debería tener esto:

![WF Fusion](./images/wffusion101.png)

Haga clic en el icono **llave inglesa** y seleccione **Agregar un módulo**.

![WF Fusion](./images/wffusion102.png)

Busque **herramientas** y seleccione **Herramientas**.

![WF Fusion](./images/wffusion103.png)

Seleccione **Obtener múltiples variables**.

![WF Fusion](./images/wffusion104.png)

Haga clic en **+ Agregar elemento** y establezca **Nombre de variable** en `done`.

![WF Fusion](./images/wffusion105.png)

Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion106.png)

Haga clic en el nodo **Set multiple variables** que configuró anteriormente. Para inicializar la variable **done**, debe establecerla en `false` aquí. Haga clic en **+ Agregar elemento**.

![WF Fusion](./images/wffusion107.png)

Para **nombre de variable**, use `done`. Para establecer el estado, se necesita un valor booleano. Para encontrar el valor booleano, haga clic en el icono **engranaje** y, a continuación, seleccione `false`. Haga clic en **Agregar**.

![WF Fusion](./images/wffusion108.png)

Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion109.png)

A continuación, haga clic en el icono **wrench** después del nodo **Get multiple variables** que configuró.

![WF Fusion](./images/wffusion110.png)

Seleccione **Configurar un filtro**. Ahora necesita comprobar el valor de la variable **done**. Si ese valor se establece en **false**, se debe ejecutar la siguiente parte del bucle. Si el valor se establece en **true**, significa que el proceso ya ha finalizado correctamente, por lo que no es necesario continuar con la siguiente parte del bucle.

![WF Fusion](./images/wffusion111.png)

Para la etiqueta, use **¿Ya terminamos?**. Establezca la **condición** con la variable ya existente **hecho**, el operador debe establecerse en **Igual a** y el valor debe ser la variable booleana `false`. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion112.png)

A continuación, deje espacio entre los nodos **Photoshop Comprobar estado** y **Agregador de matrices**. A continuación, haga clic en el icono **llave inglesa** y seleccione **Agregar un enrutador**. Esto se debe a que, después de comprobar el estado del archivo Photoshop, debe haber dos rutas. Si el estado es `succeeded`, la variable de **done** debe establecerse en `true`. Si el estado no es igual a `succeeded`, el bucle debe continuar. El enrutador hará posible comprobar y configurar esto.

![WF Fusion](./images/wffusion113.png)

Después de agregar el enrutador, haz clic en el icono **llave inglesa** y selecciona **Configurar un filtro**.

![WF Fusion](./images/wffusion114.png)

Para la etiqueta, use **Hemos terminado**. Establezca la **condición** con la respuesta del nodo **Photoshop Comprobar estado** eligiendo el campo de respuesta **data.output[].status**, el operador debe establecerse en **Igual a** y el valor debe ser `succeeded`. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion115.png)

A continuación, haga clic en el nodo vacío con el signo de interrogación y busque **herramientas**. A continuación, seleccione **Herramientas**.

![WF Fusion](./images/wffusion116.png)

Seleccione **Establecer múltiples variables**.

![WF Fusion](./images/wffusion117.png)

Cuando se utiliza esta rama del enrutador, significa que el estado de creación del archivo Photoshop se ha completado correctamente. Esto significa que el bucle do...while ya no necesita continuar comprobando el estado en Photoshop, por lo que debe establecer la variable `done` en `true`.

Para **nombre de variable**, use `done`. Para el **valor de variable**, debe usar el valor booleano `true`. Haga clic en el icono **engranaje** y luego seleccione `true`. Haga clic en **Agregar**.

![WF Fusion](./images/wffusion118.png)

Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion119.png)

A continuación, haga clic con el botón derecho en el nodo **Set multiple variables** que acaba de crear y seleccione **Clone**.

![WF Fusion](./images/wffusion120.png)

Arrastre el nodo clonado para que se conecte con **Array aggregator**. A continuación, haga clic con el botón secundario en el nodo, seleccione **Rename** y cambie el nombre a `Placeholder End`.

![WF Fusion](./images/wffusion122.png)

Elimine la variable existente y haga clic en **+ Agregar elemento**. Para **Variable name**, use `placeholder`, para **Variable value**, use `end`. Haga clic en **Agregar** y, a continuación, haga clic en **Aceptar**.

![WF Fusion](./images/wffusion123.png)

Haga clic en **Guardar** para guardar el escenario. A continuación, haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffusion124.png)

El escenario se ejecutará y finalizará correctamente. Verá que el bucle do...while que configuró funcionó correctamente. En la siguiente ejecución, puede ver que **Repeater** se ejecutó 20 veces según la burbuja del nodo **Tools > Get multiple variables**. Después de ese nodo, configuró un filtro que comprobó el estado y solo si el estado no era igual a **correcto**, se ejecutaron los siguientes nodos. En esta ejecución, la parte posterior al filtro solo se ejecutó una vez, porque el estado ya era **correcto** en la primera ejecución.

![WF Fusion](./images/wffusion125.png)

Puede comprobar el estado de creación del nuevo archivo Photoshop si hace clic en la burbuja de la solicitud HTTP **Photoshop Check Status** y explora el campo **estado**.

![WF Fusion](./images/wffusion126.png)

Ya ha configurado la versión básica de un escenario repetible que automatiza una serie de pasos. En el siguiente ejercicio, iterará agregando complejidad a esto.

Siguiente paso: [1.2.3 Automatización de procesos con Workfront Fusion](./ex3.md)

[Volver al módulo 1.2](./automation.md)

[Volver a todos los módulos](./../../../overview.md)
