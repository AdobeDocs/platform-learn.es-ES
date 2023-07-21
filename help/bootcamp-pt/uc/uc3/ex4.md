---
title: Bootcamp - Fusión física y digital - Pruebe su recorrido - Brasil
description: Bootcamp - Fusión física y digital - Pruebe su recorrido - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 04e2877f-8672-4584-8204-4489a7025c63
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 3.4 Prueba de la jornada

Para testar sua jornada, você deve usar o eventID criado no exercício 3.2, que deve ser semelhante ao seguinte.

![ACOP](./images/payloadeventID.png)

O eventID é o que precisa ser publicado à Adobe Experience Platform para acionar a jornada. Ejemplo anidado, o eventID é:
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Abra o aplicativo móvel e vá para a inicial. Categoría no disponible de **Configuración**.

![DSN](./images/appsett.png)

Cole seu eventID no campo **EventID de señalización** e clique em **Guardar**.

![DSN](./images/beacon1.png)

Antes de continuar, abra esta página da Web em seu computador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Em, será exibida a tela:

![DSN](./images/screen1.png)

Volver a la página inicial. Clique no ícone do **baliza**.

![DSN](./images/app23.png)

Primeiro, selecione **Señalización de pantalla de Bootcamp** e clique no botão de **entrada** botón. Isso que você simule uma entrada do beacon.

![DSN](./images/app21.png)

Agora confira a tela da loja. Você verá o último producto visualizado a partir de nessa tela em 5 segundos.

![DSN](./images/beacon3.png)

Você também terá recebido sua notificação push.

![DSN](./images/beacon2.png)

Você terminou este ejercicio.

[Hoteles cerca de Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos los Módulos](../../overview.md)
