---
title: 'Recuperación de actividades de Target: Migre la implementación de Adobe Target en su aplicación móvil a la extensión de Offer Decisioning y Target'
description: Obtenga información sobre cómo recuperar actividades de Adobe Target al migrar desde Adobe Target a la extensión móvil de Offer Decisioning y Target.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Recuperar actividades de Target

Las implementaciones móviles de Target utilizan mboxes regionales (ahora conocidos como &quot;ámbitos&quot;) para entregar contenido desde actividades que utilizan el Compositor de experiencias basadas en formularios de Target. Debe actualizar la aplicación móvil para incluir ámbitos en las llamadas de red.

El contenido devuelto por Target, también conocido como &quot;ofertas&quot;, suele consistir en texto o json que debe consumir en su aplicación para ofrecer la experiencia final al cliente. Las ofertas de Target se utilizan frecuentemente para:

* Habilitar los indicadores de funcionalidad en la aplicación
* Servir texto o imágenes alternativos

Si tiene actividades que deben ejecutarse en las versiones de extensión de Target y Offer Decisioning y Target de la aplicación, asegúrese de realizar pruebas exhaustivas. Si necesita utilizar distintas ofertas para distintas versiones de la aplicación, considere la posibilidad de utilizar las opciones de segmentación en la interfaz para enviar distintas ofertas a las distintas versiones.

Asegúrese siempre de incluir la gestión de errores para mostrar las experiencias adecuadas en condiciones de error.


## Solicitud y aplicación de contenido bajo demanda

>[!IMPORTANT]
>
>Después de aplicar contenido a la aplicación, es imprescindible activar la API `displayed` para que Target sepa que el visitante ha visto el contenido alternativo o predeterminado especificado en la actividad. Consulte la página [Rastrear eventos de conversión de Target](track-events.md) para obtener más información.


+++ Ejemplo de Android

>[!BEGINTABS]

>[!TAB Optimizar SDK]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ Ejemplo de iOS

>[!BEGINTABS]

>[!TAB Optimizar SDK]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++



A continuación, aprenda a [pasar parámetros de Target usando la extensión Offer Decisioning y Target](send-parameters.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Offer Decisioning y Target. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=es#M625).
