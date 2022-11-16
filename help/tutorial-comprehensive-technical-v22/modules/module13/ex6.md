---
title: 'Activación de segmentos en el centro de eventos de Microsoft Azure: acción'
description: 'Activación de segmentos en el centro de eventos de Microsoft Azure: acción'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 989dd2e4-597b-4b80-8b17-41aa6929ed64
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 13.6 Situación de extremo a extremo

## 13.6.1 Iniciar el déclencheur del centro de eventos de Azure

Para mostrar la carga útil que envía CDP en tiempo real de Adobe Experience Platform a nuestro Azure Event Hub tras la calificación de segmentos, debemos iniciar nuestra sencilla función de déclencheur de Azure Event Hub. Esta función simplemente &quot;volcará&quot; la carga útil a la consola en Visual Studio Code. Sin embargo, recuerde que esta función se puede ampliar de cualquier manera a la interfaz con todo tipo de entornos utilizando API y protocolos específicos.

### Iniciar código de Visual Studio e iniciar proyecto

Asegúrese de que el proyecto de código de Visual Studio esté abierto y en ejecución

Para iniciar/detener/reiniciar su función de Azure en Visual Studio Code, consulte los siguientes ejercicios:

- [Ejercicio 13.5.4: Iniciar proyecto de Azure](./ex5.md)
- [Ejercicio 13.5.5: Detener proyecto de Azure](./ex5.md)

El código de Visual Studio **Terminal** debería mencionar algo similar a esto:

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 13.6.2 Carga del sitio web de Luma

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../module0/images/web8.png)

Ahora puede seguir el flujo siguiente para acceder al sitio web. Haga clic en **Integraciones**.

![DSN](../module0/images/web1.png)

En el **Integraciones** , debe seleccionar la propiedad Recopilación de datos que se creó en el ejercicio 0.1.

![DSN](../module0/images/web2.png)

Verá que su sitio web de demostración se abre. Seleccione la dirección URL y cópiela en el portapapeles.

![DSN](../module0/images/web3.png)

Abra una nueva ventana del explorador incógnito.

![DSN](../module0/images/web4.png)

Pegue la dirección URL del sitio web de la demostración, que copió en el paso anterior. A continuación, se le pedirá que inicie sesión con su Adobe ID.

![DSN](../module0/images/web5.png)

Seleccione su tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../module0/images/web6.png)

Verá su sitio web cargado en una ventana del navegador incógnito. Para cada demostración, tendrá que usar una ventana nueva del explorador incógnito para cargar la URL de su sitio web de demostración.

![DSN](../module0/images/web7.png)

## 13.6.3 Cumpla los requisitos para su segmento de interés en equipos

Vaya a la **Equipo** una vez, y **no volver a cargar ni actualizar**. Esta acción debería calificarle para su `--demoProfileLdap-- - Interest in Equipment` segmento.

![6-04-luma-telco-nav-sport.png](./images/luma1.png)

Para verificarlo, abra el panel Visor de perfiles . Ahora debe ser miembro de `--demoProfileLdap-- - Interest in Equipment`. Si las suscripciones a los segmentos aún no se han actualizado en el panel Visor de perfiles, haga clic en el botón de recarga.

![6-05-luma-telco-nav-banda ancha.png](./images/luma2.png)

Vuelva al código de Visual Studio y observe su **TERMINAL** , debería ver una lista de segmentos para su **ECID**. Esta carga útil de activación se envía a su centro de eventos en cuanto cumpla los requisitos para `--demoProfileLdap-- - Interest in Equipment` segmento.

Cuando observa más de cerca la carga útil del segmento, puede ver que `--demoProfileLdap-- - Interest in Equipment` está en estado **realizado**.

Un estado de segmento de **realizado** significa que nuestro perfil acaba de entrar en el segmento. Mientras que la variable **existente** status significa que nuestro perfil sigue estando en el segmento.

![6-06-vsc-activation-performed.png](./images/luma3.png)

## 13.6.4 Visite la página Equipo por segunda vez

Realice una actualización de la variable **Equipo** página.

![6-07-back-to-sport.png](./images/luma1.png)

Ahora, vuelva al código de Visual Studio y verifique su **TERMINAL** pestaña . Verá que todavía tenemos su segmento, pero ahora en estado **existente** lo que significa que nuestro perfil sigue estando en el segmento.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 13.6.5 Visite la página de deportes por tercera vez

Si desea volver a consultar la **Deportes** por tercera vez, no se realizará ninguna activación, ya que no hay ningún cambio de estado desde el punto de vista de un segmento.

Las activaciones de segmentos solo se producen cuando cambia el estado del segmento:

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../overview.md)
