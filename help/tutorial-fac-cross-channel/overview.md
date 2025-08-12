---
title: Desbloquee perspectivas en canales múltiples con la composición de audiencias federada
description: La Composición de audiencias federada es una potente función que permite a los arquitectos e ingenieros de datos crear y enriquecer audiencias directamente desde almacenes de datos de terceros.
breadcrumb-title: Información general
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Información general

La composición de audiencias federada es una potente función disponible para los entornos de Adobe Real-Time Customer Data Platform (Real-Time CDP) y Adobe Journey Optimizer. Permite a los arquitectos de datos y a los ingenieros de datos crear y enriquecer audiencias directamente desde [almacenes de datos de terceros](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} admitidos, sin replicar los datos en Adobe Experience Platform. Este tutorial proporciona una guía práctica para que los usuarios técnicos conecten almacenes de datos empresariales, creen y enriquezcan audiencias y las activen para experiencias de marketing personalizadas.

## Objetivos de aprendizaje

Al completar este tutorial, deberá hacer lo siguiente:

- Obtenga información sobre cómo conectar Adobe Experience Platform a un almacén de datos empresarial.
- Aprenda a crear y administrar audiencias mediante la Composición de audiencias federada.
- Aprenda a enriquecer las audiencias existentes con los datos del almacén.
- Asigne audiencias federadas a destinos externos como Amazon S3.
- Genere recorridos de clientes con datos de audiencias federadas.
- Valide datos y procesos mediante ejercicios prácticos y demostraciones.

Este tutorial está diseñado para arquitectos e ingenieros de datos que trabajan con Real-Time CDP o Journey Optimizer. Supone estar familiarizado con los conceptos básicos de Adobe Experience Platform y Data Warehouse.

## Contexto empresarial

SecurFinancial es una empresa líder de servicios financieros. Utiliza su riqueza de datos de clientes en diferentes fuentes para personalizar ofertas y campañas para un gran número de segmentos. Tienen previsto utilizar la función de composición de audiencia federada de Real-Time CDP de Adobe, que permite a las empresas utilizar su almacén de datos existente mientras utilizan las aplicaciones de Adobe Experience Platform para ofrecer experiencias de cliente personalizadas. Las ventajas principales incluyen:

- **Acceso a los datos del almacén**: Cree audiencias de alto valor a partir de conjuntos de datos en almacenes de datos compatibles sin replicación de datos.
- **Movimiento de datos minimizado**: consulte los datos directamente en el almacén, reduciendo la duplicación y manteniendo el control de datos.
- **Flujos de trabajo de experiencia unificados**: Depure y active audiencias en Adobe Experience Platform para casos de uso entre canales.
- **Personalización mejorada**: enriquezca perfiles y audiencias con atributos de almacén para potenciar experiencias activadas en tiempo real.

## Escenario empresarial

SecurFinancial quiere lanzar una campaña por correo electrónico para redirigirse a sus clientes que están precualificados para un préstamo basado en un buen crédito y no tienen un préstamo activo en su cartera de SecurFinancial. Mientras están ingiriendo datos de comportamiento en línea en tiempo real, se enfrentan a desafíos para identificar la precalificación de clientes, ya que están restringidos de ingerir información de crédito en AEP. Para calificar a los clientes precalificados sin mover los datos restringidos, utilizarán la Composición de audiencia federada para enriquecer su audiencia de comportamiento de AEP.



## Requisitos previos

Para seguir este tutorial, asegúrese de lo siguiente:

- Acceso a una cuenta de Adobe Experience Platform aprovisionada con Real-Time CDP o Journey Optimizer.
- Permisos de administrador del sistema o la capacidad de configurar permisos.
- Familiaridad con conceptos de Adobe Experience Platform, tales como esquemas, conjuntos de datos y audiencias (recomendado: complete la [Introducción a la lista de reproducción de Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} en Experience League).
- Acceso a un almacén de datos empresarial compatible (por ejemplo, Amazon Redshift, Azure Synapse Analytics, Snowflake o Google BigQuery).
- Conocimientos básicos de SQL para consultar almacenes de datos.

## Uso de este tutorial

Este tutorial está estructurado para usuarios técnicos. Las lecciones se basan unas en otras, así que complételas en orden a menos que se indique lo contrario.

## Notas técnicas

- **Entornos de espacio aislado**: cree un espacio aislado en la instancia de Real-Time CDP de su organización para experimentar con seguridad sin afectar a los datos de producción.
- **Conexión de Data Warehouse**: Este tutorial usa una conexión de Snowflake, pero puede usar cualquier [almacén de nube compatible](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Empiece con la lección [Conexión de Data Warehouse](data-warehouse-connection.md) para comenzar a configurar su entorno.
