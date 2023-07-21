---
title: Bootcamp - Personalización en el centro de llamadas - Brasil
description: Bootcamp - Personalización en el centro de llamadas - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 7acf778b-042f-4deb-9406-ddcf63daacda
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 2.6 Personalización sin centro de llamadas

En este artículo se explica cómo hacer un seguimiento de la experiencia del cliente que se ha convertido en un referente de maneira omnicanal. Um call center geralmente é bastante desconectado do lista da jornada do cliente e isso pode, com frequência, levar a experiências frustrantes do cliente, mas não precisa ser assim. Vamos mostrar un ejemplo de como o call center pode ser facilmente conectado a Adobe Experience Platform, em tempo real.

## Fluxo da jornada do cliente

Sin ejercicio anterior, usando o aplicativo móvel, você compromiso um produto clicando no botão **Buy**.

![DSN](./images/app20.png)

Vamos a apoyar que você tenha uma pergunta sobre o status do seu pedido, o que você faria? , você ligaria para o centro de llamadas.

Antes de ligar para o call center, você precisa saber seu **ID de fidelización**. Você pode encontrar seu ID de fidelidade en Visualizador de Perfil do site.

![DSN](./images/cc1.png)

Nesse caso, o **ID de fidelización** é **5863105**. Como parte de nossa implementação personalizada do recurso de call center no ambiente de demostração, você deve adicionar um prefixo ao seu **ID de fidelización**. O prefijo é **11373**, portanto, o ID de fidelidade a ser usado neste ejemplo **11373 5863105**.

Vamos fazer es tan ágora. Usar seu telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

que você insira seu ID de fidelidade, seguido de **#**. Digite seu ID de fidelidade.

![DSN](./images/cc3.png)

Você ouvirá **Hola, soy yo**. Esse nome é do Perfil do Cliente em tempo real na Adobe Experience Platform. Você tem 3 escolhas. Presión o número **1**, **Estado del pedido**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu pedido, você terá a opção de pressisión **1** para voltar ao menú principal ou pressionar 2. Presión **2**.

![DSN](./images/cc5.png)

Em, se ha solicitado que você avalie sua experiência de call center, seleccionar el número entre 1 e 5, sendo 1 baixo e 5 alto. Faça a sua escolha.

![DSN](./images/cc6.png)

Sua chamada para o call center será encerrada.

Acceso [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá a página inicial da Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, você precisa selecionar um **espacio aislado**. O nome do sandbox a ser selecionado é ``Bootcamp``. Posible fazer es tan clicando no texto **[!UICONTROL Producción de producción]** na linha azul na parte superior da tela. Depois de selecionar o [!UICONTROL espacio aislado] apropiado, você va a tela mudando e agora você está em seu [!UICONTROL espacio aislado] dedicado.

![Ingesta de datos](./images/sb1.png)

Sin menú a la esquerda, acceso **Perfiles** e **Examinar**.

![Perfil del cliente](./images/homemenu.png)

Selecione o **Área de nombres de identidad** **Correo electrónico** e insira o endereço de e-mail do seu perfil de cliente. Clique em **Ver**. Clique para abrir su perfil.

![DSN](./images/cc7.png)

Você va a seu perfil de cliente novamente. Acceso **Eventos**.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **callCenter**. O primeiro evento é o resultado da sua resposta à pergunta **Valore la satisfacción de la llamada** (avalie seu chamada).

![DSN](./images/cc9.png)

Role um pouco para baixo e você va a evento que foi quando você selecionou a opção de o **Estado del pedido**.

![DSN](./images/cc10.png)

Acceso **Abono de segmentos**. Agora você que 2 se calificam em seu perfil, em tempo real, com base nas interações que você teve por meio do call center. Essas associações de podem e devem ser usadas para impactar qual comunicação e personação acontece em qualquer outro canal.

![DSN](./images/cc11.png)

Você terminou este ejercicio.

[Hoteles cerca de Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos los Módulos](../../overview.md)
