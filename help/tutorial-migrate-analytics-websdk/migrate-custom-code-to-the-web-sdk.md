---
title: Migración del código personalizado a Web SDK
description: Obtenga información sobre cómo migrar código personalizado del objeto s de la extensión de Analytics a Web SDK.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16761
source-git-commit: 346d4b2965248fb34341ad464f3f126667e3d940
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---


# Migración del código personalizado a Web SDK

En este ejercicio, aprenderá a migrar código personalizado de la extensión de Adobe Analytics a la extensión de Adobe Experience Platform Web SDK en Experience Platform Tags.

## El gran descargo de responsabilidad

Estoy seguro de que no le sorprenderá que vaya a agregar algo como esto a un documento que empiece a indicarle la forma mejor, más fácil o más eficaz de trabajar con código. Existen claramente muchas maneras diferentes de escribir, editar y manejar el código. En este ejercicio voy a proporcionarle una forma de tomar fácilmente el código que tiene en una regla existente y copiarlo, agregar un cambio y hacer que funcione para la regla migrada. Si piensa en una mejor manera de hacerlo, es fantástico, y no solo le doy la bienvenida para usarlo, sino para compartirlo con nosotros y con sus colegas en la comunidad Experience League (especialmente en el post de la comunidad con respecto a este tutorial). Lo mismo ocurre con la mitad inferior de la página, que trabaja con complementos de implementación. Te sugeriré un camino aquí, y luego haces lo que te sienta bien. Bien, vamos a entrar en los detalles.

>[!IMPORTANT]
>
>En el espíritu del último párrafo, también es importante recomendar que aproveche esta oportunidad durante la migración a Web SDK para echar un buen vistazo al código y ver si alguno de ellos debe actualizarse o incluso eliminarse. En los párrafos y pasos siguientes verá cómo migrar su código, e incluso si es más fácil mover todo de un solo golpe, sería negligente no recomendar hacer una limpieza de primavera, por así decirlo.

## ¿Migración de qué código?

El código que abordaremos primero en esta sección es el que puede tener en la ventana &quot;Código personalizado&quot; en cualquier acción de Adobe Analytics, incluidas las acciones **Establecer variable**. En otras palabras, abra una de las reglas y mire hacia abajo en la sección de acciones. Si tiene una acción &quot;Adobe Analytics - Set Variables&quot;, haga clic en para abrirla.

![Establecer código de variables](assets/set-variables-action.jpg)

A continuación, desplácese hacia abajo en el lado derecho hasta la parte inferior y verá el botón &quot;Abrir editor&quot; para la ventana Código personalizado. Haga clic para abrir.

![abrir editor de código personalizado](assets/open-aa-custom-code-editor.jpg)

Si tiene código allí, deberá migrarlo para que se pueda ejecutar y enviar a Adobe Analytics mediante Web SDK.
La idea principal aquí es que vamos a convertir el objeto &quot;s&quot; en &quot;contenido&quot;.__adobe.analytics&quot;.

Simplemente tendremos que agregar algún código adicional antes de la primera llamada al objeto s, para que Web SDK pueda entenderlo y gestionarlo. El lugar donde agregamos el código recién modificado es en la ventana Código personalizado de la acción &quot;Adobe Experience Platform Web SDK - Update variable&quot;.

Por ejemplo, supongamos que tiene el siguiente bloque de código en la ventana de código personalizado:

```javascript
const products = window.digitalData.products;
const productIndex = event.element.dataset.productIndex;
const product = products[productIndex];
s.products = [
product.cat3Tag,
product.id,
1,
product.price
].join(";");
```

El código que debe incluir es el siguiente:

```javascript
content.__adobe = content.__adobe || {};
content.__adobe.analytics = content.__adobe.analytics || {};
const s = content.__adobe.analytics;
```

Por lo tanto, siga estos pasos para migrar el código personalizado:

1. Copie el código personalizado fuera de la ventana en la acción Establecer variables de Adobe Analytics
1. Cierre esa ventana de código y cierre (cancelar fuera de) la acción.
1. Abra la acción Web SDK - Update variable haciendo clic en ella (o si aún no tiene una, agregue una).

   ![Abrir acción de actualización de variable](assets/open-sdk-update-variable.jpg)

1. Seleccione el objeto de análisis en la parte superior de la ventana derecha

   ![Seleccionar objeto de análisis](assets/select-analytics-object.jpg)

1. Desplácese hacia abajo hasta la parte inferior y abra la ventana Código personalizado

   ![abrir la ventana de código personalizado del sdk](assets/open-sdk-custom-code.jpg)

1. Pegue el código que ha traído desde la ventana de código personalizado de Analytics
1. Ahora coloque las nuevas líneas de código en medio del código existente, de modo que esté sobre la primera mención del objeto s, como en el siguiente ejemplo:

![Nuevo código s](assets/new-s-code.jpg)

Ahora puede guardar el código en la ventana Código personalizado y conservar los cambios en la acción Actualizar variables. También deberá guardar la regla y publicar los nuevos cambios en la biblioteca de trabajo.

## ¿Qué sucede con los complementos?

Si tiene una implementación &quot;appMeasurement&quot; de Adobe Analytics mediante la extensión de Analytics en Experience Platform Tags (anteriormente conocida como &quot;Launch&quot;), es probable que esté utilizando uno o más &quot;complementos&quot; de JavaScript para configurar variables o para realizar otras tareas. Si estas funciones y llamadas de JavaScript se encuentran en una ventana de código dentro de una regla, la información anterior en esta página debería ayudarle a migrar el código a Web SDK.
Sin embargo, también es más probable que el código del complemento esté en la ventana de código en la configuración de la propia extensión de Adobe Analytics. Para comprobar si tiene complementos y otro código para migrar, abra la extensión de Analytics en Recopilación de datos y etiquetas, abra su propiedad y, a continuación, haga clic en **Extensiones** en el panel de navegación izquierdo.

1. Seleccione la ficha **Instalado** situada en la parte superior de la página y, a continuación, seleccione la extensión de Adobe Analytics.
1. A continuación, en el lado derecho de la página, haga clic en **Configurar**

   ![configurar la extensión de analytics](assets/configure-analytics-extension.jpg)

1. Expanda la sección **Configurar rastreador con código personalizado**
1. Haga clic para **abrir editor**

   ![abrir editor principal](assets/aa-extension-custom-code-window.jpg)

En este punto, podrá ver el código que tiene y es posible que tenga &quot;complementos&quot; de JavaScript, es decir, fragmentos de código que le ayudan a obtener los datos que desea y asignarlos a dimensiones personalizadas, etc.

No todo lo que hay en esta ventana de código puede considerarse como complementos en su sentido más auténtico de Adobe Analytics. Esto es importante que lo entienda a medida que decida cómo migrar el código.

### Recomendación para migrar código desde la ventana de código principal de la extensión.

Bueno, de nuevo, no todo en la ventana de código puede ser un plug-in oficial creado por Adobe Consulting. Parte del mismo puede ser código que haya escrito, tanto si lo llama complemento como si no. Recomendamos dos cambios. Se utilizan para utilizar una nueva extensión y también para copiar y pegar el resto del código en un nuevo lugar.

**Primero**, hay una extensión disponible en las etiquetas llamada **Complementos comunes de Web SDK**. Esta extensión es un subconjunto de la lista total de complementos de implementación que se enumeran en la documentación de Adobe Analytics. Al instalar esta extensión en la propiedad Etiquetas, está instalando el código de los complementos incluidos. A continuación, para usar estos complementos, los encontrará al crear **elementos de datos** nuevos. Más sobre eso en un momento.

**Segundo**, hay una ventana de código en la configuración de la extensión de Web SDK donde puede colocar todo (o parte) de su código, SI desea que ese código se ejecute justo antes de que los eventos se envíen a Adobe Analytics. Los pasos para encontrar esa ventana de código son:

1. Si ya ha agregado la extensión Web SDK a su propiedad, vaya a **Extensiones** y seleccione la pestaña **Instalado**
1. Seleccione la extensión **Adobe Experience Platform Web SDK** y ábrala haciendo clic en **Configurar** en el carril derecho.

   ![Configurar extensión de Web SDK](assets/configure-websdk-extension.jpg)

1. Desplácese hacia abajo hasta la sección **Recopilación de datos** y haga clic para abrir la ventana de código de **onBeforeEventSend**.

   ![onBeforeEventSend](assets/on-before-event-send-window.jpg)

Aquí es donde pegará el código que desee ejecutar justo antes de que el evento se envíe a Analytics desde Web SDK. Esto es básicamente lo que la función doPlugins estaba haciendo en la antigua implementación de Analytics.

La **buena noticia** es que debería ejecutarse **en cualquier momento** si realiza un evento de envío, así que, independientemente de si se produce al cargar la página o con un vínculo personalizado, este código debería ejecutarse, configurar las variables, etc.

#### ¿Debo cambiar mi código?

Bueno, sí y no. Sí, es necesario cambiar un par de cosas pequeñas, pero no, no es necesario cambiar la mayor parte del código siempre y cuando se cambien estas pequeñas cosas:

_**Cambio de código 1:**_
Después (o antes de que elija) de pegar el código de &quot;complemento&quot; en la ventana de código de la extensión de Web SDK, **elimine** las líneas &quot;doPlugin&quot; de su código. No los necesitará y provocarán un error, ya que forman parte de appMeasurement.js, pero no del código SDK de Web.

![Quitar líneas de código doPlugins](assets/remove-doplugins.jpg)

_**Cambio de código 2:**_
El otro cambio que deberá hacer es agregar algún código para que se defina el objeto &quot;s&quot;, muy similar a lo que se discute arriba con respecto al código en las acciones de regla. En este caso, tendremos que definir el código un poco diferente, añadiendo un nodo de &quot;datos&quot; que ya está definido en la acción de regla, pero no aquí.
Esta definición debe colocarse en la parte superior de la ventana de código. El código que debe copiarse en (al colocarlo en la extensión Web SDK) es el siguiente:

```javascript
content.data.__adobe = content.data.__adobe || {};
content.data.__adobe.analytics = content.data.__adobe.analytics || {};
const s = content.data.__adobe.analytics;
```

_**Con ambos cambios de código:**_
Este es el código mencionado anteriormente, pero con ambos cambios acabamos de discutir:

![Código actualizado](assets/update-code.jpg)

### Pasos para migrar el código de extensión principal a Web SDK

Como se ha indicado anteriormente, la recomendación es doble: utilizar la nueva extensión Common Web SDK Plugins y también copiar y pegar el código de la configuración de la extensión de Analytics en la configuración de la extensión de Web SDK. Teniendo esto en cuenta, junto con la nota importante de la parte superior de la página para limpiar el código, estos son los pasos recomendados en un nivel superior:

1. Copie todo el código de la ventana de código de configuración de la extensión de Analytics y péguelo en la ventana onBeforeEventSend de la configuración de la extensión Web SDK (aunque es posible que tengamos que copiar código que necesite eliminarse o actualizarse, haremos algunas pasadas en el código de la nueva ventana).
1. Revise su código ahora en la extensión Web SDK y busque llamadas a complementos o definición de función para complementos definidos en la extensión **Common Web SDK Plugins**. Puede encontrar la lista de complementos en la ventana de definición de elementos de datos de Web SDK después de instalar la extensión de complementos. También puede encontrarlo en la [documentación de esa extensión](https://exchange.adobe.com/apps/ec/108520).
1. Para cada uno de los complementos que encuentre en la nueva extensión de complementos de Web SDK, elimine la extensión y la llamada a ella desde su código. Asegúrese de compensar esta eliminación creando un elemento de datos y llamando a dicho elemento de datos en la regla adecuada para establecer variables, etc.
1. A continuación, revise el código para ver si se han definido llamadas a funciones en el archivo appMeasurement.js. **Cambio de código 1** anterior es un ejemplo de esto, y puede hacer esta eliminación del código doPlugins en este momento, si aún no lo ha hecho. En el caso de otras instancias, esto será más evidente cuando tenga una llamada a una función que no esté definida en ninguna parte del código. También puede consultar con Asistencia al cliente de Adobe o con sus colegas de la Comunidad de Experience League para asegurarse de que este sea el caso con ese código.
1. A continuación, pase el código para actualizar o eliminar cualquier código antiguo que ya no se aplique a sus necesidades de análisis, como se recomienda en la parte superior de esta página.
1. Ahora realice el **Cambio de código 2** mencionado anteriormente, agregando las líneas adicionales para que cualquier referencia al objeto s no cause errores en su código.
1. Por último, pero no menos importante, probar, probar y probar un poco más. Después de eso, prueba otra vez. Asegúrese de que el código proporciona los resultados esperados tanto en Experience Platform Debugger como en los informes de Adobe Analytics.

>[!NOTE]
>
>Dos últimas ideas sobre los pasos anteriores.
>En primer lugar, es posible que piense que sería más fácil dejar todo el código del complemento allí, en lugar de eliminarlo y utilizar la nueva extensión Common Web SDK Plugins. Esto es cierto y está bien, pero al utilizar la extensión se obtienen las ventajas de utilizar una interfaz de usuario, definir un elemento de datos reutilizable y también recibir automáticamente cualquier actualización de código en el futuro. Probablemente vale la pena hacer el cambio.
>
>En segundo lugar, hablando de &quot;realizar el cambio&quot;, también puede decidir actualizar TODO el código personalizado para que no haga referencia al objeto &quot;s&quot; antiguo, que es una especie de extensión del paso 5 anterior. Esto es, por supuesto, totalmente aceptable y una gran idea. Este tutorial de migración solo intenta facilitar un poco la migración del código personalizado, en caso de que tenga mucho y no tenga los recursos para actualizar todo en este momento. Tú decides.

Terminaremos esta lección tal como la iniciamos, con el reconocimiento de que hay muchas maneras de escribir código, y este documento le da algunos pasos a seguir si desea hacerlo de esta manera. Lo principal es que el código funciona y obtiene los resultados esperados, así que siéntase libre de hacerlo a su manera, ¿y mencioné que debería probar?
