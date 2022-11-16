---
title: 'Adobe Journey Optimizer: configuración de un recorrido basado en lotes'
description: En esta sección puede configurar un recorrido de correo electrónico por lotes para enviar una newsletter
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 761da5b4-682f-430b-951c-278302fc4c54
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 8%

---

# 10.2 Configuración de un recorrido de newsletter basado en lotes

Inicie sesión en Adobe Journey Optimizer desde [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Se le redirigirá al **Página principal**  en Journey Optimizer. En primer lugar, asegúrese de que está utilizando el simulador para pruebas correcto. El entorno limitado que se va a usar se denomina `--aepSandboxId--`. Para cambiar de un simulador de pruebas a otro, haga clic en **PRODUCCIÓN (VA7)** y seleccione el simulador de pruebas de la lista. En este ejemplo, el simulador de pruebas recibe el nombre **Habilitación de AEP para el año fiscal 22**. Entonces estará en el **Página principal** vista del entorno limitado `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.2.1 Crear recorrido de newsletter

Ahora creará un recorrido basado en lotes. A diferencia del recorrido basado en eventos del ejercicio anterior, que se basa en eventos de experiencia entrantes o entradas o salidas de segmentos para obtener un recorrido para un cliente específico, los recorridos basados en lotes se dirigen a todo un segmento una vez con contenido único, como boletines informativos, promociones excepcionales o información genérica, o periódicamente con contenido similar enviado de forma regular, como por ejemplo campañas de cumpleaños y recordatorios.

En el menú , vaya a **Recorridos** y haga clic en **Crear Recorrido**.

![Journey Optimizer](./images/oc43.png)

A la derecha, verá un formulario en el que debe especificar el nombre y la descripción del recorrido. Introduzca los siguientes valores:

- **Nombre**: `--demoProfileLdap-- - Newsletter Journey`. Por ejemplo: **vangeluw: Recorrido del boletín**.
- **Descripción**: Boletín mensual

Haga clic en **Ok**.

![Journey Optimizer](./images/batchj2.png)

En **Organización**, arrastrar y soltar **Leer segmento** en el lienzo. Esto significa que, una vez publicado, el recorrido empezará recuperando la audiencia de segmento completa, que luego se convierte en la audiencia objetivo del recorrido y el mensaje. Haga clic en **Seleccionar un segmento**.

![Journey Optimizer](./images/batchj3.png)

En el **Elegir un segmento** ventana emergente, busque su LDAP y seleccione el segmento que ha creado en [Módulo 6 - CDP en tiempo real: genere un segmento y tome medidas](../module6/real-time-cdp-build-a-segment-take-action.md) named `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. por ejemplo: vangeluw - Interés en PROTEUS FITNESS JACKSHIRT. Haga clic en **Guardar**.

![Journey Optimizer](./images/batchj5.png)

Haga clic en **Ok**.

![Journey Optimizer](./images/batchj6.png)

En el menú de la izquierda, busque la **Acciones** y arrastre y suelte una **Correo electrónico** en el lienzo.

![Journey Optimizer](./images/batchj7.png)

Configure las variables **Categoría** a **Marketing** y seleccione una superficie de correo electrónico que le permita enviar correos electrónicos. En este caso, la superficie de correo electrónico que se va a seleccionar es **Correo electrónico**. Asegúrese de que las casillas de verificación de **Clics en correos electrónicos** y **aperturas por correo electrónico** están activadas.

![ACOP](./images/journeyactions1eee.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

Ahora ven esto. Haga clic en el **Línea de asunto** campo de texto.

![Journey Optimizer](./images/batch4.png)

Escriba este texto para la línea de asunto: `Luma Newsletter - your monthly update has arrived.`. Haga clic en **Guardar**.

![Journey Optimizer](./images/batch5.png)

Volverás aquí. Haga clic en **Diseñador de correo electrónico** para empezar a crear el contenido del correo electrónico.

![Journey Optimizer](./images/batch6.png)

Entonces verás esto. Haga clic en **Importar HTML**.

![Journey Optimizer](./images/batch7.png)

En la pantalla emergente, deberá arrastrar y soltar el archivo HTML del correo electrónico. Puede encontrar la plantilla de HTML [here](../../assets/html/ajo-newsletter.html.zip). Descargue el archivo zip con la plantilla de HTML en su equipo local y descomprima el archivo en su equipo de escritorio.

![Journey Optimizer](./images/html1.png)

Arrastre y suelte el archivo **ajo-newsletter.html** para cargarlo en Journey Optimizer. Haga clic en **Importar**.

![Journey Optimizer](./images/batch8.png)

Este contenido de correo electrónico está listo para utilizarse, ya que tiene toda la personalización, las imágenes y el texto esperados. Solo el marcador de posición de oferta se deja vacío.

Podría recibir un mensaje de error: **Error al intentar recuperar recursos**. Esto está vinculado a la imagen del correo electrónico.

![Journey Optimizer](./images/errorfetch.png)

Si aparece este error, seleccione la imagen y haga clic en el botón **Editar imagen** botón.

![Journey Optimizer](./images/errorfetch1.png)

Haga clic en **Assets Essentials** para volver a la biblioteca de AEM Assets Essentials.

![Journey Optimizer](./images/errorfetch2.png)

Verá esta ventana emergente. Vaya a la carpeta . **enablement-assets** y seleccione la imagen **luma-newsletterContent.png**. Haga clic en **Seleccionar**.

![Journey Optimizer](./images/errorfetch3.png)

El correo electrónico básico del boletín ya está listo. Haga clic en **Guardar**.

![Journey Optimizer](./images/ready.png)

Vuelva al panel de mensajes haciendo clic en el **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/batch9.png)

Haga clic en la flecha situada en la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/oc79aeee.png)

Haga clic en **Ok** para cerrar la acción del correo electrónico.

![Journey Optimizer](./images/oc79beee.png)

El recorrido del boletín ya está listo para publicarse. Antes de hacerlo, observe la **Programación** , donde puede cambiar este recorrido de ser una única a una campaña recurrente. Haga clic en el **Programación** botón.

![Journey Optimizer](./images/batchj12.png)

Entonces verás esto. Select **Una vez**.

![Journey Optimizer](./images/sch1.png)

Seleccione una fecha y una hora para la hora siguiente y así poder probar el recorrido. Haga clic en **Ok**.

>[!NOTE]
>
>La fecha y la hora del envío del mensaje deben ser superiores a una hora.

Haga clic en **Publicación**.

![Journey Optimizer](./images/batchj13.png)

Haga clic en **Publicación** de nuevo.

![Journey Optimizer](./images/batchj14.png)

El recorrido básico del boletín ya está publicado. El mensaje de correo electrónico de la newsletter se enviará según lo definido en la programación y el recorrido se detendrá en cuanto se envíe el último correo electrónico.

![Journey Optimizer](./images/batchj14eee.png)

Ha terminado este ejercicio.

Paso siguiente: [10.3 Aplicar personalización en un mensaje de correo electrónico](./ex3.md)

[Volver al módulo 10](./journeyoptimizer.md)

[Volver a todos los módulos](../../overview.md)
