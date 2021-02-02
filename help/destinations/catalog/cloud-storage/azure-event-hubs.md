---
keywords: Azure-gebeurtenishub-bestemming;azure-gebeurtenishub;azure-eventhub
title: (Beta) Azure Event Hubs-bestemming
seo-title: (Beta) Azure Event Hubs-bestemming
description: Creeer een uitgaande verbinding in real time aan uw opslag van de Hubs van de Azure Gebeurtenis aan stroomgegevens van Experience Platform.
seo-description: Creeer een uitgaande verbinding in real time aan uw opslag van de Hubs van de Azure Gebeurtenis aan stroomgegevens van Experience Platform.
translation-type: tm+mt
source-git-commit: 97c0a9f4726ec85b7a72dc682fbd201a6152c1ba
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# (Bèta) [!DNL Azure Event Hubs] bestemming

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] bestemming in Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

[!DNL Azure Event Hubs] is een groot platform voor gegevensstreaming en service voor het opnemen van gebeurtenissen. Het kan miljoenen gebeurtenissen per seconde ontvangen en verwerken. Gegevens die naar een gebeurtenishub worden verzonden, kunnen worden getransformeerd en opgeslagen met behulp van een realtime analyseprovider of batchadapters.

U kunt een uitgaande verbinding in real time met uw [!DNL Azure Event Hubs]-opslag maken om gegevens vanuit Adobe Experience Platform te streamen.

* Voor meer informatie over [!DNL Azure Event Hubs], zie [de documentatie van Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Als u verbinding wilt maken met [!DNL Azure Event Hubs] via API-aanroepen, raadpleegt u de [API-zelfstudie voor streaming doelen](../../api/streaming-destinations.md).
* Zie de onderstaande secties als u verbinding wilt maken met [!DNL Azure Event Hubs] via de gebruikersinterface van het Platform.

![AWS Kinesis in de gebruikersinterface](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Gevallen {#use-cases} gebruiken

Door het stromen bestemmingen zoals [!DNL Azure Event Hubs] te gebruiken, kunt u high-value segmenteringsgebeurtenissen en bijbehorende profielattributen in uw systemen van keus gemakkelijk invoeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan [!DNL Azure Event Hubs] bestemming valt, zou u deze gebeurtenis in [!DNL Azure Event Hubs] ontvangen. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Doel {#connect-destination} verbinden

Zie [Workflow ](./workflow.md)voor cloudopslagdoelen voor instructies voor het maken van een verbinding met uw cloudopslagdoelen, inclusief [!DNL Azure Event Hubs].

Voor [!DNL Azure Event Hubs] bestemmingen, ga de volgende informatie in tot bestemmingswerkschema:

### In de stap van de Authentificatie {#authentication-step}

* **[!UICONTROL SAS-sleutelnaam]** en  **[!UICONTROL SAS-sleutel]**: Vul uw SAS-sleutelnaam en -sleutel in. Meer informatie over het verifiëren van [!DNL Azure Event Hubs] met SAS sleutels in [de documentatie van Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Naamruimte]**: Vul de  [!DNL Azure Event Hubs] naamruimte in. Meer informatie over [!DNL Azure Event Hubs] naamruimten in de [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Invoer vereist in de verificatiestap](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

### In de stap {#setup-step}

* **[!UICONTROL Naam]**: Geef een naam op voor de verbinding met  [!DNL Azure Event Hubs].
* **[!UICONTROL Omschrijving]**: Geef een beschrijving van de verbinding op.  Voorbeelden: &quot;Klanten met de hoogste rang&quot;, &quot;Males die geïnteresseerd zijn in keukenvorming&quot;.
* **[!UICONTROL eventHubName]**: Geef een naam voor de stream op naar uw  [!DNL Azure Event Hubs] bestemming.

![Gegevens vereist in de installatiestap](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform]-gegevens worden in de JSON-indeling [!DNL Azure Event Hubs] geplaatst. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

```json
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
>* [Verbind met Azure Event Hubs en activeer gegevens gebruikend API vraag](../../api/streaming-destinations.md)
>* [AWS Kinesis-bestemming](./amazon-kinesis.md)
>* [Doeltypen en -categorieën](../../destination-types.md)