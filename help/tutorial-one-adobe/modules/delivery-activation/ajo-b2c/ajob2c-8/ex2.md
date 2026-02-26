---
title: Cree su campaña orquestada
description: Cree su campaña orquestada
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 0328260e8699107bc82103af98caae684319a60d
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 2%

---

# 3.8.2 Creación de una campaña orquestada

## 3.8.2.1 Crear su campaña orquestada

Ir a **Campañas**. Haga clic en **Crear campaña**.

![AJO OC](./images/ajooc1.png)

Seleccione **Orquestación - Marketing** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc2.png)

Escriba el nombre de la campaña: `--aepUserLdap-- - CitiSignal Family Account Optimization Campaign` y haga clic en **Guardar**.

![AJO OC](./images/ajooc3.png)

Entonces debería ver esto. Haga clic en el icono **+**.

![AJO OC](./images/ajooc4.png)

Seleccione **Bifurcación**.

![AJO OC](./images/ajooc5.png)

### Generar audiencia 1

Haga clic en el icono **+** y, a continuación, seleccione **Generar audiencia**.

![AJO OC](./images/ajooc6.png)

Haga clic para abrir la carpeta de **Dimensión de segmentación**.

![AJO OC](./images/ajooc7.png)

Seleccione **`--aepUserLdap--_citisignal_recipients`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc8.png)

Haga clic en **Crear audiencia**.

![AJO OC](./images/ajooc9.png)

Haga clic en **Agregar condición**.

![AJO OC](./images/ajooc10.png)

Seleccione **recipient_type** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc11.png)

Escriba **`account_holder`** en el campo **Valor** y haga clic en **Calcular**.

![AJO OC](./images/ajooc12.png)

Debería ver un número de **perfiles segmentados**. Haga clic en algún lugar del área gris como se indica.

![AJO OC](./images/ajooc13.png)

Haga clic en **Agregar condición**.

![AJO OC](./images/ajooc14.png)

Profundizar hasta **`citisignal_accounts`**.

![AJO OC](./images/ajooc15.png)

Seleccione **`account_status`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc16.png)

Escriba **`active`** en el campo **Valor**. A continuación, haga clic en algún lugar del área gris como se indica.

![AJO OC](./images/ajooc17.png)

Haga clic en **Agregar condición**.

![AJO OC](./images/ajooc18.png)

Profundizar hasta **`citisignal_mobile_subscriptions`**.

![AJO OC](./images/ajooc19.png)

Seleccione **`subscription_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc20.png)

Habilite el conmutador para **datos agregados**. A continuación, seleccione lo siguiente:

- **Función de agregado**: **Recuento**
- **Operador**: **mayor o igual que**
- **Valor**: **1**

Haga clic en **Confirmar**.

![AJO OC](./images/ajooc21.png)

Entonces debería ver esto. Haga clic en **Confirmar**.

![AJO OC](./images/ajooc22.png)

### Generar audiencia 2

Haga clic en el icono **+** en el siguiente nodo de la otra ruta.

![AJO OC](./images/ajooc23.png)

Seleccione **Generar audiencia**.

![AJO OC](./images/ajooc24.png)

Haga clic para abrir la carpeta de **Dimensión de segmentación**.

![AJO OC](./images/ajooc25.png)

Seleccione **`--aepUserLdap--_mobile_subscriptions`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc26.png)

Haga clic en **Crear audiencia**.

![AJO OC](./images/ajooc27.png)

Haga clic en **Agregar condición**.

![AJO OC](./images/ajooc28.png)

Seleccione **subscription_status** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc29.png)

Escriba **`active`** en el campo **Valor**. A continuación, haga clic en **Agregar condición**.

![AJO OC](./images/ajooc30.png)

Seleccione **`is_upgrade_eligible`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc31.png)

Establecer **Value** en **true**

![AJO OC](./images/ajooc32.png)

Haga clic en **Calcular** para ver una estimación de los perfiles aptos para esta audiencia. A continuación, haga clic en **Confirmar**

![AJO OC](./images/ajooc33.png)

### División

Haga clic en el icono **+** y luego seleccione **Dividir**.

![AJO OC](./images/ajooc34.png)

Cambie el campo **Label** a **90/10 Treatment vs Control**. Haga clic para abrir el objeto **Subconjunto**.

![AJO OC](./images/ajooc35.png)

Habilite el conmutador para **Habilitar límite** y establezca el **Tamaño límite** en **10 por ciento**.

![AJO OC](./images/ajooc36.png)

Haga clic en **Agregar segmento** y verá que se agrega el objeto **Result**.

Haga clic en **Guardar**.

![AJO OC](./images/ajooc37.png)

### Guardar público

Haga clic en el icono **+** y luego seleccione **Guardar audiencia**.

![AJO OC](./images/ajooc38.png)

Establezca el campo **Etiqueta de audiencia** en **`--aepUserLdap-- - Control Group`**. Haga clic en **Agregar asignación de audiencia**.

![AJO OC](./images/ajooc39.png)

Desglose hasta **dimensión de segmentación**.

![AJO OC](./images/ajooc40.png)

Seleccione **`account_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc41.png)

Establezca el **campo de asignación de perfiles** en **`--aepUserLdap--_citisignal_recipients - account_id`**.

![AJO OC](./images/ajooc41a.png)

### Enrichment: Suscripción a Internet

Haga clic en el icono **+**.

![AJO OC](./images/ajooc42.png)

Seleccione **Enriquecimiento**.

![AJO OC](./images/ajooc43.png)

Entonces debería ver esto. Haga clic en **Añadir datos de enriquecimiento**.

![AJO OC](./images/ajooc44.png)

Profundizar hasta **`Targeting dimension`**.

![AJO OC](./images/ajooc44a.png)

Profundizar hasta **`citisignal_accounts`**.

![AJO OC](./images/ajooc45.png)

Profundizar hasta **`citisignal_internet_subscriptions`**.

![AJO OC](./images/ajooc45a.png)

Seleccione **`account_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc46.png)

Entonces debería ver esto. Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc47.png)

Seleccione **`subscription_status`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc48.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc49.png)

Seleccione **`connection_type`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc50.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc51.png)

Seleccione **`service_city`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc52.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc53.png)

Seleccione **`avg_bandwidth_usage_gb`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc54.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc55.png)

Seleccione **`data_cap_gb`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc56.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc57.png)

Seleccione **`advertised_speed_mbps`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc58.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc59.png)

Seleccione **`monthly_recurring_charge`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc60.png)

Haga clic en **Guardar**.

![AJO OC](./images/ajooc61.png)

Desplácese hacia arriba y cambie el campo **Label** a `Enrichment: Internet Subscription`.

![AJO OC](./images/ajooc61a.png)

### Enrichment: suscripción a dispositivos móviles

Haga clic en el icono **+** en el siguiente nodo y seleccione **Enriquecimiento**.

![AJO OC](./images/ajooc62.png)

Cambie el campo **Label** a `Enrichment: Mobile Devices Subscription` y haga clic en **Agregar datos de enriquecimiento**.

![AJO OC](./images/ajooc63.png)

Profundizar hasta **Dimensión de segmentación**.

![AJO OC](./images/ajooc64.png)

Profundizar hasta **`citisignal_accounts`**.

![AJO OC](./images/ajooc65.png)

Profundizar hasta **`citisignal_mobile_subscriptions`**.

![AJO OC](./images/ajooc65a.png)

Seleccione **`phone_number`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc66.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc67.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc68.png)

Seleccione **`model`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc68a.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc69.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc69a.png)

Seleccione **`recommended_device_model`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc70.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc71.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc71a.png)

Seleccione **`is_upgrade_eligible`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc72.png)

Ahora puede probar el progreso realizando una ejecución de prueba y ver qué datos están disponibles en la campaña.

Guarde los cambios y haga clic en **Iniciar**.

![AJO OC](./images/ajooctest1.png)

Después de un tiempo, debería ver esto. Haga clic en **Vista previa de resultados**.

![AJO OC](./images/ajooctest2.png)

Entonces debería ver algo similar a esto. Haga clic en **Cerrar**.

![AJO OC](./images/ajooctest3.png)

Vuelva al nodo **Enrichment: Mobile Devices Subscription**.

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc73.png)

Seleccione **`account_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc74.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc75.png)

Seleccione **`subscription_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc76.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc77.png)

Seleccione **`renewal_eligibility_date`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc78.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc79.png)

Seleccione **`line_user_recipient_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc80.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc81.png)

Seleccione **`current_device_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc82.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc86.png)

Seleccione **`contract_start_date`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc87.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc89.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc90.png)

Seleccione **`manufacturer`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc91.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc92.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc93.png)

Seleccione **`device_age_months`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc94.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc95.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc96.png)

Seleccione **`trade_in_value`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc97.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc98.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc99.png)

Seleccione **`monthly_payment`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc100.png)

### Enrichment: suscripción a dispositivos móviles

Entonces deberías tener esto. Haga clic en **Guardar**. A continuación, haga clic en el icono **+** para agregar un nuevo nodo y seleccione **Enriquecimiento**.

![AJO OC](./images/ajooc101.png)

Entonces debería ver esto. Haga clic en **Añadir datos de enriquecimiento**.

![AJO OC](./images/ajooc102.png)

Profundizar hasta **Dimensión de segmentación**.

![AJO OC](./images/ajooc103.png)

Profundizar hasta **`citisignal_offer_eligibility`**.

![AJO OC](./images/ajooc104.png)

Profundizar hasta **`citisignal_offers`**.

![AJO OC](./images/ajooc105.png)

Seleccione **`offer_name`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc106.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc107.png)

Profundizar hasta **`citisignal_offers`**.

![AJO OC](./images/ajooc108.png)

Seleccione **`offer_code`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc109.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc110.png)

Profundizar hasta **`citisignal_offers`**.

![AJO OC](./images/ajooc111.png)

Seleccione **`offer_description`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc112.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc110.png)

Profundizar hasta **`citisignal_offers`**.

![AJO OC](./images/ajooc113.png)

Seleccione **`offer_description`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc114.png)

Activar **Habilitar ordenación**.

![AJO OC](./images/ajooc115.png)

Profundizar hasta **`citisignal_offers`**.

![AJO OC](./images/ajooc116.png)

Seleccione **`offer_priority`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc117.png)

Ahora puede probar la campaña. Haga clic en **inicio**.

![AJO OC](./images/ajooc118.png)

Después de un tiempo deberías ver esto. Haga clic en **Resultado** y, a continuación, seleccione **Previsualizar resultados**.

![AJO OC](./images/ajooc120.png)

Entonces debería ver algo similar a esto.

![AJO OC](./images/ajooc121.png)

### Actividad del correo electrónico

Haga clic en el icono **+** y luego seleccione **Correo electrónico**.

![AJO OC](./images/ajooc122.png)

Haga clic en **Editar correo electrónico**.

![AJO OC](./images/ajooc123.png)

Ir a **Acciones**.

![AJO OC](./images/ajooc124.png)

Seleccione la **configuración del canal de correo electrónico** que creó anteriormente y luego haga clic en **Editar contenido**.

![AJO OC](./images/ajooc125.png)

Para la **línea de asunto**, pegue esto:

`{{target.--aepUserLdap--_citisignal_recipients.first_name}}, Your CitiSignal Family Account Summary`

Haga clic en **Editar cuerpo del correo electrónico**.

![AJO OC](./images/ajooc126.png)

## Pasos siguientes

Volver a [Adobe Journey Optimizer: campañas orquestadas](./ajocampaigns.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
