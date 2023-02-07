---
title: Bootcamp - Customer Journey Analytics - De perspectivas a acción - Brasil
description: Bootcamp - Customer Journey Analytics - De perspectivas a acción - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: febeba3596d3f98b2352c5ef8688ee011d25c9fe
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 4.6 Dos perspectivas à ação

## ones

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Utilice esse público no CDP em tempo real e Adobe Journey Optimizer

## 4.6.1 Crie uma audiência e publique-a

Em seu projeto, você criou um chamado **Sentimientos de llamada** e iu visualizar una cuantificación de usuários que tiveram suas ligações ao call center classico como **positivas**. Agora, você poderá criar um segmento com ess usuários e ativação-los em jornadas ou em canais de comunicação.

O primeiro passo é: No dolar criado no último exercício, selecione a linha **1. Sentimiento de llamada - Positivo**, clique com o botão direito de seu mouse e selecione a opção **Crear audiencia a partir de una selección**:

![demostración](./images/aud1.png)

Em seguida, dê um nome para a sua audiência, seguindo o modelo **yourLastName: la llamada de audiencia de cia se siente positiva**:

![demostración](./images/aud2.png)

Nota que é possível ter um preview da audiência que está sendo criada:

![demostración](./images/aud3.png)

Para finalizar, clique em **Publicar**:

![demostración](./images/aud4.png)

## 4.6.2 Utilizar sua audiência como parte de um segmento

Voltando para una Adobe Experience Platform, vá em **Segmentos > Examinar** e você conseguirá visualizar o seu segmento criado no CJA pronto e disponível para ser usado nas suas ativações e jornadas!

![demostración](./images/aud5.png)

Vamos agora utilizar esse segmento em uma ativaão no Facebook e em uma do cliente!

## 4.6.3 Usar seu segmento un tempo real de Real-Time CDP em

Na Adobe Experience Platform, vá em **Segmentos > Examinar** e encontró una audiência que você criou no CJA:

![demostración](./images/aud6.png)

Clique no seu segmento e, em seguida, clique em **Activar en destino**:

![demostración](./images/aud7.png)

Selecione es un destino chamada bootcamp-facebook e, em seguida, clique em Next:

![demostración](./images/aud8.png)

Em seguida, clique em Next novamente:

![demostración](./images/aud9.png)

Selecione a opção **Origen de la audiencia** e defina como **Directamente de los clientes** e clique em Next:

![demostración](./images/aud10.png)

Por fim, un sitio **Consulte** clique em Finish!

![demostración](./images/aud11.png)

¡Pronto! Agora segmento está vinculado el caos oficial de Facebook.
Agora, vamos utilizar esse segmento no AJO!

## 4.6.4 Utilizar el segmento en Adobe Journey Optimizer

Na interface da Adobe Experience Platform clique em Journey Optimizer e, em seguida, sin menú lateral esquerdo, clique em **Recorridos** e comee una uma criar **Crear Recorrido**:

![demostración](./images/aud20.png)

![demostración](./images/aud21.png)

![demostración](./images/aud22.png)

Em seguida, sin menú lateral esquino, em Eventos, selecione **Clasificación del segmento** e arraste-o até a: jornada

![demostración](./images/aud23.png)

Em seguida, em **Segmento** clique em **Editar** para seleum segmento:

![demostración](./images/aud24.png)

Selecione a audiência que você criou no CJA e clique em **Guardar**:

![demostración](./images/aud25.png)

¡Pronto! Una nueva você pode criar uma durante la ejecución para clientes que se calificficficará segmento!

[Volver al flujo de usuario 4](./uc4.md)

[Voltar para todos módulos](./../../overview.md)
