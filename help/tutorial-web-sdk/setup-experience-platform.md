---
title: Transmisión de datos a Adobe Experience Platform con SDK web
description: Obtenga información sobre cómo transmitir datos web a Adobe Experience Platform con el SDK web. Esta lección forma parte del tutorial Implementar Adobe Experience Cloud con SDK web .
exl-id: 4d749ffa-e1c0-4498-9b12-12949807b369
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 5%

---

# Transmitir datos al Experience Platform con el SDK web

Obtenga información sobre cómo transmitir datos web a Adobe Experience Platform con el SDK web de Platform.

Experience Platform es la columna vertebral de todas las aplicaciones de Experience Cloud nuevas, como Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics y Adobe Journey Optimizer. Estas aplicaciones están diseñadas para utilizar el SDK web de Platform como su método óptimo de recopilación de datos web.

El Experience Platform utiliza el mismo esquema XDM que creó anteriormente para capturar datos de evento del sitio web de Luma. Cuando esos datos se envían a Platform Edge Network, la configuración del conjunto de datos puede reenviarlos al Experience Platform.

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Crear un conjunto de datos en Adobe Experience Platform
* Configuración del conjunto de datos para enviar datos del SDK web a Adobe Experience Platform
* Habilitar la transmisión de datos web para el perfil del cliente en tiempo real
* Valide que los datos han llegado tanto en el conjunto de datos de Platform como en el perfil del cliente en tiempo real

## Requisitos previos

Ya debería haber completado las siguientes lecciones:

* La variable **Configuración inicial** lecciones:
   * [Configure los permisos](configure-permissions.md)
   * [Configuración de un esquema XDM](configure-schemas.md)
   * [Configurar un conjunto de datos](configure-datastream.md)
   * [Configuración de un área de nombres de identidad](configure-identities.md)

* La variable **Configuración de etiquetas** lecciones:
   * [Instalación de la extensión del SDK web](install-web-sdk.md)
   * [Creación de elementos de datos](create-data-elements.md)
   * [Crear reglas de etiqueta](create-tag-rule.md)


## Crear un conjunto de datos

Todos los datos que se incorporan correctamente en Adobe Experience Platform se conservan dentro del lago de datos como conjuntos de datos. A [conjunto de datos](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=en) es una construcción de almacenamiento y administración para una recopilación de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

En este ejercicio, se crea un conjunto de datos para realizar un seguimiento del contenido y los detalles de comercio electrónico para la variable [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!WARNING]
>
>Ya debe haber creado el `Luma Web Event Data` esquema, tal como se indica en la lección anterior, [Configuración de un esquema XDM](configure-schemas.md).


1. Vaya a la [interfaz del Experience Platform](https://experience.adobe.com/platform/)
1. Confirme que se encuentra en el simulador de pruebas de desarrollo que está utilizando para este tutorial.
1. Apertura **[!UICONTROL Conjuntos de datos]** desde la navegación izquierda
1. Select **[!UICONTROL Crear conjunto de datos]**

   ![Crear esquema](assets/experience-platform-create-dataset.png)

1. Seleccione el **[!UICONTROL Crear conjunto de datos a partir del esquema]** option

   ![Crear conjunto de datos a partir del esquema](assets/experience-platform-create-dataset-schema.png)

1. Seleccione el `Luma Web Event Data` esquema creado en [lección anterior](configure-schemas.md) y, a continuación, seleccione **[!UICONTROL Siguiente]**

   ![Conjunto de datos, seleccionar esquema](assets/experience-platform-create-dataset-schema-selection.png)

1. Proporcione un **[!UICONTROL Nombre]** y opcional **[!UICONTROL Descripción]** para el conjunto de datos. Para este ejercicio, utilice `Luma Web Event Data`y, a continuación, seleccione **[!UICONTROL Finalizar]**

   ![Nombre del conjunto de datos ](assets/experience-platform-create-dataset-schema-name.png)

Ahora hay un conjunto de datos configurado para empezar a recopilar datos de su implementación del SDK web de Platform.

## Configuración del conjunto de datos

Ahora puede configurar su [!UICONTROL datastream] para enviar datos a [!UICONTROL Adobe Experience Platform]. El conjunto de datos es el vínculo entre la propiedad tag, la red perimetral de plataforma y el conjunto de datos del Experience Platform.

1. Abra el [Recopilación de datos](https://experience.adobe.com/#/data-collection)Interfaz de {target=&quot;blank&quot;}
1. Select **[!UICONTROL Datastreams]** desde la navegación izquierda
1. Abra el conjunto de datos creado en la [Configurar un conjunto de datos](configure-datastream.md) lección, `Luma Web SDK`

   ![Seleccione el conjunto de datos del SDK web de Luma](assets/datastream-luma-web-sdk.png)

1. Select **[!UICONTROL Añadir servicio]**

   ![Añadir un servicio al conjunto de datos](assets/experience-platform-addService.png)
1. Select **[!UICONTROL Adobe Experience Platform]** como el **[!UICONTROL Servicio]**
1. Select `Luma Web Event Data` como el **[!UICONTROL Conjunto de datos del evento]**

1. Seleccione **[!UICONTROL Guardar]**.

   ![Configuración del almacén de datos](assets/experience-platform-datastream-config.png)

A medida que genera tráfico en [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html) asignados a la propiedad tag, los datos rellenarán el conjunto de datos en Experience Platform.

## Validar el conjunto de datos

Este paso es crítico para asegurarse de que los datos han llegado al conjunto de datos. Existen dos aspectos para validar los datos enviados al conjunto de datos.

* Validar mediante [!UICONTROL Experience Platform Debugger]
* Validar mediante [!UICONTROL Vista previa del conjunto de datos]
* Validar mediante [!UICONTROL Servicio de consultas]

### Experience Platform Debugger

Estos pasos son más o menos iguales a lo que hizo en la [Lección de Debugger](validate-with-debugger.md). Sin embargo, como los datos solo se enviarán a Platform después de haberlos activado en el conjunto de datos, debe generar más datos de ejemplo:

1. Abra el [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) y seleccione [!UICONTROL Experience Platform Debugger] icono de extensión

1. Configure Debugger para asignar la propiedad de etiqueta a *your* Entorno de desarrollo, tal como se describe en la sección [Validación con Debugger](validate-with-debugger.md) lección

   ![El entorno de desarrollo de Launch que se muestra en Debugger](assets/experience-platform-debugger-dev.png)

1. Inicie sesión en el sitio de Luma con las credenciales `test@adobe.com`/`test`

1. Vuelva a la [página principal de Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Dentro de las señalizaciones de red de Platform Web SDK que muestra el depurador, seleccione la fila &quot;eventos&quot; para expandir los detalles en una ventana emergente

   ![SDK web en Debugger](assets/experience-platform-debugger-dev-eventType.png)

1. Busque el &quot;mapa de identidad&quot; en la ventana emergente. Aquí debería ver lumaCrmId con tres claves de authenticationState, id y primary
   ![SDK web en Debugger](assets/experience-platform-debugger-dev-idMap.png)

Ahora los datos deben rellenarse en la variable `Luma Web Event Data` conjunto de datos y listo para la validación &quot;Vista previa del conjunto de datos&quot;.

### Vista previa del conjunto de datos

Para confirmar que los datos han llegado al lago de datos de Platform, una opción rápida es usar la variable **[!UICONTROL Vista previa del conjunto de datos]** función. Los datos del SDK web se envían por lotes al lago de datos y se actualizan periódicamente en la interfaz de Platform. Los datos que ha generado pueden tardar entre 10 y 15 minutos.

1. En el [Experience Platform](https://experience.adobe.com/platform/) interfaz, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo para abrir el **[!UICONTROL Conjuntos de datos]** tablero.

   El tablero enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere el conjunto de datos y el estado de la ejecución de ingesta más reciente.

1. Seleccione su `Luma Web Event Data` conjunto de datos para abrir su **[!UICONTROL Actividad del conjunto de datos]** en el Navegador.

   ![Evento web de Luma de conjunto de datos](assets/experience-platform-dataset-validation-lumaSDK.png)

   La pantalla de actividad incluye un gráfico que visualiza la tasa de mensajes que se consumen, así como una lista de lotes correctos y fallidos.

1. En el **[!UICONTROL Actividad del conjunto de datos]** pantalla, seleccionar **[!UICONTROL Vista previa del conjunto de datos]** cerca de la esquina superior derecha de la pantalla para obtener una vista previa de hasta 100 filas de datos. Si el conjunto de datos está vacío, el vínculo de vista previa se desactiva.

   ![Vista previa del conjunto de datos](assets/experience-platform-dataset-preview.png)

   En la ventana de vista previa, la vista jerárquica del esquema para el conjunto de datos se muestra a la derecha.

   ![Vista previa de conjunto de datos 1](assets/experience-platform-dataset-preview-1.png)

>[!INFO]
>
>El servicio de consulta de Adobe Experience Platform es un método más robusto para validar los datos en el lago, pero está fuera del alcance de este tutorial. Para obtener más información, consulte [Explorar datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=es) en la sección Tutoriales de Platform .


## Habilitar el conjunto de datos y el esquema para el perfil de cliente en tiempo real

El siguiente paso es habilitar el conjunto de datos y el esquema para el perfil del cliente en tiempo real. La transmisión de datos desde el SDK web será una de las muchas fuentes de datos que ingresan a Platform y desea unir sus datos web con otras fuentes de datos para crear perfiles de clientes de 360 grados. Para obtener más información sobre el Perfil del cliente en tiempo real, vea este breve vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&learn=on&captions=eng)

>[!CAUTION]
>
>Al trabajar con su propio sitio web y sus datos, le recomendamos que realice una validación de los datos más sólida antes de habilitarlos para el perfil del cliente en tiempo real.


**Para habilitar el conjunto de datos:**

1. Abra el conjunto de datos que ha creado, `Luma Web Event Data`

1. Seleccione el **[!UICONTROL Alternar perfil]** para activarlo

   ![Alternar perfil](assets/setup-experience-platform-profile.png)

1. Confirme que desea **[!UICONTROL Habilitar]** el conjunto de datos

   ![Alternar activación de perfil](assets/setup-experience-platform-profile-enable.png)

**Para habilitar el esquema:**

1. Abra el esquema que ha creado, `Luma Web Event Data`

1. Seleccione el **[!UICONTROL Alternar perfil]** para activarlo

   ![Alternar perfil](assets/setup-experience-platform-profile-schema.png)

1. Select **[!UICONTROL Los datos de este esquema contendrán una identidad principal en el campo identityMap .]**

   >[!IMPORTANT]
   >
   >    Las identidades principales se requieren en cada registro enviado al Perfil del cliente en tiempo real. Normalmente, los campos de identidad se etiquetan dentro del esquema. Sin embargo, al utilizar mapas de identidad, los campos de identidad no son visibles dentro del esquema. Este cuadro de diálogo sirve para confirmar que tiene en mente una identidad principal y que la especificará en un mapa de identidad al enviar los datos. Como sabe, el SDK web utiliza un mapa de identidad y el ID de Experience Cloud (ECID) es la identidad principal predeterminada.


1. Select **[!UICONTROL Habilitar]**

   ![Alternar activación de perfil](assets/setup-experience-platform-profile-schema-enable.png)

1. Select **[!UICONTROL Guardar]** para guardar el esquema actualizado

Ahora el esquema también está habilitado para perfil.

>[!IMPORTANT]
>
>    Una vez que un esquema está habilitado para Perfil, no se puede deshabilitar ni eliminar. Además, los campos no se pueden eliminar del esquema después de este punto. Estas implicaciones son importantes de tener en cuenta más adelante cuando trabaje con sus propios datos en su entorno de producción. Debe utilizar un simulador para pruebas de desarrollo en este tutorial, que se puede eliminar en cualquier momento.
>
>   
> Al trabajar con sus propios datos, le recomendamos que haga las cosas en el siguiente orden:
> 
> * En primer lugar, incorpore algunos datos en sus conjuntos de datos.
> * Solucione cualquier problema que surja durante el proceso de consumo de datos (por ejemplo, problemas de validación o asignación de datos).
> * Habilitar los conjuntos de datos y esquemas para el perfil
> * Volver a introducir los datos



### Validación de un perfil

Puede buscar un perfil de cliente en la interfaz de Platform (o interfaz de Journey Optimizer) para confirmar que los datos han llegado al Perfil del cliente en tiempo real. Como el nombre sugiere, los perfiles se rellenan en tiempo real, por lo que no hay retraso como lo había con la validación de datos en el conjunto de datos.

Primero debe generar más datos de muestra. Repita los pasos anteriores en esta lección para iniciar sesión en el sitio web de Luma cuando esté asignado a la propiedad de la etiqueta. Inspect solicita al SDK web de Platform que se asegure de que envía datos con la variable `lumaCRMId`.

1. En el [Experience Platform](https://experience.adobe.com/platform/) interfaz, seleccione **[!UICONTROL Perfiles]** en la navegación izquierda

1. Como **[!UICONTROL Área de nombres de identidad]** use `lumaCRMId`
1. Copie y pegue el valor de la variable `lumaCRMId` pasó la llamada que inspeccionó en Experience Platform Debugger (probablemente `112ca06ed53d3db37e4cea49cc45b71e`).

   ![Perfil](assets/experience-platform-validate-dataset-profile.png)

1. Si hay un valor válido en el Perfil para `lumaCRMId`, un ID de perfil se rellena en la consola:

   ![Perfil](assets/experience-platform-validate-dataset-profile-set.png)

1. Haga clic en [!UICONTROL ID de perfil] y [!UICONTROL Perfil del cliente] La consola se rellena. Aquí puede ver todas las identidades vinculadas al `lumaCRMId`, como el `ECID`:

   ![Perfil del cliente](assets/experience-platform-validate-dataset-custProfile.png)

Ya ha habilitado Platform Web SDK para Experience Platform (y Real-Time CDP! ¡Y Customer Journey Analytics! ¡Y Journey Optimizer!)


[Siguiente: ](setup-analytics.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK web de Adobe Experience Platform. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)