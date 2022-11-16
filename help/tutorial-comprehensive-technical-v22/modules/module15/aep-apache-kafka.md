---
title: Transmisión de datos de Apache Kafka a Adobe Experience Platform
description: En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el conector Adobe Experience Platform Sink para Kafka Connect.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: e1e283b1-93b7-4d06-b9ed-beac48a99c3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# 15. Transmitir datos de Apache Kafka a Adobe Experience Platform

**Autores: [Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/), [Nipun Nair](https://www.linkedin.com/in/nipunnair/), [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el conector Adobe Experience Platform Sink a través de Kafka Connect.

## Objetivos de aprendizaje

- Realizar una configuración básica de un clúster local de Kafka
- Crear un tema de Kafka, usar un productor de Kafka y un consumidor de Kafka
- Configuración de Kafka Connect y el conector Adobe Experience Platform Sink
- Producir eventos manualmente y ver cómo se incorporan esos eventos en Adobe Experience Platform
- Utilice una biblioteca de productores de Twitter existente de Kafka Connect para transmitir datos de Twitter a Adobe Experience Platform

## Requisitos previos

- Java JDK11 o superior debe estar instalado en su equipo, puede descargar ese JDK aquí: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Acceso a Adobe Experience Platform

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem24.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--aepSandboxId--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[15.1 Introducción a Apache Kafka](./ex1.md)

En este ejercicio, aprenderá sobre los conceptos básicos de Apache Kafka

[15.2 Instalar y configurar el clúster de Kafka](./ex2.md)

En este ejercicio, descargará, instalará y configurará su clúster básico de Apache Kafka.

[15.3 Configurar el extremo de transmisión de API HTTP en Adobe Experience Platform](./ex3.md)

En este ejercicio, debe configurar un conector de origen de API HTTP en Adobe Experience Platform.

[15.4 Instalar y configurar Kafka Connect y el conector Adobe Experience Platform Sink](./ex4.md)

En este ejercicio, utilizará Kafka Connect para instalar y utilizar el conector Adobe Experience Platform Sink y enviará eventos a Adobe Experience Platform manualmente.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
