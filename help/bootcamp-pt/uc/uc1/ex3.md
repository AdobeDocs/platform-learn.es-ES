---
title: Bootcamp - Perfil del cliente en tiempo real - Crear un segmento - IU - Brasil
description: Bootcamp - Perfil del cliente en tiempo real - Crear un segmento - IU - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 3%

---

# 1.3 Crear un segmento: IU

En este ejercicio, creará un segmento utilizando el Generador de segmentos de Adobe Experience Platform.

## Historia

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, vaya a **Segmentos**. En esta página puede ver información general sobre todos los segmentos existentes. Haga clic en el **+ Crear segmento** para empezar a crear un segmento nuevo.

![Segmentación](./images/menuseg.png)

Una vez que esté en el nuevo generador de segmentos, inmediatamente verá la variable **Atributos** y **Perfil individual XDM** referencia.

![Segmentación](./images/segmentationui.png)

Dado que XDM es el idioma que impulsa el negocio de la experiencia, XDM también es la base del generador de segmentos. Todos los datos incorporados en Platform deben asignarse a XDM y, como tales, todos los datos pasan a formar parte del mismo modelo de datos independientemente de de la procedencia de dichos datos. Esto le ofrece una gran ventaja a la hora de crear segmentos, ya que desde esta interfaz de usuario del generador de segmentos puede combinar datos de cualquier origen en el mismo flujo de trabajo. Los segmentos creados dentro del Generador de segmentos se pueden enviar a soluciones como Adobe Target, Adobe Campaign y Adobe Audience Manager para su activación.

Ahora necesita crear un segmento de todos los clientes que han visto el producto **Real-Time CDP**.

Para crear este segmento, debe agregar un Evento de experiencia. Para encontrar todos los eventos de experiencias, haga clic en el icono **Eventos** en el **Campos** barra de herramientas.

![Segmentación](./images/findee.png)

A continuación, verá el nivel superior, **ExperienceEvents de XDM** nodo . Haga clic en **XDM ExperienceEvent**.

![Segmentación](./images/see.png)

Vaya a **Elementos de lista de productos**.

![Segmentación](./images/plitems.png)

Select **Nombre** y arrastre y suelte el **Nombre** del menú de la izquierda al lienzo del generador de segmentos en el **Eventos** para obtener más información. Verá esto:

![Segmentación](./images/eewebpdtlname.png)

El parámetro de comparación debe ser **es igual que** y en el campo de entrada, introduzca **CDP en tiempo real**.

![Segmentación](./images/pv.png)

Cada vez que agregue un elemento al Generador de segmentos, puede hacer clic en el botón **Actualizar estimación** para obtener una nueva estimación de la población en el segmento.

![Segmentación](./images/refreshest.png)

Como **Método de evaluación**, seleccione **Edge**.

![Segmentación](./images/evedge.png)

Finalmente, démosle un nombre al segmento y guárdelo.

Como convención de nomenclatura, utilice:

- `yourLastName - Interest in Real-Time CDP`

A continuación, haga clic en el **Guardar y cerrar** para guardar el segmento.

![Segmentación](./images/segmentname.png)

Volverá a la página de información general del segmento, donde verá una vista previa de muestra de perfiles de clientes que cumplen los requisitos para su segmento.

![Segmentación](./images/savedsegment.png)

Ahora puede continuar con el siguiente ejercicio y utilizar su segmento con Adobe Target.

Paso siguiente: [1.4 Acción: enviar el segmento a Adobe Target](./ex4.md)

[Volver al flujo de usuario 1](./uc1.md)

[Volver a todos los módulos](../../overview.md)
