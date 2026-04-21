---
title: Conectar el ACCS a la tienda AEM Sites CS/EDS
description: Conectar el ACCS a la tienda AEM Sites CS/EDS
kt: 5342
doc-type: tutorial
exl-id: 81d826a8-c9f0-4e2a-9107-d6e06a4b8427
source-git-commit: 7e0214226eaee0586d036d46de39c08046d43893
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# 1.5.2 Conexión de ACCS a AEM Sites CS/EDS Storefront

>[!IMPORTANT]
>
>Para completar este ejercicio, debe tener acceso a un AEM Sites y a Assets CS en funcionamiento con el entorno EDS.
>
>Si aún no cuenta con ese entorno, vaya al ejercicio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga las instrucciones allí y tendrá acceso a dicho entorno.

>[!IMPORTANT]
>
>Si ha configurado anteriormente un programa AEM CS con un entorno AEM Sites y Assets CS, es posible que la zona protegida de AEM CS haya estado en hibernación. Dado que la dehibernación de una zona protegida de este tipo tarda de 10 a 15 minutos, sería aconsejable iniciar el proceso de dehibernación ahora para que no tenga que esperar más adelante.

En este ejercicio, vinculará la tienda AEM Sites CS/EDS al servidor ACCS. En este momento, cuando abres tu AEM Sites CS/EDS Storefront y vas a la página de la lista de productos de **Phones**, todavía no ves ningún producto.

Al final de este ejercicio, debería ver los productos que configuró en el ejercicio anterior en la página de la lista de productos **Teléfonos/Relojes/Planes/Entretenimiento** de su tienda AEM Sites CS/EDS Storefront.

![ACCS+AEM Sites](./images/accsaemsites0.png)

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Asegúrese de que está en el entorno correcto, que debe llamarse `--aepImsOrgName--`. Haga clic en **Commerce**.

![ACCS+AEM Sites](./images/accsaemsites1.png)

Haga clic en el icono **información** junto a la instancia de ACCS, que debe llamarse `--aepUserLdap-- - ACCS`.

![ACCS+AEM Sites](./images/accsaemsites2.png)

Entonces debería ver esto. Copie el **extremo de GraphQL**.

![ACCS+AEM Sites](./images/accsaemsites3.png)

Vaya a [https://da.live/app/adobe-commerce/storefront-tools/tools/config-generator/config-generator](https://da.live/app/adobe-commerce/storefront-tools/tools/config-generator/config-generator). Ahora necesita generar un archivo config.json que se utilizará para vincular su tienda AEM Sites CS al servidor ACCS.

En la página **Generador de configuración**, pegue la dirección URL **GraphQL endpoint** que ha copiado.

Haga clic en **Generar**.

![ACCS+AEM Sites](./images/accsaemsites4.png)

Haga clic en **Copiar** para copiar la carga útil JSON completamente generada.

![ACCS+AEM Sites](./images/accsaemsites5.png)

Vaya al repositorio de GitHub que se creó al configurar el entorno de AEM Sites CS/EDS. Ese repositorio se creó en el ejercicio [1.1.2 Configuración de su entorno AEM CS](./../../../modules/asset-mgmt/module2.1/ex3.md){target="_blank"} y debe llamarse **citisignal-aem-accs** o **techinsidersodXX-citisignal-aem-accs** o, en caso de que asista a un curso de formación presencial en vivo, debe llamarse **techinsidersXX-citisignal-aem-accs**.

![ACCS+AEM Sites](./images/accsaemsites6.png)

En el directorio raíz, desplácese hacia abajo y haga clic para abrir el archivo **config.json**.

![ACCS+AEM Sites](./images/accsaemsites7.png)

Haga clic en el icono **Edit**.

![ACCS+AEM Sites](./images/accsaemsites8.png)

Elimine todo el texto actual y reemplácelo pegando la carga útil JSON que copió en la página **Generador de configuración**.

Haga clic en **Confirmar cambios...**.

![ACCS+AEM Sites](./images/accsaemsites9.png)

Haga clic en **Confirmar cambios**.

![ACCS+AEM Sites](./images/accsaemsites10.png)

El archivo **config.json** se ha actualizado. Debería ver los cambios en el sitio web en un par de minutos. La manera de comprobar si los cambios se han realizado correctamente es ir a la página de producto **Teléfonos**. Ahora debería ver **iPhone Air** en la página.

Abra el sitio web usando las direcciones URL **.page** o **.live** y luego vaya a **Teléfonos**. Deberías ver esto.

![ACCS+AEM Sites](./images/accsaemsites11.png)

Vaya a **Relojes**. Deberías ver esto.

![ACCS+AEM Sites](./images/accsaemsites12.png)

Ir a **Planes**. Deberías ver esto.

![ACCS+AEM Sites](./images/accsaemsites13.png)

Vaya a **Entretenimiento**. Deberías ver esto.

![ACCS+AEM Sites](./images/accsaemsites14.png)

Aunque los productos se están mostrando correctamente, aún no hay una imagen disponible para estos productos. En el siguiente ejercicio, se configura el vínculo con AEM Assets CS para imágenes de productos.

Siguiente paso: [Conectar ACCS a AEM Assets CS](./ex3.md){target="_blank"}

Volver a [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
