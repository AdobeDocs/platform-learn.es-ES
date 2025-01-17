---
title: Automatización de procesos con Workfront Fusion
description: Automatización de procesos con Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: f1f70a0e4ea3f59b5b121275e7db633caf953df9
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# 1.2.3 Automatización de procesos con Workfront Fusion

Su escenario ahora tiene este aspecto.

![WF Fusion](./images/wffusion200.png)

## 1.2.3.1 Iteración en varios valores

Hasta ahora, ha cambiado el texto de un archivo Photoshop por un valor estático. Para escalar y automatizar los flujos de trabajo de creación de contenido, es necesario iterar una lista de valores e insertar dichos valores de forma dinámica en el archivo Photoshop. En los pasos siguientes, agregará un deseo de repetir valores en el escenario existente.

Entre el nodo **Enrutador** y el nodo **Texto de cambio de Photoshop**, haga clic en el icono **llave inglesa** y seleccione **Agregar un módulo**.

![WF Fusion](./images/wffusion201.png)

Busque `flow` y seleccione **Control de flujo**.

![WF Fusion](./images/wffusion202.png)

Seleccione **Iterador**.

![WF Fusion](./images/wffusion203.png)

Entonces deberías tener esto.

![WF Fusion](./images/wffusion204.png)

Aunque es posible leer archivos de entrada como los archivos CSV, por ahora debe utilizar una versión básica de un archivo CSV definiendo una cadena de texto y dividiendo ese archivo de texto.

Para encontrar la función **split**, haga clic en el icono **T**, donde verá todas las funciones disponibles para manipular los valores de texto. Haga clic en la función **split** y debería ver esto.

![WF Fusion](./images/wffusion206.png)

La función split espera una matriz de valores antes del punto y coma y espera que especifique el separador después del punto y coma. Para esta prueba, debe usar una matriz simple con 2 campos, **Comprar ahora** y **Haga clic aquí**, y el separador que debe usar es **,**.

Escriba esto en el campo **Matriz** reemplazando la función **split** actualmente vacía: `{{split("Buy now, Click here "; ",")}}`. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion205.png)

El iterador está configurado ahora y, si ejecutara el escenario ahora, lo ejecutaría dos veces. Sin embargo, todavía hay un problema, ya que actualmente está usando valores estáticos en su nodo **Photoshop Change Text**. Haga clic en **Texto de cambio de Photoshop** para agregar algunas variables en lugar de valores estáticos para los campos de entrada y salida.

![WF Fusion](./images/wffusion207.png)

En **Solicitar contenido**, verá el texto **Haga clic aquí**. Este texto debe reemplazarse por los valores procedentes de la matriz.

![WF Fusion](./images/wffusion208.png)

Elimine el texto **Haga clic aquí** y reemplácelo seleccionando la variable **Value** del nodo **Iterator**. Esto garantizará que el texto del botón del documento de Photoshop se actualice dinámicamente.

![WF Fusion](./images/wffusion209.png)

También debe actualizar el nombre de archivo que se utiliza para escribir el archivo en su cuenta de almacenamiento de Azure. Si el nombre del archivo es estático, cada nueva iteración simplemente sobrescribirá el archivo anterior y, como tal, perderá los archivos personalizados. El nombre de archivo estático actual es **citisignal-fiber-changed-text.psd**, y ahora necesita actualizarlo. Coloque el cursor detrás de la palabra `text`.

![WF Fusion](./images/wffusion210.png)

En primer lugar, agregue un guion `-` y, a continuación, seleccione el valor **Posición de pedido del paquete**. Esto garantizará que, en la primera iteración, Workfront Fusion agregue `-1` al nombre de archivo, en la segunda iteración `-2`, etc. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion211.png)

Guarde el escenario y haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffusion212.png)

Una vez que se haya ejecutado el escenario, vuelva al Explorador de almacenamiento de Azure y actualice la carpeta. Luego debería ver los 2 archivos recién creados.

![WF Fusion](./images/wffusion213.png)

Descargue y abra cada archivo. A continuación, debería ver los distintos textos en los botones. Este es el archivo `citisignal-fiber-changed-text-1.psd`.

![WF Fusion](./images/wffusion214.png)

Este es el archivo `citisignal-fiber-changed-text-2.psd`.

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2 Activa tu escenario usando un webhook

Hasta ahora, ha ejecutado el escenario manualmente para probarlo. Actualicemos ahora su escenario con un webhook, para que pueda activarse desde un entorno externo.

Haga clic en el icono **+**, busque **webhook** y, a continuación, seleccione **Webhooks**.

![WF Fusion](./images/wffusion216.png)

Seleccione **webhook personalizado**.

Arrastre y conecte el nodo **Gancho web personalizado** para que se conecte al primer nodo del lienzo, que se llama **Inicializar constantes**.

![WF Fusion](./images/wffusion217.png)

Haga clic en el nodo **webhook personalizado**. A continuación, haga clic en **Agregar**.

![WF Fusion](./images/wffusion218.png)

Establezca el **nombre del webhook** en `--aepUserLdap-- - Tutorial 1.2`.

![WF Fusion](./images/wffusion219.png)

Marque la casilla de verificación de **Obtener encabezados de solicitud**. Haga clic en **Guardar**.

![WF Fusion](./images/wffusion220.png)

La URL del gancho web ya está disponible. Copie la dirección URL.

![WF Fusion](./images/wffusion221.png)

Abra Postman y agregue una nueva carpeta a la colección **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Asigne un nombre a la carpeta `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

En la carpeta que acaba de crear, haga clic en los 3 puntos **...** y seleccione **Agregar solicitud**.

![WF Fusion](./images/wffusion224.png)

Establece **Method type** en **POST** y pega la URL del webhook en la barra de direcciones.

![WF Fusion](./images/wffusion225.png)

Debe enviar un cuerpo personalizado para que los elementos de la variable se puedan proporcionar desde una fuente externa al escenario de Workfront Fusion. Vaya a **Cuerpo** y seleccione **sin procesar**.

![WF Fusion](./images/wffusion226.png)

Pegue el texto siguiente en el cuerpo de la solicitud. Haga clic en **Enviar**.

```json
{
    "psdTemplate": "placeholder",
    "xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

Vuelva a Workfront Fusion. Ahora verás un mensaje en tu webhook personalizado que dice: **Determinado correctamente**.

![WF Fusion](./images/wffusion227.png)

Haga clic en **Guardar** y luego en **Ejecutar una vez**. Tu escenario estará activo, pero no se ejecutará hasta que vuelvas a hacer clic en **Enviar** en Postman.

![WF Fusion](./images/wffusion230.png)

Vaya a Postman y vuelva a hacer clic en **Enviar**.

![WF Fusion](./images/wffusion228.png)

A continuación, el escenario se volverá a ejecutar y creará los dos archivos igual que antes.

![WF Fusion](./images/wffusion232.png)

Cambie el nombre de su solicitud de Postman a `POST - Send Request to Workfront Fusion Webhook`.

![WF Fusion](./images/wffusion233.png)

Ahora necesita empezar a usar la variable **psdTemplate**. En lugar de codificar la ubicación del archivo de entrada en el nodo **Texto de cambio de Photoshop**, ahora utilizará la variable entrante de la solicitud de Postman.

Abra el nodo **Photoshop Change Text** y vaya a **Solicitar contenido**. Seleccione el nombre de archivo codificado **citisignal-fiber.psd** en **input** y elimínelo.

![WF Fusion](./images/wffusion234.png)

Seleccione la variable **psdTemplate**. Haga clic en **Aceptar** y, a continuación, guarde el escenario.

![WF Fusion](./images/wffusion235.png)

Haz clic en **ACTIVADO** para activar tu escenario. Su escenario se ejecutará sin interrupciones.

![WF Fusion](./images/wffusion236.png)

Vuelva a Postman. Escriba el nombre de archivo `citisignal-fiber.psd` como valor para la variable **psdTemplate** y haga clic en **Enviar** de nuevo para volver a ejecutar el escenario.

![WF Fusion](./images/wffusion237.png)

Al especificar la plantilla del PSD como una variable proporcionada por un sistema externo, ahora ha creado un escenario reutilizable.

Ya ha terminado este ejercicio.

Siguiente paso: [Resumen y beneficios](./summary.md)

[Volver al módulo 1.2](./automation.md)

[Volver a todos los módulos](./../../../overview.md)
