---
title: Journey Optimizer Cree su evento
description: Journey Optimizer Cree su evento
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: e35d2357-21f9-4566-b2a1-cc0cf0c64956
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 7.1 Crear un evento

Inicie sesión en Adobe Journey Optimizer desde [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá al **Página principal**  en Journey Optimizer. En primer lugar, asegúrese de que está utilizando el simulador para pruebas correcto. El entorno limitado que se va a usar se denomina `--aepSandboxId--`. Para cambiar de un simulador de pruebas a otro, haga clic en **PRODUCCIÓN (VA7)** y seleccione el simulador de pruebas de la lista. En este ejemplo, el simulador de pruebas recibe el nombre **Habilitación de AEP para el año fiscal 22**. Entonces estará en el **Página principal** vista del entorno limitado `--aepSandboxId--`.

![ACOP](./images/acoptriglp.png)

En el menú de la izquierda, desplácese hacia abajo y haga clic en **Configuraciones**. A continuación, haga clic en el **Administrar** botón debajo de **Eventos**.

![ACOP](./images/acopmenu.png)

A continuación, verá una descripción general de todos los eventos disponibles. Haga clic en **Crear evento** para comenzar a crear su propio evento.

![ACOP](./images/emptyevent.png)

A continuación, aparece una nueva ventana de evento vacía.

![ACOP](./images/emptyevent1.png)

En primer lugar, asigne un nombre al evento de esta manera: `--demoProfileLdap--AccountCreationEvent`.

![ACOP](./images/eventname.png)

A continuación, añada una descripción como esta `Account Creation Event`.

![ACOP](./images/eventdescription.png)

A continuación, asegúrese de que la variable **Tipo** está configurado como **Unitario** y para la variable **Tipo de ID de evento** selección, seleccionar **Sistema generado**.

![ACOP](./images/eventidtype.png)

A continuación, se muestra la selección de Esquema. Se preparó un esquema para este ejercicio. Utilice el esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Después de seleccionar el esquema, verá una serie de campos seleccionados en el **Carga útil** para obtener más información. Ahora debe pasar el ratón por encima del **Carga útil** y verá 3 iconos emergentes. Haga clic en el **Editar** icono.

![ACOP](./images/eventpayload.png)

Verá un **Campos** ventana emergente, en la que debe seleccionar algunos de los campos que necesitamos para personalizar el correo electrónico.  Más adelante, elegiremos otros atributos de perfil, utilizando los datos que ya están en Adobe Experience Platform.

![ACOP](./images/eventfields.png)

En el objeto `--aepTenantId--.demoEnvironment`, asegúrese de seleccionar los campos **brandLogo** y **brandName**.

![ACOP](./images/eventpayloadbr.png)

En el objeto `--aepTenantId--.identification.core`, asegúrese de seleccionar el campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Haga clic en **Ok** para guardar los cambios.

![ACOP](./images/saveok.png)

Debería ver esto:

![ACOP](./images/eventsave.png)

Haga clic en **Guardar** una vez más para guardar los cambios.

![ACOP](./images/save1.png)

El evento ahora está configurado y guardado.

![ACOP](./images/eventdone.png)

Vuelva a hacer clic en el evento para abrir el **Editar evento** de nuevo. Pase el ratón sobre la **Carga útil** para volver a ver los 3 iconos. Haga clic en el **Ver carga útil** icono.

![ACOP](./images/viewevent.png)

Ahora verá un ejemplo de la carga útil esperada.

![ACOP](./images/fullpayload.png)

Su evento tiene un eventID de orquestación único que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

El ID de evento es lo que se debe enviar a Adobe Experience Platform para almacenar en déclencheur el Recorrido que se va a generar en el ejercicio 7.2. Recuerde este eventID, ya que lo necesitará en el ejercicio 7.3.
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

Haga clic en **Ok**, seguido de hacer clic en **Cancelar**.

Ya has terminado este ejercicio.

Paso siguiente: [7.2 Journey Optimizer: Cree el recorrido y el mensaje de correo electrónico](./ex2.md)

[Volver al módulo 7](./journey-orchestration-create-account.md)

[Volver a todos los módulos](../../overview.md)
