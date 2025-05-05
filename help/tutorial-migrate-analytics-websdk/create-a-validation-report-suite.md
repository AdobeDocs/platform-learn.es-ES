---
title: Crear un grupo de informes de validación
description: Cree un grupo de informes en Adobe Analytics que pueda utilizar para validar los datos de Web SDK al migrar sus sitios desde la implementación antigua.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16756
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Crear un grupo de informes de validación

Cree un grupo de informes en Adobe Analytics que pueda utilizar para validar los datos de Web SDK al migrar sus sitios desde la implementación antigua.

Según el tamaño y la complejidad de la implementación de Analytics, la migración a Web SDK podría tardar un poco. Durante ese tiempo, deberá validar su trabajo y asegurarse de que los datos fluyen correctamente a los informes de Adobe Analytics. En lugar de insertar esos datos en un grupo de informes junto con los datos de producción, o incluso con cualquier otro dato de desarrollo, se recomienda crear un nuevo grupo de informes nuevo que pueda utilizar para esta migración. En la siguiente lección crearemos y configuraremos nuevos &quot;flujos de datos&quot; para el desarrollo, el ensayo y la producción. Cuando lo hagamos, necesitaremos saber el ID del grupo de informes para la configuración.

## Creación del nuevo grupo de informes

1. Abra Adobe Analytics y vaya a la configuración del **grupo de informes** en el Admin Console

   ![Admin Console](assets/aa-admin-console.jpg).

1. Seleccionar **[!UICONTROL Agregar grupo de informes]**

   ![Agregar grupo de informes](assets/add-report-suite.jpg)

1. Rellene el formulario para crear un nuevo grupo de informes. Aunque puede elegir crear el nuevo grupo de informes a partir de una plantilla, incluso una plantilla en blanco, probablemente le irá mejor elegir la opción **Duplicar un grupo de informes existente** y elegir el grupo de informes que está migrando a Web SDK. Esto le permitirá tener los mismos nombres y configuraciones que utiliza para probar los datos recién migrados, lo que facilita su validación a medida que avanza. Rellene todos los campos obligatorios y guarde el nuevo grupo de informes de desarrollo de migración.

   ![Nuevo grupo de informes de desarrollo de migración](assets/new-websdk-validation-report-suite.jpg)

1. Tome nota del ID del nuevo grupo de informes, ya que lo necesitará en la siguiente lección cuando configure flujos de datos para la implementación de Web SDK. El título del sitio también será bueno para recordar, ya que puede utilizarlo en Analysis Workspace para elegir el grupo de informes de desarrollo de migración en su proyecto de Analytics.

>[!TIP]
>
>Para ver un vídeo introductorio sobre la creación de grupos de informes, consulte [Explicación y creación de grupos de informes](https://experienceleague.adobe.com/es/docs/analytics-learn/tutorials/intro-to-analytics/analytics-basics/understanding-and-creating-report-suites){target="_blank"}.

