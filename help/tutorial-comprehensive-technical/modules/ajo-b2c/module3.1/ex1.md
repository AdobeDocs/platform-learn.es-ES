---
title: Journey Optimizer Cree su evento
description: Journey Optimizer Cree su evento
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.1.1 Creación de un evento

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Para cambiar de una zona protegida a otra, haga clic en **PRODUCTION Prod (VA7)** y seleccione la zona protegida en la lista. En este ejemplo, la zona protegida se denomina **Habilitación de AEP para el año fiscal 22**. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

En el menú de la izquierda, desplácese hacia abajo y haga clic en **Configuraciones**. A continuación, haga clic en el botón **Administrar** en **Eventos**.

![ACOP](./images/acopmenu.png)

A continuación, verá una descripción general de todos los eventos disponibles. Haz clic en **Crear evento** para empezar a crear tu propio evento.

![ACOP](./images/emptyevent.png)

A continuación, aparece una nueva ventana de evento vacía.

![ACOP](./images/emptyevent1.png)

En primer lugar, asigne un nombre al evento como este: `--aepUserLdap--AccountCreationEvent`.

![ACOP](./images/eventname.png)

A continuación, agregue una descripción como esta `Account Creation Event`.

![ACOP](./images/eventdescription.png)

A continuación, asegúrese de que **Type** está establecido en **Unitary** y, para la selección de **Event ID Type**, seleccione **System Generated**.

![ACOP](./images/eventidtype.png)

A continuación se muestra la selección Esquema. Se ha preparado un esquema para este ejercicio. Use el esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Después de seleccionar el esquema, verá una serie de campos seleccionados en la sección **Carga útil**. Ahora debería pasar el ratón sobre la sección **Carga útil** y verá 3 iconos emergentes. Haz clic en el icono **Editar**.

![ACOP](./images/eventpayload.png)

Verá una ventana emergente de **Campos**, en la cual tendrá que seleccionar algunos de los campos que necesitamos para personalizar el correo electrónico.  Elegiremos otros atributos de perfil más adelante, utilizando los datos que ya están en Adobe Experience Platform.

![ACOP](./images/eventfields.png)

En el objeto `--aepTenantId--.demoEnvironment`, asegúrese de seleccionar los campos **brandLogo** y **brandName**.

![ACOP](./images/eventpayloadbr.png)

En el objeto `--aepTenantId--.identification.core`, asegúrese de seleccionar el campo **correo electrónico**.

![ACOP](./images/eventpayloadbrid.png)

Haga clic en **Aceptar** para guardar los cambios.

![ACOP](./images/saveok.png)

Debería ver lo siguiente:

![ACOP](./images/eventsave.png)

Haz clic en **Guardar** una vez más para guardar los cambios.

![ACOP](./images/save1.png)

El evento se ha configurado y guardado.

![ACOP](./images/eventdone.png)

Vuelva a hacer clic en el evento para abrir la pantalla **Editar evento**. Pase el ratón sobre el campo **Carga útil** de nuevo para ver los 3 iconos. Haz clic en el icono **Ver carga**.

![ACOP](./images/viewevent.png)

Ahora verá un ejemplo de la carga útil esperada.

![ACOP](./images/fullpayload.png)

Su evento tiene un identificador de evento de orquestación único, que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

El ID de evento es lo que debe enviarse a Adobe Experience Platform para almacenar en déclencheur la Recorrido que va a generar en el ejercicio 7.2. Recuerde este eventID, tal como lo necesitará en el ejercicio 7.3.
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

Haga clic en **Aceptar**, seguido de **Cancelar**.

Ya ha terminado este ejercicio.

Paso siguiente: [3.1.2 Journey Optimizer: Cree su recorrido y mensaje de correo electrónico](./ex2.md)

[Volver al módulo 3.1](./journey-orchestration-create-account.md)

[Volver a todos los módulos](../../../overview.md)
