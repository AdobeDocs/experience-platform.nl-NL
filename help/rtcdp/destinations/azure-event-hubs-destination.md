---
title: (Beta) Azure Event Hubs-bestemming
seo-title: (Beta) Azure Event Hubs-bestemming
description: Creeer een uitgaande verbinding in real time aan uw opslag van de Hubs van de Azure Gebeurtenis aan stroomgegevens van het Platform van de Ervaring.
seo-description: Creeer een uitgaande verbinding in real time aan uw opslag van de Hubs van de Azure Gebeurtenis aan stroomgegevens van het Platform van de Ervaring.
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# (Beta) Azure Event Hubs-bestemming

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] bestemming in Echte Adobe CDP in tijd is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

[!DNL Azure Event Hubs] is een groot platform voor gegevensstreaming en service voor het opnemen van gebeurtenissen. Het kan miljoenen gebeurtenissen per seconde ontvangen en verwerken. Gegevens die naar een gebeurtenishub worden verzonden, kunnen worden getransformeerd en opgeslagen met behulp van een realtime analyseprovider of batchadapters.

U kunt een uitgaande verbinding in real time met uw [!DNL Azure Event Hubs] opslag maken om gegevens te streamen vanaf het Adobe Experience Platform.

* Voor meer informatie over [!DNL Azure Event Hubs], zie de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Zie de zelfstudie over de API- [!DNL Azure Event Hubs] streamingdoelen als u verbinding wilt maken met het [gebruik van API-aanroepen](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md).
* Zie de onderstaande secties voor [!DNL Azure Event Hubs] het maken van een verbinding met de Adobe Real-Time CDP-gebruikersinterface.

![AWS Kinesis in de gebruikersinterface](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Gevallen gebruiken {#use-cases}

Door het stromen bestemmingen zoals de Hubs van de Gebeurtenis van de Azure te gebruiken, kunt u high-value segmenteringsgebeurtenissen en bijbehorende profielattributen in uw systemen van keus gemakkelijk voeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan de Azure bestemming van de Hubs van de Gebeurtenis valt, zou u deze gebeurtenis in de Hubs van de Gebeurtenis van Azure ontvangen. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloud-opslagdoelen ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)voor instructies over het maken van een verbinding met uw cloudopslagdoelen, inclusief [!DNL Azure Event Hubs].

Voor [!DNL Azure Event Hubs] bestemmingen, ga de volgende informatie in creeer bestemmingswerkschema in:

### In de stap Account {#account-step}

* **[!UICONTROL SAS-sleutelnaam]** en **[!UICONTROL SAS-sleutel]**: Vul uw SAS-sleutelnaam en -sleutel in. Meer informatie over verificatie [!DNL Azure Event Hubs] met SAS-toetsen vindt u in de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Naamruimte]**: Vul de [!DNL Azure Event Hubs] naamruimte in. Meer informatie over [!DNL Azure Event Hubs] naamruimten vindt u in de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Invoer vereist in de verificatiestap](/help/rtcdp/destinations/assets/event-hubs-account-step.png)

### In de stap Verificatie {#authentication-step}

* **[!UICONTROL Naam]**: Geef een naam op voor de verbinding met [!DNL Azure Event Hubs].
* **[!UICONTROL Omschrijving]**: Geef een beschrijving van de verbinding op.  Voorbeelden: &quot;Klanten met de hoogste rang&quot;, &quot;Males die geïnteresseerd zijn in keukenvorming&quot;.
* **[!UICONTROL eventHubName]**: Geef een naam voor de stream op naar het [!DNL Azure Event Hubs] doel.

![Gegevens vereist in de installatiestap](/help/rtcdp/destinations/assets/event-hubs-authentication-step.png)

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.


## Geëxporteerde gegevens {#exported-data}

De gegevens van uw geëxporteerde Experience Platform worden opgeslagen in [!DNL Azure Event Hubs] de JSON-indeling. Een gebeurtenisstream met de gehashte e-mailidentiteit van een publiek dat een bepaald segment heeft verlaten, zou er bijvoorbeeld als volgt kunnen uitzien:

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* [Verbind met Azure Event Hubs en activeer gegevens gebruikend API vraag](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [AWS Kinesis-bestemming](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Doeltypen en -categorieën](/help/rtcdp/destinations/destination-types.md)