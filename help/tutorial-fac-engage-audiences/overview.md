---
title: Interactúe con las audiencias de su Data Warehouse mediante la composición de audiencias federada
description: La Composición de audiencias federada es una potente función que permite a los arquitectos e ingenieros de datos crear y enriquecer audiencias directamente desde almacenes de datos de terceros.
breadcrumb-title: Información general
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Interactúe con las audiencias de su Data Warehouse mediante la composición de audiencias federada

La Composición de audiencias federada (FAC) es una potente función disponible para los entornos de Adobe Real-Time Customer Data Platform (Real-Time CDP) y Adobe Journey Optimizer. Permite a los arquitectos e ingenieros de datos revisar y activar audiencias de alto valor directamente desde [almacenes de datos empresariales admitidos](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}, sin copiar ni mover datos de clientes a Adobe Experience Platform (AEP). Este enfoque de CDP componible (una solución a medida para los clientes) se alinea con las tendencias del sector, lo que permite a las empresas aprovechar su infraestructura de datos para experiencias digitales personalizadas y, al mismo tiempo, mantener la gobernanza de los datos.

## Contexto empresarial

SecurFinancial es una empresa líder de servicios financieros. Utiliza su riqueza de datos de clientes en diferentes fuentes para personalizar ofertas y campañas para un gran número de segmentos. Tienen pensado utilizar la función de composición de audiencias federada de Real-Time CDP de Adobe para depurar audiencias de su almacén de datos y activarlas en los destinos de Adobe Experience Platform, así como Adobe Journey Optimizer para ofrecer una solución personalizada para ofrecer experiencias de cliente personalizadas.

## Escenario empresarial

SecurFinancial quiere lanzar una campaña por correo electrónico para redirigirse a sus clientes que están precualificados para un préstamo basado en un buen crédito y no tienen un préstamo activo en su cartera de SecurFinancial. Mientras están ingiriendo datos de comportamiento en línea en tiempo real, se enfrentan a desafíos para identificar la precalificación de los clientes, ya que están restringidos de ingerir información de crédito en AEP. Para calificar a los clientes preseleccionados sin mover datos restringidos, utilizarán la Composición de audiencia federada para enriquecer su audiencia de comportamiento de AEP.

## Guía

Esta guía muestra cómo se admite el escenario de SecureFinancial Business. Específicamente, cubre cómo exponemos las audiencias a sistemas que necesitan estas audiencias, incluida una cuenta de almacenamiento S3, un recorrido en Journey Optimizer para impulsar una campaña de correo electrónico y una redirección in situ a clientes que fueron preaprobados para un préstamo.

Los pasos incluyen:

1. Conecte Adobe Experience Platform a un almacén de datos empresarial.
2. Cree una audiencia con Composición de audiencia federada.
3. Asigne una audiencia federada a un destino externo de Amazon S3.
4. Cree un recorrido de cliente con datos de audiencias federadas.
5. Enriquezca una audiencia con datos federados.
6. Impulse la personalización &quot;en el momento&quot; en Edge.

## Requisitos previos

Para realizar actividades similares en su entorno, asegúrese de que dispone de lo siguiente:

- Acceso a una cuenta de Adobe Experience Platform aprovisionada con Real-Time CDP o Journey Optimizer.
- Permisos de administrador del sistema o la capacidad de configurar permisos.
- Familiaridad con conceptos de Adobe Experience Platform, tales como esquemas, conjuntos de datos y audiencias (recomendado: complete la [Introducción a la lista de reproducción de Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} en Experience League).
- Acceso a un [almacén de datos empresarial](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} compatible.
- Conocimientos básicos de SQL para consultar almacenes de datos.
- **Entornos de espacio aislado**: cree un espacio aislado en la instancia de su organización para experimentar con seguridad sin afectar a los datos de producción.
- **Conexión de Data Warehouse**: este tutorial usa una conexión de Snowflake, pero puede usar cualquier [almacén de datos compatible](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Primero, vamos a revisar la [Arquitectura y flujo de alto nivel para la composición de audiencias federada](fac-architecture-and-flow.md).
