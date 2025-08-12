---
title: Crear un público
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Crear un público
description: En esta lección, configuramos una conexión entre Adobe Experience Platform y su Data Warehouse empresarial para habilitar la Composición federada de audiencias.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: b5611dccdba66d31f7dfcd96506e06d1bdd5fb3d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 3%

---


# Ejercicio de creación de audiencias

Este ejercicio le guiará a través de la creación de una audiencia a partir de Data Warehouse mediante la Composición de audiencia federada. Creamos una audiencia para calificar a los clientes de SecurFinancial que tienen una puntuación crediticia de 650 o superior y que actualmente no tienen un préstamo en su cartera de SecurFinancial.

## Pasos

1. En el portal **Cliente > Audiencias**, haga clic en la ficha **Composiciones federadas**.
2. Haga clic en **Crear composición**.

   ![crear-composición](assets/create-composition.png)

3. Etiquete la composición como `SecurFinancial Customers - No Loans, Good Credit`. Haga clic en **Crear**.

4. Haga clic en el botón **+** del lienzo y seleccione **Generar audiencia**. Debe aparecer el carril derecho.

5. Haga clic en **Seleccionar un esquema** y seleccione el esquema **FSI_CRM**; a continuación, haga clic en **Confirmar**.

6. Haga clic en **Continuar**. En la ventana del generador de consultas, haga clic en el botón **+** y luego en **Condición personalizada**. Cree las siguientes condiciones:

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *La última condición garantiza que los datos de preferencias de marketing se usen para segmentar a los clientes que han elegido el correo electrónico como canal de comunicación preferido*.

   **Nota:** El campo de valor distingue entre mayúsculas y minúsculas.

   La consulta debería tener el siguiente aspecto:

   ![generador de consultas](assets/query-builder.png)

7. Haga clic en el siguiente botón **+** y luego haga clic en **Guardar audiencia**. Etiquete este paso como `SecurFinancial Customers - No Loans, Good Credit`. Utilice el mismo valor que la etiqueta de audiencia.

8. Añada las siguientes asignaciones de audiencia:

   - **Campo de audiencia de Source:** CORREO ELECTRÓNICO
   - **Campo de audiencia de Source:** CURRENTPRODUCTS
   - **Campo de audiencia de Source:** NOMBRE

9. Seleccione la identidad y el área de nombres principales que se utilizarán para los perfiles:

   - **Campo de identidad principal:** Correo electrónico
   - **Área de nombres de identidad:** Correo electrónico

10. Haga clic en **Guardar** y, a continuación, haga clic en **Iniciar** para ejecutar la consulta de la composición que acaba de crear.

**Nota:** Utilizamos información de productos y crédito para crear nuestra audiencia que no movió datos confidenciales, como la puntuación crediticia, a plataformas de flujo descendente para su activación.

Para obtener más información sobre la composición de audiencias, visita [Experience League](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Ahora que se ha creado nuestra audiencia federada, avanzaremos con [la asignación a una cuenta S3](map-federated-audience-to-s3.md).
