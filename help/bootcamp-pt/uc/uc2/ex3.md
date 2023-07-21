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
source-wordcount: '934'
ht-degree: 3%

---

# 2.3 Crie sua jornada e mensagem de e-mail

Neste exercício, você a jornada que precisa ser accionada quando alguém criar uma conta no site de demostração.

Iniciar sesión en Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será reorientado para la visualización de la imagen **Inicio**  no hay Journey Optimizer. Primeiro, verifique se você está usando sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selecione o sandbox na lista. Neste ejemplo, o nome do sandbox é **Bootcamp**. Você estará en visualización da **Inicio** zona protegida de do seu `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Crie a sua jornada

Sin menú a la esquerda, clique em **Recorridos**. Em, grupo em **Crear Recorrido** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você va uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Sin ejercicio anterior, você criou um novo **Evento**. Você nomeou o evento `seuSobrenomeAccountCreationEvent` e substituiu `seuSobrenome` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de Jornada. Sua Jornada agora deve ser semelhante ao seguinte:

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma etapa curta de **Esperar**. Vá para o lado esquerdo da tela até a seção **Orquestación** para encontrar a isso. Você de perfil y precisará garantir que eles sejam preenchidos no Perfil do Cliente em tempo real.

![ACOP](./images/journeywait.png)

Sua jornada agora deve ser semelhante ao seguinte. No lado direito da tela você configure o tempo de espera. como 1 minuto. Isso da bastante tempo para que os do perfil estejam disponíveis após o disparo do evento.

![ACOP](./images/journeywait1.png)

Clique em **Ok** para salvar sus alteraciones.

Como terceira etapa da jornada, você deve adicionar uma ação **Correo electrónico**. Para o lado esquerdo da tela para **Acciones**, seleccione una acción **Correo electrónico** e arraste e solte a ação no segundo nó da sua jornada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

a **Categoría** como **Marketing** e selecione uma **superficie de correo electrónico** que permite envio de e-mail. Nesse caso, a **superficie de correo electrónico** a ser selecionada é E-mail. Certifique-se de que as caixas de seleção **Clics en el correo electrónico** e **aperturas de correo electrónico** estejam marcadas.

![ACOP](./images/journeyactions1.png)

Una próxima etapa y criar su mensaje. Para isso, clique em **Editar contenido**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Crie a sua mensagem

Para criar sua mensagem, grupo em **Editar contenido**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Clique no campo de texto **Línea de asunto**.

![Journey Optimizer](./images/msg5.png)

Área de texto, comece **Olá**

![Journey Optimizer](./images/msg6.png)

A linha de assunto ainda não está pronta. Em, você precisa trazer o token de personalización para o **Nombre** que está armazenado em `profile.person.name.firstName`. No menu à esquerda, role para baixo para encontrar o elemento **Persona** e clique na seta para ver mais campos

![Journey Optimizer](./images/msg7.png)

Ágora encontre o elemento **Nombre completo** e clique na seta para ver mais campos.

![Journey Optimizer](./images/msg8.png)

Por fim, localize o campo **Nombre** e clique no hay similitud **+**  ao lado dele. Você verá o token de personalización no aparece en el campo de texto.

![Journey Optimizer](./images/msg9.png)

Em, adicione o texto, **agradecemos a sua inscrição!**. Clique em **Guardar**.

![Journey Optimizer](./images/msg10.png)

Então, você irá retornar para esta tela. Clique em **Diseñador de correo electrónico**  para criar o conteúdo do e-mail.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, se ha solicitado que você forneça o conteúdo do e-mail através de 3 métodos diferentes:

- **Diseñe desde cero**: Comece com uma tela em branco e use o editor WYSIWYG para arrastar e soltar a estrutura e os componentes de conteúdo para criar visualmente o conteúdo e-mail.
- **Codifique su propio código**: Crie seu próprio modelo de e-mail codificando usando HTML
- **Importar HTML**: Importador um modelo HTML existente, que você poderá editar.

Clique em **Importar HTML**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**, que você pode baixa [aquí](../../assets/html/mailtemplatebootcamp.html.zip). Clique em.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de correo electrónico padrão:

![Journey Optimizer](./images/msg14.png)

Vamos a enviar un correo electrónico. Clique ao lado do texto **Olá** e, em, clique no ícone **Añadir personalización**.

![Journey Optimizer](./images/msg35.png)

Em, você precisa trazer o token de personalización **Nombre** que está armazenado em `profile.person.name.firstName`. Sin menú, localizar o elemento **Persona**, faça uma busca detalle no elemento **Nombre completo** e clique no ícone **+** para añadir a campo **Nombre** editor de ao.

Clique em **Guardar**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como o campo de personalización foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clique em **Guardar** para salvar a su mensaje.

![Journey Optimizer](./images/msg55.png)

Retorne para o pain de mensagens clicando na seta ao lado do texto da linha de assunto no canto superior esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você concluiu a criação do seu e-mail de cadastro. Clique na seta no canto superior esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

Clique em **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publicación de la jornada

Você ainda precisa dar Nome à sua jornada. Você pode fazer isso clicando no ícone **Propiedades** no canto superior direito da tela.

![ACOP](./images/journeyname.png)

Você pode fazer isso clicando no item clicar no item &quot;Nombre&quot; e inserindo o seguinte nome `yourLastName - Account Creation Journey`. Clique em **OK** para salvar como mudanças.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish**  novamente.

![ACOP](./images/publish1.png)

Você va uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Você terminou este ejercicio.

Próxima etapa: [2.4 Prueba de la jornada](./ex4.md)

[Hoteles cerca de Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos los Módulos](../../overview.md)
