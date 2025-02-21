---
title: Automatización con conectores
description: Automatización con conectores
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 6ef4ce94dbbcd65ab30bcfad24f4ddd746c26b82
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 1%

---

# 1.2.4 Automatización mediante conectores

Ahora empezará a utilizar los conectores predeterminados en Workfront Fusion para Photoshop y conectará la solicitud de Firefly Text-2-Image y las solicitudes de Photoshop en un escenario.

## 1.2.4.1 duplicar y preparar su escenario

En el menú de la izquierda, vaya a **Escenarios** y seleccione la carpeta `--aepUserLdap--`. Debería ver el escenario que creó anteriormente, que se llama `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffc1.png)

Haga clic en la flecha para abrir el menú desplegable y seleccione **Clonar**.

![WF Fusion](./images/wffc2.png)

Establezca **Name** del escenario clonado en `--aepUserLdap-- - Firefly + Photoshop` y seleccione el **equipo de destino** adecuado. Haga clic en **Agregar** para agregar un nuevo enlace web.

![WF Fusion](./images/wffc3.png)

Establezca el **nombre del webhook** en `--aepUserLdap-- - Firefly + Photoshop Webhook`. Haga clic en **Guardar**.

![WF Fusion](./images/wffc4.png)

Entonces debería ver esto. Haga clic en **Guardar**.

![WF Fusion](./images/wffc5.png)

Entonces debería ver esto. Haga clic en el nodo **Webhook**.

![WF Fusion](./images/wffc6.png)

Haga clic en **Copiar dirección al portapapeles** y, a continuación, haga clic en **Volver a determinar la estructura de datos**.

![WF Fusion](./images/wffc7.png)

Abra Postman. Añada una nueva solicitud en la misma carpeta que estaba utilizando antes.

![WF Fusion](./images/wffc9.png)

Asegúrese de que se aplica la siguiente configuración:

- Nombre de solicitud: `POST - Send Request to Workfront Fusion Webhook Firefly + Photoshop`
- Tipo de solicitud: `POST`
- Solicitar URL: pegue la URL que ha copiado del webhook de su Workfront Fusion Scenario.

Vaya a **Cuerpo** y establezca **Tipo de cuerpo** en **sin procesar** - **JSON**. Pegue la siguiente carga útil en **Body**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Esta nueva carga útil garantizará que toda la información de la variable se proporcione desde fuera del escenario en lugar de estar codificada en el escenario. En un escenario empresarial, una organización necesita que un escenario se defina de forma reutilizable, lo que significa que se deben proporcionar varias variables como variables de entrada en lugar de tenerlas codificadas en el escenario.

Entonces deberías tener esto. Haga clic en **Enviar**.

![WF Fusion](./images/wffc10.png)

El webhook de Workfront Fusion sigue esperando la entrada.

![WF Fusion](./images/wffc11.png)

Una vez que hayas hecho clic en **Enviar**, el mensaje debería cambiar a **Determinado correctamente**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffc12.png)

## 1.2.4.2 Actualizar nodo T2I de Firefly

Haga clic en el nodo **Firefly T2I**. Entonces debería ver esto. La petición de datos de esta solicitud estaba previamente codificada para **caballos en un campo**. Ahora eliminará ese texto codificado y lo reemplazará por un campo proveniente del webhook.

![WF Fusion](./images/wffcfft2i1.png)

Quite el texto **horse en un campo** y reemplácelo por la variable **prompt** que se encuentra en las variables **Webhook**. Haga clic en **Aceptar** para guardar los cambios.

![WF Fusion](./images/wffcfft2i2.png)

## 1.2.4.2 Cambiar el fondo del archivo PSD

Ahora actualizará su escenario para hacerlo más inteligente mediante el uso de conectores predeterminados. También conectará la salida de Firefly a Photoshop, de modo que la imagen de fondo del archivo de PSD cambie dinámicamente mediante la salida de la acción Generar imagen de Firefly.

En el ejercicio anterior, deshabilitó la ruta **Firefly T2I**. Ahora debería deshacer eso. Haga clic en el icono **stop** para habilitar de nuevo la ruta.

![WF Fusion](./images/wffc13.png)

Verá que el icono **stop** desaparece. A continuación, haga clic en el icono **llave inglesa** en la otra ruta hacia la configuración del ejercicio anterior y seleccione **Deshabilitar ruta**.

![WF Fusion](./images/wffc14.png)

Entonces debería ver esto. A continuación, pase el ratón sobre el nodo **Firefly T2I** y haga clic en el icono **+**.

![WF Fusion](./images/wffc15.png)

En el menú de búsqueda, escribe `Photoshop` y luego haz clic en la acción **Adobe Photoshop**.

![WF Fusion](./images/wffc16.png)

Seleccione **Aplicar ediciones de PSD**.

![WF Fusion](./images/wffc17.png)

Entonces debería ver esto. Haga clic en **Agregar** para agregar una nueva conexión a Adobe Photoshop.

![WF Fusion](./images/wffc18.png)

Configure la conexión de la siguiente manera:

- Tipo de conexión: seleccionar **Adobe Photoshop (servidor a servidor)**
- Nombre de conexión: escriba `--aepUserLdap-- - Adobe IO`
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

Desplácese hacia abajo hasta que vea **Entrada**. Ahora debe definir lo que debe insertarse en la capa de fondo. En este caso, es necesario seleccionar la salida del objeto Firefly T2I, que contiene la imagen generada dinámicamente.

Para **Almacenamiento**, seleccione **Externo**. Para **ubicación de archivos**, busque y busque la variable `data.outputs[].image.url` en la salida de la solicitud **Firefly T2I**.

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

## 1.2.4.3 Cambiar las capas de texto del archivo PSD

### Texto de la llamada a la acción

A continuación, pase el ratón sobre el nodo **Adobe Photoshop - Apply PSD edits** y haga clic en el icono **+**.

![WF Fusion](./images/wffc34.png)

Seleccione **Adobe Photoshop**.

![WF Fusion](./images/wffc35.png)

Seleccione **Editar capas de texto**.

![WF Fusion](./images/wffc36.png)

Entonces debería ver esto. En primer lugar, seleccione la conexión de Adobe Photoshop que ya se configuró anteriormente y que debe llamarse `--aepUserLdap-- Adobe IO`.

Ahora necesita definir la ubicación del **archivo de entrada**, que es el resultado del paso anterior y en **Capas**, debe escribir el **Nombre** de la capa de texto que desea cambiar.

![WF Fusion](./images/wffc37.png)

Para el **archivo de entrada**, seleccione **Azure** para **almacenamiento de archivos de entrada** y asegúrese de seleccionar la salida de la solicitud anterior, **Adobe Photoshop - Aplicar ediciones de PSD**, que puede tomar desde aquí: `data[]._links.renditions[].href`

![WF Fusion](./images/wffc37a.png)

Abra el archivo **citisignal-fiber.psd**. En el archivo, verá que la capa que contiene la llamada a la acción se llama **2048x2048-cta**.

![WF Fusion](./images/wffc38.png)

Escriba el nombre **2048x2048-cta** en **Nombre** en el cuadro de diálogo.

![WF Fusion](./images/wffc39.png)

Desplácese hacia abajo hasta que vea **Texto** > **Contenido**. Seleccione la variable **cta** de la carga útil de webhook.

![WF Fusion](./images/wffc40.png)

Desplácese hacia abajo hasta que vea **Salida**. Para **Almacenamiento**, seleccione **Azure**. Para **ubicación de archivo**, ingrese la siguiente ubicación. Tenga en cuenta la adición de la variable `{{timestamp}}` al nombre de archivo que se utiliza para garantizar que cada archivo generado tenga un nombre único. Además, establezca **Type** en **vnd.adobe.photoshop**. Haga clic en **Aceptar**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc41.png)

### Texto del botón

Haga clic con el botón derecho en el nodo que acaba de crear y seleccione **Clonar**. Esto creará un segundo objeto similar.

![WF Fusion](./images/wffc42.png)

Entonces debería ver esto. En primer lugar, seleccione la conexión de Adobe Photoshop que ya se configuró anteriormente y que debe llamarse `--aepUserLdap-- Adobe IO`.

Ahora necesita definir la ubicación del **archivo de entrada**, que es el resultado del paso anterior y en **Capas**, debe escribir el **Nombre** de la capa de texto que desea cambiar.

![WF Fusion](./images/wffc43.png)

Para el **archivo de entrada**, seleccione **Azure** para **almacenamiento de archivos de entrada** y asegúrese de seleccionar el resultado de la solicitud anterior, **Adobe Photoshop - Editar capas de texto**, que puede tomar desde aquí: `data[]._links.renditions[].href`

Abra el archivo **citisignal-fiber.psd**. En el archivo, verá que la capa que contiene la llamada a la acción se llama **2048x2048-button-text**.

![WF Fusion](./images/wffc44.png)

Escriba el nombre **2048x2048-cta** en **Nombre** en el cuadro de diálogo.

![WF Fusion](./images/wffc43.png)

Desplácese hacia abajo hasta que vea **Texto** > **Contenido**. Seleccione la variable **cta** de la carga útil de webhook.

![WF Fusion](./images/wffc45.png)

Desplácese hacia abajo hasta que vea **Salida**. Para **Almacenamiento**, seleccione **Azure**. Para **ubicación de archivo**, ingrese la siguiente ubicación. Tenga en cuenta la adición de la variable `{{timestamp}}` al nombre de archivo que se utiliza para garantizar que cada archivo generado tenga un nombre único. Además, establezca **Type** en **vnd.adobe.photoshop**. Haga clic en **Aceptar**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc46.png)

Haga clic en **Guardar** para guardar los cambios.

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 respuesta de webhook

Después de aplicar estos cambios a su archivo Photoshop, debe configurar una **respuesta de webhook** que se devolverá a la aplicación que haya activado este escenario.

Pase el ratón sobre el nodo **Adobe Photoshop - Editar capas de texto** y haga clic en el icono **+**.

![WF Fusion](./images/wffc48.png)

Busque **webhook** y seleccione **Webhook**.

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

Seleccione la ruta de acceso `data[]._links.renditions[].href` de la salida de la solicitud anterior. Habilite la casilla de verificación para **Mostrar configuración avanzada** y luego haga clic en **Agregar elemento**.

![WF Fusion](./images/wffc52.png)

En el campo **Clave**, escriba `Content-Type`. En el campo **Valor**, escriba `application/json`. Haga clic en **Guardar**.

![WF Fusion](./images/wffc52a.png)

Entonces deberías tener esto. Haga clic en **Aceptar**.

![WF Fusion](./images/wffc53.png)

Haga clic en **Alinear automáticamente**.

![WF Fusion](./images/wffc54.png)

Entonces debería ver esto. Haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffc55.png)

Vuelva a Postman y haga clic en **Enviar**. La solicitud que se está usando aquí es **prados brumosos**.

![WF Fusion](./images/wffc56.png)

A continuación, se activará el escenario y, pasado un tiempo, se mostrará una respuesta en Postman que contenga la URL del archivo PSD recién creado.

![WF Fusion](./images/wffc58.png)

Como recordatorio: una vez que el escenario se haya ejecutado en Workfront Fusion, podrá ver información sobre cada nodo haciendo clic en la burbuja situada encima de cada nodo.

![WF Fusion](./images/wffc59.png)

Con el Explorador de almacenamiento de Azure, puede buscar y abrir el archivo de PSD recién creado haciendo doble clic en él en el Explorador de almacenamiento de Azure.

![WF Fusion](./images/wffc60.png)

El archivo debería tener este aspecto, con el fondo reemplazado por un fondo con **prados empañados**.

![WF Fusion](./images/wffc61.png)

Si vuelve a ejecutar el escenario y, a continuación, envía una nueva solicitud desde Postman con un mensaje diferente, verá lo fácil y reutilizable que se ha vuelto su escenario. En este ejemplo, el nuevo indicador que se está usando es **desierto soleado**.

![WF Fusion](./images/wffc62.png)

Y un par de minutos después, se ha generado un nuevo archivo PSD con un nuevo fondo.

![WF Fusion](./images/wffc63.png)

## Pasos siguientes

Vaya a [Resumen y ventajas de la automatización de servicios de Firefly](./summary.md){target="_blank"}

Volver a [Automatizar servicios de Adobe Firefly](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
