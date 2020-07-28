---
title: (Beta) Azure Event Hubs-bestemming
seo-title: (Beta) Azure Event Hubs-bestemming
description: Creeer een uitgaande verbinding in real time aan uw opslag van de Hubs van de Azure Gebeurtenis aan stroomgegevens van Experience Platform.
seo-description: Creeer een uitgaande verbinding in real time aan uw opslag van de Hubs van de Azure Gebeurtenis aan stroomgegevens van Experience Platform.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# (Beta) [!DNL Azure Event Hubs] bestemming

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] bestemming in Adobe in real time CDP is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

[!DNL Azure Event Hubs] is een groot platform voor gegevensstreaming en service voor het opnemen van gebeurtenissen. Het kan miljoenen gebeurtenissen per seconde ontvangen en verwerken. Gegevens die naar een gebeurtenishub worden verzonden, kunnen worden getransformeerd en opgeslagen met behulp van een realtime analyseprovider of batchadapters.

U kunt een uitgaande verbinding in real time aan uw [!DNL Azure Event Hubs] opslag tot stand brengen aan stroomgegevens van Adobe Experience Platform.

* Voor meer informatie over [!DNL Azure Event Hubs], zie de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Zie de zelfstudie over de API- [!DNL Azure Event Hubs] streamingdoelen als u verbinding wilt maken met het [gebruik van API-aanroepen](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md).
* Zie de onderstaande secties om verbinding te maken met [!DNL Azure Event Hubs] het gebruik van de CDP-gebruikersinterface van Adobe Real-Time.

![AWS Kinesis in de gebruikersinterface](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Gevallen gebruiken {#use-cases}

Door het stromen bestemmingen zoals te gebruiken [!DNL Azure Event Hubs], kunt u high-value segmenteringsgebeurtenissen en bijbehorende profielattributen in uw systemen van keus gemakkelijk invoeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan de [!DNL Azure Event Hubs] bestemming valt, zou u deze gebeurtenis binnen ontvangen [!DNL Azure Event Hubs]. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloud-opslagdoelen ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)voor instructies over het maken van een verbinding met uw cloudopslagdoelen, inclusief [!DNL Azure Event Hubs].

Voor [!DNL Azure Event Hubs] bestemmingen, ga de volgende informatie in creeer bestemmingswerkschema in:

### In de stap Verificatie {#authentication-step}

* **[!UICONTROL SAS-sleutelnaam]** en **[!UICONTROL SAS-sleutel]**: Vul uw SAS-sleutelnaam en -sleutel in. Meer informatie over verificatie [!DNL Azure Event Hubs] met SAS-toetsen vindt u in de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Naamruimte]**: Vul de [!DNL Azure Event Hubs] naamruimte in. Meer informatie over [!DNL Azure Event Hubs] naamruimten vindt u in de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Invoer vereist in de verificatiestap](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### In de stap Setup {#setup-step}

* **[!UICONTROL Naam]**: Geef een naam op voor de verbinding met [!DNL Azure Event Hubs].
* **[!UICONTROL Omschrijving]**: Geef een beschrijving van de verbinding op.  Voorbeelden: &quot;Klanten met de hoogste rang&quot;, &quot;Males die geïnteresseerd zijn in keukenvorming&quot;.
* **[!UICONTROL eventHubName]**: Geef een naam voor de stream op naar het [!DNL Azure Event Hubs] doel.

![Gegevens vereist in de installatiestap](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.


## Geëxporteerde gegevens {#exported-data}

De geëxporteerde [!DNL Experience Platform] gegevens worden in JSON- [!DNL Azure Event Hubs] indeling opgeslagen. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

```
{
  "person": {
    "email": "yourstruly@adobe.con"
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
>* [Verbind met Azure Event Hubs en activeer gegevens gebruikend API vraag](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [AWS Kinesis-bestemming](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Doeltypen en -categorieën](/help/rtcdp/destinations/destination-types.md)