---
title: Configuración del entorno de AEM CS
description: Configuración del entorno de AEM CS
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: 490bc79332bb84520ba084ec784ea3ef48a68fb5
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 1%

---

# 1.1.2 Configuración del entorno de AEM CS

## 1.1.2.1 Configurar su repositorio de GitHub

Vaya a [https://github.com](https://github.com){target="_blank"}. Haga clic en **Iniciar sesión**.

![AEMCS](./images/aemcssetup1.png)

Introduzca sus credenciales. Haga clic en **Iniciar sesión**.

![AEMCS](./images/aemcssetup2.png)

Cuando haya iniciado sesión, verá su panel de GitHub.

![AEMCS](./images/aemcssetup3.png)

Vaya a [https://github.com/adobe-rnd/aem-boilerplate-xcom](https://github.com/adobe-rnd/aem-boilerplate-xcom){target="_blank"}. Entonces verá esto... Haga clic en **Usar esta plantilla** y luego haga clic en **Crear un nuevo repositorio**.

![AEMCS](./images/aemcssetup4.png)

Para el **nombre del repositorio**, use `citisignal-aem-accs`. Establezca la visibilidad en **Privado**. Haga clic en **Crear repositorio**.

![AEMCS](./images/aemcssetup5.png)

Después de un par de segundos, se crea el repositorio.

![AEMCS](./images/aemcssetup6.png)

A continuación, vaya a [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Haga clic en **Instalar** o **Configurar**.

![AEMCS](./images/aemcssetup7.png)

Haga clic en el botón **Continuar** situado junto a la cuenta de usuario de GitHub.

![AEMCS](./images/aemcssetup8.png)

Haga clic en **Configurar** junto a su cuenta de usuario de GitHub.

![AEMCS](./images/aemcssetup8a.png)

Haga clic en **Seleccionar solo repositorios** y, a continuación, agregue el repositorio que acaba de crear.

![AEMCS](./images/aemcssetup9.png)

Desplácese hacia abajo y haga clic en **Guardar**.

![AEMCS](./images/aemcssetup9a.png)

Luego recibirás esta confirmación.

![AEMCS](./images/aemcssetup10.png)

## 1.1.2.2 Actualizar archivo fstab.yaml

En su repositorio de GitHub, haga clic para abrir el archivo `fstab.yaml`.

![AEMCS](./images/aemcssetup11.png)

Haga clic en el icono **editar**.

![AEMCS](./images/aemcssetup12.png)

Ahora necesita actualizar el valor del campo **url** en la línea 3.

![AEMCS](./images/aemcssetup13.png)

Debe reemplazar el valor actual por la URL de su entorno AEM Sites CS específico en combinación con la configuración de su repositorio de GitHub.

Este es el valor actual de la dirección URL: `https://author-p130360-e1272151.adobeaemcloud.com/bin/franklin.delivery/adobe-rnd/aem-boilerplate-xcom/main`.

Hay tres partes de la dirección URL que deben actualizarse

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX debe ser reemplazado por la URL de su entorno de AEM CS Author.

AAAA debe reemplazarse por su cuenta de usuario de GitHub.

ZZZ debe reemplazarse por el nombre del repositorio de GitHub que utilizó en el ejercicio anterior.

Puede encontrar la URL del entorno de AEM CS Author en [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png)

A continuación, haga clic en los 3 puntos **...** en la ficha **Entornos** y haga clic en **Ver detalles**.

![AEMCS](./images/aemcs9.png)

A continuación, verá los detalles del entorno, incluida la dirección URL del entorno **Autor**. Copie la dirección URL.

![AEMCS](./images/aemcs10.png)

XXX = `author-p166717-e1786231.adobeaemcloud.com`

Para el nombre de cuenta de usuario de GitHub, puede encontrarlo fácilmente en la URL de su explorador. En este ejemplo, el nombre de cuenta de usuario es `woutervangeluwe`.

AAAA = `woutervangeluwe`

![AEMCS](./images/aemcs11.png)

Para el nombre del repositorio de GitHub, también puede encontrarlo en la ventana del explorador que ha abierto en GitHub. En este caso, el nombre del repositorio es `citisignal`.

ZZZ = `citisignal-aem-accs`

![AEMCS](./images/aemcs12.png)

Estos tres valores combinados dan lugar a esta nueva dirección URL que debe configurarse en el archivo `fstab.yaml`.

`https://author-p166717-e1786231.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal-aem-accs/main`

Haga clic en **Confirmar cambios...**.

![AEMCS](./images/aemcs13.png)

Haga clic en **Confirmar cambios**.

![AEMCS](./images/aemcs14.png)

Se ha actualizado el archivo `fstab.yaml`.

## 1.1.2.3 cargar recursos de CitiSignal

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png)

A continuación, haga clic en la dirección URL del entorno de Author.

![AEMCS](./images/aemcssetup18.png)

Haga clic en **Iniciar sesión con Adobe**.

![AEMCS](./images/aemcssetup19.png)

A continuación, verá su entorno de Author.

![AEMCS](./images/aemcssetup20.png)

La dirección URL será similar a la siguiente: `https://author-p166717-e1786231.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

Ahora necesita acceder al entorno **CRX Package Manager** de AEM. Para ello, elimine `ui#/aem/aem/start.html?appId=aemshell` de la dirección URL y reemplácelo por `crx/packmgr`, lo que significa que la dirección URL debería tener este aspecto ahora:
`https://author-p166717-e1786231.adobeaemcloud.com/crx/packmgr`.
Pulse **Intro** para cargar el entorno del administrador de paquetes

![AEMCS](./images/aemcssetup22.png)

A continuación, haga clic en **Cargar paquete**.

![AEMCS](./images/aemcssetup21.png)

Haga clic en **Examinar** para localizar el paquete que desea cargar.

El paquete que se va a cargar se llama **citisignal-assets.zip** y se puede descargar aquí: [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip){target="_blank"}.

![AEMCS](./images/aemcssetup23.png)

Seleccione el paquete y haga clic en **Abrir**.

![AEMCS](./images/aemcssetup24.png)

A continuación, haga clic en **Aceptar**.

![AEMCS](./images/aemcssetup25.png)

A continuación, se carga el paquete.

![AEMCS](./images/aemcssetup26.png)

A continuación, haga clic en **Instalar** en el paquete que acaba de cargar.

![AEMCS](./images/aemcssetup27.png)

Haga clic en **Instalar**.

![AEMCS](./images/aemcssetup28.png)

Después de un par de minutos, el paquete se instalará.

![AEMCS](./images/aemcssetup29.png)

Ahora puede cerrar esta ventana.

## 1.1.2.4 publicar recursos de CitiSignal

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png)

A continuación, haga clic en la dirección URL del entorno de Author.

![AEMCS](./images/aemcssetup18.png)

Haga clic en **Iniciar sesión con Adobe**.

![AEMCS](./images/aemcssetup19.png)

A continuación, verá su entorno de Author. Haga clic en **Assets**.

![AEMCS](./images/aemcsassets1.png)

Haga clic en **Archivos**.

![AEMCS](./images/aemcsassets2.png)

Haga clic para seleccionar la carpeta **CitiSignal** y luego haga clic en **Administrar publicación**.

![AEMCS](./images/aemcsassets3.png)

Haga clic en **Next**.

![AEMCS](./images/aemcsassets4.png)

Haga clic en **Publicar**.

![AEMCS](./images/aemcsassets5.png)

Sus recursos se han publicado.

## 1.1.2.5 Crear sitio web de CitiSignal

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png)

A continuación, haga clic en la dirección URL del entorno de Author.

![AEMCS](./images/aemcssetup18.png)

Haga clic en **Iniciar sesión con Adobe**.

![AEMCS](./images/aemcssetup19.png)

A continuación, verá su entorno de Author. Haga clic en **Sitios**.

![AEMCS](./images/aemcssetup30.png)

Haga clic en **Crear** y luego en **Sitio a partir de la plantilla**.

![AEMCS](./images/aemcssetup31.png)

Haga clic en **Importar**.

![AEMCS](./images/aemcssetup32.png)

Ahora debe importar una plantilla preconfigurada para el sitio. Puede descargar la plantilla [aquí](./../../../assets/aem/citisignal-aem-sites-commerce-with-edge-delivery-services-template-0.4.0.zip){target="_blank"}. Guarde el archivo en el escritorio.

A continuación, seleccione el archivo `citisignal-aem-sites-commerce-with-edge-delivery-services-template-0.4.0.zip` y haga clic en **Abrir**.

![AEMCS](./images/aemcssetup33.png)

Entonces verá esto... Haga clic para seleccionar la plantilla que acaba de subir y luego haga clic en **Siguiente**.

![AEMCS](./images/aemcssetup34.png)

Ahora debe completar algunos detalles.

- Título del sitio: usar **CitiSignal**
- Nombre del sitio: usar **CitiSignal**
- URL de GitHub: copie la URL del repositorio de GitHub que estaba utilizando antes

![AEMCS](./images/aemcssetup35.png)

Entonces, tendrás esto. Haga clic en **Crear**.

![AEMCS](./images/aemcssetup36.png)

Su sitio se está creando. Esto puede tardar un par de minutos. Haga clic en **Aceptar**.

![AEMCS](./images/aemcssetup37.png)

Actualice la pantalla después de un par de minutos y verá el sitio web de CitiSignal recién creado.

![AEMCS](./images/aemcssetup38.png)

## 1.1.2.6 Actualizar rutas de archivo.json

En su repositorio de GitHub, haga clic para abrir el archivo `paths.json`.

![AEMCS](./images/aemcssetupjson1.png)

Haga clic en el icono **editar**.

![AEMCS](./images/aemcssetupjson2.png)

Ahora necesita actualizar el texto de reemplazo `aem-boilerplate-commerce` por `CitiSignal` en las líneas 3, 4, 5, 6, 7 y 10.

Haga clic en **Confirmar cambios**.

![AEMCS](./images/aemcssetupjson3.png)

Haga clic en **Confirmar cambios**.

![AEMCS](./images/aemcssetupjson4.png)

Se ha actualizado el archivo `paths.json`.

## 1.1.2.7 Publicar sitio web de CitiSignal

A continuación, haga clic en la casilla de verificación que hay delante de **CitiSignal**. A continuación, haga clic en **Administrar publicación**.

![AEMCS](./images/aemcssetup39.png)

Haga clic en **Next**.

![AEMCS](./images/aemcssetup40.png)

Haga clic en **Incluir configuración secundaria**.

![AEMCS](./images/aemcssetup41.png)

Haga clic para seleccionar la casilla de verificación **Incluir elementos secundarios** y, a continuación, haga clic para anular la selección de las demás casillas de verificación. Haga clic en **Aceptar**.

![AEMCS](./images/aemcssetup42.png)

Haga clic en **Publicar**.

![AEMCS](./images/aemcssetup43.png)

Luego te enviarán de vuelta aquí. Haga clic en **CitiSignal**, seleccione la casilla de verificación que hay delante de **índice** y, a continuación, haga clic en **Editar**.

![AEMCS](./images/aemcssetup44.png)

Su sitio web se abrirá en el **Editor universal**.

![AEMCS](./images/aemcssetup45.png)

Ahora podrá acceder a su sitio web yendo a `main--citisignal-aem-accs--XXX.aem.page` y/o `main--citisignal-aem-accs--XXX.aem.live`, después de reemplazar XXX por su cuenta de usuario de GitHub, que en este ejemplo es `woutervangeluwe`.

En este ejemplo, la dirección URL completa se convierte en lo siguiente:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` o `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Puede llevar algún tiempo antes de que todos los recursos se muestren correctamente, ya que primero deben publicarse.

A continuación, verá esto:

![AEMCS](./images/aemcssetup46.png)

## 1.1.2.8 Rendimiento de página de prueba

Vaya a [https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}. Escriba su dirección URL y haga clic en **Analizar**.

![AEMCS](./images/aemcssetup48.png)

A continuación, verá que el sitio web, tanto en una visualización móvil como de escritorio, obtiene una puntuación alta:

**Móvil**:

![AEMCS](./images/aemcssetup49.png)

**Escritorio**:

![AEMCS](./images/aemcssetup50.png)

Paso siguiente: [Desarrollar un bloque personalizado](./ex4.md){target="_blank"}

Volver a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
