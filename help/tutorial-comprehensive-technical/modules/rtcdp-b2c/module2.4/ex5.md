---
title: 'Activación de segmentos en Microsoft Azure Event Hub: definir una función de Azure'
description: 'Activación de segmentos en Microsoft Azure Event Hub: definir una función de Azure'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# 2.4.5 Crear su proyecto de Microsoft Azure

## 2.4.5.1 Familiarizarse con las funciones de Azure Event Hub

Azure Functions le permite ejecutar pequeños fragmentos de código (llamados **funciones**) sin tener que preocuparse por la infraestructura de la aplicación. Con Azure Functions, la infraestructura en la nube proporciona todos los servidores actualizados que necesita para mantener su aplicación ejecutándose a escala.

Una función está **desencadenada** por un tipo de evento específico. Los déclencheur admitidos son responder a cambios en los datos, responder a mensajes (por ejemplo, Event Hubs), ejecutarse en una programación o como resultado de una solicitud HTTP.

Azure Functions es un servicio de computación sin servidor que le permite ejecutar código activado por eventos sin tener que aprovisionar ni administrar explícitamente la infraestructura.

Azure Event Hubs se integra con Azure Functions para una arquitectura sin servidor.

## 2.4.5.2 Abrir código de Visual Studio e iniciar sesión en Azure

Visual Studio Code facilita la tarea de...

- definir y enlazar funciones de Azure a Event Hubs
- probar localmente
- implementar en Azure
- ejecución de función de registro remoto

### Abrir código de Visual Studio

Para abrir Visual Studio Code, escriba **visual** en la búsqueda del sistema operativo (Búsqueda destacada en OSX, Buscar en la barra de tareas de Windows). Si no lo encuentra, debe repetir los pasos descritos en [Ejercicio 0 - Requisitos previos](./ex0.md).

![visual-studio-code-icon.png](./images/visual-studio-code-icon.png)

### Iniciar sesión en Azure

Cuando inicia sesión con su cuenta de Azure que utilizó para registrarse en el [Ejercicio 0 - Requisitos previos](./ex0.md), el código de Visual Studio le permitirá encontrar y enlazar todos los recursos de Event Hub.

Haga clic en el icono **Azure** en Visual Studio Code. Si no tiene esa opción, es posible que haya habido un problema con la instalación de las extensiones requeridas.

A continuación, seleccione **Iniciar sesión en Azure**:

![3-01-vsc-open.png](./images/3-01-vsc-open.png)

Se le redirigirá a su explorador para iniciar sesión. Recuerde seleccionar la cuenta de Azure que utilizó para registrarse.

![3-02-vsc-pick-account.png](./images/3-02-vsc-pick-account.png)

Cuando vea la siguiente pantalla en el explorador, iniciará sesión con Visual Code Studio:

![3-03-vsc-login-ok.png](./images/3-03-vsc-login-ok.png)

Vuelva a Visual Code Studio (verá el nombre de su suscripción de Azure, por ejemplo **suscripción de Azure 1**):

![3-04-vsc-logged-in.png](./images/3-04-vsc-logged-in.png)

## 2.4.5.3 Crear un proyecto de Azure

Cuando pase el ratón sobre **Azure subscription 1**, aparecerá un menú encima de la sección, seleccione **Crear nuevo proyecto...**:

![3-05-vsc-create-project.png](./images/vsc2.png)

Seleccione una carpeta local de su elección para guardar el proyecto y haga clic en **Seleccionar**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

A continuación, se abrirá el asistente para la creación de proyectos. Seleccione **Javascript** como idioma para su proyecto:

![3-07-vsc-select-language.png](./images/vsc4.png)

Seleccione **déclencheur de Azure Event Hub** como primera plantilla de función del proyecto:

![3-08-vsc-function-template.png](./images/vsc5.png)

Escriba un nombre para la función, use el siguiente formato `--aepUserLdap---aep-event-hub-trigger` y presione Intro:

![3-09-vsc-function-name.png](./images/vsc6.png)

Seleccione **Crear nueva configuración de aplicación local**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

Seleccione un área de nombres de hub de eventos; debería ver el hub de eventos que definió en **Ejercicio 2**. En este ejemplo, el área de nombres del centro de eventos es **vangeluw-aep-enablement**:

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

Seleccione el centro de eventos, debería ver el centro de eventos que definió en **Ejercicio 2**. En mi caso, es **vangeluw-aep-enablement-event-hub**:

![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)

Seleccione **RootManageSharedAccessKey** como directiva del centro de eventos:

![3-13-vsc-function-select-eventhub-policy.png](./images/vsc10.png)

Escriba para usar **$Default**:

![3-14-vsc-eventhub-consumer-group.png](./images/vsc11.png)

Seleccione **Agregar al espacio de trabajo** sobre cómo abrir el proyecto:

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

Una vez creado el proyecto, haga clic en **index.js** para abrir el archivo en el editor:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

La carga útil enviada por Adobe Experience Platform a su centro de eventos incluirá los ID de segmento:

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

Reemplace el código del index.js de su código de Visual Studio por el código siguiente. Este código se ejecutará cada vez que Real-Time CDP envíe clasificaciones de segmentos a su destino de centro de eventos. En nuestro ejemplo, el código trata solo de mostrar y mejorar la carga útil recibida. Pero puede imaginar cualquier tipo de función para procesar cualificaciones de segmentos en tiempo real.

```javascript
// Marc Meewis - Solution Consultant Adobe - 2020
// Adobe Experience Platform Enablement - Module 13

// Main function
// -------------
// This azure function is fired for each segment activated to the Adobe Exeperience Platform Real-time CDP Azure 
// Eventhub destination
// This function enriched the received segment payload with the name fo the segment. 
// You can replace this function with any logic that is require to process and deliver
// Adobe Experience Platform segments in real-time to any application or platform that 
// would need to act upon an AEP segment qualiification.
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

## 2.4.5.4 Ejecutar proyecto de Azure

Ahora es el momento de ejecutar su proyecto. En esta fase no implementaremos el proyecto en Azure. Lo ejecutaremos localmente en modo de depuración. Seleccione el icono Ejecutar y haga clic en la flecha verde.

![3-17-vsc-run-project.png](./images/vsc14.png)

La primera vez que ejecute el proyecto en modo de depuración, tendrá que adjuntar una cuenta de almacenamiento de Azure y hacer clic en **Seleccionar cuenta de almacenamiento**.

![3-17-vsc-run-project.png](./images/vsc15.png)

En la lista de cuentas de almacenamiento, seleccione la que creó como parte de [13.1.4 Configurar su cuenta de almacenamiento de Azure](./ex1.md). Su cuenta de almacenamiento se llama `--aepUserLdap--aepstorage`, por ejemplo: **meewisaepstorage**.

![3-22-vsc-select-storage-account.png](./images/vsc16.png)

El proyecto ya está en funcionamiento y se está mostrando para eventos en el centro de eventos. En el siguiente ejercicio, se mostrará el comportamiento en el sitio web de demostración de Luma, que le permitirá acceder a esos segmentos. Como resultado, recibirá una carga útil de calificación de segmentos en el terminal de su función de déclencheur del centro de eventos:

![3-23-vsc-application-started.png](./images/vsc17.png)

## 2.4.5.5 Detener Azure Project

Para detener el proyecto, selecciona la ficha **Terminal**, haz clic en la ventana de terminal y presiona **CMD-C** en OSX o **CTRL-C** en Windows:

![3-24-vsc-application-stop.png](./images/vsc18.png)

Paso siguiente: [2.4.6 Escenario de extremo a extremo](./ex6.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
