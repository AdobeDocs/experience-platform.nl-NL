---
title: Amazon Kinesis-bestemming
seo-title: Amazon Kinesis-bestemming
description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens te streamen van het Adobe Experience Platform.
seo-description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens te streamen van het Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 883bea4aba0548e96b891987f17b8535c4d2eba7
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# (bèta) Amazon Kinesis-bestemming


>[!IMPORTANT]
>
>De [!DNL Amazon Kinesis] bestemming in Echte Adobe CDP in tijd is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

Met de [!DNL Kinesis Data Streams] service van Amazon Web Services kunt u grote stromen gegevensrecords in real-time verzamelen en verwerken.

U kunt een uitgaande verbinding in real time met uw [!DNL Amazon Kinesis] opslag maken om gegevens te streamen vanaf het Adobe Experience Platform.

* Raadpleeg de documentatie bij [!DNL Amazon Kinesis][Amazon voor meer informatie over](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)het programma.
* Zie de zelfstudie over de API- [!DNL Amazon Kinesis] streamingdoelen als u verbinding wilt maken met het [gebruik van API-aanroepen](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md).
* Zie de onderstaande secties voor [!DNL Amazon Kinesis] het maken van een verbinding met de Adobe Real-Time CDP-gebruikersinterface.

![Amazon Kinesis in de gebruikersinterface](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Gevallen gebruiken {#use-cases}

Door streamingdoelen zoals Amazon Kinesis te gebruiken, kunt u eenvoudig hoogwaardige segmentatiegebeurtenissen en de bijbehorende profielkenmerken in uw systemen van keuze doorgeven.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan de bestemming van Amazon Kinesis valt, zou u deze gebeurtenis in Amazon Kinesis ontvangen. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloud-opslagdoelen ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)voor instructies over het maken van een verbinding met uw cloudopslagdoelen, inclusief de doelen die worden ondersteund door [!DNL Amazon].

Voor [!DNL Amazon Kinesis] bestemmingen, ga de volgende informatie in creeer bestemmingswerkschema in:

### In de stap Account {#account-step}

* **Toegangssleutel en geheime sleutel** voor Amazon Web Services: In [!DNL Amazon Web Services], produceer een toegangstoets - geheim toegangszeer belangrijke paar om Adobe in real time CDP toegang tot uw [!DNL Amazon Kinesis] rekening te verlenen. Meer informatie vindt u in de documentatie [van](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon Web Services.
* **regio**: Geef aan naar welk [!DNL Amazon Web Services] gebied gegevens moeten worden gestreamd.

![Invoervelden in de stap van de account](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### In de stap Verificatie {#authentication-step}

* **Naam**: Geef een naam op voor uw verbinding met [!DNL Amazon Kinesis]
* **Omschrijving**: Geef een beschrijving op voor de verbinding met [!DNL Amazon Kinesis].
* **stream**: Geef de naam op van de bestaande gegevensstroom in uw [!DNL Amazon Kinesis] account. Adobe Real-time CDP exporteert gegevens naar deze stream.

![Invoervelden in de verificatiestap](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Geëxporteerde gegevens {#exported-data}

De gegevens van uw geëxporteerde Experience Platform worden opgeslagen in [!DNL Amazon Kinesis] de JSON-indeling. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

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
>* [Verbinding maken met Amazon Kinesis en gegevens activeren via API-aanroepen](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Azure Event Hubs-bestemming](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Doeltypen en -categorieën](/help/rtcdp/destinations/destination-types.md)

