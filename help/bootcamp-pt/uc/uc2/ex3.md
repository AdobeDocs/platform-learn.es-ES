---
title: Bootcamp - Journey Optimizer Cree su recorrido y mensaje de correo electrónico - Brasil
description: Bootcamp - Journey Optimizer Cree su recorrido y mensaje de correo electrónico - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# 2.3 Crie sua jornada e mensagem de e-mail

Neste exercício, você a jornada que precisa ser accionada quando alguém criar uma conta no site de demostração.

Iniciar sesión en Adobe Journey Optimizer accediendo a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será reorientado para la visualización de **Hogar** en Journey Optimizer. Primeiro, verifique se você está usando sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecione o sandbox na lista. Ejemplo anidado, o nome do sandbox é **Bootcamp**. Você estará en una visualización de **Inicio** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Crie a sua jornada

No hay menú a la esquerda, grupo en **Recorridos**. Em, clique em **Crear Recorrido** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você va uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Sin ejercicio anterior, você criou um novo **Evento**. Você nomeou o evento `seuSobrenomeAccountCreationEvent` e substituiu `seuSobrenome` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de Jornada. Sua Jornada agora deve ser semelhante ao seguinte:

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma etapa curta de **Espera**. Vá para o lado esquerdo da tela até a seção **Orquestación** para encontrar isso. Você de perfil y precisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

Sua jornada agora deve ser semelhante ao seguinte. No lado direito da tela você configure o tempo de espera. como 1 minuto. Isso da bastante tempo para que os do perfil estejam disponíveis após o disparo do evento.

![ACOP](./images/journeywait1.png)

Clique em **Ok** para salvar suas alterações.

Como terceira etapa da jornada, você deve adicionar uma ação **Correo electrónico**. Vá para o lado esquerdo da tela para **Actions**, selecione a ação **Email** e arraste e solte a ação no segundo nó da sua jornada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

una **Categoría** como **Marketing** e selecione uma **superficie de correo electrónico** que permita o envio de correo electrónico. Nesse caso, a **superficie de correo electrónico** a ser selecionada é E-mail. Certifique-se de que as caixas de seleção **Clics en el correo electrónico** e **email opens** estejam marcadas.

![ACOP](./images/journeyactions1.png)

Una próxima etapa y criar su mensaje. Para isso, grupo **Editar contenido**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Crie a sua mensagem

Para criar sua mensagem, grupo en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Clique no campo de texto **Línea de asunto**.

![Journey Optimizer](./images/msg5.png)

Área de texto, comece **Olá**

![Journey Optimizer](./images/msg6.png)

A linha de assunto ainda não está pronta. Em, você precisa trazer o token de personalización para o **Nombre** que está armazenado em `profile.person.name.firstName`. No menu à esquerda, role para baixo para encontrar o elemento **Person** e clique na seta para ver mais campos

![Journey Optimizer](./images/msg7.png)

Agora encontre o elemento **Full name** e clique na seta para ver mais campos.

![Journey Optimizer](./images/msg8.png)

Por fim, localiza o campo **Nombre** e clique no hay símbolo **+** ao lado dele. Você verá o token de personalización no aparece en el campo de texto.

![Journey Optimizer](./images/msg9.png)

¡Em, adicione o texto, **agradecemos a sua inscrição!**. Haz clic en **Guardar**.

![Journey Optimizer](./images/msg10.png)

Então, você irá retornar para esta tela. Clique em **Email Designer** para criar o conteúdo e-mail.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, se ha solicitado que você forneça o conteúdo do e-mail através de 3 métodos diferentes:

- **Diseño desde cero**: Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os componentes de conteúdo para criar visualmente o conteúdo do e-mail.
- **Codifique usted mismo**: Crie seu próprio modelo de e-mail codificando usando HTML
- **HTML de importación**: HTML de importación modelo existente, que você poderá editar.

Clique em **HTML de importación**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**, que você pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip). Clique em.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de correo electrónico padrão:

![Journey Optimizer](./images/msg14.png)

Vamos a enviar un correo electrónico. Clique ao lado do texto **Olá** e, em, clique no ícone **Agregar Personalization**.

![Journey Optimizer](./images/msg35.png)

Em, você precisa trazer o token de personalización **Nombre** que está armazenado en `profile.person.name.firstName`. No hay menú, localice o elemento **Person**, faça uma busca detalles no elemento **Full Name** e clique no ícone **+** para adicionar o campo **First Name** ao editor.

Haz clic en **Guardar**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalización foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Haz clic en **Guardar** para guardar tu mensaje.

![Journey Optimizer](./images/msg55.png)

Retorne para o pain de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você concluiu a criação do seu e-mail de cadastro. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

Clique em **Aceptar**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publicación de la jornada

Você ainda precisa dar Nome à sua jornada. Você pode fazer isso clicando no ícone **Propiedades** no canto superior direito da tela.

![ACOP](./images/journeyname.png)

Você pode fazer isso clicando no item clicar no item &quot;Nombre&quot; e inserindo o seguinte nome `yourLastName - Account Creation Journey`. Clique em **OK** para guardar como mudanças.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você va uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Você terminou este ejercicio.

Próxima etapa: [2.4 Prueba sua jornada](./ex4.md)

[Hoteles cerca de Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos los Módulos](../../overview.md)
