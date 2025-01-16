---
title: 'Offer decisioning: configuración de las ofertas y el ID de decisión'
description: 'Offer decisioning: configuración de las ofertas y el ID de decisión'
kt: 5342
doc-type: tutorial
source-git-commit: 926f0f1f6d6b557fd7e59a89aaa3e09d831c82a6
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 4%

---

# 3.3.2 Configurar las ofertas y la decisión

## 3.3.2.1 Creación de ofertas personalizadas

En este ejercicio, creará cuatro **Ofertas personalizadas**. Estos son los detalles que se deben tener en cuenta al crear esas ofertas:

| Nombre | Date Range | Vínculo de imagen para correo electrónico | Vínculo de imagen para web | Texto | Prioridad | Idoneidad | Idioma | Frecuencia de límite | Nombre de imagen |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | hoy - 1 mes después | https://bit.ly/4a9RJ5d | Elija de la biblioteca de Assets | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | todos: mujeres clientes | Inglés (Estados Unidos) | 3 | Apple AirPods Max - Mujer.jpg |
| `--aepUserLdap-- - Galaxy S24` | hoy - 1 mes después | https://bit.ly/3W8yuDv | Elija de la biblioteca de Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | todos: mujeres clientes | Inglés (Estados Unidos) | 3 | Galaxy S24 - Mujer.jpg |
| `--aepUserLdap-- - Apple Watch` | hoy - 1 mes después | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | todos: clientes hombres | Inglés (Estados Unidos) | 3 | Apple Watch - Hombre.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | hoy - 1 mes después | https://bit.ly/4gTrkeo | Elija de la biblioteca de Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | todos: clientes hombres | Inglés (Estados Unidos) | 3 | Galaxy Watch7 - Hombre.jpg |

{style="table-layout:auto"}

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

En el menú de la izquierda, haz clic en **Ofertas** y luego ve a **Ofertas**. Haga clic en **+ Crear oferta**.

![Regla de decisión](./images/offers1.png)

Entonces verá esta ventana emergente. Seleccione **Oferta personalizada** y haga clic en **Siguiente**.

![Regla de decisión](./images/offers2.png)

Ahora estás en la vista **Detalles**.

![Regla de decisión](./images/offers3.png)

En este caso, debe configurar la oferta `--aepUserLdap-- - AirPods Max`. Utilice la información de la tabla anterior para rellenar los campos. En este ejemplo, el nombre de la oferta personalizada es **vangeluw - AirPods Max**. Además, establezca la **fecha y hora de inicio** en hoy y la **fecha y hora de finalización** en una fecha dentro de un mes a partir de ahora.

Una vez finalizado, debería tener esto. Haga clic en **Next**.

![Regla de decisión](./images/offers4.png)

A continuación, verá esto:

![Regla de decisión](./images/constraints.png)

Seleccione **By defined decision rule** y haga clic en el icono **+** para agregar la regla **all - Female Customers**.

Complete la **Prioridad** como se indica en la tabla anterior. A continuación, haga clic en **+ Crear límite** para definir el número de veces que esta oferta se puede mostrar a un cliente.

![Regla de decisión](./images/constraints1.png)

Para el límite, seleccione lo siguiente:

- **Elegir evento de límite**: **Evento de decisión**
- **Tipo de límite**: **Por perfil (aplique un límite para cada perfil)**
- **Recuento de eventos de límite**: **3**
- **Restablecer frecuencia límite**: **Diario**
- **Cada**: **1 día**

Esto garantiza que esta oferta no se muestre más de tres veces al día por cliente.

Haga clic en **Crear**.

![Regla de decisión](./images/constraints2.png)

Entonces volverás a estar aquí. Haga clic en **Next**.

![Regla de decisión](./images/constraints3.png)

Ahora necesita crear **Representaciones**. Las representaciones son una combinación de **Placement** y un recurso real.

Para **Representación 1**, seleccione:

- Canal: web
- Ubicación: Web - Imagen
- Contenido: URL
- Ubicación pública: copie la dirección URL de la columna **Vínculo de imagen para la web** en la tabla anterior

![Regla de decisión](./images/addcontent1.png)

También puede seleccionar **Biblioteca de recursos** para el contenido y luego hacer clic en **Examinar**.

![Regla de decisión](./images/addcontent2.png)

Verá una ventana emergente de la biblioteca de Assets, vaya a la carpeta **enablement-assets** y seleccione el archivo de imagen **Apple AirPods Max - Female.jpg**. A continuación, haga clic en **Seleccionar**.

![Regla de decisión](./images/addcontent3.png)

Entonces verá esto... Haga clic en **+ Agregar representación**.

![Regla de decisión](./images/addcontentrep20.png)

Para **Representación 2**, seleccione:

- Canal: correo electrónico
- Ubicación: correo electrónico, imagen
- Contenido: URL
- Ubicación pública: seleccione **Biblioteca de recursos**. Haga clic en **Examinar**

![Regla de decisión](./images/addcontentrep21.png)

Verá una ventana emergente de la biblioteca de Assets, vaya a la carpeta **enablement-assets** y seleccione el archivo de imagen **Apple AirPods Max - Female.jpg**. A continuación, haga clic en **Seleccionar**.

![Regla de decisión](./images/addcontent3b.png)

Entonces verá esto... A continuación, haga clic en **+ Agregar representación**.

![Regla de decisión](./images/addcontentrep20b.png)

Para **Representación 3**, seleccione:

- Canal: no digital
- Ubicación: no digital, texto

A continuación, debe añadir contenido. En este caso, eso significa añadir el texto que se va a utilizar como llamada a la acción.

Seleccione **Personalizado** y haga clic en **Agregar contenido**.

![Regla de decisión](./images/addcontentrep31.png)

Entonces verá esta ventana emergente.

![Regla de decisión](./images/addcontent3text.png)

Observe el campo **Texto** de la tabla anterior e introduzca ese texto aquí, en este caso: `{{ profile.person.name.firstName }}, 10% discount on AirPods Max`.

También notará que puede seleccionar cualquier atributo de perfil e incluirlo como un campo dinámico en el texto de la oferta. En este ejemplo, el campo `{{ profile.person.name.firstName }}` se asegurará de que el nombre del cliente que recibirá esta oferta se incluya en el texto de la oferta.

Entonces verá esto... Haga clic en **Guardar**.

![Regla de decisión](./images/addcontentrep3text.png)

Ahora tiene esto. Haga clic en **Next**.

![Regla de decisión](./images/addcontentrep3textdone.png)

Verás una descripción general de tu nueva **oferta personalizada**. Haga clic en **Finalizar**.

![Regla de decisión](./images/offeroverview.png)

Haga clic en **Guardar y aprobar**.

![Regla de decisión](./images/saveapprove.png)

A continuación, verá que la oferta personalizada recién creada está disponible en la Información general de ofertas:

![Regla de decisión](./images/offeroverview1.png)

Ahora debe repetir los pasos anteriores para crear las otras tres ofertas personalizadas para los productos que puede encontrar en la tabla anterior.

Cuando termine, la pantalla **Información general de ofertas** para **Ofertas personalizadas** debe mostrar todas las ofertas.

![Ofertas finales](./images/finaloffers.png)

## 3.3.2.2 Crear su oferta de reserva

Después de haber creado cuatro ofertas personalizadas, ahora debes configurar una **Oferta de reserva**.

Asegúrese de que está en la vista **Ofertas**. Haga clic en **+ Crear oferta**.

![Regla de decisión](./images/createoffer.png)

Entonces verá esta ventana emergente. Seleccione **Oferta de reserva** y haga clic en **Siguiente**.

![Regla de decisión](./images/foffers2.png)

Entonces verá esto... Escriba este nombre para la oferta de reserva: `--aepUserLdap-- - CitiSignal Fallback Offer`. Haga clic en **Next**.

![Regla de decisión](./images/foffers4.png)

Ahora necesita crear **Representaciones**. Las representaciones son una combinación de **Placement** y un recurso real.

Para **Representación 1**, seleccione:

- **Canal**: **Web**
- **Ubicación**: **Web - Imagen**
- **Contenido**: **Biblioteca de recursos**

Haz clic en **Examinar** para seleccionar tu imagen.

![Regla de decisión](./images/addcontent1fb.png)

Verá una ventana emergente de la biblioteca Assets, irá a la carpeta **citi-signal-images** y seleccionará el archivo de imagen **App-Banner-Ad.jpg**. A continuación, haga clic en **Seleccionar**.

![Regla de decisión](./images/addcontent3fb.png)

Entonces verá esto... Haga clic en **+ Agregar representación**.

![Regla de decisión](./images/addcontentrep20fb.png)

Para **Representación 2**, seleccione:

- **Canal**: **Correo electrónico**
- **Ubicación**: **Correo electrónico - Imagen**
- **Contenido**: **Biblioteca de recursos**

Haz clic en **Examinar** para seleccionar tu imagen.

![Regla de decisión](./images/addcontentrep21fb.png)

Verá una ventana emergente de la biblioteca Assets, irá a la carpeta **citi-signal-images** y seleccionará el archivo de imagen **App-Banner-Ad.jpg**. A continuación, haga clic en **Seleccionar**.

![Regla de decisión](./images/addcontent3bfb.png)

Entonces verá esto... Haga clic en **+ Agregar representación**.

![Regla de decisión](./images/addcontentrep20bfb.png)

Para **Representación 3**, seleccione:

- **Canal**: **No digital**
- **Ubicación**: **No digital - Texto**
- **Contenido**: **Personalizado**

Haga clic en **Agregar contenido**.

![Regla de decisión](./images/addcontentrep21text.png)

Entonces verá esta ventana emergente. Escriba el texto `{{ profile.person.name.firstName }}, download the CitiSignal app now!` y haga clic en **Guardar**.

![Regla de decisión](./images/faddcontent3text.png)

Entonces verá esto... Haga clic en **Next**.

![Regla de decisión](./images/faddcontentrep3.png)

Verá una descripción general de su nueva **oferta de reserva**. Haga clic en **Finalizar**.

![Regla de decisión](./images/fofferoverview.png)

Finalmente, haga clic en **Guardar y aprobar**.

![Regla de decisión](./images/saveapprovefb.png)

En la pantalla **Información general de ofertas**, ahora verá esto:

![Ofertas finales](./images/ffinaloffers.png)

## 3.3.2.3 Crear su colección

Se usa una colección para **filtrar** un subconjunto de ofertas de la lista de ofertas personalizadas y usarlas como parte de una decisión para acelerar el proceso de decisión.

Ir a **Colecciones**. Haga clic en **+ Crear colección**.

![Regla de decisión](./images/collections.png)

Entonces verá esta ventana emergente. Configure la colección de esta manera. Haga clic en **Next**.

- Nombre de colección: usar `--aepUserLdap-- - CitiSignal Collection`
- Seleccione **Crear colección estática**.

Haga clic en **Next**.

![Regla de decisión](./images/createcollectionpopup1.png)

En la pantalla siguiente, seleccione las cuatro **Ofertas personalizadas** que creó en el ejercicio anterior. Haga clic en **Guardar**.

![Regla de decisión](./images/createcollectionpopup2.png)

Ahora verá lo siguiente:

![Regla de decisión](./images/colldone.png)

## 3.3.2.4 Crear su decisión

Una decisión combina ubicaciones, una colección de ofertas personalizadas y una oferta de reserva que el motor de Offer decisioning utilizará en última instancia para encontrar la mejor oferta para un perfil específico, en función de cada una de las características de oferta personalizadas individuales como prioridad, restricción de elegibilidad y límite total/de usuario.

Para configurar su **decisión**, vaya a **decisiones**. Haga clic en **+ Crear decisión**.

![Regla de decisión](./images/activitydd.png)

Entonces verá esto... Rellene los campos de esta manera. Haga clic en **Next**.

- Nombre: `--aepUserLdap-- - CitiSignal Decision`
- Fecha y hora de inicio: hoy
- Fecha y hora de finalización: hoy + 1 mes

![Regla de decisión](./images/activity2.png)

En la siguiente pantalla, debe agregar ubicaciones en ámbitos de decisión. Deberá crear ámbitos de decisión para las ubicaciones **Web - Imagen**, **Correo electrónico - Imagen** y **No digital - Texto**.

![Regla de decisión](./images/addplacements.png)

Primero, cree el ámbito de decisión para **No digital - Texto** al seleccionar esa ubicación en la lista desplegable. A continuación, haga clic en el botón **Agregar** para agregar criterios de evaluación.

![Regla de decisión](./images/activity3.png)

Seleccione su colección `--aepUserLdap-- - CitiSignal Collection` y haga clic en **Agregar**.

![Regla de decisión](./images/activity4text.png)

Entonces verá esto... Haga clic en el botón **+** para agregar un nuevo ámbito de decisión.

![Regla de decisión](./images/activity5text.png)

Seleccione la ubicación **Web - Imagen** y agregue la colección `--aepUserLdap-- - CitiSignal Collection` bajo criterios de evaluación. A continuación, haga clic de nuevo en el botón **+** para agregar un nuevo ámbito de decisión.

![Regla de decisión](./images/activity6text.png)

Seleccione la ubicación **Correo electrónico - Imagen** y agregue la colección `--aepUserLdap-- - CitiSignal Collection` bajo criterios de evaluación. A continuación, haga clic en **Siguiente**.

![Regla de decisión](./images/activity4.png)

Ahora necesita seleccionar su **Oferta de reserva**, que se llama `--aepUserLdap-- - CitiSignal Fallback Offer`. Haga clic en **Next**.

![Regla de decisión](./images/activity10.png)

Revise su decisión. Haga clic en **Finalizar**.

![Regla de decisión](./images/activity11.png)

En la ventana emergente, haz clic en **Guardar y activar**.

![Regla de decisión](./images/activity12.png)

Y, por último, ahora verá su decisión en la descripción general:

![Regla de decisión](./images/activity13.png)

Ahora ha configurado correctamente su decisión. Su decisión ya está activa y se puede utilizar para ofrecer ofertas optimizadas y personalizadas a sus clientes, en tiempo real.

Paso siguiente: [3.3.3 Prepare la propiedad de cliente de recopilación de datos y la configuración de Web SDK para el Offer decisioning](./ex3.md)

[Volver al módulo 3.3](./offer-decisioning.md)

[Volver a todos los módulos](./../../../overview.md)
