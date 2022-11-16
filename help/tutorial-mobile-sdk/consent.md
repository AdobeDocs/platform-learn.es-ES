---
title: Consentimiento
description: Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 7%

---

# Consentimiento

Obtenga información sobre cómo implementar el consentimiento en una aplicación móvil.

La extensión móvil de consentimiento de Adobe Experience Platform habilita la recopilación de preferencias de consentimiento de la aplicación móvil al utilizar el SDK móvil de Adobe Experience Platform y la extensión de red perimetral. Obtenga más información sobre [Extensión de consentimiento](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network), en la documentación.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección:

* Solicite el consentimiento al usuario.
* Actualice la extensión en función de la respuesta del usuario.
* Obtenga información sobre cómo obtener el estado de consentimiento actual.

## Solicitar consentimiento

Si ha seguido el tutorial desde el principio, recuerde configurar la variable **[!UICONTROL Nivel de consentimiento predeterminado]** a &quot;Pendiente&quot;. Para empezar a recopilar datos, debe obtener el consentimiento del usuario. En este tutorial, consiga el consentimiento simplemente preguntando con una alerta, en una aplicación real querrá consultar las prácticas recomendadas de consentimiento para su región.

1. Solo desea preguntar al usuario una vez. Una forma sencilla de gestionarlo es simplemente utilizando `UserDefaults`.
1. Vaya a `Home.swift`.
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

La extensión móvil de consentimiento suprime, penetra/permite automáticamente el seguimiento en función del valor de consentimiento actual. También puede acceder al estado de consentimiento actual por su cuenta:

1. Vaya a `Home.swift`.
1. Añada el siguiente código a `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

En el ejemplo anterior, simplemente está imprimiendo el estado de consentimiento en la consola. En un escenario real, puede utilizarlo para modificar los menús u opciones que se muestran al usuario.

## Validar con Assurance

1. Consulte la [Garantía](assurance.md) lección.
1. Instale la aplicación.
1. Inicie la aplicación con la URL generada por Assurance.
1. Si agregó el código anterior correctamente, se le pedirá que proporcione el consentimiento. Select **Sí**.
   ![ventana emergente de consentimiento](assets/mobile-consent-validate.png)
1. Debería ver un **[!UICONTROL Preferencias de consentimiento actualizadas]** en la interfaz de usuario de Assurance.
   ![validar consentimiento](assets/mobile-consent-update.png)

Siguiente: **[Recopilar datos del ciclo vital](lifecycle-data.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)