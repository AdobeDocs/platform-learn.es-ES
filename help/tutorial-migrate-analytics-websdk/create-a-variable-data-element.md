---
title: Crear un elemento de datos Variable
description: Añada un elemento de datos que se genere con varias reglas y que luego se envíe al Edge Network y se reenvíe a Adobe Analytics
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16759
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Crear un elemento de datos Variable

Añada un elemento de datos que se genere con varias reglas y que luego se envíe al Edge Network y se reenvíe a Adobe Analytics.

Este elemento de datos creará el objeto &quot;Data&quot;, que se utilizará para volver a pasar variables de Adobe Analytics (props, eVars, eventos, etc.) a Adobe Analytics y Adobe Target. Por lo tanto, al igual que con la creación del &quot;objeto s&quot; en una implementación de AppMeasurement de Analytics, crearemos este tipo: objeto de variable al que se debe acceder y actualizar en todas las reglas, y se puede utilizar para rellenar props y eVars en Analytics.

1. En la interfaz de recopilación de datos, haga clic en **Elementos de datos** en el panel de navegación izquierdo.

   Se le redirigirá a la página de aterrizaje de los elementos de datos, donde verá todos los elementos de datos preexistentes. Necesitamos crear un nuevo elemento de datos para facilitar la migración. Haga clic en **Agregar elemento de datos**.

   ![Agregar elemento de datos](assets/add-new-data-alement.jpg)

1. Configure el elemento de datos.
   1. Asigne a su elemento de datos el nombre que desee: algo que le ayudará a recordar que esto es crear los datos en su página y que este será el tipo &quot;Variable&quot;. Para este tutorial, lo llamaremos **Variable de datos de vista de página**.
   1. Seleccione **Adobe Experience Platform Web SDK** de la lista desplegable Extensión.
   1. Seleccione **Variable** de la lista desplegable **Tipo de elemento de datos**.
   1. En el panel derecho, seleccione el botón de opción **Datos**.
   1. Compruebe la solución **Adobe Analytics** y cualquiera de las otras soluciones que también está migrando; por ejemplo, **Adobe Target** que se muestra en esta captura de pantalla.
1. Haga clic en **Guardar**.

   ![Configurar elemento de datos de variable](assets/configure-variable-data-element.jpg)
