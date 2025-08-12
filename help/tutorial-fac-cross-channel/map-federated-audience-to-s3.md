---
title: Asignación de una audiencia federada a S3
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Asignación de una audiencia federada a S3
description: En esta lección, asignaremos una audiencia federada a un destino de Real-Time CDP descendente para ofrecer compatibilidad con una experiencia sin conexión personalizada.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Asignar una audiencia federada a S3 para aprovechar los atributos de audiencia para el enriquecimiento

En este ejercicio, aprenderá a aprovechar los atributos de audiencia en su almacén de datos para enriquecer la experiencia de su audiencia en flujos de trabajo de activación descendentes mediante destinos de RTCDP. Para SecurFinancial, estos atributos federados se pueden utilizar para mejorar la experiencia de personalización sin conexión de la audiencia del cliente. En este ejemplo, asignaremos la audiencia federada a un destino preconfigurado de Amazon S3.

## Pasos

1. Vaya al portal **Destinos**.

2. Haga clic en el botón de **3 menú de puntos** junto al destino preconfigurado de Amazon S3 y, a continuación, haga clic en **Activar audiencias**.

   ![activar-audiencias](assets/activate-audiences.png)

3. Seleccione el **destino S3** y haga clic en **Siguiente**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Seleccione la audiencia **Clientes financieros seguros - Sin préstamos, buen crédito**.

   ![select-s3-audience](assets/select-s3-audience.png)

5. En la sección **Programación**, deje todas las configuraciones predeterminadas y haga clic en **Siguiente**.

6. En el paso **Asignación**, asegúrese de que `xdm: personalEmail.address` esté incluido y seleccionado como **Clave de anulación de duplicación**. Luego haz clic en **Siguiente**:

   ![clave de anulación de duplicación](assets/deduplication-key.png)

7. En el siguiente paso de asignación, puede seleccionar atributos de enriquecimiento basados en asignaciones de campos de audiencia en la composición de audiencia federada. Haga clic en el icono **lápiz (editar)** para ver los atributos preseleccionados.

   ![edit-attributes](assets/edit-attributes.png)

   ![atributos-finales](assets/final-attribution.png)

8. Revise su asignación de audiencia y pulse **Finalizar**.

Estamos listos para pasar a [crear un recorrido](build-journey-federated-audience.md).
