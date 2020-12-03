---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: Amazon Kinesis-bestemming
seo-title: Amazon Kinesis-bestemming
description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens vanuit Adobe Experience Platform te streamen.
seo-description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens vanuit Adobe Experience Platform te streamen.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# (Beta) [!DNL Amazon Kinesis] bestemming


>[!IMPORTANT]
>
>De [!DNL Amazon Kinesis] bestemming in real time CDP is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

De [!DNL Kinesis Data Streams] dienst door [!DNL Amazon Web Services] staat u toe om grote stromen gegevensverslagen in echt te verzamelen en te verwerken.

U kunt een uitgaande verbinding in real time met uw [!DNL Amazon Kinesis] opslag maken om gegevens vanuit Adobe Experience Platform te streamen.

* Raadpleeg de documentatie bij [!DNL Amazon Kinesis][Amazon voor meer informatie over](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)het programma.
* Zie de zelfstudie over de API- [!DNL Amazon Kinesis] streamingdoelen als u verbinding wilt maken met het [gebruik van API-aanroepen](../../api/streaming-destinations.md).
* Zie de onderstaande secties om verbinding te maken met de CDP-gebruikersinterface in real time [!DNL Amazon Kinesis] .

![Amazon Kinesis in de gebruikersinterface](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)


## Use Cases {#use-cases}

Door het stromen bestemmingen zoals te gebruiken [!DNL Amazon Kinesis], kunt u high-value segmenteringsgebeurtenissen en bijbehorende profielattributen in uw systemen van keus gemakkelijk invoeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan de [!DNL Amazon Kinesis] bestemming valt, zou u deze gebeurtenis binnen ontvangen [!DNL Amazon Kinesis]. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Exporttype {#export-type}

**Op profiel gebaseerd** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloud-opslagdoelen ](./workflow.md)voor instructies over het maken van een verbinding met uw cloudopslagdoelen, inclusief de doelen die worden ondersteund door [!DNL Amazon].

Voor [!DNL Amazon Kinesis] bestemmingen, ga de volgende informatie in creeer bestemmingswerkschema in:

### In de stap Verificatie {#authentication-step}

* **[!DNL Amazon Web Services]toegangssleutel en geheime sleutel**: In [!DNL Amazon Web Services], produceer een `access key - secret access key` paar om toegang in real time CDP tot uw [!DNL Amazon Kinesis] rekening te verlenen. Meer informatie vindt u in de documentatie [van](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon Web Services.
* **regio**: Geef aan naar welk [!DNL Amazon Web Services] gebied gegevens moeten worden gestreamd.

![Invoervelden in de stap van de account](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### In de stap Setup {#setup-step}

* **Naam**: Geef een naam op voor uw verbinding met [!DNL Amazon Kinesis]
* **Omschrijving**: Geef een beschrijving op voor de verbinding met [!DNL Amazon Kinesis].
* **stream**: Geef de naam op van een bestaande gegevensstroom in uw [!DNL Amazon Kinesis] account. CDP in realtime exporteert gegevens naar deze stream.

![Invoervelden in de verificatiestap](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Geëxporteerde gegevens {#exported-data}

De geëxporteerde [!DNL Experience Platform] gegevens worden in JSON- [!DNL Amazon Kinesis] indeling opgeslagen. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

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
>* [Verbinding maken met Amazon Kinesis en gegevens activeren via API-aanroepen](../../api/streaming-destinations.md)
>* [Azure Event Hubs-bestemming](./azure-event-hubs.md)
>* [Doeltypen en -categorieën](../../destination-types.md)

