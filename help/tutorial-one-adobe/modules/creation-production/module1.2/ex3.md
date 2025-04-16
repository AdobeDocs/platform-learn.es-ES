---
title: Automatización de procesos con Workfront Fusion
description: Aprenda a procesar la automatización con Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 1.2.3 Automatización de procesos con Workfront Fusion

Aprenda a automatizar los procesos con Workfront Fusion.

## 1.2.3.1 iterando en varios valores

El escenario debería tener este aspecto:

![WF Fusion](./images/wffusion200.png)

Hasta ahora, ha cambiado el texto de un archivo Photoshop por un valor estático. Para escalar y automatizar los flujos de trabajo de creación de contenido, es necesario iterar una lista de valores e insertar dichos valores de forma dinámica en el archivo Photoshop. En los pasos siguientes, agregará un deseo de repetir valores en el escenario existente.

Entre el nodo **Router** y el nodo **Photoshop Change Text**, seleccione el icono **wrench** y seleccione **Add a module**.

![WF Fusion](./images/wffusion201.png)

Busque `flow` y seleccione **Control de flujo**.

![WF Fusion](./images/wffusion202.png)

Seleccione **Iterador**.

![WF Fusion](./images/wffusion203.png)

La pantalla debería tener un aspecto similar al siguiente:

![WF Fusion](./images/wffusion204.png)

Aunque es posible leer archivos de entrada como los archivos CSV, por ahora debe utilizar una versión básica de un archivo CSV definiendo una cadena de texto y dividiendo ese archivo de texto.

Puede encontrar la función **split** seleccionando el icono **T**, donde verá todas las funciones disponibles para manipular los valores de texto. Seleccione la función **split** y debería ver esto.

![WF Fusion](./images/wffusion206.png)

La función split espera una matriz de valores antes del punto y coma y espera que especifique el separador después del punto y coma. Para este prueba, debe usar una matriz simple con 2 campos, **Comprar ahora** y **Haga clic aquí**, y el separador a usar es **,**.

Introduzca esto en el **campo Matriz** reemplazando la función de división **actualmente vacía**: `{{split("Buy now, Click here "; ",")}}`. Seleccione **OK**.

![WF Fusion](./images/wffusion205.png)

Seleccione **Texto de cambio de Photoshop** para agregar algunas variables en lugar de valores estáticos para los campos de entrada y salida.

![WF Fusion](./images/wffusion207.png)

En **Solicitud contenido**, está el texto **Haga clic aquí**. Este texto debe ser reemplazado por los valores provenientes de su matriz.

![WF Fusion](./images/wffusion208.png)

Eliminar el texto **Haga clic aquí** y sustitúyalo seleccionando el Valor de variable **** en el **nodo Iterador**. Esto garantiza que el texto del botón del Photoshop documento se actualice de forma dinámica.

![WF Fusion](./images/wffusion209.png)

También debe actualizar el nombre de archivo usado para escribir el archivo en su cuenta de almacenamiento de Azure. Si el nombre del archivo es estático, cada nueva iteración simplemente sobrescribe el archivo anterior y, como tal, pierde los archivos personalizados. El nombre de archivo estático actual es **citisignal-fiber-changed-text.psd**, y ahora necesita actualizarlo.

Coloque el cursor detrás de la palabra `text`.

![WF Fusion](./images/wffusion210.png)

En primer lugar, agregue un guion `-` y, a continuación, seleccione el valor **Posición de pedido del paquete**. Esto garantiza que para la primera iteración, Workfront Fusion agregue `-1` al nombre del archivo, para la segunda iteración `-2`, etc. Seleccione **Aceptar**.

![WF Fusion](./images/wffusion211.png)

Guarde el escenario y seleccione **Ejecutar una vez**.

![WF Fusion](./images/wffusion212.png)

Una vez que se haya ejecutado el escenario, vuelva al Explorador de almacenamiento de Azure y actualice la carpeta. Luego debería ver los 2 archivos recién creados.

![WF Fusion](./images/wffusion213.png)

Descargue y abra cada archivo. Debe escribir varios textos en los botones. Este es el archivo `citisignal-fiber-changed-text-1.psd`.

![WF Fusion](./images/wffusion214.png)

Este es el archivo `citisignal-fiber-changed-text-2.psd`.

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2 Activar su escenario mediante un gancho web

Hasta ahora, ha ejecutado el escenario manualmente para probarlo. Actualicemos ahora su escenario con un webhook, para que pueda activarse desde un entorno externo.

Seleccione **+**, busque **webhook** y luego seleccione **Webhooks**.

![WF Fusion](./images/wffusion216.png)

Seleccione **webhook personalizado**.

Arrastre y conecte el nodo **Gancho web personalizado** para que se conecte al primer nodo del lienzo, que se llama **Inicializar constantes**.

![WF Fusion](./images/wffusion217.png)

Seleccione el nodo **webhook personalizado**. A continuación, seleccione **Agregar**.

![WF Fusion](./images/wffusion218.png)

Definir **nombre de webhook** en `--aepUserLdap-- - Tutorial 1.2`.

![WF Fusion](./images/wffusion219.png)

Marque la casilla de **Obtener encabezados de solicitud**. Seleccione **Guardar**.

![WF Fusion](./images/wffusion220.png)

La URL del gancho web ya está disponible. Copie la dirección URL.

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
	"psdTemplate": "placeholder",
	"xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

Cuando vuelva a Workfront Fusion, aparecerá un mensaje en el gancho web personalizado que dice: **Determinado correctamente**.

![WF Fusion](./images/wffusion227.png)

Seleccione **Guardar** y luego **Ejecutar una vez**. Tu escenario ahora estará activo, pero no se ejecutará hasta que vuelvas a seleccionar **Enviar** en Postman.

![WF Fusion](./images/wffusion230.png)

En Postman, seleccione **Enviar** de nuevo.

![WF Fusion](./images/wffusion228.png)

Su escenario se volverá a ejecutar y creará los dos archivos igual que antes.

![WF Fusion](./images/wffusion232.png)

Cambie el nombre de su solicitud de cartero a `POST - Send Request to Workfront Fusion Webhook`.

![WF Fusion](./images/wffusion233.png)

Ahora debe inicio utilizando la variable **psdTemplate**. En lugar de codificar la ubicación del archivo de entrada en el **nodo Cambiar texto** de Photoshop, utilizará el variable entrante del solicitud del cartero.

Abra el **nodo Cambiar texto** Photoshop y vaya a **Solicitar contenido**. Seleccione el nombre **de archivo codificado citisignal-fiber.psd** debajo **de entradas** y elimínelo.

![WF Fusion](./images/wffusion234.png)

Seleccione la variable **psdTemplate**. Seleccione **Aceptar** y, a continuación, guarde su escenario.

![WF Fusion](./images/wffusion235.png)

Seleccione **ON** para activar su escenario. Su escenario se está ejecutando sin interrupciones.

![WF Fusion](./images/wffusion236.png)

De nuevo en Postman, ingrese el nombre de archivo `citisignal-fiber.psd` como valor para la variable **psdTemplate** y seleccione **Send** nuevamente para ejecutar su escenario nuevamente.

![WF Fusion](./images/wffusion237.png)

Al especificar el plantilla PSD como un variable proporcionado por un sistema externo, ahora ha creado un escenario reutilizable.

Ahora ha completado este ejercicio.

## Pasos siguientes

Vaya a la automatización de [1.2.4 mediante conectores](./ex4.md){target="_blank"}

Volver a [Creative automatización del flujo de trabajo con Workfront Fusion](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
