---
title: Transmitir datos a Adobe Experience Platform con el SDK web de Platform
description: Obtenga información sobre cómo transmitir datos web a Adobe Experience Platform con el SDK web. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
jira: KT-15407
exl-id: 4d749ffa-e1c0-4498-9b12-12949807b369
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '2107'
ht-degree: 4%

---

# Transmitir datos al Experience Platform con SDK web

Obtenga información sobre cómo transmitir datos web a Adobe Experience Platform con SDK web de Platform.

Experience Platform es la columna vertebral de todas las nuevas aplicaciones de Experience Cloud, como Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics y Adobe Journey Optimizer. Estas aplicaciones están diseñadas para utilizar el SDK web de Platform como método óptimo de recopilación de datos web.

![Diagrama del SDK web y Adobe Experience Platform](assets/dc-websdk-aep.png)

Experience Platform utiliza el mismo esquema XDM creado anteriormente para capturar datos de evento del sitio web de Luma. Cuando esos datos se envían al Edge Network de Platform, la configuración del conjunto de datos puede reenviarlos al Experience Platform.

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Crear un conjunto de datos en Adobe Experience Platform
* Configuración de la secuencia de datos para enviar datos del SDK web a Adobe Experience Platform
* Habilitar el streaming de datos web para el perfil del cliente en tiempo real
* Validar que los datos hayan llegado tanto al conjunto de datos de Platform como al Perfil del cliente en tiempo real
* Ingesta de datos de programa de fidelización de muestra en Platform
* Crear una audiencia de Platform simple

## Requisitos previos

Para completar esta lección, primero debe:

* Tener acceso a una aplicación de Adobe Experience Platform como Real-time Customer Data Platform, Journey Optimizer o Customer Journey Analytics.
* Complete las lecciones anteriores de las secciones Configuración inicial y Configuración de etiquetas de este tutorial.

>[!NOTE]
>
>Si no tiene ninguna aplicación de Platform, puede omitir esta lección o continuar leyendo.

## Crear un conjunto de datos

Todos los datos que se incorporan correctamente a Adobe Experience Platform se conservan dentro del lago de datos como conjuntos de datos. A [conjunto de datos](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/overview) es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

Vamos a configurar un conjunto de datos para los datos de evento web de Luma:


1. Vaya a la [Experience Platform](https://experience.adobe.com/platform/) o [Journey Optimizer](https://experience.adobe.com/journey-optimizer/) interfaz
1. Confirme que se encuentra en el entorno limitado de desarrollo que utiliza para este tutorial.
1. Abrir **[!UICONTROL Administración de datos > Conjuntos de datos]** desde la navegación izquierda
1. Seleccionar **[!UICONTROL Crear conjunto de datos]**

   ![Crear esquema](assets/experience-platform-create-dataset.png)

1. Seleccione el **[!UICONTROL Crear conjunto de datos a partir de esquema]** opción

   ![Crear conjunto de datos a partir de esquema](assets/experience-platform-create-dataset-schema.png)

1. Seleccione el `Luma Web Event Data` esquema creado en [lección anterior](configure-schemas.md) y luego seleccione **[!UICONTROL Siguiente]**

   ![Conjunto de datos, seleccionar esquema](assets/experience-platform-create-dataset-schema-selection.png)

1. Proporcione un **[!UICONTROL Nombre]** y opcional **[!UICONTROL Descripción]** para el conjunto de datos. Para este ejercicio, utilice `Luma Web Event Data`, luego seleccione **[!UICONTROL Finalizar]**

   ![Nombre del conjunto de datos ](assets/experience-platform-create-dataset-schema-name.png)

Ahora hay configurado un conjunto de datos para empezar a recopilar datos de su implementación del SDK web de Platform.

## Configuración de la secuencia de datos

Ahora puede configurar los [!UICONTROL secuencia de datos] para enviar datos a [!UICONTROL Adobe Experience Platform]. La secuencia de datos es el vínculo entre la propiedad de etiquetas, el Edge Network de Platform y el conjunto de datos del Experience Platform.

1. Abra el [Recopilación de datos](https://experience.adobe.com/#/data-collection){target="blank"} interfaz
1. Seleccionar **[!UICONTROL Datastreams]** desde la navegación izquierda
1. Abra la secuencia de datos que creó en la [Configuración de una secuencia de datos](configure-datastream.md) lección, `Luma Web SDK`

   ![Seleccione la secuencia de datos del SDK web de Luma](assets/datastream-luma-web-sdk-development.png)

1. Seleccionar **[!UICONTROL Añadir servicio]**
   ![Añadir un servicio al conjunto de datos](assets/experience-platform-addService.png)
1. Seleccionar **[!UICONTROL Adobe Experience Platform]** como el **[!UICONTROL Servicio]**
1. Seleccionar `Luma Web Event Data` como el **[!UICONTROL Conjunto de datos de evento]**

1. Seleccione **[!UICONTROL Guardar]**.

   ![Configuración de secuencia de datos](assets/experience-platform-datastream-config.png)

A medida que genera tráfico en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) asignado a la propiedad tag, los datos rellenan el conjunto de datos en Experience Platform.

## Validación del conjunto de datos

Este paso es fundamental para asegurarse de que los datos hayan llegado al conjunto de datos. Existen dos aspectos para validar los datos enviados al conjunto de datos.

* Validar mediante [!UICONTROL Experience Platform Debugger]
* Validar mediante [!UICONTROL Previsualizar conjunto de datos]
* Validar mediante [!UICONTROL Servicio de consultas]

### Experience Platform Debugger

Estos pasos son más o menos los mismos que realizó en el [Lección de Debugger](validate-with-debugger.md). Sin embargo, como los datos solo se enviarán a Platform después de haberlos habilitado en el conjunto de datos, debe generar algunos datos de ejemplo más:

1. Abra el [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) y seleccione la [!UICONTROL Experience Platform Debugger] icono de extensión

1. Configure Debugger para asignar la propiedad de etiqueta a *su* Entorno de desarrollo, tal como se describe en la sección [Validar con Debugger](validate-with-debugger.md) lección

   ![El entorno de desarrollo de Launch que se muestra en Debugger](assets/experience-platform-debugger-dev.png)

1. Inicie sesión en el sitio de Luma con las credenciales `test@adobe.com`/`test`

1. Vuelva a la [página principal de Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

1. En las señalizaciones de red del SDK web de Platform que muestra Debugger, seleccione la fila &quot;events&quot; para expandir los detalles en una ventana emergente

   ![SDK web en Debugger](assets/experience-platform-debugger-dev-eventType.png)

1. Busque el &quot;identityMap&quot; en la ventana emergente. Aquí debe ver lumaCrmId con tres claves authenticationState, id y primary
   ![SDK web en Debugger](assets/experience-platform-debugger-dev-idMap.png)

Ahora, los datos deben rellenarse en `Luma Web Event Data` conjunto de datos y listo para la validación &#39;Previsualizar conjunto de datos&#39;.

### Previsualización del conjunto de datos

Para confirmar que los datos han aterrizado en el lago de datos de Platform, una opción rápida es utilizar **[!UICONTROL Previsualizar conjunto de datos]** función. Los datos del SDK web se envían en microlotes al lago de datos y se actualizan en la interfaz de Platform periódicamente. Los datos generados pueden tardar entre 10 y 15 minutos en mostrarse.

1. En el [Experience Platform](https://experience.adobe.com/platform/) interfaz, seleccione **[!UICONTROL Administración de datos > Conjuntos de datos]** en el panel de navegación izquierdo para abrir **[!UICONTROL Conjuntos de datos]** panel.

   El panel enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere el conjunto de datos y el estado de la ejecución de ingesta más reciente.

1. Seleccione su `Luma Web Event Data` conjunto de datos para abrir **[!UICONTROL Actividad de conjunto de datos]** pantalla.

   ![Evento web de conjunto de datos Luma](assets/experience-platform-dataset-validation-lumaSDK.png)

   La pantalla de actividad incluye un gráfico que visualiza la tasa de mensajes que se consumen, así como una lista de lotes correctos y fallidos.

1. Desde el **[!UICONTROL Actividad de conjunto de datos]** pantalla, seleccione **[!UICONTROL Previsualizar conjunto de datos]** cerca de la esquina superior derecha de la pantalla para obtener una vista previa de hasta 100 filas de datos. Si el conjunto de datos está vacío, se desactiva el vínculo de vista previa.

   ![Previsualización de conjunto de datos](assets/experience-platform-dataset-preview.png)

   En la ventana de vista previa, la vista jerárquica del esquema para el conjunto de datos se muestra a la derecha.

   ![Vista previa de conjunto de datos 1](assets/experience-platform-dataset-preview-1.png)


### Consulta de los datos

1. En el [Experience Platform](https://experience.adobe.com/platform/) interfaz, seleccione **[!UICONTROL Administración de datos > Consultas]** en el panel de navegación izquierdo para abrir **[!UICONTROL Consultas]** pantalla.
1. Seleccionar **[!UICONTROL Crear consulta]**
1. En primer lugar, ejecute una consulta para ver todos los nombres de las tablas del lago de datos. Entrar `SHOW TABLES` en el editor de consultas y haga clic en el icono reproducir para ejecutar la consulta.
1. En los resultados, observe cómo el nombre de la tabla es similar a `luma_web_event_data`
1. Ahora consulte la tabla con una consulta simple que haga referencia a la tabla (tenga en cuenta que, de forma predeterminada, la consulta estará limitada a 100 resultados): `SELECT * FROM "luma_web_event_data"`
1. Después de unos momentos, debería ver registros de muestra de sus datos web.

>[!ERROR]
>
>Si aparece el error &quot;Tabla no aprovisionada&quot;, vuelva a comprobar el nombre de la tabla. También podría ser que el microlote de datos aún no haya aterrizado en el lago de datos. Vuelva a intentarlo en 10-15 minutos.

>[!INFO]
>
>  Para obtener más información sobre el servicio de consultas de Adobe Experience Platform, consulte [Exploración de datos](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/queries/explore-data) en la sección Tutoriales de Platform.


## Habilitar el conjunto de datos y el esquema para el perfil del cliente en tiempo real

Para los clientes de Real-time Customer Data Platform y Journey Optimizer, el siguiente paso es habilitar el conjunto de datos y el esquema para el perfil del cliente en tiempo real. La transmisión de datos desde el SDK web será una de las muchas fuentes de datos que fluirán a Platform y desea unir los datos web con otras fuentes de datos para crear perfiles de clientes de 360 grados. Para obtener más información sobre el Perfil del cliente en tiempo real, vea este breve vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&captions=eng)

>[!CAUTION]
>
>Al trabajar con su propio sitio web y datos de, recomendamos una validación de datos más sólida antes de habilitarla para el perfil del cliente en tiempo real.


**Para habilitar el conjunto de datos:**

1. Abra el conjunto de datos que ha creado, `Luma Web Event Data`

1. Seleccione el **[!UICONTROL Alternancia de perfil]** para activarlo.

   ![Alternancia de perfil](assets/setup-experience-platform-profile.png)

1. Confirme que desea **[!UICONTROL Activar]** el conjunto de datos

   ![Alternancia de habilitación de perfil](assets/setup-experience-platform-profile-enable.png)

**Para habilitar el esquema:**

1. Abra el esquema que ha creado, `Luma Web Event Data`

1. Seleccione el **[!UICONTROL Alternancia de perfil]** para activarlo.

   ![Alternancia de perfil](assets/setup-experience-platform-profile-schema.png)

1. Seleccionar **[!UICONTROL Los datos de este esquema contienen una identidad principal en el campo identityMap.]**

   >[!IMPORTANT]
   >
   >    Las identidades principales son necesarias en cada registro enviado al Perfil del cliente en tiempo real. Normalmente, los campos de identidad se etiquetan dentro del esquema. Sin embargo, al utilizar mapas de identidad, los campos de identidad no son visibles dentro del esquema. Este cuadro de diálogo sirve para confirmar que tiene en mente una identidad principal y que la especificará en un mapa de identidad al enviar los datos. Como ya sabe, el SDK web utiliza un mapa de identidad con el ID de Experience Cloud (ECID) como identidad principal predeterminada y un ID autenticado como identidad principal cuando está disponible.


1. Seleccionar **[!UICONTROL Activar]**

   ![Alternancia de habilitación de perfil](assets/setup-experience-platform-profile-schema-enable.png)

1. Seleccionar **[!UICONTROL Guardar]** para guardar el esquema actualizado

Ahora el esquema también está habilitado para el perfil.

>[!IMPORTANT]
>
>    Una vez que un esquema está habilitado para el perfil, no se puede deshabilitar ni eliminar sin restablecer o eliminar toda la zona protegida. Además, los campos no se pueden eliminar del esquema después de este punto.
>
>   
> Al trabajar con sus propios datos, le recomendamos que haga las cosas en el siguiente orden:
> 
> * En primer lugar, introduzca algunos datos en los conjuntos de datos.
> * Solucionar cualquier problema que surja durante el proceso de ingesta de datos (por ejemplo, problemas de validación o asignación de datos).
> * Habilitar los conjuntos de datos y esquemas para el perfil
> * Vuelva a ingerir los datos si es necesario


### Validación de un perfil

Puede buscar un perfil de cliente en la interfaz de Platform (o de Journey Optimizer) para confirmar que los datos han llegado al Perfil del cliente en tiempo real. Como su nombre sugiere, los perfiles se rellenan en tiempo real, por lo que no hay retraso como con la validación de datos en el conjunto de datos.

Primero debe generar más datos de ejemplo. Repita los pasos anteriores de esta lección para iniciar sesión en el sitio web de Luma cuando esté asignado a la propiedad de etiquetas. Inspect utiliza la solicitud del SDK web de Platform para asegurarse de que envía datos con la variable `lumaCRMId`.

1. En el [Experience Platform](https://experience.adobe.com/platform/) interfaz, seleccione **[!UICONTROL Cliente]** > **[!UICONTROL Perfiles]** en el panel de navegación izquierdo

1. Como el **[!UICONTROL Área de nombres de identidad]** use `lumaCRMId`
1. Copie y pegue el valor de `lumaCRMId` pasó la llamada que inspeccionó en Experience Platform Debugger, en este caso `112ca06ed53d3db37e4cea49cc45b71e`.

   ![Perfil](assets/experience-platform-validate-dataset-profile.png)

1. Si hay un valor válido en el perfil para `lumaCRMId`, un ID de perfil se rellena en la consola:

   ![Perfil](assets/experience-platform-validate-dataset-profile-set.png)

1. Para ver la información completa **[!UICONTROL Perfil del cliente]** para cada ID, seleccione la **[!UICONTROL ID de perfil]** en la ventana principal.

   >[!NOTE]
   >
   >Nota: puede seleccionar el hipervínculo del ID de perfil o, si selecciona la fila, se abrirá un menú de la derecha en el que podrá seleccionar el hipervínculo ID de perfil
   > ![Perfil del cliente](assets/experience-platform-select-profileId.png)

   Aquí puede ver todas las identidades vinculadas a `lumaCRMId`, como el `ECID`.

   ![Perfil del cliente](assets/experience-platform-validate-dataset-custProfile.png)

Ahora ha habilitado el SDK web de Platform para Experience Platform (y Real-Time CDP! ¡Y Journey Optimizer! ¡Y Customer Journey Analytics!).

### Crear un esquema de fidelización e introducir datos de ejemplo

Se espera que los clientes de Real-time Customer Data Platform y Journey Optimizer completen este ejercicio.

Cuando los datos del SDK web se incorporan en Adobe Experience Platform, se pueden ampliar con otras fuentes de datos que haya introducido en Platform. Por ejemplo, cuando un usuario inicia sesión en el sitio de Luma, se construye un gráfico de identidades en Experience Platform y todos los demás conjuntos de datos con perfil habilitado pueden unirse para crear perfiles de cliente en tiempo real. Para ver esto en acción, cree rápidamente otro conjunto de datos en Adobe Experience Platform con algunos datos de fidelidad de ejemplo para poder utilizar Perfiles del cliente en tiempo real con Real-time Customer Data Platform y Journey Optimizer. Dado que ya ha realizado ejercicios similares, las instrucciones serán breves.

Cree el esquema de fidelización:

1. Creación de un nuevo esquema
1. Elegir **[!UICONTROL Perfil individual]** como el [!UICONTROL clase base]
1. Asignar un nombre al esquema `Luma Loyalty Schema`
1. Añada el [!UICONTROL Detalles de fidelización] grupo de campos
1. Añada el [!UICONTROL Datos demográficos] grupo de campos
1. Seleccione el `Person ID` y marcarlo como un campo [!UICONTROL Identidad] y [!UICONTROL Identidad principal] uso del `Luma CRM Id` [!UICONTROL Área de nombres de identidad].
1. Habilitar el esquema para [!UICONTROL Perfil]. Si no encuentra la opción Perfil, intente hacer clic en el nombre del esquema en la parte superior izquierda.
1. Guardar el esquema

   ![Esquema de fidelización](assets/web-channel-loyalty-schema.png)

Para crear el conjunto de datos e introducir los datos de ejemplo:

1. Cree un nuevo conjunto de datos a partir de `Luma Loyalty Schema`
1. Asignar un nombre al conjunto de datos `Luma Loyalty Dataset`
1. Habilitar el conjunto de datos para [!UICONTROL Perfil]
1. Descargar el archivo de muestra [luma-loyalty-forWeb.json](assets/luma-loyalty-forWeb.json)
1. Arrastre y suelte el archivo en el conjunto de datos
1. Confirme que los datos se han introducido correctamente.

   ![Esquema de fidelización](assets/web-channel-loyalty-dataset.png)

### Crear un público

Las audiencias agrupan perfiles en torno a rasgos comunes. Cree una audiencia rápida que pueda utilizar en su campaña web:

1. En la interfaz de Experience Platform o Journey Optimizer, vaya a **[!UICONTROL Cliente]** > **[!UICONTROL Audiencias]** en el panel de navegación izquierdo
1. Seleccionar **[!UICONTROL Crear audiencia]**
1. Seleccionar **[!UICONTROL Generar regla]**
1. Seleccionar **[!UICONTROL Crear]**

   ![Crear un público](assets/web-campaign-create-audience.png)

1. Seleccionar **[!UICONTROL Atributos]**
1. Busque el **[!UICONTROL Lealtad]** > **[!UICONTROL Nivel]** y arrástrelo al campo **[!UICONTROL Atributos]** sección
1. Defina la audiencia como usuarios cuyos `tier` es `gold`
1. Nombrar la audiencia `Luma Loyalty Rewards – Gold Status`
1. Seleccionar **[!UICONTROL Edge]** como el **[!UICONTROL Método de evaluación]**
1. Seleccionar **[!UICONTROL Guardar]**

   ![Definición de la audiencia](assets/web-campaign-define-audience.png)

Como se trata de una audiencia muy sencilla, podemos utilizar el método de evaluación de Edge. Las audiencias de Edge se evalúan en Edge, por lo que en la misma solicitud realizada por el SDK web al Edge Network de Platform, podemos evaluar la definición de la audiencia y confirmar inmediatamente si el usuario cumple los requisitos.


[Siguiente: ](setup-analytics.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
