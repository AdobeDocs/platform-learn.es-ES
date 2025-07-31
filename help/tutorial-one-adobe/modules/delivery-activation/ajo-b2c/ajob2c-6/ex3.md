---
title: AJO y GENSTUDIO FOR PERFORMANCE MARKETING
description: AJO y GENSTUDIO FOR PERFORMANCE MARKETING
kt: 5342
doc-type: tutorial
exl-id: 1424f649-d004-4b14-b8af-927ca1d47de5
source-git-commit: 10f1f6a1f77c41e3c912b3d03b73da7b6c68670c
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# 3.6.3 AJO y GenStudio for Performance Marketing

>[!IMPORTANT]
>
>Para completar este ejercicio, debe tener acceso a un entorno de Adobe Journey Optimizer que esté aprovisionado para la integración con GenStudio for Performance Marketing, que actualmente está en fase beta.

>[!IMPORTANT]
>
>Para completar este ejercicio, debe tener acceso a una instancia de aprovisionada para Adobe GenStudio for Performance Marketing.

>[!IMPORTANT]
>
>Para ejecutar todos los pasos de este ejercicio, debe tener acceso a un entorno de Adobe Workfront existente y, en ese entorno, debe haber creado un proyecto y un flujo de trabajo de aprobación. Si sigue el ejercicio [Administración del flujo de trabajo con Adobe Workfront](./../../../../modules/workflow-planning/module1.2/workfront.md){target="_blank"}, tendrá disponible la configuración necesaria.

## 1.3.4.1 Crear y aprobar experiencia de correo electrónico en Adobe GenStudio

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **GenStudio**.

![GSPeM](./../../../creation-production/module1.3/images/gspem1.png)

Entonces debería ver esto. En el menú de la izquierda, ve a **Crear**. Seleccione **Correo electrónico**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail1.png)

Seleccione la plantilla **Email** que importó anteriormente, que se llama `--aepUserLdap---citisignal-email-template`. Haga clic en **Usar**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail2.png)

Entonces debería ver esto. Cambie el nombre de su anuncio a `--aepUserLdap-- - Email Online Gamers Fiber Max`.

![GSPeM](./../../../creation-production/module1.3/images/gsemail3.png)

En **Parámetros**, seleccione las siguientes opciones:

- **Marca**: `--aepUserLdap-- - CitiSignal`
- **Idioma**: `English (US)`
- **Persona**: `--aepUserLdap-- - Smart Home Families`
- **Producto**: `--aepUserLdap-- - CitiSignal Fiber Max`

Haga clic en **Seleccionar del contenido**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail4.png)

Seleccione el recurso `--aepUserLdap-- - neon rabbit.png`. Haga clic en **Usar**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail5.png)

Escriba el mensaje `convince online gamers to start playing online multiplayer games using CitiSignal internet` y haga clic en **Generar**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail6.png)

Debería ver algo así, con 4 variaciones de correo electrónico generadas. La vista predeterminada muestra la vista **móvil**. Para cambiar a la vista de escritorio, haga clic en el icono **equipo**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail7.png)

Para cada correo electrónico, se calcula automáticamente una puntuación de conformidad. Haga clic en la puntuación para ver más detalles.

![GSPeM](./../../../creation-production/module1.3/images/gsemail8.png)

Haga clic en **Ver y corregir problemas**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail9.png)

Puede ver más detalles sobre lo que puede hacer para optimizar la puntuación de complicaciones.

![GSPeM](./../../../creation-production/module1.3/images/gsemail10.png)

A continuación, haga clic en **Solicitar aprobación**, que se conectará a Adobe Workfront.

![GSPeM](./../../../creation-production/module1.3/images/gsemail11.png)

Seleccione el proyecto de Adobe Workfront, que debe tener el nombre `--aepUserLdap-- - CitiSignal Fiber Launch`. Escriba su propia dirección de correo electrónico en **Invitar a personas** y asegúrese de que su rol esté establecido en **Aprobador**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail12.png)

También puede utilizar un flujo de trabajo de aprobación existente en Adobe Workfront. Para ello, haga clic en **Usar plantilla** y seleccione la plantilla `--aepuserLdap-- - Approval Workflow`. Haga clic en **Enviar**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail13.png)

Haga clic en **Ver comentarios en Workfront**, ahora se le enviará a la interfaz de usuario de Adobe Workfront Proof.

![GSPeM](./../../../creation-production/module1.3/images/gsemail14.png)

En la IU de Adobe Workfront Proof, haga clic en **Tomar decisión**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail15.png)

Seleccione **Aprobado** y haga clic en **Tomar decisión**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail16.png)

Haga clic en **Publicar**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail17.png)

Seleccione su campaña `--aepUserLdap-- - CitiSignal Fiber Launch Campaign` y haga clic en **Publicar**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail18.png)

Haga clic en **Abrir en el contenido**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail19.png)

Las 4 experiencias de correo electrónico ya están disponibles en **Contenido** > **Experiencias**.

![GSPeM](./../../../creation-production/module1.3/images/gsemail20.png)

## 1.3.4.2 Crear una campaña en AJO

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Ahora creará una campaña. A diferencia del recorrido basado en eventos del ejercicio anterior, que se basa en eventos de experiencia entrantes o entradas o salidas de audiencia para almacenar en déclencheur un recorrido para un cliente específico, las campañas se dirigen a una audiencia completa una vez con contenido único como boletines informativos, promociones únicas o información genérica, o periódicamente con contenido similar enviado de forma regular como, por ejemplo, campañas de cumpleaños y recordatorios.

En el menú, ve a **Campañas** y haz clic en **Crear campaña**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail21.png)

Seleccione **Programado - Marketing** y haga clic en **Crear**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail22.png)

En la pantalla de creación de campañas, configure lo siguiente:

- **Nombre**: `--aepUserLdap--  - Online Gamers CitiSignal Fiber Max`.
- **Descripción**: Campaña de fibra para jugadores en línea

Haga clic en **Acciones**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail23.png)

Haga clic en **+ Agregar acción** y luego seleccione **Correo electrónico**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail24.png)

A continuación, seleccione una **configuración de correo electrónico** existente y haga clic en **Editar contenido**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail25.png)

Entonces verá esto... Para la **línea de asunto**, use esto:

```
{{profile.person.name.firstName}}, say goodbye to delays!
```

A continuación, haga clic en **Editar contenido**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail26.png)

Haga clic en **Importar HTML**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail27.png)

A continuación, haga clic en el botón de **Adobe GenStudio for Performance Marketing**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail28.png)

A continuación, debería ver una ventana emergente que muestra todas las experiencias de correo electrónico publicadas en GenStudio for Performance Marketing. Seleccione una de las experiencias de correo electrónico disponibles y haga clic en **Usar**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail29.png)

Seleccione su propio repositorio de AEM Assets CS, que debería llamarse `--aepUserLdap-- - CitiSignal dev`, y haga clic en **Importar**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail30.png)

Entonces debería ver esto. Seleccione el botón de imagen que falta y haga clic en **Seleccionar un recurso**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail31.png)

Vaya a la carpeta que se parece a esta, empezando por **GenStudio.zip.....** y seleccione la imagen `--aepUserLdap-- - neon rabbit.png`. Seleccionar **Seleccionar**

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail32.png)

Entonces debería ver esto.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail33.png)

Desplácese hacia abajo hasta el pie de página, seleccione la palabra **Cancelar suscripción** y haga clic en el icono **vínculo**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail38.png)

Establezca **Type** en **Exclusión/baja externa** y establezca la dirección URL en `https://techinsiders.org/unsubscribe.html` (no se permite tener una dirección URL en blanco para el vínculo de cancelación de suscripción).

Haga clic en **Guardar** y luego haga clic en la **flecha** en la esquina superior izquierda de la pantalla para volver a la configuración de la campaña.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail39.png)

Ir a **Audiencia**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail34.png)

Haga clic en **Seleccionar audiencia**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail35.png)

Seleccione la audiencia de la lista de suscripción para jugadores en línea, que debe llamarse `--aepUserLdap--_SL_Interest_Online_Gaming`. Haga clic en **Guardar**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail36.png)

Haga clic en **Revisar para activar**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail37.png)

Si la configuración de tu campaña no tiene problemas, podrás hacer clic en **Activar**.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail40.png)

La campaña se activará, lo que tarda un par de minutos.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail41.png)

Después de un par de minutos, la campaña está activa y el correo electrónico se enviará a la lista de suscripción seleccionada.

![Journey Optimizer](./../../../creation-production/module1.3/images/gsemail42.png)

Ahora ha completado este ejercicio.

## Pasos siguientes

Ir a [Resumen y beneficios](./summary.md)

Volver a [Adobe Journey Optimizer: administración de contenido](./ajocontent.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
