---
title: 'Adobe Journey Optimizer: Aplicar personalización en un mensaje de correo electrónico'
description: Este ejercicio explica cómo utilizar la personalización de segmentos dentro de un contenido de correo electrónico
kt: 5342
doc-type: tutorial
exl-id: bb5f8130-0237-4381-bc1e-f6b62950b1fc
source-git-commit: 9865b5697abe2d344fb530636a1afc3f152a9e8f
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 3.4.3 Aplicar la personalización basada en segmentos en un mensaje de correo electrónico

Inicie sesión en Adobe Experience Cloud en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Adobe Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepTenantId--``.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.3.1 Personalización basada en segmentos

En este ejercicio mejorará el mensaje de correo electrónico de la newsletter que creó en el ejercicio anterior con un texto personalizado basado en el abono a segmentos.

Ir a **Campañas**. Busque el recorrido de la newsletter que ha creado en el ejercicio anterior. Busque `--aepUserLdap-- - CitiSignal Newsletter`. Haga clic con el botón derecho en los 3 puntos **...** y haga clic en **Duplicar**.

![Journey Optimizer](./images/sbp1.png)

Entonces verá esto... Use esto para **Title**: `--aepUserLdap-- - CitiSignal Newsletter (SBP)`. Haga clic en **Duplicate**.

![Journey Optimizer](./images/sbp2.png)

Haga clic en la campaña duplicada para abrirla.

![Journey Optimizer](./images/sbp3.png)

Haga clic en **Editar** para cambiar el contenido.

![Journey Optimizer](./images/sbp3a.png)

Haga clic en **Editar cuerpo del correo electrónico**.

![Journey Optimizer](./images/sbp4.png)

Entonces verá esto...

![Journey Optimizer](./images/sbp5.png)

Abra **Componentes de contenido** y arrastre una columna **1:1** sobre la oferta de AirPods.

![Journey Optimizer](./images/sbp6.png)

Arrastre y suelte un componente **Text** en esa columna 1:1.

![Journey Optimizer](./images/sbp6a.png)

Seleccione todo el texto predeterminado y elimínelo. A continuación, haga clic en el botón **Agregar personalización** de la barra de herramientas.

![Journey Optimizer](./images/sbp7.png)

Entonces verá esto... En el menú de la izquierda, haga clic en **Audiencias**.

![Journey Optimizer](./images/seg1.png)

Seleccione el segmento `--aepUserLdap-- - Interest in Plans` y haga clic en el icono **+** para agregarlo al lienzo.

![Journey Optimizer](./images/seg3.png)

A continuación, debe dejar la primera línea tal cual, y sustituir las líneas 2 y 3 por este código:

``
    PS: It may be a good idea to check if your plan still meets your needs! Click here to be contacted by one of our experts!
{%else%}
    PS: Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: NEWSLETTER10
{%/if%}
``

Entonces, tendrás esto. Haga clic en **Guardar**.

![Journey Optimizer](./images/seg4.png)

Cambie la alineación del texto a **Alineación central**.

![Journey Optimizer](./images/sbp9.png)

Ahora puedes guardar este mensaje haciendo clic en el botón **Guardar** en la esquina superior derecha. A continuación, haga clic en **flecha** junto al texto de la línea de asunto, en la esquina superior izquierda.

![Journey Optimizer](./images/sbp9a.png)

Haga clic en **Revisar para activar**.

![Journey Optimizer](./images/oc79afff.png)

Haga clic en **Activar**.

![Journey Optimizer](./images/oc79bfff.png)

Ya se ha publicado su newsletter con personalización basada en segmentos. El mensaje de correo electrónico de la newsletter se enviará en función de su programación y el recorrido se detendrá en cuanto se haya enviado el último correo electrónico.

Si cumple los requisitos para el segmento utilizado, verá esto en el correo electrónico que recibirá:

![Journey Optimizer](./images/sbp20fff.png)

Ha terminado este ejercicio.

Siguiente paso: [3.4.4 Configuración y uso de notificaciones push para iOS](./ex4.md)

[Volver al módulo 3.4](./journeyoptimizer.md)

[Volver a todos los módulos](../../../overview.md)
