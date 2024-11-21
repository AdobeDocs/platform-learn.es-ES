---
title: 'Audience Activation de Microsoft Azure Event Hub: definir una función de Azure'
description: 'Audience Activation de Microsoft Azure Event Hub: definir una función de Azure'
kt: 5342
doc-type: tutorial
exl-id: c39fea54-98ec-45c3-a502-bcf518e6fd06
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# 2.4.6 Crear su proyecto de Microsoft Azure

## Familiarizarse con las funciones de Azure Event Hub

Las funciones de Azure le permiten ejecutar pequeños fragmentos de código (llamados **funciones**) sin tener que preocuparse por la infraestructura de la aplicación. Con Azure Functions, la infraestructura en la nube proporciona todos los servidores actualizados que necesita para mantener su aplicación ejecutándose a escala.

Una función está **desencadenada** por un tipo de evento específico. Los déclencheur admitidos son responder a cambios en los datos, responder a mensajes (por ejemplo, Event Hubs), ejecutarse en una programación o como resultado de una solicitud HTTP.

Azure Functions es un servicio de computación sin servidor que le permite ejecutar código activado por eventos sin tener que aprovisionar ni administrar explícitamente la infraestructura.

Azure Event Hubs se integra con Azure Functions para una arquitectura sin servidor.

## Abra Código de Visual Studio e inicie sesión en Azure

Visual Studio Code facilita la tarea de...

- definir y enlazar funciones de Azure a Event Hubs
- probar localmente
- implementar en Azure
- ejecución de función de registro remoto

### Abrir código de Visual Studio

### Iniciar sesión en Azure

Cuando inicia sesión con su cuenta de Azure utilizada para registrarse en el ejercicio anterior, Visual Studio Code le permitirá encontrar y enlazar todos los recursos de Event Hub.

Abra Visual Studio Code y haga clic en el icono **Azure**.

A continuación, seleccione **Iniciar sesión en Azure**:

![3-01-vsc-open.png](./images/301vscopen.png)

Se le redirigirá a su explorador para iniciar sesión. Recuerde seleccionar la cuenta de Azure que utilizó para registrarse.

Cuando vea la siguiente pantalla en el explorador, iniciará sesión con Visual Code Studio:

![3-03-vsc-login-ok.png](./images/303vscloginok.png)

Vuelva a Visual Code Studio (verá el nombre de su suscripción de Azure, por ejemplo **suscripción de Azure 1**):

![3-04-vsc-logged-in.png](./images/304vscloggedin.png)

## Crear un proyecto de Azure

Haga clic en **Crear proyecto de función...**:

![3-05-vsc-create-project.png](./images/vsc2.png)

Seleccione una carpeta local de su elección para guardar el proyecto y haga clic en **Seleccionar**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

A continuación, se abrirá el asistente para la creación de proyectos. Haga clic en **Javascript** como idioma para su proyecto:

![3-07-vsc-select-language.png](./images/vsc4.png)

Luego seleccione **Modelo v4**.

![3-07-vsc-select-language.png](./images/vsc4a.png)

Seleccione **déclencheur de Azure Event Hub** como primera plantilla de función del proyecto:

![3-08-vsc-function-template.png](./images/vsc5.png)

Escriba un nombre para la función, use el siguiente formato `--aepUserLdap---aep-event-hub-trigger` y presione Intro:

![3-09-vsc-function-name.png](./images/vsc6.png)

Seleccione **Crear nueva configuración de aplicación local**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

Haga clic aquí para seleccionar el área de nombres del centro de eventos que creó anteriormente, que se denomina `--aepUserLdap---aep-enablement`.

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

A continuación, haga clic para seleccionar el centro de eventos que creó anteriormente, que se llama `--aepUserLdap---aep-enablement-event-hub`.

![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)

Haga clic para seleccionar **RootManageSharedAccessKey** como directiva de Event Hub:

![3-13-vsc-function-select-eventhub-policy.png](./images/vsc10.png)

Seleccione **Agregar al espacio de trabajo** sobre cómo abrir el proyecto:

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

Entonces puedes recibir un mensaje como este. En ese caso, haga clic en **Sí, confío en los autores**.

![3-15-vsc-project-add-to-workspace.png](./images/vsc12a.png)

Una vez creado el proyecto, haga clic en **index.js** para abrir el archivo en el editor:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

La carga útil enviada por Adobe Experience Platform a su centro de eventos incluirá los ID de audiencia:

```json
[{
"segmentMembership": {
"ups": {
"ca114007-4122-4ef6-a730-4d98e56dce45": {
"lastQualificationTime": "2020-08-31T10:59:43Z",
"status": "realized"
},
"be2df7e3-a6e3-4eb4-ab12-943a4be90837": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
},
"39f0feef-a8f2-48c6-8ebe-3293bc49aaef": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
}
}
},
"identityMap": {
"ecid": [{
"id": "08130494355355215032117568021714632048"
}]
}
}]
```

Reemplace el código del index.js de su código de Visual Studio por el código siguiente. Este código se ejecutará cada vez que Real-time CDP envíe las cualificaciones de audiencia a su destino de centro de eventos. En nuestro ejemplo, el código trata solo de mostrar y mejorar la carga útil recibida. Pero puede imaginar cualquier tipo de función para procesar cualificaciones de audiencia en tiempo real.

```javascript
// Marc Meewis - Solution Consultant Adobe - 2020
// Adobe Experience Platform Enablement - Module 2.4

// Main function
// -------------
// This azure function is fired for each audience activated to the Adobe Exeperience Platform Real-time CDP Azure 
// Eventhub destination
// This function enriched the received audience payload with the name of the audience. 
// You can replace this function with any logic that is require to process and deliver
// Adobe Experience Platform audiences in real-time to any application or platform that 
// would need to act upon an AEP audience qualification.
// 

module.exports = async function (context, eventHubMessages) {

    return new Promise (function (resolve, reject) {

        context.log('Message : ' + JSON.stringify(eventHubMessages, null, 2));

        resolve();

    });    

};
```

El resultado debería ser similar al siguiente:

![3-16b-vsc-edit-index-js.png](./images/vsc1.png)

## Ejecutar proyecto de Azure

Ahora es el momento de ejecutar su proyecto. En esta fase no implementaremos el proyecto en Azure. Lo ejecutaremos localmente en modo de depuración. Seleccione el icono Ejecutar y haga clic en la flecha verde.

![3-17-vsc-run-project.png](./images/vsc14.png)

La primera vez que ejecute el proyecto en modo de depuración, deberá adjuntar una cuenta de almacenamiento de Azure, hacer clic en **Seleccionar cuenta de almacenamiento** y, a continuación, seleccionar la cuenta de almacenamiento que creó anteriormente, que se denomina `--aepUserLdap--aepstorage`.

El proyecto ya está en funcionamiento y se está mostrando para eventos en el centro de eventos. En el siguiente ejercicio demostrará el comportamiento en el sitio web de demostración de CitiSignal, que le cualificará para recibir audiencias. Como resultado, recibirá una carga útil de calificación de audiencia en el terminal de su función de déclencheur del centro de eventos.

![3-24-vsc-application-stop.png](./images/vsc18.png)

## Detener proyecto de Azure

Para detener el proyecto, ve al menú **CALL STACK** en VSC, haz clic en la flecha del proyecto en ejecución y luego haz clic en **Detener**.

![3-24-vsc-application-stop.png](./images/vsc17.png)

Paso siguiente: [2.4.7 Escenario de extremo a extremo](./ex7.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
