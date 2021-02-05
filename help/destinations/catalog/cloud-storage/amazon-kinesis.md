---
keywords: Amazon Kinesis;kinesis-bestemming;kinesis
title: Amazon Kinesis Connection Destination
description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens vanuit Adobe Experience Platform te streamen.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# (Bèta) [!DNL Amazon Kinesis] verbinding

>[!IMPORTANT]
>
>De [!DNL Amazon Kinesis] bestemming in Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

Met de [!DNL Kinesis Data Streams]-service van [!DNL Amazon Web Services] kunt u grote stromen gegevensrecords in real-time verzamelen en verwerken.

U kunt een uitgaande verbinding in real time met uw [!DNL Amazon Kinesis]-opslag maken om gegevens vanuit Adobe Experience Platform te streamen.

* Raadpleeg de [Amazon-documentatie](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) voor meer informatie over [!DNL Amazon Kinesis].
* Als u verbinding wilt maken met [!DNL Amazon Kinesis] via API-aanroepen, raadpleegt u de [API-zelfstudie voor streaming doelen](../../api/streaming-destinations.md).
* Zie de onderstaande secties als u verbinding wilt maken met [!DNL Amazon Kinesis] via de gebruikersinterface van het Platform.

![Amazon Kinesis in de gebruikersinterface](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Gevallen {#use-cases} gebruiken

Door het stromen bestemmingen zoals [!DNL Amazon Kinesis] te gebruiken, kunt u high-value segmenteringsgebeurtenissen en bijbehorende profielattributen in uw systemen van keus gemakkelijk invoeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan [!DNL Amazon Kinesis] bestemming valt, zou u deze gebeurtenis in [!DNL Amazon Kinesis] ontvangen. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Doel {#connect-destination} verbinden

Zie [Workflow ](./workflow.md)voor cloudopslagdoelen voor instructies voor het maken van een verbinding met uw cloudopslagdoelen, inclusief de doelen die worden ondersteund door [!DNL Amazon].

Voor [!DNL Amazon Kinesis] bestemmingen, ga de volgende informatie in tot bestemmingswerkschema:

### In de stap van de Authentificatie {#authentication-step}

* **[!DNL Amazon Web Services]toegangssleutel en geheime sleutel**: In  [!DNL Amazon Web Services], produceer een  `access key - secret access key` paar om Platform toegang tot uw  [!DNL Amazon Kinesis] rekening te verlenen. Meer informatie vindt u in de [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **regio**: Geef aan naar welk  [!DNL Amazon Web Services] gebied gegevens moeten worden gestreamd.

![Invoervelden in de stap van de account](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### In de stap {#setup-step}

* **Naam**: Geef een naam op voor uw verbinding met  [!DNL Amazon Kinesis]
* **Omschrijving**: Geef een beschrijving op voor de verbinding met  [!DNL Amazon Kinesis].
* **stream**: Geef de naam op van een bestaande gegevensstroom in uw  [!DNL Amazon Kinesis] account. Platform exporteert gegevens naar deze stream.

![Invoervelden in de verificatiestap](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform]-gegevens worden in de JSON-indeling [!DNL Amazon Kinesis] geplaatst. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

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

