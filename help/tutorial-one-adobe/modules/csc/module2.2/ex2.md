---
title: Revisión con Workfront
description: Revisión con Workfront
kt: 5342
doc-type: tutorial
source-git-commit: 246bb91496104818f357848f41b79523b7771638
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 2.2.2 Revisión con Workfront

## 2.2.2.1 Crear un nuevo flujo de aprobación

Vaya a [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Haga clic en el icono de 9 puntos **hamburguesa** y seleccione **Revisión**.

![WF](./images/wfp1.png)

Vaya a **Flujos de trabajo**, haga clic en **+ Nuevo** y, a continuación, seleccione **Nueva plantilla**.

![WF](./images/wfp2.png)

Establezca **Template name** en `--aepUserLdap-- - Approval Workflow` y establezca el **Propietario de la plantilla** en usted mismo.

![WF](./images/wfp3.png)

Desplácese hacia abajo y en **Fases** > **Fase 1**, agregue **Wouter Van Geluwe** con la **Función** de **Revisor y aprobador**.

Haga clic en **Crear**.

![WF](./images/wfp4.png)

El flujo de trabajo básico de aprobación ya está listo para su uso.

![WF](./images/wfp5.png)

## 2.2.2.2 Crear un nuevo proyecto

En la página de inicio de Workfront, haga clic en **Nuevo** en la ficha **Mis proyectos**. Seleccionar **proyecto en blanco**.

![WF](./images/wfp6.png)

Entonces debería ver esto. Cambie el nombre a `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6a.png)

El proyecto se ha creado.

![WF](./images/wfp7.png)

## 2.2.2.3 Crear una nueva tarea

Escriba este nombre para la tarea: **Crear recursos para la campaña de fibra**. Haga clic en **Crear tarea**.

![WF](./images/wfp8.png)

Entonces debería ver esto.

![WF](./images/wfp9.png)

## 2.2.2.4 Agregar un nuevo documento a su tarea para pasar por el flujo de aprobación

Haga clic en **+ Agregar nuevo** y luego seleccione **Documento**.

![WF](./images/wfp10.png)

Descarga [este archivo](./images/2048x2048.png) en tu escritorio.

![WF](./images/2048x2048.png){width="50px" align="left"}

Seleccione el archivo **2048x2048.png** y haga clic en **Abrir**.

![WF](./images/wfp12.png)

Entonces deberías tener esto. Haga clic en **Crear revisión** y luego elija **Revisión avanzada**.

![WF](./images/wfp13.png)

En la ventana **nueva prueba**, seleccione la plantilla de flujo de trabajo que creó anteriormente, que debe llamarse `--aepuserLdap-- - Approval Workflow`. Haga clic en **Crear revisión**.

![WF](./images/wfp14.png)

Luego volverás a estar en tu tarea. Haga clic en el botón **Asignar a** y seleccione **Asignármelo**.

![WF](./images/wfp15.png)

Haga clic en **Guardar**.

![WF](./images/wfp16.png)

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

Entonces deberías estar de vuelta aquí. Ahora necesita cargar una segunda imagen que tenga en cuenta los comentarios proporcionados.

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

Cierre la previsualización de prueba.

![WF](./images/wfp33.png)

A continuación, volverá a la vista de tareas con un recurso aprobado. Este recurso ahora debe compartirse con los AEM Assets.

![WF](./images/wfp34.png)

Haga clic en el icono **Compartir flecha** y seleccione la integración de AEM Assets, que debe llamarse `--aepUserLdap-- - Citi Signal AEM`.

![WF](./images/wfp35.png)

Haga doble clic en la carpeta que creó anteriormente, que debe tener el nombre `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfp36.png)

Haga clic en **Seleccionar carpeta**.

![WF](./images/wfp37.png)

Después de 1-2 minutos, el documento se publicará en AEM Assets. AEM Verá un icono de junto al nombre del documento.

![WF](./images/wfp37a.png)

Haga clic en **Abrir resumen**.

![WF](./images/wfp38.png)

Vaya a **Metadatos**, debería ver lo siguiente:

![WF](./images/wfp39.png)

Vaya a **Información general** y haga clic en **+ Agregar** para agregar una descripción.

![WF](./images/wfp40.png)

Escriba su descripción. La configuración de la prueba y del documento ha finalizado.

![WF](./images/wfp41.png)

## 2.2.2.5 Ver el archivo en AEM Assets

Vaya a la carpeta en AEM Assets, que se llama `--aepUserLdap - Workfront Assets`.

![WF](./images/wfppaem1.png)

Haga clic en los 3 puntos debajo de la imagen y seleccione **Detalles**.

![WF](./images/wfppaem2.png)

A continuación, verá el formulario de metadatos que creó anteriormente, con los valores que se han rellenado automáticamente con la integración entre Workfront y los AEM Assets.

![WF](./images/wfppaem3.png)

[Volver al módulo 2.2](./workfront.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
