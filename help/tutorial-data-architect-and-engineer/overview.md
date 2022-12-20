---
title: Introducción a Adobe Experience Platform para arquitectos de datos e ingenieros de datos
description: Introducción a Adobe Experience Platform para arquitectos de datos e ingenieros de datos.
breadcrumb-title: Información general
role: Data Architect, Data Engineer
kt: 4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# Introducción a Adobe Experience Platform para arquitectos de datos e ingenieros de datos

<!--5min-->

_Introducción a Adobe Experience Platform para arquitectos de datos e ingenieros de datos_ es el punto de partida perfecto para ponerse manos a la obra con el Experience Platform.


<!--How do we address ETL-->

## Objetivos de aprendizaje

Los arquitectos de datos y los ingenieros de datos deben colaborar estrechamente para lograr una implementación de Experience Platform exitosa. Este tutorial práctico le enseña las tareas clave ejecutadas por _ambas funciones_ por lo tanto, sabe cómo empezar a implementar Platform para su propia empresa. Se le guiarán en ejercicios que le presentarán la terminología clave, las características, la interfaz y la API de Experience Platform. Los clientes de aplicaciones de Adobe Experience Cloud como Real-time Customer Data Platform, Customer Journey Analytics y Journey Optimizer también encontrarán este contenido útil, ya que los servicios de plataforma son cimientos críticos de esas aplicaciones.

![Marketing de Adobe Experience Cloud que destaca los servicios de plataforma cubiertos en este tutorial: identidad, perfil, segmentación, ingesta, consulta y administración](assets/marketecture.png)

Los temas incluyen:

* Configuración de permisos de usuario
* Creación de entornos limitados
* Configuración de un proyecto de Developer Console y uso de la API de plataforma
* Administración de datos: incluida la creación de esquemas, conjuntos de datos, identidades, políticas de combinación y control de datos
* Ingesta de datos mediante los modos de flujo continuo y por lotes
* Captura de datos web con el SDK web de Adobe Experience Platform
* Creación de perfiles de cliente en tiempo real
* Uso del servicio de consulta para validar datos y extraer datos
* Generación de segmentos

## Escenario empresarial

Adobe Experience Platform es una plataforma técnica diseñada para ayudarle a lograr los objetivos de marketing. Los casos de uso empresarial deben impulsar la forma en que se diseña e implementa la tecnología. Este tutorial se centra en una marca comercial ficticia llamada Luma. Luma tiene tiendas de ladrillos y morteros en varios países y también tiene presencia en línea con un sitio web y aplicaciones móviles. Están invirtiendo en Adobe Experience Platform para combinar los datos de fidelidad, CRM, web y compras sin conexión en perfiles de clientes en tiempo real y activar estos perfiles para llevar su marketing al siguiente nivel. Los objetivos comerciales de Luma pueden o no estar alineados con los objetivos de su empresa, pero debería poder relacionar los pasos prácticos de este tutorial con sus propios objetivos empresariales.

## Requisitos previos

* Ha completado el [Curso de introducción a Adobe Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1) en Experience League y estén familiarizados con las funcionalidades de Platform
* Tiene acceso a una cuenta aprovisionada con Adobe Experience Platform (o una aplicación basada en Platform como Real-Time CDP o Journey Optimizer) y Recopilación de datos (anteriormente Launch).
* Es administrador del sistema de esa cuenta o puede tener una [configurar permisos de usuario](configure-permissions.md) para usted.

## Uso de este tutorial

Este tutorial combina tareas para ingenieros de datos y arquitectos de datos. Como se trata de un tutorial de introducción, debe poder completar las tareas para ambas funciones. Puesto que muchas de las lecciones se basan en lo que se implementó en lecciones anteriores, se debe avanzar por las lecciones en orden. Llamaré sobre qué lecciones se pueden saltar.

A medida que crea varios elementos de Platform durante este tutorial, intente atenerse a los nombres que recomiendo en la medida de lo posible. Sin embargo, hay algunos nombres de elementos de alto nivel que puede que desee personalizar en caso de que haya varias personas en la organización que tomen este tutorial simultáneamente. Por ejemplo, es posible que desee nombrar el entorno limitado de la plataforma &quot;Plataforma Tutorial de Luma: Ignatius J Reilly&quot; en lugar de &quot;Plataforma Tutorial de Luma&quot;.

Si se queda atascado, intente volver a leer primero las instrucciones y, a continuación, utilice el ![Registrar un problema](https://experienceleague.adobe.com/assets/img/feedback.svg) en la barra lateral de cada página para contactarme.

## Notas técnicas

### Entornos de espacio aislado

En el tutorial, creará un entorno de entorno limitado y lo utilizará para completar los ejercicios. El entorno de entorno limitado le garantiza completar los ejercicios y el experimento sin preocuparse por poner en peligro los datos de producción.

### API

Platform es la API creada primero. Aunque los flujos de trabajo de la interfaz existen para todos los flujos de trabajo de la plataforma principales y se utilizarán principalmente, el tutorial contiene algunos ejercicios orientados a la API. Le guiaré a través de la configuración básica del proyecto en la consola de Adobe Developer y le proporcionaré [!DNL Postman] entornos y colecciones para empezar a usar la API de Platform. Después de completar el tutorial, puede que le resulte útil estar familiarizado con la API de Platform y utilizarla en su propia implementación.

### Tecnologías de terceros

Aunque utilizará varias tecnologías en este tutorial, permanecerá casi completamente dentro del ecosistema del Adobe. En su propia implementación de Platform, es probable que integre Platform con tecnologías de terceros específicas. Para mantener este tutorial relevante para todos los clientes, utilizaremos una implementación más genérica.

Ahora pasemos a la primera lección...[configurar permisos](configure-permissions.md).
