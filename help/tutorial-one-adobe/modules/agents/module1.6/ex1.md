---
title: Introducción a AEM Agents
description: Introducción a AEM Agents
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: 22691d40708e3b48b9365841dff0d3643e041481
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 1%

---

# 1.6.1 Introducción a AEM Agents

>[!IMPORTANT]
>
>Es posible que la zona protegida de AEM CS esté en hibernación. Dado que la dehibernación de una zona protegida tarda de 10 a 15 minutos, sería aconsejable iniciar el proceso de dehibernación ahora para no tener que esperarla más adelante.

## Agente de detección 1.6.1.1

Adobe Experience Manager (AEM) Discovery Agent es una herramienta con tecnología de IA en AEM as a Cloud Service que permite a los usuarios buscar, recuperar y utilizar contenido, incluidos Assets, fragmentos de contenido y Forms adaptable, mediante peticiones en lenguaje natural. Esto elimina la necesidad de realizar filtros manuales, con muchos clics o complejos. Para ello, comprende la intención y realiza búsquedas en todo el repositorio.

Para usar **Discovery Agent**, primero creará algunas etiquetas en Adobe Experience Manager y luego etiquetará algunos recursos usando esas etiquetas. Una vez hecho esto, podrá usar AI Assistant para descubrir recursos de una manera fácil y fácil de usar.

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. La organización que debe seleccionar es `--aepImsOrgName--`.

### Creación y uso de etiquetas con Assets

Haga clic en para abrir el programa de Cloud Manager, que debe utilizar las siguientes opciones de nomenclatura:

- **`Tech Insiders - AEM + ACCS X`**, donde X significa el número que se le asignó.
- **`Tech Insiders On Demand - AEM + ACCS X`**, donde X significa el número que se le asignó.
- **`--aepUserLdap-- - CitiSignal AEM+ACCS`**, en este caso no tiene un número porque está usando su propio programa de AEM que creó usted mismo.

En este ejemplo, se utilizará el programa **Tech Insiders - AEM + ACCS 100**. Debe utilizar su propio programa.

![Agentes de AEM](./images/aemagents1.png)

Haga clic en la dirección URL del entorno para abrirlo.

![Agentes de AEM](./images/aemagents2.png)

Haga clic en el icono **herramientas**.

![Agentes de AEM](./images/aemagents3.png)

En **General**, haga clic en **Etiquetado**.

![Agentes de AEM](./images/aemagents4.png)

Entonces debería ver esto. Haga clic en **Crear** y luego seleccione **Crear área de nombres**.

![Agentes de AEM](./images/aemagents5.png)

En el campo **Título**, escriba: `--aepUserLdap-- - CitiSignal`. Haga clic en **Crear**.

![Agentes de AEM](./images/aemagents6.png)

Explore en profundidad el espacio de nombres **`--aepUserLdap-- - CitiSignal`** haciendo clic en él. Haga clic en **Crear** y luego seleccione **Crear etiqueta**.

![Agentes de AEM](./images/aemagents7.png)

En el campo **Título**, escriba: `--aepUserLdap-- - Campaign`. Haga clic en **Enviar**.

![Agentes de AEM](./images/aemagents8.png)

Seleccione la etiqueta **`--aepUserLdap-- - Campaign`** al hacer clic en ella. Haga clic en **Crear** y luego seleccione **Crear etiqueta**.

![Agentes de AEM](./images/aemagents9.png)

En el campo **Título**, escriba: `--aepUserLdap-- - Winter 2026`. Haga clic en **Enviar**.

![Agentes de AEM](./images/aemagents10.png)

Seleccione la etiqueta **Campaign** haciendo clic en ella. Haga clic en **Crear** y luego seleccione **Crear etiqueta**.

![Agentes de AEM](./images/aemagents11.png)

En el campo **Título**, escriba: `--aepUserLdap-- - Spring 2026`. Haga clic en **Enviar**.

![Agentes de AEM](./images/aemagents12.png)

Ahora debería tener esto.

![Agentes de AEM](./images/aemagents13.png)

Haga clic en **Adobe Experience Manager** y luego en **Assets**.

![Agentes de AEM](./images/aemagents14.png)

Haga clic en **Archivos**.

![Agentes de AEM](./images/aemagents15.png)

Haga clic en la carpeta **CitiSignal** para abrirla.

![Agentes de AEM](./images/aemagents16.png)

Haga clic en **Crear** y luego seleccione **Archivos**.

![Agentes de AEM](./images/aemagents17.png)

Descargue el archivo [citisignal-images-campaign.zip](./assets/citisignal-images-campaign.zip) y descomprímalo en su escritorio.

![Agentes de AEM](./images/aemagents17a.png)

Seleccione los tres archivos que acaba de descargar y haga clic en **abrir**.

![Agentes de AEM](./images/aemagents18.png)

Haga clic en **Cargar**.

![Agentes de AEM](./images/aemagents19.png)

Entonces debería ver esto.

![Agentes de AEM](./images/aemagents20.png)

Seleccione la primera imagen (citisignal_lion.png) y luego haga clic en **Propiedades**.

![Agentes de AEM](./images/aemagents21.png)

Haga clic en el icono **carpeta** en Etiquetas.

![Agentes de AEM](./images/aemagents22.png)

Seleccione la etiqueta **`--aepUserLdap-- - Spring 2026`** y haga clic en **Seleccionar**.

![Agentes de AEM](./images/aemagents23.png)

Haga clic en **Guardar y cerrar**.

![Agentes de AEM](./images/aemagents23a.png)

Repita esto para estas imágenes:

- `citisignal_leopard.png`
- `citisignal_gorilla.png`
- `citisignal_neon_rabbit.png`

Una vez que hayas seleccionado esa etiqueta para todas las imágenes, ve a **Experience Manager Assets**.

![Agentes de AEM](./images/aemagents24.png)

Haz clic en el icono **perfil** en la parte superior derecha de la pantalla. Haga clic en **Cambiar vista**.

![Agentes de AEM](./images/aemagents25.png)

Entonces debería ver esto.

![Agentes de AEM](./images/aemagents26.png)

Haga doble clic para abrir la primera imagen.

![Agentes de AEM](./images/aemagents27.png)

Seleccione **Aprobado** y haga clic en **Guardar**.

![Agentes de AEM](./images/aemagents28.png)

En **Etiquetas**, puede ver la etiqueta que seleccionó anteriormente.

![Agentes de AEM](./images/aemagents29.png)

Repita ese proceso para que se aprueben las 4 imágenes.

![Agentes de AEM](./images/aemagents30.png)

A continuación, ve a **Mi espacio de trabajo** y haz clic para abrir **Asistente de IA**.

![Agentes de AEM](./images/aemagents31.png)

Escriba la siguiente solicitud y haga clic en **Enviar**.

```javascript
find all assets tagged with '--aepUserLdap-- - Spring 2026'
```

![Agentes de AEM](./images/aemagents32.png)

Si tiene acceso a varios entornos de AEM Assets CS, verá algo similar a esto. Haga clic en la respuesta propuesta para el entorno que desee usar y, a continuación, haga clic en **Enviar**.

![Agentes de AEM](./images/aemagents34.png)

Debería ver una respuesta similar. Haga clic en el icono para expandir el asistente de IA a pantalla completa.

![Agentes de AEM](./images/aemagents35.png)

Revise las respuestas.

![Agentes de AEM](./images/aemagents36.png)

Haga clic en el icono **Ver información** en cualquiera de los recursos.

![Agentes de AEM](./images/aemagents37.png)

A continuación, verá una vista ampliada del recurso seleccionado, con algunos metadatos.

![Agentes de AEM](./images/aemagents38.png)

## 1.6.1.2 agente de producción de experiencia

### Actualización de contenido: Assets

La aptitud para la actualización de contenido actualiza fácilmente el contenido existente, incluidos los fragmentos de contenido, las páginas, los formularios y los recursos. El agente puede realizar acciones como actualizar, quitar, reemplazar o agregar elementos de contenido para mantener las experiencias precisas y actualizadas. Las entradas pueden ser descripciones en lenguaje natural y, cuando se utilizan con PDF de Jira y capturas de pantalla, pueden proporcionar entradas a.

Vuelva a la pantalla del asistente de IA. Cierre el panel lateral.

![Agentes de AEM](./images/aemagents40.png)

Seleccione uno de los indicadores propuestos y haga clic en **Enviar**.

`For the first image, generate renditions for Instagram and LinkedIn posts`

![Agentes de AEM](./images/aemagents40a.png)

Después de un par de minutos, debería ver una respuesta similar.

![Agentes de AEM](./images/aemagents41.png)

Revise las imágenes que se generaron.

![Agentes de AEM](./images/aemagents42.png)

Siéntase libre de experimentar con otros indicadores. Desplácese hacia arriba y seleccione uno de los otros indicadores propuestos, o escriba el suyo propio y haga clic en **Enviar**.

`For the first image, generate a mirrored image`

![Agentes de AEM](./images/aemagents42a.png)

Revise las imágenes que se generaron.

![Agentes de AEM](./images/aemagents42b.png)

### Actualización de contenido: páginas

Vuelva a su entorno de Adobe Experience Manager Author y luego vaya a **Sites**.

![Agentes de AEM](./images/aemagents43.png)

Vaya a **CitiSignal**. Haga clic en **Crear** y seleccione **Página**.

![Agentes de AEM](./images/aemagents44.png)

Seleccione **Página** y haga clic en **Siguiente**.

![Agentes de AEM](./images/aemagents45.png)

Introduzca los siguientes valores:

- Título: **Fibra máxima**
- Nombre: **fiber-max**
- Título de página: **Fibra máxima**

Haga clic en **Crear**.

![Agentes de AEM](./images/aemagents46.png)

Seleccione **Abrir**.

![Agentes de AEM](./images/aemagents47.png)

Entonces debería ver esto.

![Agentes de AEM](./images/aemagents48.png)

Haga clic en el área en blanco para seleccionar el componente **section**. A continuación, haga clic en el icono más **+** del menú derecho y seleccione **Hero**.

![Agentes de AEM](./images/aemagents49.png)

Entonces debería ver esto. Haga clic en **+ Agregar** para agregar una imagen.

![Agentes de AEM](./images/aemagents50.png)

Seleccione el repositorio de recursos. A continuación, abra la carpeta **CitiSignal**.

![Agentes de AEM](./images/aemagents51.png)

Elija la imagen del león que subió anteriormente. Haga clic en **Seleccionar**.

![Agentes de AEM](./images/aemagents52.png)

Entonces debería ver esto. Haga clic en el área **texto** para cambiar el texto.

![Agentes de AEM](./images/aemagents53.png)

Pegue este texto en la área:

```
This winter, be as fast as a lion.
```

Seleccione **Encabezado 1** y haga clic en **Listo**.

![Agentes de AEM](./images/aemagents54.png)

Entonces debería ver esto. Vaya a **Árbol de contenido** y seleccione el área **Sección**.

![Agentes de AEM](./images/aemagents55.png)

Haga clic en el icono **+** y luego seleccione **Tarjetas**.

![Agentes de AEM](./images/aemagents56.png)

Entonces debería ver esto. Asegúrese de que en el **árbol de contenido**, **Tarjetas** esté seleccionado.

A continuación, haga clic en el botón **+** 4 veces.

![Agentes de AEM](./images/aemagents57.png)

Ahora debería ver esto, donde hay 4 objetos **Card** en el objeto **Cards**.

![Agentes de AEM](./images/aemagents58.png)

Seleccione la primera **tarjeta**. Haga clic en el área **texto** para cambiar el texto.

![Agentes de AEM](./images/aemagents59.png)

Pegue el siguiente texto. Asegúrese de que la primera línea de texto esté usando **Encabezado 1**. Haga clic en **Finalizado**.

```
99.9% network reliability

Game, video chat and stream on multiple devices with ultra low lag.
```

![Agentes de AEM](./images/aemagents60.png)

Seleccione la segunda **tarjeta**. Haga clic en el área **texto** para cambiar el texto.

![Agentes de AEM](./images/aemagents61.png)

Pegue el siguiente texto. Asegúrese de que la primera línea de texto esté usando **Encabezado 1**. Haga clic en **Finalizado**.

```
3-year

price lock guarantee

For new and existing Fiber Max customers on all internet plans.

No hidden fees.
```

![Agentes de AEM](./images/aemagents62.png)

Seleccione la tercera **tarjeta**. Haga clic en el área **texto** para cambiar el texto.

![Agentes de AEM](./images/aemagents63.png)

Pegue el siguiente texto. Asegúrese de que la primera línea de texto esté usando **Encabezado 1**. Haga clic en **Finalizado**.

```
More ways to save

Save over 45% on the best entertainment with CitiSignal
```

![Agentes de AEM](./images/aemagents64.png)

Seleccione la cuarta **tarjeta**. Haga clic en el área **texto** para cambiar el texto.

![Agentes de AEM](./images/aemagents65.png)

Pegue el siguiente texto. Asegúrese de que la primera línea de texto esté usando **Encabezado 1**. Haga clic en **Finalizado**.

```
Get Fiber Max now!

Fill out the form here to get started.
```

![Agentes de AEM](./images/aemagents66.png)

Ahora debería tener esto. Haga clic en **Publicar**.

![Agentes de AEM](./images/aemagents67.png)

Vuelva a hacer clic en **Publicar**.

![Agentes de AEM](./images/aemagents68.png)

Haga clic en **Abrir página**.

![Agentes de AEM](./images/aemagents69.png)

Copie la dirección URL de la página como la necesitará a continuación.

La dirección URL debe ser similar a: `https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/content/CitiSignal/fiber-max.html`.

![Agentes de AEM](./images/aemagents70.png)

Vaya a [https://experience.adobe.com/#/experiencemanager/](https://experience.adobe.com/#/experiencemanager/). Haga clic para abrir **Asistente de IA**.

![Agentes de AEM](./images/aemagents71.png)

Pegue la siguiente solicitud y haga clic en **enviar**. Sustituya XXX en este mensaje por la URL que copió en el paso anterior.

```
On the page XXX, please make the following changes:

- change the word 'winter' to 'spring'
- change the word 'lion' to 'leopard'
- change the image in the hero block to use the image 'citisignal_leopard.png'
- change the text '99.9% network reliability' to '99.999% network reliability'
```

![Agentes de AEM](./images/aemagents72.png)

Después de 1-2 minutos, debería ver esto. Escriba el mensaje `generate` y haga clic en **Enviar**.

![Agentes de AEM](./images/aemagents74.png)

Un par de minutos después, debería ver una confirmación como esta de que se han realizado los cambios. Haga clic en **Vista previa de la página actualizada**.

![Agentes de AEM](./images/aemagents75.png)

Ahora obtiene una confirmación visual de los cambios que se han realizado. Esta página de vista previa tiene un propósito meramente informativo. No puede realizar acciones desde esta página.

![Agentes de AEM](./images/aemagents76.png)

Para realizar una acción, haga clic en **Editar en AEM**.

![Agentes de AEM](./images/aemagents75a.png)

En el editor universal, ahora puede ver todos los cambios en detalle, con la capacidad de cambiar cualquier cosa. Una vez que hayas revisado la página, haz clic en **Publicar**.

![Agentes de AEM](./images/aemagents77.png)

Vuelva a hacer clic en **Publicar**. El cambio que ha realizado aún no se ha publicado en el entorno de producción. En su lugar, se ha publicado en **Lanzamientos** en AEM.

Los lanzamientos le permiten desarrollar contenido de forma eficaz para una versión futura. Se crea un lanzamiento para permitirle realizar cambios como preparación para una publicación futura, al mismo tiempo que mantiene sus páginas actuales. Esto significa que está editando dos versiones al mismo tiempo: páginas que se publican actualmente y una versión de esas páginas, que se publicarán a la vez en el futuro. Una vez que llegue ese momento, puede reemplazar las páginas originales y publicar la nueva versión.

![Agentes de AEM](./images/aemagents78.png)

Para **promocionar** tus cambios pendientes para una versión futura, vuelve a AEM. Haz clic en **Adobe Experience Manager** en la parte superior de la página, haz clic en el icono de **martillo** y, a continuación, selecciona **Lanzamientos**.

![Agentes de AEM](./images/aemagents79.png)

Ahora debería ver un **lanzamiento** pendiente. Marque la casilla de verificación delante del **lanzamiento** pendiente.

![Agentes de AEM](./images/aemagents80.png)

Haga clic en **Promocionar**.

![Agentes de AEM](./images/aemagents81.png)

Seleccione **Promocionar lanzamiento completo** y haga clic en **Siguiente**.

![Agentes de AEM](./images/aemagents82.png)

Haga clic en **Promocionar**.

![Agentes de AEM](./images/aemagents83.png)

Ahora debería ver esto. Los cambios se están produciendo.

![Agentes de AEM](./images/aemagents84.png)

Actualice la página, debería ver todos los cambios en la página publicada.

![Agentes de AEM](./images/aemagents85.png)

Alternativamente, en lugar de pasar por el proceso de promoción manual, también puede introducir el indicador `accept` en el asistente de IA.

![Agentes de AEM](./images/aemagents86.png)

A continuación, debería recibir una confirmación de que los cambios se han publicado.

![Agentes de AEM](./images/aemagents87.png)

### Actualización de contenido: creación de formularios

En el módulo [Adobe Experience Manager Forms con Edge Delivery Services](./../../asset-mgmt/module1.3/aemforms.md){target="_blank"} puede encontrar los pasos necesarios para crear un formulario de forma manual.

La habilidad Creación de formularios ahora permite a los usuarios crear formularios adaptables mediante peticiones de datos en lenguaje natural sin depender de equipos de desarrollo o TI. Esta capacidad acelera el desarrollo de formularios a la vez que mantiene la coherencia de la marca y permite a los usuarios empresariales crear formularios sin tener conocimientos técnicos profundos del producto.

Vaya a [https://experience.adobe.com/#/ai-assistant/chat](https://experience.adobe.com/#/ai-assistant/chat).

![Agentes de AEM](./images/aemagentsforms1.png)

Escriba la siguiente solicitud y haga clic en **enviar**.

```
Create a new adaptive form using Edge Delivery Services and the existing CitiSignal site, with the following details:
- Form name: "citisignal-fiber-max-interest-2"
- Form fields: 4 text input fields are needed, for "first-name", "last-name", "email" and "city"
- When the form is submitted, send the submission to a spreadsheet, with this URL: https://docs.google.com/spreadsheets/d/1WwKrcM8mZ2d_W3sMheUAw3nFhP_OFk05TsqxhHkudfQ/edit?usp=sharing.
```

## Pasos siguientes

Ir a [1.6.2 servidores y cursor de AEM MCP](./ex2.md){target="_blank"}

Volver a [AEM y agentes](./aemagents.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
