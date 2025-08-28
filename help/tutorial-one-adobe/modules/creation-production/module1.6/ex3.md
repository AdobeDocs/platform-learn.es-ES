---
title: Cree su aplicación DAM externa
description: Cree su aplicación DAM externa
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 6823e8a0-dde7-460a-a48a-6787e65e4104
source-git-commit: 8219f3bd33448f90b87bf9ccb15738f1294e5965
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 1%

---

# 1.6.3 Creación e implementación de la aplicación DAM externa

## 1.6.3.1 descargar archivos de aplicación de ejemplo

Vaya a [https://github.com/woutervangeluwe/genstudio-external-dam-app](https://github.com/woutervangeluwe/genstudio-external-dam-app). Haga clic en **Código** y, a continuación, seleccione **Descargar ZIP**.

![Ext DAM](./images/extdam1.png)

Desempaquete el archivo zip en su escritorio.

![Ext DAM](./images/extdam2.png)

## 1.6.3.2 Configurar la interfaz de línea de comandos de Adobe Developer

Haga clic con el botón derecho en la carpeta **genstudio-external-dam-app-main** y seleccione **Nuevo terminal en la carpeta**.

![Ext DAM](./images/extdam5.png)

Entonces debería ver esto. Escriba el comando `aio login`. Este comando se redireccionará al explorador y se espera que inicie sesión.

![Ext DAM](./images/extdam6.png)

Después de iniciar sesión correctamente, debería ver esto en el explorador.

![Ext DAM](./images/extdam7.png)

A continuación, el explorador redireccionará de nuevo a la ventana de terminal. Debería ver un mensaje que indique **Inicio de sesión correcto** y un token largo que devuelve el explorador.

![Ext DAM](./images/extdam8.png)

El siguiente paso es configurar la instancia y el proyecto de Adobe IO que utilizará para la aplicación DAM externa.

Para ello, debe descargar un archivo del proyecto de Adobe IO que configuró anteriormente.

Vaya a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} y abra el proyecto que creó anteriormente, que se llama `--aepUserLdap-- GSPeM EXT`. Abra el área de trabajo **Producción**.

![Ext DAM](./images/extdam9.png)

Haga clic en **Descargar todo**. Esto descargará un archivo JSON.

![Ext DAM](./images/extdam10.png)

Copie el archivo JSON del directorio **Descargas** en el directorio raíz de la aplicación DAM externa.

![Ext DAM](./images/extdam11.png)

Vuelve a la ventana de tu terminal. Escriba el comando `aio app use XXX-YYY-Production.json`.

>[!NOTE]
>
>Debe cambiar el nombre del archivo en el comando anterior para que coincida con el nombre del archivo.

Una vez ejecutado el comando, la aplicación DAM externa se conectará al proyecto de Adobe IO con App Builder que creó anteriormente.

![Ext DAM](./images/extdam12.png)

## 1.6.3.3 Instalar GenStudio Extensibility SDK

A continuación, debe instalar **GenStudio Extensibility SDK**. Puede encontrar más detalles sobre SDK aquí: [https://github.com/adobe/genstudio-extensibility-sdk](https://github.com/adobe/genstudio-extensibility-sdk).

Para instalar SDK, ejecute este comando en la ventana de terminal:

`npm install @adobe/genstudio-extensibility-sdk`

![Ext DAM](./images/extdam13.png)

Después de un par de minutos, se instalará SDK.

![Ext DAM](./images/extdam14.png)

## 1.6.3.4: revise la aplicación DAM externa en Visual Studio Code.

Abra Código de Visual Studio. Haga clic en **Abrir...** para abrir una carpeta.

![Ext DAM](./images/extdam15.png)

Seleccione la carpeta **genstudio-external-dam-app-main** que contiene la aplicación que descargó anteriormente. Haga clic en **Abrir**.

![Ext DAM](./images/extdam16.png)

Haga clic para abrir el archivo **.env**.

![Ext DAM](./images/extdam17.png)

El archivo **.env** se creó mediante el comando `aio app use` que ejecutó en el paso anterior y contiene la información necesaria para conectarse al proyecto de Adobe IO con App Builder.

![Ext DAM](./images/extdam18.png)

Ahora necesita agregar los siguientes detalles al archivo **.env**, para que la aplicación DAM externa pueda conectarse al contenedor de AWS S3 que creó anteriormente.

```
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
AWS_BUCKET_NAME=
```

Los campos **`AWS_ACCESS_KEY_ID`** y **`AWS_SECRET_ACCESS_KEY`** estaban disponibles después de crear el usuario de IAM en el ejercicio anterior. Se le pidió que los anotara, ahora puede copiar los valores.

![ETL](./images/cred1.png)

El campo **`AWS_REGION`** se puede tomar de la vista de inicio de AWS S3, junto al nombre del contenedor. En este ejemplo, la región es **us-west-2**.

![ETL](./images/bucket2.png)

El campo **`AWS_BUCKET_NAME`** debe ser `--aepUserLdap---gspem-dam`.

Esta información le permite actualizar los valores de cada una de estas variables.

```
AWS_ACCESS_KEY_ID=XXX
AWS_SECRET_ACCESS_KEY=YYY
AWS_REGION=us-west-2
AWS_BUCKET_NAME=--aepUserLdap---gspem-dam
```

Ahora debería pegar este texto en el archivo `.env`. No olvide guardar los cambios.

![Ext DAM](./images/extdam21.png)

A continuación, vuelve a la ventana de tu terminal. Ejecute este comando:

`export $(grep -v '^#' .env | xargs)`

![Ext DAM](./images/extdam23.png)

Por último, debe cambiar la etiqueta que se mostrará dentro de GenStudio for Performance Marketing para poder distinguir la aplicación DAM externa de otras integraciones. Para ello, abra el archivo **Constants.ts** que puede encontrar explorando en profundidad en el explorador **src/genstudiopem > web-src > src**.

La línea 14 debe cambiarse a

`export const extensionLabel: string = "--aepUserLdap-- - External S3 DAM";`

No olvide guardar los cambios.

![Ext DAM](./images/extdam22.png)

## 1.6.3.5 Ejecute su aplicación DAM externa

En la ventana de terminal, ejecute el comando `aio app run`. Debería ver esto después de 1-2 minutos.

>[!NOTE]
>
>Cuando ejecuta `aio app run` por primera vez, es posible que se le redirija al explorador para aceptar un nuevo certificado. Si esto sucede, acepte el certificado y podrá continuar con los pasos siguientes.

![Ext DAM](./images/extdam24.png)

Ya ha confirmado que la aplicación se está ejecutando. El siguiente paso es implementarlo.

En primer lugar, presione **CTRL+C** para evitar que la aplicación se ejecute. A continuación, escriba el comando `aio app deploy`. Este comando implementará el código en Adobe IO.

Como resultado, recibirá una dirección URL similar para acceder a la aplicación implementada:

`https://133309-201burgundyguan.adobeio-static.net/index.html`

![Ext DAM](./images/extdam27.png)

Para hacer pruebas, ahora puede usar esa dirección URL como parámetro de cadena de consulta agregando `?ext=` como prefijo a la dirección URL anterior. Esto da como resultado este parámetro de cadena de consulta:

`?ext=https://133309-201burgundyguan.adobeio-static.net/index.html`

Vaya a [https://experience.adobe.com/genstudio/create](https://experience.adobe.com/genstudio/create).

![Ext DAM](./images/extdam25.png)

A continuación, agregue el parámetro de cadena de consulta justo antes de **#**. La nueva dirección URL debería tener este aspecto:

`https://experience.adobe.com/?ext=https://133309-201burgundyguan.adobeio-static.net/index.html#/@experienceplatform/genstudio/create`

La página se cargará normalmente. Haga clic en **Banners** para empezar a crear un nuevo banner.

![Ext DAM](./images/extdam26.png)

Seleccione una plantilla y haga clic en **Usar**.

![Ext DAM](./images/extdam28.png)

Haga clic en **Seleccionar del contenido**.

![Ext DAM](./images/extdam29.png)

A continuación, debe poder seleccionar el DAM externo, que debe llamarse `--aepUserLdap-- - External S3 DAM`, de la lista desplegable.

![Ext DAM](./images/extdam30.png)

Entonces debería ver esto. Seleccione la imagen **neon_rabbit_banner.jpg** y haga clic en **Usar**.

![Ext DAM](./images/extdam31.png)

Ahora ha seleccionado una imagen de la DAM externa ejecutándose en un compartimento de S3. Con la imagen seleccionada, ahora puede seguir el flujo de trabajo normal como se documenta en el ejercicio [1.3.3.4 Crear y aprobar metadatos ](./../module1.3/ex3.md#create--approve-meta-ad).

![Ext DAM](./images/extdam32.png)

Al realizar cambios en el código en el equipo local, deberá volver a implementar la aplicación. Cuando vuelva a implementar, utilice este comando de terminal:

`aio app deploy --force-build --force-deploy`

![Ext DAM](./images/extdam33.png)

La aplicación ya está lista para publicarse.

## Pasos siguientes

Vaya a [Publicar su aplicación en privado](./ex4.md){target="_blank"}

Volver a [GenStudio for Performance Marketing - Extensibilidad](./genstudioext.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
