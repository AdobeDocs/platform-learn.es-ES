---
title: Revisión con Workfront
description: Revisión con Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: 42f6d8a07baa03a9ab31cff0ef518ae2c5ad930e
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 1.2.2 Revisión con Workfront

>[!IMPORTANT]
>
>Si ha configurado anteriormente un programa AEM CS con un entorno de AEM Assets CS, es posible que la zona protegida de AEM CS esté en hibernación. Dado que la dehibernación de una zona protegida de este tipo tarda de 10 a 15 minutos, sería aconsejable iniciar el proceso de dehibernación ahora para que no tenga que esperar más adelante.

## 1.2.2.1 Crear un nuevo flujo de aprobación

Volver a **Adobe Workfront**. Haga clic en el icono **menú** y seleccione **Revisión**.

![WF](./images/wfp1.png)

Vaya a **Flujos de trabajo**, haga clic en **+ Nuevo** y, a continuación, seleccione **Nueva plantilla**.

![WF](./images/wfp2.png)

Establezca **Template name** en `--aepUserLdap-- - Approval Workflow` y establezca el **Propietario de la plantilla** en usted mismo.

![WF](./images/wfp3.png)

Desplácese hacia abajo y en **Fases** > **Fase 1**, agréguese con la **Función** de **Revisor y aprobador**.

Haga clic en **Crear**.

![WF](./images/wfp4.png)

El flujo de trabajo básico de aprobación ya está listo para su uso.

![WF](./images/wfp5.png)

## 1.2.2.2 Crear un nuevo proyecto

Abra el **menú** y vaya a **Programas**.

![WF](./images/wfp6a.png)

Haga clic en el programa que creó anteriormente, que se denomina `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Creó un programa como parte del ejercicio en [Workfront Planning](./../module1.1/ex1.md) con la automatización que creó y ejecutó. Si aún no lo ha hecho, puede encontrar las instrucciones allí.

![WF](./images/wfp6b.png)

En su programa, vaya a **Proyectos**. Haga clic en **+ Nuevo proyecto** y luego seleccione **Nuevo proyecto**.

![WF](./images/wfp6.png)

Entonces debería ver esto. Cambie el nombre a `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6c.png)

Vaya a **Detalles del proyecto**. Haga clic en **+Agregar** en **Descripción**.

![WF](./images/wfp6d.png)

Definir la descripción en `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Haga clic en **Guardar cambios**.

![WF](./images/wfp6e.png)

El proyecto se ha creado.

![WF](./images/wfp7.png)

## 1.2.2.3 Crear una nueva tarea

Vaya a **Tareas** y haga clic en **+ Nueva tarea**.

![WF](./images/wfp7a.png)

Escriba este nombre para la tarea: `Create assets for Fiber campaign`.

Establecer el campo **Descripción** en: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Haga clic en **Crear tarea**.

![WF](./images/wfp8.png)

Entonces debería ver esto.

![WF](./images/wfp9.png)

En la columna **Asignación**, agregue su propio nombre.

![WF](./images/wfp9a.png)

A continuación, se le asignará la tarea.

![WF](./images/wfp9b.png)

## 1.2.2.4 Agregar un nuevo documento a su tarea para pasar por el flujo de aprobación

Haz clic en el logotipo de **Workfront** para volver a la página de información general. A continuación, debería ver el proyecto que acaba de crear en la descripción general. Haga clic en el proyecto para abrirlo.

![WF](./images/wfp9c.png)

En **Tareas**, haga clic para abrir la tarea.

![WF](./images/wfp9d.png)

Ir a **Documentos**. Haga clic en **+ Agregar nuevo** y luego seleccione **Documento**.

![WF](./images/wfp10.png)

Descarga [este archivo](./images/2048x2048.png) en tu escritorio.

![WF](./images/2048x2048.png){width="50px" align="left"}

Seleccione el archivo **2048x2048.png** y haga clic en **Abrir**.

![WF](./images/wfp12.png)

Entonces deberías tener esto. Pase el ratón sobre el documento cargado. Haga clic en **Crear revisión** y luego elija **Revisión avanzada**.

![WF](./images/wfp13.png)

En la ventana **nueva prueba**, seleccione **Automatizada** y luego seleccione la plantilla de flujo de trabajo que creó anteriormente, que debería llamarse `--aepUserLdap-- - Approval Workflow`. Haga clic en **Crear revisión**.

![WF](./images/wfp14.png)

Haga clic en **Trabajar en ello**.

![WF](./images/wfp17.png)

Haga clic en **Abrir revisión**

![WF](./images/wfp18.png)

Ahora puede revisar la revisión. Seleccione **Agregar comentario** para agregar un comentario que requiera que se cambie el documento.

![WF](./images/wfp19.png)

Escriba su comentario y haga clic en **Publicar**. Haga clic en **Cerrar**.

![WF](./images/wfp20.png)

A continuación, debe cambiar su función de **Revisor** a **Revisor y aprobador**. Para ello, vuelva a su tarea y haga clic en **Flujo de trabajo de revisión**.

![WF](./images/wfp21.png)

Cambia tu rol de **Revisor** a **Revisor y aprobador**.

![WF](./images/wfp22.png)

Vuelva a la tarea y abra la prueba de nuevo. Ahora verá un nuevo botón, **Tomar decisión**. Haga clic en ella.

![WF](./images/wfp23.png)

Seleccione **Cambios necesarios** y haga clic en **tomar decisión**.

![WF](./images/wfp24.png)

Regresa a tu **Tarea** y al **Documento**. Ahora necesita cargar una segunda imagen que tenga en cuenta los comentarios proporcionados.

![WF](./images/wfp25.png)

Descarga [este archivo](./images/2048x2048_buynow.png) en tu escritorio.

![este archivo](./images/2048x2048_buynow.png){width="50px" align="left"}

En la vista de tareas, seleccione el archivo de imagen anterior que no se aprobó. A continuación, haga clic en **+ Agregar nuevo**, seleccione **Versión** y después seleccione **Documento**.

![WF](./images/wfp26.png)

Seleccione el archivo **2048x2048_buynow.png** y haga clic en **Abrir**.

![WF](./images/wfp27.png)

Entonces deberías tener esto. Haga clic en **Crear revisión** y luego seleccione de nuevo **Revisión avanzada**.

![WF](./images/wfp28.png)

Entonces verá esto... La **plantilla de flujo de trabajo** se preseleccionó ya que Workfront supone que el flujo de trabajo de aprobación anterior sigue siendo válido. Haga clic en **Crear revisión**.

![WF](./images/wfp29.png)

Seleccione **Abrir revisión**.

![WF](./images/wfp30.png)

Ahora puede ver dos versiones del archivo una al lado de la otra.

![WF](./images/wfp31.png)

Haga clic en **Tomar decisión**, seleccione **Aprobado** y haga clic en **Tomar decisión** de nuevo.

![WF](./images/wfp32.png)

Haga clic en **Nombre de tarea** para volver a la descripción general de la tarea.

![WF](./images/wfp33.png)

A continuación, volverá a la vista de tareas con un recurso aprobado. Este recurso ahora debe compartirse con los AEM Assets.

![WF](./images/wfp34.png)

Seleccione el documento aprobado. Haga clic en el icono **Compartir flecha** y seleccione la integración de AEM Assets, que debe llamarse `--aepUserLdap-- - CitiSignal AEM`.

![WF](./images/wfp35.png)

Haga doble clic en la carpeta que creó anteriormente, que debe tener el nombre `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfp36.png)

Haga clic en **Seleccionar carpeta**.

![WF](./images/wfp37.png)

Después de 1-2 minutos, el documento se publicará en AEM Assets. Verá un icono de AEM junto al nombre del documento.

![WF](./images/wfp37a.png)

Haga clic en **Marcar como completado** para finalizar esta tarea.

![WF](./images/wfp37b.png)

Entonces debería ver esto.

![WF](./images/wfp37c.png)

## 1.2.2.5 Ver el archivo en AEM Assets

Vaya a la carpeta en AEM Assets CS, que se llama `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfppaem1.png)

Seleccione la imagen y, a continuación, elija **Detalles**.

![WF](./images/wfppaem2.png)

A continuación, verá el formulario de metadatos que creó anteriormente, con los valores que se han rellenado automáticamente con la integración entre Workfront y los AEM Assets.

![WF](./images/wfppaem3.png)

Volver a la administración de [flujos de trabajo con Adobe Workfront](./workfront.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
