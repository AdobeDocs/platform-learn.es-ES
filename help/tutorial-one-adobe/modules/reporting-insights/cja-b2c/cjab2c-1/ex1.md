---
title: Customer Journey Analytics - Customer Journey Analytics 101
description: Customer Journey Analytics - Customer Journey Analytics 101
kt: 5342
doc-type: tutorial
exl-id: ea1469a4-cbfd-4633-8678-9467c2146a2a
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---

# 1.1.1 Customer Journey Analytics 101

## Objetivos

- Comprender el servicio de aplicaciones de CJA
- Aprenda a posicionar CJA
- Comprender el flujo de trabajo de CJA: de la conexión de datos a las perspectivas

## 1.1.1.1 ¿Qué es Customer Journey Analytics?

Customer Journey Analytics (CJA) proporciona un conjunto de herramientas a los equipos de inteligencia empresarial y ciencia de datos para vincular y analizar datos de canales cruzados (en línea y sin conexión). Las funciones dentro de CJA ofrecen contexto y claridad al complejo recorrido de clientes multicanal. El contexto proporcionado proporciona una perspectiva procesable para eliminar puntos problemáticos del proceso de conversión del cliente y diseñar y ofrecer experiencias excepcionales en los momentos más importantes.

CJA pone Analysis Workspace sobre Adobe Experience Platform. Adobe Experience Platform es el cerebro para la comunicación y la orquestación y, con CJA, las marcas ahora pueden contextualizar y visualizar todos esos datos, de modo que los equipos de Business and Insight puedan aprender de ellos analizando el recorrido completo de los clientes en línea y sin conexión.

Los equipos de Business and Insight pueden hablar con CJA, hacer preguntas y obtener respuestas sobre la marcha con la interfaz de usuario de Analysis Workspace de arrastrar y soltar, apuntar y hacer clic y fácil de usar.

![demostración](./images/cja-adv-analysis1.png)

## 1.1.1.2 Ventajas principales

Las tres ventajas principales para los clientes son:

- La capacidad de poner perspectivas a disposición de todos (es decir, democratizar el acceso a los datos)
- La capacidad de ver al cliente en un recorrido contextual (es decir, los datos se pueden visualizar secuencialmente abarcando varios canales, tanto en línea como sin conexión)
- La capacidad de aprovechar el poder de los datos sin la necesidad de (es decir, permite a los seres humanos normales utilizar datos para desbloquear perspectivas y análisis profundos para la activación de marketing)

## 1.1.1.3 ¿Por qué elegir Customer Journey Analytics?

CJA no pretende reemplazar una aplicación de BI actual como Power BI, Microstrategy, Locker o Tableau. Estas aplicaciones de BI están pensadas para visualizar datos con el fin de crear paneles corporativos para que todos en una organización puedan ver rápidamente las métricas importantes.\
El objetivo de CJA es aportar poder de análisis a los equipos de marketing y negocios, convirtiéndola en una herramienta de análisis &quot;obligatoria&quot; para esas personas.

Tradicionalmente, las aplicaciones de BI no han podido habilitar la inteligencia de clientes real:

- No pueden realizar procesos de atribución ni análisis de recorrido de clientes.
- Las aplicaciones de BI necesitan conocer la pregunta con antelación
- La estructura de la base de datos limita las consultas interactivas
- Se requieren habilidades SQL.
- Las aplicaciones de BI no te dan la capacidad de preguntar por qué pasó algo.
- Las aplicaciones de BI no tienen conexión directa con los puntos de contacto del cliente.

Debido a lo anterior, los usuarios y analistas de negocios llegan a callejones sin salida casi inmediatamente, lo que hace que el análisis sea costoso, lento, inflexible y desconectado de los sistemas de acción.

Con CJA puede tener una vista 360 del recorrido del cliente, utilizando datos sin conexión y en línea, con las herramientas adecuadas para reducir el tiempo de obtención de información, lo que hace que los usuarios empresariales sean independientes para comprender por qué ocurrió algo y cómo responderlo.

![demostración](./images/cja-use-case.png)

## 1.1.1.4 Comprensión del flujo de trabajo de Customer Journey Analytics

Antes de comenzar los próximos ejercicios, es clave comprender qué pasos son necesarios para introducir datos de Adobe Experience Platform en CJA para visualizarlos y obtener información más detallada. Es lo que llamamos flujo de trabajo de CJA. Echemos un vistazo a esto:

![demostración](./images/cja-work-flow.jpg)

Antes de comenzar los pasos anteriores, no se olvide del paso 0, que es comprender los datos disponibles en Adobe Experience Platform.

**basura entra, basura sale.** ¿Se acuerda? Debe tener una idea clara de qué datos están disponibles y cómo se configuran los esquemas en Adobe Experience Platform. Comprender los datos que se encuentran en Adobe Experience Platform facilitará las cosas, no solo en la parte de conexión de datos, sino también al crear visualizaciones y realizar análisis.

## 1.1.1.5 Paso 0: Explicación de los esquemas y conjuntos de datos de Adobe Experience Platform

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Eche un vistazo a estos esquemas y conjuntos de datos en Adobe Experience Platform.

| Conjunto de datos | Esquema |
| ----------------- |-------------| 
| Sistema de demostración: conjunto de datos de eventos para el sitio web (Global v1.1) | Sistema de demostración: Esquema de eventos para el sitio web (Global v1.1) |
| Sistema de demostración: conjunto de datos de eventos para el centro de llamadas (Global v1.1) | Sistema de demostración: esquema de eventos para el centro de llamadas (Global v1.1) |
| Sistema de demostración: conjunto de datos de eventos para asistentes de voz (Global v1.1) | Sistema de demostración: esquema de eventos para asistentes de voz (Global v1.1) |

Asegúrese de haber comprobado cosas como las siguientes:

- Identidades: CRMID, phoneNumber, ECID, correo electrónico. ¿Qué identidades son los identificadores principales y cuáles son los identificadores secundarios?
Puede encontrar los identificadores abriendo un esquema y mirando el objeto `--aepTenantId--.identification.core`. Eche un vistazo al esquema [Sistema de demostración: esquema de eventos para el sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/identity.png)

- Explore el objeto de comercio dentro del esquema [Sistema de demostración: esquema de eventos para el sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/commerce.png)

- Obtenga una vista previa de todos los [conjuntos de datos](https://experience.adobe.com/platform/dataset/browse?limit=50&page=1&sortDescending=1&sortField=created) y observe los datos

Ya está listo para empezar a utilizar la interfaz de usuario de Customer Journey Analytics.

## Pasos siguientes

Ir a [1.1.2 Conectar conjuntos de datos de Adobe Experience Platform en Customer Journey Analytics](./ex2.md){target="_blank"}

Volver a [Customer Journey Analytics](./customer-journey-analytics-build-a-dashboard.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
