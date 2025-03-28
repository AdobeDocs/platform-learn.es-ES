---
title: 'AEM CS: crear un sitio web basado en documentos'
description: 'AEM CS: crear un sitio web basado en documentos'
kt: 5342
doc-type: tutorial
exl-id: db366111-3873-4504-95f1-b240836c833f
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# 1.1.2 Crear un sitio web basado en documentos

Mientras espera a que se cree su programa de Cloud Manager, tiene tiempo suficiente para configurar su primer sitio web de creación basada en documentos. El siguiente ejercicio se basa en el [Tutorial para desarrolladores de aem.live](https://www.aem.live/developer/tutorial){target="_blank"}. Siga los pasos a continuación para empezar.

## 1.1.2.1 Configurar la unidad de Google

Vaya a [https://drive.google.com](https://drive.google.com){target="_blank"}. Haga clic en **+ Nueva** y luego haga clic en **Nueva carpeta**.

![AEMCS](./images/googledrive1.png){zoomable="yes"}

Asigne un nombre a la carpeta `aemdocb-test`. Haga clic en **Crear**.

![AEMCS](./images/googledrive2.png){zoomable="yes"}

Descargue el archivo [aemboilerplate.zip](./../../../assets/aem/aemboilerplate.zip){target="_blank"} y extráigalo en su equipo.

![AEMCS](./images/googledrive3.png){zoomable="yes"}

Verá 3 archivos en esa carpeta. Copie esos archivos en la nueva carpeta de Google Drive.

![AEMCS](./images/googledrive4.png){zoomable="yes"}

Ahora debe convertir estos archivos en un archivo nativo de Google. Para ello, abra cada archivo y vaya a **Archivo** > **Guardar como Google Docs**.

![AEMCS](./images/googledrive5.png){zoomable="yes"}

Debe hacer esto para los 3 archivos y después verá 6 archivos en la carpeta de Google Drive.

![AEMCS](./images/googledrive6.png){zoomable="yes"}

Luego tiene esto en su carpeta.

![AEMCS](./images/googledrive7.png){zoomable="yes"}

Para que funcione la demostración de creación basada en documentos, ahora debe compartir la carpeta de Google Drive con la dirección de correo electrónico **helix@adobe.com**. Haz clic en el nombre de tu carpeta, haz clic en **Compartir** y luego haz clic en **Compartir** de nuevo.

![AEMCS](./images/googledrive8.png){zoomable="yes"}

Escriba la dirección de correo electrónico **helix@adobe.com** y haga clic en **Enviar**.

![AEMCS](./images/googledrive9.png){zoomable="yes"}

A continuación, copie y anote la dirección URL de la carpeta Google Drive tal como la necesitará en el siguiente ejercicio. Haz clic en el nombre de tu carpeta, haz clic en **Compartir** y luego haz clic en **Copiar vínculo**.

![AEMCS](./images/googledrive10.png){zoomable="yes"}

`https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5?usp=drive_link`

Debe quitar el parámetro de cadena de consulta `?usp=drive_link` para que la dirección URL tenga el aspecto siguiente:

`https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5`

## 1.1.2.2 Configurar el repositorio de GitHub

Vaya a [https://github.com](https://github.com){target="_blank"}. Haga clic en **Iniciar sesión**.

![AEMCS](./images/aemcssetup1.png){zoomable="yes"}

Introduzca sus credenciales. Haga clic en **Iniciar sesión**.

![AEMCS](./images/aemcssetup2.png){zoomable="yes"}

Cuando haya iniciado sesión, verá su panel de GitHub.

![AEMCS](./images/aemcssetup3.png){zoomable="yes"}

Vaya a [https://github.com/adobe/aem-boilerplate](https://github.com/adobe/aem-boilerplate){target="_blank"}. Entonces verá esto... Haga clic en **Usar esta plantilla** y luego haga clic en **Crear un nuevo repositorio**.

![AEMCS](./images/aemdocbcssetup4.png){zoomable="yes"}

Para el **nombre del repositorio**, use `aemdocb-test`. Establezca la visibilidad en **Privado**. Haga clic en **Crear repositorio**.

![AEMCS](./images/aemdocbcssetup5.png){zoomable="yes"}

Después de un par de segundos, se crea el repositorio.

![AEMCS](./images/aemdocbcssetup6.png){zoomable="yes"}

A continuación, ve a [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Haga clic en **Configurar**.

![AEMCS](./images/aemcssetup7.png){zoomable="yes"}

Haga clic en su cuenta de GitHub.

![AEMCS](./images/aemcssetup8.png){zoomable="yes"}

Haga clic en **Seleccionar solo repositorios** y, a continuación, agregue el repositorio que acaba de crear. A continuación, haga clic en **Instalar**.

![AEMCS](./images/aemdocbcssetup9.png){zoomable="yes"}

Luego recibirás esta confirmación.

![AEMCS](./images/aemcssetup10.png){zoomable="yes"}

## 1.1.2.3 Actualizar archivo fstab.yaml

En su repositorio de GitHub, haga clic para abrir el archivo `fstab.yaml`.

![AEMCS](./images/aemdocbcssetup11.png){zoomable="yes"}

Haga clic en el icono **editar**.

![AEMCS](./images/aemdocbcssetup12.png){zoomable="yes"}

Ahora necesita actualizar el valor del campo **url** en la línea 2.

![AEMCS](./images/aemdocbcssetup13.png){zoomable="yes"}

Debe reemplazar el valor actual por la URL de su entorno AEM CS específico en combinación con la configuración de su repositorio de GitHub.

Este es el valor actual de la dirección URL: `https://drive.google.com/drive/u/0/folders/1MGzOt7ubUh3gu7zhZIPb7R7dyRzG371j`.

Reemplace ese valor por la dirección URL que copió de la carpeta de Google Drive, `https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5`. Haga clic en **Confirmar cambios...**.

![AEMCS](./images/aemdocbcssetup14.png){zoomable="yes"}

Haga clic en **Confirmar cambios**.

![AEMCS](./images/aemdocbcssetup15.png){zoomable="yes"}

## 1.1.2.4 Instalación de la extensión de AEM Sidekick

Vaya a [https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo](https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo){target="_blank"}. Haga clic en **Agregar a Chrome**.

![AEMCS](./images/aemdocbcssetup16.png){zoomable="yes"}

Anclar la extensión **AEM Sidekick**.

![AEMCS](./images/aemdocbcssetup17.png){zoomable="yes"}

## 1.1.2.5 Previsualizar y publicar el sitio web basado en documentos

Vuelva a la carpeta de Google Drive. En la barra de tareas, haga clic en la extensión **AEM Sidekick**. A continuación, verá una ventana emergente de la barra de AEM Sidekick en la carpeta.

![AEMCS](./images/aemdocbcssetup18.png){zoomable="yes"}

Seleccione los 3 archivos de la carpeta Google Drive. Haga clic en **Vista previa**.

![AEMCS](./images/aemdocbcssetup19.png){zoomable="yes"}

Vuelva a hacer clic en **Vista previa**.

![AEMCS](./images/aemdocbcssetup20.png){zoomable="yes"}

Haga clic en para cerrar la ventana emergente de diálogo verde.

![AEMCS](./images/aemdocbcssetup21.png){zoomable="yes"}

Vuelva a seleccionar los tres archivos de la carpeta Google Drive. Ahora, haga clic en **Publicar**.

![AEMCS](./images/aemdocbcssetup22.png){zoomable="yes"}

Haga clic en **Publicar**.

![AEMCS](./images/aemdocbcssetup23.png){zoomable="yes"}

Haga clic en para cerrar de nuevo el cuadro de diálogo verde. Ahora, selecciona el archivo **index**, haz clic en **Copiar URL** y luego haz clic en **Copiar URL de Live**.

![AEMCS](./images/aemdocbcssetup24.png){zoomable="yes"}

La dirección URL que se copió tendrá el siguiente aspecto: `https://main--aemdocb-test--woutervangeluwe.aem.live/`.

En la URL anterior:

- **main** hace referencia a la rama de su repositorio de GitHub
- **aemdocb-test** hace referencia al nombre del repositorio de GitHub
- **woutervangeluwe** hace referencia al nombre de cuenta de usuario de GitHub
- **.live** hace referencia al entorno en vivo de su instancia de AEM
- Puede reemplazar **.live** por **.page** para abrir el entorno de vista previa de su instancia de AEM

Abra una nueva ventana del explorador y vaya a la dirección URL.

![AEMCS](./images/aemdocbcssetup25.png){zoomable="yes"}

## 1.1.2.6 Realice un cambio y publíquelo

Vuelva a la unidad de Google y abra el filtro **index** en Google.

![AEMCS](./images/aemdocbcssetup27.png){zoomable="yes"}

Reemplace el texto **Testing** por cualquier otro texto de su elección. Haga clic en **Vista previa**.

![AEMCS](./images/aemdocbcssetup28.png){zoomable="yes"}

Se abrirá la versión de vista previa del sitio web. Revise el cambio y haga clic en **Publicar**.

![AEMCS](./images/aemdocbcssetup29.png){zoomable="yes"}

A continuación, verá la versión activa del sitio web.

![AEMCS](./images/aemdocbcssetup30.png){zoomable="yes"}

El ejercicio anterior era una buena manera de empezar y experimentar la creación basada en documentos. Ahora puede continuar con el siguiente ejercicio, en el que configurará su propio sitio web de demostración con CitiSignal como marca de demostración.

Siguiente paso: [1.1.3 Configurar el entorno de AEM CS](./ex3.md){target="_blank"}

Volver a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
