---
title: Configuración de un recorrido con mensajes push
description: Configuración de un recorrido con mensajes push
kt: 5342
doc-type: tutorial
exl-id: 63d7ee24-b6b5-4503-b104-a345c2b26960
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---

# 3.3.2 Configuración de un recorrido con mensajes push

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.2.1 Crear un nuevo evento

En el menú de la izquierda, ve a **Configuraciones** y haz clic en **Administrar** en **Eventos**.

![ACOP](./images/acopmenu.png)

En la pantalla **Eventos**, verá una vista similar a esta. Haga clic en **Crear evento**.

![ACOP](./images/add.png)

A continuación, verá una configuración de evento vacía.
En primer lugar, asigne al evento un Nombre como este: `--aepUserLdap--StoreEntryEvent` y establezca la descripción en `Store Entry Event`.
A continuación se muestra la selección **Tipo de evento**. Seleccione **Unitario**.
A continuación se muestra la selección **Tipo de ID de evento**. Seleccione **Sistema generado**.

![ACOP](./images/eventname.png)

A continuación se muestra la selección Esquema. Se ha preparado un esquema para este ejercicio. Use el esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

Después de seleccionar el esquema, verá una serie de campos seleccionados en la sección **Carga útil**. Compruebe que el campo **Namespace** esté establecido en **ECID**. El evento está ahora completamente configurado.

Haga clic en **Guardar**.

![ACOP](./images/eventschema.png)

El evento se ha configurado y guardado. Vuelve a hacer clic en el evento para abrir de nuevo la pantalla **Editar evento**.

![ACOP](./images/eventdone.png)

Pase el ratón sobre el campo **Carga útil** y haga clic en el icono **Ver carga útil**.

![ACOP](./images/hover.png)

Ahora verá un ejemplo de la carga útil esperada.

Su evento tiene un identificador de evento de orquestación único, que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

El ID de evento es lo que debe enviarse a Adobe Experience Platform para almacenar en déclencheur el Recorrido que va a generar en el siguiente paso. Escriba este eventID, tal como lo necesitará en el paso siguiente.
`"eventID": "aa895251f76831e6440f169f1bb9d2a4388f0696d8e2782cfab192a275817dfa"`

Haga clic en **Ok**.

![ACOP](./images/payloadeventID.png)

Haga clic en **Cancelar**.

![ACOP](./images/payloadeventIDa.png)

## 3.3.2.2 Crear un recorrido

En el menú de la izquierda, ve a **Recorridos** y haz clic en **Crear Recorrido**.

![DSN](./images/sjourney1.png)

Entonces verá esto... Asigne un nombre al recorrido: `--aepUserLdap-- - Store Entry journey`. Haga clic en **Guardar**.

![DSN](./images/sjourney3.png)

En primer lugar, debe agregar el evento como punto de partida del recorrido. Busque el evento `--aepUserLdap--StoreEntryEvent`, arrástrelo y suéltelo en el lienzo. Haga clic en **Guardar**.

![DSN](./images/sjourney4.png)

A continuación, en **Acciones**, busque la acción **Push**. Arrastre y suelte la acción **Push** en el lienzo.

Establezca **Category** en **Marketing** y seleccione una superficie push que le permita enviar notificaciones push. En este caso, la superficie de correo electrónico que se va a seleccionar es **Push-iOS-Android**.

>[!NOTE]
>
>Debe existir un canal en Journey Optimizer que esté usando la **superficie de aplicación** tal como se revisó anteriormente.

![ACOP](./images/journeyactions1push.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2push.png)

Entonces verá esto... Haga clic en el icono **personalización** para el campo **Título**.

![Push](./images/bp5.png)

Entonces verá esto... Ahora puede seleccionar cualquier atributo de perfil directamente desde el Perfil del cliente en tiempo real.

Busque el campo **Nombre** y, a continuación, haga clic en el icono **+** situado junto al campo **Nombre**. Verá el token de personalización del nombre que se está agregando: **{{profile.person.name.firstName}}**.

![Push](./images/bp9.png)

A continuación, agregue el texto **, ¡bienvenido a nuestra tienda!** detrás de **{{profile.person.name.firstName}}**.

Haga clic en **Guardar**.

![Push](./images/bp10.png)

Ahora tiene esto. Haga clic en el icono **personalización** para el campo **Cuerpo**.

![Push](./images/bp11.png)

Escriba este texto **Haga clic aquí para obtener un descuento del 10% al comprar hoy.** y haga clic en **Guardar**.

![Push](./images/bp12.png)

Entonces, tendrás esto. Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/bp12a.png)

Haga clic en **Guardar** para cerrar la acción de inserción.

![DSN](./images/sjourney8.png)

Haga clic en **Publicar**.

![DSN](./images/sjourney10.png)

Vuelva a hacer clic en **Publicar**.

![DSN](./images/sjourney10a.png)

El recorrido se ha publicado.

![DSN](./images/sjourney11.png)

## 3.3.2.3 Actualizar la propiedad de recopilación de datos para dispositivos móviles

En **Introducción**, Sistema de demostración creó propiedades de etiquetas para usted: una para el sitio web y otra para la aplicación móvil. Encuéntralos buscando `--aepUserLdap--` en el cuadro **Buscar**. Haga clic para abrir la propiedad **Mobile**.

![DSN](./images/pushpoi1.png)

Entonces debería ver esto.

![DSN](./images/pushpoi2.png)

En el menú de la izquierda, ve a **Reglas** y haz clic para abrir la regla **Entrada de ubicación**.

![DSN](./images/pushpoi3.png)

Entonces debería ver esto. Haga clic en la acción **Núcleo móvil: adjuntar datos**.

![DSN](./images/pushpoi4.png)

Entonces debería ver esto.

![DSN](./images/pushpoi5.png)

Pegue el eventID del evento `--aepUserLdap--StoreEntryEvent` en la ventana **Carga JSON**. Haga clic en **Conservar cambios**.

![DSN](./images/pushpoi6.png)

Haga clic en **Guardar** o en **Guardar en biblioteca**.

![DSN](./images/pushpoi7.png)

Vaya a **Flujo de publicación** y haga clic para abrir la biblioteca **Principal**.

![DSN](./images/pushpoi8.png)

Haga clic en **Agregar todos los recursos modificados** y, a continuación, haga clic en **Guardar y generar en desarrollo**.

![DSN](./images/pushpoi9.png)

## 3.3.2.4: probar el recorrido y el mensaje push

Abra la aplicación **DSN Mobile**.

![DSN](./images/dxdemo1.png)

Vaya a la página **Localizador de tiendas**.

![DSN](./images/dxdemo2.png)

Haga clic en **Simular entrada de punto de interés**.

![DSN](./images/dxdemo3.png)

Después de un par de segundos, verá aparecer la notificación push.

![DSN](./images/dxdemo4.png)

## Pasos siguientes

Ir a [3.3.3 Configurar una campaña con mensajes en la aplicación](./ex3.md){target="_blank"}

Volver a [Adobe Journey Optimizer: mensajes push y en la aplicación](ajopushinapp.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}