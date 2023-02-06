---
title: Bootcamp - Journey Optimizer Crear su evento - Brasil
description: Bootcamp - Journey Optimizer Crear su evento - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crimen de evento

Inicio de sesión en Facebook en Adobe Journey Optimizer access a [Adobe Experience Cloud](https://experience.adobe.com). Clique **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redireasí para una visualización **Página principal** sin Journey Optimizer. Primeiro verifique se você está está o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, clique em Prod e selecione o sandbox na lista. Neste exemplo o nome do sandbox é **Bootcamp**. Você estará na visualização da **Página principal** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

No menú à esquerda, rol para baixo e clique em **Configuraciones**. Em seguida, clique no botão **Administrar** abaixo de **Eventos**.

![ACOP](./images/acopmenu.png)

Você para uma visão geral de todos los eventos disponíveis. Clique **Crear evento** para cómplice a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar, dê um nome ao seu evento como, por ejemplo: `yourLastNameAccountCreationEvent` e adicione uma describe ção como, por ejemplo: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certificfique-se de que **Tipo** está definido **Unitario** e, para a seleção de **Tipo de ID de evento**, selecione **Sistema generado**.

![ACOP](./images/eventidtype.png)

Un etapa seguido é un seleção do schema. Um schema foi preparado para este exercício. Uso de esquema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de seleo Schema, você vários campos sendo seleAsentadores na seção **Campos**. Agora você deve passar o mouse sobre un seção **Campos** e três ícones pop-up serão exibidos. Clique no ícone **Editar**.

![ACOP](./images/eventpayload.png)

Você yuma janela pop-up de **Campos**, onde você deve selecionar s dos campos que precisamos personalizar e-mail. Escolheremos outros atributos de posteriormente, utilizando os dados já existentes un Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Sin objeto `_experienceplatform.demoEnvironment`, pcertificfique-se de selecionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Sin objeto `_experienceplatform.identification.core`, certifica-se de seleedico campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clique **Ok** a para salvar suas alterações.

![ACOP](./images/saveok.png)

Em seguida, una tela abaixo deve ser exibida. Clique **Guardar**  mais uma vez para salvar suas alterações..

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para que el abrique es uma vez a tela **Editar evento**. Pasar el ratón sobre **Campos** para ver os 3 ícones outra vez. Clique no ícone **Ver carga útil**.

![ACOP](./images/viewevent.png)

Agora vocvea ê um exemplo da carga útil.
Seu evento tem umID de orquestração único, que você pode encontrar rolando baixo nessa útil carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é que deve ser enviado à Adobe Experience Platform para acionar a una jornada que você irá em dos próximos exercícios. Lembre-se deste eventID, você pode precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clique **Ok** e, em seguida, clique em **Cancelar**.

Agora você terminou este exercício.

Próxima etapa: [ 2.3 Crie sua mensagem de e-mail](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos los Módulos](../../overview.md)
