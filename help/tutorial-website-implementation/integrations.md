---
title: Implementar integraciones de Experience Cloud con etiquetas
description: Descubra cómo validar las integraciones de audiencias, A4T y Atributos del cliente en su implementación de Adobe Experience Cloud. Esta lección forma parte del tutorial Implementación del Experience Cloud en sitios web .
exl-id: 1d02efce-a50a-4f4d-a0cf-eb8275cf0faa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 91%

---

# Integraciones de Experience Cloud

En esta lección, repasaremos las integraciones clave entre las soluciones que acaba de implementar. La buena noticia es que al completar las lecciones anteriores, ya ha implementado los aspectos de código de las integraciones. No es necesario que realice ningún trabajo más en esta lección, aparte de leer y validar.

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

1. Explicar los casos de uso básicos de las integraciones de Compartir audiencias, Analytics para Target (A4T) y Atributos del cliente.
1. Validar los aspectos básicos de la implementación del lado del cliente de estas integraciones.

## Requisitos previos

Debe completar todas las lecciones anteriores de este tutorial antes de seguir las instrucciones de esta lección.

>[!NOTE]
>
>Existen diversos requisitos de permisos de usuario, configuraciones de cuenta y pasos de aprovisionamiento necesarios para utilizar completamente estas integraciones y que están fuera del ámbito de este tutorial. Si aún no utiliza estas integraciones en su implementación actual de Experience Cloud, debe tener en cuenta lo siguiente:
>
>* Examinar todos los requisitos de las [integraciones de servicios principales](https://experienceleague.adobe.com/docs/core-services/interface/about-core-services/core-services.html?lang=es).
>* Revise todos los requisitos de la [integración de Analytics para Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html).
>* Pida a un administrador de su organización de Experience Cloud [que solicite la provisión de estas integraciones](https://www.adobe.com/go/audiences).


## Audiencias

[Audiencias](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=es) forma parte del servicio principal People y le permite compartir audiencias entre soluciones. Por ejemplo, puede crear una audiencia en Audience Manager y utilizarla para enviar contenido personalizado con Target.

Los requisitos principales para implementar A4T (que ya ha hecho) son:

1. Implementación del servicio de ID de Adobe Experience Platform
1. Implementar Audience Manager
1. Implemente otras soluciones en las que desee recibir o crear audiencias, como Target y Analytics

### Validar la integración de audiencias

La mejor manera de validar la integración de audiencias es crear una audiencia, compartirla en otra solución y luego usarla por completo en la otra solución (por ejemplo, confirmar que un visitante apto para un segmento de AAM puede cumplir los requisitos para una actividad de Target dirigida a ese segmento). Sin embargo, eso no entra dentro del ámbito de este tutorial.

Estos pasos de validación se centran en la parte fundamental visible de la implementación del lado del cliente: el ID de visitante.

1. Abra el [sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Asegúrese de que Debugger asigne la propiedad de etiqueta a *your* Entorno de desarrollo, tal como se describe en la sección [lección anterior](switch-environments.md)

   ![El entorno de desarrollo de etiquetas que se muestra en Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

1. Vaya a la pestaña Red (Network) de Debugger.

1. Haga clic en **[!UICONTROL Borrar todas las solicitudes]** para mantenerlo todo aseado.

1. Vuelva a cargar la página de Luma y asegúrese de que ve tanto las solicitudes de Target como las de Analytics en Debugger.

1. Vuelva a cargar la página de Luma.

1. Ahora debe ver cuatro solicitudes en la pestaña Red (Network): dos para Target y dos para Analytics.

1. Busque en la fila denominada “ID de visitante de Experience Cloud”. Los ID de cada solicitud por cada solución siempre deben ser iguales.

   ![Confirmar los SDID coincidentes](images/integrations-matchingECIDs.png)

1. Los ID son únicos de cada visitante y los puede confirmar solicitando a un compañero que repita estos pasos.

## Analytics para Target (A4T)

La integración de [Analytics para Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es) le permite aprovechar sus datos de Analytics como fuente para crear informes de métricas en Target.

Los requisitos principales para implementar A4T (que ya ha hecho) son:

1. Implementación del servicio de ID de Adobe Experience Platform
1. Active la solicitud de carga de página de Target antes de la señalización de vista de página de Analytics

A4T funciona uniendo una solicitud de servidor de Target a Analytics con la señalización de vista de página de Analytics, que llamamos “vinculación de visitas”.  La vinculación de visitas requiere que la solicitud de Target que envía la actividad (o aumenta una métrica de objetivos basada en Target) tenga un parámetro que coincida con un parámetro en la señalización de vista de página de Analytics. Este parámetro se denomina ID de datos suplementario (SDID).

### Validación de la implementación de A4T

La mejor manera de validar la integración de A4T es crear una actividad de Target con A4T y validar los datos de informes. Sin embargo, es un tema que sobrepasa el ámbito de este tutorial. Este tutorial muestra cómo confirmar que los ID de datos suplementarios coinciden entre las llamadas de solución.

**Para validar de los SDID**

1. Abra el [sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Asegúrese de que Debugger asigne la propiedad de etiqueta a *your* Entorno de desarrollo, tal como se describe en la sección [lección anterior](switch-environments.md)

   ![El entorno de desarrollo de etiquetas que se muestra en Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

1. Vaya a la pestaña Red (Network) de Debugger.

1. Haga clic en **[!UICONTROL Borrar todas las solicitudes]** para mantenerlo todo aseado.

1. Vuelva a cargar la página de Luma y asegúrese de que ve tanto las solicitudes de Target como las de Analytics en Debugger.

1. Vuelva a cargar la página de Luma.

1. Ahora debe ver cuatro solicitudes en la pestaña Red (Network): dos para Target y dos para Analytics.

1. Busque en la fila denominada “ID de datos suplementario”. Los ID de la primera carga de página deben coincidir entre Target y Analytics. Los ID de la segunda carga de página también deben coincidir, pero deben diferir de la primera carga de página.

   ![Confirmar los SDID coincidentes](images/integrations-matchingSDIDs.png)

Si realiza solicitudes de Target adicionales en el ámbito de una carga de página (sin incluir aplicaciones de una sola página) que formen parte de actividades de A4T, asígneles nombres únicos (no target-global-mbox) para que sigan teniendo los mismos SDID de las solicitudes iniciales de Target y Analytics.

## Atributos del cliente

[Los atributos del cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=es) forman parte del servicio principal People, que permite cargar datos de la base de datos de administración de la relación con los clientes (CRM) y aprovecharlos en Adobe Analytics y Adobe Target.

Los requisitos principales para implementar los atributos del cliente (que ya ha hecho) son:

1. Implementación del servicio de ID de Adobe Experience Platform
1. Configuración de los ID de cliente mediante el servicio de ID *before* Target y Analytics activan sus solicitudes (algo que ya ha hecho mediante la función de orden de reglas en etiquetas)

### Validación de la implementación de los atributos del cliente

Ya ha validado que los ID de cliente se pasan al servicio de ID y a Target en lecciones anteriores. También puede validar el ID de cliente en la visita de Analytics. En este momento, el ID de cliente es uno de los pocos parámetros que no aparecen en Experience Cloud Debugger, pero puede utilizar la consola de JavaScript del navegador para verlo.

1. Abra el sitio de Luma.
1. Abra las herramientas para desarrolladores del navegador
1. Vaya a la pestaña Red (Network).
1. En el campo de filtro, escriba `b/ss` que limitará lo que ve para las solicitudes de Adobe Analytics.

   ![Abra las herramientas para desarrolladores y filtre la pestaña Red (Network) para mostrar solo las solicitudes de Analytics](images/aam-openTheJSConsole.png).

1. Haga clic en el vínculo **[!UICONTROL LOGIN]** en la esquina superior derecha del sitio.

   ![Haga clic en Iniciar sesión en la parte superior derecha](images/idservice-loginNav.png)

1. Escriba `test@adobe.com` como nombre de usuario.
1. Escriba `test` como contraseña.
1. Haga clic en el botón **[!UICONTROL LOGIN]**.

   ![Escriba las credenciales y haga clic en iniciar sesión](images/idservice-login.png)

1. Debería volver a la página principal, que también activará una señalización que puede ver en las herramientas para desarrolladores. Si le conduce a la página de información de la cuenta, haga clic en el logotipo de WE.RETAIL para volver a la página principal.
1. Haga clic en la solicitud y seleccione la pestaña Encabezados:
1. Desplácese hacia abajo hasta que vea varios parámetros anidados
   1. CID: es el delimitador estándar para la parte del ID de cliente de la solicitud.
   1. crm_id: es el código de integración personalizado que especificó en la lección de servicio de ID.
   1. ID: el valor de ID de cliente que proviene del elemento de datos `Email (Hashed)`.
   1. AS: es el estado de autenticación, en el que “1” significa que ha iniciado sesión.

   ![Validación de ID de cliente de Analytics](images/integrations-analyticsCustomerIDValidation.png)

[Siguiente: “Publicar su propiedad” >](publish.md)
