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
source-wordcount: '835'
ht-degree: 1%

---

# 3.3 Crie sua jornada e notificação push

Neste exercício, você a jornada e a mensagem que precisa ser accionada quando alguém inserir uma sinalização (beacon) usando o aplicativo móvel.

Iniciar sesión en Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será reorientado para la visualización de la imagen **Inicio** no hay Journey Optimizer. Primeiro, verifique se você está usando sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecione o sandbox na lista. Neste ejemplo, o nome do sandbox é **Bootcamp**. Você estará en visualización da **Inicio**  zona protegida de do seu `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Crie a sua jornada

Sin menú a la esquerda, clique em **Recorridos**. Em, grupo em **Crear Recorrido** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você va uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Sin ejercicio anterior, você criou um novo **Evento**. Você nomeou o evento `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de jornada. Sua jornada agora deve ser semelhante ao seguinte. Clique em **Ok** para salvar sus alteraciones.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma ação **Push**. Para o lado esquerdo da tela para **Acciones**, seleccione una acción **Push** e arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

a **Categoría** como **Marketing** e selecione um push surface que permite enviar notificaciones push. Nesse caso, a superfície push a ser selecionada é **mmeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

Clique em **Editar contenido**.

![ACOP](./images/emptymsg.png)

Em, a tela abaixo será exibida:

![ACOP](./images/emailmsglist.png)

Vamos a definir o conteúdo da notificación push.

Clique no campo de texto **Título**.

![Journey Optimizer](./images/msg5.png)

Área de texto, comece **Olá**. Clique no ícone de personalización.

![Journey Optimizer](./images/msg6.png)

Agora você precisa trazer o token de personalización para o campo **Nombre** que está armazenado em `profile.person.name.firstName`. Sin menú a la esquerda, selecione **Atributos de perfil**, role para baixo/navegación para encontrar o elemento **Persona** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para añadir a campo à tela. Clique em **Guardar**.

![Journey Optimizer](./images/msg7.png)

Então, você irá retornar para esta tela. Clique no ícone de personação ao lado do campo **Cuerpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em, grupo em  **Atributos contextuales** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Eventos**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Contexto del lugar**.

![ACOP](./images/jomsg6.png)

Clique em **Interacción del PDI**.

![ACOP](./images/jomsg7.png)

Clique em **Detalles del PDI**.

![ACOP](./images/jomsg8.png)

Clique no **+** icono no **Nombre del PDI**.
Em, no seguinte será exibido. Clique em **Guardar**.

![ACOP](./images/jomsg9.png)

Sua mensagem agora está pronta. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

Clique em **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você deve adicionar uma ação  **sendMessageToScreen**. Para o lado esquerdo da tela para **Acciones**, seleccione una acción **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em, el você va a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no **Extremo** usado pela exibição na loja. A ação **sendMessageToScreen** Ver todos los detalles de la versión en inglés de sejam. Você pode variáveis rolando para baixo até ver **Parámetros de acción**.

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

Para definir los valores, clique no ícone **Editar**.

![ACOP](./images/jomsg17.png)

Em, selecione **Modo avanzado**.

![ACOP](./images/jomsg18.png)

Em, el cole o el valor com base na tabela acima. Clique em **Ok**.

![ACOP](./images/jomsg19.png)

Repita este proceso para agregar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Lembre-se de substituir  `yourLastName` pelo seu sobrenome.

O resultado final deve ser semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

Role para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Aún necesita darle un Nombre a su recorrido. Para ello, haga clic en el icono **Propiedades** en la parte superior derecha de la pantalla.

![ACOP](./images/journeyname.png)

Você pode inserir o nome da jornada aquí. En su lugar, utilice `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar sus alteraciones.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você va uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este ejercicio.

Próxima etapa: [3.4 Prueba de la jornada](./ex4.md)

[Hoteles cerca de Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos los Módulos](../../overview.md)
