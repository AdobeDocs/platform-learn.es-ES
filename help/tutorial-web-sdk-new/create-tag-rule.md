---
title: Creación de una regla de etiqueta
description: Obtenga información sobre cómo enviar un evento a la red perimetral de Platform con el objeto XDM mediante una regla de etiqueta. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---

# Creación de una regla de etiqueta

Obtenga información sobre cómo enviar un evento a la red perimetral de Platform con el objeto XDM mediante una regla de etiqueta. Una regla de etiqueta es una combinación de eventos, condiciones y acciones que indica a la propiedad de etiqueta que haga algo.

>[!NOTE]
>
> Para fines de demostración, los ejercicios de esta lección se basan en el ejemplo utilizado durante la [Creación de identidades](create-identities.md) paso; envío de una acción de evento de XDM para capturar contenido e identidades de usuarios en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Utilice una convención de nombres para administrar reglas dentro de las etiquetas
* Envío de un evento XDM mediante los tipos de acción Actualizar variable y Enviar evento en una regla de etiqueta
* Publicación de una regla de etiqueta en una biblioteca de desarrollo


## Requisitos previos

Está familiarizado con las etiquetas de recopilación de datos y las [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html)y debe haber completado las siguientes lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)
* [Creación de identidades](create-identities.md)

## Convenciones de nomenclatura

Para administrar mejor las reglas en las etiquetas, se recomienda seguir una convención de nombres estándar. Este tutorial utiliza una convención de nombres de tres partes:

* [**ubicación**] - [**evento**] - [**herramienta**] (**Secuencia**)

donde;

1. **ubicación** es la página o páginas del sitio donde se activa la regla
1. **evento** es el déclencheur de la regla
1. **herramienta** es la aplicación o aplicaciones específicas utilizadas en el paso de acción para esa regla
1. **Secuencia** es el orden en que la regla debe activarse en relación con otras reglas
<!-- minor update -->

## Crear regla de etiqueta

En las etiquetas, las reglas se utilizan para ejecutar acciones (llamadas de activación) bajo varias condiciones. La extensión de etiquetas del SDK web de Platform incluye dos acciones que se utilizarán en esta lección:

* **[!UICONTROL Actualizar variable]** asigna elementos de datos a campos XDM
* **[!UICONTROL Enviar evento]** envía el objeto XDM a Experience Platform Edge Network

### Actualizar variable

Cree esta primera regla como una &quot;configuración global&quot; para establecer todas las variables de contenido esenciales en el objeto XDM mediante los SDK web de Platform **[!UICONTROL Actualizar variable]** acción. A continuación, cree una segunda regla, secuenciada en déclencheur después de la primera, para enviar el objeto XDM a Platform Edge Network mediante **[!UICONTROL Enviar evento]** acción. Más adelante en este tutorial, enviará diferentes campos XDM en función del tipo de página en la que se encuentra el visitante (por ejemplo, SKU de productos en páginas de productos). Para ello, secuencie las reglas que contienen **[!UICONTROL Actualizar variable]** acciones antes de la regla que utiliza la variable **[!UICONTROL Enviar evento]** acción.

Para crear una regla de etiqueta:

1. Abra la propiedad de etiqueta que está utilizando para este tutorial.

1. Ir a **[!UICONTROL Reglas]** en el panel de navegación izquierdo

1. Seleccione el **[!UICONTROL Crear nueva regla]** botón

   ![Creación de una regla](assets/rules-create.png)

1. Asigne un nombre a la regla `all pages global content variables - page bottom - AA (order 1)`.

1. En el **[!UICONTROL Eventos]** , seleccione **[!UICONTROL Añadir]**

   ![Asignar un nombre a la regla y añadir un evento](assets/rule-name-new.png)

1. Utilice el **[!UICONTROL Extensión principal]** y seleccione `Page Bottom` como el **[!UICONTROL Tipo de evento]**

1. En el **[!UICONTROL Nombre]** , asígnele un nombre `Core - Page Bottom - order 1`. Esto le ayuda a describir el déclencheur con un nombre significativo.

1. Seleccionar **[!UICONTROL Avanzadas]** desplegable e introduzca `1` in **[!UICONTROL Pedido]**

   >[!NOTE]
   >
   > Cuanto mayor sea el número introducido, más adelante en el orden general de las operaciones que déclencheur.

1. Seleccionar **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal
   ![Seleccionar Déclencheur inferior de la página](assets/create-tag-rule-trigger-bottom.png)

1. En el **[!UICONTROL Acciones]** , seleccione **[!UICONTROL Añadir]**

1. Como el **[!UICONTROL Extensión]**, seleccione **[!UICONTROL SDK web de Adobe Experience Platform]**

1. Como el **[!UICONTROL Tipo de acción]**, seleccione **[!UICONTROL Actualizar variable]**

1. Como el **[!UICONTROL Elemento de datos]**, seleccione la `xdm.variable.content` que creó en la [Creación de elementos de datos](create-data-elements.md) lección

   ![Actualizar esquema de variables](assets/create-rule-update-variable.png)

Ahora, asigne los [!UICONTROL elementos de datos] a la [!UICONTROL esquema] utilizado por el objeto XDM.

>[!NOTE]
> 
> Puede asignar a propiedades individuales u objetos completos. En este ejemplo, se asigna a propiedades individuales.


1. Desplácese hacia abajo hasta que llegue al **`web`** objeto

1. Seleccione para abrirlo

1. Asigne los siguientes elementos de datos al correspondiente `web` Variables XDM

   * **`web.webPageDetials.name`** hasta `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** hasta `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** hasta `%page.pageInfo.hierarchie1%`

   ![Actualización del contenido de variables](assets/create-rule-xdm-variable-content.png)

1. A continuación, busque la `identityMap` en el esquema y selecciónelo

1. Mapa a `identityMap.loginID` elemento de datos

   ![Actualizar mapa de identidad variable](assets/create-rule-variable-identityMap.png)

1. A continuación, busque el campo eventType y selecciónelo

1. Introduzca el valor `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > Este menú desplegable rellena el **`xdm.eventType`** en el objeto XDM. Aunque también puede escribir etiquetas de forma libre en este campo, es muy recomendable que **no** ya que tiene efectos adversos con Platform.

   >[!TIP]
   >
   > Para comprender qué valores se rellenan en `eventType` , debe ir a la página de esquema y seleccionar el campo `eventType` para ver los valores sugeridos en el carril derecho.

   ![Actualizar mapa de identidad variable](assets/create-tag-rule-eventType.png)


1. Seleccionar **[!UICONTROL Conservar cambios]** y luego **[!UICONTROL Guardar]** la regla de la siguiente pantalla para terminar de crearla

### Enviar evento

Ahora que ha establecido las variables, puede crear la segunda regla para enviar el objeto XDM a Platform Edge Network con la variable **[!UICONTROL Enviar evento]** tipo de acción.

1. A la derecha, seleccione para **[!UICONTROL Agregar regla]** para crear otra regla

1. Asigne un nombre a la regla `all pages send event - page bottom - AA (order 50)`.

1. En el **[!UICONTROL Eventos]** , seleccione **[!UICONTROL Añadir]**

1. Utilice el **[!UICONTROL Extensión principal]** y seleccione `Page Bottom` como el **[!UICONTROL Tipo de evento]**

1. En el **[!UICONTROL Nombre]** , asígnele un nombre `Core - Page Bottom - order 50`. Esto le ayuda a describir el déclencheur con un nombre significativo.

1. Seleccionar **[!UICONTROL Avanzadas]** desplegable e introduzca `50` in **[!UICONTROL Pedido]**. Esto garantizará que el segundo déclencheur de regla sea posterior al primero que configure como déclencheur `1`.

1. Seleccionar **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal
   ![Seleccionar Déclencheur inferior de la página](assets/create-tag-rule-trigger-bottom-send.png)

1. En el **[!UICONTROL Acciones]** , seleccione **[!UICONTROL Añadir]**

1. Como el **[!UICONTROL Extensión]**, seleccione  **[!UICONTROL SDK web de Adobe Experience Platform]**

1. Como el  **[!UICONTROL Tipo de acción]**, seleccione  **[!UICONTROL Enviar evento]**

1. Como el **[!UICONTROL XDM]**, seleccione la `xdm.variable.content` elemento de datos creado en la lección anterior

1. Seleccionar **[!UICONTROL Conservar cambios]** para volver a la pantalla de regla principal

   ![Añadir la acción Enviar evento](assets/create-rule-send-event-action.png)
1. Seleccionar **[!UICONTROL Guardar]** para guardar la regla

   ![Guarde la regla](assets/create-rule-save-rule.png)

## Publicación de la regla en una biblioteca

A continuación, publique la regla en el entorno de desarrollo para poder verificar si funciona.

Para crear una biblioteca:

1. Ir a **[!UICONTROL Flujo de publicación]** en el panel de navegación izquierdo

1. Seleccionar **[!UICONTROL Añadir biblioteca]**

   ![Seleccione Añadir biblioteca.](assets/rule-publish-library.png)
1. Para el **[!UICONTROL Nombre]**, introduzca `Luma Web SDK Tutorial`
1. Para el **[!UICONTROL Entorno]**, seleccione `Development`
1. Seleccionar  **[!UICONTROL Añadir todos los recursos modificados]**

   >[!NOTE]
   >
   >    Además de la extensión SDK para web de Adobe Experience Platform y la `all pages global content variables - page bottom - AA (order 50)` , verá los componentes de etiquetas creados en lecciones anteriores. La extensión Core contiene el JavaScript base requerido por todas las propiedades de etiquetas web.

1. Seleccionar **[!UICONTROL Guardar y generar para desarrollo]**

   ![Crear y crear la biblioteca](assets/create-tag-rule-library-changes.png)

La biblioteca puede tardar unos minutos en crearse y, cuando se completa, muestra un punto verde a la izquierda del nombre de la biblioteca:

![Compilación completa](assets/create-rule-development-success.png)

Como puede ver en el [!UICONTROL Flujo de publicación] En la pantalla de, hay mucho más en el proceso de publicación que está fuera del ámbito de este tutorial. Este tutorial solo utiliza una biblioteca en el entorno de desarrollo.

Ahora está listo para validar los datos en la solicitud utilizando el Adobe Experience Platform Debugger.

[Siguiente ](validate-with-debugger.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
