---
title: Configuración del entorno de AEM CS
description: Configuración del entorno de AEM CS
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: 457e7d0dec233edf75717fb9930585a3511bdc65
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 1%

---

# 1.1.3 Configuración del entorno de AEM CS

## 1.1.3.1 Configurar su repositorio de GitHub

Vaya a [https://github.com](https://github.com){target="_blank"}. Haga clic en **Iniciar sesión**.

![AEMCS](./images/aemcssetup1.png){zoomable="yes"}

Introduzca sus credenciales. Haga clic en **Iniciar sesión**.

![AEMCS](./images/aemcssetup2.png){zoomable="yes"}

Cuando haya iniciado sesión, verá su panel de GitHub.

![AEMCS](./images/aemcssetup3.png){zoomable="yes"}

Vaya a [https://github.com/AdobeDevXSC/citisignal-one](https://github.com/AdobeDevXSC/citisignal-one){target="_blank"}. Entonces verá esto... Haga clic en **Usar esta plantilla** y luego haga clic en **Crear un nuevo repositorio**.

![AEMCS](./images/aemcssetup4.png){zoomable="yes"}

Para el **nombre del repositorio**, use `citisignal`. Establezca la visibilidad en **Privado**. Haga clic en **Crear repositorio**.

![AEMCS](./images/aemcssetup5.png){zoomable="yes"}

Después de un par de segundos, se crea el repositorio.

![AEMCS](./images/aemcssetup6.png){zoomable="yes"}

A continuación, vaya a [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Haga clic en **Configurar**.

![AEMCS](./images/aemcssetup7.png){zoomable="yes"}

Haga clic en su cuenta de GitHub.

![AEMCS](./images/aemcssetup8.png){zoomable="yes"}

Haga clic en **Seleccionar solo repositorios** y, a continuación, agregue el repositorio que acaba de crear. A continuación, haga clic en **Instalar**.

![AEMCS](./images/aemcssetup9.png){zoomable="yes"}

Luego recibirás esta confirmación.

![AEMCS](./images/aemcssetup10.png){zoomable="yes"}

## 1.1.3.2 Actualizar archivo fstab.yaml

En su repositorio de GitHub, haga clic para abrir el archivo `fstab.yaml`.

![AEMCS](./images/aemcssetup11.png){zoomable="yes"}

Haga clic en el icono **editar**.

![AEMCS](./images/aemcssetup12.png){zoomable="yes"}

Ahora necesita actualizar el valor del campo **url** en la línea 4.

![AEMCS](./images/aemcssetup13.png){zoomable="yes"}

Debe reemplazar el valor actual por la URL de su entorno AEM CS específico en combinación con la configuración de su repositorio de GitHub.

Este es el valor actual de la dirección URL: `https://author-p131639-e1282833.adobeaemcloud.com/bin/franklin.delivery/adobedevxsc/citisignal-one/main`.

Hay tres partes de la dirección URL que deben actualizarse

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX debe ser reemplazado por la URL de su entorno de AEM CS Author.

AAAA debe reemplazarse por su cuenta de usuario de GitHub.

ZZZ debe reemplazarse por el nombre del repositorio de GitHub que utilizó en el ejercicio anterior.

Puede encontrar la URL del entorno de AEM CS Author en [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

A continuación, haga clic en los 3 puntos **...** en la ficha **Entornos** y haga clic en **Ver detalles**.

![AEMCS](./images/aemcs9.png){zoomable="yes"}

A continuación, verá los detalles del entorno, incluida la dirección URL del entorno **Autor**. Copie la dirección URL.

![AEMCS](./images/aemcs10.png){zoomable="yes"}

XXX = `author-p148073-e1511503.adobeaemcloud.com`

Para el nombre de cuenta de usuario de GitHub, puede encontrarlo fácilmente en la URL de su explorador. En este ejemplo, el nombre de cuenta de usuario es `woutervangeluwe`.

AAAA = `woutervangeluwe`

![AEMCS](./images/aemcs11.png){zoomable="yes"}

Para el nombre del repositorio de GitHub, también puede encontrarlo en la ventana del explorador que ha abierto en GitHub. En este caso, el nombre del repositorio es `citisignal`.

ZZZ = `citisignal`

![AEMCS](./images/aemcs12.png){zoomable="yes"}

Estos tres valores combinados dan lugar a esta nueva dirección URL que debe configurarse en el archivo `fstab.yaml`.

`https://author-p148073-e1511503.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal/main`

Haga clic en **Confirmar cambios...**.

![AEMCS](./images/aemcs13.png){zoomable="yes"}

Haga clic en **Confirmar cambios**.

![AEMCS](./images/aemcs14.png){zoomable="yes"}

Se ha actualizado el archivo `fstab.yaml`.

## 1.1.3.3 cargar recursos de CitiSignal

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

A continuación, haga clic en la dirección URL del entorno de Author.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Haga clic en **Iniciar sesión con Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

A continuación, verá su entorno de Author.

![AEMCS](./images/aemcssetup20.png){zoomable="yes"}

La dirección URL será similar a la siguiente: `https://author-p148073-e1511503.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

Ahora necesita acceder al entorno **CRX Package Manager** de AEM. Para ello, elimine `ui#/aem/aem/start.html?appId=aemshell` de la dirección URL y reemplácelo por `crx/packmgr`, lo que significa que la dirección URL debería tener este aspecto ahora:
`https://author-p148073-e1511503.adobeaemcloud.com/crx/packmgr`.
Pulse **Intro** para cargar el entorno del administrador de paquetes

![AEMCS](./images/aemcssetup22.png){zoomable="yes"}

A continuación, haga clic en **Cargar paquete**.

![AEMCS](./images/aemcssetup21.png){zoomable="yes"}

Haga clic en **Examinar** para localizar el paquete que desea cargar.

El paquete que se va a cargar se llama **citisignal-assets.zip** y se puede descargar aquí: [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip){target="_blank"}.

![AEMCS](./images/aemcssetup23.png){zoomable="yes"}

Seleccione el paquete y haga clic en **Abrir**.

![AEMCS](./images/aemcssetup24.png){zoomable="yes"}

A continuación, haga clic en **Aceptar**.

![AEMCS](./images/aemcssetup25.png){zoomable="yes"}

A continuación, se carga el paquete.

![AEMCS](./images/aemcssetup26.png){zoomable="yes"}

A continuación, haga clic en **Instalar** en el paquete que acaba de cargar.

![AEMCS](./images/aemcssetup27.png){zoomable="yes"}

Haga clic en **Instalar**.

![AEMCS](./images/aemcssetup28.png){zoomable="yes"}

Después de un par de minutos, el paquete se instalará.

![AEMCS](./images/aemcssetup29.png){zoomable="yes"}

Ahora puede cerrar esta ventana.


## 1.1.3.4 publicar recursos de CitiSignal

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

A continuación, haga clic en la dirección URL del entorno de Author.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Haga clic en **Iniciar sesión con Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

A continuación, verá su entorno de Author. Haga clic en **Assets**.

![AEMCS](./images/aemcsassets1.png){zoomable="yes"}

Haga clic en **Archivos**.

![AEMCS](./images/aemcsassets2.png){zoomable="yes"}

Haga clic para seleccionar la carpeta **CitiSignal** y luego haga clic en **Administrar publicación**.

![AEMCS](./images/aemcsassets3.png){zoomable="yes"}

Haga clic en **Next**.

![AEMCS](./images/aemcsassets4.png){zoomable="yes"}

Haga clic en **Publicar**.

![AEMCS](./images/aemcsassets5.png){zoomable="yes"}

Sus recursos se han publicado.

## 1.1.3.5 Crear sitio web de CitiSignal

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

A continuación, haga clic en la dirección URL del entorno de Author.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Haga clic en **Iniciar sesión con Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

A continuación, verá su entorno de Author. Haga clic en **Sitios**.

![AEMCS](./images/aemcssetup30.png){zoomable="yes"}

Haga clic en **Crear** y luego en **Sitio a partir de la plantilla**.

![AEMCS](./images/aemcssetup31.png){zoomable="yes"}

Haga clic en **Importar**.

![AEMCS](./images/aemcssetup32.png){zoomable="yes"}

Ahora debe importar una plantilla preconfigurada para el sitio. Puede descargar la plantilla [aquí](./../../../assets/aem/citisignal-edge-delivery-services-template-0.0.4.zip){target="_blank"}. Guarde el archivo en el escritorio.

A continuación, seleccione el archivo `citisignal-edge-delivery-services-template-0.0.4.zip` y haga clic en **Abrir**.

![AEMCS](./images/aemcssetup33.png){zoomable="yes"}

Entonces verá esto... Haga clic para seleccionar la plantilla que acaba de subir y luego haga clic en **Siguiente**.

![AEMCS](./images/aemcssetup34.png){zoomable="yes"}

Ahora debe completar algunos detalles.

- Título del sitio: usar **CitiSignal**
- Nombre del sitio: usar **citisignal-one**
- URL de GitHub: copie la URL del repositorio de GitHub que estaba utilizando antes

![AEMCS](./images/aemcssetup35.png){zoomable="yes"}

Entonces, tendrás esto. Haga clic en **Crear**.

![AEMCS](./images/aemcssetup36.png){zoomable="yes"}

Su sitio se está creando. Esto puede tardar un par de minutos. Haga clic en **Aceptar**.

![AEMCS](./images/aemcssetup37.png){zoomable="yes"}

Actualice la pantalla después de un par de minutos y verá el sitio web de CitiSignal recién creado.

![AEMCS](./images/aemcssetup38.png){zoomable="yes"}

## 1.1.3.6 Publicar sitio web de CitiSignal

A continuación, haga clic en la casilla de verificación que hay delante de **CitiSignal**. A continuación, haga clic en **Administrar publicación**.

![AEMCS](./images/aemcssetup39.png){zoomable="yes"}

Haga clic en **Next**.

![AEMCS](./images/aemcssetup40.png){zoomable="yes"}

Haga clic en **Incluir configuración secundaria**.

![AEMCS](./images/aemcssetup41.png){zoomable="yes"}

Haga clic para seleccionar la casilla de verificación **Incluir elementos secundarios** y, a continuación, haga clic para anular la selección de las demás casillas de verificación. Haga clic en **Aceptar**.

![AEMCS](./images/aemcssetup42.png){zoomable="yes"}

Haga clic en **Publicar**.

![AEMCS](./images/aemcssetup43.png){zoomable="yes"}

Luego te enviarán de vuelta aquí. Vaya a **CitiSignal** > **us** > **en**. Haga clic en la casilla de verificación que hay delante de **index** y, a continuación, haga clic en **Editar**.

![AEMCS](./images/aemcssetup44.png){zoomable="yes"}

Su sitio web se abrirá en el **Editor universal**.

![AEMCS](./images/aemcssetup45.png){zoomable="yes"}

Ahora podrá acceder a su sitio web yendo a `main--citisignal--XXX.aem.page/us/en/` y/o `main--citisignal--XXX.aem.live/us/en/`, después de reemplazar XXX por su cuenta de usuario de GitHub, que en este ejemplo es `woutervangeluwe`.

En este ejemplo, la dirección URL completa se convierte en lo siguiente:
`https://main--citisignal--woutervangeluwe.aem.page/us/en/` o `https://main--citisignal--woutervangeluwe.aem.live/us/en/`.

Puede llevar algún tiempo antes de que todos los recursos se muestren correctamente, ya que primero deben publicarse.

A continuación, verá esto:

![AEMCS](./images/aemcssetup46.png){zoomable="yes"}

Después de un par de minutos, los recursos se cargarán correctamente.

![AEMCS](./images/aemcssetup47.png){zoomable="yes"}

## 1.1.3.7 Rendimiento de página de prueba

Vaya a [https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}. Escriba su dirección URL y haga clic en **Analizar**.

![AEMCS](./images/aemcssetup48.png){zoomable="yes"}

A continuación, verá que el sitio web, tanto en una visualización móvil como de escritorio, obtiene una puntuación alta:

**Móvil**:

![AEMCS](./images/aemcssetup49.png){zoomable="yes"}

**Escritorio**:

![AEMCS](./images/aemcssetup50.png){zoomable="yes"}

Paso siguiente: [1.1.4 Configuración de un bloque personalizado](./ex4.md){target="_blank"}

Volver a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
