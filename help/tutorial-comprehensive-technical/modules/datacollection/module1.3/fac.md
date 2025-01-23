---
title: 'Recopilación de datos: composición de audiencia federada'
description: 'Recopilación de datos: composición de audiencia federada'
kt: 5342
doc-type: tutorial
exl-id: 44660f3e-0594-4578-9531-1c918992aa9d
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 1.3 Composición de audiencia federada

En este módulo, el objetivo es aprender todo acerca de la creación de audiencias mediante la Composición de audiencias federada.

Composición de audiencias federada (FAC) en Experience Platform le permite acceder y crear audiencias con atributos de alto valor correspondientes de los almacenes de datos empresariales, que enriquecen y complementan el perfil del cliente en tiempo real y las audiencias en Experience Platform para mejorar la segmentación, la segmentación, la activación y el envío de experiencias de cliente impactantes. Con Federated Audience Composition, se crea una base de datos virtual vinculando bases de datos remotas a través de metadatos. Este método simplifica el acceso, reduce la duplicación y mejora la experiencia del usuario final. Los equipos disponen de la flexibilidad para introducir conjuntos de datos directamente en el Experience Platform o acceder a conjuntos de datos que residan en almacenes de datos al combinar audiencias para flujos de trabajo de participación. Este enfoque aprovecha las inversiones y los activos de Data Warehouse para complementar a Real-Time CDP y Journey Optimizer. La composición de audiencia federada permite a los clientes utilizar y combinar las funciones por lotes y en tiempo real en nuevos patrones de casos de uso críticos:

- Segmentación de audiencia federada: un equipo puede crear una audiencia utilizando la IU de composición de audiencia de arrastrar y soltar fácil de usar para los expertos en marketing en Real-Time CDP y Journey Optimizer, pero con una consulta insertada en el almacén de datos, dejando los datos subyacentes confidenciales en el almacén sin duplicaciones y proporcionando acceso flexible a conjuntos de datos esenciales.
- Enriquecimiento de la audiencia: las audiencias integradas en Real-Time CDP y Journey Optimizer se pueden enriquecer con datos empresariales adicionales para mejorar la segmentación y personalización con conjuntos de datos adicionales basados en perfiles y no basados en perfiles que no persistirán en Adobe Experience Platform. Por ejemplo, una marca comercial puede complementar una audiencia de compradores en línea recientes con una lista de ubicaciones principales para crear una audiencia con una promoción en línea y en la tienda multicanal.
- Enriquecimiento del perfil: los equipos pueden seleccionar atributos de perfil del almacén de datos que son críticos para que las experiencias en el momento se retengan dentro de perfiles de clientes procesables que residan en Real-Time CDP y a los que se acceda a través de Journey Optimizer. Estos puntos de datos adicionales están disponibles para la segmentación y personalización descendente desencadenada por comportamientos de evento según la acción del usuario y el caso de uso del cliente. Esto permite que los atributos traídos junto con audiencias federadas estén disponibles para la segmentación y personalización en el momento, junto con otros atributos y señales de comportamiento retenidos en un perfil de cliente.

La Composición de audiencias federada proporciona a los clientes de Real-Time CDP y Journey Optimizer la flexibilidad para decidir qué datos desean utilizar cuando y ayuda a evitar conjuntos de datos duplicados o patrones de integración innecesarios. Esto representa una combinación única de un enfoque federado para utilizar datos empresariales con el fin de depurar audiencias y atributos de alto valor, combinado con un sistema optimizado para la participación en canales múltiples en el momento. Esto resulta en menos movimiento de datos, pero también en nuevas oportunidades para utilizar audiencias y atributos de alto valor para una activación coherente de baja latencia en todos los canales.

## Objetivos de aprendizaje

- Obtenga información sobre cómo conectar Snowflake con Adobe Experience Platform
- Obtenga información sobre cómo crear un modelo de datos para los datos federados en Adobe Experience Platform
- Obtenga información sobre cómo crear composiciones de audiencias federadas en Adobe Experience Platform

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a un almacén de datos de Snowflake

## Ejercicios

[1.3.1 Configuración del entorno de Snowflake](./ex1.md)

En este ejercicio, configurará la cuenta de prueba de Snowflake y la conectará a Adobe Experience Platform

[1.3.2 Creación de esquemas, modelos de datos y vínculos](./ex2.md)

En este ejercicio, configurará el modelo de datos en AEP para los datos federados.

[1.3.3 Crear una composición federada](./ex3.md)

En este ejercicio, configurará el modelo de datos en AEP para los datos federados.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

![Perspectivas técnicas](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](../../../overview.md)
