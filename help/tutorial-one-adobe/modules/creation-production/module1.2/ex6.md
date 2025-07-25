---
title: Frame I/O to Workfront Fusion to AEM Assets
description: Frame I/O to Workfront Fusion to AEM Assets
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: f02ecbe4-f1d7-4907-9bbc-04e037546091
source-git-commit: 1d1ee3462bd890556037c8e24ba2fe94c3423187
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---

# 1.2.6 E/S de cuadro a Workfront Fusion para AEM Assets

>[!IMPORTANT]
>
>Para completar este ejercicio, debe tener acceso a un entorno de trabajo de AEM Assets y autores de CS. Si sigue el ejercicio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}, tendrá acceso a dicho entorno.

>[!IMPORTANT]
>
>Si ha configurado anteriormente un programa de AEM Assets CS con un entorno de creación, es posible que la zona protegida de AEM CS esté en hibernación. Dado que la dehibernación de una zona protegida de este tipo tarda de 10 a 15 minutos, sería aconsejable iniciar el proceso de dehibernación ahora para no quedarse atascado más adelante.

En el ejercicio anterior configuró un escenario que genera automáticamente variaciones de un archivo PSD de Adobe Photoshop utilizando Adobe Firefly, las API de Photoshop y Workfront Fusion. El resultado de ese escenario fue un nuevo archivo PSD de Photoshop.

Los equipos empresariales, sin embargo, no necesitan un archivo PSD, sino un archivo PNG o un archivo JPG. En este ejercicio, configurará una nueva automatización que dará como resultado la generación de un archivo PNG una vez aprobado el recurso en E/S de fotograma y que el archivo PNG se almacenará automáticamente en AEM Assets.

## 1.2.6.1 Crear un nuevo escenario

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

En el menú de la izquierda, vaya a **Escenarios** y seleccione la carpeta `--aepUserLdap--`. Haga clic en **Crear un nuevo escenario**.

![E/S de cuadro](./images/aemf1.png)

Use el nombre `--aepUserLdap-- - Asset Approved PNG AEM Assets`. A continuación, haga clic en **?Módulo**, escriba el término de búsqueda `webhook` y haga clic en **Webhooks**.

![E/S de cuadro](./images/aemf2.png)

Haga clic en **webhook personalizado**.

![E/S de cuadro](./images/aemf3.png)

Haga clic en **Agregar** para crear un nuevo enlace web.

![E/S de cuadro](./images/aemf4.png)

Use el nombre `--aepUserLdap-- - Frame.io Webhook`. Haga clic en **Guardar**.

![E/S de cuadro](./images/aemf5.png)

Entonces debería ver esto. Haga clic en **Copiar dirección al portapapeles**.

![E/S de cuadro](./images/aemf6.png)

## 1.2.6.2 Configurar webhook en Frame.io

Vaya a Postman y abra la solicitud **POST - Obtener token de acceso** en la colección **Adobe IO - OAuth**. A continuación, haga clic en **Enviar** para solicitar un nuevo **token de acceso**.

![E/S de cuadro](./images/frameV4api2.png)

En el menú de la izquierda, vuelva a **Colecciones**. Abra la solicitud **POST - Crear webhook** en la colección **Frame.io V4 - Tech Insiders**, en la carpeta **Webhooks**.

Vaya a **Cuerpo** de la solicitud. Cambie el campo **name** a `--aepUserLdap--  - Fusion to AEM Assets` y luego cambie el campo **url** al valor de la URL del webhook que copió de Workfront Fusion.

Haga clic en **Enviar**.

![E/S de cuadro](./images/framewh1.png)

Se ha creado la acción personalizada Frame.io V4.

![E/S de cuadro](./images/framewh2.png)

Vaya a [https://next.frame.io/project](https://next.frame.io/project){target="_blank"} y luego al proyecto que creó anteriormente, que debería llamarse `--aepUserLdap--` y abra la carpeta **CitiSignal Fiber Campaign**. Ahora debería ver los recursos creados en el ejercicio anterior.

![E/S de cuadro](./images/aemf11a.png)

Haga clic en el campo **Estado** y cambie el estado a **En curso**.

![E/S de cuadro](./images/aemf12.png)

Cambie a Workfront Fusion. Ahora debería ver que la conexión se ha **determinado correctamente**.

![E/S de cuadro](./images/aemf13.png)

Haga clic en **Guardar** para guardar los cambios y, a continuación, haga clic en **Ejecutar una vez** para realizar una prueba rápida.

![E/S de cuadro](./images/aemf14.png)

Cambie a Frame.io, haga clic en el campo **En curso** y cambie el estado a **Necesita revisión**.

![E/S de cuadro](./images/aemf15.png)

Vuelva a Workfront Fusion y haga clic en la burbuja del módulo **Gancho web personalizado**.

La vista detallada de la burbuja muestra los datos recibidos de Frame.io. Debe ver varios ID de. Por ejemplo, el campo **resource.id** muestra el ID único en Frame.io del recurso **citisignal-fiber.psd**.

![E/S de cuadro](./images/aemf16.png)

## 1.2.6.3: obtener detalles de recursos de Frame.io

Ahora que la comunicación entre Frame.io y Workfront Fusion se ha establecido a través de un webhook personalizado, debería obtener más detalles sobre el recurso para el que se actualizó la etiqueta de estado. Para ello, utilizará una vez más el conector Frame.io en Workfront Fusion, de forma similar al ejercicio anterior.

Pase el ratón sobre el objeto **webhook personalizado** y haga clic en el icono **+** para agregar otro módulo.

![E/S de cuadro](./images/aemf18a.png)

Escriba el término de búsqueda `frame`. Haga clic en **Frame.io**.

![E/S de cuadro](./images/aemf18.png)

Haga clic en **Frame.io**.

![E/S de cuadro](./images/aemf19.png)

Haga clic en **Realizar una llamada de API personalizada**.

![E/S de cuadro](./images/aemf20.png)

Compruebe que la conexión está establecida en la misma conexión que creó en el ejercicio anterior, que debe llamarse `--aepUserLdap-- - Adobe I/O - Frame.io S2S`.

![E/S de cuadro](./images/aemf21.png)

Para la configuración del módulo **Frame.io: realice una llamada de API personalizada**, use la dirección URL: `/v4/accounts/{{1.account.id}}/files/{{1.resource.id}}`.

>[!NOTE]
>
>Las variables de Workfront Fusion se pueden especificar manualmente con esta sintaxis: `{{1.account.id}}` y `{{1.resource.id}}`. El número de la variable hace referencia al módulo en el escenario. En este ejemplo, puede ver que el primer módulo del escenario se llama **Webhooks** y tiene un número de secuencia de **1**. Esto significa que las variables `{{1.account.id}}` y `{{1.resource.id}}` tendrán acceso a ese campo desde el módulo con el número de secuencia 1. Los números de secuencia a veces pueden ser diferentes, por lo que debe prestar atención al copiar/pegar estas variables y comprobar siempre que el número de secuencia utilizado sea el correcto.

A continuación, haga clic en **+ Agregar elemento** en **Cadena de consulta**.

![E/S de cuadro](./images/aemf21a.png)

Escriba estos valores y haga clic en **Agregar**.

| Clave | Valor |
|:-------------:| :---------------:| 
| `include` | `media_links.original` |

![E/S de cuadro](./images/aemf21b.png)

Ahora debería tener esto. Haga clic en **Aceptar**.

![E/S de cuadro](./images/aemf22.png)

Haga clic en **Guardar** para guardar los cambios y, a continuación, haga clic en **Ejecutar una vez** para probar la configuración.

![E/S de cuadro](./images/aemf23.png)

Vuelva a Frame.io y cambie el estado a **En curso**.

![E/S de cuadro](./images/aemf24.png)

Vuelva a Workfront Fusion y haga clic en la burbuja del módulo **Frame.io: realice una llamada de API personalizada**. Debería ver una descripción general similar.

![E/S de cuadro](./images/aemf25.png)

A continuación, debe configurar un filtro para asegurarse de que solo se procese un archivo PNG en el caso de los recursos que tengan un estado **Aprobado**. Para ello, haga clic en el icono **Llave inglesa** entre los módulos **Gancho web personalizado** y **Frame.io: realice una llamada API personalizada** y, a continuación, seleccione **Configurar un filtro**.

![E/S de cuadro](./images/aemf25a.png)

Configure los campos siguientes:

- **Etiqueta**: use `Status = Approved`.
- **Condición**: `{{1.metadata.value[]}}`.
- **Operadores básicos**: seleccione **Igual a**.
- **Valor**: `Approved`.

Haga clic en **Aceptar**.

![E/S de cuadro](./images/aemf35.png)

Entonces deberías tener esto. Haga clic en **Guardar** para guardar los cambios.

![E/S de cuadro](./images/aemf35a.png)

## 1.2.6.4 convertir a PNG

Pase el ratón sobre el módulo **Frame.io - Realizar una llamada de API personalizada** y haga clic en el icono **+**.

![E/S de cuadro](./images/aemf27.png)

Escriba el término de búsqueda `photoshop` y haga clic en **Adobe Photoshop**.

![E/S de cuadro](./images/aemf28.png)

Haga clic en **Convertir formato de imagen**.

![E/S de cuadro](./images/aemf29.png)

Compruebe que el campo **Conexión** está usando la conexión creada anteriormente, que se llama `--aepUserLdap-- - Adobe IO`.

En **Entrada**, establezca el campo **Almacenamiento** en **Externo** y la **Ubicación de archivo** para usar la variable **Original** que devuelve el módulo **Frame.io: realice una llamada de API personalizada**.

A continuación, haga clic en **Agregar elemento** en **Salidas**.

![E/S de cuadro](./images/aemf30.png)

Para la configuración de **Output**, establezca el campo **Storage** en **Fusion internal storage** y el **Type** en **image/png**. Haga clic en **Agregar**.

![E/S de cuadro](./images/aemf31.png)

Haga clic en **Aceptar**.

![E/S de cuadro](./images/aemf33.png)

Haga clic en **Guardar** para guardar los cambios y, a continuación, haga clic en **Ejecutar una vez** para probar la configuración.

![E/S de cuadro](./images/aemf32.png)

Vuelva a Frame.io, haga clic en el campo **En curso** y cambie el estado a **Aprobado**.

![E/S de cuadro](./images/aemf37.png)

Vuelva a Workfront Fusion. Ahora debería ver que todos los módulos de su escenario se han ejecutado correctamente. Haga clic en la burbuja en el módulo **Adobe Photoshop - Convertir formato de imagen**.

![E/S de cuadro](./images/aemf38.png)

En los detalles de la ejecución del módulo **Adobe Photoshop - Convert image format**, puede ver que ahora se generó un archivo PNG. El siguiente paso es almacenar ese archivo en AEM Assets CS.

![E/S de cuadro](./images/aemf39.png)

## 1.2.6.5 Almacenar PNG en AEM Assets CS

Pase el ratón sobre el módulo **Adobe Photoshop - Convertir formato de imagen** y haga clic en el icono **+**.

![E/S de cuadro](./images/aemf40.png)

Escriba el término de búsqueda `aem` y seleccione **AEM Assets**.

![E/S de cuadro](./images/aemf41.png)

Haga clic en **Cargar un recurso**.

![E/S de cuadro](./images/aemf42.png)

Ahora debe configurar la conexión con AEM Assets CS. Haga clic en **Agregar**.

![E/S de cuadro](./images/aemf43.png)

Utilice la siguiente configuración:

- **Tipo de conexión**: **AEM Assets as a Cloud Service**.
- **Nombre de conexión**: `--aepUserLdap-- AEM Assets CS`.
- **URL de instancia**: copie la URL de instancia del entorno de autor de AEM Assets CS, que debería tener el aspecto siguiente: `https://author-pXXXXX-eXXXXXXX.adobeaemcloud.com`.
- **Opciones de relleno de detalles de acceso**: seleccione **Proporcionar JSON**.

Ahora necesita proporcionar las **credenciales de la cuenta técnica en formato JSON**. Para ello, hay que seguir una serie de pasos a seguir mediante AEM Cloud Manager. Mientras lo hace, mantenga esta pantalla abierta.

![E/S de cuadro](./images/aemf44.png)

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. La organización que debe seleccionar es `--aepImsOrgName--`. Entonces verás algo como esto. Haga clic para abrir el programa, que debe tener el nombre `--aepUserLdap-- - Citi Signal`.

![E/S de cuadro](./images/aemf45.png)

Haga clic en los 3 puntos **...** y seleccione **Developer Console**.

![E/S de cuadro](./images/aemf46.png)

Haga clic en **Iniciar sesión con Adobe**.

![E/S de cuadro](./images/aemf47.png)

Vaya a **Herramientas** > **Integraciones**.

![E/S de cuadro](./images/aemf47a.png)

Haga clic en **Crear nueva cuenta técnica**.

![E/S de cuadro](./images/aemf48.png)

Entonces deberías ver algo como esto. Abra la cuenta técnica recién creada. Haga clic en los 3 puntos **...** y, a continuación, seleccione **Ver**.

![E/S de cuadro](./images/aemf48a.png)

Debería ver una carga útil de token de cuenta técnica similar. Copie la carga útil JSON completa en el portapapeles.

![E/S de cuadro](./images/aemf50.png)

Vuelva a Workfront Fusion y pegue la carga útil JSON completa en el campo **Credenciales de cuenta técnica en formato JSON**. Haga clic en **Continuar**.

![E/S de cuadro](./images/aemf49.png)

La conexión se validará y, cuando se realice correctamente, la conexión se seleccionará automáticamente en el módulo AEM Assets. Lo siguiente que hay que hacer es configurar una carpeta. Como parte del ejercicio, debe crear una nueva carpeta dedicada.

![E/S de cuadro](./images/aemf51.png)

Para crear una nueva carpeta dedicada, ve a [https://experience.adobe.com](https://experience.adobe.com/){target="_blank"}. Asegúrese de que esté seleccionada la instancia correcta de Experience Cloud, que debería ser `--aepImsOrgName--`. A continuación, haga clic en **Experience Manager Assets**.

![E/S de cuadro](./images/aemf52.png)

Haga clic en **Seleccionar** en el entorno de AEM Assets CS, que debería llamarse `--aepUserLdap-- - Citi Signal dev`.

![E/S de cuadro](./images/aemf53.png)

Vaya a **Assets** y haga clic en **Crear carpeta**.

![E/S de cuadro](./images/aemf54.png)

Escriba el nombre `--aepUserLdap-- - CitiSignal Fiber Campaign` y haga clic en **Crear**.

![E/S de cuadro](./images/aemf55.png)

A continuación, se crea la carpeta.

![E/S de cuadro](./images/aemf56.png)

Vuelva a Workfront Fusion, seleccione **Haga clic aquí para elegir la carpeta** y, a continuación, elija la carpeta `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![E/S de cuadro](./images/aemf57.png)

Compruebe que el destino esté establecido en `--aepUserLdap-- - CitiSignal Fiber Campaign`. A continuación, en **Archivo Source**, seleccione **Mapa**.

En **Nombre de archivo**, elija la variable `{{3.filenames[1]}}`.

En **Datos**, elija la variable `{{3.files[1]}}`.

>[!NOTE]
>
>Las variables de Workfront Fusion se pueden especificar manualmente con esta sintaxis: `{{3.filenames[1]}}`. El número de la variable hace referencia al módulo en el escenario. En este ejemplo, puede ver que el tercer módulo del escenario se llama **Adobe Photoshop - Convertir formato de imagen** y tiene un número de secuencia de **3**. Esto significa que la variable `{{3.filenames[1]}}` tendrá acceso al campo **filenames[]** desde el módulo con el número de secuencia 3. Los números de secuencia a veces pueden ser diferentes, por lo que debe prestar atención al copiar/pegar estas variables y comprobar siempre que el número de secuencia utilizado sea el correcto.

Haga clic en **Aceptar**.

![E/S de cuadro](./images/aemf58.png)

Haga clic en **Guardar** para guardar los cambios.

![E/S de cuadro](./images/aemf59.png)

A continuación, debe establecer permisos específicos para la cuenta técnica que acaba de crear. Cuando se creó la cuenta en **Developer Console** en **Cloud Manager**, se le otorgaron derechos de acceso de **Lectura**, pero para este caso de uso, se requieren derechos de acceso de **Escritura**. Para ello, vaya al entorno de AEM CS Author.

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. La organización que debe seleccionar es `--aepImsOrgName--`. Haga clic para abrir el programa, que debe tener el nombre `--aepUserLdap-- - Citi Signal`. Entonces verás algo como esto. Haga clic en la URL del autor.

![E/S de cuadro](./images/aemf60.png)

Haga clic en **Iniciar sesión con Adobe**.

![E/S de cuadro](./images/aemf61.png)

Vaya a **Configuración** > **Seguridad** > **Usuarios**.

![E/S de cuadro](./images/aemf62.png)

Haga clic en para abrir la cuenta de usuario de Technical Account.

![E/S de cuadro](./images/aemf63.png)

Vaya a **Grupos** y agregue este usuario de cuenta técnica al grupo **Usuarios DAM**.

![E/S de cuadro](./images/aemf64.png)

Haga clic en **Guardar y cerrar**.

![E/S de cuadro](./images/aemf65.png)

Vuelva a Workfront Fusion. Haga clic en **Ejecutar una vez** para probar el escenario.

![E/S de cuadro](./images/aemf66.png)

Cambie a Frame.io y asegúrese de que el estado del recurso se cambie a **Aprobado** de nuevo.

>[!NOTE]
>
>Es posible que tenga que cambiarlo primero a **En curso** o **Necesita revisión**, para luego volver a cambiarlo a **Aprobado**.

![E/S de cuadro](./images/aemf15.png)

Su escenario de Workfront Fusion se activará y debería completarse correctamente. Al ver la información de la burbuja en el módulo **AEM Assets**, ya puede ver que el archivo PNG se almacenó correctamente en AEM Assets CS.

![E/S de cuadro](./images/aemf67.png)

Vuelva a AEM Assets CS y abra la carpeta `--aepUserLdap-- - Frame.io PNG`. Ahora debería ver el archivo PNG generado como parte del escenario de Workfront Fusion. Haga doble clic para abrir el archivo.

![E/S de cuadro](./images/aemf68.png)

Ahora puede ver más detalles sobre los metadatos del archivo PNG generado.

![E/S de cuadro](./images/aemf69.png)

Ahora ha completado correctamente este ejercicio.

## Pasos siguientes

Vaya a [Resumen y ventajas de la automatización del flujo de trabajo de Creative con Workfront Fusion](./summary.md){target="_blank"}

Volver a [Automatización del flujo de trabajo de Creative con Workfront Fusion](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
