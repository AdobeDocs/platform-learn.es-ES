---
title: 'Offer decisioning: utilice su decisión en un correo electrónico'
description: Usar su decisión en un correo electrónico
kt: 5342
doc-type: tutorial
source-git-commit: 91dbf1aac923c26608528b163bbd68218d45425b
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 1%

---

# 3.3.5 Usar su decisión en un correo electrónico

En este ejercicio, utilizará su decisión para personalizar el envío de un correo electrónico y un SMS.

Ir a **Recorridos**. Busque el recorrido que creó en el ejercicio 3.1.3, que se llama `--aepUserLdap-- - Registration Journey`. Haga clic en el recorrido para abrirlo.

![Journey Optimizer](./images/emailoffer1.png)

Entonces verá esto... Haga clic en **... Más** y luego haz clic en **Crear una nueva versión**.

![Journey Optimizer](./images/journey1.png)

Haga clic en **Crear una nueva versión**.

![Journey Optimizer](./images/journey2.png)

Haga clic en la acción **Correo electrónico** y, a continuación, haga clic en **Editar contenido**.

![Journey Optimizer](./images/journey3.png)

A continuación, verá el panel de mensajes. Haga clic en **Editar cuerpo del correo electrónico**.

![Journey Optimizer](./images/emailoffer2.png)

Entonces verá esto... Arrastre un nuevo componente de estructura **1:1 column** al lienzo.

![Journey Optimizer](./images/emailoffer6.png)

En el menú, ve a **Contenido**. Seleccione el componente **Offer decision** y arrastre y suelte este componente en el marcador de posición de la oferta de contenido del correo electrónico como se indica. A continuación, haga clic en **Agregar**.

![Journey Optimizer](./images/emailoffer7.png)

Seleccione el tipo de ubicación que desea incluir en el correo electrónico. En el menú desplegable **Ubicaciones**, seleccione **Correo electrónico - Imagen** y, a continuación, seleccione su decisión `--aepUserLdap-- - CitiSignal Decision`. Haga clic en **Agregar**.

![Journey Optimizer](./images/emailoffer8.png)

Ahora puede recorrer todas las ofertas personalizadas y la oferta de reserva, todas ellas visualizadas dentro del diseñador de correo electrónico. Haga clic en **Guardar**.

![Journey Optimizer](./images/emailoffer9.png)

A continuación, haga clic en la flecha para volver a la pantalla anterior.

![Journey Optimizer](./images/emailoffer13.png)

Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/emailoffer14.png)

Haga clic en **Guardar** para cerrar la acción **Enviar correo electrónico**.

![Journey Optimizer](./images/emailoffer14a.png)

Haga clic en **Publish** para publicar el recorrido actualizado.

![Journey Optimizer](./images/emailoffer14b.png)

Confirme haciendo clic de nuevo en **Publish**.

![Journey Optimizer](./images/emailoffer15.png)

El mensaje se ha publicado.

![Journey Optimizer](./images/emailoffer16.png)

Al crear una nueva cuenta en el sitio web de demostración, ahora recibe este correo electrónico:

![Journey Optimizer](./images/emailoffer17.png)

Ha terminado este ejercicio.

Paso siguiente: [3.3.6 Pruebe su decisión con la API](./ex6.md)

[Volver al módulo 3.3](./offer-decisioning.md)

[Volver a todos los módulos](./../../../overview.md)
