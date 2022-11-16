---
title: Introducción a Apache Kafka
description: Introducción a Apache Kafka
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 7b600c79-03c5-46fc-9ac9-a15599608c35
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 15.1 Introducción a Apache Kafka

## 15.1.1 Introducción

Cada organización comienza de una manera muy simple desde una perspectiva de datos. El ecosistema de datos de una organización comienza con un sistema de origen y un destino. El sistema de origen envía datos al sistema de destino, y eso es todo. Fácil, ¿verdad?
Si sólo fuera así de simple. Las organizaciones crecen rápidamente por encima de esa sencilla configuración y el número de sistemas de origen y sistemas de destino aumenta rápidamente. Todas estas fuentes y destinos diferentes necesitan intercambiar datos entre sí, y las cosas rápidamente se vuelven muy complejas.
Por ejemplo, si una organización tiene 4 orígenes y 6 destinos y todas estas aplicaciones deben comunicarse entre sí, deberá crear 24 integraciones... Cada una de estas integraciones tiene sus propias dificultades:

- protocolo: cómo se transportan los datos (TCP, HTTP, REST, FTP, ...)
- formato de datos: cómo se analizan los datos (binario, CSV, JSON, Parquet, ...)
- evolución y esquema de datos: ¿cuál es el modelo de datos y cómo evolucionará?

Además, cada vez que conecte un sistema de origen a un sistema de destino, habrá una carga mayor en esos sistemas desde esa conexión.

Entonces, ¿cómo resolver esto? Ahí es donde Apache Kafka entra en la foto. Apache Kafka permite que una organización desvincule flujos de datos y sistemas al proporcionar un sistema de mensajería común, de alto rendimiento y distribuido. Los sistemas de origen enviarán sus datos a Apache Kafka, y los sistemas de destino consumirán los datos de Apache Kafka.

Piense en todos los tipos de fuentes de datos que las empresas tienen que administrar:

- eventos del sitio web
- eventos de aplicaciones móviles
- Eventos de POS
- Datos CRM
- datos de callcenter
- historial de transacciones
- ...

Y piensen en todos los tipos de destinos que las empresas utilizan en su ecosistema que todos pueden necesitar datos de esos sistemas de origen:

- CRM
- lago de datos
- sistema de correo electrónico
- auditoría
- Analytics
- ...

Apache Kafka fue creado por LinkedIn y ahora es un proyecto de código abierto principalmente mantenido por Confluent.
Apache Kafka proporciona una arquitectura distribuida y flexible que es tolerante a fallos. Puede escalar horizontalmente hasta los 100 metros de corredores y puede escalar a millones de mensajes por segundo. Proporciona un alto rendimiento con latencias inferiores a 10 ms, lo que resulta ideal para casos de uso en tiempo real.

Un par de ejemplos de casos de uso:

- Sistema de mensajería
- Seguimiento de actividades
- Recopilar métricas de muchas ubicaciones diferentes
- Recopilación de registros de aplicaciones
- Procesamiento de flujo (con la API de Kafka Streams o Spark)
- Desacoplamiento de las dependencias del sistema
- Integración con Spark, Flink, Storm, Hadoop y muchas otras tecnologías de Big Data.

Por ejemplo:

- Netflix usa Kafka para aplicar recomendaciones en tiempo real mientras estás viendo programas de televisión
- Uber utiliza Kafka para recopilar datos de usuarios, taxis y viajes en tiempo real para calcular y pronosticar la demanda y calcular los precios de las subidas de los precios en tiempo real
- linkedIn utiliza Kafka para evitar el spam, recopila interacciones de los usuarios para hacer mejores recomendaciones de conexión en tiempo real

Para todos estos casos de uso, Kafka se utiliza solamente como mecanismo de transporte. Kafka es muy bueno para mover datos entre aplicaciones.

## Terminología de kafka

### Mensaje

Un mensaje es una comunicación enviada por un sistema a Kafka. Un mensaje contiene una carga útil y una carga útil contiene elementos de datos. Por ejemplo, un evento de experiencia enviado por un sitio web a Adobe Experience Platform se considera un mensaje.

### Tema, particiones, desplazamientos

Un tema es un flujo particular de datos, similar a una tabla de una base de datos. Puede tener tantos temas como desee y este se identifica con su nombre. Los temas se dividen en particiones. Cada partición está ordenada y cada mensaje dentro de una partición obtiene un id incremental, que se llama **offset**. Los mensajes se almacenan en un tema, en una partición y se hace referencia a ellos mediante un desplazamiento. Los mensajes se conservan únicamente durante un tiempo limitado (el valor predeterminado es 1 semana). Una vez que se escribe un mensaje en una partición, ya no se puede cambiar.

### Corredores

Un agente es similar a un servidor. Un clúster de Kafka está compuesto por varios intermediarios (servidores). Cada agente se identifica con un ID y contiene ciertas particiones de tema.

### Replicación

Kafka es un sistema distribuido. Una de las cosas importantes de un sistema distribuido es que los datos se almacenan de forma segura y, como tal, se necesita replicación. Después de todo, cuando un corredor (servidor) se cae, otro corredor (servidor) debería poder proporcionar acceso a los mensajes que inicialmente se almacenaron en el corredor que se cerró. La replicación creará copias de mensajes en varios agentes para garantizar que no se pierdan datos.

### Productores

¿Cómo se envían los datos a Kafka? Ese es el papel de un productor. Un productor se conecta a un sistema de origen y toma los datos del sistema de origen, y luego escribe esos datos en temas en particiones. Basándose en la configuración de su clúster Kafka, los productores sabrán automáticamente a qué agente y partición escribirán. En un sistema distribuido con varios agentes de bolsa y estrategia de replicación, un productor almacenará datos aleatoriamente entre varios agentes de bolsa, lo que significa que realizará el equilibrio de carga automáticamente.

### Claves del mensaje

Los productores pueden elegir enviar una clave con el mensaje. Una clave puede ser cualquier cadena, número, etc. Si no se proporciona ninguna clave, se envía un mensaje aleatoriamente a los corredores. Si se envía una clave, todos los mensajes para esa clave siempre irán a la misma partición. Una clave de mensaje como tal se utiliza para solicitar mensajes en función de un campo específico.

### Consumidores

Los consumidores leen datos de un tema de Apache Kafka y luego comparten esos datos con los sistemas de destino. Los consumidores saben de qué agente leer. Los datos los lee un consumidor en orden, dentro de cada partición. Los consumidores leen datos en grupos de consumidores.

### Zookeeper

ZooKeeper es esencialmente un servicio para sistemas distribuidos que ofrecen un almacén jerárquico de clave-valor, que se utiliza para proporcionar un servicio de configuración distribuida, servicio de sincronización y registro de nombres para sistemas distribuidos grandes. Zookeeper necesita estar corriendo antes de poder usar Apache Kafka, y Zookeeper es una especie de maestro de ceremonias para Kafka, administrando servicios distribuidos en el backend mientras Kafka produce y consume eventos.

Ha terminado este ejercicio.

Paso siguiente: [15.2 Instalar y configurar el clúster de Kafka](./ex2.md)

[Volver al módulo 15](./aep-apache-kafka.md)

[Volver a todos los módulos](../../overview.md)
