---
title: Módulo 7 Actualizar su ID de configuración y Probar su Recorrido
description: Actualizar el ID de configuración y probar el Recorrido
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: d3ceb676-d7f5-4f52-85a4-deaa5ef24034
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 1%

---

# 7.3 Actualizar la propiedad de recopilación de datos y probar el recorrido

## 7.3.1 Actualizar la propiedad de recopilación de datos

Vaya a [Recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/launch/) y seleccione **Etiquetas**.

Esta es la página Propiedades de la recopilación de datos de Adobe Experience Platform que vio anteriormente.

![Página de Properties](../module1/images/launch1.png)

En el módulo 0, Sistema de demostración creó dos propiedades de cliente para usted: uno para el sitio web y otro para la aplicación móvil. Para encontrarlos, busque `--demoProfileLdap--` en el **[!UICONTROL Buscar]** en la ventana Haga clic en para abrir el **Web** propiedad.

![Cuadro de búsqueda](../module1/images/property6.png)

Entonces verás esto.

![Configuración de Launch](./images/rule1.png)

En el menú de la izquierda, vaya a **Reglas** y buscar la regla **Registrar perfil**. Haga clic en la regla **Registrar perfil** para abrirlo.

![Configuración de Launch](./images/rule2.png)

A continuación, verá los detalles de esta regla. Haga clic en para abrir la acción **Enviar &quot;Evento de registro&quot; a AEP: déclencheur JO**.

![Configuración de Launch](./images/rule3.png)

A continuación, verá que, cuando se active esta acción, se utiliza un elemento de datos específico para definir la estructura de datos XDM. Debe actualizar ese elemento de datos y definir la variable **ID de evento** del evento que configuró en [Ejercicio 7.1](./ex1.md).

![Configuración de Launch](./images/rule4.png)

Ahora necesita actualizar el elemento de datos **XDM - Evento de registro**. Para ello, vaya a **Elementos de datos**. Buscar **XDM - Evento de registro** y haga clic en para abrir ese elemento de datos.

![Configuración de Launch](./images/rule5.png)

Verá esto:

![Configuración de Launch](./images/rule6.png)

Navegar al campo `_experience.campaign.orchestration.eventID`. Elimine el valor actual y pegue su eventID allí.

Como recordatorio, el ID de evento se puede encontrar en Adobe Journey Optimizer en **Configuraciones > Eventos** y encontrará el ID de evento en la carga útil de ejemplo de su evento, que tiene este aspecto: `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

Después de pegar el eventID, la pantalla debería tener este aspecto. A continuación, haga clic en **Guardar** o **Guardar en biblioteca**.

![Configuración de Launch](./images/rule7.png)

Finalmente, debe publicar los cambios. Vaya a **Flujo de publicación** en el menú de la izquierda.

![Configuración de Launch](./images/rule8.png)

Haga clic en **Agregar todos los recursos modificados** y haga clic en **Guardar y crear en desarrollo**.

![Configuración de Launch](./images/rule9.png)

La biblioteca se actualizará y después de 1-2 minutos podrá probar la configuración.

## 7.3.2 Pruebe el Recorrido

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../module0/images/web8.png)

En el **Pantallas** página, haga clic en **Ejecutar**.

![DSN](../module1/images/web2.png)

Verá que su sitio web de demostración se abre. Seleccione la dirección URL y cópiela en el portapapeles.

![DSN](../module0/images/web3.png)

Abra una nueva ventana del explorador incógnito.

![DSN](../module0/images/web4.png)

Pegue la dirección URL del sitio web de la demostración, que copió en el paso anterior. A continuación, se le pedirá que inicie sesión con su Adobe ID.

![DSN](../module0/images/web5.png)

Seleccione su tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../module0/images/web6.png)

Verá su sitio web cargado en una ventana del navegador incógnito. Para cada demostración, tendrá que usar una ventana nueva del explorador incógnito para cargar la URL de su sitio web de demostración.

![DSN](../module0/images/web7.png)

Haga clic en el icono del logotipo de Adobe en la esquina superior izquierda de la pantalla para abrir el Visor de perfiles.

![Demostración](../module2/images/pv1.png)

Consulte el panel Visualizador de perfiles y el perfil del cliente en tiempo real con el **ID de Experience Cloud** como identificador principal para este cliente actualmente desconocido.

![Demostración](../module2/images/pv2.png)

Vaya a la página Registro/Inicio de sesión . Haga clic en **CREAR UNA CUENTA**.

![Demostración](../module2/images/pv9.png)

Complete los detalles y haga clic en **Registro** después de lo cual, se le redirigirá a la página anterior.

![Demostración](../module2/images/pv10.png)

Abra el panel Visor de perfiles y vaya a Perfil del cliente en tiempo real. En el panel Visor de perfiles, debería ver todos los datos personales mostrados, como los identificadores de correo electrónico y teléfono recién agregados.

![Demostración](../module2/images/pv11.png)

1 minuto después de haber creado su cuenta, recibirá el correo electrónico de creación de su cuenta de Adobe Journey Optimizer.

![Configuración de Launch](./images/email.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 7](./journey-orchestration-create-account.md)

[Volver a todos los módulos](../../overview.md)
