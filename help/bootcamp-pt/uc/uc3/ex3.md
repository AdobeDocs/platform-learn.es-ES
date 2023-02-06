---
title: Bootcamp - Fusión física y digital - Journey Optimizer Crear su recorrido y push - Brazilnotification
description: Bootcamp - Fusión física y digital - Journey Optimizer Crear su recorrido y push - Brazilnotification
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 2%

---

# 3.3 Criar durante la jornada e notificação push

Neste exercício, você irá configurar una jornada e a mensagem que ser acionada alguém inserir ma sinalização (baliza) quo aplicativo móvel.

Inicio de sesión en Facebook en Adobe Journey Optimizer access a [Adobe Experience Cloud](https://experience.adobe.com). Clique **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redireasí para una visualización **Página principal** sin Journey Optimizer. Primeiro verifique se você está está o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecione o sandbox na lista. Neste exemplo o nome do sandbox é **Bootcamp**. Você estará na visualização da **Página principal**  do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Criar a una superjornada

No menú à esquerda, clique em **Recorridos**. Em seguida, clique em **Crear Recorrido** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você será uma tela de vana jornada.

![ACOP](./images/journeyempty.png)

No exercício anterior, você criou um novo **Evento**. Você nomeou o evento `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer es indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu, de evento, organiza e solte o evento na tela de jornada completa. Sua jornada agora deve ser semelhante ao seguinte. Clique **Ok** para salvar suas alterações.

![ACOP](./images/journeyevent.png)

Como segunda etapa jornada, você deve adiuma ação **Push**. Vá para o lado esquerdo **Acciones**, selecione a ação **Push** e arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

Defina a **Categoría** como **Marketing** e selecione empuja a las autoridades para que cumplan con las notificaciones. Nesse caso, un superfície empuja a un ser selecionada **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Criar a sua mensagem

Clique **Editar contenido**.

![ACOP](./images/emptymsg.png)

Em seguida, una tela abaixo será exbida:

![ACOP](./images/emailmsglist.png)

Vamos definir o conteúdo da notificação push.

Clique no campo de texto **Título**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, orden de inclusión **Olá**. Clique no ícone de personação.

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o token de personação para o campo **Nombre** que está armazencadem `profile.person.name.firstName`. No hay menú a esquerda, selecione **Atributos de perfil**, función para baixo/navegación para encontrar o elemento **Persona** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar o campo à tela. Clique **Guardar**.

![Journey Optimizer](./images/msg7.png)

Então, você irá retornar para esta tela. Clique no ícone de personação ao lado do campo **Cuerpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, clique em  **Atributos contextuales** y luego **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique **Eventos**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que deve ser semelhante ao seguía: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique **Contexto del lugar**.

![ACOP](./images/jomsg6.png)

Clique **Interacción de puntos de interés**.

![ACOP](./images/jomsg7.png)

Clique **Detalle del punto de interés**.

![ACOP](./images/jomsg8.png)

Clique no **+** icono no **Nombre de punto de interés**.
Em seguida, o seguinte será exibido. Clique **Guardar**.

![ACOP](./images/jomsg9.png)

Sua mensagem agora está pronta. Clique na seta no canto superior esquerdo para tornar à sua jornada.

![ACOP](./images/jomsg11.png)

Clique **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você deve adiuma ação  **sendMessageToScreen** acción. Vá para o lado esquerdo **Acciones**, selecione a ação **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no ponto de extremidade usado pela exibição na loja. A ação **sendMessageToScreen** espera que múlti plas variáveis sejam definidas. Você pode visualizar essas variáveis rolando para baixo até ver **Parámetros de acción**.

![ACOP](./images/jomsg16.png)

Agora você precisa definir os para cada parâmetro de ação. Siga tabela para entender quais são necesarios ários e onde.

| Parámetro | valor |
|:-------------:| :---------------:|
| ENTREGA | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOMBRE | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

Para definir dice: **Editar**.

![ACOP](./images/jomsg17.png)

Em seguida, selecione **Modo avanzado**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clique **Ok**.

![ACOP](./images/jomsg19.png)

Repita se processo para adiita para campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Lembre-se-substituir  `yourLastName` pelo seu sobrenome.

O resultado deve ser semelhante ao seguenció:

![ACOP](./images/jomsg20.png)

Rol para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Aún necesita darle un Nombre a su recorrido. Para ello, haga clic en el botón **Propiedades** en la parte superior derecha de la pantalla.

![ACOP](./images/journeyname.png)

Você pode inserir en nome da durante la jornada. En su lugar, utilice `yourLastName - Beacon Entry Journey`. Clique **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você podo publicar sua jornada **Publicación**.

![ACOP](./images/publishjourney.png)

Clique **Publicación** novamente.

![ACOP](./images/publish1.png)

Você uma barra de confirmación verde informando que sua agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este exercício.

Próxima etapa: [3.4 Sesión de prueba](./ex4.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos los Módulos](../../overview.md)
