---
title: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: Déclencheur el Recorrido de cliente orquestado'
description: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: Déclencheur el Recorrido de cliente orquestado'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# 3.2.5 Déclencheur de su recorrido

En este ejercicio, probará y almacenará en déclencheur el recorrido que configuró en este módulo.

## 3.2.5.1 Actualizar la configuración del evento de geovalla

Vaya a [Recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/launch/) y seleccione **Etiquetas**.

Esta es la página de Propiedades de recopilación de datos de Adobe Experience Platform que vio antes.

![Página de propiedades](./../../../modules/datacollection/module1.1/images/launch1.png)

En el módulo 0, Demo System creó dos propiedades de cliente para usted: una para el sitio web y otra para la aplicación móvil. Encuéntralos buscando `--aepUserLdap--` en el cuadro **[!UICONTROL Buscar]**. Haga clic para abrir la propiedad **Web**.

![Cuadro de búsqueda](./../../../modules/datacollection/module1.1/images/property6.png)

Entonces verá esto...

![Configuración de lanzamiento](./images/rule1.png)

En el menú de la izquierda, ve a **Reglas** y busca la regla **Evento de geoperímetro**. Haga clic en la regla **Evento de geoperímetro** para abrirla.

![Configuración de lanzamiento](./images/rule2.png)

A continuación, verá los detalles de esta regla. Haga clic para abrir la acción **Enviar &quot;evento de geovalla&quot; a AEP - déclencheur JO**.

![Configuración de lanzamiento](./images/rule3.png)

Verá que, cuando se active esta acción, se utilizará un elemento de datos específico para definir la estructura de datos XDM. Debe actualizar ese elemento de datos y definir el **ID de evento** del evento que configuró en el [Ejercicio 8.1](./ex1.md).

![Configuración de lanzamiento](./images/rule4.png)

Ahora necesita actualizar el elemento de datos **XDM - Evento de geoperímetro**. Para ello, vaya a **Elementos de datos**. Busque **XDM - Evento de geoperímetro** y haga clic para abrir ese elemento de datos.

![Configuración de lanzamiento](./images/rule5.png)

A continuación, verá esto:

![Configuración de lanzamiento](./images/rule6.png)

Vaya al campo `_experience.campaign.orchestration.eventID`. Elimine el valor actual y pegue su eventID allí.

Como recordatorio, el ID de evento se puede encontrar en Adobe Journey Optimizer en **Configuraciones > Eventos** y encontrará el ID de evento en la carga útil de ejemplo del evento, que tiene este aspecto: `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

A continuación, debe definir la ciudad en este elemento de datos. Vaya a **placeContext > ubicación geográfica > ciudad** y escriba la ciudad que desee. A continuación, haga clic en **Guardar** o **Guardar en biblioteca**.

![ACOP](./images/payloadeventIDgeo.png)

Finalmente, debe publicar los cambios. Vaya a **Flujo de publicación** en el menú de la izquierda.

![Configuración de lanzamiento](./images/rule8.png)

Haga clic en **Agregar todos los recursos modificados** y, a continuación, haga clic en **Guardar y generar en desarrollo**.

![Configuración de lanzamiento](./images/rule9.png)

## 3.2.5.2 Déclencheur de su recorrido

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

En la página **Screens**, haga clic en **Ejecutar**.

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

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

En el panel Visor de perfiles, haga clic en **UTILIDADES**. Escriba `geofenceevent` y haga clic en **Enviar**.

![Demostración](./images/smsdemo1.png)

Un par de segundos después, recibirá un SMS de Adobe Journey Optimizer.

![Demostración](./images/smsdemo4.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Volver a todos los módulos](../../../overview.md)
