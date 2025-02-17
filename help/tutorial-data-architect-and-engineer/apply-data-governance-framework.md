---
title: Aplicación del marco de gobernanza de datos
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Aplicación del marco de gobernanza de datos
description: En esta lección, aplicará el marco de trabajo de control de datos a los datos que ha introducido en su zona protegida.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---

# Aplicación del marco de gobernanza de datos

<!--15min-->

En esta lección, aplicará el marco de trabajo de control de datos a los datos que ha introducido en su zona protegida.

Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de Experience Platform en varios niveles, incluido el control del uso de datos.

Antes de comenzar los ejercicios, vea estos vídeos cortos sobre la gobernanza de datos:
>[!VIDEO](https://video.tv.adobe.com/v/36653?learn=on&enablevpops)

>[!VIDEO](https://video.tv.adobe.com/v/29708?learn=on&enablevpops)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## Escenario empresarial

Luma promete a los miembros de su programa de fidelidad que los datos de fidelidad no se compartirán con terceros. Implementaremos este escenario en el resto de la lección.

## Aplicar etiquetas de gobernanza de datos

El primer paso del proceso de control de datos es aplicar etiquetas de control a los datos. Antes de hacerlo, echemos un vistazo rápido a las etiquetas disponibles:

1. En la interfaz de usuario de Platform, seleccione **[!UICONTROL Políticas]** en el panel de navegación izquierdo
1. Vaya a la pestaña **[!UICONTROL Etiquetas]** para ver todas las etiquetas de la cuenta.

Hay muchas etiquetas listas para usar, además de que puede crear las suyas propias con el botón [!UICONTROL Crear etiqueta]. Existen tres tipos principales: [!UICONTROL etiquetas de contrato], [!UICONTROL etiquetas de identidad] y [!UICONTROL etiquetas confidenciales] que corresponden a motivos comunes por los que los datos pueden estar restringidos. Cada una de las etiquetas tiene un [!UICONTROL Nombre descriptivo] y un [!UICONTROL Nombre] corto, que es solo una abreviatura del tipo y un número. Por ejemplo, la etiqueta [!DNL C1] es para &quot;Sin exportación de terceros&quot;, que es lo que necesitamos para nuestra política de fidelización.

![Etiqueta de control de datos](assets/governance-policies.png)

Ahora es el momento de etiquetar los datos cuyo uso queremos restringir:

1. En la interfaz de usuario de Platform, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo
1. Abrir `Luma Loyalty Dataset`
1. Vaya a la pestaña **[!UICONTROL Control de datos]**
1. Puede aplicar etiquetas a campos individuales o aplicarlas a todo el conjunto de datos. Aplicaremos la etiqueta a todo el conjunto de datos. Haga clic en el icono de lápiz. Si no ve el icono, intente hacer que el explorador sea más ancho o desplácese por el panel central hacia la derecha.
   ![Gobernanza de datos](assets/governance-dataset.png)
1. En el modal, expanda la sección **[!UICONTROL Etiquetas de contrato]** y compruebe la etiqueta **[!UICONTROL C2]**
1. Seleccione el botón **[!UICONTROL Guardar cambios]**
   ![Gobernanza de datos](assets/governance-applyLabel.png)
1. Al volver a la pantalla principal [!UICONTROL Control de datos], con la opción **[!UICONTROL Mostrar etiquetas heredadas]** activada, puede ver cómo se ha aplicado la etiqueta a todos los campos del conjunto de datos.
   ![Gobernanza de datos](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## Crear políticas de gobernanza de datos

Ahora que nuestros datos están etiquetados, podemos crear una política.

1. En la interfaz de usuario de Platform, seleccione **[!UICONTROL Políticas]** en el panel de navegación izquierdo
1. En la pestaña Examinar, ya existe una directiva predeterminada llamada &quot;restricción de exportación de terceros&quot; que asocia la etiqueta C2 con la acción de marketing [!UICONTROL Exportar a terceros], exactamente lo que necesitamos.
1. Seleccione la directiva y, a continuación, actívela mediante la opción **[!UICONTROL Estado de la directiva]**
   ![Gobernanza de datos](assets/governance-enablePolicy.png)

Puede crear sus propias directivas si selecciona el botón **[!UICONTROL Crear directiva]**. Esto abre un asistente que le permite combinar varias etiquetas y restricciones de acciones de marketing.

## Aplicar políticas de gobernanza

La aplicación de las políticas de gobernanza es obviamente un componente clave del marco. La aplicación se produce después del flujo cuando los datos se activan y envían fuera de Platform, especialmente con Real-Time Customer Data Platform, para el que puede obtener o no licencias. De cualquier manera, está fuera del alcance de este tutorial. Pero para que no te quedes colgado, puedes aprender más sobre cómo se aplican las políticas en este video, que he puesto en la cola de la porción relevante. También le mostrará lo que sucede cuando se infringe una directiva.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on&enablevpops)


## Recursos adicionales

* [Documentación de control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es)
* [Referencia de API del servicio de conjunto de datos](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [Referencia de API del servicio de directivas de gobernanza](https://www.adobe.io/experience-platform-apis/references/policy-service/)

Ahora pasemos al [servicio de consultas](run-queries.md).
