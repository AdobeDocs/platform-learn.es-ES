---
title: 'Adobe Journey Optimizer: Aplicar personalización en un mensaje de correo electrónico'
description: Este ejercicio explica cómo utilizar la personalización de segmentos dentro de un contenido de correo electrónico
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 573ecfba-4f1d-4242-8358-1d33109aaea3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 10%

---

# 10.3 Aplicar personalización en un mensaje de correo electrónico

Inicie sesión en Adobe Experience Cloud desde [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Adobe Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Se le redirigirá al **Página principal** en Journey Optimizer. Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepTenantId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla.

![ACOP](../module7/images/acoptriglp.png)

## 10.3.1 Personalización basada en segmentos

En este ejercicio, mejorará el mensaje de correo electrónico de la newsletter con un texto personalizado basado en la pertenencia a los segmentos.

Vaya a **Recorridos**. Busque el recorrido de boletín que ha creado en el ejercicio anterior. Buscar `--demoProfileLdap-- - Newsletter`. Haga clic en el recorrido para abrirlo.

![Journey Optimizer](./images/sbp1.png)

Entonces verás esto. Haga clic en **Duplicate**.

![Journey Optimizer](./images/sbp2.png)

Haga clic en ** Duplicar**.

![Journey Optimizer](./images/sbp3.png)

Seleccione su **Correo electrónico** acción y haga clic en **Editar contenido**.

![Journey Optimizer](./images/sbp3a.png)

Haga clic en **Diseñador de correo electrónico**.

![Journey Optimizer](./images/sbp4.png)

Entonces verás esto.

![Journey Optimizer](./images/sbp5.png)

Apertura **Componentes de contenido** y arrastre un **Texto** debajo del contenido de la newsletter actual.

![Journey Optimizer](./images/sbp6.png)

Seleccione todo el texto predeterminado y elimínelo. A continuación, haga clic en el **Añadir personalización** en la barra de herramientas.

![Journey Optimizer](./images/sbp7.png)

Verá esto:

![Journey Optimizer](./images/seg1.png)

En el menú de la izquierda, haga clic en **Pertenencia a segmentos**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Si no encuentra el segmento en esta lista, desplácese hacia abajo un poco para encontrar instrucciones sobre cómo recuperar el ID de segmento manualmente.

Seleccione el segmento `Luma - Women's Category Interest` y haga clic en el botón **+** , que debería tener este aspecto:

![Journey Optimizer](./images/seg3.png)

A continuación, debe dejar la primera línea tal cual y reemplazar las líneas 2 y 3 por este código:

``
Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

Entonces tendrá esto:

![Journey Optimizer](./images/seg4.png)

Haga clic en **Validar** para asegurarse de que el código es correcto. Haga clic en **Guardar**.

![Journey Optimizer](./images/sbp8.png)

Ahora puede guardar este mensaje haciendo clic en el botón **Guardar** en la esquina superior derecha. A continuación, haga clic en **Simular contenido**.

![Journey Optimizer](./images/sbp9.png)

Seleccione uno de los perfiles que ha creado como parte de este tutorial y haga clic en **Vista previa**. A continuación, verá el resultado de su configuración.

![Journey Optimizer](./images/sbp10.png)

Entonces verás esto. A continuación, haga clic en **Cerrar**.

![Journey Optimizer](./images/sbp10fff.png)

Vuelva al panel de mensajes haciendo clic en el **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/sbp11.png)

Haga clic en la flecha situada en la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/oc79afff.png)

Haga clic en **Ok** para cerrar la acción del correo electrónico.

![Journey Optimizer](./images/oc79bfff.png)

Cambie el **Programación** a **Una vez** y defina una **Fecha y hora**. Haga clic en **Ok**.

>[!NOTE]
>
>La fecha y la hora del envío del mensaje deben ser superiores a una hora.

![Journey Optimizer](./images/sbp18.png)

Haga clic en el **Publicación** en el recorrido.

![Journey Optimizer](./images/sbp19.png)

En la ventana emergente, haga clic en **Publicación** de nuevo.

![Journey Optimizer](./images/sbp20.png)

El recorrido básico del boletín ya está publicado. El mensaje de correo electrónico de la newsletter se enviará según la programación y el recorrido se detendrá en cuanto se envíe el último correo electrónico.

![Journey Optimizer](./images/sbp20fff.png)

Ha terminado este ejercicio.

Paso siguiente: [10.4 Configuración y uso de notificaciones push para iOS](./ex4.md)

[Volver al módulo 10](./journeyoptimizer.md)

[Volver a todos los módulos](../../overview.md)
