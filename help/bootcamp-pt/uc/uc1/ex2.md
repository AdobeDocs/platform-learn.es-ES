---
title: Bootcamp - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - UI - España
description: Bootcamp - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - UI - España
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# 1.2 Visualiza tu perfil de cliente en tiempo real - UI

Neste exercício, você irá fazer Iniciar sesión en Adobe Experience Platform e iniciar sesión en un perfil de cliente en tiempo real en la interfaz de usuario.

## História

No Perfil do cliente em tempo real, todos os dados do perfil são exibidos juntamente com os dados do evento, além das associações de. Os dados mostrados podem vir de qualquer lugar, de aplicativos da Adobe e soluções. Essa é a exibição mais da Adobe Experience Platform, o verdadeiro local do sistema de experiência.

## 1.2.1 Uso de una visualización del perfil del cliente en Adobe Experience Platform

Acceder a [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá a página inicial da Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, você precisa selecionar um **espacio aislado**. O nome do sandbox a ser selecionado é Bootcamp. No se puede escribir más **[!UICONTROL Production Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropiado, você a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingesta de datos](./images/sb1.png)

No hay menú a la sombra, accede a **Perfiles** y **Examinar**.

![Perfil del cliente](./images/homemenu.png)

No pain Visualizador de perfil no seu site, você pode encontrar a visão geral da identidade. Cada identificador está a um namespace.

![Perfil del cliente](./images/identities.png)

No pain Visualizador de perfil, agora você pode ver uma identidade semelhante a seguinte:

| Área de nombres | Identidad |
|:-------------:| :---------------:|
| ID DEL Experience Cloud (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform, todos os IDs são igualmente importantes. Anteriormente, o ECID era o ID mais importante no da Adobe e todos os outros IDs estavam vinculado ao ECID em uma relação jerárquica. Com a Adobe Experience Platform, isso mudou e cada ID pode ser identificador um identificador primário.

, o identificador primário dependo do do contexto. Ver você perguntar ao seu Call Center: **Cual é o ID mais importante?** Eles provavelmente responderão: **o número de teléfono!** Mas se você perguntar à sua equipe de CRM, eles responderão: **o endereço de e-mail!** A Adobe Experience Platform entende essa complexidade e gerencia isso para você. Cada aplicativo, seja um aplicativo da Adobe ou não, se com a Adobe Experience Platform referindo-se ao ID que consideram principal. E simplesmente funciona.

Para o campo **Área de nombres de identidad**, selecione **ECID** e para o campo **Valor de identidad** insira o ECID que você pode encontrar no pain Visualizador de perfil do site do Bootcamp. Clique em **Vista**. Você va a seu perfil na lista. Haz clic en **ID de perfil** para abrir tu perfil.

![Perfil del cliente](./images/popupecid.png)

Agora você tem uma visão geral de some s **de perfil** importantes do seu perfil de cliente.

![Perfil del cliente](./images/profile.png)

Entradas de cada evento de experiência ligada a perfil: **Events**, onde você pode ver as entradas de cada evento de experiência ligada ao seu Perfil.

![Perfil del cliente](./images/profileee.png)

De forma automática, acceda a la opción de menú **Abono a segmentos**. Agora você todos os que se calificam para este perfil.

![Perfil del cliente](./images/profileseg.png)

Agora vamos criar um novo, que es la primera vez que te gusta personalizar una experiencia de cliente para un cliente anônimo ou conhecido.

Próxima etapa: [1.3 Crie um... - Interfaz de usuario](./ex3.md)

[Hoteles cerca de Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos los Módulos](../../overview.md)
