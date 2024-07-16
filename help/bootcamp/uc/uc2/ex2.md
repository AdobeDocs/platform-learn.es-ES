---
title: Bootcamp - Journey Optimizer Cree su evento
description: Bootcamp - Journey Optimizer Cree su evento
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 2.2 Crear su evento

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `Bootcamp`. Para cambiar de una zona protegida a otra, haga clic en **Prod** y seleccione la zona protegida en la lista. En este ejemplo, la zona protegida se llama **Bootcamp**. Estará en la vista **Inicio** de su zona protegida `Bootcamp`.

![ACOP](./images/acoptriglp.png)

En el menú de la izquierda, desplácese hacia abajo y haga clic en **Configuraciones**. A continuación, haga clic en el botón **Administrar** en **Eventos**.

![ACOP](./images/acopmenu.png)

A continuación, verá una descripción general de todos los eventos disponibles. Haz clic en **Crear evento** para empezar a crear tu propio evento.

![ACOP](./images/emptyevent.png)

A continuación, aparece una nueva ventana de evento vacía.

![ACOP](./images/emptyevent1.png)

En primer lugar, asigne a su evento un nombre como este: `yourLastNameAccountCreationEvent` y agregue una descripción como esta `Account Creation Event`.

![ACOP](./images/eventdescription.png)

A continuación, asegúrese de que **Type** está establecido en **Unitary** y, para la selección de **Event ID Type**, seleccione **System Generated**.

![ACOP](./images/eventidtype.png)

A continuación se muestra la selección Esquema. Se ha preparado un esquema para este ejercicio. Use el esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Después de seleccionar el esquema, verá una serie de campos seleccionados en la sección **Campos**. Ahora debería pasar el ratón sobre la sección **Campos** y verá 3 iconos emergentes. Haz clic en el icono **Editar**.

![ACOP](./images/eventpayload.png)

Verá una ventana emergente de **Campos**, en la cual tendrá que seleccionar algunos de los campos que necesitamos para personalizar el correo electrónico.  Elegiremos otros atributos de perfil más adelante, utilizando los datos que ya están en Adobe Experience Platform.

![ACOP](./images/eventfields.png)

En el objeto `_experienceplatform.demoEnvironment`, asegúrese de seleccionar los campos **brandLogo** y **brandName**.

![ACOP](./images/eventpayloadbr.png)

En el objeto `_experienceplatform.identification.core`, asegúrese de seleccionar el campo **correo electrónico**.

![ACOP](./images/eventpayloadbrid.png)

Haga clic en **Aceptar** para guardar los cambios.

![ACOP](./images/saveok.png)

Entonces debería ver esto. Haz clic en **Guardar** una vez más para guardar los cambios.

![ACOP](./images/eventsave.png)

El evento se ha configurado y guardado.

![ACOP](./images/eventdone.png)

Vuelva a hacer clic en el evento para abrir la pantalla **Editar evento**. Pase el ratón sobre **Campos** de nuevo para ver los 3 iconos. Haz clic en el icono **Ver carga**.

![ACOP](./images/viewevent.png)

Ahora verá un ejemplo de la carga útil esperada.
El evento tiene un identificador de evento de orquestación único, que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

El ID de evento es lo que debe enviarse a Adobe Experience Platform para almacenar en déclencheur el recorrido que creará en uno de los próximos ejercicios. Recuerde este ID de evento, ya que puede necesitarlo más adelante.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Haga clic en **Aceptar**, seguido de **Cancelar**.

Ya ha terminado este ejercicio.

Paso siguiente: [2.3 Crea tu mensaje de correo electrónico](./ex3.md)

[Volver al flujo de usuario 2](./uc2.md)

[Volver a todos los módulos](../../overview.md)
