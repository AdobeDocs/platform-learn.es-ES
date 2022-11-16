---
title: 'CDP en tiempo real: genere un segmento y realice una acción: Envíe su segmento a Adobe Target'
description: 'CDP en tiempo real: genere un segmento y realice una acción: Envíe su segmento a Adobe Target'
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7883cfa9-0119-47c2-a300-3ff0f741191a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 3%

---

# 6.5 Acción: enviar el segmento a Adobe Target

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepSandboxId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](../module2/images/sb1.png)

## 6.5.1 Verificar el almacén de datos

El destino de Adobe Target en Real-Time CDP está conectado al conjunto de datos que se utiliza para introducir datos en la red perimetral de Adobe. Si desea configurar el destino de Adobe Target, primero debe comprobar si el conjunto de datos ya está habilitado para Adobe Target. El datastram se configuró en [Ejercicio 0.2 Crear el conjunto de datos](./../module0/ex2.md) y se denominó `--demoProfileLdap-- - Demo System Datastream`.

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)y haga clic en **Datastreams** o **Datastreams (Beta)**.

![Ingesta de datos](./images/atdestds1.png)

En la esquina superior derecha de la pantalla, seleccione el nombre del simulador de pruebas, que debería ser `--aepSandboxId--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

En Datastreams, busque el conjunto de datos con el nombre `--demoProfileLdap-- - Demo System Datastream`. Haga clic en el conjunto de datos para abrirlo.

![Ingesta de datos](./images/atdestds3.png)

A continuación, verá esto, haga clic en **...** junto a **Adobe Experience Platform** y haga clic en **Editar**.

![Ingesta de datos](./images/atdestds4.png)

Marque las casillas de verificación para ambas **Segmentación de Edge** y **Destinos de personalización**. Haga clic en **Guardar**.

![Ingesta de datos](./images/atdestds4a.png)

A continuación, haga clic en **+ Añadir servicio**.

![Ingesta de datos](./images/atdestds4b.png)

Seleccione el servicio **Adobe Target**. Haga clic en **Guardar**.

![Ingesta de datos](./images/atdestds5.png)

El conjunto de datos ya está configurado para Adobe Target.

![Ingesta de datos](./images/atdestds5a.png)

## 6.5.2 Configurar su destino de Adobe Target

Adobe Target está disponible como destino en Real-Time CDP. Para configurar la integración de Adobe Target, vaya a **Destinos**, a **Catálogo**.

![AT](./images/atdest1.png)

Haga clic en **Personalización** en el **Categorías** para abrir el Navegador. Verá el **Adobe Target** tarjeta de destino. Haga clic en **Activar segmentos** (o **Configuración** según el entorno).

![AT](./images/atdest2.png)

Según el entorno, es posible que tenga que hacer clic en **+ Configurar nuevo destino** para empezar a crear su destino.

![AT](./images/atdest3.png)

Entonces verás esto.

![AT](./images/atdest4.png)

En el **Configurar nuevo destino** , debe configurar dos opciones:

- Nombre: use el nombre `--demoProfileLdap-- - Adobe Target (Web)`, que debería tener este aspecto: **vangeluw - Adobe Target (Web)**.
- ID de almacén de datos: debe seleccionar el conjunto de datos configurado en [Ejercicio 0.2 Crear el conjunto de datos](./../module0/ex2.md). El nombre del conjunto de datos debe ser: `--demoProfileLdap-- - Demo System Datastream`.

Haga clic en **Siguiente**.

![AT](./images/atdest5.png)

En la siguiente pantalla, puede seleccionar una directiva de control de forma opcional. No es necesario seleccionar uno, en este caso no es necesario seleccionar uno, por lo que haga clic en **Crear**.

![AT](./images/atdest6.png)

El destino se ha creado y se mostrará en la lista. Seleccione el destino y haga clic en **Siguiente** para empezar a enviar segmentos a su destino.

![AT](./images/atdest7.png)

En la lista de segmentos disponibles, seleccione el segmento en el que ha creado [Ejercicio 6.1 Crear un segmento](./ex1.md), cuyo nombre es `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. A continuación, haga clic en **Siguiente**.

![AT](./images/atdest8.png)

En la página siguiente, haga clic en **Siguiente**.

![AT](./images/atdest9.png)

Haga clic en **Finalizar**.

![AT](./images/atdest10.png)

El segmento ahora se activa para Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Cuando acaba de crear su destino de Adobe Target en Real-Time CDP, puede que tarde hasta una hora en estar activo el destino. Es un tiempo de espera único, debido a la configuración del servidor. Una vez que se haya completado la configuración inicial de 1 hora de espera y back-end, los segmentos Edge recién añadidos que se envíen al destino de Adobe Target estarán disponibles para su segmentación en tiempo real.

## 6.5.3 Configurar la actividad basada en formularios de Adobe Target

Ahora que el segmento de Real-Time CDP está configurado para enviarse a Adobe Target, puede configurar la actividad de segmentación de experiencias en Adobe Target. En este ejercicio debe configurar una actividad basada en formularios.

Vaya a la página de inicio de Adobe Experience Cloud en [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Haga clic en **Target** para abrirlo.

![RTCDP](./images/excl.png)

En el **Adobe Target** página principal, verá todas las actividades existentes.

![RTCDP](./images/exclatov.png)

Haga clic en **+ Crear actividad** para crear una nueva actividad.

![RTCDP](./images/exclatcr.png)

Select **Segmentación de experiencias**.

![RTCDP](./images/exclatcrxt.png)

Select **Formulario** y seleccione **Sin restricciones de propiedad**. Haga clic en **Siguiente**.

![RTCDP](./images/exclatcrxtdtlform.png)

Ahora se encuentra en el Compositor de actividades basadas en formularios.

![RTCDP](./images/atform1.png)

Para el campo **UBICACIÓN 1**, seleccione **target-global-mbox**.

![RTCDP](./images/atform2.png)

Actualmente, la audiencia predeterminada es **Todos los visitantes**. Haga clic en el **3 puntos** junto a **Todos los visitantes** y haga clic en **Cambiar audiencia**.

![RTCDP](./images/atform3.png)

Ahora está viendo la lista de audiencias disponibles, y el segmento de Adobe Experience Platform que creó anteriormente y envió a Adobe Target ahora forma parte de esta lista. Seleccione el segmento que ha creado anteriormente en Adobe Experience Platform. Haga clic en **Asignar audiencia**.

![RTCDP](./images/exclatvecchaud.png)

El segmento de Adobe Experience Platform ahora forma parte de esta actividad de segmentación de experiencias.

![RTCDP](./images/atform4.png)

Ahora vamos a cambiar la imagen principal en la página de inicio del sitio web. Haga clic en para abrir la lista desplegable junto a **Contenido predeterminado** y haga clic en **Crear oferta HTML**.

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

- `--demoProfileLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Haga clic en **Siguiente**.

![RTCDP](./images/exclatvecnamenext.png)

En el **Objetivos y configuración** - página, vaya a **Métricas de objetivo**.

![RTCDP](./images/atform9.png)

Definir el objetivo principal como **Participación** - **Tiempo en el sitio**.

![RTCDP](./images/vec3.png)

Haga clic en **Guardar y cerrar**.

![RTCDP](./images/vecsave.png)

Ahora estás en el **Información general de actividad** página. Aún necesita activar su actividad.

![RTCDP](./images/atform10.png)

Haga clic en el campo . **Inactivo** y seleccione **Activar**.

![RTCDP](./images/atform11.png)

A continuación, obtendrá una confirmación visual de que su actividad ya está activa.

![RTCDP](./images/atform12.png)

La actividad ya está activa y se puede probar en el sitio web de demostración.

>[!IMPORTANT]
>
>Cuando acaba de crear su destino de Adobe Target en Real-Time CDP, puede que tarde hasta una hora en estar activo el destino. Es un tiempo de espera único, debido a la configuración del servidor. Una vez que se haya completado la configuración inicial de 1 hora de espera y back-end, los segmentos Edge recién añadidos que se envíen al destino de Adobe Target estarán disponibles para su segmentación en tiempo real.

Si vuelve al sitio web de la demostración y visita la página del producto para PROTEUS FITNESS JACKSHIRT, calificará instantáneamente para el segmento que ha creado y verá que la actividad de Adobe Target se muestra en la página principal en tiempo real.

![RTCDP](./images/atform13.png)

Paso siguiente: [6.6 Audiencias externas](./ex6.md)

[Volver al módulo 6](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../overview.md)
