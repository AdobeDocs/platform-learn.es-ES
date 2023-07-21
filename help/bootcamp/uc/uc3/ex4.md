---
title: Bootcamp - Fusión física y digital - Pruebe su recorrido
description: Bootcamp - Fusión física y digital - Pruebe su recorrido
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 45c77177-9ea9-4c3d-a40e-c04a747938eb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# 3.4 Probar el recorrido

Para probar el recorrido, deberá utilizar el ID de evento del evento que creó en el ejercicio 3.2, que tiene este aspecto.

![ACOP](./images/payloadeventID.png)

El ID de evento es lo que debe enviarse a Adobe Experience Platform para almacenar el recorrido en déclencheur. En este ejemplo, el eventID es:
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Abra la aplicación móvil y vaya a la página principal. Haga clic en el icono **Configuración**.

![DSN](./images/appsett.png)

Pegue el ID de evento en el campo **EventID de señalización** y haga clic en **Guardar**.

![DSN](./images/beacon1.png)

Antes de continuar, abre esta página web en tu ordenador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

A continuación, verá esto:

![DSN](./images/screen1.png)

A continuación, vuelva a la página principal. Haga clic en **baliza** icono.

![DSN](./images/app23.png)

Entonces verá esto... Primero, seleccione **Señalización de pantalla de Bootcamp** y, a continuación, haga clic en **entrada** botón. Esto le permite simular una entrada de señalización.

![DSN](./images/app21.png)

Eche un vistazo a la pantalla de la tienda. Verá el último producto que vio aparecer allí en 5 segundos.

![DSN](./images/beacon3.png)

También ha recibido su notificación push.

![DSN](./images/beacon2.png)

Ya ha terminado este ejercicio.

[Volver al flujo de usuario 3](./uc3.md)

[Volver a todos los módulos](../../overview.md)
