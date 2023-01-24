---
title: Bootcamp - Journey Optimizer Crear su recorrido - Brasil
description: Bootcamp - Journey Optimizer Crear su recorrido - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---

# 2.4 Probar el recorrido

## Flujo de recorrido del cliente

Abra una ventana nueva, limpia y de incógnito del navegador y vaya a [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Haga clic en **Permitir todo**. Según el comportamiento de navegación en el flujo de usuarios anterior, verá que la personalización se produce en la página principal del sitio web.

![DSN](./images/web8a.png)

Haga clic en el **Perfil** en la esquina superior derecha de la pantalla.

![Demostración](./images/web8b.png)

Haga clic en **Crear una cuenta**.

![Demostración](./images/pv5.png)

Rellene todos los campos del formulario. Utilice un valor real para la dirección de correo electrónico y el número de teléfono, ya que se utilizará en ejercicios posteriores para el envío de correos electrónicos y SMS.

![Demostración](./images/pv7a.png)

Desplácese hacia abajo. Ahora necesita introducir el eventID del evento personalizado que ha creado en el ejercicio 2.2. Puede encontrarlo aquí:

![ACOP](./images/payloadeventID.png)

El ID de evento es lo que debe enviarse a Adobe Experience Platform para almacenar en déclencheur el recorrido que ha generado. Este es el eventID de este ejemplo: `19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f`

Complete el eventID en el campo **Su ID de evento de creación de cuenta** y haga clic en **Registro**.

![Demostración](./images/pv8a.png)

Entonces verás esto.

![Demostración](./images/pv9.png)

También recibirá este correo electrónico, que es el que usted mismo creó como parte de este ejercicio.

![Demostración](./images/pv10a.png)

Ya has terminado este ejercicio.

Paso siguiente: [2.5 Instalación y uso de la aplicación móvil](./ex5.md)

[Volver al flujo de usuario 2](./uc2.md)

[Volver a todos los módulos](../../overview.md)
