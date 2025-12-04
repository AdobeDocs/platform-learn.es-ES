---
title: Implementación de Brand Concierge en el sitio web
description: Implementación de Brand Concierge en el sitio web
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---

# 1.4.2 Implementar Brand Concierge en el sitio web

>[!IMPORTANT]
>
>Para completar este ejercicio, debe tener acceso a un entorno de trabajo de AEM Assets CS Author y a un sitio web de AEM CS/EDS.
>
>Si no tiene ese entorno, vaya a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga las instrucciones allí y tendrá acceso a dicho entorno.

>[!IMPORTANT]
>
>Si ha configurado anteriormente un programa AEM CS con un entorno de AEM Assets CS, es posible que la zona protegida de AEM CS esté en hibernación. Dado que la dehibernación de una zona protegida de este tipo tarda de 10 a 15 minutos, sería aconsejable iniciar el proceso de dehibernación ahora para que no tenga que esperar más adelante.

## 1.4.2.1 Configurar el sitio web para que muestre Brand Concierge - Autor de AEM

Para que Brand Concierge aparezca en su sitio web, debe crear un nuevo bloque personalizado que debe añadirse a una nueva página, y debe asegurarse de que la nueva página se añada a la navegación de su sitio web.

Ahora debe configurar las siguientes cosas en este orden:

- Cree un nuevo bloque personalizado que se utilizará para cargar Brand Concierge en el sitio web.
- Cree una nueva página en el sitio web para Brand Concierge.
- Vincule el bloque personalizado recién creado en la página de Brand Concierge recién creada.
- Agregue una referencia para navegar a la página de Brand Concierge recién creada en el archivo de encabezado de navegación del sitio web.

### Crear nuevo bloque personalizado

Para crear el nuevo bloque personalizado, vaya al repositorio de GitHub vinculado a su sitio web.

![Bloquear](./images/block1.png)

#### component-definition.json

Desplácese hacia abajo hasta que vea el archivo **component-definition.json** y ábralo

![Bloquear](./images/block8.png)

Haga clic en el icono **lápiz** para comenzar a editar el archivo.

![Bloquear](./images/block8a.png)

Desplácese hacia abajo hasta que vea **Bloques**. Coloque el cursor bajo el corchete de cierre del componente **Tarjetas**

![Bloquear](./images/block9.png)

Pegue este código e introduzca una coma **,** después del bloque de código:

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

Haga clic en **Confirmar cambios...**.

![Bloquear](./images/block10.png)

Haga clic en **Confirmar cambios**.

![Bloquear](./images/block10a.png)

#### component-models.json

Desplácese hacia abajo hasta que vea el archivo **component-models.json** y haga clic en el icono **lápiz** para empezar a editar el archivo.

![Bloquear](./images/block11.png)

Desplácese hacia abajo hasta que vea el último elemento. Coloque el cursor junto al corchete de cierre del último componente.

![Bloquear](./images/block12.png)

Escriba una coma **,** y, a continuación, presione Intro y, en la línea siguiente, pegue este código:

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

Haga clic en **Confirmar cambios...**.

![Bloquear](./images/block13.png)

Haga clic en **Confirmar cambios**.

![Bloquear](./images/block13a.png)

#### component-filters.json

Desplácese hacia abajo hasta que vea el archivo **component-filters.json** y haga clic en el icono **lápiz** para empezar a editar el archivo.

![Bloquear](./images/block14.png)

Entonces debería ver esto.

![Bloquear](./images/block14a.png)

En la **sección**, escriba una coma `,` y pegue el identificador del componente `"brandconcierge"` después de la última línea actual.

Haga clic en **Confirmar cambios...**.

![Bloquear](./images/block15.png)

Haga clic en **Confirmar cambios**.

![Bloquear](./images/block15a.png)

#### brandconcierge.css

Al crear un bloque, se recomienda crear un archivo para el estilo del bloque y que tenga el mismo nombre que el bloque. ahora debería crear ese archivo, que dejaremos vacío por ahora.

Vaya a la carpeta **blocks**. A continuación, haga clic en **Agregar archivo** y seleccione **Crear nuevo archivo**.

![Bloquear](./images/css1.png)

En el cuadro de texto, escriba `brandconcierge/brandconcierge.css`. El archivo puede permanecer vacío por ahora. Haga clic en **Confirmar cambios...**.

![Bloquear](./images/css2.png)

Haga clic en **Confirmar cambios**.

![Bloquear](./images/css3.png)

#### brandconcierge.js

Al crear un bloque, se recomienda crear un archivo para el javascript relacionado con el bloque y que tenga el mismo nombre que el bloque.

Haga clic en **Agregar archivo** y seleccione **Crear nuevo archivo**.

![Bloquear](./images/js1.png)

En el cuadro de texto, escriba `brandconcierge.js`. El archivo puede permanecer vacío por ahora. Haga clic en **Confirmar cambios...**.

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![Bloquear](./images/js2.png)

Haga clic en **Confirmar cambios**.

![Bloquear](./images/js3.png)

### Crear nueva página y vincular nuevo bloque personalizado

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Haga clic en **Programa** para abrirlo.

![AEMCS](./images/aemcs6.png)

A continuación, haga clic en los 3 puntos **...** en la ficha **Entornos** y haga clic en **Ver detalles**.

![AEMCS](./images/aemcs9.png)

A continuación, verá los detalles del entorno. Haga clic en la dirección URL del entorno **Author**.

>[!NOTE]
>
>Es posible que el entorno esté en hibernación. En ese caso, primero deberá anular la hibernación del entorno.

![AEMCS](./images/aemcs10.png)

Luego debería ver el entorno de AEM Author. Ir a **Sitios**.

![AEMCS](./images/block21.png)

Vaya a **CitiSignal**. Haga clic en **Crear** y seleccione **Página**.

![AEMCS](./images/block23.png)

Seleccione **Página** y haga clic en **Siguiente**.

![AEMCS](./images/block24.png)

Introduzca los siguientes valores:

- Título: **Brand Concierge**
- Nombre: **brandconcierge**
- Título de página: **Brand Concierge**

Haga clic en **Crear**.

![AEMCS](./images/block25.png)

Seleccione **Abrir**.

![AEMCS](./images/block22.png)

Entonces debería ver esto.

![AEMCS](./images/block26.png)

Haga clic en el área en blanco para seleccionar el componente **section**. A continuación, haga clic en el icono más **+** en el menú derecho.

![AEMCS](./images/block27.png)

Debería ver el bloque personalizado en la lista de bloques disponibles. Haga clic en para seleccionarlo.

![AEMCS](./images/block28.png)

Debería ver un bloque vacío que se está agregando a esta página. Este bloque se cargará dinámicamente con las bibliotecas de JavaScript que agregará en el siguiente paso.

Haga clic en **Publicar**.

![AEMCS](./images/block29.png)

Vuelva a hacer clic en **Publicar**.

![AEMCS](./images/block30.png)

La nueva página se ha publicado y ahora se puede agregar al encabezado de navegación en el siguiente paso.

### Actualizar archivo de encabezado de navegación

En tu descripción general de AEM Sites, ve a **CitiSignal** y marca la casilla de verificación del archivo **Header/nav**. Haga clic en **Edit**.

![AEMCS](./images/nav0.png)

Seleccione el campo **Texto** en la pantalla de vista previa y luego haga clic en el campo **Texto** en el lado derecho de la pantalla para editarlo.

![AEMCS](./images/nav0a.png)

Cree una nueva opción de menú en el menú de navegación con el texto `Brand Concierge`. A continuación, seleccione el texto **Brand Concierge** y haga clic en el icono **vínculo**.

![AEMCS](./images/nav1.png)

Escriba esto para el campo **Ruta de acceso o dirección URL** `/content/CitiSignal/brandconcierge.html` e introduzca `Brand Concierge` para el campo **Título**. Haga clic en **Guardar**.

![AEMCS](./images/nav3.png)

Entonces deberías tener esto. Haga clic en **Finalizado**.

![AEMCS](./images/nav4.png)

Entonces deberías tener esto. Haga clic en **Publicar**.

![AEMCS](./images/nav4a.png)

Vuelva a hacer clic en **Publicar**.

![AEMCS](./images/nav5.png)

La nueva página se agregará al menú.

## 1.4.2.2 Configuración del sitio web para mostrar Brand Concierge: GitHub

Después de actualizar el contenido con el entorno de AEM Author, debe actualizar parte del código del repositorio de GitHub que se utiliza para el sitio web.

### Bibliotecas JavaScript

Se requieren las siguientes bibliotecas para implementar Brand Concierge en el sitio web que se ejecuta en AEM CS/EDS:

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

Descargue los 3 archivos en su escritorio.

![Brand Concierge](./images/aem0.png)

Vaya al proyecto GitHub del sitio web de AEM CS/EDS. Ir a **scripts**.

![Brand Concierge](./images/aem1.png)

Haga clic en **Agregar archivo** y, a continuación, seleccione **Cargar archivos**.

![Brand Concierge](./images/aem3.png)

Haga clic en **Elegir los archivos**.

![Brand Concierge](./images/aem3a.png)

Seleccione los 3 archivos **styleConfigurations.js, alloy.js y brandconciergemain.js** de su escritorio y haga clic en **Abrir**.

![Brand Concierge](./images/aem4.png)

Haga clic en **Confirmar cambios**.

![Brand Concierge](./images/aem5.png)

### Actualizar head.html

En el paso anterior ha cargado 3 bibliotecas nuevas. Estas bibliotecas ahora deben cargarse cuando se cargue el sitio web y la manera de hacerlo es agregar referencias a estos archivos en el archivo **head.html**.

Además, también debe proporcionar instrucciones en el archivo **head.html** para asegurarse de que las bibliotecas se cargan en el orden correcto y de manera correcta.

Para ello, vaya al proyecto GitHub de su sitio web de AEM CS/EDS haciendo clic en **Código**.

![Brand Concierge](./images/aem6.png)

Desplácese un poco hacia abajo. Abra el archivo **head.html**.

![Brand Concierge](./images/aem7.png)

Haga clic en el icono **lápiz** para editar este archivo.

![Brand Concierge](./images/aem8.png)

Entonces debería ver esto.

![Brand Concierge](./images/aem9.png)

Desplácese hacia abajo hasta la línea 43 y pegue lo siguiente:

Hay 2 campos en el siguiente código que debe actualizar:

>[!IMPORTANT]
>
>- **datastreamId** está actualmente establecido en &quot;XXXXX&quot; y debe reemplazarse por el ID de la secuencia de datos que creó en el paso anterior.
>- **orgId** debe reemplazarse por el identificador de organización de IMS de su instancia de Adobe Experience Cloud.

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

Haga clic en **Confirmar cambio...**.

![Brand Concierge](./images/aem10.png)

Haga clic en **Confirmar cambio**.

![Brand Concierge](./images/aem11.png)

Ahora ha actualizado el código necesario para cargar las bibliotecas de en el sitio web.

![Brand Concierge](./images/aem12.png)

## 1.4.2.3 Probar la configuración

Ahora podrá probar los cambios en su sitio web yendo a `main--citisignal-aem-accs--XXX.aem.page` o `main--citisignal-aem-accs--XXX.aem.live`, después de reemplazar XXX por su cuenta de usuario de GitHub, que en este ejemplo es `woutervangeluwe`.

En este ejemplo, la dirección URL completa se convierte en lo siguiente:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` o `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Puede llevar algún tiempo antes de que todos los recursos se muestren correctamente, ya que primero deben publicarse.

Entonces debería ver esto. Haga clic en **Brand Concierge**.

![Brand Concierge](./images/aem13.png)

Luego debería ver esta Brand Concierge donde puede introducir su solicitud.

![Brand Concierge](./images/aem14.png)

Volver a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}