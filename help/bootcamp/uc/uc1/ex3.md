---
title: Bootcamp - Perfil del cliente en tiempo real - Creación de una audiencia - IU
description: Bootcamp - Perfil del cliente en tiempo real - Creación de una audiencia - IU
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3 Crear una audiencia: IU

En este ejercicio, creará una audiencia utilizando el Generador de audiencias de Adobe Experience Platform.

## Historia

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, ve a **Audiencias**. En esta página, verá paneles con información esencial sobre el rendimiento de **Audience**.

![Segmentación](./images/menuseg.png)

Haz clic en **Examinar** para ver una descripción general de todas las audiencias existentes. Haga clic en el botón **+ Crear audiencia** para comenzar a crear una audiencia nueva.


![Segmentación](./images/segmentationui.png)

Aparecerá una ventana emergente que le preguntará si desea **&#39;Componer audiencia&#39;** o **&#39;Generar regla&#39;**. Elija **&#39;Generar regla&#39;** para continuar y haga clic en **crear**.

![Segmentación][def]

Una vez que esté en el generador de audiencias, verá inmediatamente la opción de menú **Atributos** y la referencia de **Perfil individual XDM**.


Dado que XDM es el lenguaje que potencia el negocio de la experiencia, XDM también es la base del generador de audiencias. Todos los datos que se incorporen en Platform deben asignarse a XDM y, como tales, todos los datos pasan a formar parte del mismo modelo de datos independientemente de dónde provengan. Esto le ofrece una gran ventaja a la hora de crear audiencias, ya que desde esta interfaz de usuario del generador de audiencias puede combinar datos de cualquier origen en el mismo flujo de trabajo. Las audiencias creadas en el Generador de audiencias se pueden enviar a soluciones como Adobe Target, Adobe Campaign o cualquier otro canal de activación.

Ahora necesita crear una audiencia de todos los clientes que han visto el producto **Real-Time CDP**.

Para crear esta audiencia, debe añadir un Evento de experiencia. Puede encontrar todos los eventos de experiencias haciendo clic en el icono **Eventos** en la barra de menús de **Campos**.

![Segmentación](./images/findee.png)

A continuación, verá el nodo **XDM ExperienceEvents** de nivel superior. Haga clic en **ExperienceEvent de XDM**.

![Segmentación](./images/see.png)

Vaya a **Elementos de lista de productos**.

![Segmentación](./images/plitems.png)

Seleccione **Name** y arrastre y suelte el objeto **Name** del menú de la izquierda en el lienzo del generador de audiencias en la sección **Events**. A continuación, verá esto:

![Segmentación](./images/eewebpdtlname.png)

El parámetro de comparación debe ser **igual a** y en el campo de entrada, ingrese **CDP en tiempo real**.

![Segmentación](./images/pv.png)

Cada vez que añada un elemento al generador de audiencias, puede hacer clic en el botón **Actualizar estimación** para obtener una nueva estimación de la población de su audiencia.

![Segmentación](./images/refreshest.png)

Como **método de evaluación**, seleccione **Edge**.

![Segmentación](./images/evedge.png)

Por último, pongamos un nombre a la audiencia y guárdela.

Como convención de nombres, utilice:

- `yourLastName - Interest in Real-Time CDP`

A continuación, haga clic en el botón **Guardar y cerrar** para guardar la audiencia.

![Segmentación](./images/segmentname.png)

Ahora se le redirigirá a la página de información general de audiencia, donde verá una vista previa de muestra de los perfiles de clientes que cumplen los requisitos para su audiencia.

![Segmentación](./images/savedsegment.png)

Ahora puede continuar con el siguiente ejercicio y utilizar la audiencia con Adobe Target.

Paso siguiente: [1.4 Realizar acción: enviar la audiencia a Adobe Target](./ex4.md)

[Volver al flujo de usuario 1](./uc1.md)

[Volver a todos los módulos](../../overview.md)


[def]: ./images/segmentationpopup.png
