---
title: Crear políticas de combinación
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Crear políticas de combinación
description: En esta lección, debe crear políticas de combinación para determinar cómo se combinan los datos en los perfiles.
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# Crear políticas de combinación

<!--20 min-->

En esta lección, debe crear políticas de combinación para priorizar cómo se combinan varias fuentes de datos en los perfiles.

Adobe Experience Platform permite reunir datos de varias fuentes y combinarlos para ver una vista completa de cada cliente individual. Al unir estos datos, las políticas de combinación determinan cómo se priorizan los datos y qué datos se combinan para crear esa vista unificada.

Nos ceñiremos a la interfaz de usuario para esta lección, pero también existen opciones de API para crear políticas de combinación.

**Los arquitectos de datos** deberán crear políticas de combinación fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre las políticas de combinación:
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on&enablevpops)

## Permisos necesarios

En la lección [Configurar permisos](configure-permissions.md), configuró todos los controles de acceso necesarios para completar esta lección.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Acerca de las políticas de combinación y esquema de unión

Como recordará, en la lección sobre la ingesta por lotes, cargamos dos registros con información ligeramente diferente para el mismo cliente. En los datos de [!DNL Loyalty], el nombre del cliente era `Daniel` y vivía en `New York City`, pero en los datos de CRM el nombre del cliente era `Danny` y vivía en `Portland`. Los datos de los clientes cambian con el tiempo. Tal vez se movió de `Portland` a `New York City`. Otras cosas también cambian, como números de teléfono y direcciones de correo electrónico. Las políticas de combinación le ayudan a decidir cómo gestionar estos tipos de conflictos cuando dos fuentes de datos proporcionan información diferente para el mismo usuario.

Entonces, ¿por qué `Danny` ganó como nombre? Vamos a echar un vistazo:

1. En la interfaz de usuario de Platform, seleccione **[!UICONTROL Perfiles]** en el panel de navegación izquierdo
1. Vaya a la ficha **[!UICONTROL Políticas de combinación]**
1. La política de combinación predeterminada es la marca de tiempo solicitada. Como cargó los datos de CRM después de los datos de Fidelidad, `Danny` ganó como nombre en el perfil:

![Pantalla de políticas de combinación](assets/mergepolicies-default.png)

Cuando hay varios esquemas habilitados para el perfil, se crea automáticamente un [!UICONTROL Esquema de unión] para todos los esquemas de registro habilitados para perfiles que comparten una clase base. Para ver los [!UICONTROL esquemas de unión], vaya a la ficha **[!UICONTROL Esquema de unión]**.

![Pantalla de políticas de combinación](assets/mergepolicies-unionSchema.png)

Tenga en cuenta que no hay ningún esquema de unión para la clase ExperienceEvent. Aunque los datos de ExperienceEvent siguen entrando en el perfil, ya que se basan en series temporales, cada evento incluye una marca de tiempo y un ID, y los conflictos no representan un problema.

Ahora, ¿qué sucede si no le gusta esa política de combinación predeterminada? ¿Qué sucede si Luma decide que su sistema de lealtad debe ser la fuente de la verdad cuando hay un conflicto? Para ello, vamos a crear una política de combinación.

## Creación de una política de combinación en la IU

1. En la pantalla Políticas de combinación, seleccione el botón **[!UICONTROL Crear política de combinación]** en la esquina superior derecha
1. Como **[!UICONTROL Nombre]**, escriba `Loyalty Prioritized`
1. Como **[!UICONTROL Esquema]**, seleccione **[!UICONTROL Perfil XDM]** (tenga en cuenta que su clase personalizada, como es datos de registro, también está disponible para políticas de combinación)
1. Para la vinculación de ID **[!UICONTROL 1, seleccione**&#x200B;[!UICONTROL &#x200B; Gráfico privado &#x200B;]&#x200B;**]**
1. Para **[!UICONTROL Combinar atributos]**, seleccione **[!UICONTROL Prioridad de conjuntos de datos]**
1. Arrastre y suelte `Luma Loyalty Dataset` y `Luma CRM Dataset` en el panel **[!UICONTROL Conjunto de datos]**.
1. Asegúrese de que `Luma Loyalty Dataset` esté en la parte superior arrastrándolo y soltándolo encima de `Luma CRM Dataset`
1. Seleccione el botón **[!UICONTROL Guardar]**
   <!--do i need to explain Private Graph? Is that GA?-->
   ![Política de combinación](assets/mergepolicies-newPolicy.png)

## Validación de la política de combinación

Veamos si la política de combinación está haciendo lo que esperaríamos:

1. Vaya a la ficha **[!UICONTROL Examinar]**
1. Cambiar la **[!UICONTROL política de combinación]** a la nueva política `Loyalty Prioritized`
1. Como **[!UICONTROL área de nombres de identidad]**, use su `Luma CRM Id`
1. Como **[!UICONTROL valor de identidad]**, use `112ca06ed53d3db37e4cea49cc45b71e`
1. Seleccione el botón **[!UICONTROL Mostrar perfil]**
1. `Daniel` ha vuelto.

![Ver un perfil con una política de combinación diferente](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Crear una política de combinación con conjuntos de datos limitados

Al crear directivas de combinación que utilizan la prioridad de conjuntos de datos, solo se incluyen en el perfil los conjuntos de datos de la misma clase base que se incluyen en la derecha. Vamos a configurar otra política de combinación

1. En la pantalla Políticas de combinación, seleccione el botón **[!UICONTROL Crear política de combinación]** en la esquina superior derecha
1. Como **[!UICONTROL Nombre]**, escriba `Loyalty Only`
1. Como **[!UICONTROL Esquema]**, seleccione **[!UICONTROL Perfil XDM]**
1. Para **[!UICONTROL Vinculación de ID]**, seleccione **[!UICONTROL Ninguno]**
1. Para **[!UICONTROL Combinar atributos]**, seleccione **[!UICONTROL Prioridad de conjuntos de datos]**
1. Arrastre y suelte solo el `Luma Loyalty Dataset` en el panel **[!UICONTROL Conjunto de datos seleccionado]**.
1. Seleccione el botón **[!UICONTROL Guardar]**

![Política de combinación solo de fidelización](assets/mergepolicies-loyaltyOnly.png)

## Validación de la política de combinación

Veamos ahora lo que hace esta política de combinación:

1. Vaya a la ficha **[!UICONTROL Examinar]**
1. Cambiar la **[!UICONTROL política de combinación]** a la nueva política `Loyalty Only`
1. Como **[!UICONTROL área de nombres de identidad]**, use su `Luma CRM Id`
1. Como **[!UICONTROL valor de identidad]**, use `112ca06ed53d3db37e4cea49cc45b71e`
1. Seleccione el botón **[!UICONTROL Mostrar perfil]**
1. Confirme que no se han encontrado perfiles:
   ![Fidelidad solamente sin búsqueda de ID de CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

El ID de CRM es un campo de identidad en `Luma Loyalty Dataset`, pero solo se pueden usar identidades principales para buscar perfiles. Así que vamos a buscar el perfil usando la identidad principal, `Luma Loyalty Id`&quot;

1. Cambiar **[!UICONTROL área de nombres de identidad]** a `Luma Loyalty Id`
1. Como **[!UICONTROL valor de identidad]**, use `5625458`
1. Seleccione el botón **[!UICONTROL Mostrar perfil]**
1. Seleccione el ID de perfil para abrir el perfil
1. Vaya a la ficha **[!UICONTROL Atributos]**
1. Tenga en cuenta que otros detalles de perfil del conjunto de datos de CRM, como el número de teléfono móvil y la dirección de correo electrónico, no están disponibles porque solo
   ![Los datos CRM no se pueden ver en la directiva Solo fidelización](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Vaya a la ficha **[!UICONTROL Eventos]**
1. Los datos de ExperienceEvent están disponibles a pesar de no incluirlos explícitamente en los conjuntos de datos de las políticas de combinación:
   ![Los eventos se pueden ver en la directiva Solo fidelización](assets/mergepolicies-loyaltyOnly-events.png)

## Más información sobre las políticas de combinación

En la búsqueda de perfiles, cambie la política de combinación utilizada a `Default Timebased` y seleccione el botón **[!UICONTROL Mostrar perfil]**. ¡Danny ha vuelto!

![Ver un perfil con una política de combinación diferente](assets/mergepolicies-backToDanny.png)

¿Qué está pasando aquí? Bueno, la combinación de perfiles no es una cosa única. Los perfiles de clientes en tiempo real se ensamblan sobre la marcha, en función de varios factores, incluida la política de combinación que se utiliza. Puede crear varias políticas de combinación para utilizarlas en diferentes contextos, según la vista del cliente que desee.

Un caso de uso clave de las políticas de combinación es la gobernanza de datos. Por ejemplo, supongamos que ingiere datos de terceros en Platform que no se pueden usar en casos de uso de personalización, pero _se puede_ usar en casos de uso de publicidad. Puede crear una política de combinación que excluya este conjunto de datos de terceros y utilizar esta política de combinación para generar segmentos para los casos de uso de publicidad.

## Recursos adicionales

* [Documentación de políticas de combinación](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [Referencia de la API de políticas de combinación (parte de la API del perfil del cliente en tiempo real)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Ahora pasemos al [marco de control de datos](apply-data-governance-framework.md).
