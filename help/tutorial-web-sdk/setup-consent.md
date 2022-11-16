---
title: Configuración del consentimiento con el SDK web de Platform
description: Obtenga información sobre cómo configurar la configuración de privacidad de la extensión de etiqueta del SDK web de Experience Platform. Esta lección forma parte del tutorial Implementar Adobe Experience Cloud con SDK web .
exl-id: 502a7467-3699-4b2b-93bf-6b6069ea2090
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 0%

---

# Configuración del consentimiento con el SDK web de Platform

Obtenga información sobre cómo configurar la configuración de privacidad de la extensión de etiqueta del SDK web de Experience Platform. Establezca el consentimiento en función de la interacción del visitante con un banner de una plataforma de administración de consentimiento (CMP).

>[!NOTE]
> 
>Para fines de demostración, este tutorial utiliza [Klaro](https://heyklaro.com/) como CMP. Puede seguir utilizando Klaro o el CMP que utilice con su sitio web.


## Objetivos de aprendizaje

Al final de esta lección, puede:

* Carga de una CMP mediante etiquetas
* Configuración de la privacidad en la extensión de etiquetas del SDK web de Experience Platform
* Establezca el consentimiento para el SDK web del Experience Platform en función de la acción del visitante

## Requisitos previos

Debe estar familiarizado con las etiquetas y los pasos para crear reglas, elementos de datos, crear bibliotecas en entornos y cambiar las bibliotecas de etiquetas mediante el depurador de Experience Platform.

Antes de empezar a configurar la configuración de privacidad y a crear las reglas para configurar el consentimiento, asegúrese de haber insertado el script de la plataforma de administración de consentimiento en el sitio web y de que esté funcionando correctamente. Una CMP puede cargarse directamente en el código fuente con la ayuda de los desarrolladores del sitio o cargarse mediante las propias etiquetas. Esta lección demuestra este último enfoque.
>[!NOTE]
> 
>1. Las organizaciones utilizan una plataforma de administración de consentimiento (o CMP) para documentar y administrar de forma legal las opciones de consentimiento de un visitante antes de recopilar, compartir o vender datos de visitantes de fuentes en línea como sitios web y aplicaciones.
>
>2. El método recomendado para inyectar una CMP es directamente a través del código fuente antes del script del administrador de etiquetas.


### Configurar Klaro

Antes de entrar en las configuraciones de etiquetas, obtenga más información sobre la plataforma de administración de consentimiento utilizada en este tutorial, Klaro.

1. Visita [Klaro](https://heyklaro.com/) y configurar una cuenta.
1. Vaya a **Administrador de privacidad** y cree una instancia según las instrucciones.
1. Utilice la variable **Código de integración** para inyectar Klaro en la propiedad tag (las instrucciones están en el siguiente ejercicio).
1. Omita el **Escaneo** , ya que detecta la propiedad tag que está codificada en el sitio web de demostración de Luma y no la que ha creado para este tutorial.
1. Añada un servicio llamado `aep web sdk` y active la opción **Estado predeterminado del servicio**. Cuando está activado, el valor de consentimiento predeterminado es `true`, de lo contrario `false`. Esta configuración es útil cuando desea decidir cuál es el estado de consentimiento predeterminado (antes del consentimiento del visitante) para su aplicación web. Por ejemplo:
   * Para la CCPA, el consentimiento predeterminado se suele establecer en `true`. Va a hacer referencia a este escenario como **Inclusión implícita** a través de este tutorial
   * Para el RGPD, el consentimiento predeterminado se suele establecer en `false`. Va a hacer referencia a este escenario como **Exclusión implícita** a lo largo de este tutorial.

<!--
    This consent value can be verified by returning the JavaScript object ```klaro.getManager().consents``` in the browser's developer console.
-->
    >[!NOTE]
    >
    >Generalmente, los pasos mencionados son realizados y atendidos por el equipo o la persona responsable de manejar la CMP, como OneTrust o TrustArc.

## Inyectar una CMP

>[!WARNING]
>
>La práctica recomendada para implementar una plataforma de administración de consentimiento es generalmente cargar el CMP _before_ cargando el administrador de etiquetas. Para facilitar este tutorial, se cargará el CMP _con_ el administrador de etiquetas. Esta lección está diseñada para mostrarle cómo utilizar las funciones de consentimiento en el SDK web de Platform y no debe utilizarse como guía para configurar correctamente Klaro o cualquier otra CMP.


Ahora, una vez que haya terminado con las configuraciones de Klaro, cree una regla de etiqueta con las siguientes configuraciones:

* [!UICONTROL Nombre]: `all pages - library load - Klaro`
* [!UICONTROL Evento]: [!UICONTROL Biblioteca cargada (Principio de página)] con [!UICONTROL Opciones avanzadas] > [!UICONTROL Pedido] configurado en 1
* [!UICONTROL Acción]: [!UICONTROL Código personalizado], [!UICONTROL Idioma]: HTML para cargar el script CMP.

![Inyectar regla CMP](assets/consent-cmp-inject-rule-1.png)

El bloque de código personalizado debe tener un aspecto similar al siguiente:

![Inyectar regla CMP](assets/consent-cmp-inject-rule-2.png)

Ahora guarde y cree esta regla en la biblioteca de desarrollo, valide el banner de consentimiento que se muestra cambiando la biblioteca de etiquetas del sitio de Luma por la suya propia. Debería ver un banner CMP en el sitio web como se muestra a continuación. Y para comprobar el permiso de consentimiento del visitante actual, puede utilizar el siguiente fragmento de código en la consola del explorador.

```javascript
    klaro.getManager().consents 
```

![Banner de consentimiento](assets/consent-cmp-banner.png)

Para entrar en el modo de depuración, utilice la siguiente casilla de verificación en Adobe Experience Platform Debugger.

![Modo de depuración de etiquetas](assets/consent-rule-debugging.png)

Además, es posible que tenga que borrar las cookies y el almacenamiento local varias veces mientras sigue este tutorial, ya que el valor de consentimiento del visitante se almacena allí. Puede hacerlo de la siguiente manera:

![Borrado de almacenamiento](assets/consent-clearning-cookies.png)

## Escenarios de consentimiento

Los actos de privacidad, como el RGPD, la CCPA y otros, desempeñan un papel vital en la forma en que se diseña la implementación del consentimiento. En esta lección, puede explorar cómo un visitante puede interactuar con el banner de consentimiento bajo dos actos de privacidad más destacados.
![Escenarios de consentimiento](assets/consent-scenarios.jpeg)


### Escenario 1: Inclusión implícita

La inclusión implícita significa que la empresa no necesita obtener el consentimiento del visitante (o la &quot;inclusión&quot;) antes de recopilar sus datos y, por lo tanto, todos los visitantes del sitio web se consideran como participantes de forma predeterminada. Sin embargo, el visitante puede rechazar las cookies mediante el banner de consentimiento. Este caso de uso es similar a la CCPA.

Ahora configurará e implementará el consentimiento para este escenario:

1. En el **[!UICONTROL Privacidad]** de la extensión de etiqueta del SDK web de Experience Platform, asegúrese de que la función  **[!UICONTROL Consentimiento predeterminado]** está configurado como **[!UICONTROL En]** :


   ![Configuración de privacidad de la extensión de AEP de consentimiento](assets/consent-web-sdk-privacy-in.png)

   >[!NOTE]
   > 
   >Para una solución dinámica, seleccione la opción &quot;Proporcionar un elemento de datos&quot; y pase un elemento de datos que devuelva el valor de ```klaro.getManager().consents```
   >
   >Esta opción se utiliza si la CMP se inserta en el código fuente *before* el código incrustado de la etiqueta de modo que el consentimiento predeterminado esté disponible antes de que la extensión SDK web de Experience Platform empiece a cargarse. En este ejemplo, no se puede utilizar esta opción, ya que la CMP se carga con etiquetas y no antes de las etiquetas .



2. Guarde y cree este cambio en la biblioteca de etiquetas
3. Cargue la biblioteca de etiquetas en el sitio de demostración de Luma
4. Habilite la depuración de etiquetas en el sitio de Luma y vuelva a cargar la página. En la consola de desarrollador del explorador, debería ver que defaultConsent es igual a **[!UICONTROL En]**
5. Con esta configuración, la extensión web SDK de Experience Platform sigue realizando solicitudes de red, a menos que un visitante decida rechazar las cookies y la exclusión:

   ![Inclusión implícita en el consentimiento](assets/consent-Implied-optin-default.png)



Si un visitante decide excluirse (rechaza las cookies de seguimiento), debe cambiar el consentimiento a **[!UICONTROL Salida]**. Cambie la configuración del consentimiento siguiendo estos pasos:

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

1. Cree una regla con déclencheur cuando el visitante haga clic en **Me reduzco**.  Asigne a esta regla el nombre: `all pages - click consent banner - set consent "out"`

1. Como **[!UICONTROL Evento]**, use **[!UICONTROL Haga clic en]** en **[!UICONTROL Elementos que coinciden con el selector de CSS]** `#klaro .cn-decline`

   ![El usuario de la condición de regla hace clic en &quot;Rechazo&quot;](assets/consent-optOut-clickEvent.png)

1. Ahora, utilice el SDK web de Experience Platform, [!UICONTROL Establecer consentimiento] [!UICONTROL tipo de acción] para establecer el consentimiento como &quot;out&quot;:

   ![Acción de exclusión de regla de consentimiento](assets/consent-rule-optout-action.png)

1. Select **[!UICONTROL Guardar en biblioteca y crear]**:

   ![Guarde y cree su biblioteca](assets/consent-rule-optout-saveAndBuild.png)

Ahora, cuando un visitante se excluye, la regla configurada de la forma anterior se activa y establece el consentimiento del SDK web como **[!UICONTROL Salida]**.

Valide accediendo al sitio de demostración de Luma, rechace las cookies y confirme que no se activa ninguna solicitud de SDK web tras la exclusión.

### Escenario 2: Exclusión implícita


La exclusión implícita significa que los visitantes deben ser tratados como excluidos de forma predeterminada y no se deben configurar cookies. Las solicitudes del SDK web no se deben activar a menos que los visitantes decidan aceptar manualmente las cookies mediante el banner de consentimiento. Es posible que tenga que lidiar con un caso de uso de este tipo en la región de la Unión Europea donde se aplica el RGPD.

Así puede configurar la configuración para un escenario de exclusión implícito:

1. En Klaro, desactive la **Estado predeterminado del servicio** en su `aep web sdk` y guarde la configuración actualizada.

1. En **[!UICONTROL Privacidad]** sección de la extensión Experience Platform Web SDK, establezca el consentimiento predeterminado en **[!UICONTROL Salida]** o **[!UICONTROL Pendiente]** según sea necesario.

   ![Configuración de privacidad de la extensión de AEP de consentimiento](assets/consent-implied-opt-out.png)

1. **Guardar** la configuración actualizada a la biblioteca de etiquetas y reconstruirla.

   Con esta configuración, el SDK web de Experience Platform garantiza que no se activará ninguna solicitud a menos que el permiso de consentimiento cambie a **[!UICONTROL En]**. Esto puede suceder como resultado de que un visitante acepte manualmente las cookies al activar.

1. En Debugger, asegúrese de que el sitio de Luma esté asignado a la propiedad de etiqueta y de que el registro de consola de etiquetas esté activado.
1. Utilice la consola de desarrollador del explorador para **Borrar datos del sitio** en **Aplicación** > **Almacenamiento**

1. Vuelva a cargar el sitio de Luma y debería ver que `defaultConsent` está configurado como **[!UICONTROL Salida]** y no se han realizado solicitudes de SDK web

   ![Consentimiento de exclusión implícita](assets/consent-implied-out-cmp.png)

Si un visitante decide aceptar la inclusión (acepta las cookies de seguimiento), debe cambiar el consentimiento y configurarlo en **[!UICONTROL En]**. Así puede hacerlo con una regla:

1. Cree una regla con déclencheur cuando el visitante haga clic en **Está bien**.  Asigne a esta regla el nombre: `all pages - click consent banner - set consent "in"`

1. Como **[!UICONTROL Evento]**, use **[!UICONTROL Haga clic en]** en **[!UICONTROL Elementos que coinciden con el selector de CSS]** `#klaro .cm-btn-success`

   ![El usuario de la condición de regla hace clic en &quot;Eso está bien&quot;](assets/consent-optIn-clickEvent.png)

1. Añadir una acción mediante el SDK web del Experience Platform [!UICONTROL Extensión], **[!UICONTROL Tipo de acción]** de **[!UICONTROL Establecer consentimiento]**, **[!UICONTROL Consentimiento general]** como **[!UICONTROL En]**.

   ![Acción de inclusión de regla de consentimiento](assets/consent-rule-optin-action.png)

   Una cosa a tener en cuenta es que esto [!UICONTROL Establecer consentimiento] la acción será la primera solicitud que salga y establezca la identidad. Debido a esto, puede ser importante sincronizar identidades en la primera solicitud en sí. El mapa de identidad se puede agregar a [!UICONTROL Establecer consentimiento] acción pasando un elemento de datos de tipo de identidad.

1. Select **[!UICONTROL Guardar en biblioteca y crear]**:

   ![Exclusión de regla de consentimiento](assets/consent-rule-optin-saveAndBuild.png)

1. **[!UICONTROL Guardar]** la regla a la biblioteca y reconstruirla.

Una vez que haya establecido esta regla, la recopilación de eventos debe comenzar cuando un visitante decida entrar.

![Opción de exclusión de visitantes de anuncio de consentimiento](assets/consent-post-user-optin.png)


Para obtener más información sobre el consentimiento en el SDK web, consulte [Compatibilidad con las preferencias de consentimiento del cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=en).


Para obtener más información sobre [!UICONTROL Establecer consentimiento] acción, consulte [Establecer consentimiento](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/action-types.html?lang=en#set-consent).

[Siguiente: ](setup-event-forwarding.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK web de Adobe Experience Platform. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
