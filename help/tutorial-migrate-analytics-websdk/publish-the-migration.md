---
title: Publicar la migración en ensayo y producción
description: Cuando se haya completado y validado todo el desarrollo de la migración, genérelo en fase de ensayo y, a continuación, publíquelo en producción cuando esté listo.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16767
exl-id: 47c86999-6a9c-4451-8a59-475e8c65ab6a
source-git-commit: 3084590685bee9cd139c27b9a27026f08abf897f
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Publicar la migración en ensayo y producción

Cuando se haya completado y validado todo el desarrollo de la migración, genérelo en fase de ensayo y, a continuación, publíquelo en producción cuando esté listo.

## Información general

Este es realmente el último paso principal de la migración y es mover la biblioteca que ha estado utilizando para desarrollar y probar la migración junto con el entorno de ensayo para la prueba final allí y luego al entorno de producción.

Si vuelve a la lección [Crear y configurar un conjunto de datos](create-and-configure-the-analytics-datastream.md), verá al final que señalamos el conjunto de datos de ensayo para enviar los datos de análisis al mismo grupo de informes de desarrollo (o, alternativamente, a un nuevo grupo de informes de ensayo). También se le recordará que hemos señalado el flujo de datos de producción para enviar datos al grupo de informes de producción existente que ha estado utilizando.
Es solo buena información, ya que ahora insertamos la biblioteca migrada en la ruta de publicación para el ensayo y la producción.

## Inserción en entornos de ensayo y producción

Estos son los pasos que impulsarán nuestra biblioteca a los entornos de ensayo y producción:

1. En la interfaz Etiquetas, seleccione Flujo de publicación en el panel de navegación izquierdo
1. Debería ver su biblioteca de migración en Desarrollo (el nombre es lo que haya elegido al principio de este proceso de migración)

   ![Biblioteca de migración en Dev](assets/migration-lib-in-dev.jpg)

1. Si está seguro de que ya ha agregado todos los cambios a la biblioteca, puede mover la biblioteca hacia adelante bajo los tres puntos y omitir los pasos siguientes. Si no está seguro, siga los siguientes cinco pasos.
1. Haga clic en el nombre de la biblioteca para ir a los detalles de la biblioteca
1. Verifique que se encuentra en la biblioteca correcta mediante el nombre
1. Seleccione Añadir todos los recursos modificados en la parte inferior de la página
1. A continuación, haga clic en Guardar y generar en desarrollo para agregar todos los cambios en cola a la biblioteca

   ![Agregar todos los recursos modificados](assets/add-all-changed-resources.jpg)

1. Esto le llevará de nuevo a la interfaz de flujo de publicación y, si la compilación se completa correctamente, aparecerá un punto verde junto a la biblioteca.
1. A continuación, puede mover la biblioteca hacia adelante en el proceso de publicación, según sus necesidades. Puede configurarlo para aprobarlo, moverlo directamente al entorno de ensayo para probarlo y aprobarlo allí, o incluso moverlo para su aprobación o publicación directamente en producción. De nuevo, esto depende de las necesidades de publicación de su organización.

   ![Proceso de publicación](assets/publishing-process.jpg)

¡Felicidades! En este punto, la implementación de Analytics está completamente en Web SDK.

Voy a añadir una nota importante aquí que tuvimos al principio de este tutorial:

>[!IMPORTANT]
>
>Es importante tener en cuenta que una de las principales razones por las que está realizando esta migración de la implementación es para prepararse para utilizar aplicaciones de Adobe Experience Platform, como Customer Journey Analytics, Real-Time CDP o Journey Optimizer. El uso de los datos del sitio web para este fin incluirá pasos adicionales que no se incluyen en este tutorial, pero este tutorial será sin duda un requisito previo para que progrese aún más su implementación. Ahora que ha completado este tutorial, está listo para realizar los pasos necesarios para enviar estos mismos datos del sitio web a Experience Platform.

¡Buena suerte en su recorrido con los análisis y otros esfuerzos de contenido y marketing!
