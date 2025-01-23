---
title: Transmitir datos de Apache Kafka a Adobe Experience Platform
description: En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el Conector del receptor de Adobe Experience Platform para Kafka Connect.
kt: 5342
doc-type: tutorial
exl-id: 2b7010f3-ab31-4099-aecd-fd4e73b7e96e
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# 2.6 Transmitir datos de Apache Kafka a Adobe Experience Platform

En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el Conector del receptor de Adobe Experience Platform a través de Kafka Connect.

## Objetivos de aprendizaje

- Realizar una configuración básica de un clúster local de Kafka
- Crear un tema de Kafka, utilizar un productor de Kafka y un consumidor de Kafka
- Configuración de Kafka Connect y el conector del receptor de Adobe Experience Platform
- Produzca eventos manualmente y vea que esos eventos se incorporan en Adobe Experience Platform
- Utilice una biblioteca de productor de Twitteres existente de Kafka Connect para transmitir los datos de Twitter a Adobe Experience Platform

## Requisitos previos

- Java JDK23 o superior debe estar instalado en su equipo, puede descargar ese JDK aquí: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Acceso a Adobe Experience Platform

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se hace referencia en [Instalar la extensión de Chrome para la documentación del Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Ejercicios

[2.6.1 Introducción a Apache Kafka](./ex1.md)

En este ejercicio, aprenderá los conceptos básicos de Apache Kafka

[2.6.2 Instalar y configurar el clúster de Kafka](./ex2.md)

En este ejercicio, descargará, instalará y configurará su clúster básico de Apache Kafka.

[2.6.3 Configuración del punto final de flujo de API HTTP en Adobe Experience Platform](./ex3.md)

En este ejercicio, debe configurar un conector Source de la API HTTP en Adobe Experience Platform.

[2.6.4 Instalar y configurar Kafka Connect y el conector del receptor de Adobe Experience Platform](./ex4.md)

En este ejercicio, utilizará Kafka Connect para instalar y utilizar el conector del receptor de Adobe Experience Platform y enviará eventos a Adobe Experience Platform manualmente.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

![Perspectivas técnicas](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](../../../overview.md)
