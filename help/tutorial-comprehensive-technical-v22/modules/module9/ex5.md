---
title: 'offer decisioning: use su decisión en un mensaje de correo electrónico'
description: Use su decisión en un mensaje de correo electrónico
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0fb8c244-1025-479f-b82e-374d1aa5e4dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 11%

---

# 9.5 Use su decisión en un mensaje de correo electrónico

En este ejercicio, utilizará su decisión para personalizar el envío de un correo electrónico y un SMS.

Vaya a **Recorridos**. Busque el recorrido que creó en el ejercicio 7.2, que se llama `--demoProfileLdap-- - Account Creation Journey`. Haga clic en el recorrido para abrirlo.

![Journey Optimizer](./images/emailoffer1.png)

Entonces verás esto. Haga clic en **Crear una nueva versión**.

![Journey Optimizer](./images/journey1.png)

Haga clic en **Crear una nueva versión**.

![Journey Optimizer](./images/journey2.png)

Haga clic en el **Correo electrónico** a continuación, haga clic en **Editar contenido**.

![Journey Optimizer](./images/journey3.png)

A continuación, verá el panel de mensajes. Haga clic en **Diseñador de correo electrónico**.

![Journey Optimizer](./images/emailoffer2.png)

Entonces verás esto.

![Journey Optimizer](./images/emailoffer5.png)

Entonces verás esto. Arrastre una nueva **Columna 1:1** estructura del componente en el lienzo.

![Journey Optimizer](./images/emailoffer6.png)

En el menú , vaya a **Componentes de contenido**. Seleccione el **Decisión de oferta** y arrastre y suelte este componente en el marcador de posición de oferta de contenido del correo electrónico como se indica. A continuación, haga clic en **Agregar**.

![Journey Optimizer](./images/emailoffer7.png)

Seleccione el tipo de colocación que desea incluir en el correo electrónico. En el **Ubicaciones** menú desplegable seleccionar **Correo electrónico: imagen** y, a continuación, seleccione su decisión `--demoProfileLdap-- - Luma Decision`. Haga clic en **Agregar**.

![Journey Optimizer](./images/emailoffer8.png)

Ahora ve todas las ofertas personalizadas y la oferta de reserva que se visualizan dentro del diseñador de correo electrónico. Haga clic en  **Simular contenido** para previsualizar el mensaje de correo electrónico con un perfil de cliente real.

![Journey Optimizer](./images/emailoffer9.png)

Comience por identificar qué perfil desea utilizar para la vista previa. Seleccione el **email** e introduzca la dirección de correo electrónico de un perfil de cliente que ha creado en el sitio web de demostración. A continuación, haga clic en **Vista previa**.

![Journey Optimizer](./images/emailoffer10.png)

Una vez que se haya mostrado el correo electrónico y la oferta se muestre correctamente, haga clic en el **Cerrar** botón.

![Journey Optimizer](./images/emailoffer11.png)

Finalmente, haga clic en **Guardar**.

![Journey Optimizer](./images/emailoffer12.png)

Ahora, haga clic en la flecha para volver a la pantalla anterior.

![Journey Optimizer](./images/emailoffer13.png)

Entonces verás esto. Haga clic en la flecha situada en la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/emailoffer14.png)

Haga clic en **Ok** para cerrar el **Correo electrónico** acción.

![Journey Optimizer](./images/emailoffer14a.png)

Haga clic en **Publicación** para publicar el recorrido actualizado.

![Journey Optimizer](./images/emailoffer14b.png)

Confirme haciendo clic en **Publicación** de nuevo.

![Journey Optimizer](./images/emailoffer15.png)

El mensaje ya está publicado.

![Journey Optimizer](./images/emailoffer16.png)

Al crear una cuenta nueva en el sitio web de demostración, ahora recibirá este correo electrónico:

![Journey Optimizer](./images/emailoffer17.png)

Ha terminado este ejercicio.

Paso siguiente: [9.6 Probar su decisión utilizando la API](./ex6.md)

[Volver al módulo 9](./offer-decisioning.md)

[Volver a todos los módulos](./../../overview.md)
