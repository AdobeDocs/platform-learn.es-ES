---
title: Uso de la plantilla de medios dinámicos con Adobe Journey Optimizer
description: Uso de la plantilla de medios dinámicos con Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
source-git-commit: 261475b85bfb15f7e9f630d1c5203732c2d4c254
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 1.4.2 Uso de la plantilla de medios dinámicos con Adobe Journey Optimizer

## 1.4.2.1 Cree su campaña en Adobe Journey Optimizer

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

Ahora creará una campaña. A diferencia del recorrido basado en eventos del ejercicio anterior, que se basa en eventos de experiencia entrantes o entradas o salidas de audiencia para almacenar en déclencheur un recorrido para un cliente específico, las campañas se dirigen a una audiencia completa una vez con contenido único como boletines informativos, promociones únicas o información genérica, o periódicamente con contenido similar enviado de forma regular como, por ejemplo, campañas de cumpleaños y recordatorios.

En el menú, ve a **Campañas** y haz clic en **Crear campaña**.

![Journey Optimizer](./images/gsemail21.png)

Seleccione **Programado - Marketing** y haga clic en **Crear**.

![Journey Optimizer](./images/gsemail22.png)

En la pantalla de creación de campañas, configure lo siguiente:

- **Nombre**: `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`.

Haga clic en **Acciones**.

![Journey Optimizer](./images/gsemail23.png)

Haga clic en **+ Agregar acción** y luego seleccione **Correo electrónico**.

![Journey Optimizer](./images/gsemail24.png)

A continuación, seleccione una **configuración de correo electrónico** existente y haga clic en **Editar contenido**.

![Journey Optimizer](./images/gsemail25.png)

Entonces verá esto... Para la **línea de asunto**, use esto:

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

A continuación, haga clic en **Editar contenido**.

![Journey Optimizer](./images/gsemail26.png)

Seleccione **Diseño desde cero**.

![Journey Optimizer](./images/gsemail27.png)

Entonces debería ver esto.

![Journey Optimizer](./images/gsemail28.png)

Agregar 2x **1:1 columna** al lienzo.

![Journey Optimizer](./images/gsemail29.png)

Vaya a **Fragmentos**, arrastre el fragmento **encabezado** a la primera columna {1:1 y, a continuación, arrastre el fragmento **pie de página** a la segunda columna {1:1.

![Journey Optimizer](./images/gsemail30.png)

Agregue una nueva columna 1:1 entre los 2 fragmentos y, a continuación, agregue una **imagen** a esa columna 1:1. A continuación, haga clic en **Examinar**.

![Journey Optimizer](./images/gsemail31.png)

Vaya a la carpeta en la que ha almacenado la plantilla de Dynamic Media. Seleccione su plantilla de Dynamic Media y haga clic en **Seleccionar**.

![Journey Optimizer](./images/gsemail32.png)

Entonces debería ver esto.

![Journey Optimizer](./images/gsemail33.png)

## Pasos siguientes

Volver a [Adobe Experience Manager Assets y Dynamic Media](./aemassetsdm.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
