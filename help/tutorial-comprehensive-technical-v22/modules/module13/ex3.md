---
title: 'Activación de segmentos en el centro de eventos de Microsoft Azure: crear un segmento de flujo continuo'
description: 'Activación de segmentos en el centro de eventos de Microsoft Azure: crear un segmento de flujo continuo'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: de3824bd-553c-4281-8edf-29abcc28a8e7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 13.3 Crear un segmento

## 13.3.1 Introducción

Creará un segmento simple:

- **Interés en equipos** para los que se calificarán los perfiles de cliente cuando visiten la variable **Equipamiento** página del sitio web de la demostración de Luma.

### Bien sabido

CDP en tiempo real déclencheur una activación a un destino cuando cumpla los requisitos para un segmento que forme parte de la lista de activación de ese destino. Cuando ese sea el caso, la carga útil de calificación de segmentos que se enviará a ese destino contendrá **todos los segmentos para los que su perfil califica**.

El objetivo de este módulo es mostrar que la calificación de segmentos de su perfil de cliente se envía a **your** destino del centro de eventos en tiempo real.

### Estado del segmento

Una calificación de segmento en Adobe Experience Platform siempre tiene un **status**-y puede ser una de las siguientes:

- **realizado**: esto indica una nueva calificación de segmento
- **existente**: esto indica una calificación de segmento existente
- **exitado**: esto indica que el perfil ya no cumple los requisitos para el segmento

## 13.3.2 Generación del segmento

La creación de un segmento se explica en detalle en [Módulo 6](../module6/real-time-cdp-build-a-segment-take-action.md).

### Crear segmento

Inicie sesión en Adobe Experience Platform accediendo a esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepSandboxId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar el simulador para pruebas apropiado, verá el cambio de pantalla y ahora estará en su simulador para pruebas dedicado.

![Ingesta de datos](../module2/images/sb1.png)

Vaya a **Segmentos**. Haga clic en el **+ Crear segmento** botón.

![Ingesta de datos](./images/seg.png)

Asigne un nombre al segmento `--demoProfileLdap-- - Interest in Equipment` y añada el evento experience de nombre de página:

Haga clic en **Eventos** y arrastrar y soltar **XDM ExperienceEvent > Web > Detalles de página web > Nombre**. Entrar **equipo** como valor:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Arrastrar y soltar **XDM ExperienceEvent > `--aepTenantIdSchema--` > demoEnvironment > brandName**. Entrar `--demoProfileLdap--` como valor, establezca el parámetro de comparación en **contains** y haga clic en **Guardar**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### Definición de PQL

El PQL del segmento tiene el siguiente aspecto:

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--demoProfileLdap--", false))])
```

Paso siguiente: [13.4 Activar segmento](./ex4.md)

[Volver al módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Volver a todos los módulos](./../../overview.md)
