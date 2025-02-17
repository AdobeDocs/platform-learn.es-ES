---
title: Introducción a Workfront
description: Introducción a Workfront
kt: 5342
doc-type: tutorial
exl-id: 7ed76d37-5d3e-49c7-b3d3-ebcfe971896d
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# 1.2.1 Introducción a Workfront

Inicie sesión en Adobe Workfront en [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Entonces verá esto.

![WF](./images/wfb1.png)

## 1.2.1.1 Configuración de la integración de AEM Assets

Haga clic en el icono de 9 puntos **hamburguesa** y, a continuación, seleccione **Configuración**.

![WF](./images/wfb2.png)

En el menú de la izquierda, desplácese hacia abajo hasta **Documentos** y, a continuación, haga clic en **Experience Manager Assets**.

![WF](./images/wfb3.png)

Haga clic en **+ Agregar integración de Experience Manager**.

![WF](./images/wfb4.png)

Para el nombre de su integración, use `--aepUserLdap-- - Citi Signal AEM`.

Abra el menú desplegable **Repositorio de Experience Manager** y seleccione su instancia de AEM CS, que debe llamarse `--aepUserLdap-- - Citi Signal`.

![WF](./images/wfb5.png)

En **Metadatos**, configure la siguiente asignación:

| Campo de Workfront | Campo de Experience Manager Assets |
| --------------- | ------------------------------ | 
| **Documento** > **Nombre** | **wm:nombreDocumento** |
| **Proyecto** > **Descripción** | **wm:projectDescription** |
| **Tarea** > **Nombre** | **wm:taskName** |
| **Tarea** > **Descripción** | **wm:taskDescription** |

Habilite el conmutador para **sincronizar metadatos de objeto**.

Haga clic en **Guardar**.

![WF](./images/wfb6.png)

Ya está configurada la integración de Workfront a AEM Assets CS.

![WF](./images/wfb7.png)

## 1.2.1.2 Configuración de la integración de metadatos con AEM Assets

A continuación, debe configurar los AEM Assets para que los campos de metadatos del recurso de Workfront se compartan con AEM.

Para ello, vaya a [https://experience.adobe.com/](https://experience.adobe.com/). Haga clic en **Experience Manager Assets**.

![WF](./images/wfbaem1.png)

Haga clic para seleccionar el entorno de AEM Assets, que debería llamarse `--aepUserLdap-- - Citi Signal dev`.

![WF](./images/wfbaem2.png)

Entonces debería ver esto. En el menú de la izquierda, ve a **Assets** y haz clic en **Crear carpeta**.

![WF](./images/wfbaem3.png)

Asigne un nombre a la carpeta `--aepUserLdap-- - Workfront Assets` y haga clic en **Crear**.

![WF](./images/wfbaem4.png)

A continuación, ve a **Metadata Forms** en el menú de la izquierda y luego haz clic en **Crear**.

![WF](./images/wfbaem5.png)

Use el nombre `--aepUserLdap-- - Metadata Form` y haga clic en **Crear**.

![WF](./images/wfbaem6.png)

Agregue 3 nuevos campos **Texto de una sola línea** al formulario y seleccione el primer campo. A continuación, haga clic en el icono **Esquema** junto al campo **Propiedad de metadatos**.

![WF](./images/wfbaem7.png)

En el campo de búsqueda, escriba `wm:project` y, a continuación, seleccione el campo **Descripción del proyecto**. Haga clic en **Seleccionar**.

![WF](./images/wfbaem8.png)

Cambie la etiqueta del campo a **Descripción del proyecto**.

![WF](./images/wfbaem9.png)

A continuación, seleccione el segundo campo **Texto de una sola línea** y haga clic en el icono **Esquema** junto al campo **Propiedad de metadatos** de nuevo.

![WF](./images/wfbaem10b.png)

Luego verá esta ventana emergente de nuevo. En el campo de búsqueda, escriba `wm:project` y, a continuación, seleccione el campo **Id. de proyecto**. Haga clic en **Seleccionar**.

![WF](./images/wfbaem10.png)

Cambie la etiqueta del campo a **ID de proyecto**.

![WF](./images/wfbaem10a.png)

Seleccione el tercer campo **Texto de una sola línea** y haga clic en el icono **Esquema** junto al campo **Propiedad de metadatos** de nuevo.

![WF](./images/wfbaem11a.png)

Luego verá esta ventana emergente de nuevo. En el campo de búsqueda, escriba `wm:project` y, a continuación, seleccione el campo **Nombre de proyecto**. Haga clic en **Seleccionar**.

![WF](./images/wfbaem11.png)

Cambie la etiqueta del campo a **Nombre de proyecto**. Haga clic en **Guardar**.

![WF](./images/wfbaem12.png)

Cambie **Tab name** del formulario a `--aepUserLdap-- - Workfront Metadata`. Haga clic en **Guardar** y **Cerrar**.

![WF](./images/wfbaem13.png)

Su **formulario de metadatos** ya está configurado.

![WF](./images/wfbaem14.png)

A continuación, debe asignar el formulario de metadatos a la carpeta creada anteriormente. Marque la casilla de verificación del formulario de metadatos y haga clic en **Asignar a las carpetas**.

![WF](./images/wfbaem15.png)

Seleccione su carpeta, que debe tener el nombre `--aepUserLdap-- - Workfront Assets`. Haga clic en **Asignar**.

![WF](./images/wfbaem16.png)

El formulario de metadatos se ha asignado correctamente a la carpeta.

![WF](./images/wfbaem17.png)

## 1.2.1.2 Configuración de la integración de AEM Sites

>[!NOTE]
>
>Este complemento está actualmente en modo **Acceso anticipado** y no está disponible en general todavía.
>
>Es posible que este complemento ya esté instalado en la instancia de Workfront que utiliza. Si ya está instalado, puede revisar las siguientes instrucciones, pero no es necesario cambiar nada en la configuración.

Vaya a [https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}.

Asegúrese de que **toggle** para este complemento esté establecido en **Enabled**. A continuación, haga clic en el icono **engranaje**.

![WF](./images/wfb8.png)

Verá una ventana emergente de **Configuración de la extensión**. Configure los campos siguientes para utilizar este complemento.

| Clave | Valor |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **PROD** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{&quot;previewUrl&quot;: true, &quot;publishUrl&quot;: true}&#39;** |

Haga clic en **Guardar**.

![WF](./images/wfb8.png)

Vuelva a la interfaz de usuario de Workfront y haga clic en el icono de 9 puntos **hamburguesa**. Seleccione **Configuración**.

![WF](./images/wfb9.png)

En el menú de la izquierda, ve a **Forms personalizado** y selecciona **Formulario**. Haga clic en **+ Nuevo formulario personalizado**.

![WF](./images/wfb10.png)

Seleccione **Tarea** y haga clic en **Continuar**.

![WF](./images/wfb11.png)

A continuación, verá un formulario personalizado vacío. Escriba el nombre del formulario `Content Fragment & Integration ID`.

![WF](./images/wfb12.png)

Arrastre y suelte un nuevo campo **Texto de una sola línea** en el lienzo.

![WF](./images/wfb13.png)

Configure el nuevo campo de esta manera:

- **Etiqueta**: **Fragmento de contenido**
- **Nombre**: **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

Agregue un nuevo campo **Texto de una sola línea** al lienzo y configure el nuevo campo de esta manera:

- **Etiqueta**: **Id. de integración**
- **Nombre**: **`aem_workfront_integration_id`**

Haga clic en **Aplicar**.

![WF](./images/wfb15.png)

Ahora debe configurar un segundo formulario personalizado. Haga clic en **+ Nuevo formulario personalizado**.

![WF](./images/wfb10.png)

Seleccione **Tarea** y haga clic en **Continuar**.

![WF](./images/wfb11.png)

A continuación, verá un formulario personalizado vacío. Escriba el nombre del formulario `Preview & Publish URL`.

![WF](./images/wfb16.png)

Arrastre y suelte un nuevo campo **Texto de una sola línea** en el lienzo.

![WF](./images/wfb17.png)

Configure el nuevo campo de esta manera:

- **Etiqueta**: **URL de vista previa**
- **Nombre**: **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

Agregue un nuevo campo **Texto de una sola línea** al lienzo y configure el nuevo campo de esta manera:

- **Etiqueta**: **URL de publicación**
- **Nombre**: **`aem_workfront_integration_publish_url`**

Haga clic en **Aplicar**.

![WF](./images/wfb19.png)

A continuación, debe tener disponibles dos formularios personalizados.

![WF](./images/wfb20.png)

Paso siguiente: [1.2.2 Revisión con Workfront](./ex2.md){target="_blank"}

Volver a la administración de [flujos de trabajo con Adobe Workfront](./workfront.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
