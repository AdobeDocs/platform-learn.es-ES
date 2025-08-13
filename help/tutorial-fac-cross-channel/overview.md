---
title: Desbloquee perspectivas en canales múltiples con la composición de audiencias federada
description: La Composición de audiencias federada es una potente función que permite a los arquitectos e ingenieros de datos crear y enriquecer audiencias directamente desde almacenes de datos de terceros.
breadcrumb-title: Información general
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: 15619a8419f608da6a77745fabf72c356a2ac4b4
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Información general

La composición de audiencias federada es una potente función disponible para los entornos de Adobe Real-Time Customer Data Platform (Real-Time CDP) y Adobe Journey Optimizer. Permite a los arquitectos de datos y a los ingenieros de datos crear y enriquecer audiencias directamente desde [almacenes de datos de terceros admitidos](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} sin replicar datos en Adobe Experience Platform. Este tutorial proporciona una guía práctica para que los usuarios técnicos conecten almacenes de datos empresariales, creen y enriquezcan audiencias y las activen para experiencias de marketing personalizadas.

## Guía visual

Esta guía visual muestra los pasos de cada una de las actividades realizadas para admitir distintos aspectos del escenario empresarial. El objetivo es proporcionarle actividades que pueda aprovechar en su entorno, como las siguientes:

- Conecte Adobe Experience Platform a un almacén de datos empresarial.
- Cree y gestione audiencias mediante la Composición de audiencias federada.
- Asigne audiencias federadas a destinos externos como Amazon S3.
- Enriquezca las audiencias existentes con datos federados.
- Cree audiencias para impulsar la personalización &quot;en el momento&quot;.
- Genere recorridos de clientes con datos de audiencias federadas.

Esta guía está diseñada para arquitectos e ingenieros de datos que trabajan con Real-Time CDP o Journey Optimizer. Supone estar familiarizado con los conceptos básicos de Adobe Experience Platform y Data Warehouse.

## Contexto empresarial

SecurFinancial es una empresa líder de servicios financieros. Utiliza su riqueza de datos de clientes en diferentes fuentes para personalizar ofertas y campañas para un gran número de segmentos. Tienen previsto utilizar la función de composición de audiencia federada de Real-Time CDP de Adobe, que permite a las empresas utilizar su almacén de datos existente mientras utilizan las aplicaciones de Adobe Experience Platform para ofrecer experiencias de cliente personalizadas. Las ventajas principales incluyen:

- **Acceso a los datos del almacén**: Cree audiencias de alto valor a partir de conjuntos de datos en almacenes de datos compatibles sin replicación de datos.
- **Movimiento de datos minimizado**: consulte los datos directamente en el almacén, reduciendo la duplicación y manteniendo el control de datos.
- **Flujos de trabajo de experiencia unificados**: Depure y active audiencias en Adobe Experience Platform para casos de uso entre canales.
- **Personalización mejorada**: enriquezca perfiles y audiencias con atributos de almacén para potenciar experiencias activadas en tiempo real.

## Escenario empresarial

SecurFinancial quiere lanzar una campaña por correo electrónico para redirigirse a sus clientes que están precualificados para un préstamo basado en un buen crédito y no tienen un préstamo activo en su cartera de SecurFinancial. Mientras están ingiriendo datos de comportamiento en línea en tiempo real, se enfrentan a desafíos para identificar la precalificación de clientes, ya que están restringidos de ingerir información de crédito en AEP. Para calificar a los clientes precalificados sin mover los datos restringidos, utilizarán la Composición de audiencia federada para enriquecer su audiencia de comportamiento de AEP.

## Requisitos previos

Para realizar actividades similares en su entorno, asegúrese de que dispone de lo siguiente:

- Acceso a una cuenta de Adobe Experience Platform aprovisionada con Real-Time CDP o Journey Optimizer.
- Permisos de administrador del sistema o la capacidad de configurar permisos.
- Familiaridad con conceptos de Adobe Experience Platform, tales como esquemas, conjuntos de datos y audiencias (recomendado: complete la [Introducción a la lista de reproducción de Adobe Experience Platform](https://experienceleague.adobe.com/es/playlists/experience-platform-introduction?lang=en){target="_blank"} en Experience League).
- Acceso a un almacén de datos empresarial compatible (por ejemplo, Amazon Redshift, Azure Synapse Analytics, Snowflake o Google BigQuery).
- Conocimientos básicos de SQL para consultar almacenes de datos.
- **Entornos de espacio aislado**: cree un espacio aislado en la instancia de Real-Time CDP de su organización para experimentar con seguridad sin afectar a los datos de producción.
- **Conexión de Data Warehouse**: Este tutorial usa una conexión de Snowflake, pero puede usar cualquier [almacén de nube compatible](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/start/access-prerequisites).

Empecemos con [Data Warehouse Connection](data-warehouse-connection.md).
