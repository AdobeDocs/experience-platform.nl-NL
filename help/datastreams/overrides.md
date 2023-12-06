---
title: Gegevensstroomoverschrijvingen configureren
description: Leer hoe te om gegevensstroom met voeten te treden in de UI van Datastreams en hen via het Web SDK te activeren.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 0%

---

# Gegevensstroomoverschrijvingen configureren

Met de gegevensstroom overschrijft kunt u aanvullende configuraties voor uw gegevensstromen definiëren. Deze configuraties worden via de SDK van het Web doorgegeven aan het Edge-netwerk.

Dit helpt u verschillend gegevensstroomgedrag dan de standaarddegenen teweegbrengen, zonder een gegevensstroom te creëren of uw bestaande montages te wijzigen.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst moet u de configuratieoverschrijving voor de gegevensstroom definiëren in het dialoogvenster [configuratiepagina gegevensstroom](configure.md).
2. Dan, moet u de met voeten treedt naar het Netwerk van de Rand op één van de volgende manieren verzenden:
   * Via de `sendEvent` of `configure` [Web SDK](#send-overrides-web-sdk) opdrachten.
   * Via de web SDK [tagextensie](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Via de mobiele SDK [sendEvent](#send-overrides-mobile-sdk) gebruiken.

Dit artikel verklaart het proces van de de configuratieopheffing van begin tot eind van de gegevensstroom voor elk type van gesteunde opheffing.

>[!IMPORTANT]
>
>Gegevensstroomoverschrijvingen worden alleen ondersteund voor [Web SDK](../edge/home.md) en [Mobile SDK](https://developer.adobe.com/client-sdks/home/) integratie. [Server-API](../server-api/overview.md) Integraties bieden momenteel geen ondersteuning voor gegevensstroomoverschrijvingen.
><br>
>De overrides van DataStream zouden moeten worden gebruikt wanneer u verschillende gegevens nodig hebt die naar verschillende gegevensstromen worden verzonden. Gebruik geen gegevensstroomoverschrijvingen voor gevallen van verpersoonlijking of toestemmingsgegevens.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer om datastream met voeten te treden, zijn hier sommige gebruiksgevallen die de klanten van Adobe Experience Platform kunnen oplossen door deze eigenschap te gebruiken.

**Gegevensverzameling over meerdere regio&#39;s**

Een bedrijf heeft verschillende websites of subdomeinen voor verschillende landen waarin het actief is. Ze hebben [geconfigureerd](configure.md) afzonderlijke gegevensstromen met overeenkomstige analytische-specifieke rapportreeksen, land-specifieke eigenschappen van Adobe Target tokens, landspecifieke schema&#39;s, datasets, configuraties van Journey Optimizer, etc. De onderneming heeft ook een algemene reeks configuraties waarbij alle landspecifieke gegevens worden samengevoegd.

Door gegevensstroomoverschrijvingen te gebruiken, kan het bedrijf dynamisch de stroom van gegevens aan verschillende gegevensstromen, in plaats van het standaardgedrag schakelen om gegevens naar één gegevensstroom te verzenden.

Een veelvoorkomend geval van gebruik kan het verzenden van gegevens naar een landspecifieke gegevensstroom en ook naar een globale gegevensstroom zijn waar klanten een belangrijke actie uitvoeren, zoals het plaatsen van een orde of het bijwerken van hun gebruikersprofiel.

**Verschillende profielen en identiteiten voor verschillende bedrijfseenheden**

Een bedrijf met veelvoudige bedrijfseenheden wil veelvoudige Experience Platforms zandbakken gebruiken om gegevens op te slaan specifiek voor elke bedrijfseenheid.

In plaats van gegevens naar een standaardgegevensstroom te verzenden, kan het bedrijf gegevensstroomoverschrijvingen gebruiken om ervoor te zorgen dat elke bedrijfseenheid zijn eigen gegevensstroom heeft om gegevens door te ontvangen.

## Gegevensstroomoverschrijvingen configureren in de interface voor gegevensstromen {#configure-overrides}

De configuratieoverschrijvingen van DataStream staan u toe om de volgende configuraties van de gegevensstroom te wijzigen:

* Gegevenssets voor gebeurtenissen Experience Platform
* Adobe Target-eigenschapstokens
* Audience Manager-id-synchronisatiecontainers
* Adobe Analytics rapport suites

### DataStream-overschrijvingen voor Adobe Target {#target-overrides}

Als u gegevensstroomoverschrijvingen voor een Adobe Target-gegevensstroom wilt configureren, moet u eerst een Adobe Target-gegevensstroom hebben gemaakt. Volg de instructies op [configureren, een gegevensstroom](configure.md) met de [Adobe Target](configure.md#target) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Target](configure.md#target) service die u hebt toegevoegd en gebruikt **[!UICONTROL Property Token Overrides]** om de gewenste gegevensstroomoverschrijvingen toe te voegen, zoals in de onderstaande afbeelding wordt getoond. Voeg één eigenschapstoken per regel toe.

![Het het schermschot van gegevensstromen UI die de de dienstmontages van Adobe Target toont, met de het bezitstoken met voeten getreden benadrukt.](assets/overrides/override-target.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Target-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

### DataStream-overschrijvingen voor Adobe Analytics {#analytics-overrides}

Als u gegevensstroomoverschrijvingen voor een Adobe Analytics-gegevensstroom wilt configureren, moet u eerst een [Adobe Analytics](configure.md#analytics) datastream gemaakt. Volg de instructies op [configureren, een gegevensstroom](configure.md) met de [Adobe Analytics](configure.md#analytics) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Analytics](configure.md#target) service die u hebt toegevoegd en gebruikt **[!UICONTROL Report Suite Overrides]** om de gewenste gegevensstroomoverschrijvingen toe te voegen, zoals in de onderstaande afbeelding wordt getoond.

Selecteren **[!UICONTROL Show Batch Mode]** om batch-bewerking van de rapportsuite-overschrijvingen in te schakelen. U kunt een lijst met rapportsuite-overschrijvingen kopiëren en plakken en per regel één rapportsuite invoeren.

![De het schermschot van gegevensstromen UI die de de dienstmontages van Adobe Analytics toont, met de de rapportreeks benadrukt met voeten treedt.](assets/overrides/override-analytics.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Analytics-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

### DataStream-overschrijvingen voor gegevenssets met gebeurtenissen Experience Platform {#event-dataset-overrides}

Om gegevensstroomoverschrijvingen voor de gebeurtenisdatasets van het Experience Platform te vormen, moet u eerst hebben [Adobe Experience Platform](configure.md#aep) datastream gemaakt. Volg de instructies op [configureren, een gegevensstroom](configure.md) met de [Adobe Experience Platform](configure.md#aep) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Experience Platform](configure.md#aep) service die u hebt toegevoegd en selecteer de **[!UICONTROL Add Event Dataset]** optie om één of meerdere met voeten te treden gebeurtenis datasets, zoals aangetoond in het hieronder beeld toe te voegen.

![Het schermschot UI van gegevensstromen die de de dienstmontages van Adobe Experience Platform tonen, met de met voeten getreden van de gebeurtenisdataset.](assets/overrides/override-aep.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Experience Platform-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

### DataStream overschrijft de synchronisatie-containers van externe id&#39;s {#container-overrides}

Als u gegevensstroomoverschrijvingen voor synchronisatie-containers van derden wilt configureren, moet u eerst een gegevensstroom hebben gemaakt. Volg de instructies op [configureren, een gegevensstroom](configure.md) om er een te maken.

Wanneer u de gegevensstroom hebt gemaakt, gaat u naar **[!UICONTROL Advanced Options]** en de **[!UICONTROL Third Party ID Sync]** -optie.

Gebruik vervolgens de **[!UICONTROL Container ID Overrides]** om de container-id&#39;s toe te voegen die u wilt overschrijven met de standaardinstelling, zoals in de onderstaande afbeelding wordt getoond.

>[!IMPORTANT]
>
>Container-id&#39;s moeten numerieke waarden zijn, zoals `1234567`en niet tekenreeksen, zoals `"1234567"`. Als u een koordwaarde door SDK van het Web als de opheffing van containeridentiteitskaart verzendt, zult u een fout ontvangen.

![De het schermschot van gegevensstromen UI die de montages van de gegevensstroom toont, met de derde benadrukte de containeroverschrijvingen van de de synchronisatiecontainer van identiteitskaart](assets/overrides/override-container.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

U moet nu de containeroverschrijvingen voor id-synchronisatie hebben geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

## Verzend de overschrijvingen naar het Netwerk van de Rand via het Web SDK {#send-overrides-web-sdk}

>[!NOTE]
>
>Als alternatief voor het verzenden van de configuratieoverschrijvingen via de bevelen van SDK van het Web, kunt u de configuratieoverschrijvingen aan SDK van het Web toevoegen [tagextensie](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

Na [configureren van gegevensstroomoverschrijvingen](#configure-overrides) in de UI van de Inzameling van Gegevens, kunt u de met voeten getreden naar het Netwerk van de Rand, via het Web SDK nu verzenden.

Als u Web SDK gebruikt, verzendt het verzenden van de overschrijvingen naar het Netwerk van de Rand via `edgeConfigOverrides` bevel is de tweede en definitieve stap van het activeren van de configuratieoverschrijvingen van de gegevensstroom.

De gegevensstroomconfiguratieoverschrijvingen worden verzonden naar het Netwerk van de Rand door `edgeConfigOverrides` Web SDK, opdracht. Met deze opdracht maakt u gegevensstroomoverschrijvingen die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht. Als u het `configure` , worden de overschrijvingen voor elk verzoek overgegaan.

De `edgeConfigOverrides` wordt gebruikt om gegevensstroomoverschrijvingen te maken die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht.

Wanneer een configuratieopheffing met wordt verzonden `configure` bevel, is het inbegrepen op de volgende bevelen van SDK van het Web.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [vormen](../edge/fundamentals/configuring-the-sdk.md)

De opties globaal worden gespecificeerd kunnen door de configuratieoptie op individuele bevelen worden met voeten getreden.

### Het verzenden van configuratieoverschrijvingen via het Web SDK `sendEvent` command {#send-event}

In het onderstaande voorbeeld ziet u hoe een configuratieoverschrijving eruit kan zien op een `sendEvent` gebruiken.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Parameter | Beschrijving |
|---|---|
| `edgeConfigOverrides.datastreamId` | Met deze parameter kan één aanvraag naar een andere gegevensstroom gaan dan de gegevensstroom die door de `configure` gebruiken. |

### Het verzenden van configuratieoverschrijvingen via het Web SDK `configure` command {#send-configure}

In het onderstaande voorbeeld ziet u hoe een configuratieoverschrijving eruit kan zien op een `configure` gebruiken.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

## De overschrijvingen naar het Edge-netwerk verzenden via de mobiele SDK {#send-overrides-mobile-sdk}

Na [configureren van gegevensstroomoverschrijvingen](#configure-overrides) in de UI van de Inzameling van Gegevens, kunt u de overschrijvingen naar het Netwerk van de Rand, via Mobiele SDK nu verzenden.

Als u de SDK voor mobiele apparaten gebruikt, kunt u de overschrijvingen via de `sendEvent` API is de tweede en laatste stap van het activeren van gegevensstroomconfiguratieoverschrijvingen.

Voor meer informatie over het Experience Platform Mobile SDK, zie [Mobiele SDK-documentatie](https://developer.adobe.com/client-sdks/edge/edge-network/).

### DataStream ID-overschrijving via Mobile SDK {#id-override-mobile}

In de onderstaande voorbeelden ziet u hoe een gegevensstroom-id-overschrijving eruit zou kunnen zien op een mobiele SDK-integratie. Selecteer de tabbladen hieronder om de [!DNL iOS] en [!DNL Android] voorbeelden.

>[!BEGINTABS]

>[!TAB iOS (Swift)]

In dit voorbeeld wordt getoond hoe een gegevensstroom-id-overschrijving eruit ziet in een mobiele SDK [!DNL iOS] integratie.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]
let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamIdOverride: "SampleDatastreamId")

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android™ (Kotlin)]

In dit voorbeeld wordt getoond hoe een gegevensstroom-id-overschrijving eruit ziet in een mobiele SDK [!DNL Android] integratie.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamIdOverride("SampleDatastreamId")
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

### De configuratieopheffing van gegevensstroom via Mobiele SDK {#config-override-mobile}

De voorbeelden tonen hieronder hoe een de configuratieopheffing van gegevensstroom op een Mobiele integratie van SDK kon kijken. Selecteer de tabbladen hieronder om de [!DNL iOS] en [!DNL Android] voorbeelden.

>[!BEGINTABS]

>[!TAB iOS (Swift)]

In dit voorbeeld wordt getoond hoe een configuratieoverschrijving voor gegevensstroom eruit ziet in een mobiele SDK [!DNL iOS] integratie.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]

let configOverrides: [String: Any] = [
  "com_adobe_experience_platform": [
    "datasets": [
      "event": [
        "datasetId": "SampleEventDatasetIdOverride"
      ]
    ]
  ],
  "com_adobe_analytics": [
  "reportSuites": [
        "MyFirstOverrideReportSuite",
          "MySecondOverrideReportSuite",
          "MyThirdOverrideReportSuite"
      ]
  ],
  "com_adobe_identity": [
    "idSyncContainerId": "1234567"
  ],
  "com_adobe_target": [
    "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
 ],
]

let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamConfigOverride: configOverrides)

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android (Kotlin)]

In dit voorbeeld wordt getoond hoe een configuratieoverschrijving voor gegevensstroom eruit ziet in een mobiele SDK [!DNL Android] integratie.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val configOverrides = mapOf(
    "com_adobe_experience_platform"
    to mapOf(
        "datasets"
        to mapOf(
            "event"
            to mapOf("datasetId"
                to "SampleEventDatasetIdOverride")
        )
    ),
    "com_adobe_analytics"
    to mapOf(
        "reportSuites"
        to listOf(
            "MyFirstOverrideReportSuite",
            "MySecondOverrideReportSuite",
            "MyThirdOverrideReportSuite"
        )
    ),
    "com_adobe_identity"
    to mapOf(
        "idSyncContainerId"
        to "1234567"
    ),
    "com_adobe_target"
    to mapOf(
        "propertyToken"
        to "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    )
)

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamConfigOverride(configOverrides)
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

## Payload-voorbeeld {#payload-example}

De bovenstaande voorbeelden genereren een [!DNL Edge Network] lading gelijkend op hieronder.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
          }
        }
      },
      "com_adobe_analytics": {
        "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
      },
      "com_adobe_identity": {
        "idSyncContainerId": "1234567"
      },
      "com_adobe_target": {
        "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
      }
    },
    "state": {  }
  },
  "events": [  ]
}
```
