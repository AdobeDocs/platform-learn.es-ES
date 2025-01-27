---
title: AEM - Bloque personalizado básico
description: AEM - Bloque personalizado básico
kt: 5342
doc-type: tutorial
exl-id: 57c08a88-d885-471b-ad78-1dba5992da9d
source-git-commit: e075ac0cf4a9132eb78524b50447aa564e82fff6
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 1%

---

# 2.1.4 Desarrollar un bloque personalizado básico

## 2.1.4.1 Configuración del entorno de desarrollo local

Vaya a [https://desktop.github.com/download/](https://desktop.github.com/download/){target="_blank"}, descargue e instale **Github Desktop**.

![Bloquear](./images/block1.png)

Una vez instalado Github Desktop, vaya al repositorio de GitHub que creó en el ejercicio anterior. Haga clic en **&lt;> código** y, a continuación, haga clic en **Abrir con GitHub Desktop**.

![Bloquear](./images/block2.png)

El repositorio de GitHub se abrirá en GitHub Desktop. No dude en cambiar la **Ruta local**. Haga clic en **Clonar**.

![Bloquear](./images/block3.png)

A continuación, se creará una carpeta local.

![Bloquear](./images/block4.png)

Abra Código de Visual Studio. Vaya a **Archivo** > **Abrir carpeta**.

![Bloquear](./images/block5.png)

Seleccione la carpeta que usa la configuración de GitHub para **citisignal**.

![Bloquear](./images/block6.png)

Ahora verá esa carpeta abierta en Visual Studio Code y ya estará listo para crear un nuevo bloque.

![Bloquear](./images/block7.png)

## 2.1.4.2 Crear un bloque personalizado básico

Adobe recomienda desarrollar bloques en un enfoque de tres fases:

- Cree la definición y el modelo para el bloque, revíselo y llevelo a producción.
- Cree contenido con el nuevo bloque.
- Implemente la decoración y los estilos para el nuevo bloque.

### component-definition.json

En Visual Studio Code, abra el archivo **component-definition.json**.

![Bloquear](./images/block8.png)

Desplácese hacia abajo hasta que vea el componente **Cita**. Coloque el cursor junto al corchete de cierre del último componente.

![Bloquear](./images/block9.png)

Pegue este código e introduzca una coma **,** después del bloque de código:

```json
{
  "title": "FiberOffer",
  "id": "fiberoffer",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "FiberOffer",
          "model": "fiberoffer",
          "offerText": "<p>Fiber will soon be available in your region!</p>",
          "offerCallToAction": "Get your offer now!",
          "offerImage": ""
        }
      }
    }
  }
}
```

Guarde los cambios.

![Bloquear](./images/block10.png)

### component-models.json

En Visual Studio Code, abra el archivo **component-models.json**.

![Bloquear](./images/block11.png)

Desplácese hacia abajo hasta que vea el último elemento. Coloque el cursor junto al corchete de cierre del último componente.

![Bloquear](./images/block12.png)

Escriba una coma **,** y, a continuación, presione Intro y, en la línea siguiente, pegue este código:

```json
{
  "id": "fiberoffer",
  "fields": [
     {
       "component": "richtext",
       "name": "offerText",
       "value": "",
       "label": "Offer Text",
       "valueType": "string"
     },
     {
       "component": "richtext",
       "valueType": "string",
       "name": "offerCallToAction",
       "label": "Offer CTA",
       "value": ""
     },
     {
       "component": "reference",
       "valueType": "string",
       "name": "offerImage",
       "label": "Offer Image",
        "multi": false
     }
   ]
}
```

Guarde los cambios.

![Bloquear](./images/block13.png)

### component-filters.json

En Visual Studio Code, abra el archivo **component-filters.json**.

![Bloquear](./images/block14.png)

En la **sección**, escriba una coma **,** y el identificador de su componente **fiberoffer** después de la última línea actual.

Guarde los cambios.

![Bloquear](./images/block15.png)

## 2.1.4.3 Confirmar los cambios

Ahora ha realizado varios cambios en el proyecto que deben volver a enviarse al repositorio de GitHub. Para ello, abra **GitHub Desktop**.

Entonces debería ver los 3 archivos que acaba de editar en **Cambios**. Revise los cambios.

![Bloquear](./images/block16.png)

Escriba un nombre para su PR, `Fiber Offer custom block`. Haga clic en **Compromiso con main**.

![Bloquear](./images/block17.png)

Entonces debería ver esto. Haga clic en **Origen push**.

![Bloquear](./images/block18.png)

Después de un par de segundos, los cambios se han insertado en el repositorio de GitHub.

![Bloquear](./images/block19.png)

En el navegador, vaya a su cuenta de GitHub y al repositorio que ha creado para CitiSignal. Debería ver algo similar a esto, que muestre que se han recibido los cambios.

![Bloquear](./images/block20.png)

## 2.1.4.4 Añadir el bloque a una página

Ahora que el bloque de presupuesto básico está definido y comprometido con el proyecto CitiSignal, puede agregar un bloque **fiberoffer** a una página existente.

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png)

A continuación, haga clic en los 3 puntos **...** en la ficha **Entornos** y haga clic en **Ver detalles**.

![AEMCS](./images/aemcs9.png)

A continuación, verá los detalles del entorno. Haga clic en la dirección URL del entorno **Author**.

>[!NOTE]
>
>Es posible que el entorno esté en hibernación. En ese caso, primero deberá anular la hibernación del entorno.

![AEMCS](./images/aemcs10.png)

AEM A continuación, debería ver el entorno de autor de la. Ir a **Sitios**.

![AEMCS](./images/block21.png)

Vaya a **CitiSignal** > **us** > **en**.

![AEMCS](./images/block22.png)

Haga clic en **Crear** y seleccione **Página**.

![AEMCS](./images/block23.png)

Seleccione **Página** y haga clic en **Siguiente**.

![AEMCS](./images/block24.png)

Introduzca los siguientes valores:

- Título: **CitiSignal Fiber**
- Nombre: **citisignal-fiber**
- Título de página: **CitiSignal Fiber**

Haga clic en **Crear**.

![AEMCS](./images/block25.png)

Entonces debería ver esto.

![AEMCS](./images/block26.png)

Haga clic en el área en blanco para seleccionar el componente **section**. A continuación, haga clic en el icono más **+** en el menú derecho.

![AEMCS](./images/block27.png)

Debería ver el bloque personalizado en la lista de bloques disponibles. Haga clic en para seleccionarlo.

![AEMCS](./images/block28.png)

Verá campos como **Texto de oferta**, **CTA de oferta** e **Imagen de oferta** que se agregan al editor. Haga clic en **+ Agregar** en el campo **Imagen de la oferta** para seleccionar una imagen.

![AEMCS](./images/block29.png)

Entonces debería ver esto. Haga clic para abrir la carpeta **citisignal**.

![AEMCS](./images/blockpub1.png)

Seleccione la imagen **product-enrichment-1.png**. Haga clic en **Seleccionar**.

![AEMCS](./images/blockpub2.png)

Entonces deberías tener esto. Haga clic en **Publish**.

![AEMCS](./images/blockpub3.png)

Vuelva a hacer clic en **Publish**.

![AEMCS](./images/blockpub4.png)

Se ha publicado su nueva página.

## 2.1.4.5 Añada la nueva página al menú de navegación

En la descripción general de AEM Sites, ve a **CitiSignal** > **Fragmentos** y marca la casilla de verificación de **Encabezado**. Haga clic en **Edit**.

![AEMCS](./images/nav0.png)

Agregue una opción de menú al menú de navegación con el texto `Fiber`. Seleccione el texto **Fibra** y haga clic en el icono **vínculo**.

![AEMCS](./images/nav1.png)

Escriba esto para la **URL** `/us/en/citisignal-fiber` y haga clic en el icono **V** para confirmar.

![AEMCS](./images/nav3.png)

Entonces deberías tener esto. Haga clic en **Publish**.

![AEMCS](./images/nav4.png)

Vuelva a hacer clic en **Publish**.

![AEMCS](./images/nav5.png)

Ahora podrá ver los cambios en su sitio web yendo a `main--citisignal--XXX.aem.page/us/en` y/o `main--citisignal--XXX.aem.live/us/en`, después de reemplazar XXX por su cuenta de usuario de GitHub, que en este ejemplo es `woutervangeluwe`.

En este ejemplo, la dirección URL completa se convierte en lo siguiente:
`https://main--citisignal--woutervangeluwe.aem.page/us/en` o `https://main--citisignal--woutervangeluwe.aem.live/us/en`.

Entonces debería ver esto. Haga clic en **Fibra**.

![AEMCS](./images/nav6.png)

Este es el bloque personalizado básico, pero que ahora se representa en el sitio web.

![AEMCS](./images/nav7.png)



Paso siguiente: [2.1.5 Bloque personalizado avanzado](./ex5.md){target="_blank"}

[Volver al módulo 2.1](./aemcs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
