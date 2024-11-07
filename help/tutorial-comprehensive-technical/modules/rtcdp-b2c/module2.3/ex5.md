---
title: 'Real-time CDP: cree un segmento y tome medidas . Envíe su segmento a Adobe Target'
description: 'Real-time CDP: cree un segmento y tome medidas . Envíe su segmento a Adobe Target'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 3%

---

# 2.3.5 Tomar medidas: enviar el segmento a Adobe Target

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

## 2.3.5.1 Verificar su secuencia de datos

El destino de Adobe Target en Real-Time CDP está conectado a la secuencia de datos que se utiliza para introducir datos en la red perimetral de Adobe. Si desea configurar el destino de Adobe Target, primero debe comprobar si el conjunto de datos ya está habilitado para Adobe Target. Su secuencia de datos se configuró en [Ejercicio 0.2 Crear su secuencia de datos](./../../../modules/gettingstarted/gettingstarted/ex2.md) y se llamó `--aepUserLdap-- - Demo System Datastream`.

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) y haga clic en **Datastreams** o **Datastreams (Beta)**.

![Ingesta de datos](./images/atdestds1.png)

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

En Flujos de datos, busque su secuencia de datos denominada `--aepUserLdap-- - Demo System Datastream`. Haga clic en el conjunto de datos para abrirlo.

![Ingesta de datos](./images/atdestds3.png)

Verá esto, haga clic en **...** junto a **Adobe Experience Platform** y luego haga clic en **Editar**.

![Ingesta de datos](./images/atdestds4.png)

Marque las casillas de verificación de **Segmentación de Edge** y **Destinos de Personalization**. Haga clic en **Guardar**.

![Ingesta de datos](./images/atdestds4a.png)

A continuación, haga clic en **+ Agregar servicio**.

![Ingesta de datos](./images/atdestds4b.png)

Seleccione el servicio **Adobe Target**. Haga clic en **Guardar**.

![Ingesta de datos](./images/atdestds5.png)

El conjunto de datos está configurado para Adobe Target.

![Ingesta de datos](./images/atdestds5a.png)

## 2.3.5.2 Configuración del destino de Adobe Target

Adobe Target está disponible como destino en Real-Time CDP. Para configurar tu integración con Adobe Target, ve a **Destinos**, a **Catálogo**.

![A LAS](./images/atdest1.png)

Haga clic en **Personalization** en el menú **Categorías**. Verá la tarjeta de destino **Adobe Target**. Haga clic en **Activar segmentos** (o **Configurar** según su entorno).

![A LAS](./images/atdest2.png)

Según el entorno, es posible que tenga que hacer clic en **+ Configurar nuevo destino** para empezar a crear el destino.

![A LAS](./images/atdest3.png)

Entonces verá esto...

![A LAS](./images/atdest4.png)

En la pantalla **Configurar nuevo destino**, debe configurar dos cosas:

- Nombre: use el nombre `--aepUserLdap-- - Adobe Target (Web)`, que debería tener el siguiente aspecto: **vangeluw - Adobe Target (Web)**.
- ID de secuencia de datos: debe seleccionar la secuencia de datos que configuró en [Ejercicio 0.2 Crear la secuencia de datos](./../../../modules/gettingstarted/gettingstarted/ex2.md). El nombre de su secuencia de datos debe ser: `--aepUserLdap-- - Demo System Datastream`.

Haga clic en **Next**.

![A LAS](./images/atdest5.png)

En la pantalla siguiente, puede seleccionar una política de gobernanza. No es necesario seleccionar uno, en este caso no es necesario seleccionar uno, así que haga clic en **Crear**.

![A LAS](./images/atdest6.png)

El destino se habrá creado y se mostrará en la lista. Seleccione su destino y haga clic en **Siguiente** para comenzar a enviar segmentos a su destino.

![A LAS](./images/atdest7.png)

En la lista de segmentos disponibles, seleccione el segmento que creó en [Ejercicio 6.1 Crear un segmento](./ex1.md), que se llama `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. A continuación, haga clic en **Siguiente**.

![A LAS](./images/atdest8.png)

En la página siguiente, haz clic en **Siguiente**.

![A LAS](./images/atdest9.png)

Haga clic en **Finalizar**.

![A LAS](./images/atdest10.png)

El segmento ahora está activado para Adobe Target.

![A LAS](./images/atdest11.png)

>[!IMPORTANT]
>
>Cuando haya creado su destino de Adobe Target en Real-Time CDP, el destino puede tardar hasta una hora en estar activo. Este es un tiempo de espera único, debido a la configuración del back-end. Una vez que se haya completado el tiempo de espera de 1 hora inicial y la configuración del back-end, los segmentos Edge recién añadidos que se envíen al destino de Adobe Target estarán disponibles para la segmentación en tiempo real.

## 2.3.5.3 Configuración de la actividad basada en formularios de Adobe Target

Ahora que el segmento de Real-Time CDP está configurado para enviarse a Adobe Target, puede configurar la actividad de segmentación de experiencias en Adobe Target. En este ejercicio configurará una actividad basada en formularios.

Vaya a la página principal de Adobe Experience Cloud en [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Haga clic en **Destino** para abrirlo.

![RTCDP](./images/excl.png)

En la página de inicio de **Adobe Target**, verás todas las actividades existentes.

![RTCDP](./images/exclatov.png)

Haga clic en **+ Crear actividad** para crear una nueva actividad.

![RTCDP](./images/exclatcr.png)

Seleccione **Segmentación de experiencias**.

![RTCDP](./images/exclatcrxt.png)

Seleccione **Formulario** y seleccione **Sin restricciones de propiedad**. Haga clic en **Next**.

![RTCDP](./images/exclatcrxtdtlform.png)

Ahora está en el Compositor de actividades basadas en formularios.

![RTCDP](./images/atform1.png)

Para el campo **LOCATION 1**, seleccione **target-global-mbox**.

![RTCDP](./images/atform2.png)

La audiencia predeterminada es **Todos los visitantes**. Haz clic en **3 puntos** junto a **Todos los visitantes** y haz clic en **Cambiar audiencia**.

![RTCDP](./images/atform3.png)

Ahora está viendo la lista de audiencias disponibles y el segmento de Adobe Experience Platform que creó anteriormente y envió a Adobe Target ahora forma parte de esta lista. Seleccione el segmento que creó anteriormente en Adobe Experience Platform. Haga clic en **Asignar audiencia**.

![RTCDP](./images/exclatvecchaud.png)

El segmento de Adobe Experience Platform ahora forma parte de esta actividad de segmentación de experiencias.

![RTCDP](./images/atform4.png)

Ahora vamos a cambiar la imagen de héroe en la página principal del sitio web. Haga clic para abrir la lista desplegable junto a **Contenido predeterminado** y haga clic en **Crear oferta de HTML**.

![RTCDP](./images/atform5.png)

Pegue el siguiente código. A continuación, haga clic en **Siguiente**.

```javascript
<script>document.querySelector("#home > div > div > div > div > div.banner_img.d-none.d-lg-block > img").src="https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/ff92fdc3885972c0090ad5419e0ef4d4_Luma - Product - Proteus - Hero Banner.png"; document.querySelector(".banner_text > *").remove()</script>
```

![RTCDP](./images/atform6.png)

A continuación, verá la nueva experiencia con la nueva imagen para la audiencia seleccionada.

![RTCDP](./images/atform7.png)

Haga clic en el título de la actividad en la esquina superior izquierda para cambiarle el nombre.

![RTCDP](./images/exclatvecname.png)

Para el nombre, utilice:

- `--aepUserLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Haga clic en **Next**.

![RTCDP](./images/exclatvecnamenext.png)

En la página **Objetivos y configuración** - , ve a **Métricas de objetivos**.

![RTCDP](./images/atform9.png)

Establezca el objetivo principal en **Participación** - **Tiempo en el sitio**.

![RTCDP](./images/vec3.png)

Haga clic en **Guardar y cerrar**.

![RTCDP](./images/vecsave.png)

Ahora se encuentra en la página **Información general de actividad**. Aún debe activar su actividad.

![RTCDP](./images/atform10.png)

Haga clic en el campo **Inactivo** y seleccione **Activar**.

![RTCDP](./images/atform11.png)

A continuación, recibirá una confirmación visual de que la actividad está activa.

![RTCDP](./images/atform12.png)

La actividad ya está activa y se puede probar en el sitio web de demostración.

>[!IMPORTANT]
>
>Cuando haya creado su destino de Adobe Target en Real-Time CDP, el destino puede tardar hasta una hora en estar activo. Este es un tiempo de espera único, debido a la configuración del back-end. Una vez que se haya completado el tiempo de espera de 1 hora inicial y la configuración del back-end, los segmentos Edge recién añadidos que se envíen al destino de Adobe Target estarán disponibles para la segmentación en tiempo real.

Si ahora regresa a su sitio web de demostración y visita la página de producto de PROTEUS FITNESS JACKSHIRT, calificará instantáneamente para el segmento que creó y verá la actividad de Adobe Target en la página de inicio en tiempo real.

![RTCDP](./images/atform13.png)

Paso siguiente: [2.3.6 Audiencias externas](./ex6.md)

[Volver al módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../../overview.md)
