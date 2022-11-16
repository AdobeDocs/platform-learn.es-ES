---
title: Crear una propiedad de etiqueta
description: Obtenga información sobre cómo iniciar sesión en la interfaz de recopilación de datos y crear una propiedad de etiqueta. Esta lección forma parte del tutorial Implementación del Experience Cloud en sitios web .
exl-id: f83d374a-a831-4598-b9d3-6f183224b589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 60%

---

# Crear una propiedad de etiqueta

En esta lección, debe crear la primera propiedad de etiqueta.

Una propiedad es básicamente un contenedor que se rellena con extensiones, reglas, elementos de datos y bibliotecas al implementar etiquetas en el sitio.

## Requisitos previos

Para completar las siguientes lecciones, debe tener permiso para desarrollar, aprobar, publicar, administrar extensiones y administrar entornos en etiquetas. Si no puede completar estos pasos porque ninguna de las opciones de la interfaz de usuario está disponible, póngase en contacto con su administrador de Experience Cloud para solicitar el acceso. Para obtener más información sobre los permisos de usuario de etiquetas, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al usar este contenido:
>
> * El platform launch (lado del cliente) ya está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El servidor de platform launch está ahora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Las configuraciones de Edge ahora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**


## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Inicie sesión en la interfaz de usuario de la recopilación de datos
* Crear una nueva propiedad de etiqueta
* Configuración de una propiedad de etiqueta

## Vaya a la interfaz de recopilación de datos

**Para llegar a la recopilación de datos**

1. Inicie sesión en [Adobe Experience Cloud](https://experiencecloud.adobe.com).

1. Haga clic en el ![Icono de cambio de solución](images/launch-solutionSwitcher.png) para abrir el conmutador de aplicaciones

1. Select **[!UICONTROL Inicio/Recopilación de datos]** en el menú ![Abra el conmutador de soluciones mediante el icono y haga clic en Iniciar/Recopilación de datos](images/launch-solutionSwitcherActivation.png)

Ahora debería ver la pantalla de `Tags Properties` (si nunca se han creado propiedades en la cuenta, esta pantalla puede estar vacía):

![Pantalla Propiedades](images/launch-propertiesScreen.png)

## Crear una propiedad

Una propiedad es básicamente un contenedor que se rellena con extensiones, reglas, elementos de datos y bibliotecas al implementar etiquetas en el sitio. Una propiedad puede ser cualquier conjunto de uno o varios dominios y subdominios. Puede administrar y rastrear estos recursos de manera similar. Por ejemplo, supongamos que tiene varios sitios web basados en una plantilla y quiere rastrear los mismos recursos en todos. Puede aplicar una propiedad a varios dominios. Para obtener más información sobre la creación de propiedades, consulte [“Empresas y propiedades”](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html) en la documentación del producto.

**Para crear una propiedad**

1. Haga clic en el botón **[!UICONTROL Nueva propiedad]**:

   ![Haga clic en Nueva propiedad](images/launch-addNewProperty.png)

1. Asigne un nombre a la propiedad (por ejemplo `Luma Tutorial` o `Luma Tutorial - Daniel`)
1. Como dominio, introduzca `enablementadobe.com` porque es el dominio en el que se aloja el sitio de demostración de Luma. Aunque el campo &quot;Dominio&quot; es obligatorio, la propiedad tag funcionará en cualquier dominio en el que esté implementada. El principal propósito de este campo es que se puedan rellenar previamente las opciones de menú en el generador de reglas.
1. Expanda el **[!UICONTROL Opciones avanzadas]** y marque la casilla para **[!UICONTROL Ejecutar componentes de regla en secuencia]**
1. Haga clic en el botón **[!UICONTROL Guardar]**.

   ![Creación de una nueva propiedad](images/launch-newProperty.png)

La nueva propiedad se debe mostrar en la página de Propiedades. Recuerde que si marca la casilla situada al lado del nombre de la propiedad, las opciones **[!UICONTROL Configurar]** o **[!UICONTROL Eliminar]** aparecerán encima de la lista de propiedades. Haga clic en el nombre de la propiedad (p. ej. `Luma Tutorial`) para abrir la pantalla `Overview`.
![Haga clic en el nombre de la propiedad para abrirla.](images/launch-openProperty.png)

[Siguiente: “Añadir el código de incrustación de ](add-embed-code.md)
