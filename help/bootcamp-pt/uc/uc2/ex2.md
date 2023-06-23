---
title: Bootcamp - Journey Optimizer Crea tu evento - Brasil
description: Bootcamp - Journey Optimizer Crea tu evento - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crie seu evento

Iniciar sesión en Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será reorientado para la visualización de la imagen **Inicio** no hay Journey Optimizer. Primeiro, verifique se você está usando sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em Prod e selecione o sandbox na lista. Neste ejemplo, o nome do sandbox é **Bootcamp**. Você estará en visualización da **Inicio** zona protegida de do seu `Bootcamp`.

![ACOP](./images/acoptriglp.png)

No menu à esquerda, role para baixo e clique em **Configuraciones**. Em, grupo no botão **Administrar** abaixo de **Eventos**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos los eventos disponíveis. Clique em **Crear evento** para venir a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar, dê um nome ao seu evento como, por ejemplo: `seuSobrenomeAccountCreationEvent` e adicione uma descripción como, por ejemplo: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em, certifica-se de que **Tipo** está definido como **Unitario** e, para a seleção de **Tipo de ID de evento**, selecione **Sistema generado**.

![ACOP](./images/eventidtype.png)

Una etapa seguinte é a seleção do schema. Um esquema para preparar este ejercicio. Uso del esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Campos**. Agora você deve passar o mouse sobre a seção **Campos** e três ícones pop-up serão exibidos. Clique no ícone **Editar**.

![ACOP](./images/eventpayload.png)

Você va uma janela pop-up de **Campos**, onde você deve selecionar algunos s dos campos que precisamos para personalizar el correo electrónico. Escolheremos outros de perfil, os dados já existe na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Sin objeto `_experienceplatform.demoEnvironment`, certifica-se de selecionar los campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Sin objeto `_experienceplatform.identification.core`, certifica-se de selecionar o campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clique em **Ok** para salvar suas alterações.

![ACOP](./images/saveok.png)

Em, a tela abaixo deve ser exibida. Clique em **Guardar**  mais uma vez para salvar suas alterações..

![ACOP](./images/eventsave.png)

Seu evento agora está e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **Editar evento**. Pasa el ratón sobre **Campos** para ver os 3 ícones outra vez. Clique no ícone **Ver carga útil**.

![ACOP](./images/viewevent.png)

Agora você verá un ejemplo de carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (payload) até `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser publicado à Adobe Experience Platform para acionar a jornada que você construir em um dos próximos exercícios. Lembre-se deste eventID, você pode precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clique em **Ok** e, em, clique em **Cancelar**.

Agora você terminou este ejercicio.

Próxima etapa: [ 2.3 Crie sua mensagem de e-mail](./ex3.md)

[Hoteles cerca de Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos los Módulos](../../overview.md)
