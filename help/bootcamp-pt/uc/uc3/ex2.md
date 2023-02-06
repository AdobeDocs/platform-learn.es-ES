---
title: Bootcamp - Fusión física y digital - Journey Optimizer Crear su evento - Brasil
description: Bootcamp - Fusión física y digital - Journey Optimizer Crear su evento - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 3.2 Crimen de evento

Inicio de sesión en Facebook en Adobe Journey Optimizer access a [Adobe Experience Cloud]. Clique **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será rediredeterminado para a **Página principal** sin Journey Optimizer. Primeiro verifique se você está está o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecione o sandbox na lista. Neste exemplo o nome do sandbox é **Bootcamp2**. Você estará na visualização da **Página principal** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

No menú à esquerda, rol para baixo e clique em **Configuraciones**. Em seguida, clique no botão **Administrar** em Eventos.

![ACOP](./images/acopmenu.png)

Você para uma visão geral de todos los eventos disponíveis. Clique **Crear evento** para cómplice a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

Em primeiro lugar, dê um nome ao seu evento como, por ejemplo: `yourLastNameBeaconEntryEvent` e adicione uma describe ção como, por ejemplo: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certificfique-se de que **Tipo** está definido **Unitario** e, para a seleção de **Tipo de ID de evento**, selecione **Sistema generado**.

![ACOP](./images/eventidtype.png)

Un etapa seguido é un seleção do schema. Um schema foi preparado para este exercício. Uso de esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de seleo Schema, você vários campos sendo seleAsentadores na seção **Campos**. Agora você deve passar o mouse sobre un seção **Campos** e três ícones pop-up serão exibidos. Clique no ícone de **Editar**.

![ACOP](./images/eventpayload.png)

Você yuma janela pop-up de **Campos**, onde você deve selecionar s dos campos que precisamos personalizar una jornada. Escolheremos outros atributos de posteriormente, utilizando os dados já existentes na Adobe Experience Platform

![ACOP](./images/eventfields.png)

Función para baixo até ver to objeto `Place context` e marque a caixa de seleção. Com es, todo contexto da localização do cliente disponibilidad para una jornada. Clique **Ok** para salvar suas alterações.

![ACOP](./images/eventpayloadbr.png)

Em seguida, você devolverá a una tela abaixo. Clique **Guardar** mais uma vez para salvar suas alterações.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para la protección de la información **Editar evento** mais uma vez. Pasar el ratón sobre **Campos** para ver os 3 íconos. Clique no ícone **Ver**.

![ACOP](./images/viewevent.png)

Agora vocvea ê um exemplo da carga útil.
Seu evento tem umID de orquestração único, que você pode encontrar rolando baixo nessa utilidad útil visual `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é que deve ser enviado à Adobe Experience Platform para acionar a una jornada que você irá em dos próximos exercícios. Lembre-se deste eventID, você pode precisar dele posteriormente.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Clique **Ok** e, em seguida, clique em **Cancelar**.

Você terminou este exercício.

Próxima etapa: [3.3 Criar durante la jornada e notificação push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos los Módulos](../../overview.md)
