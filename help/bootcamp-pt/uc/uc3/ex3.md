---
title: Bootcamp - Fusión física y digital - Journey Optimizer Cree su recorrido y empuje - Brazilnotification
description: Bootcamp - Fusión física y digital - Journey Optimizer Cree su recorrido y empuje - Brazilnotification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# 3.3 Crie sua jornada e notificação push

Neste exercício, você a jornada e a mensagem que precisa ser accionada quando alguém inserir uma sinalização (beacon) usando o aplicativo móvel.

Iniciar sesión en Adobe Journey Optimizer accediendo a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será reorientado para la visualización de **Hogar** en Journey Optimizer. Primeiro, verifique se você está usando sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecione o sandbox na lista. Ejemplo anidado, o nome do sandbox é **Bootcamp**. Você estará en una visualización de **Inicio** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Crie a sua jornada

No hay menú a la esquerda, grupo en **Recorridos**. Em, clique em **Crear Recorrido** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você va uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Sin ejercicio anterior, você criou um novo **Evento**. Você nomeou o evento `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de jornada. Sua jornada agora deve ser semelhante ao seguinte. Clique em **Ok** para salvar suas alterações.

![ACOP](./images/journeyevent.png)

Como segunda etapa de la jornada, você deve adicionar uma ação **Push**. Vá para o lado esquerdo da tela para **Actions**, selecione a ação **Push** e arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

una superficie de inserción de **Category** como **Marketing** e selecione um que permite enviar notificaciones push. Nesse caso, a superfície push a ser selecionado é **meeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

Haga clic en **Editar contenido**.

![ACOP](./images/emptymsg.png)

Em, a tela abaixo será exibida:

![ACOP](./images/emailmsglist.png)

Vamos a definir o conteúdo da notificación push.

Clique no campo de texto **Title**.

![Journey Optimizer](./images/msg5.png)

Área de texto, comece **Olá**. Clique no ícone de personalización.

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o token de personalización para o campo **Nombre** que está armazenado em `profile.person.name.firstName`. No menu à esquerda, selecione **Atributos de perfil**, role para baixo/navegación para encontrar o elemento **Person** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar a campo à tela. Haz clic en **Guardar**.

![Journey Optimizer](./images/msg7.png)

Então, você irá retornar para esta tela. Clique no ícone de personalização ao lado do campo **Cuerpo**.

![Journey Optimizer](./images/msg11.png)

Área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em, grupo **Atributos contextuales** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Haga clic en **Eventos**.

![ACOP](./images/jomsg4.png)

No te pierdas el evento, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Contexto del lugar**.

![ACOP](./images/jomsg6.png)

Clique em **Interacción POI**.

![ACOP](./images/jomsg7.png)

Clique em **Detalle del punto de interés**.

![ACOP](./images/jomsg8.png)

Clique no **+** icono no **Nombre POI**.
Em, no seguinte será exibido. Haz clic en **Guardar**.

![ACOP](./images/jomsg9.png)

Sua mensagem agora está pronta. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

Clique em **Aceptar**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você deve adicionar uma ação **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Actions**, selecione a ação **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em, el você va a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá a publicar uma mensagem no **Endpoint** usado pela exibição na loja. Una ação **sendMessageToScreen** espera que se multiplas variáveis sejam (mensaje a pantalla) que se puede mostrar como se muestra a continuación. Você pode como variáveis rolando para baixo até ver **Parámetros de acción**.

![ACOP](./images/jomsg16.png)

Agora você precisa definir los valores para cada parâmetro de ação. Siga esta tabela para entender los valores necesarios y el nodo.

| Parámetro | valor |
|:-------------:| :---------------:|
| ENVÍO | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOMBRE | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| ZONA PROTEGIDA | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para definir los valores, haga clic en **Editar**.

![ACOP](./images/jomsg17.png)

Em, seleccione **Modo avanzado**.

![ACOP](./images/jomsg18.png)

Em, el cole o el valor com base na tabela acima. Clique em **Aceptar**.

![ACOP](./images/jomsg19.png)

Repita este proceso para agregar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Lembre-se de substituir `yourLastName` pelo seu sobrenome.

O resultado final deve ser semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

Rol para cima y grupo **Ok**.

![ACOP](./images/jomsg21.png)

Aún necesita darle un Nombre a su recorrido. Para ello, haga clic en el icono **Propiedades** en la parte superior derecha de la pantalla.

![ACOP](./images/journeyname.png)

Você pode inserir o nome da jornada aquí. Usar `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você va uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este ejercicio.

Próxima etapa: [3.4 Prueba sua jornada](./ex4.md)

[Hoteles cerca de Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos los Módulos](../../overview.md)
