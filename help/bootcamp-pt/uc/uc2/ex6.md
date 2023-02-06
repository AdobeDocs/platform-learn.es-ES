---
title: Bootcamp - Personalización en el centro de llamadas - Brasil
description: Bootcamp - Personalización en el centro de llamadas - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# 2.6 Personalización sin centro de llamadas

Como ya se ha comentado varias veces durante el bootcamp, la personalización de la experiencia del cliente es algo que debería suceder de forma omnicanal. Un centro de llamadas suele estar bastante desconectado del resto del recorrido del cliente y a menudo provoca experiencias frustrantes para el cliente, pero no es necesario. Veamos un ejemplo de cómo el centro de llamadas puede conectarse fácilmente a Adobe Experience Platform en tiempo real.

## Fluxe da jornada do cliente

No exercício anterior, o aplicativo móvel, você compromeu produto clicando no botão **Buy**.

![DSN](./images/app20.png)

Vamos supor que você tenha uma pergunta sobre o status do seu pedido o que você faria? Normalmente, você ligaria para o call center.

Antes de ligar para o call center, você precisa sable seu **ID de fidelidad**. Você pode encontrar seu ID de fidelidade no Visualizador de Perfil do site.

![DSN](./images/cc1.png)

Nesse caso, o **ID de fidelidad** é **5863105**. Como parte de nossa implação do personalizada de call center no ambiente de demostração, você deve adition um prefixo ao seu **ID de fidelidad**. O prefixo é **11373**, portanto o ID de fidelidade a ser usado neste exemplo é **11373 5863105**.

Vamos fazer es agora. Use seu telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Será solicitado que você insira seu ID de fidelidade, seguidas **#**. Digite seu ID de fidelidade.

![DSN](./images/cc3.png)

Você ouvirá **Hola, seu nome**, nome. Esse nome é retirado do Perfil do Cliente em tempo real na Adobe Experience Platform. Você ellos 3 escolas. Presa o número **1**, **Estado del pedido**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu pedido, você terá a opção de presinfluyente **1** para voltar ao menú principal ou prespuesta 2. Presa **2**.

![DSN](./images/cc5.png)

Em seguida, Seré solicitado que você avalie sua experiência de call center, selefecum número entre 1 e 5 sendo 1 baixo e 5 alto. Facha un sua escolha.

![DSN](./images/cc6.png)

Sua chamada para llamar al centro sera eninvolucrada.

Aceses [Adobe Experience Platform](https://experience.adobe.com/platform). Inicio de sesión en Depois de fazer, você irá acessar a post inicial da Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

precisa selecionar um de continuar, você **entorno limitado**. O nome do sandbox a ser selector é é ``Bootcamp``. É possível fazer isso clicando no texto **[!UICONTROL Producción]** na linha azul na parte superior da tela. Depoes de seleción o [!UICONTROL entorno limitado] apropiado, você verá a tela mudando e agora você está em seu [!UICONTROL entorno limitado] dedicado.

![Ingesta de datos](./images/sb1.png)

No menú à esquerda, acesse **Perfiles** e **Examinar**.

![Perfil del cliente](./images/homemenu.png)

Selecione o **Área de nombres de identidad** **Correo electrónico** e insira o endereço e-mail do seu de cliente. Clique **Ver**. Clique para abrio seu.

![DSN](./images/cc7.png)

Você aparecerá de memoria de cliente novamente. Aceses **Eventos**.

![DSN](./images/cc8.png)

Em eventos, você 2 eventos com um eventType de **callCenter**. O primeiro evento é o resultado sua resposta à pergunta Avalie o seu n **Valore la satisfacción de las llamadas**.

![DSN](./images/cc9.png)

Rol um pouco para baixo y verá o evento que foi quando você selecionou a opção o verificar **Estado del pedido**.

![DSN](./images/cc10.png)

Aceses **Pertenencia a segmentos**. Agora você que 2 segmentos se qualification ficam em seu, em tempo real, com base nas interações você teve por meio do call center. Essas associated ações de segmento podem e devem ser usadas para impactar qual comunicação e personação acontece em qualquer outro canal.

![DSN](./images/cc11.png)

Você terminou este exercício.

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos los Módulos](../../overview.md)
