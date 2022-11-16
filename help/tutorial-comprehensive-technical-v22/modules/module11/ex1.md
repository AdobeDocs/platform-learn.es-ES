---
title: Customer Journey Analytics - Customer Journey Analytics 101
description: Customer Journey Analytics - Customer Journey Analytics 101
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 3bfa32a7-cf7a-43ad-a375-0d8c8cdb52fc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# 11.1 Customer Journey Analytics 101

## Objetivos

- Comprender el servicio de aplicaciones de CJA
- Aprenda a colocar CJA
- Comprender el flujo de trabajo de CJA: de conexión de datos a perspectivas

## 11.1.1 ¿Qué es Customer Journey Analytics?

Customer Journey Analytics (CJA) proporciona un kit de herramientas a los equipos de inteligencia empresarial y ciencia de datos para vincular y analizar datos de canales múltiples (en línea y sin conexión). Las funciones de CJA proporcionan contexto y claridad al complejo recorrido de clientes multicanal. El contexto proporcionado lleva a una perspectiva procesable para eliminar puntos problemáticos del proceso de conversión del cliente y diseñar y ofrecer experiencias excepcionales para los momentos más importantes.

CJA incorpora a Analysis Workspace en la parte superior de Adobe Experience Platform. Adobe Experience Platform es el centro de la comunicación y la orquestación y, con CJA, las marcas ahora pueden contextualizar y visualizar todos esos datos, de modo que los equipos de negocios y de perspectiva puedan aprender de ellos analizando el recorrido completo de los clientes en línea y sin conexión.

Los equipos empresariales y de Insight pueden hablar con CJA, hacer preguntas y obtener respuestas sobre la marcha con la IU de Analysis Workspace, sencilla para el usuario, con tan solo arrastrar y soltar.

![demostración](./images/cja-adv-analysis1.png)

## 11.1.2 Ventajas principales

Las tres ventajas principales para los clientes son:

- La capacidad de poner perspectivas a disposición de todos (es decir, democratizar el acceso a los datos)
- La capacidad de ver al cliente en un recorrido contextual (es decir, los datos se pueden visualizar secuencialmente, abarcando varios canales tanto en línea como sin conexión)
- La capacidad de aprovechar el poder de los datos sin necesidad de (es decir, permite que los seres humanos normales utilicen los datos para desbloquear perspectivas y análisis profundos para la activación de marketing)

## 11.1.3 ¿Por qué elegir Customer Journey Analytics?

CJA no pretende reemplazar una aplicación BI actual como Power BI, Microestrategia, Locker o Tableau. Estas aplicaciones de BI están pensadas para visualizar datos con el fin de crear tableros corporativos de modo que todos los miembros de una organización puedan ver rápidamente métricas importantes.\
El objetivo de CJA es llevar la potencia de análisis a los equipos de Marketing y Negocios, convirtiéndola en una herramienta de análisis &#39;imprescindible&#39; para esas personas.

Tradicionalmente, las aplicaciones de BI no han sido capaces de habilitar una verdadera inteligencia de clientes:

- No pueden realizar atribuciones y no realizar análisis de recorrido de clientes.
- Las aplicaciones de BI necesitan conocer la pregunta con antelación
- Las consultas interactivas están limitadas por la estructura de la base de datos
- Se requieren habilidades SQL.
- Las aplicaciones de BI no le permiten preguntar por qué ocurrió algo.
- Las aplicaciones de BI no tienen conexión directa con los puntos de contacto del cliente.

Debido a lo anterior, los usuarios de negocios y analistas llegaron a los callejones sin salida casi inmediatamente, lo que hace que el análisis sea caro, lento, inflexible y esté desconectado de los sistemas de acción.

Con CJA puede tener una vista 360 del recorrido del cliente, utilizando datos sin conexión y en línea, con las herramientas adecuadas para reducir el tiempo de perspectiva, hacer que los usuarios empresariales sean independientes en la comprensión de por qué algo sucedió y cómo responder a él.

![demostración](./images/cja-use-case.png)

## 11.1.4 Comprender el flujo de trabajo del Customer Journey Analytics

Antes de comenzar los próximos ejercicios, es fundamental comprender qué pasos se necesitan para introducir datos de Adobe Experience Platform en CJA para visualizarlos y obtener información detallada. Es lo que llamamos Flujo de Trabajo de CJA. Echémosle un vistazo:

![demostración](./images/cja-work-flow.jpg)

Antes de iniciar los pasos anteriores, no olvide el paso 0, que es comprender los datos disponibles en Adobe Experience Platform.

**La basura entra, la basura sale.** ¿Recuerdas? Debe tener una idea clara de qué datos están disponibles y cómo se configuran los esquemas en Adobe Experience Platform. Comprender los datos que se encuentran en Adobe Experience Platform facilitará las cosas, no solo en la parte de conexión de datos, sino también al crear visualizaciones y realizar análisis.

## 11.1.5 Paso 0: Explicación de los esquemas y conjuntos de datos de Adobe Experience Platform

Inicie sesión en Adobe Experience Platform accediendo a esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepSandboxId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar el simulador para pruebas apropiado, verá el cambio de pantalla y ahora estará en su simulador para pruebas dedicado.

![Ingesta de datos](../module2/images/sb1.png)

Eche un vistazo a estos esquemas y conjuntos de datos en Adobe Experience Platform.

| Conjunto de datos | Esquema |
| ----------------- |-------------| 
| Sistema de demostración: conjunto de datos de evento para sitio web (Global v1.1) | Sistema de demostración: Esquema de eventos para sitio web (Global v1.1) |
| Sistema de demostración: conjunto de datos de evento para el centro de llamadas (Global v1.1) | Sistema de demostración: Esquema de eventos para el centro de llamadas (Global v1.1) |
| Sistema de demostración: conjunto de datos de evento para asistentes de voz (Global v1.1) | Sistema de demostración: Esquema de eventos para asistentes de voz (Global v1.1) |

Asegúrese de haber comprobado al menos cosas como:

- Identidades: CRMID, phoneNumber, ECID, correo electrónico. ¿Qué identidades son los identificadores principales, cuáles son los identificadores secundarios?
Puede encontrar los identificadores abriendo un esquema y mirando el objeto `--aepTenantId--.identification.core`. Eche un vistazo al esquema [Sistema de demostración: Esquema de eventos para sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/identity.png)

- Explorar el objeto de comercio dentro del esquema [Sistema de demostración: Esquema de eventos para sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/commerce.png)

- Previsualice todas las [conjuntos de datos](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) y echen un vistazo a los datos

Ya está listo para empezar a usar la interfaz de usuario del Customer Journey Analytics.

Paso siguiente: [11.2 Conectar conjuntos de datos de Adobe Experience Platform en Customer Journey Analytics](./ex2.md)

[Volver al módulo 11](./customer-journey-analytics-build-a-dashboard.md)

[Volver a todos los módulos](../../overview.md)
