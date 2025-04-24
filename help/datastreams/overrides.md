---
title: Gegevensstroomoverschrijvingen configureren
description: Leer hoe te om gegevensstroom met voeten te treden in de UI van Datastreams en hen via het Web SDK of Mobiele SDK te activeren.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# Gegevensstroomoverschrijvingen configureren

Met gegevensstroomoverschrijvingen kunt u aanvullende configuraties voor uw gegevensstreams definiëren. Deze worden via de webpagina SDK of de mobiele SDK aan de Edge Network doorgegeven.

Dit helpt u verschillend gegevensstroomgedrag dan de standaarddegenen teweegbrengen, zonder een gegevensstroom te creëren of uw bestaande montages te wijzigen.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst, moet u uw de configuratieopheffing van de gegevensstroom in de [ gegevenstream configuratiepagina ](configure.md) bepalen.
2. Vervolgens moet u de overschrijvingen op een van de volgende manieren naar de Edge Network verzenden:
   * Door `sendEvent` of `configure` [ SDK van het Web ](#send-overrides) bevelen.
   * Door het Web SDK [ markeringsuitbreiding ](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Door Mobiele SDK [ sendEvent ](#send-overrides) API of door [ Regels ](#send-overrides) te gebruiken.

Dit artikel verklaart het proces van de de configuratieopheffing van begin tot eind van de gegevensstroom voor elk type van gesteunde opheffing.

>[!IMPORTANT]
>
>De overrides van de gegevensstroom worden slechts gesteund voor [ SDK van het Web ](../web-sdk/home.md) en [ Mobiele integratie van SDK ](https://developer.adobe.com/client-sdks/home/). [ de integratie van Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/api/) steunt momenteel geen gegevensstroomoverschrijvingen.
><br>
>De overrides van DataStream zouden moeten worden gebruikt wanneer u verschillende gegevens nodig hebt die naar verschillende gegevensstromen worden verzonden. Gebruik geen gegevensstroomoverschrijvingen voor gevallen van verpersoonlijking of toestemmingsgegevens.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer om datastream met voeten te treden, zijn hier sommige gebruiksgevallen die de klanten van Adobe Experience Platform kunnen oplossen door deze eigenschap te gebruiken.

**Multiregion gegevensinzameling**

Een bedrijf heeft verschillende websites of subdomeinen voor verschillende landen waarin het actief is. Zij hebben [ gevormd ](configure.md) afzonderlijke gegevensstromen met overeenkomstige analytische-specifieke rapportsuites, land-specifieke het bezitstokens van Adobe Target, land-specifieke schema&#39;s, datasets, de configuraties van Journey Optimizer, etc. De onderneming heeft ook een algemene reeks configuraties waarbij alle landspecifieke gegevens worden samengevoegd.

Door gegevensstroomoverschrijvingen te gebruiken, kan het bedrijf dynamisch de stroom van gegevens aan verschillende gegevensstromen, in plaats van het standaardgedrag schakelen om gegevens naar één gegevensstroom te verzenden.

Een veelvoorkomend geval van gebruik kan het verzenden van gegevens naar een landspecifieke gegevensstroom en ook naar een globale gegevensstroom zijn waar klanten een belangrijke actie uitvoeren, zoals het plaatsen van een orde of het bijwerken van hun gebruikersprofiel.

**het Verschillende profielen en identiteiten voor verschillende bedrijfseenheden**

Een bedrijf met veelvoudige bedrijfseenheden wil de veelvoudige zandbakken van de Platforms van de Ervaring gebruiken om gegevens op te slaan specifiek voor elke bedrijfseenheid.

In plaats van gegevens naar een standaardgegevensstroom te verzenden, kan het bedrijf gegevensstroomoverschrijvingen gebruiken om ervoor te zorgen dat elke bedrijfseenheid zijn eigen gegevensstroom heeft om gegevens door te ontvangen.

## Gegevensstroomoverschrijvingen configureren in de interface voor gegevensstromen {#configure-overrides}

De configuratieoverschrijvingen van DataStream staan u toe om de volgende configuraties van de gegevensstroom te wijzigen:

* Experience Platform-gebeurtenisgegevenssets
* Adobe Target-eigenschapstokens
* Audience Manager ID-synchronisatiecontainers
* Adobe Analytics rapport suites

### DataStream-overschrijvingen voor Adobe Target {#target-overrides}

Als u gegevensstroomoverschrijvingen voor een Adobe Target-gegevensstroom wilt configureren, moet u eerst een Adobe Target-gegevensstroom hebben gemaakt. Volg de instructies om [ een datastream ](configure.md) met de [ Adobe Target ](configure.md#target) dienst te vormen.

Zodra u de gegevensstroom hebt gecreeerd, geef de [ dienst van Adobe Target ](configure.md#target) uit die u hebt toegevoegd en gebruik de **[!UICONTROL Property Token Overrides]** sectie om de gewenste gegevensstroom met voeten te treden, zoals aangetoond in het hieronder beeld. Voeg één eigenschapstoken per regel toe.

{het schermschot van 0} gegevensstromen UI die de de dienstmontages van Adobe Target toont, met de benadrukte de bezitstoken met voeten treedt.](assets/overrides/override-target.png)![

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Target-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [ de overschrijvingen naar Edge Network via het Web SDK of Mobiele SDK ](#send-overrides) verzenden.

### DataStream-overschrijvingen voor Adobe Analytics {#analytics-overrides}

Om gegevensstroomoverschrijvingen voor een Adobe Analytics datastream te vormen, moet u eerst een [ gemaakte Adobe Analytics ](configure.md#analytics) datastream hebben. Volg de instructies om [ een datastream ](configure.md) met de [ Adobe Analytics ](configure.md#analytics) dienst te vormen.

Zodra u de gegevensstroom hebt gecreeerd, geef de [ dienst van Adobe Analytics ](configure.md#target) uit die u hebt toegevoegd en gebruik de **[!UICONTROL Report Suite Overrides]** sectie om de gewenste gegevensstroom met voeten te treden, zoals aangetoond in het hieronder beeld.

Selecteer **[!UICONTROL Show Batch Mode]** om het in batch bewerken van de rapportsuite overschrijven in te schakelen. U kunt een lijst met rapportsuite-overschrijvingen kopiëren en plakken en per regel één rapportsuite invoeren.

{het schermschot van 0} gegevensstromen UI die de de dienstmontages van Adobe Analytics toont, met de benadrukte de opheffing van de rapportreeks.](assets/overrides/override-analytics.png)![

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Analytics-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [ de overschrijvingen naar Edge Network via het Web SDK of Mobiele SDK ](#send-overrides) verzenden.

### DataStream overschrijft de gegevenssets voor Experience Platform-gebeurtenissen {#event-dataset-overrides}

Om gegevensstroomoverschrijvingen voor de gebeurtenisdatasets van Experience Platform te vormen, moet u eerst een [ gemaakte Adobe Experience Platform ](configure.md#aep) datastream hebben. Volg de instructies om [ een datastream ](configure.md) met de [ Adobe Experience Platform ](configure.md#aep) dienst te vormen.

Zodra u de gegevensstroom hebt gecreeerd, geef de [ dienst van Adobe Experience Platform ](configure.md#aep) uit die u hebt toegevoegd en selecteer de **[!UICONTROL Add Event Dataset]** optie om één of meerdere met voeten getreden gebeurtenisdatasets, zoals aangetoond in het hieronder beeld toe te voegen.

{het schermschot van 0} gegevensstromen UI die de de dienstmontages van Adobe Experience Platform toont, met de benadrukte overschrijvingen van de gebeurtenisdataset.](assets/overrides/override-aep.png)![

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

De Adobe Experience Platform-gegevensstroomoverschrijvingen moeten nu zijn geconfigureerd. Nu kunt u [ de overschrijvingen naar Edge Network via het Web SDK of Mobiele SDK ](#send-overrides) verzenden.

### DataStream overschrijft de synchronisatie-containers van externe id&#39;s {#container-overrides}

Als u gegevensstroomoverschrijvingen voor synchronisatie-containers van derden wilt configureren, moet u eerst een gegevensstroom hebben gemaakt. Volg de instructies om [ een datastream ](configure.md) te vormen om te creëren.

Wanneer u de gegevensstroom hebt gemaakt, gaat u naar **[!UICONTROL Advanced Options]** en schakelt u de optie **[!UICONTROL Third Party ID Sync]** in.

Voeg vervolgens in de sectie **[!UICONTROL Container ID Overrides]** de container-id&#39;s toe die u de standaardinstelling wilt overschrijven, zoals in de onderstaande afbeelding wordt getoond.

>[!IMPORTANT]
>
>Container-id&#39;s moeten numerieke waarden zijn, zoals `1234567` , en geen tekenreeksen, zoals `"1234567"` . Als u een tekenreekswaarde via de Web SDK verzendt als een containerid-overschrijving, ontvangt u een fout.

![ het schermschot van gegevensstromen UI die de montages van de gegevensstroom toont, met de benadrukte de synchronisatiecontainer van derdeidentiteitskaart.](assets/overrides/override-container.png)

Nadat u de gewenste overschrijvingen hebt toegevoegd, slaat u de gegevensstroominstellingen op.

U moet nu de containeroverschrijvingen voor id-synchronisatie hebben geconfigureerd. Nu kunt u [ de overschrijvingen naar Edge Network via het Web SDK of Mobiele SDK ](#send-overrides) verzenden.

## De overschrijvingen naar de Edge Network verzenden {#send-overrides}

Nadat u gegevensstroomoverschrijvingen hebt geconfigureerd in de gebruikersinterface voor gegevensverzameling, kunt u de overschrijvingen naar de Edge Network verzenden via de webpagina SDK of de mobiele SDK.

* **SDK van het Web**: Zie [ configuratie gegevensstroom met voeten treedt ](../web-sdk/commands/datastream-overrides.md#library) voor de instructies van de markeringsuitbreiding en de voorbeelden van de de bibliotheekcode van JavaScript.
* **Mobiele SDK**: U kunt gegeven-identiteitskaart met voeten treden of gebruikend [ sendEvent API ](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) of door [ Regels ](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/) te gebruiken.

## Payload-voorbeeld {#payload-example}

In de bovenstaande voorbeelden wordt een [!DNL Edge Network] -lading gegenereerd die vergelijkbaar is met de hieronder vermelde.

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
