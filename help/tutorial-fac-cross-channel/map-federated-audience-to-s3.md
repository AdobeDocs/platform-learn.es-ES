---
title: Asignación de una audiencia federada a S3
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Asignación de una audiencia federada a S3
description: En este ejercicio visual, asignaremos una audiencia federada a un destino de Real-Time CDP descendente para ofrecer compatibilidad con una experiencia sin conexión personalizada.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: 15619a8419f608da6a77745fabf72c356a2ac4b4
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Asignar una audiencia federada a S3 para aprovechar los atributos de audiencia para el enriquecimiento

Puede aprovechar los atributos de audiencia en su almacén de datos para enriquecer la experiencia de su audiencia en flujos de trabajo de activación descendentes mediante destinos de RTCDP. Para SecurFinancial, estos atributos federados se pueden utilizar para mejorar la experiencia de personalización sin conexión de la audiencia del cliente. A continuación, la audiencia federada se asigna a un destino preconfigurado de Amazon S3.

## Pasos

1. Vaya al portal **Destinos**.

2. Haga clic en el botón de **3 menú de puntos** junto al destino preconfigurado de Amazon S3 y, a continuación, haga clic en **Activar audiencias**.

   ![activar-audiencias](assets/activate-audiences.png)

3. Seleccione el **destino S3** y haga clic en **Siguiente**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Seleccione la audiencia adecuada. En nuestro ejemplo: **Clientes financieros seguros - Sin préstamos, buen crédito** audiencia.

   ![select-s3-audience](assets/select-s3-audience.png)

5. En la sección **Programación**, use la configuración predeterminada y haga clic en **Siguiente**.

6. En el paso **Mapping**, elija la clave de anulación de duplicación. En nuestro ejemplo, `xdm: personalEmail.address` se incluye y se selecciona como **Clave de deduplicación**. Luego haz clic en **Siguiente**:

   ![clave de anulación de duplicación](assets/deduplication-key.png)

7. En el paso de asignación, seleccione atributos de enriquecimiento basados en asignaciones de campos de audiencia en la composición de audiencia federada. Haga clic en el icono **lápiz (editar)** para ver los atributos preseleccionados.

   ![edit-attributes](assets/edit-attributes.png)

   ![atributos-finales](assets/final-attribution.png)

8. Revise su asignación de audiencia y pulse **Finalizar**.

>[**RESUMEN**]
>
> Creamos con éxito una audiencia y la activamos en un destino S3 con facilidad. La interfaz de usuario de la plataforma permite a los equipos de marketing crear y activar audiencias rápidamente, lo que reduce el tiempo de obtención de valor. Los clientes que siguen este enfoque han utilizado tres casos de uso por primera vez en menos de dos meses.

Estamos listos para pasar a [crear un recorrido](build-journey-federated-audience.md).
