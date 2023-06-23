---
title: Bootcamp - Customer Journey Analytics - De las perspectivas a la acción - Brasil
description: Bootcamp - Customer Journey Analytics - De las perspectivas a la acción - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Objetivos

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Use esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Crie uma audiência e publique-a

Em seu projeto, você criou um filtro chamado **Sentimientos de llamada** e conseguiu a Quantidade de usuários que tiveram suas ligações ao call center classificado como ****. Agora, você poderá criar um com ess usuários e ativação-los em jornadas ou em canais de comunicação.

O primeiro passo é: No pain criado no último exercício, selecione a linha **1. Sensación de llamada: positiva**, clique com o botão direito de seu mouse e selecione a opção **Crear audiencia a partir de selección**:

![demostración](./images/aud1.png)

Em, el nombre para la audiência seguindo o modelo **yourLastName - la llamada de la audiencia de la CIA se siente positiva**:

![demostración](./images/aud2.png)

Note que é possível ter um preview da audiência que está sendo criada:

![demostración](./images/aud3.png)

Para, clique em **Público**:

![demostración](./images/aud4.png)

## 4.6.2 Usar sua audiência como parte de um

Voltando para a Adobe Experience Platform, vá em **Segmentos > Examinar** e você conse o seu criado no CJA pronto e disponível para ser usado nas suas ativações e jornadas!

![demostración](./images/aud5.png)

¡Vamos agora usar esse en la vida activa en Facebook e em uma jornada do cliente!

## 4.6.3 Usar el tiempo real de los usuarios de la plataforma de de Real-Time CDP

Na Adobe Experience Platform, vá em **Segmentos > Examinar** e encontre a audiência que você criou no CJA:

![demostración](./images/aud6.png)

Clique no seu, me gusta, me gusta, me gusta, me gusta... **Activar en destino**:

![demostración](./images/aud7.png)

Selecione a destination chamada bootcamp-facebook e, em, clique em Siguiente:

![demostración](./images/aud8.png)

Em, clique em Siguiente novamente:

![demostración](./images/aud9.png)

Selecciona una opción **Origen de la audiencia** e **Directamente de los clientes** e clique em Siguiente:

![demostración](./images/aud10.png)

Por fim, na página **Revisar** ¡Terminen!

![demostración](./images/aud11.png)

¡Pronto! Ágora o seu está vinculado aos públicos personalizados do Facebook.
¡Agora, vamos a utilizar esse no es AJO! ¡No! ¡No! ¡AJO!

## 4.6.4 Uso de la segmentación de datos en Adobe Journey Optimizer

Na interfaz da Adobe Experience Platform clique em Journey Optimizer e, em, no menu lateral esquerdo, clique em **Recorridos** e comece a criar uma jornada clicando em **Crear Recorrido**:

![demostración](./images/aud20.png)

![demostración](./images/aud21.png)

![demostración](./images/aud22.png)

Em, sin menú lateral esquerdo, em Eventos, selecione **Calificación de segmentos** e arraste-o até a jornada:

![demostración](./images/aud23.png)

Em, em **Segmento** círculo em **Editar** para selecionar un:

![demostración](./images/aud24.png)

Seleccione una audiencia que você criou no CJA e clique em **Guardar**:

![demostración](./images/aud25.png)

¡Pronto! A partir daí você pode criar uma jornada para clientes que se calificam para esse!

[Volver al flujo de usuario 4](./uc4.md)

[Voltar para todos los tiempos](./../../overview.md)
