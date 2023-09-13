---
title: Creación de una zona protegida
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Creación de una zona protegida
description: En esta lección, debe crear una zona protegida del entorno de desarrollo que puede utilizar para el resto del tutorial.
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: fdb6a49caa29d98d73524fd0887d25641ef67780
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 2%

---

# Creación de una zona protegida

<!--25min-->

En esta lección, debe crear una zona protegida de entorno de desarrollo que utilizará para el resto del tutorial.

Los entornos limitados proporcionan entornos aislados en los que puede probar la funcionalidad sin mezclar recursos y datos con el entorno de producción. Para obtener más información, consulte la [documentación de zonas protegidas](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=es).

**Arquitectos de datos** y **Ingenieros de datos** deberá crear entornos limitados fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre las zonas protegidas:
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) Esta lección, ha configurado todos los controles de acceso necesarios para completar esta lección.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## Crear una zona protegida

Vamos a crear una zona protegida:

1. Inicie sesión en [Adobe Experience Platform](https://experience.adobe.com/platform) interfaz
1. Ir a **[!UICONTROL Zonas protegidas]** en el panel de navegación izquierdo
1. Seleccionar **[!UICONTROL Crear zona protegida]** en la parte superior derecha
   ![Seleccione Crear zona protegida](assets/sandbox-createSandbox.png)

1. Seleccionar **[!UICONTROL Desarrollo]** como el **[!UICONTROL Tipo]**
1. Asigne un nombre a la zona protegida `luma-tutorial` (considere añadir su nombre al final)
1. Título del tutorial `Luma Tutorial` (considere añadir su nombre al final)
1. Seleccione el botón **[!UICONTROL Crear]**
   ![Crear su zona protegida](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >Aunque puede utilizar valores arbitrarios para el nombre y el título de la zona protegida, se recomienda mantener los valores sugeridos, ya que nos referiremos a estas etiquetas en todo el tutorial. Si varias personas de su organización completan este tutorial, considere la posibilidad de agregar su nombre al final del título y el nombre de la zona protegida, por ejemplo, luma-tutorial-ignatiusjreilly.

Las zonas protegidas tardan aproximadamente 30 segundos en crearse, tiempo durante el cual[!UICONTROL Creando]&quot; estado aparece. Cuando la zona protegida esté completamente creada, se mostrará como &quot;[!UICONTROL Activo]&quot;:
![Estado activo](assets/sandbox-active.png)

Espere hasta que su zona protegida sea &quot;[!UICONTROL Activo]&quot; antes de continuar con el siguiente ejercicio.

## Agregar la nueva zona protegida a la función

Una vez que la zona protegida esté activa, debe incluirla en su función para poder utilizarla. Para agregarlo a su función (requiere privilegios de administrador del sistema o administrador de productos):

1. Vaya a la [!UICONTROL Permisos] pantalla
1. Abra el `Luma Tutorial Platform` función
1. Opcionalmente _quitar_ el `Prod` zona protegida de la función
1. Añada el `Luma Tutorial` espacio aislado
1. Seleccione **[!UICONTROL Guardar]**
1. En el [!UICONTROL Zonas protegidas] fila, seleccione **[!UICONTROL Editar]**

   ![Añadir el tutorial de Luma](assets/sandbox-addLumaTutorial.png)

1. Vuelva a cargar (o Mayús-recargar) la página y ahora debería estar en el `Luma Tutorial` o debería aparecer en la lista desplegable de la zona protegida
1. Cambie a la `Luma Tutorial` zona protegida si aún no está en ella

   ![Confirmar zona protegida](assets/sandbox-confirmDropdown.png)

Genial. Ha creado su zona protegida y está listo para lo siguiente [Configuración de Developer Console y Postman](set-up-developer-console-and-postman.md)!
