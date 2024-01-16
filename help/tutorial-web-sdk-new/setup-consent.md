---
title: Configuración del consentimiento con el SDK web de Platform
description: Obtenga información sobre cómo establecer la configuración de privacidad de la extensión de etiquetas de SDK web de Experience Platform. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Tags,Consent
source-git-commit: 695c12ab66df33af00baacabc3b69eaac7ada231
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 0%

---

# Configuración del consentimiento con el SDK web de Platform

Obtenga información sobre cómo establecer la configuración de privacidad de la extensión de etiquetas de SDK web de Experience Platform. Establezca el consentimiento en función de la interacción del visitante con un titular de una plataforma de administración de consentimiento (CMP).

>[!NOTE]
> 
>Para fines de demostración, este tutorial utiliza [Klaro](https://heyklaro.com/) como CMP. Puede seguir a través de Klaro o el CMP que use con su sitio web.


## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Carga de una CMP mediante etiquetas
* Configuración de privacidad en la extensión de etiquetas del SDK web de Experience Platform
* Establezca el consentimiento para el SDK web de Experience Platform en función de la acción del visitante

## Requisitos previos

Debe estar familiarizado con las etiquetas y los pasos para crear reglas, elementos de datos, crear bibliotecas en entornos y cambiar de bibliotecas de etiquetas con Experience Platform Debugger.

Antes de empezar a configurar la configuración de privacidad y a crear las reglas para configurar el consentimiento, asegúrese de haber insertado el script de la plataforma de administración de consentimiento en el sitio web y de que funcione correctamente. Una CMP se puede cargar directamente en el código fuente con la ayuda de los desarrolladores del sitio o cargarse a través de las etiquetas. Esta lección demuestra este último enfoque.
>[!NOTE]
> 
>1. Las organizaciones utilizan una plataforma de administración de consentimiento (o CMP) para documentar y administrar legalmente las opciones de consentimiento de un visitante antes de recopilar, compartir o vender datos de visitantes de fuentes en línea como sitios web y aplicaciones.
>
>2. El método recomendado para insertar una CMP es directamente a través del código fuente antes del script del administrador de etiquetas.

### Configuración de Klaro

Antes de ir a las configuraciones de etiquetas, obtenga más información acerca de la plataforma de administración de consentimiento utilizada en este tutorial de Klaro.

1. Visita [Klaro](https://heyklaro.com/) y configure una cuenta.
1. Ir a **Administrador de privacidad** y cree una instancia de acuerdo con las instrucciones.
1. Utilice el **Código de integración** para inyectar Klaro en su propiedad de etiquetas (las instrucciones se encuentran en el siguiente ejercicio).
1. Omita el **Digitalización** , ya que detectará la propiedad de etiqueta que está codificada en el sitio web de demostración de Luma y no la que ha creado para este tutorial.
1. Añada un servicio llamado `aep web sdk` y active la opción **Estado predeterminado del servicio**. Cuando está activado, el valor de consentimiento predeterminado es `true`, de lo contrario `false`. Esta configuración es útil cuando desea decidir cuál va a ser el estado de consentimiento predeterminado (antes del consentimiento del visitante) para la aplicación web. Por ejemplo:
   * Para la CCPA, el consentimiento predeterminado suele establecerse en `true`. Va a hacer referencia a este escenario como **Inclusión implícita** en este tutorial
   * Para el RGPD, el consentimiento predeterminado suele estar establecido en `false`. Va a hacer referencia a este escenario como **Exclusión implícita** en este tutorial.

<!--
    This consent value can be verified by returning the JavaScript object ```klaro.getManager().consents``` in the browser's developer console.
-->
    >[!NOTA]
    >
    >En general, los pasos mencionados anteriormente los realiza y cuida el equipo o la persona responsable de administrar la CMP, como OneTrust o TrustArc.

## Inyectar una CMP

>[!WARNING]
>
>La práctica recomendada para implementar una plataforma de administración de consentimiento es cargar la CMP _antes_ cargando el administrador de etiquetas. Para facilitar este tutorial, cargará el CMP _con_ el administrador de etiquetas. Esta lección está diseñada para mostrarle cómo utilizar las funciones de consentimiento del SDK web de Platform y no debe utilizarse como guía para configurar correctamente Klaro o cualquier otra CMP.


Ahora, una vez que haya terminado con las configuraciones de Klaro, cree una regla de etiqueta con las siguientes configuraciones:

* [!UICONTROL Nombre]: `all pages - library load - Klaro`
* [!UICONTROL Evento]: [!UICONTROL Library Loaded (Page Top)] con [!UICONTROL Opciones avanzadas] > [!UICONTROL Pedido] establezca en 1
* [!UICONTROL Acción]: [!UICONTROL Código personalizado], [!UICONTROL Idioma]: HTML para cargar el script CMP.

![Inyectar regla CMP](assets/consent-cmp-inject-rule-1.png)

El bloque de código personalizado debe ser similar al siguiente:

![Inyectar regla CMP](assets/consent-cmp-inject-rule-2.png)

Ahora guarde y cree esta regla en su biblioteca de desarrollo y valide que se muestra el banner de consentimiento cambiando la biblioteca de etiquetas del sitio de Luma por la suya propia. Debería ver un banner de CMP en el sitio web, como se muestra a continuación. Y para comprobar el permiso de consentimiento del visitante actual, puede utilizar el siguiente fragmento en la consola del explorador.

```javascript
    klaro.getManager().consents 
```

![Titular de consentimiento](assets/consent-cmp-banner.png)

Para entrar en modo de depuración, utilice la siguiente casilla de verificación en Adobe Experience Platform Debugger.

![Modo de depuración de etiquetas](assets/consent-rule-debugging.png)

Además, es posible que tenga que borrar las cookies y el almacenamiento local varias veces mientras sigue este tutorial, ya que el valor de consentimiento del visitante se almacena allí. Puede hacerlo de la siguiente manera:

![Borrando almacenamiento](assets/consent-clearning-cookies.png)

## Escenarios de consentimiento

Los actos de privacidad como el RGPD, la CCPA y otros desempeñan un papel vital en la forma en que crea la implementación del consentimiento. En esta lección, explora cómo un visitante puede interactuar con el banner de consentimiento en dos actos de privacidad más destacados.
![Escenarios de consentimiento](assets/consent-scenarios.jpeg)


### Escenario 1: inclusión implícita

La inclusión implícita significa que la empresa no necesita obtener el consentimiento del visitante (o la &quot;inclusión&quot;) antes de recopilar sus datos y, por lo tanto, todos los visitantes del sitio web se tratan como &quot;incluidos&quot; de forma predeterminada. Sin embargo, el visitante puede excluirse rechazando las cookies a través del banner de consentimiento. Este caso de uso es similar a la CCPA.

Ahora configurará e implementará el consentimiento para este escenario:

1. En el **[!UICONTROL Privacidad]** de la extensión de etiqueta del SDK web de Experience Platform, asegúrese de que la variable  **[!UICONTROL Consentimiento predeterminado]** se establece en **[!UICONTROL Entrada]** :


   ![Consentimiento Configuración de privacidad de la extensión AEP](assets/consent-web-sdk-privacy-in.png)

   >[!NOTE]
   > 
   >Para una solución dinámica, seleccione la opción &quot;Proporcionar un elemento de datos&quot; y pase un elemento de datos que devuelva el valor de ```klaro.getManager().consents```
   >
   >Esta opción se utiliza si la CMP se inserta en el código fuente *antes* Utilice el código incrustado de etiqueta para que el consentimiento predeterminado esté disponible antes de que la extensión del SDK web de Experience Platform comience a cargarse. En este ejemplo, no se puede utilizar esta opción porque CMP se carga con etiquetas y no antes de las etiquetas.



2. Guarde y cree este cambio en la biblioteca de etiquetas
3. Cargue la biblioteca de etiquetas en el sitio de demostración de Luma.
4. Habilite la depuración de etiquetas en el sitio de Luma y vuelva a cargar la página. En la consola para desarrolladores del explorador, debería ver que defaultConsent es igual a **[!UICONTROL Entrada]**
5. Con esta configuración, la extensión SDK para web de Experience Platform sigue realizando solicitudes de red, a menos que un visitante decida rechazar las cookies y la exclusión:

   ![Consentimiento de inclusión implícito](assets/consent-Implied-optin-default.png)



Si un visitante decide excluirse (rechazar las cookies de seguimiento), debe cambiar el consentimiento a **[!UICONTROL Fuera]**. Cambie la configuración de consentimiento siguiendo estos pasos:

<!--
1. Create a data element to store the consent value of the visitor. Let's call it `klaro consent value`. Use the code snippet to create a custom code type data element:
    
    ```javascript
    return klaro.getManager().consents["aep web sdk"]
    ```

    ![Data Element consent value](assets/consent-data-element-value.png)


1. Create another custom code data element, `consent confirmed`, with the following snippet which returns ```true``` only after a visitor confirms consent:

    
    ```javascript
    return klaro.getManager().confirmed
    ```

    ![Data Element consent confirmed](assets/consent-data-element-confirmed.png)
-->

1. Cree una regla que genere un déclencheur cuando el visitante haga clic en **Me niego**.  Asigne un nombre a esta regla como: `all pages - click consent banner - set consent "out"`

1. Como el **[!UICONTROL Evento]**, use **[!UICONTROL Clic]** el **[!UICONTROL Elementos que coinciden con el selector de CSS]** `#klaro .cn-decline`

   ![El usuario de condición de regla hace clic en &quot;Rechazar&quot;](assets/consent-optOut-clickEvent.png)

1. Ahora, utilice el SDK web de Experience Platform, [!UICONTROL Definir consentimiento] [!UICONTROL tipo de acción] para establecer el consentimiento como &quot;fuera&quot;:

   ![Acción de exclusión de regla de consentimiento](assets/consent-rule-optout-action.png)

1. Seleccionar **[!UICONTROL Guardar en biblioteca y crear]**:

   ![Guarde y cree su biblioteca](assets/consent-rule-optout-saveAndBuild.png)

Ahora, cuando un visitante se excluye, la regla configurada de la forma anterior se activaría y establecería el consentimiento del SDK web como **[!UICONTROL Fuera]**.

Para validarlo, vaya al sitio de demostración de Luma, rechace las cookies y confirme que no se activa ninguna solicitud del SDK web después de la exclusión.

### Escenario 2: exclusión implícita


La exclusión implícita significa que los visitantes deben tratarse como excluidos de forma predeterminada y no se deben configurar cookies. Las solicitudes del SDK web no se deben activar a menos que los visitantes decidan incluirse manualmente aceptando las cookies a través del banner de consentimiento. Es posible que tenga que tratar un caso de uso de este tipo en la región de la Unión Europea donde se aplique el RGPD.

A continuación se muestra cómo puede configurar la configuración para un escenario de exclusión implícito:

1. En Klaro, desactive la **Estado predeterminado del servicio** en su `aep web sdk` y guarde la configuración actualizada.

1. Entrada **[!UICONTROL Privacidad]** de la extensión SDK para web de Experience Platform, establezca el consentimiento predeterminado en **[!UICONTROL Fuera]** o **[!UICONTROL Pendiente]** según sea necesario.

   ![Consentimiento Configuración de privacidad de la extensión AEP](assets/consent-implied-opt-out.png)

1. **Guardar** Actualice la configuración a la biblioteca de etiquetas y vuelva a crearla.

   Con esta configuración, el SDK web de Experience Platform garantiza que no se active ninguna solicitud a menos que el permiso de consentimiento cambie a **[!UICONTROL Entrada]**. Esto puede ocurrir como resultado de la aceptación manual por parte de un visitante de las cookies mediante la inclusión.

1. En Debugger, asegúrese de que el sitio de Luma esté asignado a la propiedad de etiquetas y de que el registro de consola de etiquetas esté activado.
1. Utilice la consola para desarrolladores del explorador para lo siguiente **Borrar datos del sitio** in **Aplicación** > **Almacenamiento**

1. Vuelva a cargar el sitio de Luma y debería verlo `defaultConsent` se establece en **[!UICONTROL Fuera]** y no se han realizado solicitudes de SDK web

   ![Exclusión implícita de consentimiento](assets/consent-implied-out-cmp.png)

En caso de que un visitante decida incluirse (aceptar las cookies de seguimiento), debe cambiar el consentimiento y establecerlo en **[!UICONTROL Entrada]**. Así se puede hacer esto con una regla:

1. Cree una regla que genere un déclencheur cuando el visitante haga clic en **Eso está bien**.  Asigne un nombre a esta regla como: `all pages - click consent banner - set consent "in"`

1. Como el **[!UICONTROL Evento]**, use **[!UICONTROL Clic]** el **[!UICONTROL Elementos que coinciden con el selector de CSS]** `#klaro .cm-btn-success`

   ![El usuario de condición de regla hace clic en &quot;No hay problema&quot;](assets/consent-optIn-clickEvent.png)

1. Añadir una acción mediante el SDK web de Experience Platform [!UICONTROL Extensión], **[!UICONTROL Tipo de acción]** de **[!UICONTROL Definir consentimiento]**, **[!UICONTROL Consentimiento general]** as **[!UICONTROL Entrada]**.

   ![Acción de inclusión de regla de consentimiento](assets/consent-rule-optin-action.png)

   Una cosa que hay que tener en cuenta es que esto [!UICONTROL Definir consentimiento] La acción será la primera solicitud que salga y establezca la identidad. Debido a esto, puede ser importante sincronizar las identidades en la primera solicitud en sí. El mapa de identidad se puede añadir a [!UICONTROL Definir consentimiento] acción al pasar un elemento de datos de tipo de identidad.

1. Seleccionar **[!UICONTROL Guardar en biblioteca y crear]**:

   ![Exclusión de la regla de consentimiento](assets/consent-rule-optin-saveAndBuild.png)

1. **[!UICONTROL Guardar]** Envíe la regla a la biblioteca y vuelva a crearla.

Una vez que haya establecido esta regla, la recopilación de eventos debe comenzar cuando un visitante se incluye.

![Opción de visitante de publicación de consentimiento](assets/consent-post-user-optin.png)


Para obtener más información sobre el consentimiento en el SDK web, consulte [Compatibilidad con preferencias de consentimiento del cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=en).


Para obtener más información sobre [!UICONTROL Definir consentimiento] acción, consulte [Definir consentimiento](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/action-types.html?lang=en#set-consent).

[Siguiente: ](setup-event-forwarding.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
