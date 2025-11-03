---
title: Revisión con Workfront
description: Revisión con Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: 6b93c7ed76ef38dda8903d63f4800a98f4e46e1d
workflow-type: tm+mt
source-wordcount: '1319'
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

Desplácese hacia abajo y en **Fases** > **Fase 1**, cambie la función de **Creador de pruebas** a **Revisor y aprobador**. También puede agregar a cualquier otra persona, por ejemplo, agréguese a usted mismo seleccionando su usuario y estableciendo la **Función** de **Revisor y aprobador**.

Haga clic en **Crear**.

![WF](./images/wfp4.png)

El flujo de trabajo básico de aprobación ya está listo para su uso.

![WF](./images/wfp5.png)

## 1.2.2.2 Habilitar modelo de Workfront

En el siguiente paso, creará un nuevo proyecto con una plantilla. Adobe Workfront proporciona una serie de modelos disponibles que solo requieren activarse.

Para el caso de uso de CitiSignal, el modelo **Ejecución de campaña integrada** es el que necesita usar.

Para instalar ese modelo, abra el menú y seleccione **Modelos**.

![WF](./images/blueprint1.png)

Seleccione el filtro **Marketing** y desplácese hacia abajo para encontrar el modelo **Ejecución de campaña integrada**. Haga clic en **Instalar**.

![WF](./images/blueprint2.png)

Haga clic en **Continuar**.

![WF](./images/blueprint3.png)

Haga clic en **Instalar tal cual...**.

![WF](./images/blueprint4.png)

Entonces debería ver esto. La instalación puede tardar un par de minutos.

![WF](./images/blueprint5.png)

Después de un par de minutos, se instalará el modelo.

![WF](./images/blueprint6.png)

## 1.2.2.3 Crear un nuevo proyecto

Abra el **menú** y vaya a **Programas**.

![WF](./images/wfp6a.png)

Haga clic en el programa que creó anteriormente, que se denomina `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Creó un programa como parte del ejercicio en [Workfront Planning](./../module1.1/ex1.md) con la automatización que creó y ejecutó. Si aún no lo ha hecho, puede encontrar las instrucciones allí.

![WF](./images/wfp6b.png)

En su programa, vaya a **Proyectos**. Haga clic en **+ Nuevo proyecto** y, a continuación, seleccione **Nuevo proyecto de la plantilla**.

![WF](./images/wfp6.png)

Seleccione la plantilla **Ejecución de campaña integrada** y haga clic en **Usar plantilla**.

![WF](./images/wfp6g.png)

Entonces debería ver esto. Cambie el nombre a `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` y haga clic en **Crear proyecto**.

![WF](./images/wfp6c.png)

El proyecto se ha creado. Vaya a **Detalles del proyecto**.

![WF](./images/wfp6h.png)

Vaya a **Detalles del proyecto**. Haga clic para seleccionar el texto actual bajo **Descripción**.

![WF](./images/wfp6d.png)

Definir la descripción en `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Haga clic en **Guardar cambios**.

![WF](./images/wfp6e.png)

El proyecto está listo para utilizarse.

![WF](./images/wfp7.png)

Las tareas y dependencias del proyecto se han creado en función de la plantilla elegida y se ha establecido como. propietario del proyecto. El estado del proyecto se ha establecido en **Planificación**. Puede cambiar el estado del proyecto seleccionando otro valor en la lista.

![WF](./images/wfp7z.png)

## 1.2.2.4 Crear una nueva tarea

Pase el ratón sobre la tarea **Comenzar a crear plantillas de diseño** y haga clic en los 3 puntos **...**.

![WF](./images/wfp7a.png)

Seleccione la opción **Insertar tarea debajo**.

![WF](./images/wfp7x.png)

Escriba este nombre para la tarea: `Create layout using approved assets and copy`.

Establezca el campo **Asignaciones** en el rol **Designer**.
Establezca el campo **Duration** en **5 días**.
Establezca el predecesor del campo en **9**.
Escriba una fecha para los campos **Comienza el** y **Vence el**.

Haga clic en otro lugar de la pantalla para guardar la nueva tarea.

![WF](./images/wfp8.png)

Entonces debería ver esto. Haga clic en la tarea para abrirla.

![WF](./images/wfp9.png)

Vaya a **Detalles de la tarea** y establezca el campo **Descripción** en: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Haga clic en **Guardar cambios**.

![WF](./images/wfp9a.png)

Entonces debería ver esto. Haga clic en el campo **Proyecto** para regresar al proyecto.

![WF](./images/wfp9b.png)

En la vista **Proyecto**, vaya a **Distribuidor de cargas de trabajo**.

![WF](./images/wfpwlb1.png)

Haga clic en **Asignaciones en lotes**.

![WF](./images/wfpwlb2.png)

Seleccione la **asignación de rol** de **Designer** y luego haga clic en el campo **Usuario para asignar**. Se mostrarán todos los usuarios que tengan el rol **Designer** en su instancia de Workfront. En este caso, seleccione al usuario ficticio **Melissa Jenkins**.

![WF](./images/wfpwlb3.png)

Haga clic en **Asignar**. El usuario que has seleccionado ahora se asignará a las tareas del proyecto que están vinculadas al rol **Designer**.

![WF](./images/wfpwlb4.png)

Las tareas ahora están asignadas. Haga clic en **Tareas** para volver a la página de información general de **Tareas**.

![WF](./images/wfpwlb5.png)

Haga clic en la tarea que ha creado, que se denomina
**Crear diseño con recursos aprobados y copiar**.

![WF](./images/wfpwlb6.png)

Ahora empezará a trabajar en esta tarea como parte de este ejercicio. Se puede ver que Melissa Jenkins está asignada a esta tarea en este momento. Para cambiarlo, haga clic en el campo **Asignaciones** y seleccione **Asignármelo**.

![WF](./images/wfpwlb7.png)

Haga clic en **Guardar**.

![WF](./images/wfpwlb8.png)

Haga clic en **Trabajar en ello**.

![WF](./images/wfpwlb9.png)

Entonces debería ver esto.

![WF](./images/wfpwlb10.png)

Como parte de esta tarea, debe crear una nueva imagen y luego cargarla como documento en Workfront. Ahora creará ese recurso usted mismo mediante Adobe Express.

## 1.2.2.5 Agregar un nuevo documento a su tarea e iniciar el flujo de aprobación

Para realizar este ejercicio, debe descargar y utilizar este recurso: [timetravelnow.png](./images/timetravelnow.png)

![WF](./images/timetravelnow.png)

Vuelva a la pantalla **Detalles de la tarea**. Ir a **Documentos**. Haga clic en **+ Agregar nuevo** y, a continuación, seleccione el repositorio de AEM Assets CS, que debe llamarse `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfp10.png)

Haga doble clic para abrir la carpeta `--aepUserLdap-- CitiSignal Fiber Campaign`.

![WF](./images/wfp10a.png)

Seleccione el archivo que creó en el paso anterior, que se llama **CitiSignal - Neon rabbit - Timetravel Now!.png**. Haga clic en **Seleccionar**.

![WF](./images/2048x2048.png){width="50px" align="left"}

Entonces deberías tener esto. Pase el ratón sobre el documento cargado. Haga clic en **Crear revisión** y luego elija **Revisión avanzada**.

![WF](./images/wfp13.png)

En la ventana **nueva prueba**, seleccione **Automatizada** y luego seleccione la plantilla de flujo de trabajo que creó anteriormente, que debería llamarse `--aepUserLdap-- - Approval Workflow`. Haga clic en **Crear revisión**.

![WF](./images/wfp14.png)

Haga clic en **Abrir revisión**

![WF](./images/wfp18.png)

Ahora puede revisar la revisión. Seleccione **Agregar comentario** para agregar un comentario que requiera que se cambie el documento.

![WF](./images/wfp19.png)

Escriba su comentario y haga clic en **Publicar**. A continuación, haga clic en **Tomar una decisión**.

![WF](./images/wfp20.png)

Seleccione **Cambios necesarios** y haga clic en **tomar decisión**.

![WF](./images/wfp24.png)

Regresa a tu **Tarea** y al **Documento**. Verá el texto **Cambios necesarios** que también aparece allí.

![WF](./images/wfp25.png)

Ahora debe realizar cambios de diseño, lo que hará en Adobe Express.

## 1.2.2.6 Agregar una nueva versión del documento a la tarea

Para este ejercicio, debe descargar y utilizar este recurso: [getonboard.png](./images/getonboard.png)

![WF](./images/getonboard.png)

En la vista de tareas de Adobe Workfront, seleccione el archivo de imagen antiguo que no se aprobó. A continuación, haga clic en **+ Agregar nuevo**, seleccione **Versión** y, a continuación, seleccione el repositorio de AEM Assets CS, que debería llamarse `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfp26.png)

Vaya a la carpeta `--aepUserLdap-- CitiSignal Fiber Campaign` y seleccione el archivo `CitiSignal - Neon Rabit - Get On Board Now!.png`. Haga clic en **Seleccionar**.

![WF](./images/wfp26a.png)

Entonces deberías tener esto. Haga clic en **Crear revisión** y luego seleccione de nuevo **Revisión avanzada**.

![WF](./images/wfp28.png)

Entonces verá esto... La **plantilla de flujo de trabajo** se preseleccionó ya que Workfront supone que el flujo de trabajo de aprobación anterior sigue siendo válido. Haga clic en **Crear revisión**.

![WF](./images/wfp29.png)

Seleccione **Abrir revisión**.

![WF](./images/wfp30.png)

Ahora puede ver dos versiones del archivo una al lado de la otra. Haga clic en el botón **Comparar pruebas**.

![WF](./images/wfp31.png)

Luego debería ver ambas versiones de la imagen una al lado de la otra. Haga clic en **Tomar decisión**.

![WF](./images/wfp32.png)

Seleccione **Aprobado** y haga clic de nuevo en **Tomar decisión**.

![WF](./images/wfp32a.png)

Cierre la vista **Comparar revisiones** cerrando la versión izquierda de la imagen. Haga clic en **Nombre de tarea** para volver a la descripción general de la tarea.

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

## 1.2.2.7 Ver el archivo en AEM Assets

Vaya a la carpeta en AEM Assets CS, que se llama `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfppaem1.png)

Seleccione la imagen y, a continuación, elija **Detalles**.

![WF](./images/wfppaem2.png)

A continuación, verá el formulario de metadatos que creó anteriormente, con los valores que se han rellenado automáticamente con la integración entre Workfront y los AEM Assets.

![WF](./images/wfppaem3.png)

Volver a la administración de [flujos de trabajo con Adobe Workfront](./workfront.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
