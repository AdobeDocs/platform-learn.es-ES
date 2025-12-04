---
title: Introducción a Brand Concierge
description: Introducción a Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 1%

---

# 1.4.1 Introducción a Brand Concierge

## Vídeo

En este vídeo, obtendrá una explicación y una demostración de todos los pasos involucrados en este ejercicio.

## Información general de 1.4.1.1 Brand Concierge

Al configurar Brand Concierge, los dos elementos principales que utilizará son:

- **Compositor de agentes (capa de configuración)**

  Objetivo: La plataforma de IU principal utilizada para crear y configurar experiencias de IA conversacional.

  Responsabilidades clave:

   - Definición y administración de fuentes de datos y bases de conocimiento
   - Establecer la expresión de marca (tono, estilo, protecciones)
   - Configurar el agente de reserva de reuniones

- **Agent Orchestrator (Motor de ejecución)**

  Objetivo: Motor de razonamiento y orquestación que interpreta las solicitudes de los usuarios y ejecuta las acciones del agente adecuadas.

  Responsabilidades clave:

   - Interpretar intenciones del usuario en lenguaje natural
   - Generar y ejecutar planes de razonamiento de varios pasos
   - Seleccione e invoque los operadores o herramientas adecuados
   - Aplicar el contexto, el cumplimiento y las protecciones de la marca
   - Coordinación de flujos de trabajo de varios agentes
   - Agregar y componer respuestas de varias fuentes de datos

- **Tiempo de ejecución de la conversación Brand Concierge (capa de servicio)**

  Objetivo: La capa de servicio conversacional orientada al cliente que administra las sesiones de chat, el contexto y las interacciones con el cliente.

  Componentes clave:

   - Agente web (cliente): interfaz de usuario del explorador o del chat móvil integrada mediante Web SDK
   - Servicio de conversación (servidor): administra el estado de la sesión y actúa como puerta de enlace de la orquestación

  Responsabilidades clave:

   - Administrar sesiones de usuario y transcripciones de conversaciones
   - Administrar la autenticación y los perfiles de usuario
   - Enrutar mensajes entre el cliente y Agent Orchestrator
   - Contexto de conversación persistente
   - Registrar eventos de comportamiento y operativos en AEP para análisis
   - Aplicar configuraciones específicas de la superficie

## 1.4.1.2 configuración de instancia de Brand Concierge

Para empezar a crear su propia instancia de Brand Concierge, siga los pasos a continuación.

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Brand Concierge**.

![Brand Concierge](./images/bc1.png)

Entonces debería ver esto. Haga clic en el menú **selección de zona protegida**.

![Brand Concierge](./images/bc2.png)

Elija la zona protegida que se le ha asignado. Esa zona protegida debe llamarse `--aepUserLdap-- - bc`.

![Brand Concierge](./images/bc3.png)

Haga clic en **Comenzar**.

![Brand Concierge](./images/bc4.png)

Para el nombre de su instancia de Brand Concierge, utilice: `--aepUserLdap-- - CitiSignal Brand Concierge`.

Escriba el siguiente texto en **¿Qué desea que haga el conserje?**.

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

Haga clic en **Crear**.

![Brand Concierge](./images/bc5.png)

Entonces debería ver esto. Haga clic en **Comenzar** para agregar una fuente de conocimientos.

![Brand Concierge](./images/bc6.png)

Seleccione **Vínculos al sitio web** y haga clic en **Continuar**.

![Brand Concierge](./images/bc7.png)

Entonces debería ver esto. Escriba `CitiSignal website` como nombre para la fuente de conocimientos.

Ahora necesita cargar un archivo .csv que contenga los enlaces de su sitio web. Descargue el sitio web [CitiSignal vincula el archivo CSV](./assets/citisignal-website-links.csv) con su escritorio.

Haga clic en **Examinar archivos**.

![Brand Concierge](./images/bc8.png)

Abra el archivo **citisignal-website-links.csv** y actualice los vínculos para que apunten a su propio sitio web de Citisignal.

![Brand Concierge](./images/bc8a.png)

Seleccione el archivo **citisignal-website-links.csv** que acaba de descargar y editar. Haga clic en **Abrir**.

![Brand Concierge](./images/bc9.png)

El archivo se agregará a esta fuente de conocimientos. Haga clic en **Agregar**.

![Brand Concierge](./images/bc10.png)

Entonces debería ver esto. Haz clic en **Llévame a casa**.

![Brand Concierge](./images/bc11.png)

Entonces debería ver esto. Haga clic en **Introducción** en la tarjeta **Asesoramiento de productos para consumidores**.

![Brand Concierge](./images/bc12.png)

Entonces debería ver esto. Rellene los campos siguientes con el texto siguiente.

**¿Qué debe saber el conserje sobre el producto o la audiencia antes de hacer recomendaciones?**

```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

**¿Hay alguna regla de negocio o limitación que el conserje deba seguir al hacer recomendaciones?**

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

**¿Hay alguna palabra clave o frase específica que el conserje deba seguir o evitar?**

```
Competitor pricing, competitor products
```

Las actualizaciones se guardan automáticamente. Haga clic en la **flecha** para regresar a la pantalla anterior.

![Brand Concierge](./images/bc13.png)

Entonces debería ver esto. Haga clic en **Comenzar** para personalizar la expresión de marca.

![Brand Concierge](./images/bc14.png)

Puede realizar sus propias elecciones en la página **Expresión de marca**; asegúrese de seleccionar una opción para cada pregunta.

![Brand Concierge](./images/bc15.png)

Desplácese hacia abajo y seleccione cualquier configuración para el campo **Longitud de respuesta**.

Las actualizaciones se guardan automáticamente.

![Brand Concierge](./images/bc16.png)

Desplácese hacia arriba y haga clic en la **flecha** para volver a la pantalla anterior.

![Brand Concierge](./images/bc17.png)

Entonces volverás a estar aquí. Haga clic en **Fuentes de conocimientos**.

![Brand Concierge](./images/bc18.png)

Haga clic en **Crear sus fuentes de conocimientos**.

![Brand Concierge](./images/bc19.png)

Seleccione **Catálogo de productos** y haga clic en **Continuar**.

![Brand Concierge](./images/bc20.png)

Entonces debería ver esto. Escriba `CitiSignal Products` como nombre para la fuente de conocimientos.

![Brand Concierge](./images/bc21.png)

Ahora necesita cargar un archivo .csv que contenga los enlaces de su sitio web. Descargue el [catálogo de productos CitiSignal](./assets/CitiSignal-catalog.json.zip) en su escritorio y descomprímalo.

![Brand Concierge](./images/bc26.png)

Haz clic en **Examinar archivos** y, a continuación, selecciona **Examinar desde tu dispositivo**.

![Brand Concierge](./images/bc22.png)

Seleccione el archivo **Citysignal-catalog.json** y haga clic en **Abrir**.

![Brand Concierge](./images/bc23.png)

Entonces debería ver esto. Haga clic en **Agregar**.

![Brand Concierge](./images/bc24.png)

Entonces volverás a estar aquí.

![Brand Concierge](./images/bc25.png)

Después de 10-20 minutos, el **estado** de ambas fuentes de conocimiento debería ser **Completado**. Haga clic en **Inicio**.

![Brand Concierge](./images/bc27.png)

Entonces debería ver esto. Haga clic en **+ Conectar** en la tarjeta **Vínculos al sitio web**.

![Brand Concierge](./images/bc28.png)

Seleccione la fuente de conocimiento **Sitio web de CitiSignal** y haga clic en **Guardar**.

![Brand Concierge](./images/bc29.png)

Entonces debería ver esto. Haga clic en **+ Conectar** en la tarjeta **Catálogo de productos**.

![Brand Concierge](./images/bc30.png)

Seleccione la fuente de conocimientos **Productos CitiSignal** y haga clic en **Guardar**.

![Brand Concierge](./images/bc31.png)

Entonces debería ver esto. Haga clic en **Vista previa** para comenzar a interactuar con su Brand Concierge.

![Brand Concierge](./images/bc32.png)

Ahora puede empezar a hacer preguntas relacionadas con las fuentes de conocimiento proporcionadas.

![Brand Concierge](./images/bc33.png)

## 1.4.1.3 pasos de incorporación a AEP

Brand Concierge usa Adobe Experience Platform para almacenar datos de interacción de conversaciones. La conexión entre Brand Concierge y Experience Platform requiere que Brand Concierge configure y utilice un conjunto de datos.

### Secuencia de datos

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Experience Platform**.

![Brand Concierge](./images/aep1.png)

Asegúrese de haber seleccionado la zona protegida correcta, que debe llamarse `--aepUserLdap-- - bc`. En el menú de la izquierda, desplácese hacia abajo y seleccione **Datastreams**.

![Brand Concierge](./images/aep2.png)

Haga clic en **Nueva secuencia de datos**.

![Brand Concierge](./images/aep3.png)

Escriba **Nombre de secuencia de datos** `--aepUserLdap-- - Brand Concierge` y, a continuación, seleccione **Esquema de asignación** `cja-brand-concierge-sb-XXX`.

Haga clic en **Guardar**.

![Brand Concierge](./images/aep4.png)

La secuencia de datos ya está configurada. Copie el nombre del flujo de datos y el ID del flujo de datos y escríbalos en un archivo de texto en el equipo.

![Brand Concierge](./images/aep5.png)

### API de administración de configuración de Brand Concierge

El siguiente paso es habilitar la API de administración de configuración de Brand Concierge para configurar el conjunto de datos que acaba de crear. Esto es necesario para resolver cosas como el ID de organización de IMS y los detalles de la zona protegida durante el procesamiento de la solicitud.

Actualmente, este es un paso interno de Adobe que debe producirse. Este paso es necesario porque, de lo contrario, la configuración del conjunto de datos no es correcta para que la utilice Brand Concierge.

Paso siguiente: [Implementar Brand Concierge en el sitio web](./ex2.md){target="_blank"}

Volver a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}