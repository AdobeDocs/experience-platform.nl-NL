---
keywords: Azure-gebeurtenishub-bestemming;azure-gebeurtenishub;azure-eventhub
title: (bèta) [!DNL Azure Event Hubs] verbinding
description: Creeer een uitgaande verbinding in real time aan uw [!DNL Azure Event Hubs] opslag naar streamgegevens van Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: b0c2c8313e05d1316f23dc15d99893e1887f8dcf
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# (bèta) [!DNL Azure Event Hubs] verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] doel in Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

[!DNL Azure Event Hubs] is een groot platform voor gegevensstreaming en service voor het opnemen van gebeurtenissen. Het kan miljoenen gebeurtenissen per seconde ontvangen en verwerken. Gegevens die naar een gebeurtenishub worden verzonden, kunnen worden getransformeerd en opgeslagen met behulp van een realtime analyseprovider of batchadapters.

U kunt een uitgaande verbinding in real time aan uw creëren [!DNL Azure Event Hubs] opslag om gegevens uit Adobe Experience Platform te streamen.

* Meer informatie over [!DNL Azure Event Hubs], zie de [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Verbinding maken met [!DNL Azure Event Hubs] programmatically, zie [Zelfstudie voor Streaming doelen-API](../../api/streaming-destinations.md).
* Verbinding maken met [!DNL Azure Event Hubs] in de gebruikersinterface van het Platform raadpleegt u de onderstaande secties.

![AWS Kinesis in de gebruikersinterface](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Gevallen gebruiken {#use-cases}

Door streamingdoelen zoals [!DNL Azure Event Hubs]kunt u bovendien gemakkelijk hoogwaardige segmentatiegebeurtenissen en de bijbehorende profielkenmerken in uw eigen systemen importeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan [!DNL Azure Event Hubs] doel, ontvangt u deze gebeurtenis in [!DNL Azure Event Hubs]. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Exporttype {#export-type}

**Op basis van profiel** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met selectiekenmerken van het dialoogvenster [activeringsworkflow voor publiek](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL SAS Key Name]** en **[!UICONTROL SAS Key]**: Vul uw SAS-sleutelnaam en -sleutel in. Meer informatie over verifiëren bij [!DNL Azure Event Hubs] met SAS-toetsen in de [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Vul uw [!DNL Azure Event Hubs] naamruimte. Meer informatie over [!DNL Azure Event Hubs] naamruimten in het dialoogvenster [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Name]**: Geef een naam op voor de verbinding met [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Geef een beschrijving van de verbinding op.  Voorbeelden: &quot;Klanten met de hoogste rang&quot;, &quot;Males die geïnteresseerd zijn in keukenvorming&quot;.
* **[!UICONTROL eventHubName]**: Geef een naam op voor de stream aan uw [!DNL Azure Event Hubs] bestemming.

## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](../../ui/activate-streaming-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Exportgedrag profiel {#profile-export-behavior}

Het Experience Platform optimaliseert het profiel uitvoergedrag aan uw bestemming van de Hubs van de Gebeurtenis Azure, om gegevens naar uw bestemming slechts uit te voeren wanneer de relevante updates aan een profiel na segmentkwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd teweeggebracht door een verandering in segmentlidmaatschap voor minstens één van de segmenten die aan de bestemming in kaart werden gebracht. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is geactiveerd door een wijziging in de [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate werd geactiveerd door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform] gegevenslagen in [!DNL Azure Event Hubs] in JSON-indeling. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```


>[!MORELIKETHIS]
>
>* [Verbind met Azure Event Hubs en activeer gegevens gebruikend de Dienst API van de Stroom](../../api/streaming-destinations.md)
>* [AWS Kinesis-bestemming](./amazon-kinesis.md)
>* [Doeltypen en -categorieën](../../destination-types.md)

