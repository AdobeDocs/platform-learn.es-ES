---
title: 'Audience Activation a Microsoft Azure Event Hub: acción'
description: 'Audience Activation a Microsoft Azure Event Hub: acción'
kt: 5342
doc-type: tutorial
exl-id: f5b224bf-60b9-46e0-abdb-9d96a7e8c59f
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 2.4.7 Escenario de extremo a extremo

## Iniciar déclencheur de Azure Event Hub

Para mostrar la carga útil enviada por Adobe Experience Platform Real-time CDP a nuestro Azure Event Hub tras la calificación de audiencia, necesitamos iniciar nuestra función de déclencheur simple de Azure Event Hub. Esta función simplemente &quot;volcará&quot; la carga útil a la consola en Visual Studio Code. Pero recuerde que esta función se puede ampliar de cualquier manera para interactuar con todo tipo de entornos utilizando API y protocolos dedicados.

### Iniciar código de Visual Studio e iniciar proyecto

Asegúrese de que el proyecto de código de Visual Studio esté abierto y en ejecución

Para iniciar, detener o reiniciar la función de Azure en Visual Studio Code, consulte el ejercicio anterior.

El **Terminal** de su código de Visual Studio debe mencionar algo similar a esto:

```code
[2024-11-20T20:07:12.316Z] Debugger listening on ws://127.0.0.1:9229/86c8e251-8e2f-4c65-a063-cda77edbf2ca
[2024-11-20T20:07:12.318Z] For help, see: https://nodejs.org/en/docs/inspector
[2024-11-20T20:07:12.343Z] Worker process started and initialized.
[2024-11-20T20:07:12.359Z] Debugger attached.

Functions:

        vangeluw-aep-event-hub-trigger: eventHubTrigger

For detailed output, run func with --verbose flag.
[2024-11-20T20:07:18.150Z] Host lock lease acquired by instance ID '000000000000000000000000000C19D8'.
```

## Cargue su sitio web de Citi Signal

Vaya a [https://dsn.adobe.com](https://dsn.adobe.com). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en los 3 puntos **...** del proyecto del sitio web y, a continuación, haga clic en **Ejecutar** para abrirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada ejercicio, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

## Apto para su audiencia

Vaya a la página **Planes**. Esta acción lo calificará para la audiencia `--aepUserLdap-- - Interest in Plans`.

![6-04-luma-telco-nav-sports.png](./images/cs1.png)

Para verificarlo, abra el panel Visor de perfiles. Ahora debería ser miembro de `--aepUserLdap-- - Interest in Plans`. Si las suscripciones a audiencias aún no se han actualizado en el panel Visor de perfiles, haga clic en el botón Recargar.

![6-05-luma-telco-nav-broadband.png](./images/cs2.png)

Cambie a Visual Studio Code y observe su ficha **TERMINAL**; debería ver una lista de audiencias para su **ECID** específico. Esta carga de activación se envía a su centro de eventos en cuanto cumple los requisitos para la audiencia `--aepUserLdap-- - Interest in Plans`.

![6-06-vsc-activation-realizado.png](./images/cs3.png)

Si examina más de cerca la carga de la audiencia, verá que `--aepUserLdap-- - Interest in Plans` está en estado **realizado**.

```json
{
  "identityMap": {
    "ecid": [
      {
        "id": "36281682065771928820739672071812090802"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "94db5aed-b90e-478d-9637-9b0fad5bba11": {
        "createdAt": 1732129904025,
        "lastQualificationTime": "2024-11-21T07:33:52Z",
        "mappingCreatedAt": 1732130611000,
        "mappingUpdatedAt": 1732130611000,
        "name": "vangeluw - Interest in Plans",
        "status": "realized",
        "updatedAt": 1732129904025
      }
    }
  }
}
```

Un estado de audiencia de **realizado** significa que tu perfil forma parte de la audiencia, mientras que el estado de **saliente** significa que nuestro perfil se ha eliminado de la audiencia.

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
