---
title: 'CDP en tiempo real: genere un segmento y realice una acción: genere un segmento'
description: 'CDP en tiempo real: genere un segmento y realice una acción: genere un segmento'
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: c0778e81-4282-433d-9e02-37e32bf370ef
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---

# 6.1 Crear un segmento

En este ejercicio, creará un segmento utilizando el generador de segmentos de Adobe Experience Platform.

## 6.1.1 Contexto

En el mundo actual, responder al comportamiento de un cliente debe ser en tiempo real. Una de las formas de responder al comportamiento de los clientes en tiempo real es mediante el uso de un segmento, con la condición de que el segmento esté cualificado en tiempo real. En este ejercicio, debe crear un segmento, teniendo en cuenta la actividad real en el sitio web que hemos estado utilizando.

## 6.1.2 Identifique el comportamiento al que desee reaccionar

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

En este ejemplo, desea responder a un cliente específico que está viendo un producto específico.
En el **Luma** página principal, vaya a **Hombres** y haga clic en el producto **MAZO DE CABLES DE LA PROTESTA**.

![Ingesta de datos](./images/homenadia.png)

Por lo tanto, cuando alguien visita la página del producto durante **MAZO DE CABLES DE LA PROTESTA**, desea poder realizar acciones. Lo primero que hay que hacer para actuar es definir un segmento.

![Ingesta de datos](./images/homenadiapp.png)

## 6.1.3 Crear el segmento

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepSandboxId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](../module2/images/sb1.png)

En el menú de la izquierda, vaya a **Segmentos** y vaya a **Examinar** donde puede ver información general sobre todos los segmentos existentes. Haga clic en el **Crear segmento** para empezar a crear un segmento nuevo.

![Segmentación](./images/menuseg.png)

Como se ha mencionado anteriormente, debe crear un segmento a partir de todos los clientes que han visto el producto **MAZO DE CABLES DE LA PROTESTA**.

Para crear este segmento, debe añadir un evento . Para encontrar todos los eventos, haga clic en el botón **Eventos** en el **Segmentos** barra de herramientas.

A continuación, verá el nivel superior **XDM ExperienceEvent** nodo .

Para encontrar clientes que hayan visitado la **MAZO DE CABLES DE LA PROTESTA** producto, haga clic en **XDM ExperienceEvent**.

![Segmentación](./images/findee.png)

Desplácese hacia abajo hasta **Elementos de lista de productos** y haga clic en ella.

![Segmentación](./images/see.png)

Select **Nombre** y arrastre y suelte el **Nombre** objeto de la izquierda **Elementos de lista de productos** del lienzo del generador de segmentos al **Eventos** para obtener más información.

![Segmentación](./images/eewebpdtlname1.png)

El parámetro de comparación debe ser **es igual que** y en el campo de entrada, introduzca `PROTEUS FITNESS JACKSHIRT`.

![Segmentación](./images/pv.png)

Su **Reglas de evento** debería verse así. Cada vez que agregue un elemento al Generador de segmentos, puede hacer clic en el botón **Actualizar estimación** para obtener una nueva estimación de la población en el segmento.

![Segmentación](./images/ldap4.png)

Finalmente, démosle un nombre al segmento y guárdelo.

Como convención de nomenclatura, utilice:

- `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

El nombre del segmento debería tener este aspecto:
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

A continuación, haga clic en el **Guardar y cerrar** para guardar el segmento.

![Segmentación](./images/segmentname.png)

Ahora volverá a la página de información general del segmento.

![Segmentación](./images/savedsegment.png)

Paso siguiente: [6.2 Revise cómo configurar el destino DV360 mediante destinos](./ex2.md)

[Volver al módulo 11](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../overview.md)
