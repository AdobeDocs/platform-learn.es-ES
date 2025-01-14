---
title: Eliminar los elementos de la extensión de Adobe Analytics
description: Cuando la depuración y validación hayan finalizado, elimine todas las referencias a los elementos de extensión de Adobe Analytics y elimine la extensión en sí.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16766
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Eliminar los elementos de la extensión de Adobe Analytics

Cuando la depuración y validación hayan finalizado, elimine todas las referencias a los elementos de extensión de Adobe Analytics y elimine la extensión en sí.

## Información general

Una vez que esté seguro de que todo el contenido de la propiedad se ha migrado a Web SDK y haya finalizado la depuración y validación (en su entorno de desarrollo), estará listo para quitar las referencias a la extensión de Adobe Analytics. La rapidez con la que elimine estos elementos y la cantidad de veces que realice la prueba mientras lo hace depende de usted. Si desea tener más cuidado, quite las referencias lentamente y compruébelas entre cada extracción. Si está seguro de que todo funciona correctamente y migra correctamente, puede &quot;quitar la tirita&quot; y quitar todos los elementos. Por supuesto, recomendamos realizar pruebas al final del ejercicio.

## Eliminación de acciones antiguas de las reglas

De nuevo, vamos a suponer que ya ha probado todo y que funciona correctamente. En este punto, puede entrar en las reglas una por una y eliminar las acciones que pertenecen a la extensión de Adobe Analytics.

1. Abra una de las reglas, por ejemplo, la regla de carga de página predeterminada.
1. Tras haber migrado esta regla, es probable que tenga 4 (o más) acciones.

   ![Las 4 acciones](assets/all-four-actions.jpg)

1. Se puede ver que los dos primeros tienen el identificador &quot;Adobe Analytics&quot;. Estas son las acciones que queremos eliminar.
1. Pase el ratón sobre la primera, como la acción &quot;Adobe Analytics - Set Variables&quot;, y aparecerá una X que permitirá la eliminación. Haga clic en la X y verá desaparecer la acción. Elimine todas y cada una de las acciones de Adobe Analytics de la regla, en este caso la acción Establecer variable y la acción Enviar señalización.
1. Esto solo deja las acciones de Web SDK

   ![Solo acciones de Web SDK](assets/websdk-actions-only.jpg)

1. Guardar en biblioteca
1. Genere la biblioteca y pruebe el sitio para asegurarse de que no hay errores nuevos y de que todo funciona correctamente
1. Repita esta acción para las demás reglas, compilando en la biblioteca de desarrollo y probando entre cada eliminación (o con la frecuencia que crea conveniente). Solo tiene que probar en Debugger o también comprobar los informes en el grupo de informes de migración, en función de su nivel de comodidad.

## Eliminación de extensiones

Ahora que ha eliminado las referencias a su extensión de Adobe Analytics, puede eliminar (o deshabilitar) la extensión, así como cualquier otra extensión que la utilice o que dependa de ella. Personalmente, me gusta un enfoque cuidadoso, y por lo tanto &quot;deshabilitar&quot; es mi elección en lugar de desinstalar, al menos inicialmente.

1. Seleccione **Extensiones** del carril izquierdo de la interfaz de usuario.
1. Asegúrese de que la ficha **Instalado** esté seleccionada.
1. Seleccione la extensión de Adobe Analytics.
1. En el carril derecho, elija desactivar la extensión (o haga clic en los tres puntos y desinstale si lo prefiere).

   ![Deshabilitar extensión de Analytics](assets/disable-analytics-extension.jpg)

1. Haga lo mismo con la extensión del Servicio de ID de Experience Cloud, ya que ya no la necesitará. La extensión Web SDK administra el ID y, por lo tanto, no necesita la extensión adicional.
1. Haga lo mismo con cualquier otra extensión asociada con la extensión de Adobe Analytics, pero solo después de haber realizado los cambios de migración necesarios.
1. Genere los cambios en su entorno de desarrollo.

