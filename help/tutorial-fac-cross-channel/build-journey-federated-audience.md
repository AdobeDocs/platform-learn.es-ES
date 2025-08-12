---
title: Crear un recorrido con datos de audiencias federadas
seo-title: Build a journey with federated audience data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Crear un recorrido con datos de audiencias federadas
description: En esta lección, utilizaremos una audiencia federada en un recorrido de Journey Optimizer.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-build-a-journey-with-federated-audience-data.jpg
hide: true
source-git-commit: fcfadca95c12d0123cfb221e44909f7e0fa8abab
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Creación de un Recorrido con datos de audiencias federadas

En esta lección, aprenderá cómo se puede utilizar una audiencia federada en recorridos dentro de Adobe Journey Optimizer (AJO). Esto incluye el uso de atributos consultados de la Composición de audiencias federada para personalizar la mensajería. Para continuar con la historia del cliente de SecurFinancial y abordar el caso de uso de resegmentación y personalización de clientes, organizamos un recorrido para clientes precalificados. El objetivo es enviar un correo electrónico personalizado basado en atributos federados de Data Warehouse de SecurFinancial.

## Pasos

### Creación de un Recorrido con una audiencia de lectura

1. Vaya al portal **Recorrido** y haga clic en el botón **Crear Recorrido**.

   ![crear-un-recorrido](assets/create-journey.png)

2. Actualice las propiedades del Recorrido con un nuevo nombre: `SecurFinancial - Home Loan Offer - [your lab user ID]`.

3. Haga clic en **Orquestación** y, a continuación, arrastre y suelte el mosaico **Leer audiencia** en el lienzo.

4. Haz clic en el **icono de lápiz** que está junto al cuadro Audiencia, en la parte derecha de la pantalla.

5. En la barra de búsqueda, busca `SecureFinancial Customers - No Loans, Good Credit` y luego haz clic en **Guardar**.

   ![crear-un-recorrido](assets/select-audience.png)

6. Deje todos los ajustes como predeterminados en el menú del lado derecho y haga clic en **Guardar**.

   ![save-audience-settings](assets/save-audience-settings.png)

### Personalizar correo electrónico

1. Haz clic en **Acciones**, luego haz clic en el mosaico **Correo electrónico** y arrástralo al lienzo.

2. En el menú del lado derecho, haga clic en **Configuración de correo electrónico** y seleccione **Marketing por correo electrónico**. Luego haz clic en **Editar contenido**.

3. En la línea de asunto, agregue: `Learn more about SecurFinancial Home Loan`. Luego haz clic en **Editar cuerpo del correo electrónico**.

4. Haga clic en el botón **Plantilla de contenido** en la esquina superior derecha. Busque y seleccione `SecureFinancial Template`, luego haga clic en **Confirmar**.

   ![recorrido-email-config](assets/journey-email-config.png)

   ![recorrido-email-confirm](assets/journey-email-confirm.png)

5. Revise la plantilla y haga clic en **Usar plantilla**.

6. Ahora se encuentra en el Designer de correo electrónico. Pase el ratón sobre la macro `{profile.person.name.firstName}` y haga clic en el **avatar de personalización**.

7. En la ventana de personalización, explore en profundidad la siguiente ruta de carpeta: `[sandbox] > audienceEnrichment > CustomerAudienceUpload`

8. Haga clic en la carpeta **leer audiencia**. Los atributos de enriquecimiento de su audiencia federada se pueden encontrar aquí.

9. Seleccione el atributo **First Name** en el generador de expresiones. El correo electrónico expresará de forma dinámica el valor del nombre del cliente para personalizar el correo electrónico.

10. Haga clic en **Guardar**.

11. Ahora que se ha agregado la personalización del nombre, agregue `Hi, ` delante de la variable de personalización. Luego haz clic en **Guardar**.

    ![recorrido-email-save](assets/journey-email-save.png)

12. Haga clic dos veces en el botón **Atrás** para regresar al lienzo de recorrido. A continuación, en el menú **Acción: enviar correo electrónico** que se encuentra a la derecha, haga clic en **Guardar**.

   ![guardar-final-recorrido](assets/save-final-journey.png)

¡Felicidades! Ha creado un recorrido en AJO utilizando una audiencia federada y atributos de enriquecimiento federados.

Ahora veremos cómo [enriquecer audiencias existentes](audience-enrichment-demo.md) en Experience Platform con datos federados del almacén de datos.
