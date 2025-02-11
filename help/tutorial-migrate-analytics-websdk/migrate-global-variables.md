---
title: Migrar variables globales
description: Obtenga información sobre cómo migrar variables globales de la configuración de la extensión de Analytics a Web SDK
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16764
exl-id: 0917e951-c7e0-4723-8354-d308890bdaac
source-git-commit: d01889ca317e29ed0c37b20e17291c4cb5a3abd1
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 3%

---

# Migrar variables globales

En este ejercicio aprenderá a migrar variables globales de la configuración de la extensión de Analytics a Web SDK.

## Información general

En la extensión de Adobe Analytics, hay una sección de configuración llamada &quot;Variables globales&quot;.

![Etiqueta de variables globales](assets/analytics-global-variables-label.jpg)

Las variables globales son variables que se establecen en el objeto de seguimiento de Analytics cuando el objeto se inicializa en la página. Todas las variables que configure se establecerán cuando el objeto de seguimiento se cree en cada página.

![Conjunto de variables globales](assets/analytics-set-global-variables.jpg)

Si tiene variables configuradas aquí, también debemos migrarlas al SDK web.

## Dónde se agregan variables globales en Web SDK

La **conclusión** aquí es que no hay un área equivalente en la configuración de la extensión de Web SDK, por lo que no será tan fácil como copiar las variables como lo hicimos en el ejercicio Regla de carga de página predeterminada.
En su lugar, la respuesta breve es: **Cree una nueva regla que se ejecute antes que las demás reglas de todas las páginas y establezca las variables en ella.**

Si no necesita definir los pasos necesarios, vaya a hacerlo y habrá terminado esta lección. Si desea ayuda, continúe...

### Pasos para migrar variables globales a Web SDK

1. Abra la configuración de la extensión de Adobe Analytics.

   ![Configuración de extensión AA](assets/configure-analytics-extension.jpg)

1. Desplácese hacia abajo hasta la sección Variables globales (imagen anterior), ábrala y anote una o todas las variables configuradas. Deberá conocer estas variables y valores en un paso posterior.
1. Cancele de nuevo la extensión de Analytics.
1. Seleccione **Reglas** en el panel de navegación izquierdo y haga clic en **Agregar regla**.
1. Asigne a la nueva regla el nombre &quot;Variables globales&quot;.
1. Haga clic en el botón Añadir en Eventos.

   ![Regla de variable global 1](assets/global-variable-rule-1.jpg)

1. Configure el evento para que se almacene en déclencheur antes que el resto de reglas. Deberá conocer el tipo de evento y el orden que ha utilizado en otras reglas. Valores de ejemplo:
   1. Definir la **extensión** como principal
   1. **Tipo de evento** podría estar preparado para DOM, según su implementación
   1. Expandir **Opciones avanzadas**
   1. Establezca **Order** en un número inferior al de las demás reglas para que se ejecute primero.
      ![Configurar evento de variable global](assets/configure-global-variable-event.jpg)
      >[!NOTE]
      >
      >Lo principal aquí es que esta regla se activa antes de la regla de carga de página predeterminada, de modo que cualquier variable configurada en esta regla puede enviarse a Analytics mediante la regla sendEvent. Sin embargo, sugerimos que esta regla ejecute **first** en general, ya que las variables configuradas en la sección Variables globales de la extensión de Analytics podrían modificarse en otras reglas. Estamos imitando esa funcionalidad. En el ejemplo anterior, suponemos que &quot;10&quot; es un número de orden inferior al de cualquiera de las demás reglas. Si esto no es correcto, cambie el número a un número inferior al resto de las reglas.
1. Seleccione **Conservar cambios** para guardar el trabajo.
1. No es necesario agregar condiciones a esta regla, por lo que puede dejar sola esa sección de creación de reglas.
1. Haga clic en el icono de signo más debajo de la sección **Acciones**
1. Configuración de la nueva acción
   1. Elija la extensión **Extension** de Adobe Experience Platform Web SDK
   1. Para **Tipo de acción**, elija Actualizar variable
   1. A la derecha, elija la variable **Elemento de datos** (para este tutorial, se llamó &quot;Elemento de datos de vista de página&quot;, pero el suyo puede variar)
   1. Seleccione **Analytics** en el objeto de datos
   1. Rellene las variables que guardó desde la sección Variables globales en la configuración de la extensión de Analytics (en el ejemplo de este tutorial, estableciendo eVar 10 en el elemento de datos de tipo de página)

   ![websdk-global-variables-action](assets/websdk-global-variables-action.jpg)

1. Conservar cambios
1. Guarde la regla en la biblioteca de trabajo y créela

Las variables globales se migrarán a Web SDK y se activarán al cargar cualquier página.
