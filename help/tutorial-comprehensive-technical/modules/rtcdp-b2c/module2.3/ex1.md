---
title: 'CDP en tiempo real: cree un segmento y tome medidas; genere un segmento'
description: 'CDP en tiempo real: cree un segmento y tome medidas; genere un segmento'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# 2.3.1 Crear un segmento

En este ejercicio, creará un segmento utilizando el generador de segmentos de Adobe Experience Platform.

## 2.3.1.1 Contexto

En el mundo actual, responder al comportamiento de un cliente debe ser en tiempo real. Una de las formas de responder al comportamiento del cliente en tiempo real es mediante el uso de un segmento, con la condición de que el segmento se califique en tiempo real. En este ejercicio, debe crear un segmento que tenga en cuenta la actividad real en el sitio web que hemos estado utilizando.

## 2.3.1.2 Identificar el comportamiento al que desea reaccionar

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Ahora puede seguir el siguiente flujo para acceder al sitio web. Haga clic en **Integraciones**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

En la página **Integraciones**, debe seleccionar la propiedad de recopilación de datos que se creó en el ejercicio 0.1.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

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

En este ejemplo, desea responder a un cliente específico que ve un producto específico.
En la página de inicio de **Luma**, ve a **Hombres** y haz clic en el producto **PROTEUS FITNESS JACKSHIRT**.

![Ingesta de datos](./images/homenadia.png)

Así que cuando alguien visita la página de productos de **PROTEUS FITNESS JACKSHIRT**, querrás poder actuar. Lo primero que debe hacer para realizar una acción es definir un segmento.

![Ingesta de datos](./images/homenadiapp.png)

## 2.3.1.3 Creación del segmento

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Segmentos** y luego a **Examinar**, donde podrás ver una descripción general de todos los segmentos existentes. Haga clic en el botón **Crear segmento** para comenzar a crear un nuevo segmento.

![Segmentación](./images/menuseg.png)

Como se mencionó anteriormente, debe generar un segmento con todos los clientes que hayan visto el producto **PROTEUS FITNESS JACKSHIRT**.

Para crear este segmento, debe añadir un evento. Puede encontrar todos los eventos haciendo clic en el icono **Eventos** en la barra de menús **Segmentos**.

A continuación, verá el nodo **XDM ExperienceEvent** de nivel superior.

Para encontrar clientes que han visitado el producto **PROTEUS FITNESS JACKSHIRT**, haz clic en **XDM ExperienceEvent**.

![Segmentación](./images/findee.png)

Desplácese hacia abajo hasta **Elementos de lista de productos** y haga clic en él.

![Segmentación](./images/see.png)

Seleccione **Name** y arrastre y suelte el objeto **Name** del menú izquierdo de **Elementos de lista de productos** en el lienzo del generador de segmentos en la sección **Eventos**.

![Segmentación](./images/eewebpdtlname1.png)

El parámetro de comparación debe ser **igual a** y en el campo de entrada, escriba `PROTEUS FITNESS JACKSHIRT`.

![Segmentación](./images/pv.png)

Las **reglas de eventos** deben tener un aspecto similar al siguiente. Cada vez que agregue un elemento al generador de segmentos, puede hacer clic en el botón **Actualizar estimación** para obtener una nueva estimación de la población del segmento.

![Segmentación](./images/ldap4.png)

Por último, asigne un nombre al segmento y guárdelo.

Como convención de nombres, utilice:

- `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

El nombre del segmento debería tener un aspecto similar al siguiente:
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

A continuación, haga clic en el botón **Guardar y cerrar** para guardar el segmento.

![Segmentación](./images/segmentname.png)

A continuación, se le redirigirá a la página de resumen del segmento.

![Segmentación](./images/savedsegment.png)

Siguiente paso: [2.3.2 Revise cómo configurar el destino DV360 mediante Destinos](./ex2.md)

[Volver al módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../../overview.md)
