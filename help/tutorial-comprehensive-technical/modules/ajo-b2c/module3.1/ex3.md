---
title: Actualizar el ID de configuración y probar el Recorrido
description: Actualizar el ID de configuración y probar el Recorrido
kt: 5342
doc-type: tutorial
exl-id: 6807f93d-bd44-4f63-8005-6819c9f5f1ed
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 3.1.3 Actualizar la propiedad de recopilación de datos y probar el recorrido

## 3.1.3.1 Actualizar la propiedad de recopilación de datos

Vaya a [Recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/launch/) y seleccione **Etiquetas**.

Esta es la página de Propiedades de recopilación de datos de Adobe Experience Platform que vio antes.

![Página de propiedades](./../../../modules/datacollection/module1.1/images/launch1.png)

En el módulo 0, Demo System creó dos propiedades de cliente para usted: una para el sitio web y otra para la aplicación móvil. Encuéntralos buscando `--aepUserLdap--` en el cuadro **[!UICONTROL Buscar]**. Haga clic para abrir la propiedad **Web**.

![Cuadro de búsqueda](./../../../modules/datacollection/module1.1/images/property6.png)

Entonces verá esto...

![Configuración de lanzamiento](./images/rule1.png)

En el menú de la izquierda, ve a **Reglas** y busca la regla **Registrar perfil**. Haga clic en la regla **Registrar perfil** para abrirla.

![Configuración de lanzamiento](./images/rule2.png)

A continuación, verá los detalles de esta regla. Haga clic para abrir la acción **Enviar &quot;Evento de registro&quot; a AEP - déclencheur JO**.

![Configuración de lanzamiento](./images/rule3.png)

Verá que, cuando se active esta acción, se utilizará un elemento de datos específico para definir la estructura de datos XDM. Debe actualizar ese elemento de datos y definir el **ID de evento** del evento que configuró en [Ejercicio 7.1](./ex1.md).

![Configuración de lanzamiento](./images/rule4.png)

Ahora necesita actualizar el elemento de datos **XDM - Evento de registro**. Para ello, vaya a **Elementos de datos**. Busque **XDM - Evento de registro** y haga clic para abrir ese elemento de datos.

![Configuración de lanzamiento](./images/rule5.png)

A continuación, verá esto:

![Configuración de lanzamiento](./images/rule6.png)

Vaya al campo `_experience.campaign.orchestration.eventID`. Elimine el valor actual y pegue su eventID allí.

Como recordatorio, el ID de evento se puede encontrar en Adobe Journey Optimizer en **Configuraciones > Eventos** y encontrará el ID de evento en la carga útil de ejemplo del evento, que tiene este aspecto: `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

Después de pegar el ID de evento, la pantalla debería tener este aspecto. A continuación, haga clic en **Guardar** o **Guardar en biblioteca**.

![Configuración de lanzamiento](./images/rule7.png)

Finalmente, debe publicar los cambios. Vaya a **Flujo de publicación** en el menú de la izquierda.

![Configuración de lanzamiento](./images/rule8.png)

Haga clic en **Agregar todos los recursos modificados** y, a continuación, haga clic en **Guardar y generar en desarrollo**.

![Configuración de lanzamiento](./images/rule9.png)

La biblioteca se actualizará y, después de uno o dos minutos, podrá probar la configuración.

## 3.1.3.2 Prueba del Recorrido

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada demostración, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

Haga clic en el Adobe del logotipo situado en la esquina superior izquierda de la pantalla para abrir el Visor de perfiles.

![Demostración](./../../../modules/datacollection/module1.2/images/pv1.png)

Eche un vistazo al panel Visor de perfiles y al Perfil del cliente en tiempo real con el **ID de Experience Cloud** como identificador principal de este cliente actualmente desconocido.

![Demostración](./../../../modules/datacollection/module1.2/images/pv2.png)

Vaya a la página Registrar/Iniciar sesión. Haga clic en **CREAR UNA CUENTA**.

![Demostración](./../../../modules/datacollection/module1.2/images/pv9.png)

Complete sus detalles y haga clic en **Registrarse** después de lo cual se le redirigirá a la página anterior.

![Demostración](./../../../modules/datacollection/module1.2/images/pv10.png)

Abra el panel Visualizador de perfiles y vaya a Perfil del cliente en tiempo real. En el panel Visor de perfiles, debería ver todos los datos personales que se muestran, como los identificadores de correo electrónico y teléfono que acaba de agregar.

![Demostración](./../../../modules/datacollection/module1.2/images/pv11.png)

1 minuto después de crear la cuenta, Adobe Journey Optimizer le enviará un correo electrónico para crearla.

![Configuración de lanzamiento](./images/email.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 3.1](./journey-orchestration-create-account.md)

[Volver a todos los módulos](../../../overview.md)
