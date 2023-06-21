---
title: Introducción a Adobe Experience Platform para arquitectos e ingenieros de datos
description: Introducción a Adobe Experience Platform para arquitectos e ingenieros de datos.
breadcrumb-title: Información general
role: Data Architect, Data Engineer
kt: 4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: 191fe710c6cd00b5355881158a7e0af85523e22e
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# Introducción a Adobe Experience Platform para arquitectos e ingenieros de datos

<!--5min-->

_Introducción a Adobe Experience Platform para arquitectos e ingenieros de datos_ es el punto de partida perfecto para ponerse en contacto con Experience Platform.


<!--How do we address ETL-->

## Objetivos de aprendizaje

Los arquitectos de datos y los ingenieros de datos deben colaborar estrechamente para que la implementación de Experience Platform se realice correctamente. Este tutorial práctico le enseña las tareas clave ejecutadas por _ambas funciones_ para que sepa cómo empezar a implementar Platform para su propio negocio. Se le guiará a través de ejercicios que le presentarán la terminología, las funciones, la interfaz y la API clave de Experience Platform. Los clientes de aplicaciones de Adobe Experience Cloud como Real-time Customer Data Platform, Customer Journey Analytics y Journey Optimizer también encontrarán útil este contenido, ya que los servicios de Platform son fundamentos críticos de dichas aplicaciones.

![La arquitectura de marketing de Adobe Experience Cloud destaca los servicios de Platform que se tratan en este tutorial: identidad, perfil, segmentación, ingesta, consulta y administración](assets/marketecture.png)

Los temas incluyen:

* Configuración de permisos de usuario
* Creación de zonas protegidas
* Configuración de un proyecto de Developer Console y uso de la API de Platform
* Administración de datos, incluida la creación de esquemas, conjuntos de datos, identidades, políticas de combinación y administración de datos
* Ingesta de datos mediante los modos por lotes y streaming
* Captura de datos web con el SDK web de Adobe Experience Platform
* Creación de perfiles de cliente en tiempo real
* Uso del servicio de consultas para validar datos y extraer datos
* Generación de segmentos

## Escenario empresarial

Adobe Experience Platform es una plataforma técnica diseñada para ayudarle a lograr sus objetivos de marketing. Los casos de uso empresariales deben orientar la forma en que se diseña e implementa la tecnología. Este tutorial se centra en una marca minorista ficticia llamada Luma. Luma opera tiendas físicas en varios países y también tiene presencia en línea con un sitio web y aplicaciones móviles. Están invirtiendo en Adobe Experience Platform para combinar datos de lealtad, CRM, web y compras sin conexión en perfiles de clientes en tiempo real y activar estos perfiles para llevar su marketing al siguiente nivel. Los objetivos empresariales de Luma pueden o no coincidir con los objetivos de su compañía, pero debe poder relacionar los pasos prácticos de este tutorial con sus propios objetivos empresariales.

## Requisitos previos

* Ha completado la [Curso de introducción a Adobe Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1&amp;lang=es) en el Experience League y estén familiarizados con las funcionalidades de Platform
* Tiene acceso a una cuenta aprovisionada con Adobe Experience Platform (o una aplicación basada en Platform, como Real-Time CDP o Journey Optimizer) y a la recopilación de datos (anteriormente Launch).
* Usted es administrador del sistema de esa cuenta o puede tener una [configurar permisos de usuario](configure-permissions.md) para usted.

## Uso de este tutorial

Este tutorial combina tareas para ingenieros y arquitectos de datos. Como es un tutorial de nivel introductorio, debe poder completar las tareas para ambas funciones. Dado que muchas de las lecciones se basan en lo implementado en lecciones anteriores, debe avanzar por las lecciones en orden. Voy a llamar a qué lecciones se pueden saltar.

A medida que crea varios elementos de Platform durante este tutorial, intente adherirse a los nombres que recomiendo en la medida de lo posible. Sin embargo, hay algunos nombres de elementos de alto nivel que puede que desee personalizar en caso de que haya varias personas en su organización que realicen este tutorial simultáneamente. Por ejemplo, es posible que desee asignar el nombre &quot;Plataforma de tutorial de Luma: Ignatius J Reilly&quot; a la zona protegida de Platform en lugar de &quot;Plataforma de tutorial de Luma&quot;.

Si se queda atascado, intente volver a leer las instrucciones primero y, a continuación, utilice el ![Registrar un problema](https://experienceleague.adobe.com/assets/img/feedback.svg) en la barra lateral de cada página para ponerse en contacto conmigo.

## Notas técnicas

### Entornos de zona protegida

En el tutorial, creará un entorno de zona protegida y lo utilizará para completar los ejercicios. El entorno de zona protegida garantiza que pueda completar los ejercicios y experimentar sin poner en peligro los datos de producción.

### API

Platform se crea primero según la API. Aunque los flujos de trabajo de la interfaz existen para todos los flujos de trabajo de plataforma principales y se utilizarán principalmente, el tutorial contiene algunos ejercicios orientados a la API. Le guiaré a través de la configuración básica del proyecto en la consola de Adobe Developer y le proporcionaré lo siguiente [!DNL Postman] Entornos y colecciones para empezar a usar la API de Platform. Después de completar el tutorial, puede que le resulte útil familiarizarse con la API de Platform y utilizarla en su propia implementación.

### Tecnologías de terceros

Aunque utilizará varias tecnologías en este tutorial, permanecerá casi completamente dentro del ecosistema de Adobe. En su propia implementación de Platform, probablemente integrará Platform con tecnologías de terceros específicas. Para mantener este tutorial relevante para todos los clientes, utilizaremos una implementación más genérica.

Ahora pasemos a la primera lección...[configuración de permisos](configure-permissions.md).
