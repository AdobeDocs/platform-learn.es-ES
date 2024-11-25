---
title: Instale y configure su clúster de Kafka
description: Instale y configure su clúster de Kafka
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: adffeead-9bcb-4632-9a2c-c6da1c40b7f2
source-git-commit: be5a7dec47a83a14d74024015a15a9c24d04cd95
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# 2.6.2 Instalar y configurar el clúster de Kafka

## Descargar Apache Kafka

Vaya a [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads) y descargue la versión más reciente. Seleccione la última versión binaria, en este caso **3.9.0**. Se iniciará la descarga.

![Kafka](./images/kafka1.png)

Cree una carpeta en su escritorio llamada **Kafka_AEP** y coloque el archivo descargado en ese directorio.

![Kafka](./images/kafka3.png)

Abra una ventana de **Terminal** haciendo clic con el botón derecho en la carpeta y luego en **Nuevo terminal en la carpeta**.

![Kafka](./images/kafka4.png)

Ejecute este comando en la ventana de terminal para descomprimir el archivo descargado:

`tar -xvf kafka_2.13-3.9.0.tgz`

>[!NOTE]
>
>Compruebe que el comando anterior coincida con la versión del archivo descargado. Si su versión es más reciente, deberá actualizar el comando anterior para que coincida con esa versión.

![Kafka](./images/kafka5.png)

A continuación, verá esto:

![Kafka](./images/kafka6.png)

Después de descomprimir ese archivo, ahora tiene un directorio como este:

![Kafka](./images/kafka7.png)

Y en ese directorio, verán estos subdirectorios:

![Kafka](./images/kafka8.png)

Vuelva a la ventana de terminal. Introduzca el siguiente comando:

`cd kafka_2.13-3.9.0`

>[!NOTE]
>
>Compruebe que el comando anterior coincida con la versión del archivo descargado. Si su versión es más reciente, deberá actualizar el comando anterior para que coincida con esa versión.

![Kafka](./images/kafka9.png)

A continuación, escriba el comando `bin/kafka-topics.sh`.

![Kafka](./images/kafka10a.png)

Entonces debería ver esta respuesta. Esto significa que Kafka está correctamente instalado y que Java funciona correctamente. (Recordatorio: para que esto funcione, necesita instalar el JDK de Java 23.) Puede ver qué versión de Java ha instalado mediante el comando `java -version`.)

![Kafka](./images/kafka10.png)

## Iniciar Kafka

Para iniciar Kafka, tendrá que iniciar Kafka Zookeeper y Kafka, en este orden.

Abra una ventana de **Terminal** haciendo clic con el botón derecho en la carpeta **kafka_2.13-3.9.0** y luego en **Nuevo terminal en la carpeta**.

![Kafka](./images/kafka11.png)

Introduzca este comando:

`bin/zookeeper-server-start.sh config/zookeeper.properties`

![Kafka](./images/kafka12.png)

A continuación, verá esto:

![Kafka](./images/kafka13.png)

Mantenga esta ventana abierta mientras realiza estos ejercicios.

Abra otra ventana de **Terminal** nueva haciendo clic con el botón derecho en la carpeta **kafka_2.13-3.9.0** y luego en **Nuevo terminal en la carpeta**.

![Kafka](./images/kafka11.png)

Introduzca este comando:

`bin/kafka-server-start.sh config/server.properties`

![Kafka](./images/kafka14.png)

A continuación, verá esto:

![Kafka](./images/kafka15.png)

Mantenga esta ventana abierta mientras realiza estos ejercicios.

## Crear un tema de Kafka

Abra una ventana de **Terminal** haciendo clic con el botón derecho en la carpeta **kafka_2.13-3.9.0** y luego en **Nuevo terminal en la carpeta**.

![Kafka](./images/kafka11.png)

Escriba este comando para crear un nuevo tema de Kafka con el nombre **aeptest**. Este tema se utilizará para probar en este ejercicio.

`bin/kafka-topics.sh --create --topic aeptest --bootstrap-server localhost:9092`

A continuación, verá una confirmación:

![Kafka](./images/kafka17a.png)

Introduzca este comando para crear un nuevo tema de Kafka con el nombre **aep**. Este tema lo utilizará el conector del receptor de Adobe Experience Platform que configurará en los próximos ejercicios.

`bin/kafka-topics.sh --create --topic aep --bootstrap-server localhost:9092`

A continuación, verá una confirmación similar:

![Kafka](./images/kafka17.png)

## Producir eventos

Vuelva a la ventana de terminal en la que creó el primer tema de Kafka e introduzca el siguiente comando:

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aeptest`

![Kafka](./images/kafka18.png)

Entonces verá esto... Cada nueva línea seguida de presionar el botón Enter dará como resultado que se envíe un nuevo mensaje al tema **aeptest**.

![Kafka](./images/kafka19.png)

Escriba `Hello AEP` y presione Intro. Su primer evento se ha enviado a su instancia local de Kafka, al tema **aeptest**.

![Kafka](./images/kafka20.png)

Escriba `Hello AEP again.` y presione Intro.

Escriba `AEP Data Collection is the best.` y presione Intro.

Ahora ha producido tres eventos en el tema **aeptest**. Estos eventos ahora los puede consumir una aplicación que pueda necesitar esos datos.

![Kafka](./images/kafka21.png)

En el teclado, haga clic en `Control` y `C` al mismo tiempo para cerrar el productor.

![Kafka](./images/kafka22.png)

## Consumir eventos

En la misma ventana de terminal que utilizó para producir eventos, introduzca el siguiente comando:

`bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic aeptest --from-beginning`

Verá todos los mensajes que se produjeron en el ejercicio anterior para el tema **aeptest**, que aparecen en el consumidor. Así es como funciona Apache Kafka: un productor crea eventos en una canalización y un consumidor consume esos eventos.

![Kafka](./images/kafka23.png)

En el teclado, haga clic en `Control` y `C` al mismo tiempo para cerrar el productor.

![Kafka](./images/kafka24.png)

En este ejercicio, ha pasado por todos los conceptos básicos para configurar un clúster local de Kafka, crear un tema de Kafka, producir eventos y consumir eventos.

El objetivo de este módulo es simular lo que sucedería si una organización real ya ha implementado un clúster de Apache Kafka y desea transmitir datos de su clúster de Kafka a Adobe Experience Platform.

Para facilitar una implementación de este tipo, se creó un conector de receptor de Adobe Experience Platform que puede implementarse mediante Kafka Connect. Puede encontrar la documentación de ese conector del receptor de Adobe Experience Platform aquí: [https://github.com/adobe/experience-platform-streaming-connect](https://github.com/adobe/experience-platform-streaming-connect).

En los próximos ejercicios, implementará todo lo necesario para utilizar el conector del receptor de Adobe Experience Platform desde su propio clúster local de Kafka.

Cierre la ventana del terminal.

Ha terminado este ejercicio.

Paso siguiente: [2.6.3 Configuración del extremo de la API HTTP en Adobe Experience Platform](./ex3.md)

[Volver al módulo 2.6](./aep-apache-kafka.md)

[Volver a todos los módulos](../../../overview.md)
