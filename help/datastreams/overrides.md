---
title: Gegevensstroomoverschrijvingen configureren
description: Leer hoe te om gegevensstroom met voeten te treden in de UI van Datastreams en hen via het Web SDK of Mobiele SDK te activeren.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 17ed5f3c14d4787352f72d3d7721cbb6416d533e
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Gegevensstroomoverschrijvingen configureren

Met overschrijvingen van gegevensstroom kunt u aanvullende configuraties voor uw gegevensstromen definiëren. Deze configuraties worden via de SDK van het Web of de mobiele SDK aan de Edge Network doorgegeven.

Dit helpt u verschillend gegevensstroomgedrag dan de standaarddegenen teweegbrengen, zonder een gegevensstroom te creëren of uw bestaande montages te wijzigen.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst moet u de configuratieoverschrijving voor de gegevensstroom definiëren in het dialoogvenster [configuratiepagina gegevensstroom](configure.md).
2. Vervolgens moet u de overschrijvingen op een van de volgende manieren naar de Edge Network verzenden:
   * Via de `sendEvent` of `configure` [Web SDK](#send-overrides) opdrachten.
   * Via de web SDK [tagextensie](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Via de mobiele SDK [sendEvent](#send-overrides) API of door gebruik [Regels](#send-overrides).

Dit artikel verklaart het proces van de de configuratieopheffing van begin tot eind van de gegevensstroom voor elk type van gesteunde opheffing.

>[!IMPORTANT]
>
>Gegevensstroomoverschrijvingen worden alleen ondersteund voor [Web SDK](../web-sdk/home.md) en [Mobile SDK](https://developer.adobe.com/client-sdks/home/) integratie. [Server-API](../server-api/overview.md) Integraties bieden momenteel geen ondersteuning voor gegevensstroomoverschrijvingen.
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

De Adobe Target-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar de Edge Network via het Web SDK of Mobiele SDK](#send-overrides).

### DataStream-overschrijvingen voor Adobe Analytics {#analytics-overrides}

Als u gegevensstroomoverschrijvingen voor een Adobe Analytics-gegevensstroom wilt configureren, moet u eerst een [Adobe Analytics](configure.md#analytics) datastream gemaakt. Volg de instructies op [configureren, een gegevensstroom](configure.md) met de [Adobe Analytics](configure.md#analytics) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Analytics](configure.md#target) service die u hebt toegevoegd en gebruikt **[!UICONTROL Report Suite Overrides]** om de gewenste gegevensstroomoverschrijvingen toe te voegen, zoals in de onderstaande afbeelding wordt getoond.

Selecteren **[!UICONTROL Show Batch Mode]** om batch-bewerking van de rapportsuite-overschrijvingen in te schakelen. U kunt een lijst met rapportsuite-overschrijvingen kopiëren en plakken en per regel één rapportsuite invoeren.

![De het schermschot van gegevensstromen UI die de de dienstmontages van Adobe Analytics toont, met de de rapportreeks benadrukt met voeten treedt.](assets/overrides/override-analytics.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Analytics-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar de Edge Network via het Web SDK of Mobiele SDK](#send-overrides).

### DataStream-overschrijvingen voor gegevenssets met gebeurtenissen Experience Platform {#event-dataset-overrides}

Om gegevensstroomoverschrijvingen voor de gebeurtenisdatasets van het Experience Platform te vormen, moet u eerst hebben [Adobe Experience Platform](configure.md#aep) datastream gemaakt. Volg de instructies op [configureren, een gegevensstroom](configure.md) met de [Adobe Experience Platform](configure.md#aep) service.

Als u de gegevensstroom hebt gemaakt, bewerkt u de [Adobe Experience Platform](configure.md#aep) service die u hebt toegevoegd en selecteer de **[!UICONTROL Add Event Dataset]** optie om één of meerdere met voeten te treden gebeurtenis datasets, zoals aangetoond in het hieronder beeld toe te voegen.

![Het schermschot UI van gegevensstromen die de de dienstmontages van Adobe Experience Platform tonen, met de met voeten getreden van de gebeurtenisdataset.](assets/overrides/override-aep.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Experience Platform-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [verzend de met voeten treedt naar de Edge Network via het Web SDK of Mobiele SDK](#send-overrides).

### DataStream overschrijft de synchronisatie-containers van externe id&#39;s {#container-overrides}

Als u gegevensstroomoverschrijvingen voor synchronisatie-containers van derden wilt configureren, moet u eerst een gegevensstroom hebben gemaakt. Volg de instructies op [configureren, een gegevensstroom](configure.md) om er een te maken.

Wanneer u de gegevensstroom hebt gemaakt, gaat u naar **[!UICONTROL Advanced Options]** en de **[!UICONTROL Third Party ID Sync]** -optie.

Gebruik vervolgens de **[!UICONTROL Container ID Overrides]** om de container-id&#39;s toe te voegen die u wilt overschrijven met de standaardinstelling, zoals in de onderstaande afbeelding wordt getoond.

>[!IMPORTANT]
>
>Container-id&#39;s moeten numerieke waarden zijn, zoals `1234567`en niet tekenreeksen, zoals `"1234567"`. Als u een koordwaarde door SDK van het Web als de opheffing van containeridentiteitskaart verzendt, zult u een fout ontvangen.

![De het schermschot van gegevensstromen UI die de montages van de gegevensstroom toont, met de derde benadrukte de containeroverschrijvingen van de de synchronisatiecontainer van identiteitskaart](assets/overrides/override-container.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

U moet nu de containeroverschrijvingen voor id-synchronisatie hebben geconfigureerd. Nu kunt u [verzend de met voeten treedt naar de Edge Network via het Web SDK of Mobiele SDK](#send-overrides).

## De overschrijvingen naar de Edge Network verzenden {#send-overrides}

Na het vormen van gegevensstroom treedt in de Inzameling UI van Gegevens met voeten, kunt u de met voeten treedt naar de Edge Network door het Web SDK of Mobiele SDK verzenden.

* **Web SDK**: Zie [gegevensstroomconfiguratie overschrijft](../web-sdk/commands/datastream-overrides.md#library) voor instructies voor het toevoegen van tags en voorbeelden van JavaScript-bibliotheekcode.
* **Mobile SDK**: U kunt ID-overschrijvingen van gegevensstroom verzenden met de opdracht [sendEvent-API](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) of door [Regels](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

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
