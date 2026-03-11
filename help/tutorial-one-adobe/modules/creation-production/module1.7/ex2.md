---
title: Ejecutar el flujo de trabajo personalizado mediante programación
description: Ejecutar el flujo de trabajo personalizado mediante programación
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 1.7.2 Ejecutar el flujo de trabajo personalizado mediante programación

## 1.7.2.1: ejecute el flujo de trabajo personalizado con Postman

Después de publicar el flujo de trabajo en el ejercicio anterior, debería ver algo así. Haga clic en el botón **Copiar** para copiar la carga útil de ejemplo.

![Flujos de trabajo personalizados de Firefly](./images/ffcw61.png)

Abra Postman y cree una nueva **colección** con el nombre **Flujos de trabajo personalizados de Firefly**. A continuación, haga clic en **agregar solicitud**.

![Flujos de trabajo personalizados de Firefly](./images/ffcw62.png)

Debería ver una nueva solicitud vacía. En la barra de direcciones, pegue la carga útil que ha copiado del flujo de trabajo publicado.

Postman reconocerá el comando cURL que ha pegado y tomará toda la información de la carga útil y la añadirá en la solicitud de la manera correcta para usted.

![Flujos de trabajo personalizados de Firefly](./images/ffcw63.png)

Ahora debería ver estas variables **Header**.

![Flujos de trabajo personalizados de Firefly](./images/ffcw64.png)

Vaya a **Cuerpo**, donde debería ver algo similar a esto.

![Flujos de trabajo personalizados de Firefly](./images/ffcw65.png)

Ahora debe proporcionar las instrucciones necesarias en el cuerpo de esta solicitud. Al trabajar con archivos de forma programática, se requiere el uso de direcciones URL prefirmadas. Para este ejercicio, puede encontrar las URL prefirmadas a continuación para las 3 imágenes que forman parte de este ejercicio. Estas direcciones URL prefirmadas se crearon con las funciones de almacenamiento de Microsoft Azure. Si desea obtener más información sobre cómo crear direcciones URL con firma previa, consulte: [Optimizar el proceso de Firefly con Microsoft Azure y direcciones URL con firma previa](./../module1.1/ex2.md).

Para este ejercicio, puede utilizar las siguientes direcciones URL, de modo que no necesite crear nuevas direcciones URL con firma previa.

- **aerópodos.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D
```

- **watch.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/watch.jpg?sv=2023-01-03&st=2026-03-11T01%3A26%3A54Z&se=2027-03-12T01%3A26%3A00Z&sr=b&sp=r&sig=xCwQ09E%2F%2FT%2B7RLcb31Fum4uUBfsX0xHITKZTz4Ds9Zs%3D
```

- **teléfono.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/phone.png?sv=2023-01-03&st=2026-03-11T01%3A27%3A20Z&se=2027-03-12T01%3A27%3A00Z&sr=b&sp=r&sig=VVbX88P2sFSHHo9lmgoRhXRIXb42c0nDQhM9Z8nUG%2Bc%3D
```

También debe proporcionar indicadores como parte de la solicitud de Postman. A continuación se muestran las indicaciones que puede utilizar.

- **Mensaje 1**:

```
magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts
```

- **Mensaje 2**:

```
background hearts fluttering
```

Esta es una carga útil de ejemplo, pero no puede copiarla y reutilizarla, ya que los campos de **node_id** son exclusivos de su flujo de trabajo, por lo que esto solo sirve para darle una idea de cómo debería ser la carga útil:

```json
{
    "workflow": {
        "workflowId": "e0c63806-cf7c-442d-8884-26d57e9c0518",
        "inputs": [
            [
                {
                    "node_id": "node_1772156869527_d8mjasues_1_u10dlg",
                    "content": [
                        {
                            "presignedUrl": "https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D",
                            "storageType": "Azure"
                        }
                    ]
                },
                {
                    "node_id": "node_1772157264659_oq2csr2nn_5_fh5hek",
                    "content": "magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts"
                },
                {
                    "node_id": "node_1772157397147_qdwxiyktg_8_nm0o2k",
                    "content": "background hearts fluttering"
                }
            ]
        ]
    }
}
```

Después de realizar los cambios en la carga útil, debería tener este aspecto. Una vez finalizado, haga clic en **Enviar**. A continuación, usa **CMD + S** o **CTRL + S** para **guardar** tu solicitud.

![Flujos de trabajo personalizados de Firefly](./images/ffcw66.png)

En la carga de respuesta ahora puede encontrar un par de vínculos. Estos vínculos permiten consultar el **estado** del flujo de trabajo y, una vez que el estado sea **completado**, puede usar la dirección URL **results** para recuperar la imagen y el vídeo generados.

Seleccione la URL **status** y cópiela.

![Flujos de trabajo personalizados de Firefly](./images/ffcw67.png)

Haz clic en los 3 puntos de la solicitud que estás usando y luego selecciona **Duplicar**.

![Flujos de trabajo personalizados de Firefly](./images/ffcw69.png)

En la nueva solicitud, cambie el tipo de solicitud a **GET** y reemplace la URL por la URL de estado que acaba de copiar.

![Flujos de trabajo personalizados de Firefly](./images/ffcw70.png)

En **Cuerpo**, asegúrese de que se ha eliminado todo. A continuación, haga clic en **Enviar**. A continuación, debería recibir una carga útil de respuesta similar, que mostrará un estado. Puede volver a enviar esta solicitud hasta que el estado cambie a **completado**. No olvides usar **CMD + S** o **CTRL + S** para **guardar** tu solicitud.

![Flujos de trabajo personalizados de Firefly](./images/ffcw71.png)

Volver a la primera solicitud **POST**. Ahora copie la URL de **results**.

![Flujos de trabajo personalizados de Firefly](./images/ffcw72.png)

Haga clic en los 3 puntos **...** de la segunda solicitud que creó y, a continuación, seleccione **Duplicar**.

![Flujos de trabajo personalizados de Firefly](./images/ffcw73.png)

En la nueva solicitud, pegue la URL **results** que copió y luego haga clic en **Enviar**. No olvides usar **CMD + S** o **CTRL + S** para **guardar** tu solicitud.

![Flujos de trabajo personalizados de Firefly](./images/ffcw74.png)

Desplácese hacia abajo en la carga útil de respuesta, donde encontrará referencias a la imagen y al vídeo creados. Haga clic en los vínculos para abrir estos archivos.

![Flujos de trabajo personalizados de Firefly](./images/ffcw75.png)

Esta es la imagen que se generó.

![Flujos de trabajo personalizados de Firefly](./images/ffcw76.png)

## 1.7.2.2 Ejecute su flujo de trabajo personalizado con Workfront Fusion

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Ir a **escenarios**. Si todavía no tiene una carpeta, cree una y, para el nombre de la carpeta, utilice: `--aepUserLdap--`. Seleccione su carpeta y luego seleccione **Crear nuevo escenario**.

![WF Fusion](./images/wffusion2.png)

Entonces debería ver esto.

![WF Fusion](./images/wffusion3.png)

Después de publicar el flujo de trabajo en el ejercicio anterior, debería ver algo así. Haga clic en el botón **Copiar** para copiar la carga útil de ejemplo.

![Flujos de trabajo personalizados de Firefly](./images/ffcw61.png)

Vuelva a su escenario de Workfront Fusion. Use **CMD + V** o **CTRL + V** para pegar la carga que copió en el escenario. Workfront Fusion detectará automáticamente la solicitud cURL y creará un nuevo módulo **HTTP - Realizar una solicitud** automáticamente.

Arrastre el icono **clock** al módulo **HTTP - Make a request**.

![WF Fusion](./images/wffusion5.png)

Entonces debería ver esto. Haga clic en el módulo **HTTP - Make a request** para abrirlo.

![WF Fusion](./images/wffusion6.png)

Debería ver que las variables **Header** ya están disponibles.

![WF Fusion](./images/wffusion7.png)

Desplácese hacia abajo para ver la carga útil predeterminada. Haga clic en el **icono** como se indica para mejorar la carga útil JSON.

![WF Fusion](./images/wffusion8.png)

Volver a Postman, a la primera **petición POST**. Copie la carga útil.

![WF Fusion](./images/wffusion9.png)

Vuelva a su escenario de Workfront Fusion. Reemplace la carga útil predeterminada existente por la carga útil copiada de Postman. Haga clic en el **icono** como se indica para mejorar la carga útil JSON.

Marque la casilla de verificación de **Analizar respuesta**.

Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion10.png)

Guarde los cambios y haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffusion11.png)

Una vez que se haya ejecutado el escenario, podrá ver una respuesta similar a la que obtuvo en Postman. Con esta información disponible en Workfront Fusion, ahora puede basarse en ella para sondear la dirección URL **status** hasta que se complete el estado y, una vez que esto haya sucedido, puede utilizar la dirección URL **results** para recopilar la imagen y el vídeo generados.

![WF Fusion](./images/wffusion12.png)

## Pasos siguientes

Volver a [flujos de trabajo personalizados de Firefly](./workflowbuilder.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
