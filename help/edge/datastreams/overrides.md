---
title: Gegevensstroomoverschrijvingen configureren
description: Leer hoe te om gegevensstroom met voeten te treden in de UI van Datastreams en hen via het Web SDK te activeren.
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Gegevensstroomoverschrijvingen configureren

Met de gegevensstroom overschrijft kunt u aanvullende configuraties voor uw gegevensstromen definiëren. Deze configuraties worden via de SDK van het Web doorgegeven aan het Edge-netwerk.

Dit helpt u verschillend gegevensstroomgedrag dan de standaarddegenen teweegbrengen, zonder het creëren van een nieuwe gegevensstroom of het wijzigen van uw bestaande montages.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst moet u de configuratie van uw gegevensstroom overschrijven in het dialoogvenster [databaseconfiguratiepagina](configure.md).
2. Dan, moet u de met voeten treedt naar het Netwerk van de Rand of via het bevel van SDK van het Web of door SDK van het Web te gebruiken verzenden [tagextensie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

Dit artikel verklaart het proces van de de configuratieopheffing van begin tot eind van de gegevensstroom voor elk type van gesteunde opheffing.

## Gegevensstroomoverschrijvingen configureren in de interface voor gegevensstromen {#configure-overrides}

De configuratieoverschrijvingen van DataStream staan u toe om de volgende configuraties van de gegevensstroom te wijzigen:

* Gegevenssets voor gebeurtenissen Experience Platform
* Adobe Target-eigenschapstokens
* Audience Manager-id-synchronisatiecontainers
* Adobe Analytics-rapportensuites

### DataStream-overschrijvingen voor Adobe Target {#target-overrides}

Als u gegevensstroomoverschrijvingen voor een Adobe Target-gegevensstroom wilt configureren, moet u eerst een Adobe Target-gegevensstroom hebben gemaakt. Volg de instructies op [configureren, gegevensstroom](configure.md) met de [Adobe Target](configure.md#target) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Target](configure.md#target) service die u hebt toegevoegd en gebruikt **[!UICONTROL Property Token Overrides]** om de gewenste gegevensstroomoverschrijvingen toe te voegen, zoals in de onderstaande afbeelding wordt getoond. Voeg één eigenschapstoken per regel toe.

![Het het schermschot van gegevensstromen UI die de de dienstmontages van Adobe Target toont, met de het bezitstoken met voeten getreden benadrukt.](../assets/datastreams/overrides/override-target.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Target-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

### DataStream-overschrijvingen voor Adobe Analytics {#analytics-overrides}

Als u gegevensstroomoverschrijvingen voor een Adobe Analytics-gegevensstroom wilt configureren, moet u eerst een [Adobe Analytics](configure.md#analytics) datastream gemaakt. Volg de instructies op [configureren, gegevensstroom](configure.md) met de [Adobe Analytics](configure.md#analytics) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Analytics](configure.md#target) service die u hebt toegevoegd en gebruikt **[!UICONTROL Report Suite Overrides]** om de gewenste gegevensstroomoverschrijvingen toe te voegen, zoals in de onderstaande afbeelding wordt getoond.

Selecteren **[!UICONTROL Show Batch Mode]** om batch-bewerking van de rapportsuite-overschrijvingen in te schakelen. U kunt een lijst met rapportsuite-overschrijvingen kopiëren en plakken en per regel één rapportsuite invoeren.

![De het schermschot van gegevensstromen UI die de de dienstmontages van Adobe Analytics toont, met de de rapportreeks benadrukt met voeten treedt.](../assets/datastreams/overrides/override-analytics.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Analytics-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

### DataStream-overschrijvingen voor gegevenssets met gebeurtenissen Experience Platform {#event-dataset-overrides}

Om gegevensstroomoverschrijvingen voor de gebeurtenisdatasets van het Experience Platform te vormen, moet u eerst hebben [Adobe Experience Platform](configure.md#aep) datastream gemaakt. Volg de instructies op [configureren, gegevensstroom](configure.md) met de [Adobe Experience Platform](configure.md#aep) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Experience Platform](configure.md#aep) service die u hebt toegevoegd en selecteer de **[!UICONTROL Add Event Dataset]** optie om één of meerdere met voeten te treden gebeurtenis datasets, zoals aangetoond in het hieronder beeld toe te voegen.

![Het schermschot UI van gegevensstromen die de de dienstmontages van Adobe Experience Platform tonen, met de met voeten getreden van de gebeurtenisdataset.](../assets/datastreams/overrides/override-aep.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Experience Platform-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

### DataStream overschrijft de synchronisatie-containers van externe id&#39;s {#container-overrides}

Als u gegevensstroomoverschrijvingen voor synchronisatie-containers van derden wilt configureren, moet u eerst een gegevensstroom hebben gemaakt. Volg de instructies op [configureren, gegevensstroom](configure.md) om er een te maken.

Wanneer u de gegevensstroom hebt gemaakt, gaat u naar **[!UICONTROL Advanced Options]** en de **[!UICONTROL Third Party ID Sync]** optie.

Gebruik vervolgens de **[!UICONTROL Container ID Overrides]** om de container-id&#39;s toe te voegen die u wilt overschrijven met de standaardinstelling, zoals in de onderstaande afbeelding wordt getoond.

>[!IMPORTANT]
>
>Container-id&#39;s moeten numerieke waarden zijn, zoals `1234567`en niet tekenreeksen, zoals `"1234567"`. Als u een koordwaarde door SDK van het Web als de opheffing van containeridentiteitskaart verzendt, zult u een fout ontvangen.

![De het schermschot van gegevensstromen UI die de montages van de gegevensstroom toont, met de derde benadrukte de containeroverschrijvingen van de de synchronisatiecontainer van identiteitskaart](../assets/datastreams/overrides/override-container.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

U moet nu de containeroverschrijvingen voor id-synchronisatie hebben geconfigureerd. Nu kunt u [verzend de met voeten treedt naar het Netwerk van de Rand via het Web SDK](#send-overrides).

## Verzend de overschrijvingen naar het Netwerk van de Rand via het Web SDK {#send-overrides}

>[!NOTE]
>
>Als alternatief voor het verzenden van de configuratieoverschrijvingen via de bevelen van SDK van het Web, kunt u de configuratieoverschrijvingen aan SDK van het Web toevoegen [tagextensie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

Na [configureren van gegevensstroomoverschrijvingen](#configure-overrides) in de UI van de Inzameling van Gegevens, kunt u de met voeten getreden naar het Netwerk van de Rand, via het Web SDK nu verzenden.

Het verzenden van de overschrijvingen naar het Edge-netwerk via de SDK van het web is de tweede en laatste stap van het activeren van de configuratieoverschrijvingen van de gegevensstroom.

De gegevensstroomconfiguratieoverschrijvingen worden verzonden naar het Netwerk van de Rand door `edgeConfigOverrides` Web SDK, opdracht. Met deze opdracht maakt u gegevensstroomoverschrijvingen die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht, of, in het geval van de `configure` voor elke aanvraag.

De `edgeConfigOverrides` command maakt gegevensstroomoverschrijvingen die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht, of, in het geval van `configure`, voor elk verzoek.

Wanneer een configuratieopheffing met wordt verzonden `configure` wordt opgenomen in de volgende ondersteunde opdrachten.

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [vormen](../fundamentals/configuring-the-sdk.md)

De opties globaal worden gespecificeerd kunnen door de configuratieoptie op individuele bevelen worden met voeten getreden.

### Configuratieoverschrijvingen verzenden via de `sendEvent` command {#send-event}

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
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
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

### Configuratieoverschrijvingen verzenden via de `configure` command {#send-configure}

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
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
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

### Payload-voorbeeld {#payload-example}

De bovenstaande voorbeelden genereren een [!DNL Edge Network] lading die als dit kijkt:

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
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
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```
