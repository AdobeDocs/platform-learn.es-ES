---
title: Automatización de procesos con Workfront Fusion
description: Aprenda a procesar la automatización con Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: e419f07dbef519d9cf2f0100878e4cc880ad5f94
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# Automatización de procesos con Workfront Fusion

Aprenda a procesar la automatización con Workfront Fusion.

## Iteración en varios valores

El escenario debería tener este aspecto:

![WF Fusion](./images/wffusion200.png)

Hasta ahora, ha cambiado el texto de un archivo Photoshop por un valor estático. Para escalar y automatizar los flujos de trabajo de creación de contenido, es necesario iterar una lista de valores e insertar dichos valores de forma dinámica en el archivo Photoshop. En los pasos siguientes, agregará un deseo de repetir valores en el escenario existente.

1. Entre el nodo **Router** y el nodo **Photoshop Change Text**, seleccione el icono **wrench** y seleccione **Add a module**.

   ![WF Fusion](./images/wffusion201.png)

1. Busque `flow` y seleccione **Control de flujo**.

   ![WF Fusion](./images/wffusion202.png)

1. Seleccione **Iterador**.

   ![WF Fusion](./images/wffusion203.png)

   La pantalla debería tener un aspecto similar al siguiente:

   ![WF Fusion](./images/wffusion204.png)

   Aunque es posible leer archivos de entrada como los archivos CSV, por ahora debe utilizar una versión básica de un archivo CSV definiendo una cadena de texto y dividiendo ese archivo de texto.

1. Puede encontrar la función **split** seleccionando el icono **T**, donde verá todas las funciones disponibles para manipular los valores de texto. Seleccione la función **split** y debería ver esto.

   ![WF Fusion](./images/wffusion206.png)

1. La función split espera una matriz de valores antes del punto y coma y espera que especifique el separador después del punto y coma. Para esta prueba, debe usar una matriz simple con 2 campos, **Comprar ahora** y **Haga clic aquí**, y el separador que debe usar es **,**.

1. Escriba esto en el campo **Matriz** reemplazando la función **split** actualmente vacía: `{{split("Buy now, Click here "; ",")}}`. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion205.png)



1. Seleccione **Texto de cambio de Photoshop** para agregar algunas variables en lugar de valores estáticos para los campos de entrada y salida.

   ![WF Fusion](./images/wffusion207.png)

   En **Solicitar contenido**, está el texto **Haga clic aquí**. Este texto debe reemplazarse por los valores procedentes de la matriz.

   ![WF Fusion](./images/wffusion208.png)

1. Elimine el texto **Haga clic aquí** y reemplácelo seleccionando la variable **Value** del nodo **Iterator**. Esto garantiza que el texto del botón del documento de Photoshop se actualice dinámicamente.

   ![WF Fusion](./images/wffusion209.png)

   También debe actualizar el nombre de archivo utilizado para escribir el archivo en su cuenta de almacenamiento de Azure. Si el nombre del archivo es estático, cada nueva iteración simplemente sobrescribe el archivo anterior y, como tal, pierde los archivos personalizados. El nombre de archivo estático actual es **citisignal-fiber-changed-text.psd**, y ahora necesita actualizarlo.

1. Coloque el cursor detrás de la palabra `text`.

   ![WF Fusion](./images/wffusion210.png)

1. En primer lugar, agregue un guion `-` y, a continuación, seleccione el valor **Posición de pedido del paquete**. Esto garantiza que para la primera iteración, Workfront Fusion agregue `-1` al nombre del archivo, para la segunda iteración `-2`, etc. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion211.png)

1. Guarde el escenario y seleccione **Ejecutar una vez**.

   ![WF Fusion](./images/wffusion212.png)

   Una vez que se haya ejecutado el escenario, vuelva al Explorador de almacenamiento de Azure y actualice la carpeta. Luego debería ver los 2 archivos recién creados.

   ![WF Fusion](./images/wffusion213.png)

1. Descargue y abra cada archivo. Debe escribir varios textos en los botones. Este es el archivo `citisignal-fiber-changed-text-1.psd`.

   ![WF Fusion](./images/wffusion214.png)

   Este es el archivo `citisignal-fiber-changed-text-2.psd`.

   ![WF Fusion](./images/wffusion215.png)

## Activa tu escenario usando un webhook

Hasta ahora, ha ejecutado el escenario manualmente para probarlo. Actualicemos ahora su escenario con un webhook, para que pueda activarse desde un entorno externo.

1. Seleccione **+**, busque **webhook** y luego seleccione **Webhooks**.

   ![WF Fusion](./images/wffusion216.png)

1. Seleccione **webhook personalizado**.

1. Arrastre y conecte el nodo **Gancho web personalizado** para que se conecte al primer nodo del lienzo, que se llama **Inicializar constantes**.

   ![WF Fusion](./images/wffusion217.png)

1. Seleccione el nodo **webhook personalizado**. A continuación, seleccione **Agregar**.

   ![WF Fusion](./images/wffusion218.png)

1. Definir **nombre de webhook** en `--aepUserLdap-- - Tutorial 1.2`.

   ![WF Fusion](./images/wffusion219.png)

1. Marque la casilla de **Obtener encabezados de solicitud**. Seleccione **Guardar**.

   ![WF Fusion](./images/wffusion220.png)

1. La URL del gancho web ya está disponible. Copie la dirección URL.

   ![WF Fusion](./images/wffusion221.png)

1. Abra Postman y agregue una nueva carpeta a la colección **FF - Firefly Services Tech Insiders**.

   ![WF Fusion](./images/wffusion222.png)

1. Asigne un nombre a la carpeta `--aepUserLdap-- - Workfront Fusion`.

   ![WF Fusion](./images/wffusion223.png)

1. En la carpeta que acaba de crear, seleccione los 3 puntos **...** y seleccione **Agregar solicitud**.

   ![WF Fusion](./images/wffusion224.png)

1. Establece **Method type** en **POST** y pega la URL del webhook en la barra de direcciones.

   ![WF Fusion](./images/wffusion225.png)

   Debe enviar un cuerpo personalizado para que los elementos de la variable se puedan proporcionar desde una fuente externa al escenario de Workfront Fusion.

1. Vaya a **Cuerpo** y seleccione **sin procesar**.

   ![WF Fusion](./images/wffusion226.png)

1. Pegue el texto siguiente en el cuerpo de la solicitud. Seleccione **Enviar**.

   ```json
   {
       "psdTemplate": "placeholder",
       "xlsFile": "placeholder"
   }
   ```

   ![WF Fusion](./images/wffusion229.png)

1. Cuando vuelva a Workfront Fusion, aparecerá un mensaje en el gancho web personalizado que dice: **Determinado correctamente**.

   ![WF Fusion](./images/wffusion227.png)

1. Seleccione **Guardar** y luego **Ejecutar una vez**. Tu escenario ahora estará activo, pero no se ejecutará hasta que vuelvas a seleccionar **Enviar** en Postman.

   ![WF Fusion](./images/wffusion230.png)

1. En Postman, vuelva a seleccionar **Enviar**.

   ![WF Fusion](./images/wffusion228.png)

   Su escenario se volverá a ejecutar y creará los dos archivos igual que antes.

   ![WF Fusion](./images/wffusion232.png)

1. Cambie el nombre de su solicitud de Postman a `POST - Send Request to Workfront Fusion Webhook`.

   ![WF Fusion](./images/wffusion233.png)

   Ahora necesita empezar a usar la variable **psdTemplate**. En lugar de codificar la ubicación del archivo de entrada en el nodo **Texto de cambio de Photoshop**, utilizará la variable entrante de la solicitud de Postman.

1. Abra el nodo **Photoshop Change Text** y vaya a **Solicitar contenido**. Seleccione el nombre de archivo codificado **citisignal-fiber.psd** en **input** y elimínelo.

   ![WF Fusion](./images/wffusion234.png)

1. Seleccione la variable **psdTemplate**. Seleccione **Aceptar** y, a continuación, guarde su escenario.

   ![WF Fusion](./images/wffusion235.png)

1. Seleccione **ON** para activar su escenario. Su escenario se está ejecutando sin interrupciones.

   ![WF Fusion](./images/wffusion236.png)

1. De nuevo en Postman, ingrese el nombre de archivo `citisignal-fiber.psd` como valor para la variable **psdTemplate** y seleccione **Send** nuevamente para ejecutar su escenario nuevamente.

   ![WF Fusion](./images/wffusion237.png)

   Al especificar la plantilla del PSD como una variable proporcionada por un sistema externo, ahora ha creado un escenario reutilizable.

   Ahora ha completado este ejercicio.

## Pasos siguientes

Vaya a [Resumen y ventajas de la automatización de servicios de Firefly](./summary.md){target="_blank"}

Volver a [Automatizar servicios de Adobe Firefly](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
