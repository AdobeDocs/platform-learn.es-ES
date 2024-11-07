---
title: 'Offer decisioning: utilice su decisión en un correo electrónico'
description: Usar su decisión en un correo electrónico
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 3.3.5 Usar su decisión en un correo electrónico

En este ejercicio, utilizará su decisión para personalizar el envío de un correo electrónico y un SMS.

Ir a **Recorridos**. Busque el recorrido que creó en el ejercicio 7.2, que se llama `--aepUserLdap-- - Account Creation Journey`. Haga clic en el recorrido para abrirlo.

![Journey Optimizer](./images/emailoffer1.png)

Entonces verá esto... Haga clic en **Crear una nueva versión**.

![Journey Optimizer](./images/journey1.png)

Haga clic en **Crear una nueva versión**.

![Journey Optimizer](./images/journey2.png)

Haga clic en la acción **Correo electrónico** y, a continuación, haga clic en **Editar contenido**.

![Journey Optimizer](./images/journey3.png)

A continuación, verá el panel de mensajes. Haga clic en **Enviar correo electrónico a Designer**.

![Journey Optimizer](./images/emailoffer2.png)

Entonces verá esto...

![Journey Optimizer](./images/emailoffer5.png)

Entonces verá esto... Arrastre un nuevo componente de estructura **1:1 column** al lienzo.

![Journey Optimizer](./images/emailoffer6.png)

En el menú, vaya a **Componentes de contenido**. Seleccione el componente **Offer decision** y arrastre y suelte este componente en el marcador de posición de la oferta de contenido del correo electrónico como se indica. A continuación, haga clic en **Agregar**.

![Journey Optimizer](./images/emailoffer7.png)

Seleccione el tipo de ubicación que desea incluir en el correo electrónico. En el menú desplegable **Ubicaciones**, seleccione **Correo electrónico - Imagen** y, a continuación, seleccione su decisión `--aepUserLdap-- - Luma Decision`. Haga clic en **Agregar**.

![Journey Optimizer](./images/emailoffer8.png)

Ahora verá todas las ofertas personalizadas y la oferta de reserva que se visualiza dentro del diseñador de correo electrónico. Haga clic en **Simular contenido** para obtener una vista previa del mensaje de correo electrónico con un perfil de cliente real.

![Journey Optimizer](./images/emailoffer9.png)

Comience por identificar qué perfil desea utilizar para la vista previa. Seleccione el área de nombres **email** e introduzca la dirección de correo electrónico de un perfil de cliente que haya creado en el sitio web de demostración. A continuación, haga clic en **Vista previa**.

![Journey Optimizer](./images/emailoffer10.png)

Una vez que el correo electrónico se haya mostrado y la oferta se muestre correctamente, haga clic en el botón **Cerrar**.

![Journey Optimizer](./images/emailoffer11.png)

Finalmente, haga clic en **Guardar**.

![Journey Optimizer](./images/emailoffer12.png)

A continuación, haga clic en la flecha para volver a la pantalla anterior.

![Journey Optimizer](./images/emailoffer13.png)

Entonces verá esto... Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/emailoffer14.png)

Haga clic en **Aceptar** para cerrar la acción **Enviar correo electrónico**.

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
