---
title: Consentimiento
description: Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 7%

---

# Consentimiento

Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.

La extensión móvil Adobe Experience Platform Consent habilita la recopilación de preferencias de consentimiento de su aplicación móvil al utilizar el SDK móvil de Adobe Experience Platform y la extensión de red perimetral. Obtenga más información acerca de [Extensión de consentimiento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/), en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Solicitar el consentimiento al usuario.
* Actualice la extensión en función de la respuesta del usuario.
* Obtenga información sobre cómo obtener el estado de consentimiento actual.

## Pedir consentimiento

Si ha seguido el tutorial desde el principio, recordará haber configurado la variable **[!UICONTROL Nivel de consentimiento predeterminado]** a &quot;Pendiente&quot;. Para empezar a recopilar datos, debe obtener el consentimiento del usuario. En este tutorial, obtenga el consentimiento simplemente preguntando con una alerta; en una aplicación del mundo real, querrá consultar las prácticas recomendadas de consentimiento para su región.

1. Solo desea preguntar al usuario una vez. Una forma sencilla de gestionarlo es simplemente utilizando `UserDefaults`.
1. Navegue hasta `Home.swift`.
1. Añada el siguiente código a `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. Si el usuario no ha visto la alerta antes, muéstrela y actualice el consentimiento en función de su respuesta. Añada el siguiente código a `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## Obtener estado de consentimiento actual

La extensión móvil de consentimiento suprimirá/anulará/permitirá automáticamente el seguimiento en función del valor de consentimiento actual. También puede acceder al estado de consentimiento actual usted mismo:

1. Navegue hasta `Home.swift`.
1. Añada el siguiente código a `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

En el ejemplo anterior, simplemente imprime el estado de consentimiento en la consola. En un escenario real, puede usarlo para modificar qué menús u opciones se muestran al usuario.

## Validar con Assurance

1. Revise la [Assurance](assurance.md) lección.
1. Instale la aplicación.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. Si agregó el código anterior correctamente, se le solicitará que proporcione consentimiento. Seleccionar **Sí**.
   ![ventana emergente de consentimiento](assets/mobile-consent-validate.png)
1. Debería ver una **[!UICONTROL Preferencias de consentimiento actualizadas]** en la interfaz de usuario de Assurance.
   ![validación del consentimiento](assets/mobile-consent-update.png)

Siguiente: **[Recopilar datos del ciclo vital](lifecycle-data.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)