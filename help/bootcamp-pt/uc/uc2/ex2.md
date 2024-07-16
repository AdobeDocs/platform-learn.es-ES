---
title: Bootcamp - Journey Optimizer Crea tu evento - Brasil
description: Bootcamp - Journey Optimizer Crea tu evento - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 2.2 Crie seu evento

Iniciar sesión en Adobe Journey Optimizer accediendo a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será reorientado para la visualización de **Hogar** en Journey Optimizer. Primeiro, verifique se você está usando sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em Prod e selecione o sandbox na lista. Ejemplo anidado, o nome do sandbox é **Bootcamp**. Você estará en una visualización de **Inicio** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Sin menú a la esquerda, rol para baixo e clique em **Configurations**. Em, clique no botão **Administrar** abaixo de **Eventos**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos los eventos disponíveis. Clique em **Crear evento** para recibir un evento de criar o próprio.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar, dê um nome ao seu evento como, por ejemplo: `seuSobrenomeAccountCreationEvent` e adicione uma descripção como, por ejemplo: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em, certifica-se de que **Type** está definido como **Unitary** e, para a seleção de **Event ID Type**, selecione **System Generated**.

![ACOP](./images/eventidtype.png)

Una etapa seguinte é a seleção do schema. Um esquema para preparar este ejercicio. Usar en esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Campos**. Agora você deve passar o mouse sobre a seção **Campos** e três ícones pop-up serão exibidos. Clique no ícone **Editar**.

![ACOP](./images/eventpayload.png)

Você va uma janela pop-up de **Fields**, onde você deve selecionar algunos s dos campos que precisamos para personalizar el correo electrónico. Escolheremos outros de perfil, os dados já existe na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Sin objeto `_experienceplatform.demoEnvironment`, certifica-se de selecionar los campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

No objeto `_experienceplatform.identification.core`, certificfique-se de selecionar o campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clique em **Ok** para salvar sus alteraciones.

![ACOP](./images/saveok.png)

Em, a tela abaixo deve ser exibida. Clique em **Guardar** mais uma vez para salvar suas alterações..

![ACOP](./images/eventsave.png)

Seu evento agora está e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **Editar evento**. Passe o mouse sobre **Fields** para ver os 3 ícones outra vez. Clique no ícone **Ver carga**.

![ACOP](./images/viewevent.png)

Agora você verá un ejemplo de carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (payload) até a ver `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser publicado à Adobe Experience Platform para acionar a jornada que você construir em um dos próximos exercícios. Lembre-se deste eventID, você pode precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clique em **Ok** e, em, clique em **Cancelar**.

Agora você terminou este ejercicio.

Próxima etapa: [ 2.3 Crie sua mensagem de e-mail](./ex3.md)

[Hoteles cerca de Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos los Módulos](../../overview.md)
