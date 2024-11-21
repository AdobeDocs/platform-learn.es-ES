---
title: 'Audience Activation de Microsoft Azure Event Hub: crear una audiencia'
description: 'Audience Activation de Microsoft Azure Event Hub: crear una audiencia'
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# 2.4.4 Crear una audiencia

## Introducción

Va a crear una audiencia sencilla:

- **Interés en planes** para los cuales los clientes calificarán cuando visiten la página de **Planes** del sitio web de demostración de CitiSignal.

### Es bueno saber

Real-time CDP almacenará en déclencheur una activación en un destino cuando cumpla los requisitos de una audiencia que forme parte de la lista de activación de ese destino. En ese caso, la carga útil de calificación de audiencia que se enviará a ese destino contendrá **todas las audiencias a las que califica su perfil de cliente**.

El objetivo de este módulo es mostrar que la calificación de audiencia del perfil del cliente se envía a su destino de centro de eventos en tiempo casi real.

### Estado de audiencia

Una calificación de audiencia en Adobe Experience Platform siempre tiene una propiedad **status** y puede ser una de las siguientes:

- **realizado**: esto indica una nueva calificación de audiencia
- **saliente**: esto indica que el perfil ya no cumple los requisitos para la audiencia

## Creación de la audiencia

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

Ir a **Audiencias**. Haga clic en el botón **+ Crear audiencia**.

![Ingesta de datos](./images/seg.png)

Seleccione **Generar regla** y haga clic en **Crear**.

![Ingesta de datos](./images/seg1.png)

Asigne un nombre a la audiencia `--aepUserLdap-- - Interest in Plans`, establezca el método de evaluación en **Edge** y agregue el nombre de página del evento de experiencia.

Haga clic en **Eventos** y arrastre y suelte **XDM ExperienceEvent > Web > Detalles de página web > Nombre**. Escriba **planes** como valor:

![4-05-create-ee-2.png](./images/405createee2.png)

Arrastre y suelte **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Escriba `--aepUserLdap--` como valor, establezca el parámetro de comparación en **contiene** y haga clic en **Publish**:

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

La audiencia se ha publicado.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

Paso siguiente: [2.4.5 Activar la audiencia](./ex5.md)

[Volver al módulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../../overview.md)
