---
title: Adición del servicio de identidad de Adobe Experience Platform con etiquetas
description: Obtenga información sobre cómo añadir la extensión del servicio de identidad de Adobe Experience Platform y utilizar la acción “Set Customer ID” (establecer ID de cliente) para recopilar los ID de cliente. Esta lección forma parte del tutorial Implementación del Experience Cloud en sitios web.
solution: Data Collection, Experience Cloud Services
exl-id: f226c171-2bd2-44fa-ae2e-cbfa2fe882f0
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1945'
ht-degree: 65%

---

# Añadir el servicio de identidad de Adobe Experience Platform

Esta lección le guiará por los pasos necesarios para implementar la [extensión del servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=es) y enviar los ID de cliente.

El [servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es) establece un identificador de visitante común en todas las soluciones de Adobe para potenciar las funciones de Experience Cloud, como el uso compartido de audiencias entre soluciones. También puede enviar sus propios ID de cliente al servicio para permitir integraciones y segmentaciones en todos los dispositivos con los sistemas de administración de la relación con los clientes (CRM).

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al utilizar este contenido:
>
> * El platform launch (lado del cliente) ahora es **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El lado del servidor de platform launch ahora es **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=es)**
> * Ahora, las configuraciones de Edge son **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Añadir la extensión del servicio de identidad
* Crear un elemento de datos para recopilar los ID de cliente.
* Crear una regla que utilice la acción “Set Customer ID” (establecer ID de cliente) para enviar los ID de cliente a Adobe.
* Utilizar la función de orden de reglas para secuenciar las reglas que se activan con el mismo evento.

## Requisitos previos

Ya debería haber completado las lecciones en la sección [Configurar etiquetas](create-a-property.md).

## Añadir la extensión del servicio de identidad

Dado que es la primera extensión que añade, a continuación le ofrecemos una descripción general rápida de lo que son las extensiones. Las extensiones son una de las funciones principales de las etiquetas. Una extensión es una integración creada por Adobe, un socio de Adobe o cualquier cliente de Adobe que añada opciones nuevas e ilimitadas a las etiquetas que puede incorporar a un sitio web. Si piensa en las etiquetas como un sistema operativo, las extensiones son las aplicaciones que instala para que las etiquetas puedan hacer lo que usted necesite.

**Para añadir la extensión de servicio de identidad**

1. En el panel de navegación izquierdo, haga clic en **[!UICONTROL Extensiones]**

1. Haga clic en **[!UICONTROL Catálogo]** para ir a la página Catálogo de extensiones

1. Tenga en cuenta la variedad de extensiones disponibles en el catálogo.

1. En el filtro de la parte superior, escriba &quot;ID&quot; para filtrar el catálogo.

1. En la tarjeta del servicio de identidad de Adobe Experience Platform, haga clic en **[!UICONTROL Instalar]**

   ![Instalación de la extensión del servicio de identidad](images/idservice-install.png)

1. Tenga en cuenta que el ID de su organización de Experience Cloud se ha detectado automáticamente.

1. Deje todos los ajustes predeterminados y haga clic en **[!UICONTROL Guardar en biblioteca y crear]**

   ![Guardar la extensión](images/idservice-save.png)

>[!NOTE]
>
>Cada versión de la extensión del servicio de ID incluye una versión específica de VisitorAPI.js que se indica en la descripción de la extensión. Para actualizar la versión VisitorAPI.js, actualice la extensión del servicio de identidad.

### Validación de la extensión

La extensión del servicio de ID es una de las pocas extensiones de etiqueta que realiza una solicitud sin tener que utilizar una acción de regla. La extensión realiza automáticamente una solicitud al servicio de identidad en la primera carga de página de la primera visita a un sitio web. Una vez solicitado el ID, se almacena en una cookie de origen que comienza con “AMCV_”.

**Para validar la extensión del servicio de identidad**

1. Abra el [sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Asegúrese de que Debugger asigne la propiedad de etiqueta a *su entorno de desarrollo*, tal como se describe en la [lección anterior](switch-environments.md).

1. En la pestaña Resumen de Debugger, la sección de etiquetas debe indicar que se ha implementado la extensión del servicio de ID de Adobe Experience Platform.

1. Además, en la pestaña Resumen, la sección del servicio de ID debe rellenarse con el mismo ID de organización mostrado en la pantalla de configuración de la extensión en la interfaz de recopilación de datos:

   ![Compruebe que la extensión del servicio de identidad de Adobe Experience Platform esté implementada](images/idservice-debugger-summary.png)

1. La solicitud inicial para recuperar el ID de visitante puede aparecer en la pestaña del servicio de identidad de Debugger. Puede que ya se haya solicitado, por lo que no debe preocuparse si no la ve:
   ![Compruebe si hay una solicitud al servicio de identidad con el ID de su organización](images/idservice-idRequest.png)

1. Después de la solicitud inicial para recuperar el ID de visitante, el ID se almacena en una cookie cuyo nombre comienza con `AMCV_`. Puede confirmar que la cookie se ha configurado haciendo lo siguiente:
   1. Abra las herramientas para desarrolladores del navegador
   1. Vaya a la pestaña `Application`.
   1. Amplíe `Cookies` en el lado izquierdo.
   1. Haga clic en el dominio `https://luma.enablementadobe.com`.
   1. Busque la cookie “AMCV_” en el lado derecho. Es posible que haya visto varias desde que ha cargado el sitio de Luma usando tanto su propiedad de etiqueta codificada como también la asignada a la suya propia.

      ![Verifique la cookie “AMCV_”](images/idservice-AMCVCookie.png)

¡Ya está! ¡Ha añadido su primera extensión! Para obtener más información sobre las opciones de configuración del servicio de identidad, consulte [la documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html?lang=es).

## Envío de los ID de cliente

A continuación, enviará un [ID de cliente](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=es) al servicio de identidad. Esto le permite [integrar su CRM](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=es) con Experience Cloud, así como rastrear a los visitantes entre dispositivos.

En la lección anterior [Añadir elementos de datos, reglas y bibliotecas](add-data-elements-rules.md) ha creado un elemento de datos y lo ha utilizado en una regla. Ahora se utilizan las mismas técnicas para enviar un ID de cliente cuando se autentica al visitante.

### Creación de elementos de datos para el ID de cliente

Comience creando dos elementos de datos:

1. `Authentication State`: para recopilar si el visitante ha iniciado sesión o no.
1. `Email (Hashed)`: para recopilar la versión con hash de la dirección de correo electrónico (utilizada como ID de cliente) de la capa de datos.

**Para crear el elemento de datos del estado de autenticación**

1. Haga clic en **[!UICONTROL Elementos de datos]** en el panel de navegación izquierdo
1. Haga clic en el botón **[!UICONTROL Agregar elemento de datos]**

   ![Haga clic en “Añadir elemento de datos”](images/idservice-addDataElement1.png)

1. Asigne un nombre al elemento de datos `Authentication State`.
1. Para el **[!UICONTROL Tipo de elemento de datos]**, seleccione **[!UICONTROL Código personalizado]**
1. Haga clic en el botón **[!UICONTROL Abrir editor]**

   ![Abra el editor para agregar el código personalizado para el elemento de datos](images/idservice-authenticationState.png).

1. En la ventana [!UICONTROL Editar código], utilice el siguiente código para devolver valores de “logged in” (sesión iniciada) o “logged out” (sesión finalizada) según un atributo de la capa de datos del sitio de Luma:

   ```javascript
   if (digitalData.user[0].profile[0].attributes.loggedIn)
       return "logged in"
   else
       return "logged out"
   ```

1. Haga clic en **[!UICONTROL Guardar]** para guardar el código personalizado

   ![Guarde el código personalizado](images/idservice-authenticationCode.png)

1. Mantenga el resto de configuraciones en sus valores predeterminados.
1. Haga clic en **[!UICONTROL Guardar en biblioteca]** para guardar el elemento de datos y volver a la página de elementos de datos. No tendremos que hacer una &quot;compilación&quot; hasta que hayamos realizado todos los cambios y estemos listos para validarla.

   ![Guarde el elemento de datos](images/idservice-authenticationStateFinalSave.png)

Al conocer el estado de autenticación del usuario, sabe cuándo debe existir un ID de cliente en la página para enviarlo al servicio de identidad. El siguiente paso es crear un elemento de datos para el propio ID de cliente. En el sitio de muestra de Luma se utiliza la versión con hash de la dirección de correo electrónico del visitante.

**Para añadir el elemento de datos para el correo electrónico con hash**

1. Haga clic en el botón **[!UICONTROL Agregar elemento de datos]**

   ![Añadir un elemento de datos](images/idservice-addDataElement2.png)

1. Asigne un nombre al elemento de datos `Email (Hashed)`.
1. Para el **[!UICONTROL Tipo de elemento de datos]**, seleccione **[!UICONTROL Variable de JavaScript]**
1. Como **[!UICONTROL nombre de variable de JavaScript]**, use el siguiente puntero a una variable en la capa de datos del sitio de Luma: `digitalData.user.0.profile.0.attributes.username`
1. Mantenga el resto de configuraciones en sus valores predeterminados.
1. Haga clic en **[!UICONTROL Guardar en biblioteca]** para guardar el elemento de datos

   ![Guarde el elemento de datos](images/idservice-emailHashed.png)

### Añadir una regla para enviar los ID de cliente

El servicio de identidad de Adobe Experience Platform pasa los ID de cliente en reglas mediante una acción denominada “Set Customer ID” (establecer ID de cliente).  Cree una regla para activar esta acción cuando se autentique el visitante.

**Para crear una regla para enviar los ID de cliente**

1. En el panel de navegación izquierdo, haga clic en **[!UICONTROL Reglas]**
1. Haga clic en **[!UICONTROL Agregar regla]** para abrir el Generador de reglas.

   ![Añadir una regla](images/idservice-addRule.png)

1. Asigne un nombre a la regla `All Pages - Library Loaded - Authenticated - 10`.

   >[!TIP]
   >
   >Esta convención de nombres indica que está activando esta regla en la parte superior de todas las páginas cuando el usuario está autenticado y que tendrá un orden de &quot;10&quot;. El uso de una convención de nombres como esta (en lugar de asignarle un nombre para las soluciones activadas en las acciones) le permitirá minimizar el número total de reglas que necesita la implementación.

1. En **[!UICONTROL Eventos]**, haga clic en **[!UICONTROL Agregar]**

   ![Añadir un evento](images/idservice-customerId-addEvent.png)

   1. Para el **[!UICONTROL Tipo de evento]**, seleccione **[!UICONTROL Biblioteca cargada (Principio de página)]**
   1. Expanda la sección **[!UICONTROL Opciones avanzadas]** y para el **[!UICONTROL Pedido]** escriba `10`. El orden controla la secuencia de reglas activadas por el mismo evento. Las reglas con un orden inferior se activan antes que las reglas con un orden superior. En este caso, debe configurar el ID de cliente antes de activar la solicitud de Target, lo que se explica en la siguiente lección con una regla con un orden de `50`.
   1. Haga clic en el botón **[!UICONTROL Conservar cambios]** para volver al Generador de reglas.

   ![Guardar el evento](images/idservice-customerId-saveEvent.png)

1. En **[!UICONTROL condiciones]**, haga clic en **[!UICONTROL Agregar]**

   ![Añadir una condición a la regla](images/idservice-customerId-addCondition.png)

   1. Para el **[!UICONTROL Tipo de condición]**, seleccione **[!UICONTROL Comparación de valores]**
   1. Haga clic en el ![icono de elemento de datos](images/icon-dataElement.png) para abrir el modal del elemento de datos.

      ![Abrir el modal del elemento de datos](images/idservice-customerId-valueComparison.png)

   1. En el modal del elemento de datos, haz clic en **[!UICONTROL Estado de autenticación]** y luego haz clic en **[!UICONTROL Seleccionar]**

      ![Establecer el estado de autenticación](images/idservice-customerId-authStateCondition.png)

1. Asegúrese de que el operador es `Equals`.
1. Escriba “logged in” en el campo de texto, lo que hace que la regla se active siempre que el elemento de datos “Estado de autenticación” (Authentication State) tenga el valor “logged in”.

1. Haga clic en **[!UICONTROL Conservar cambios]**

   ![Guardar la condición](images/idservice-customerId-loggedIn.png)

1. En **[!UICONTROL Acciones]**, haga clic en **[!UICONTROL Agregar]**

   ![Añadir una acción nueva](images/idservice-customerId-addAction.png)

   1. Para la **[!UICONTROL extensión]**, seleccione **[!UICONTROL Servicio de ID de Experience Cloud]**
   1. Para el **[!UICONTROL tipo de acción]**, seleccione **[!UICONTROL Establecer ID de cliente]**
   1. Para el **[!UICONTROL código de integración]**, escriba `crm_id`
   1. Para **[!UICONTROL Value]**, abra el modal del selector de elementos de datos y seleccione `Email (Hashed)`
   1. Para el **[!UICONTROL estado de autenticación]**, seleccione **[!UICONTROL Autenticado]**
   1. Haga clic en el botón **[!UICONTROL Conservar cambios]** para guardar la acción y volver al Generador de reglas

      ![Configure la acción y guarde los cambios](images/idservice-customerId-action.png)

1. Haga clic en el botón **[!UICONTROL Guardar en biblioteca y crear]** para guardar la regla

   ![Guardar la regla](images/idservice-customerId-saveRule.png)

Ha creado una regla que enviará el ID de cliente como variable `crm_id` cuando el visitante se autentique. Ya que especificó el orden como `10`, esta regla se activará antes de la regla `All Pages - Library Loaded` que se cree en la lección [Añadir elementos de datos, reglas y bibliotecas](add-data-elements-rules.md), que utiliza el valor de orden predeterminado de `50`.

### Validación de los ID de cliente

Para validar su trabajo, iniciará sesión en el sitio de Luma para confirmar el comportamiento de la nueva regla.

**Para iniciar sesión en el sitio Luma**

1. Abra el [sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Asegúrese de que Debugger asigne la propiedad de etiqueta a *su entorno de desarrollo*, tal como se describe en la [lección anterior](switch-environments.md)

   ![Se muestra el entorno de desarrollo de etiquetas en Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

1. Haga clic en el vínculo **[!UICONTROL LOGIN]** en la esquina superior derecha del sitio de Luma

   ![Haga clic en LOGIN en la barra de navegación superior](images/idservice-loginNav.png)

1. Escriba `test@adobe.com` como nombre de usuario.
1. Escriba `test` como contraseña.
1. Haga clic en el botón **[!UICONTROL INICIAR SESIÓN]**

   ![Escriba las credenciales y haga clic en iniciar sesión](images/idservice-login.png)

1. Vuelva a la página principal.

Ahora, confirme que el ID de cliente se envía al servicio mediante la extensión de Debugger.

**Para validar que el servicio de identidad está pasando el ID del cliente**

1. Asegúrese de que la pestaña del sitio de Luma esté centrada.
1. En Debugger, vaya a la pestaña del servicio de identidad de Adobe Experience Platform.
1. Expandir su ID de organización.
1. Haga clic en la celda con el valor `Customer ID - crm_id`.
1. En el modal, observe el valor de ID de cliente y que se refleja el estado `AUTHENTICATED`:

   ![Confirmar el ID de cliente en Debugger](images/idservice-debugger-confirmCustomerId.png)

1. Tenga en cuenta que puede confirmar el valor de correo electrónico con hash observando el código fuente de la página de Luma y la propiedad de nombre de usuario. Debe coincidir con el valor que se ve en Debugger:

   ![correo electrónico con hash en el código fuente](images/idservice-customerId-inSourceCode.png)

### Sugerencias de validación adicionales

Las etiquetas también tienen abundantes funciones de registro de consola. Para activarlos, vaya a la ficha **[!UICONTROL Herramientas]** en Debugger y active la opción **[!UICONTROL Registro de consola de etiquetas]**.

![Activar el registro de consola de las etiquetas](images/idservice-debugger-logging.png)

Esto activa el registro de la consola, tanto en la consola del navegador como en la pestaña Logs de Debugger. Debería ver el registro de todas las reglas creadas hasta el momento. Tenga en cuenta que las nuevas entradas de registro se añaden en la parte superior de la lista, por lo que la regla “Todas las páginas - Biblioteca cargada - Autenticado - 10” se debe activar antes que la regla “Todas las páginas - Biblioteca cargada” y aparecer debajo de ella en el registro de consola de Debugger:

![Pestaña Logs de Debugger](images/idservice-debugger-loggingStatements.png)

[Siguiente: &quot;Añadir Adobe Target&quot; >](target.md)
