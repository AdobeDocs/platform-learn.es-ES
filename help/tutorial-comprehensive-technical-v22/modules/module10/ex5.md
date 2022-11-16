---
title: 'Adobe Journey Optimizer: Eventos empresariales'
description: En esta sección se explica cómo utilizar la capacidad de eventos empresariales para realizar un caso de uso de "elemento de nuevo en existencias"
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: cc06d847-a405-4223-836c-c22ad6c9caca
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 8%

---

# 10.5 Crear un recorrido de evento empresarial

Inicie sesión en Adobe Journey Optimizer desde [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Se le redirigirá al **Página principal**  en Journey Optimizer. En primer lugar, asegúrese de que está utilizando el simulador para pruebas correcto. El entorno limitado que se va a usar se denomina `--aepSandboxId--`. Para cambiar de un simulador de pruebas a otro, haga clic en **PRODUCCIÓN (VA7)** y seleccione el simulador de pruebas de la lista. En este ejemplo, el simulador de pruebas recibe el nombre **Habilitación de AEP para el año fiscal 22**. Entonces estará en el **Página principal** vista del entorno limitado `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.5.1 Crear un evento empresarial

En el menú de la izquierda, haga clic en **Configuraciones**. Haga clic en el **Administrar** dentro del **Eventos** tarjeta.

![Journey Optimizer](./images/be1.png)

Los eventos comerciales son un nuevo tipo de evento que puede crear dentro de Journey Optimizer. A diferencia de **Unitario** que haya creado en módulos anteriores, el cliente no activa los eventos comerciales, sino la organización. Ahora creará su evento empresarial.

Haga clic en **Crear evento**.

![Journey Optimizer](./images/be2.png)

Introduzca los siguientes valores en el formulario Event creation :

- **Nombre**: `--demoProfileLdap--ItemBackInStock`. Por ejemplo: **vangeluwItemBackInStock**
- **Descripción**: Este evento se activa cuando un producto vuelve a estar en existencias
- **Tipo**: select **Empresa** en la lista desplegable

![Journey Optimizer](./images/evde.png)

Para el esquema, seleccione **Sistema de demostración: Esquema de eventos para eventos empresariales JO (Global v1.1) v.1**. Ahora debe seleccionar los campos del esquema que necesita para nuestro caso de uso.

![Journey Optimizer](./images/evdes.png)

Siga estos pasos:

Haga clic en el **lápiz** en el campo donde dice **1 campo seleccionado**.

![Journey Optimizer](./images/23.8-4.png)

Seleccione todos los campos disponibles en el esquema y haga clic en **OK**.

![Journey Optimizer](./images/23.8-5.png)

Para la condición : debe especificar qué registros de este esquema activarán el evento empresarial.

Siga estos pasos:

Haga clic en el **lápiz** en el campo donde dice **Añadir una condición**.

![Journey Optimizer](./images/23.8-6.png)

En el lado izquierdo, expanda el `--aepTenantId--` objeto, expandir el objeto **joBusinessEvents** y arrastre y suelte el campo **eventName** en el lienzo.

![Journey Optimizer](./images/23.8-7.png)

Para el campo **eventName**, introduzca el siguiente valor: `--demoProfileLdap--ItemBackInStock`. Por ejemplo: vangeluwItemBackInStock.
Haga clic en **Aceptar**.

![Journey Optimizer](./images/23.8-8.png)

Haga clic en **Aceptar**.

![Journey Optimizer](./images/23.8-9.png)

Finalmente, el formulario de creación de eventos debe tener este aspecto. Haga clic en **Guardar** para guardar el evento empresarial.

![Journey Optimizer](./images/23.8-10.png)

## 10.5.2 Crear un recorrido de evento empresarial

Ahora puede aprovechar este evento comercial y el mensaje dentro de un recorrido. Vaya a **Recorridos**. Haga clic en **Crear Recorrido**.

![Journey Optimizer](./images/bej10.png)

A la derecha, verá un formulario en el que debe especificar el nombre y la descripción del recorrido. Introduzca los siguientes valores:

- **Nombre**: `--demoProfileLdap-- - Item back in stock journey`. Por ejemplo: vangeluw - Elemento de vuelta en el recorrido de existencias
- **Descripción**: Este recorrido envía un SMS cuando un artículo vuelve a estar en existencias a los visitantes que han mostrado interés.

Haga clic en **Aceptar**.

![Journey Optimizer](./images/bej11.png)

En el menú de la izquierda, debajo de **Eventos**, busque su LDAP. Encontrará el evento comercial creado anteriormente `--demoProfileLdap--ItemBackInStock`. Arrastre y suelte este evento en el lienzo, ya que será el punto de partida del recorrido.

![Journey Optimizer](./images/bej12.png)

Como puede verse, una **Leer segmento** se ha añadido automáticamente al lienzo. Esto se debe a que los eventos empresariales solo envían un déclencheur para que el recorrido lea un segmento específico, que recuperará la lista de perfiles para ese recorrido.

Haga clic en el **Leer segmento** actividad.
La variable **Leer segmento** espera que seleccione el segmento al que desea notificar el evento comercial que acaba de ocurrir. Haga clic en el **Seleccionar un segmento** campo .

![Journey Optimizer](./images/bej13.png)

En el **Elegir un segmento** ventana emergente, busque su LDAP y seleccione el segmento que ha creado en [Módulo 6 - CDP en tiempo real: genere un segmento y tome medidas](../module6/real-time-cdp-build-a-segment-take-action.md) named `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. por ejemplo: vangeluw - Interés en PROTEUS FITNESS JACKSHIRT. Haga clic en **Guardar**.

![Journey Optimizer](./images/bej14.png)

A continuación, haga clic en **Ok**.

![Journey Optimizer](./images/bej15.png)

El siguiente paso es arrastrar y soltar la acción que queremos realizar en este recorrido. Seleccione la acción **SMS**, luego arrástrela y suéltela después de la condición que acaba de añadir.

![Demostración](./images/jop9.png)

Configure las variables **Categoría** a **Marketing** y seleccione una superficie sms que le permita enviar sms. En este caso, la superficie de correo electrónico que se va a seleccionar es **SMS**.

![ACOP](./images/journeyactions1x.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2x.png)

Ahora verá el panel de mensajes, donde puede configurar el texto del SMS. Haga clic en el **Componer mensaje** para crear el mensaje.

![Journey Optimizer](./images/sms3.png)

Escriba el siguiente texto: `Hi {{profile.person.name.firstName}}, the Proteus Fitness Jackshirt is back in stock at Luma.`. Haga clic en **Guardar**.

![Journey Optimizer](./images/sms4.png)

Vuelva al panel de mensajes haciendo clic en el **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/oc79xx.png)

Ahora verá la acción SMS completada. Haga clic en **Ok**.

![Journey Optimizer](./images/oc79xxy.png)

El recorrido ya está listo para publicarse. Haga clic en **Publicación**.

![Journey Optimizer](./images/jop13.png)

Haga clic en **Publicación** de nuevo.

![Journey Optimizer](./images/jop14.png)

El recorrido ya está publicado, ¡ahora puede probarlo!

![Journey Optimizer](./images/jop15.png)

## 10.5.3 Pruebe el recorrido de eventos empresariales

Ahora simulará la repoblación de un producto introduciendo un nuevo evento en el **Sistema de demostración: Esquema de eventos para eventos empresariales JO (Global v1.1) v.1** usar Postman.

En el menú de la izquierda, haga clic en **Fuentes** y haga clic en la **Cuentas** pestaña .

![Journey Optimizer](./images/s1.png)

En el **Cuentas** , encontrará la cuenta denominada **Eventos empresariales de Journey Optimizer**. Haga clic en él para abrirlo.

![Journey Optimizer](./images/s2.png)

Esta cuenta solo tiene un flujo de datos, haga clic en el nombre del flujo de datos para seleccionarlo.

![Journey Optimizer](./images/s3.png)

Haga clic en **Copiar carga útil de esquema** en el menú de la derecha. Esta opción copia todo el **curl** para insertar un registro en el **Sistema de demostración: Esquema de eventos para eventos empresariales JO (Global v1.1) v.1** al portapapeles.

![Journey Optimizer](./images/s4.png)

Pegar el comando Curl dentro de un editor de texto

![Journey Optimizer](./images/s5.png)

Analicemos más de cerca esta solicitud,

- La solicitud del POST se envía al ID de entrada de DCS
- La solicitud hace referencia al esquema, al conjunto de datos y al ID de organización.
- Finalmente, contiene el nodo xdmEntity que representa los datos que queremos crear dentro del conjunto de datos.

Ahora debe reemplazar lo siguiente `xdmEntity` línea...

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "string",
      "eventName": "string",
      "stockEventId": "string"
    }
  },
  "_id": "/uri-reference",
  "eventType": "advertising.completes",
  "timestamp": "2018-11-12T20:20:39+00:00"
}
```

...por esta línea, asegúrese de verificar el campo eventName como debería decir `--demoProfileLdap--ItemBackInStock`, que representa la condición especificada en el evento empresarial para almacenar en déclencheur el recorrido.

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "Product Proteus Fitness Jackshirt is back in stock",
      "eventName": "--demoProfileLdap--ItemBackInStock",
      "stockEventId": "1"
    }
  },
  "_id": "/uri-reference",
  "eventType": "productBackInStock",
  "timestamp": "2021-04-19T15:25:39+00:00"
}
```

El **curl** debe tener este aspecto:

![Journey Optimizer](./images/s6.png)

Seleccione todo y cópielo en el portapapeles.

Abra Postman. En el lado izquierdo de Postman, haga clic en **Importar**.

![Journey Optimizer](./images/23.8-46.png)

Seleccione el **Texto sin procesar** y pegue el comando copiado anteriormente aquí. Haga clic en **Continuar**.

![Journey Optimizer](./images/s7.png)

Haga clic en **Importar**.

![Journey Optimizer](./images/23.8-50.png)

Postman ha convertido automáticamente la variable **curl** en un comando REST listo para ser activado, simplemente presione la tecla **Enviar** para solicitar la creación de ese registro dentro del conjunto de datos.

![Journey Optimizer](./images/23.8-51.png)

Compruebe que la solicitud se ha recibido correctamente. Busque un **200 OK** en postman.

![Journey Optimizer](./images/s8.png)

El SMS puede tardar un par de minutos en llegar a su teléfono móvil. Si no es así, su **Interés en la funda protésica Fitness** es posible que el segmento no contenga un perfil con un teléfono móvil correcto. Si es así, vaya al sitio web de Luma, visite la **Chaqueta para el gimnasio Proteus** y regístrese asegurándose de proporcionar el número de teléfono móvil correcto.

![Journey Optimizer](./images/s9.png)

Ha terminado este ejercicio.

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 10](./journeyoptimizer.md)

[Volver a todos los módulos](../../overview.md)
