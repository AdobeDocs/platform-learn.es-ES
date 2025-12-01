---
title: Introducción a Brand Concierge
description: Introducción a Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: 6642acb3fdce2c9d3a9b919d5c9457191e4780a6
workflow-type: tm+mt
source-wordcount: '536'
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

Elija la zona protegida que se le ha asignado. Esa zona protegida debe llamarse `--aepUserLdap--`.

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



```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

```
Competitor pricing, competitor products
```

Las actualizaciones se guardan automáticamente. Haga clic en la **flecha** para regresar a la pantalla anterior.

![Brand Concierge](./images/bc13.png)

Entonces debería ver esto. Haga clic en **Comenzar** para personalizar la expresión de marca.

![Brand Concierge](./images/bc14.png)

Puede realizar sus propias elecciones en la página **Expresión de marca**.

![Brand Concierge](./images/bc15.png)

Desplácese hacia abajo y seleccione cualquier configuración para el campo **Longitud de respuesta**.

Las actualizaciones se guardan automáticamente.

![Brand Concierge](./images/bc16.png)

Desplácese hacia arriba y haga clic en la **flecha** para volver a la pantalla anterior.

![Brand Concierge](./images/bc17.png)


Volver a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}