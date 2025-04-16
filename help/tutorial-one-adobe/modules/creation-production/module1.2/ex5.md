---
title: Frame.io y Workfront Fusion
description: Frame.io y Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 37de6ceb-833e-4e75-9201-88bddd38a817
source-git-commit: 003c0ff26183acbafbe745276bde6f90d5adef34
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 0%

---

# 1.2.5 Frame.io y Workfront Fusion

En el ejercicio anterior configuró el escenario `--aepUserLdap-- - Firefly + Photoshop` y configuró un webhook entrante para almacenar en déclencheur el escenario, así como una respuesta de webhook cuando el escenario se haya completado correctamente. A continuación, utilizó Postman para desencadenar ese escenario. Postman es un gran herramienta para realizar pruebas, pero en un escenario empresarial real, los usuarios empresariales no usarían Postman para activar un escenario. En su lugar, utilizarían otro aplicación y esperarían que ese otro aplicación activara un escenario en Workfront Fusion. En este ejercicio, eso es exactamente lo que harás con Frame.io.

>[!NOTE]
>
>Para completar correctamente este ejercicio, debe ser un usuario administrador en su cuenta de Frame.io. El siguiente ejercicio se creó para Frame.io V3 y se actualizará en una fase posterior para Frame.io V4.

## 1.2.5.1 accediendo a Frame.io

Vaya a [https://app.frame.io/projects](https://app.frame.io/projects).

Haga clic en el icono **+** para crear su propio proyecto en Frame.io.

![E/S de cuadro](./images/frame1.png)

Escriba el nombre `--aepUserLdap--` y haga clic en **Crear proyecto**.

![E/S de cuadro](./images/frame2.png)

A continuación, verá el proyecto en el menú de la izquierda.
En uno de los ejercicios anteriores, descargó [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} en su escritorio. Seleccione ese archivo y, a continuación, arrástrelo y suéltelo en la carpeta del proyecto que acaba de crear.

![E/S de cuadro](./images/frame3.png)

## 1.2.5.2 Workfront Fusion y Frame.io

En el ejercicio anterior, creaste el escenario `--aepUserLdap-- - Firefly + Photoshop`, que comenzó con un webhook personalizado y que terminó con una respuesta de webhook. El uso de los webhooks se probó usando Postman, pero obviamente, el objetivo de tal escenario es ser llamado por un aplicación externo. Como se indicó anteriormente, Frame.io será ese ejercicio, pero entre Frame.io y el `--aepUserLdap-- - Firefly + Photoshop` otro escenario de Workfront Fusion es necesario. Ahora configurará ese escenario.

En el menú de la izquierda, vaya a **Escenarios** y seleccione la carpeta `--aepUserLdap--`. Haga clic en **Crear un nuevo escenario**.

![E/S de cuadro](./images/frame4.png)

Utilice el nombre `--aepUserLdap-- - Frame IO Custom Action`.

![Fotograma IO](./images/frame5.png)

Haga clic en el objeto **de signo de** interrogación en el lienzo. Introduzca el texto `webhook` en el cuadro búsqueda y haga clic en **Webhooks**.

![Fotograma IO](./images/frame6.png)

Haga clic en **Webhook** personalizado.

![E/S de cuadro](./images/frame7.png)

Haga clic en **Agregar** para crear una nueva URL de enlace web.

![E/S de cuadro](./images/frame8.png)

Para el **nombre del webhook**, use `--aepUserLdap-- - Frame IO Custom Action Webhook`. Haga clic en **Guardar**.

![E/S de cuadro](./images/frame9.png)

Entonces debería ver esto. Deje esta pantalla abierta y sin tocar, ya que la necesitará en un paso siguiente. En un paso siguiente, tendrás que copiar la URL del webhook, haciendo clic en **Copiar dirección al portapapeles**.

![E/S de cuadro](./images/frame10.png)

Vaya a [https://developer.frame.io/](https://developer.frame.io/). Haga clic en **HERRAMIENTAS PARA DESARROLLADORES** y, a continuación, elija **Acciones personalizadas**.

![E/S de cuadro](./images/frame11.png)

Haga clic en **Crear una acción personalizada**.

![E/S de cuadro](./images/frame12.png)

Introduzca los siguientes valores:

- **NOMBRE**: use `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **DESCRIPCIÓN**: use `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **EVENTO**: use `fusion.tutorial`.
- **URL**: introduzca la URL del webhook que acaba de crear en Workfront Fusion
- **EQUIPO**: seleccione el equipo Frame.io apropiado, en este caso **Un tutorial de Adobe**.

Haga clic en **Enviar**.

![E/S de cuadro](./images/frame15.png)

Entonces debería ver esto.

![E/S de cuadro](./images/frame14.png)

Volver a [https://app.frame.io/projects](https://app.frame.io/projects). Actualice la página.

![E/S de cuadro](./images/frame16.png)

Después de haber actualizado la página, haga clic en los 3 puntos **...** del recurso **citisignal-fiber.psd**. A continuación, debería ver la acción personalizada que creó anteriormente en el menú que se muestra. Haga clic en la acción personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion`.

![Fotograma IO](./images/frame17.png)

¡Entonces deberías ver un éxito similar **!** ventana emergente. Esta ventana emergente es el resultado de la comunicación entre Frame.io y Workfront Fusion.

![E/S de cuadro](./images/frame18.png)

Vuelva a cambiar la pantalla a Workfront Fusion. Ahora debería ver **Determinado correctamente** en el objeto Webhook personalizado. Haga clic en **Aceptar**.

![E/S de cuadro](./images/frame19.png)

Haga clic en **Ejecutar una vez** para habilitar el modo de prueba y vuelva a probar la comunicación con Frame.io.

![E/S de cuadro](./images/frame20.png)

Vuelva a Frame.io y haga clic en la acción `--aepUserLdap-- - Frame IO Custom Action Fusion` personalizada nuevamente.

![Fotograma IO](./images/frame21.png)

Cambie la pantalla a Workfront Fusion. Ahora debería ver una marca de verificación verde y una burbuja que muestre **1**. Haga clic en la burbuja para ver los detalles.

![E/S de cuadro](./images/frame22.png)

La vista detallada de la burbuja muestra los datos recibidos de Frame.io. Debe ver varios ID de. Por ejemplo, el campo **resource.id** muestra el ID único en Frame.io del recurso **citisignal-fiber.psd**

![E/S de cuadro](./images/frame23.png)

Ahora que se ha establecido la comunicación entre Frame.io y Workfront Fusion, puede continuar con la configuración.

## 1.2.5.3 que proporciona una respuesta de formulario personalizada a Frame.io

Cuando se invoca la acción personalizada en Frame.io, Frame.io espera recibir una respuesta de Workfront Fusion. Si piensa en el escenario que creó en el ejercicio anterior, se requieren varias variables para actualizar el archivo PSD estándar de Photoshop. Estas variables se definen en la carga útil utilizada:

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Así que para que el escenario `--aepUserLdap-- - Firefly + Photoshop` se ejecute correctamente, se necesitan campos como **prompt**, **cta**, **button** y **psdTemplate**.

Los tres primeros campos, **prompt**, **cta**, **button**, requieren la entrada del usuario que debe recopilarse en Frame.io cuando el usuario invoca la acción personalizada. Por lo tanto, lo primero que hay que hacer dentro de Workfront Fusion es comprobar si estas variables están disponibles o no y, de lo contrario, Workfront Fusion debe responder a Frame.io solicitando que se introduzcan esas variables. La forma de lograrlo es mediante el uso de un formulario en Frame.io.

Vuelva a Workfront Fusion y abra su escenario `--aepUserLdap-- - Frame IO Custom Action`. Pase el ratón sobre el **objeto Webhook** personalizado y haga clic en el **icono +** para añadir otro módulo.

![E/S de cuadro](./images/frame24.png)

Busque `Flow Control` y haga clic en **Control de flujo**.

![E/S de cuadro](./images/frame25.png)

Haga clic para seleccionar **Router**.

![Fotograma IO](./images/frame26.png)

Entonces deberías ver esto.

![Fotograma IO](./images/frame27.png)

Haga clic en el botón **?** y, a continuación, haga clic para seleccionar **Webhooks**.

![E/S de cuadro](./images/frame28.png)

Seleccione **Respuesta de webhook**.

![E/S de cuadro](./images/frame29.png)

Entonces debería ver esto.

![E/S de cuadro](./images/frame30.png)

Copie el siguiente código JSON y péguelo en el campo **Cuerpo**.


```json
{
  "title": "What do you want Firefly to generate?",
  "description": "Enter your Firefly prompt.",
  "fields": [
    {
      "type": "text",
      "label": "Prompt",
      "name": "Prompt",
      "value": ""
    },
    {
      "type": "text",
      "label": "CTA Text",
      "name": "CTA Text",
      "value": ""
    },
    {
      "type": "text",
      "label": "Button Text",
      "name": "Button Text",
      "value": ""
    }
  ]
}
```

Haga clic en el icono para limpiar y embellecer el código JSON. A continuación, haga clic en **Aceptar**.

![E/S de cuadro](./images/frame31.png)

Haga clic en **Guardar** para guardar los cambios.

![E/S de cuadro](./images/frame32.png)

A continuación, debe configurar un filtro para asegurarse de que esta ruta del escenario solo se ejecute cuando no haya ninguna solicitud disponible. Haz clic en el icono **llave inglesa** y, a continuación, selecciona **Configurar un filtro**.

![E/S de cuadro](./images/frame33.png)

Configure los campos siguientes:

- **Etiqueta**: use `Prompt isn't available`.
- **Condición**: use `{{1.data.Prompt}}`.
- **Operadores básicos**: seleccione **No existe**.

>[!NOTE]
>
>Las variables de Workfront Fusion se pueden especificar manualmente con esta sintaxis: `{{1.data.Prompt}}`. El número de la variable hace referencia al módulo en el escenario. En este ejemplo, puede ver que el primer módulo del escenario se llama **Webhooks** y tiene un número de secuencia de **1**. Esto significa que la variable `{{1.data.Prompt}}` tendrá acceso al campo **data.Prompt** desde el módulo con el número de secuencia 1. Los números de secuencia a veces pueden ser diferentes, por lo que debe prestar atención al copiar/pegar estas variables y comprobar siempre que el número de secuencia utilizado sea el correcto.

Haga clic en **Aceptar**.

![E/S de cuadro](./images/frame34.png)

Entonces debería ver esto. Primero haz clic en el icono **Guardar** y luego haz clic en **Ejecutar una vez** para probar el escenario.

![E/S de cuadro](./images/frame35.png)

Entonces debería ver esto.

![E/S de cuadro](./images/frame36.png)

Vuelva a Frame.io y haga clic en la acción personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion` en el recurso **citisignal-fiber.psd** de nuevo.

![Fotograma IO](./images/frame37.png)

Ahora debería ver un mensaje dentro de Frame.io. No rellene los campos aún y no envíe el formulario aún. Este mensaje se muestra en función de la respuesta de Workfront Fusion que acaba de configurar.

![E/S de cuadro](./images/frame38.png)

Vuelva a Workfront Fusion y haga clic en la burbuja del módulo **Respuesta de webhook**. Verá que en **OUTPUT**, verá el cuerpo que contiene la carga útil JSON para el formulario. Haga clic en **Ejecutar una vez** de nuevo.

![E/S de cuadro](./images/frame40.png)

Entonces deberías ver esto de nuevo.

![Fotograma IO](./images/frame41.png)

Vuelva a Frame.io y rellene los campos como se indica. Haga clic en **Enviar**.

![E/S de cuadro](./images/frame39.png)

¡Debería ver un **de éxito!** elemento emergente.

![E/S de cuadro](./images/frame42.png)

Vuelva a Workfront Fusion y haga clic en la burbuja del módulo **Gancho web personalizado**. En la operación 1, en **OUTPUT**, ahora puede ver un nuevo objeto **data** que contiene campos como **Button Text**, **CTA Text** y **Prompt**. Con estas variables de entrada de usuario disponibles en su escenario, tiene suficiente para continuar con la configuración.

![E/S de cuadro](./images/frame43.png)

## 1.2.5.4 Recuperar ubicación de archivo de Frame.io

Como se mencionó anteriormente, se necesitan campos como **prompt**, **cta**, **button** y **psdTemplate** para que este escenario funcione. Los primeros 3 campos ya están disponibles, pero falta la **psdTemplate** que se va a usar. **psdTemplate** hará referencia a una ubicación Frame.io, ya que el archivo **citisignal-fiber.psd** está hospedado en Frame.io. Para recuperar la ubicación de ese archivo, debe configurar y utilizar la conexión Frame.io en Workfront Fusion.

Vuelva a Workfront Fusion y abra su escenario `--aepUserLdap-- - Frame IO Custom Action`. ¿Desea pasar el ratón sobre **?** módulo, haga clic en el **icono +** para añadir otro módulo y búsqueda para `frame`. Haga clic en **Frame.io**.

![Fotograma IO](./images/frame44.png)

Haga clic en **Frame.io (heredado)**.

![E/S de cuadro](./images/frame45.png)

Haga clic en **Obtener un recurso**.

![Fotograma IO](./images/frame46.png)

Para utilizar la conexión Frame.io, primero debe configurarla. Haga clic en **Agregar** para hacerlo.

![E/S de cuadro](./images/frame47.png)

Abra la lista desplegable **Tipo de conexión**.

![E/S de cuadro](./images/frame48.png)

Seleccione la clave de API **Frame.io** y escriba el nombre `--aepUserLdap-- - Frame.io Token`.

![E/S de cuadro](./images/frame49.png)

Para obtener un token de API, ve a [https://developer.frame.io/](https://developer.frame.io/). Haga clic en **HERRAMIENTAS PARA DESARROLLADORES** y luego elija **Tokens**.

![E/S de cuadro](./images/frame50.png)

Haga clic en **Crear un token**.

![E/S de cuadro](./images/frame51.png)

Use la **descripción** `--aepUserLdap-- - Frame.io Token` y haga clic en **Seleccionar todos los ámbitos**.

![E/S de cuadro](./images/frame52.png)

Desplácese hacia abajo y haga clic en **Enviar**.

![E/S de cuadro](./images/frame53.png)

Se ha creado el token. Haga clic en **Copiar** para copiarlo en el portapapeles.

![E/S de cuadro](./images/frame54.png)

Vuelva a su escenario en Workfront Fusion. Pegue el token en el campo **Su clave de API Frame.io**. Haga clic en **OK**. Workfront Fusion probará su conexión a partir de ahora.

![E/S de cuadro](./images/frame55.png)

Si la conexión se probó correctamente, aparecerá automáticamente en **Conexión**. Ahora tiene una conexión correcta y debe finalizar la configuración para obtener todos los detalles del recurso de Frame.io, incluida la ubicación del archivo. Para ello, debe proporcionar **Asset ID**.

![E/S de cuadro](./images/frame56.png)

Frame.io comparte el **ID de recurso** con Workfront Fusion como parte de la comunicación inicial de **gancho web personalizado**. Se puede encontrar en el campo **resource.id**. Seleccione **resource.id** y haga clic en **Aceptar**.

![E/S de cuadro](./images/frame57.png)

Ahora debería ver esto. Guarde los cambios y haga clic en **Ejecutar una vez** para probar el escenario.

![E/S de cuadro](./images/frame58.png)

Vuelva a Frame.io y haga clic en la acción personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion` en el recurso **citisignal-fiber.psd** de nuevo.

![E/S de cuadro](./images/frame37.png)

Ahora debería ver un mensaje dentro de Frame.io. No rellene los campos aún y no envíe el formulario aún. Este mensaje se muestra en función de la respuesta de Workfront Fusion que acaba de configurar.

![Fotograma IO](./images/frame38.png)

Cambie a Workfront Fusion. Haga clic en **Ejecutar una vez** más.

![E/S de cuadro](./images/frame59.png)

Vuelva a Frame.io y rellene los campos como se indica. Haga clic en **Enviar**.

![E/S de cuadro](./images/frame39.png)

Vuelva a Workfront Fusion y haga clic en la burbuja del módulo **Frame.io: obtenga un recurso**.

![E/S de cuadro](./images/frame60.png)

Ahora puede ver muchas metadatos sobre el recurso **específico citisignal-fiber.psd**.

![Fotograma IO](./images/frame61.png)

La información específica necesaria para este caso de uso es la dirección URL de ubicación del archivo **citisignal-fiber.psd**, que puede encontrar desplazándose hacia abajo hasta el campo **Original**.

![E/S de cuadro](./images/frame62.png)

Ahora tiene disponibles todos los campos (**prompt**, **cta**, **button** y **psdTemplate**) necesarios para que este escenario funcione.

## 1.2.5.5 Invocar escenario de Workfront

En el ejercicio anterior configuró el escenario `--aepUserLdap-- - Firefly + Photoshop`. Ahora debe realizar un cambio menor en ese escenario.

Abra el escenario `--aepUserLdap-- - Firefly + Photoshop` en otra pestaña y haga clic en el primer módulo **Adobe Photoshop - Aplicar ediciones de PSD**. Ahora debería ver que el archivo de entrada está configurado para utilizar una ubicación dinámica en Microsoft Azure. Dado que, para este caso de uso, el archivo de entrada ya no se almacena en Microsoft Azure, sino que utiliza el almacenamiento Frame.io, debe cambiar esta configuración.

![E/S de cuadro](./images/frame63.png)

Cambie **Storage** a **External** y cambie **File location** para usar únicamente la variable **psdTemplate** que se toma del módulo **Custom Webhook** entrante. Haga clic en **Aceptar** y, a continuación, haga clic en **Guardar** para guardar los cambios.

![E/S de cuadro](./images/frame64.png)

Haga clic en el módulo **Gancho web personalizado** y, a continuación, haga clic en **Copiar dirección al portapapeles**. Debe copiar la dirección URL, ya que deberá utilizarla en el otro escenario.

![E/S de cuadro](./images/frame65.png)

Vuelva a su escenario `--aepUserLdap-- - Frame IO Custom Action`. Pase el ratón sobre el módulo **Frame.io - Obtener un recurso** y haga clic en el icono **+**.

![E/S de cuadro](./images/frame66.png)

Escriba `http` y haga clic en **HTTP**.

![E/S de cuadro](./images/frame67.png)

Seleccione **Realizar una solicitud**.

![E/S de cuadro](./images/frame68.png)

Pegue la dirección URL del webhook personalizado en el campo **URL**. Establezca el **Método** en POST**.

![E/S de cuadro](./images/frame69.png)

Establezca **Body type** en **Raw** y **Content type** en **JSON (application/json)**.
Pegue la siguiente carga útil JSON en el campo **Solicitar contenido** y active la casilla de verificación para **Analizar respuesta**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Ahora tiene una carga útil estática configurada, pero debe volverse dinámica mediante las variables recopiladas anteriormente.

![E/S de cuadro](./images/frame70.png)

Para el campo **psdTemplate**, reemplace la variable estática **citisignal-fiber.psd** por la variable **Original**.

![E/S de cuadro](./images/frame71.png)

Para los campos **prompt**, **cta** y **button**, reemplace las variables estáticas por las variables dinámicas que se insertaron en el escenario mediante la solicitud entrante de webhook desde Frame.io, que son los campos **data.Prompt**, **data.CTA Text** y **data.Button Text**.

Haga clic en **Aceptar**.

![E/S de cuadro](./images/frame72.png)

Haga clic en **Guardar** para guardar los cambios.

![E/S de cuadro](./images/frame73.png)

## 1.2.5.6 Guardar nuevo recurso en Frame.io

Una vez que se haya invocado el otro escenario de Workfront Fusion, el resultado será una nueva plantilla de Photoshop PSD disponible. Ese archivo PSD debe almacenarse de nuevo en Frame.io, que es el último paso en este escenario.

Pase el ratón sobre el módulo **HTTP - Make a request** y haga clic en el icono **+**.

![E/S de cuadro](./images/frame74.png)

Seleccione **Frame.io (heredado)**.

![E/S de cuadro](./images/frame75.png)

Seleccione **Crear un recurso**.

![E/S de cuadro](./images/frame76.png)

La conexión de Frame.io se seleccionará automáticamente.

![E/S de cuadro](./images/frame77.png)

Seleccione las siguientes opciones:

- **Id. de equipo**: seleccione el Id. de equipo apropiado, en este caso `One Adobe Tutorial`.
- **Id. de proyecto**: use `--aepUserLdap--`.
- **Id. de carpeta**: use `root`.
- **Tipo**: use `File`.

![E/S de cuadro](./images/frame78.png)

Para el nombre del campo ****, puede utilizar un variable como **timestamp** (o cambiarlo por algo que tenga más sentido para usted). Puede encontrar la marca **de tiempo variable** predefinida en el **pestaña Fecha y hora**.

![Fotograma IO](./images/frame79.png)

Para el campo **Origen URL**, utilice el siguiente código JSON.

```json
{{6.data.newPsdTemplate}}
```

>[!NOTE]
>
>Las variables de Workfront Fusion se pueden especificar manualmente con esta sintaxis: `{{6.data.newPsdTemplate}}`. El número de la variable hace referencia al módulo en el escenario. En este ejemplo, puede ver que el sexto módulo del escenario se llama **HTTP - Realizar una solicitud** y tiene un número de secuencia de **6**. Esto significa que la variable `{{6.data.newPsdTemplate}}` tendrá acceso al campo **data.newPsdTemplate** desde el módulo con el número de secuencia 6. Los números de secuencia a veces pueden ser diferentes, por lo que debe prestar atención al copiar/pegar estas variables y comprobar siempre que el número de secuencia utilizado sea el correcto.

Haga clic en **Aceptar**.

![Fotograma IO](./images/frame80.png)

Haga clic en **Guardar** para guardar los cambios.

![E/S de cuadro](./images/frame81.png)

Por último, debe configurar un filtro para asegurarse de que esta ruta del escenario solo se ejecute cuando haya una solicitud disponible. Haz clic en el icono **llave inglesa** y, a continuación, selecciona **Configurar un filtro**.

![E/S de cuadro](./images/frame82.png)

Configure los campos siguientes:

- **Etiqueta**: use `Prompt is available`.
- **Condición**: use `{{1.data.Prompt}}`.
- **Operadores básicos**: seleccione **existe**.

>[!NOTE]
>
>Las variables de Workfront Fusion se pueden especificar manualmente con esta sintaxis: `{{1.data.Prompt}}`. El número de la variable hace referencia al módulo en el escenario. En este ejemplo, puede ver que el primer módulo del escenario se llama **Webhooks** y tiene un número de secuencia de **1**. Esto significa que la variable `{{1.data.Prompt}}` tendrá acceso al campo **data.Prompt** desde el módulo con el número de secuencia 1. Los números de secuencia a veces pueden ser diferentes, por lo que debe prestar atención al copiar/pegar estas variables y comprobar siempre que el número de secuencia utilizado sea el correcto.

Haga clic en **Aceptar**.

![E/S de cuadro](./images/frame83.png)

Haga clic en **Guardar** para guardar los cambios.

![E/S de cuadro](./images/frame84.png)

## 1.2.5.7: pruebe su caso de uso de extremo a extremo

Haga clic en **Ejecutar una vez** en su escenario `--aepUserLdap-- - Frame IO Custom Action`.

![E/S de cuadro](./images/frame85.png)

Vuelva a Frame.io y haga clic en la acción personalizada `--aepUserLdap-- - Frame IO Custom Action Fusion` en el recurso **citisignal-fiber.psd** de nuevo.

![E/S de cuadro](./images/frame37.png)

Ahora debería ver un mensaje dentro de Frame.io. No rellene los campos aún y no envíe el formulario aún. Este mensaje se muestra a partir de la respuesta de Workfront Fusion que acaba de configurar.

![E/S de cuadro](./images/frame38.png)

Cambie a Workfront Fusion. Haga clic en **Ejecutar una vez** en su escenario `--aepUserLdap-- - Frame IO Custom Action`.

![E/S de cuadro](./images/frame86.png)

En Workfront Fusion, abra el escenario `--aepUserLdap-- - Firefly + Photoshop` y haga clic en **Ejecutar una vez** en ese escenario.

![E/S de cuadro](./images/frame87.png)

Vuelva a Frame.io y rellene los campos como se indica. Haga clic en **Enviar**.

![E/S de cuadro](./images/frame39.png)

Después de 1-2 minutos, debería ver un nuevo recurso que aparece automáticamente en Frame.io. Haga doble clic en el nuevo recurso para abrirlo.

![E/S de cuadro](./images/frame88.png)

Ahora puede ver claramente que todas las variables de entrada del usuario se han aplicado automáticamente.

![E/S de cuadro](./images/frame89.png)

Ahora ha completado correctamente este ejercicio.

## Pasos siguientes

Ir a [1.2.6 Frame.io para Fusion para AEM Assets](./ex6.md){target="_blank"}

Volver a [Automatización del flujo de trabajo de Creative con Workfront Fusion](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}

