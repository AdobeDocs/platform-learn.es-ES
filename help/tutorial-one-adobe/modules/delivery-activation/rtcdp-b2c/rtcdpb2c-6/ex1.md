---
title: Introducción a Apache Kafka
description: Introducción a Apache Kafka
kt: 5342
doc-type: tutorial
exl-id: e0209ffc-621b-4e8d-aaa7-ac92eef3f86a
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# 2.6.1 Introducción a Apache Kafka

## 2.6.1.1 Introducción

Cada organización comienza de una manera muy sencilla desde la perspectiva de los datos. El ecosistema de datos de una organización comienza con un sistema de origen y un destinatario. El sistema de origen envía datos al sistema de destino, y eso es todo. Tranquilo, ¿verdad?
Si tan solo fuera así de simple. Las organizaciones superan rápidamente esa configuración sencilla y el número de sistemas de origen y de destino aumenta rápidamente. Todas estas fuentes y destinos diferentes necesitan intercambiar datos entre sí, y las cosas se vuelven muy complejas rápidamente.
Por ejemplo, si una organización tiene 4 fuentes y 6 destinos y todas estas aplicaciones necesitan hablar entre sí, tendrá que crear 24 integraciones... Cada una de estas integraciones tiene sus propias dificultades:

- protocol: cómo se transportan los datos (TCP, HTTP, REST, FTP, etc.)
- formato de datos: cómo se analizan los datos (binario, CSV, JSON, Parquet, etc.)
- esquema de datos y evolución: ¿qué es el modelo de datos y cómo evolucionará?

Además, cada vez que conecte un sistema de origen a un sistema de destino, habrá una carga mayor en esos sistemas desde esa conexión.

Entonces, ¿cómo se resuelve esto? Ahí es donde Apache Kafka entra en escena. Apache Kafka permite a una organización desvincular flujos de datos y sistemas al proporcionar un sistema de mensajería distribuido común, de alto rendimiento. Los sistemas de Source enviarán sus datos a Apache Kafka y los sistemas de destino consumirán datos de Apache Kafka.

Piense en todos los tipos de fuentes de datos que las empresas de experiencia tienen que administrar:

- eventos de sitio web
- eventos de aplicaciones móviles
- Eventos POS
- Datos CRM
- datos del centro de llamadas
- historial de transacciones
- ...

Y piense en todos los tipos de destinos que las empresas utilizan en su ecosistema y que pueden necesitar datos de esos sistemas de origen:

- CRM
- lago de datos
- sistema de correo electrónico
- auditoría
- Analytics
- ...

Apache Kafka fue creado por LinkedIn y ahora es un proyecto de código abierto mantenido principalmente por Confluent.
Apache Kafka proporciona una arquitectura resistente y distribuida que tolera errores. Puede escalar horizontalmente a 100 agentes y puede escalar a millones de mensajes por segundo. Proporciona un alto rendimiento con latencias inferiores a 10 ms, lo que resulta ideal para casos de uso en tiempo real.

Un par de ejemplos de casos de uso:

- Sistema de mensajería
- Seguimiento de actividades
- Recopilar métricas de muchas ubicaciones diferentes
- Recopilación de registros de aplicaciones
- Procesamiento de transmisiones (con la API de Kafka Streams o Spark)
- Desacoplamiento de dependencias del sistema
- Integración con Spark, Flink, Storm, Hadoop y muchas otras tecnologías de Big Data.

Por ejemplo:

- Netflix usa Kafka para aplicar recomendaciones en tiempo real mientras ves programas de televisión
- Uber utiliza Kafka para recopilar datos de usuarios, taxis y viajes en tiempo real para calcular y prever la demanda y calcular los precios de las subidas en tiempo real
- LinkedIn usa Kafka para evitar el spam, recopilar interacciones de usuarios para hacer mejores recomendaciones de conexión en tiempo real

Para todos estos casos de uso, Kafka solo se utiliza como mecanismo de transporte. Kafka es muy bueno moviendo datos entre aplicaciones.

## 2.6.1.2 Terminología de Kafka

### Mensaje

Un mensaje es una comunicación enviada por un sistema a Kafka. Un mensaje contiene una carga útil, y una carga útil contiene elementos de datos. Por ejemplo, un evento de experiencia enviado por un sitio web a Adobe Experience Platform se considera un mensaje.

### Tema, particiones, desplazamientos

Un tema es una secuencia particular de datos, similar a una tabla de una base de datos. Puede tener tantos temas como desee y un tema se identifica con su nombre. Los temas se dividen en particiones. Cada partición se ordena y cada mensaje dentro de una partición obtiene un identificador incremental, que se denomina **offset**. Los mensajes se almacenan en un tema, en una partición y se hace referencia a ellos mediante un desplazamiento. Los mensajes se conservan solo durante un tiempo limitado (el valor predeterminado es 1 semana). Una vez que se escribe un mensaje en una partición, ya no se puede cambiar.

### Corredores

Un agente es similar a un servidor. Un clúster de Kafka está compuesto por varios agentes (servidores). Cada corredor se identifica con un ID y contiene ciertas particiones temáticas.

### Replicación

Kafka es un sistema distribuido. Una de las cosas importantes de un sistema distribuido es que los datos se almacenan de forma segura y, como tal, es necesaria la replicación. Después de todo, cuando un corredor (servidor) se cae, otro corredor (servidor) todavía debe ser capaz de proporcionar acceso a los mensajes que se almacenaron inicialmente en el corredor que se cayó. La replicación creará copias de los mensajes en varios agentes para garantizar que no se pierdan datos.

### Productores

¿Cómo se envían los datos a Kafka? Ese es el papel de un productor. Un productor se conecta a un sistema de origen y toma los datos del sistema de origen y, a continuación, escribe esos datos en los temas en las particiones. Según la configuración de su clúster de Kafka, los productores sabrán automáticamente en qué broker y partición escribir. En un sistema distribuido con varios agentes y una estrategia de replicación, un productor almacenará datos aleatoriamente en varios agentes, lo que significa que equilibrará la carga automáticamente.

### Claves de mensaje

Los productores pueden elegir enviar una clave con el mensaje. Una clave puede ser cualquier cadena, número, etc. Si no se proporciona ninguna clave, se envía un mensaje aleatoriamente a los corredores. Si se envía una clave, todos los mensajes para esa clave siempre irán a la misma partición. Se utiliza una clave de mensaje como tal para ordenar los mensajes en función de un campo específico.

### Consumidores

Los consumidores leen datos de un tema de Apache Kafka y luego los comparten con sistemas de destino. Los consumidores saben de qué agente leer. Un consumidor lee los datos en orden, dentro de cada partición. Los consumidores leen datos en grupos de consumidores.

### Zookeeper

ZooKeeper es esencialmente un servicio para sistemas distribuidos que ofrece un almacén jerárquico de clave-valor, que se utiliza para proporcionar un servicio de configuración distribuida, servicio de sincronización y registro de nombres para sistemas distribuidos grandes. Zookeeper necesita estar en ejecución antes de poder usar Apache Kafka, y Zookeeper es como el maestro de ceremonias de Kafka, y administra los servicios distribuidos en el servidor mientras Kafka produce y consume eventos.

Ha terminado este ejercicio.

## Pasos siguientes

Vaya a [2.6.2. Instale y configure su clúster de Kafka](./ex2.md){target="_blank"}

Volver a [Transmitir datos de Apache Kafka a Adobe Experience Platform](./aep-apache-kafka.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
