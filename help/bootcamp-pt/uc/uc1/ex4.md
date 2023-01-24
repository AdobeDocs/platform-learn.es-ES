---
title: Bootcamp - CDP en tiempo real - Construya un segmento y tome medidas - Envíe su segmento a Adobe Target - Brasil
description: Bootcamp - CDP en tiempo real - Construya un segmento y tome medidas - Envíe su segmento a Adobe Target - Brasil
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 1%

---

# 1.4 Acción: enviar el segmento a Adobe Target

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](./images/sb1.png)

## 1.4.1 Activar el segmento en el destino de Adobe Target

Adobe Target está disponible como destino en Real-Time CDP. Para configurar la integración de Adobe Target, vaya a **Destinos**, a **Catálogo**.

Haga clic en **Personalización** en el **Categorías** para abrir el Navegador. Verá el **Adobe Target** tarjeta de destino. Haga clic en **Activar segmentos**.

![AT](./images/atdest1.png)

Seleccione el destino ``Bootcamp Target`` y haga clic en **Siguiente**.

![AT](./images/atdest3.png)

En la lista de segmentos disponibles, seleccione el segmento que ha creado en [1.3 Crear un segmento](./ex3.md), cuyo nombre es `yourLastName - Interest in Real-Time CDP`. A continuación, haga clic en **Siguiente**.

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

## 1.4.2 Configurar la actividad basada en formularios de Adobe Target

Ahora que el segmento de Real-Time CDP está configurado para enviarse a Adobe Target, puede configurar la actividad de segmentación de experiencias en Adobe Target. En este ejercicio configurará una actividad basada en el Compositor de experiencias visuales.

Vaya a la página de inicio de Adobe Experience Cloud en [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Haga clic en **Target** para abrirlo.

![RTCDP](./images/excl.png)

En el **Adobe Target** página principal, verá todas las actividades existentes.
Haga clic en **+ Crear actividad** para crear una nueva actividad.

![RTCDP](./images/exclatov.png)

Select **Segmentación de experiencias**.

![RTCDP](./images/exclatcrxt.png)

Select **Visual** y establezca la variable **URL de actividad** a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, pero antes de hacerlo, sustituya XX por un número entre 01 y 30.

>[!IMPORTANT]
>
>Todos los participantes en la habilitación deben utilizar una página web independiente para evitar conflictos con las distintas experiencias de Adobe Target. Puede elegir una página web y encontrar la URL aquí: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas las páginas comparten la misma dirección URL base y finalizan en el número del participante.
>
>Por ejemplo, el participante 1 debe utilizar la URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, el participante 30 debe utilizar la URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Seleccionar el espacio de trabajo **AT Bootcamp**.

Haga clic en **Siguiente**.

![RTCDP](./images/exclatcrxtdtlform.png)

Ahora está en el Compositor de experiencias visuales. Puede tardar entre 20 y 30 segundos hasta que el sitio web esté completamente cargado.

![RTCDP](./images/atform1.png)

Actualmente, la audiencia predeterminada es **Todos los visitantes**. Haga clic en el **3 puntos** junto a **Todos los visitantes** y haga clic en **Cambiar audiencia**.

![RTCDP](./images/atform3.png)

Ahora está viendo la lista de audiencias disponibles, y el segmento de Adobe Experience Platform que creó anteriormente y envió a Adobe Target ahora forma parte de esta lista. Seleccione el segmento que ha creado anteriormente en Adobe Experience Platform. Haga clic en **Asignar audiencia**.

![RTCDP](./images/exclatvecchaud.png)

El segmento de Adobe Experience Platform ahora forma parte de esta actividad de segmentación de experiencias.

![RTCDP](./images/atform4.png)

Para poder cambiar la imagen a pantalla completa (hero), debe hacer clic en **Permitir todo** en el banner de la cookie.

Para ello, vaya a **Examinar**

![RTCDP](./images/cook1.png)

A continuación, haga clic en **Permitir todo**.

![RTCDP](./images/cook2.png)

A continuación, vuelva a **Componer**.

![RTCDP](./images/cook3.png)

Cambiemos ahora la imagen a pantalla completa en la página de inicio del sitio web. Haga clic en la imagen a pantalla completa predeterminada del sitio web y haga clic en **Reemplazar contenido** y, a continuación, seleccione **Imagen**.

![RTCDP](./images/atform5.png)

Buscar el archivo de imagen **rtcdp.png**. Selecciónelo y haga clic en **Guardar**.

![RTCDP](./images/atform6.png)

A continuación, verá la nueva experiencia con la nueva imagen para la audiencia seleccionada.

![RTCDP](./images/atform7.png)

Haga clic en el título de la actividad en la esquina superior izquierda para cambiarle el nombre.

![RTCDP](./images/exclatvecname.png)

Para el nombre, utilice:

- `yourLastName - RTCDP - XT (VEC)`

Haga clic en **Siguiente**.

![RTCDP](./images/atform8.png)

Haga clic en **Siguiente**.

![RTCDP](./images/atform8a.png)

En el **Objetivos y configuración** - página, vaya a **Métricas de objetivo**.

![RTCDP](./images/atform9.png)

Definir el objetivo principal como **Participación** - **Tiempo en el sitio**. Haga clic en **Guardar y cerrar**.

![RTCDP](./images/vec3.png)

Ahora estás en el **Información general de actividad** página. Aún necesita activar su actividad.

![RTCDP](./images/atform10.png)

Haga clic en el campo . **Inactivo** y seleccione **Activar**.

![RTCDP](./images/atform11.png)

A continuación, obtendrá una confirmación visual de que su actividad ya está activa.

![RTCDP](./images/atform12.png)

Su actividad ya está activa y se puede probar en el sitio web de bootcamp.

Si ahora vuelve al sitio web de demostración y visita la página del producto durante **Real-Time CDP**, calificará instantáneamente para el segmento que ha creado y verá que la actividad de Adobe Target se muestra en la página principal en tiempo real.

>[!IMPORTANT]
>
>Todos los participantes en la habilitación deben utilizar una página web independiente para evitar conflictos con las distintas experiencias de Adobe Target. Puede elegir una página web y encontrar la URL aquí: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas las páginas comparten la misma dirección URL base y finalizan en el número del participante.
>
>Por ejemplo, el participante 1 debe utilizar la URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, el participante 30 debe utilizar la URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Paso siguiente: [1.5 Acción: enviar el segmento a Facebook](./ex5.md)

[Volver al flujo de usuario 1](./uc1.md)

[Volver a todos los módulos](../../overview.md)
