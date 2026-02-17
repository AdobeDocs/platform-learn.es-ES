---
title: Cree su campaña orquestada
description: Cree su campaña orquestada
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 53be5cf34db144e346f9810359b583072743382f
workflow-type: tm+mt
source-wordcount: '830'
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

Seleccione **`avg_dowload_usage_gb`** y haga clic en **Confirmar**.

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

Profundizar hasta **`citisignal_mobile_subscriptions`**.

![AJO OC](./images/ajooc65.png)

Seleccione **`account_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc66.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc67.png)

Seleccione **`subscription_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc68.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc69.png)

Seleccione **`phone_number`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc70.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc71.png)

Seleccione **`renewal_eligibility_date`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc72.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc73.png)

Seleccione **`line_user_recipient_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc74.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc75.png)

Seleccione **`is_upgrade_eligible`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc76.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc77.png)

Seleccione **`current_device_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc78.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc79.png)

Seleccione **`contract_start_date`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc80.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc81.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc82.png)

Seleccione **`model`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc83.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc86.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc87.png)

Seleccione **`manufacturer`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc88.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc89.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc90.png)

Seleccione **`device_age_months`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc91.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc92.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc93.png)

Seleccione **`is_upgrade_eligible`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc94.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc95.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc96.png)

Seleccione **`recommended_upgrade_product_id`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc97.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc98.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc99.png)

Seleccione **`monthly_payment`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc100.png)

Haga clic en **Agregar atributo**.

![AJO OC](./images/ajooc101.png)

Profundizar hasta **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc102.png)

Habilite el modificador para **Habilitar ordenación**. Haga clic en el icono **Edit**.

![AJO OC](./images/ajooc103.png)

Seleccione **`phone_number`** y haga clic en **Confirmar**.

![AJO OC](./images/ajooc104.png)

Entonces deberías tener esto.

![AJO OC](./images/ajooc105.png)




Entonces deberías tener esto. Haga clic en **Guardar**.

![AJO OC](./images/ajooc80a.png)














![AJO OC](./images/ajooc103.png)


## Pasos siguientes

Volver a [Adobe Journey Optimizer: campañas orquestadas](./ajocampaigns.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
