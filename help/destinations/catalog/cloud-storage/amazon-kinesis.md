---
keywords: Amazon Kinesis;kinesis-bestemming;kinesis
title: (Beta) Amazon Kinesis-verbinding
description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens vanuit Adobe Experience Platform te streamen.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: b2ac26589527313ec9f3cf84126e3e23da6c7b83
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---

# (bèta) [!DNL Amazon Kinesis] verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
>De [!DNL Amazon Kinesis] doel in Platform is momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

De [!DNL Kinesis Data Streams] service door [!DNL Amazon Web Services] Hiermee kunt u grote stromen gegevensrecords in real-time verzamelen en verwerken.

U kunt een uitgaande verbinding in real time aan uw creëren [!DNL Amazon Kinesis] opslag om gegevens uit Adobe Experience Platform te streamen.

* Meer informatie over [!DNL Amazon Kinesis], zie de [Amazon-documentatie](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Verbinding maken met [!DNL Amazon Kinesis] programmatically, zie [Zelfstudie voor Streaming doelen-API](../../api/streaming-destinations.md).
* Verbinding maken met [!DNL Amazon Kinesis] in de gebruikersinterface van het Platform raadpleegt u de onderstaande secties.

![Amazon Kinesis in de gebruikersinterface](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Gebruiksscenario’s {#use-cases}

Door streamingdoelen zoals [!DNL Amazon Kinesis]kunt u bovendien gemakkelijk hoogwaardige segmentatiegebeurtenissen en de bijbehorende profielkenmerken in uw eigen systemen importeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan [!DNL Amazon Kinesis] doel, ontvangt u deze gebeurtenis in [!DNL Amazon Kinesis]. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## IP adres lijst van gewenste personen {#ip-address-allowlist}

Om klanten&#39; veiligheid en nalevingsvereisten te ontmoeten, verstrekt het Experience Platform een lijst van statische IPs die u lijst van gewenste personen voor kunt [!DNL Amazon Kinesis] bestemming. Zie [IP adres lijst van gewenste personen voor het stromen bestemmingen](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor de volledige lijst van IPs aan lijst van gewenste personen.

## Vereist [!DNL Amazon Kinesis] machtigingen {#required-kinesis-permission}

Om gegevens met succes te verbinden en uit te voeren aan uw [!DNL Amazon Kinesis] streams, Experience Platform heeft machtigingen nodig voor de volgende handelingen:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Deze machtigingen worden gerangschikt via de [!DNL Kinesis] -console en worden gecontroleerd door Platform als u de Kinesis-bestemming hebt geconfigureerd in de gebruikersinterface van het Platform.

In het onderstaande voorbeeld worden de minimale toegangsrechten weergegeven die vereist zijn om gegevens naar een [!DNL Kinesis] bestemming.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `kinesis:ListStreams` | Een handeling waarmee uw Amazon Kinesis-gegevensstromen worden vermeld. |
| `kinesis:PutRecord` | Een handeling waarmee één gegevensrecord in een Kinesis-gegevensstroom wordt geschreven. |
| `kinesis:PutRecords` | Een handeling die meerdere gegevensrecords in één aanroep naar een Kinesis-gegevensstroom schrijft. |

Voor meer informatie over het beheren van toegang voor [!DNL Kinesis] gegevensstromen, lees het volgende [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!DNL Amazon Web Services]toegangssleutel en geheime sleutel**: In [!DNL Amazon Web Services], een `access key - secret access key` paar om Platform toegang tot uw te verlenen [!DNL Amazon Kinesis] account. Meer informatie in het dialoogvenster [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **regio**: Vermeld welke [!DNL Amazon Web Services] gebied waarnaar gegevens moeten worden gestreamd.
* **Naam**: Geef een naam op voor uw verbinding met [!DNL Amazon Kinesis]
* **Beschrijving**: Geef een beschrijving op voor uw verbinding met [!DNL Amazon Kinesis].
* **stream**: Geef de naam op van een bestaande gegevensstroom in uw [!DNL Amazon Kinesis] account. Platform exporteert gegevens naar deze stream.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](../../ui/activate-streaming-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw [!DNL Amazon Kinesis] doel, om gegevens naar uw bestemming slechts uit te voeren wanneer de relevante updates aan een profiel na segmentkwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een verandering in segmentlidmaatschap voor minstens één van de segmenten in kaart gebracht aan de bestemming. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is bepaald door een wijziging in het dialoogvenster [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten van *wat bepalend is voor het exporteren van gegevens naar uw [!DNL Amazon Kinesis] doel* en *welke gegevens in de uitvoer worden opgenomen*.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als om het even welke in kaart gebrachte segmenten staten (van ongeldig aan gerealiseerd of van gerealiseerde/bestaande aan het weggaan) veranderen of om het even welke in kaart gebrachte attributen worden bijgewerkt, een bestemmingsuitvoer zou worden weggeduwd.</li><li>Omdat identiteiten momenteel niet kunnen worden toegewezen aan [!DNL Amazon Kinesis] doelen, wijzigingen in een identiteit in een bepaald profiel bepalen ook de export van de bestemming.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Alle segmenten (met de nieuwste lidmaatschapsstatus), ongeacht of ze in de dataflow zijn toegewezen of niet, worden opgenomen in de `segmentMembership` object.</li><li>Alle identiteiten in de `identityMap` object wordt ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de [!DNL Amazon Kinesis] bestemming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Neem bijvoorbeeld deze gegevensstroom naar een [!DNL Amazon Kinesis] doel waar drie segmenten in dataflow worden geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![Amazon Kinesis-doeldatabase](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de *drie toegewezen segmenten*. Bij de gegevensexport moet u `segmentMembership` object (zie [Geëxporteerde gegevens](#exported-data) (zie hieronder), zouden andere niet in kaart gebrachte segmenten kunnen verschijnen, als dat bepaalde profiel een lid van hen is. Als een profiel in aanmerking komt voor de klant met het segment DeLorean Cars, maar ook lid is van de segmenten &quot;Terug naar de toekomst&quot; film en science fiction, dan zullen deze andere twee segmenten ook aanwezig zijn in de `segmentMembership` -object van de gegevensexport, ook al worden deze niet toegewezen in de gegevensstroom.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform] gegevensterreinen in uw [!DNL Amazon Kinesis] doel in JSON-indeling. Bijvoorbeeld, bevat de hieronder uitvoer een profiel dat voor een bepaald segment heeft gekwalificeerd, een lid van andere twee segmenten is, en een ander segment verliet. Het exporteren bevat ook de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

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
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
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
>* [Verbinding maken met Amazon Kinesis en gegevens activeren met de Flow Service API](../../api/streaming-destinations.md)
>* [Azure Event Hubs-bestemming](./azure-event-hubs.md)
>* [Doeltypen en -categorieën](../../destination-types.md)

