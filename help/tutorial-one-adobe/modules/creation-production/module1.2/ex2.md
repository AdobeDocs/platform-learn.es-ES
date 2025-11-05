---
title: Automatización con conectores
description: Automatización con conectores
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 0b20ba91-28d4-4f4d-8abe-074f802c389e
source-git-commit: c9807ef0787f4390d12bc7285cfe71260aa3eabf
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 1%

---

# 1.2.4 Automatización mediante conectores

Ahora empezará a utilizar los conectores predeterminados en Workfront Fusion para Photoshop y conectará la solicitud de Firefly Text-2-Image y las solicitudes de Photoshop en un escenario.

## 1.2.4.1 variables de actualización

Antes de continuar con la configuración del conector, es necesario agregar las siguientes variables al módulo **Inicializar constantes**.

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Vuelva al primer nodo, seleccione **Inicializar constantes** y, a continuación, elija **Agregar elemento** para cada una de estas variables.

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

La pantalla debería tener un aspecto similar al siguiente. Seleccione **Aceptar**.

![WF Fusion](./images/wffusion68.png)

## 1.2.4.2 Activar su escenario mediante un gancho web

Hasta ahora, ha ejecutado el escenario manualmente para probarlo. Actualicemos ahora su escenario con un webhook, para que pueda activarse desde un entorno externo.

Seleccione **+**, busque **webhook** y luego seleccione **Webhooks**.

![WF Fusion](./images/wffusion216.png)

Seleccione **webhook personalizado**.

![WF Fusion](./images/wffusion217.png)

Arrastre el módulo **Gancho web personalizado** al principio del escenario. A continuación, selecciona el icono **clock** y arrástralo al módulo **Custom Webhook**.

![WF Fusion](./images/wffusion217a.png)

Entonces debería ver esto. A continuación, arrastre el punto rojo del primer módulo hacia el punto morado del segundo módulo.

![WF Fusion](./images/wffusion217b.png)

Entonces debería ver esto. Newt, haz clic en el módulo **Gancho web personalizado**.

![WF Fusion](./images/wffusion217c.png)

Haga clic en **Agregar**.

![WF Fusion](./images/wffusion218.png)

Establezca el **nombre del webhook** en `--aepUserLdap-- - Firefly + Photoshop Webhook`. Haga clic en **Guardar**.

![WF Fusion](./images/wffusion219.png)

La URL del gancho web ya está disponible. Haga clic en **Copiar dirección al portapapeles** para copiar la dirección URL.

![WF Fusion](./images/wffusion221.png)

Abra Postman y agregue una nueva carpeta a la colección **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Asigne un nombre a la carpeta `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

En la carpeta que acaba de crear, seleccione los 3 puntos **...** y seleccione **Agregar solicitud**.

![WF Fusion](./images/wffusion224.png)

Establece **Method type** en **POST** y pega la URL de tu webhook en la barra de direcciones.

![WF Fusion](./images/wffusion225.png)

Debe enviar un cuerpo personalizado para que los elementos de la variable se puedan proporcionar desde una fuente externa al escenario de Workfront Fusion.

Vaya a **Cuerpo** y seleccione **sin procesar**.

![WF Fusion](./images/wffusion226.png)

Pegue el texto siguiente en el cuerpo de la solicitud. Seleccione **Enviar**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

![WF Fusion](./images/wffusion229.png)

Cuando vuelva a Workfront Fusion, aparecerá un mensaje en el gancho web personalizado que dice: **Determinado correctamente**.

![WF Fusion](./images/wffusion227.png)

## 1.2.4.3 Conector De Adobe Firefly

Haga clic en el icono **+** para agregar un módulo nuevo.

![WF Fusion](./images/wffcff2.png)

Escriba el término de búsqueda `Adobe Firefly` y seleccione **Adobe Firefly**.

![WF Fusion](./images/wffcff2a.png)

Seleccione **Generar una imagen**.

![WF Fusion](./images/wffcff3.png)

Haga clic en el módulo **Adobe Firefly** para abrirlo y, a continuación, haga clic en **Agregar** para crear una nueva conexión.

![WF Fusion](./images/wffcff5.png)

Rellene los campos siguientes:

- **Nombre de conexión**: use `--aepUserLdap-- - Firefly connection`.
- **Entorno**: use **Producción**.
- **Tipo**: use **cuenta personal**.
- **ID de cliente**: copie el **ID de cliente** de su proyecto de Adobe I/O, que se llama `--aepUserLdap-- - One Adobe tutorial`.
- **Secreto de cliente**: copie el **Secreto de cliente** de su proyecto de Adobe I/O, que se llama `--aepUserLdap-- - One Adobe tutorial`.

Puedes encontrar los **ID de cliente** y el **Secreto de cliente** de tu proyecto Adobe I/O [aquí](https://developer.adobe.com/console/projects.){target="_blank"}.

![WF Fusion](./images/wffc20.png)

Una vez que hayas rellenado todos los campos, haz clic en **Continuar**. La conexión se validará automáticamente.

![WF Fusion](./images/wffcff6.png)

A continuación, seleccione la variable **prompt** proporcionada al escenario por el **webhook personalizado** entrante.

![WF Fusion](./images/wffcff7.png)

Establezca **Versión de modelo** **prompt** en **image4 standard**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffcff7b.png)

Haga clic en **Guardar** para guardar los cambios y, a continuación, haga clic en **Ejecutar una vez** para probar la configuración.

![WF Fusion](./images/wffcff8.png)

Vaya a Postman, compruebe el mensaje de su solicitud y, a continuación, haga clic en **Enviar**.

![WF Fusion](./images/wffcff8a.png)

Una vez que haya hecho clic en enviar, vuelva a Workfront Fusion y haga clic en el icono de burbuja del módulo **Adobe Firefly** para comprobar los detalles.

![WF Fusion](./images/wffcff9.png)

Vaya a **OUTPUT** para **Detalles** > **url** para encontrar la URL de la imagen generada por **Adobe Firefly**.

![WF Fusion](./images/wffcff10.png)

Copie la dirección URL y péguela en el explorador. Ahora debería ver una imagen que representa el mensaje que envió desde la solicitud de Postman, en este caso **misty meadows**.

![WF Fusion](./images/wffcff11.png)

## 1.2.4.2 Cambiar el fondo del archivo PSD

Ahora actualizará su escenario para hacerlo más inteligente mediante el uso de más conectores predeterminados. También conectará la salida de Firefly a Photoshop, de modo que la imagen de fondo del archivo de PSD cambie dinámicamente mediante la salida de la acción Generar imagen de Firefly.

Entonces debería ver esto. A continuación, pase el ratón sobre el módulo **Adobe Firefly** y haga clic en el icono **+**.

![WF Fusion](./images/wffc15.png)

En el menú de búsqueda, escriba `Photoshop` y haga clic en la acción **Adobe Photoshop**.

![WF Fusion](./images/wffc16.png)

Seleccione **Aplicar ediciones de PSD**.

![WF Fusion](./images/wffc17.png)

Entonces debería ver esto. Haga clic en **Agregar** para agregar una nueva conexión a Adobe Photoshop.

![WF Fusion](./images/wffc18.png)

Configure la conexión de la siguiente manera:

- Tipo de conexión: seleccionar **Adobe Photoshop (servidor a servidor)**
- Nombre de conexión: escriba `--aepUserLdap-- - Adobe I/O`
- ID de cliente: pegue su ID de cliente
- Secreto del cliente: pegue el secreto del cliente

Haga clic en **Continuar**.

![WF Fusion](./images/wffc19.png)

Para encontrar tu **ID de cliente** y **Secreto de cliente**, ve a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} y abre tu proyecto de Adobe I/O, que se llama `--aepUserLdap-- One Adobe tutorial`. Vaya a **Servidor a servidor de OAuth** para encontrar su ID de cliente y Secreto de cliente. Copie esos valores y péguelos en la configuración de conexión de Workfront Fusion.

![WF Fusion](./images/wffc20.png)

Después de hacer clic en **Continuar**, se mostrará brevemente una ventana emergente mientras se verifican sus credenciales. Una vez finalizado, debería ver esto.

![WF Fusion](./images/wffc21.png)

Ahora debe introducir la ubicación del archivo PSD con el que desea que Fusion trabaje. Para **Storage**, seleccione **Azure** y para **Ubicación de archivo**, escriba `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/{{1.AZURE_STORAGE_SAS_READ}}`. Coloque el cursor junto al segundo `/`. A continuación, eche un vistazo a las variables disponibles y desplácese hacia abajo para encontrar la variable **psdTemplate**. Haga clic en la variable **psdTemplate** para seleccionarla.

![WF Fusion](./images/wffc22.png)

Entonces debería ver esto.

![WF Fusion](./images/wffc23.png)

Desplácese hacia abajo hasta que vea **Capas**. Haga clic en **Agregar elemento**.

![WF Fusion](./images/wffc24.png)

Entonces debería ver esto. Ahora debe introducir el nombre de la capa en la plantilla de Photoshop PSD que se utiliza para el fondo del archivo.

![WF Fusion](./images/wffc25.png)

En el archivo **citisignal-fiber.psd**, encontrará la capa que se usa para el fondo. En este ejemplo, esa capa se denomina **2048x2048-background**.

![WF Fusion](./images/wffc26.png)

Pegue el nombre **2048x2048-background** en el diálogo de Workfront Fusion.

![WF Fusion](./images/wffc27.png)

Desplácese hacia abajo hasta que vea **Entrada**. Ahora debe definir lo que debe insertarse en la capa de fondo. En este caso, debe seleccionar la salida del módulo **Adobe Firefly**, que contiene la imagen generada dinámicamente.

Para **Almacenamiento**, seleccione **Externo**. Para **Ubicación de archivo**, tendrá que copiar y pegar la variable `{{XX.details[].url}}` de la salida del módulo **Adobe Firefly**, pero tendrá que reemplazar **XX** en la variable por el número de secuencia del módulo **Adobe Firefly**, que en este ejemplo es **5**.

![WF Fusion](./images/wffc28.png)

A continuación, desplácese hacia abajo hasta que vea **Editar**. Establezca **Edit** en **Yes** y establezca **Type** en **Layer**. Haga clic en **Agregar**.

![WF Fusion](./images/wffc29.png)

Entonces debería ver esto. A continuación, debe definir el resultado de la acción. Haga clic en **Agregar elemento** en **resultados**.

![WF Fusion](./images/wffc30.png)

Seleccione **Azure** para **Storage**, pegue este(a) `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{1.AZURE_STORAGE_SAS_WRITE}}` en **Ubicación de archivo** y seleccione **vnd.adobe.photoshop** en **Type**. Haga clic para habilitar **Mostrar configuración avanzada**.

![WF Fusion](./images/wffc31.png)

En **Configuración avanzada**, seleccione **Sí** para sobrescribir archivos con el mismo nombre.
Haga clic en **Agregar**.

![WF Fusion](./images/wffc32.png)

Entonces deberías tener esto. Haga clic en **Aceptar**.

![WF Fusion](./images/wffc33.png)

Haga clic en **Guardar** para guardar los cambios y, a continuación, haga clic en **Ejecutar una vez** para probar la configuración.

![WF Fusion](./images/wffc33a.png)

Vaya a Postman, compruebe el mensaje de su solicitud y, a continuación, haga clic en **Enviar**.

![WF Fusion](./images/wffcff8a.png)

Entonces debería ver esto. Haga clic en la burbuja en el módulo **Adobe Photoshop - Aplicar ediciones de PSD**.

![WF Fusion](./images/wffc33b.png)

Ahora puede ver que un nuevo archivo de PSD se generó correctamente y se almacenó en su cuenta de almacenamiento de Microsoft Azure.

![WF Fusion](./images/wffc33c.png)

## 1.2.4.3 Cambiar las capas de texto del archivo PSD

A continuación, pase el ratón sobre el módulo **Adobe Photoshop - Aplicar ediciones de PSD** y haga clic en el icono **+**.

![WF Fusion](./images/wffc34.png)

Seleccione **Adobe Photoshop**.

![WF Fusion](./images/wffc35.png)

Seleccione **Editar capas de texto**.

![WF Fusion](./images/wffc36.png)

Entonces debería ver esto. En primer lugar, seleccione la conexión de Adobe Photoshop que ya se configuró anteriormente y que debe llamarse `--aepUserLdap-- Adobe I/O`.

![WF Fusion](./images/wffc37.png)

Para el **archivo de entrada**, seleccione **Azure** para **almacenamiento de archivos de entrada** y asegúrese de seleccionar la salida de la solicitud anterior, **Adobe Photoshop - Aplicar ediciones de PSD**, que puede definir de esta manera: ``{{XX.data[].`_links`.renditions[].href}}`` (reemplace XX por el número de secuencia del módulo anterior Adobe Photoshop - Aplicar ediciones de PSD).

A continuación, haga clic en **+Agregar elemento** en **Capas** para empezar a agregar las capas de texto que deben actualizarse.

![WF Fusion](./images/wffc37a.png)

Hay dos cambios que se deben realizar, el texto de CTA y el texto del botón del archivo **citisignal-fiber.psd** deben actualizarse.

Para encontrar los nombres de las capas, abra el archivo **citisignal-fiber.psd**. En el archivo, verá que la capa que contiene call to action se llama **2048x2048-cta**.

![WF Fusion](./images/wffc38.png)

En el archivo **citisignal-fiber.psd**, también notará que la capa que contiene el call to action se llama **2048x2048-button-text**.

![WF Fusion](./images/wffc44.png)

Primero debe configurar los cambios que deben ocurrir en la capa **2048x2048-cta**. Escriba el nombre **2048x2048-cta** en **Nombre** en el cuadro de diálogo.

![WF Fusion](./images/wffc39.png)

Desplácese hacia abajo hasta que vea **Texto** > **Contenido**. Seleccione la variable **cta** de la carga útil de webhook. Haga clic en **Agregar**.

![WF Fusion](./images/wffc40.png)

Entonces debería ver esto. Haga clic en **+Agregar elemento** en **Capas** para empezar a agregar la siguiente capa de texto que necesite actualizarse.

![WF Fusion](./images/wffc40a.png)

Escriba el nombre **2048x2048-button-text** en **Nombre** en el cuadro de diálogo.

![WF Fusion](./images/wffc40b.png)

Desplácese hacia abajo hasta que vea **Texto** > **Contenido**. Seleccione la variable **button** de la carga útil de webhook. Haga clic en **Agregar**.

![WF Fusion](./images/wffc40c.png)

Entonces debería ver esto.

![WF Fusion](./images/wffc40d.png)

Desplácese hacia abajo hasta que vea **Salida**. Para **Almacenamiento**, seleccione **Azure**. Para **ubicación de archivo**, ingrese la siguiente ubicación. Tenga en cuenta la adición de la variable `{{timestamp}}` al nombre de archivo que se utiliza para garantizar que cada archivo generado tenga un nombre único. Además, establezca **Type** en **vnd.adobe.photoshop**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

Establezca **Type** en **vnd.adobe.photoshop**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffc41.png)

Haga clic en **Guardar** para guardar los cambios.

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 respuesta de webhook

Después de aplicar estos cambios a su archivo Photoshop, debe configurar una **respuesta de webhook** que se devolverá a la aplicación que haya activado este escenario.

Pase el ratón sobre el módulo **Adobe Photoshop - Editar capas de texto** y haga clic en el icono **+**.

![WF Fusion](./images/wffc48.png)

Busque `webhooks` y seleccione **Webhook**.

![WF Fusion](./images/wffc49.png)

Seleccione **Respuesta de webhook**.

![WF Fusion](./images/wffc50.png)

Entonces debería ver esto. Pegue la siguiente carga útil en **Cuerpo**.

```json
{
    "newPsdTemplate": ""
}
```

![WF Fusion](./images/wffc51.png)

Copie y pegue la variable `{{XX.data[]._links.renditions[].href}}` y reemplace **XX** por el número de secuencia del último módulo **Adobe Photoshop - Editar capas de texto**, que en este caso es **7**.

![WF Fusion](./images/wffc52.png)

Habilite la casilla de verificación para **Mostrar configuración avanzada** y luego haga clic en **Agregar elemento**.

![WF Fusion](./images/wffc52b.png)

En el campo **Clave**, escriba `Content-Type`. En el campo **Valor**, escriba `application/json`. Haga clic en **Agregar**.

![WF Fusion](./images/wffc52a.png)

Entonces deberías tener esto. Haga clic en **Aceptar**.

![WF Fusion](./images/wffc53.png)

Haga clic en **Alinear automáticamente**.

![WF Fusion](./images/wffc54.png)

Entonces debería ver esto. Haga clic en **Guardar** para guardar los cambios y, a continuación, haga clic en **Ejecutar una vez** para probar el escenario.

![WF Fusion](./images/wffc55.png)

Vuelva a Postman y haga clic en **Enviar**. La solicitud que se está usando aquí es **prados brumosos**.

![WF Fusion](./images/wffc56.png)

A continuación, se activará el escenario y, pasado un tiempo, se mostrará una respuesta en Postman que contenga la URL del archivo PSD recién creado.

![WF Fusion](./images/wffc58.png)

Como recordatorio: una vez que el escenario se haya ejecutado en Workfront Fusion, podrá ver información sobre cada módulo haciendo clic en la burbuja situada encima de cada módulo.

![WF Fusion](./images/wffc59.png)

Con el Explorador de almacenamiento de Azure, puede buscar y abrir el archivo de PSD recién creado haciendo doble clic en él en el Explorador de almacenamiento de Azure.

![WF Fusion](./images/wffc60.png)

El archivo debería tener este aspecto, con el fondo reemplazado por un fondo con **prados empañados**.

![WF Fusion](./images/wffc61.png)

Si vuelve a ejecutar el escenario y, a continuación, envía una nueva solicitud desde Postman con un mensaje diferente, verá lo fácil y reutilizable que se ha vuelto su escenario. En este ejemplo, el nuevo indicador que se está usando es **desierto soleado**.

![WF Fusion](./images/wffc62.png)

Y un par de minutos después, se ha generado un nuevo archivo PSD con un nuevo fondo.

![WF Fusion](./images/wffc63.png)

## Próximos pasos

Vaya a [1.2.3 Frame.io y Workfront Fusion](./ex3.md){target="_blank"}

Volver a [Automatización del flujo de trabajo de Creative con Workfront Fusion](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
