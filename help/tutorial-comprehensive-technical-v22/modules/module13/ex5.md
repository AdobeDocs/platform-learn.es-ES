---
title: 'Activación de segmentos en el centro de eventos de Microsoft Azure: definir una función de Azure'
description: 'Activación de segmentos en el centro de eventos de Microsoft Azure: definir una función de Azure'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b4a76dbc-bcea-47f6-bee3-889982f26ba8
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# 13.5 Crear su proyecto de Microsoft Azure

## 13.5.1 Familiarizarse con las funciones de Azure Event Hub

Funciones de Azure le permite ejecutar pequeños fragmentos de código (llamados **funciones**) sin preocuparse por la infraestructura de las aplicaciones. Con las funciones de Azure, la infraestructura de nube proporciona todos los servidores actualizados que necesita para mantener su aplicación en funcionamiento a escala.

Una función es **activado** por un tipo específico de evento. Los déclencheur admitidos incluyen responder a cambios en los datos, responder a mensajes (por ejemplo, centros de eventos), ejecutar una programación o como resultado de una solicitud HTTP.

Funciones de Azure es un servicio de computación sin servidor que le permite ejecutar código activado por evento sin tener que aprovisionar o administrar explícitamente infraestructura.

Azure Event Hubs se integra con las funciones de Azure para una arquitectura sin servidor.

## 13.5.2 Abrir código de Visual Studio e iniciar sesión en Azure

Visual Studio Code facilita...

- definir y enlazar funciones de Azure a centros de eventos
- probar localmente
- implementar en Azure
- ejecución de la función de registro remoto

### Abrir código de Visual Studio

Para abrir el código de Visual Studio, escriba **visual** en la búsqueda de su sistema operativo (Spotlight search on OSX, Search in Window&#39;s Taskbar). Si no lo encuentra, debe repetir los pasos descritos en [Ejercicio 0: requisitos previos](./ex0.md).

![visual-studio-code-icon.png](./images/visual-studio-code-icon.png)

### Iniciar sesión en Azure

Al iniciar sesión con su cuenta de Azure que utilizó para registrarse en [Ejercicio 0: requisitos previos](./ex0.md), el código de Visual Studio le permitirá encontrar y enlazar todos los recursos de Event Hub.

Haga clic en el **Azure** en el código de Visual Studio. Si no tiene esa opción, es posible que algo haya salido mal con la instalación de las extensiones requeridas.

Siguiente seleccione **Iniciar sesión en Azure**:

![3-01-vsc-open.png](./images/3-01-vsc-open.png)

Se le redirigirá al navegador para que inicie sesión. Recuerde seleccionar la cuenta de Azure que utilizó para registrarse.

![3-02-vsc-pick-account.png](./images/3-02-vsc-pick-account.png)

Cuando ve la siguiente pantalla en el explorador, ha iniciado sesión con Visual Code Studio:

![3-03-vsc-login-ok.png](./images/3-03-vsc-login-ok.png)

Vuelva a Visual Code Studio (verá el nombre de su suscripción de Azure, por ejemplo **suscripción de Azure 1**):

![3-04-vsc-logged-in.png](./images/3-04-vsc-logged-in.png)

## 13.5.3 Crear un proyecto de Azure

Cuando pasa el ratón por encima **suscripción de Azure 1**, aparece un menú encima de la sección , seleccione **Crear nuevo proyecto...**:

![3-05-vsc-create-project.png](./images/vsc2.png)

Seleccione una carpeta local de su elección para guardar el proyecto y haga clic en **Select**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

A continuación, entrará en el asistente para la creación del proyecto. Select **Javascript** como idioma del proyecto:

![3-07-vsc-select-language.png](./images/vsc4.png)

Select **Déclencheur de Azure Event Hub** como la primera plantilla de función del proyecto:

![3-08-vsc-function-template.png](./images/vsc5.png)

Escriba un nombre para la función, use el siguiente formato `--demoProfileLdap---aep-event-hub-trigger` y pulse Intro:

![3-09-vsc-function-name.png](./images/vsc6.png)

Select **Crear nueva configuración de aplicación local**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

Seleccione un área de nombres de centro de eventos, debería ver el centro de eventos definido en **Ejercicio 2**. En este ejemplo, el espacio de nombres de Event Hub es **vangeluw-aep-enablement**:

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

Seleccione el centro de eventos, debería ver el centro de eventos definido en **Ejercicio 2**. En mi caso, es **vangeluw-aep-enablement-event-hub**:

![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)

Select **RootManageSharedAccessKey** como política de Event Hub:

![3-13-vsc-function-select-eventhub-policy.png](./images/vsc10.png)

Escriba para usar **$Default**:

![3-14-vsc-eventhub-Consumer-group.png](./images/vsc11.png)

Select **Agregar al espacio de trabajo** sobre cómo abrir el proyecto:

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

Una vez creado el proyecto, haga clic en **index.js** para que el archivo se abra en el editor:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

La carga útil que envía Adobe Experience Platform a su centro de eventos incluirá los ID de segmento:

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

Reemplace el código en index.js de su código de Visual Studio por el código siguiente. Este código se ejecutará cada vez que CDP en tiempo real envíe cualificaciones de segmento a su destino de centro de eventos. En nuestro ejemplo, el código trata simplemente de mostrar y mejorar la carga útil recibida. Pero puede imaginar cualquier tipo de función para procesar las clasificaciones de segmentos en tiempo real.

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

El resultado debería ser así:

![3-16b-vsc-edit-index-js.png](./images/vsc1.png)

## 13.5.4 Ejecutar proyecto de Azure

Ahora es el momento de ejecutar el proyecto. En este momento no implementaremos el proyecto en Azure. Lo ejecutaremos localmente en modo de depuración. Seleccione el icono Ejecutar y haga clic en la flecha verde.

![3-17-vsc-run-project.png](./images/vsc14.png)

La primera vez que ejecute el proyecto en modo de depuración, deberá adjuntar una cuenta de almacenamiento de Azure y hacer clic en **Seleccionar cuenta de almacenamiento**.

![3-17-vsc-run-project.png](./images/vsc15.png)

En la lista de cuentas de almacenamiento, seleccione la que ha creado como parte de [13.1.4 Configurar su cuenta de almacenamiento de Azure](./ex1.md). El nombre de su cuenta de almacenamiento es `--demoProfileLdap--aepstorage`, por ejemplo: **mmeewisaepstorage**.

![3-22-vsc-select-storage-account.png](./images/vsc16.png)

El proyecto ya está en marcha y en ejecución, y está listado para eventos en el Centro de eventos. En el próximo ejercicio, demostrará el comportamiento en el sitio web de demostración de Luma que le calificará para esos segmentos. Como resultado, recibirá una carga útil de calificación de segmentos en la terminal de la función de déclencheur de Event Hub:

![3-23-vsc-application-started.png](./images/vsc17.png)

## 13.5.5 Detener proyecto de Azure

Para detener el proyecto, seleccione la opción **Terminal** , haga clic en la ventana de terminal y pulse **CMD-C** en OSX o **CTRL-C** en Windows:

![3-24-vsc-application-stop.png](./images/vsc18.png)

Paso siguiente: [13.6 Situación de extremo a extremo](./ex6.md)

[Volver al módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../overview.md)
