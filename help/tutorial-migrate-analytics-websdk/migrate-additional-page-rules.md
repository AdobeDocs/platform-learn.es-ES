---
title: Migración de reglas de página adicionales
description: Obtenga información sobre cómo migrar reglas adicionales basadas en páginas a la extensión Web SDK.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16764
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Migración de reglas de página adicionales

En este ejercicio aprenderá a migrar reglas adicionales basadas en páginas a la extensión Web SDK. Esto es similar al ejercicio que ya realizó al migrar la regla de carga de página predeterminada a Web SDK. Los métodos aún se aplican. La mayor diferencia es que con estas reglas no se añade una acción Enviar evento, ya que en la mayoría de los casos la regla no contiene la acción Enviar señalización de una extensión de Analytics.

## Información general

Hagamos una copia de seguridad y hablemos de las implementaciones de Analytics tal como son con la extensión de etiquetas de Adobe Analytics (también conocida como implementación de &quot;AppMeasurement&quot;, ya que ese es el nombre del archivo de JavaScript).

No supondré saber exactamente cómo se implementa, pero en muchas implementaciones que utilizan etiquetas de Experience Platform (anteriormente conocidas como &quot;Launch&quot;), hay cualquier número de reglas que solo se activan condicionalmente, en función de algo en la página o en la dirección URL. Algunos ejemplos de esto son:

* Regla de resultados de búsqueda, que solo se activa cuando se ha realizado una búsqueda interna y aparece la página de resultados de la búsqueda
* Regla de página de aterrizaje de Campaign, que solo se activa cuando hay un código de seguimiento en la dirección URL
* Regla de tipo de página, que solo se activa para una página que es un tipo determinado de página, por ejemplo, página de detalles del producto, página del carro de compras, etc.
* Cualquier otra página que se active condicionalmente

El punto clave aquí es que todos estos casos de uso solo activan **a veces** en una página, y esperaríamos **también** que la regla de página predeterminada se activara. Por lo tanto, no se desea incluir una señalización de envío (extensión AA) o un evento de envío (extensión Web SDK) con ninguna de estas reglas o, de lo contrario, se producirían dos visitas que se activarían para la misma carga de página.

Por lo tanto, estas reglas crean el objeto, pero no envían los datos. Solo nos aseguramos de que estas reglas se activen **antes de** la regla de carga de página predeterminada, de modo que después de que creen el objeto, la acción Enviar señalización/Enviar evento en la regla de carga de página predeterminada envíe todo. Ahora, es probable que sepa todo esto y que así es como se configura su sitio. Pero si es nuevo en su propia implementación o si necesita &quot;corregir&quot; la implementación para parecerse a este método, este ejercicio es especialmente útil para usted.

## Ejemplo de migración de una regla condicional

Este es un ejemplo de migración de una regla que se activa condicionalmente. Utilizaré el ejemplo anterior de una página de aterrizaje de campaña. Como he dicho anteriormente, esto sigue el mismo patrón con el que ya hemos trabajado en nuestra regla de página predeterminada, excepto que es aún más fácil porque solo configuramos variables y no activamos ninguna visita.

1. Busque la regla condicional. En este ejemplo, encontramos la regla de código de seguimiento de campaña y la seleccionamos.

   ![Selección de regla de código de seguimiento de campaña](assets/campaign-tracking-code-rule-select.jpg)

1. Cuando se abre la regla, podemos ver que hay una condición en esta regla que se activa en función de un parámetro de cadena de consulta. No es necesario cambiar nada sobre la condición, ya que solo queremos actualizar/migrar la acción, no el evento o la condición.
1. Haga clic en la acción **Adobe Analytics - Set Variable**
1. Anote todo lo que se haya configurado en la acción. En este ejemplo, observamos que **event101** está establecido, así como la variable **Campaign**.

   ![event101](assets/event101.jpg)
   ![campaign var](assets/campaign-variable.jpg)

1. Solo hemos hecho clic aquí para tomar la nota y no es necesario cambiar nada, así que ahora podemos simplemente hacer clic en **cancelar**.
1. Cree una nueva acción haciendo clic en el **icono de signo más** de la sección de acciones

   ![nueva acción](assets/new-action-conditional-rule.jpg)

1. Configuración de la nueva regla
   1. Seleccione **Adobe Experience Platform Web SDK** de la lista desplegable Extensión.
   1. Seleccione **Actualizar variable** de la lista desplegable Tipo de acción.
   1. En el panel derecho, seleccione el objeto **Analytics** dentro del objeto de datos

      ![Acción de actualización de variable](assets/configure-conditional-rule-action.jpg)

1. Ahora establezca event101 y la variable de campaña con los mismos valores que se establecieron en la acción existente.

   ![Establecer evento101](assets/web-sdk-event101.jpg)
   ![Establecer campaña](assets/web-sdk-campaign-var.jpg)

1. Ahora puede **Conservar cambios** y **Guardar en biblioteca**, y la regla se ha migrado a Web SDK.

>[!IMPORTANT]
>
>Al igual que la regla de carga de página predeterminada, dejamos la acción **Set Variable** de la extensión de Analytics en la regla para que podamos comparar los datos a medida que validamos la migración. Recuerde volver más tarde y eliminar la acción de la extensión de Analytics cuando realice la limpieza final.



