---
keywords: Amazon Kinesis;kinesis-bestemming;kinesis
title: Amazon Kinesis-verbinding
description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens vanuit Adobe Experience Platform te streamen.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
> Deze bestemming is alleen beschikbaar voor [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

De [!DNL Kinesis Data Streams] service door [!DNL Amazon Web Services] Hiermee kunt u grote stromen gegevensrecords in real-time verzamelen en verwerken.

U kunt een uitgaande verbinding in real time aan uw creëren [!DNL Amazon Kinesis] opslag om gegevens uit Adobe Experience Platform te streamen.

* Voor meer informatie over [!DNL Amazon Kinesis], zie de [Amazon-documentatie](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Verbinding maken met [!DNL Amazon Kinesis] programmatically, zie [Zelfstudie voor Streaming doelen-API](../../api/streaming-destinations.md).
* Verbinding maken met [!DNL Amazon Kinesis] in de gebruikersinterface van Platform raadpleegt u de onderstaande secties.

![Amazon Kinesis in de gebruikersinterface](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Gebruiksscenario’s {#use-cases}

Door streamingdoelen zoals [!DNL Amazon Kinesis]kunt u bovendien gemakkelijk hoogwaardige segmentatiegebeurtenissen en de bijbehorende profielkenmerken in uw eigen systemen importeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het publiek in kaart te brengen dat het vooruitzicht binnen aan [!DNL Amazon Kinesis] doel, ontvangt u deze gebeurtenis in [!DNL Amazon Kinesis]. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#ip-address-allowlist}

Om klanten&#39; veiligheid en nalevingsvereisten te ontmoeten, verstrekt het Experience Platform een lijst van statische IPs die u lijst van gewenste personen voor kunt [!DNL Amazon Kinesis] bestemming. Zie [IP adres lijst van gewenste personen voor het stromen bestemmingen](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor de volledige lijst van IPs aan lijst van gewenste personen.

## Vereist [!DNL Amazon Kinesis] machtigingen {#required-kinesis-permission}

Om gegevens met succes te verbinden en uit te voeren aan uw [!DNL Amazon Kinesis] streams, Experience Platform heeft machtigingen nodig voor de volgende handelingen:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Deze machtigingen worden via de [!DNL Kinesis] -console en worden gecontroleerd door Platform nadat u uw Kinesis-bestemming hebt geconfigureerd in de gebruikersinterface van Platform.

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

{style="table-layout:auto"}

Voor meer informatie over het beheren van toegang voor [!DNL Kinesis] gegevensstromen, lees het volgende [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Wanneer u verbinding maakt met dit doel, moet u de volgende informatie opgeven:

### Verificatiegegevens {#authentication-information}

Voer de onderstaande velden in en selecteer **[!UICONTROL Connect to destination]**:

![Afbeelding van het UI-scherm met de voltooide velden voor de Amazon Kinesis-verificatiedetails](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]toegangssleutel en geheime sleutel**: In [!DNL Amazon Web Services], een `access key - secret access key` paar om Platform toegang tot uw te verlenen [!DNL Amazon Kinesis] account. Meer informatie in het dialoogvenster [Amazon Web Services-documentatie](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Region]**: aangeven welke [!DNL Amazon Web Services] gebied waarnaar gegevens moeten worden gestreamd.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="Segmentnamen opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen worden opgenomen van het publiek dat u exporteert. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="Tijdstempels segment opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de UNIX-tijdstempel wordt opgenomen wanneer het publiek is gemaakt en bijgewerkt, en ook de UNIX-tijdstempel wanneer het publiek voor activering aan de bestemming is toegewezen. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Afbeelding van het UI-scherm met de voltooide velden voor de Amazon Kinesis-doelgegevens](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL Name]**: Geef een naam op voor uw verbinding met [!DNL Amazon Kinesis]
* **[!UICONTROL Description]**: Geef een beschrijving op voor uw verbinding met [!DNL Amazon Kinesis].
* **[!UICONTROL Stream]**: Geef de naam op van een bestaande gegevensstroom in uw [!DNL Amazon Kinesis] account. Platform zal gegevens naar deze stroom uitvoeren.
* **[!UICONTROL Include Segment Names]**: Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen worden opgenomen van het publiek dat u exporteert. Voor een voorbeeld van een gegevensexport waarbij deze optie is geselecteerd, raadpleegt u de [Geëxporteerde gegevens](#exported-data) hieronder.
* **[!UICONTROL Include Segment Timestamps]**: Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de UNIX-tijdstempel wordt gebruikt wanneer het publiek is gemaakt en bijgewerkt, en ook de UNIX-tijdstempel wanneer het publiek voor activering aan de bestemming is toegewezen. Voor een voorbeeld van een gegevensexport waarbij deze optie is geselecteerd, raadpleegt u de [Geëxporteerde gegevens](#exported-data) hieronder.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](../../ui/activate-streaming-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw [!DNL Amazon Kinesis] doel, om alleen gegevens naar uw bestemming te exporteren wanneer relevante updates naar een profiel zijn opgetreden na kwalificatie van het publiek of andere belangrijke gebeurtenissen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een wijziging in het publiekslidmaatschap voor ten minste een van de doelgroepen. Het profiel is bijvoorbeeld gekwalificeerd voor een van de soorten publiek die aan de bestemming zijn toegewezen of heeft een van de soorten publiek afgesloten die aan de bestemming zijn toegewezen.
* De profielupdate is bepaald door een wijziging in het dialoogvenster [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de soorten publiek dat aan de bestemming is toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een publiek dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten van *wat bepalend is voor het exporteren van gegevens naar uw [!DNL Amazon Kinesis] doel* en *welke gegevens in de uitvoer worden opgenomen*.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en doelgroepen fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als een toegewezen publiek de status wijzigt (van `null` tot `realized` of van `realized` tot `exiting`) of toegewezen kenmerken worden bijgewerkt, wordt een doelexport uitgeschakeld.</li><li>Omdat identiteiten momenteel niet kunnen worden toegewezen aan [!DNL Amazon Kinesis] doelen, wijzigingen in een identiteit in een bepaald profiel bepalen ook de export van de bestemming.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>De `segmentMembership` bevat het publiek dat is toegewezen in de activeringsgegevensstroom, waarvoor de status van het profiel is gewijzigd na een afsluitgebeurtenis voor kwalificatie of het publiek. Andere niet-toegewezen soorten publiek waarvoor het profiel waarvoor is gekwalificeerd, deel kan uitmaken van de doelexport, als deze soorten publiek tot hetzelfde behoren [samenvoegingsbeleid](/help/profile/merge-policies/overview.md) als het publiek is toegewezen in de activeringsgegevensstroom. </li><li>Alle identiteiten in de `identityMap` object wordt ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de [!DNL Amazon Kinesis] bestemming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style="table-layout:fixed"}

Neem bijvoorbeeld deze gegevensstroom naar een [!DNL Amazon Kinesis] doel waar drie publiek in dataflow wordt geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![Amazon Kinesis-doeldatabase](../../assets/catalog/http/profile-export-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de *drie toegewezen segmenten*. Bij de gegevensexport moet u echter in de `segmentMembership` object (zie [Geëxporteerde gegevens](#exported-data) in de onderstaande sectie), kunnen andere niet-toegewezen doelgroepen worden weergegeven als dat specifieke profiel lid van die doelgroepen is en als deze hetzelfde samenvoegingsbeleid delen als het publiek dat de exportactie heeft geactiveerd. Als een profiel voor het **Klant met DeLorean Auto&#39;s** publiek maar ook lid van **&quot;Terug naar de toekomst&quot;** film en **Favorieten voor science fiction** publiek , dan zullen deze twee andere doelgroepen ook aanwezig zijn in de `segmentMembership` -object van de gegevensexport, ook al worden deze niet toegewezen in de gegevensstroom, als deze hetzelfde samenvoegbeleid delen met de **Klant met DeLorean Auto&#39;s** segment.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

## Back-up van historische gegevens {#historical-data-backfill}

Wanneer u een nieuw publiek aan een bestaande bestemming toevoegt, of wanneer u een nieuw doel en kaartpubliek aan het creeert, voert het Experience Platform historische gegevens van de publiekskwalificatie naar de bestemming uit. Profielen die in aanmerking komen voor het publiek *voor* het publiek dat aan de bestemming is toegevoegd, wordt binnen ongeveer een uur naar de bestemming geëxporteerd.

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

Hieronder vindt u meer voorbeelden van geëxporteerde gegevens, afhankelijk van de UI-instellingen die u hebt geselecteerd in de doelstroom voor het verbinden van **[!UICONTROL Include Segment Names]** en **[!UICONTROL Include Segment Timestamps]** opties:

+++ In het onderstaande voorbeeld voor het exporteren van gegevens worden publieksnamen opgenomen in het deelvenster `segmentMembership` sectie

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ Het onderstaande voorbeeld voor het exporteren van gegevens bevat tijdstempels voor het publiek in het dialoogvenster `segmentMembership` sectie

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Beperkingen en beleid opnieuw proberen {#limits-retry-policy}

In 95 percent van de tijd, probeert het Experience Platform om een productietolerantie van minder dan 10 minuten voor met succes verzonden berichten met een tarief van minder dan 10.000 verzoeken per seconde voor elke dataflow aan een bestemming van HTTP aan te bieden.

In het geval van ontbroken verzoeken aan uw bestemming van HTTP API, slaat het Experience Platform de ontbroken verzoeken op en probeert tweemaal om de verzoeken naar uw eindpunt te verzenden.

>[!MORELIKETHIS]
>
>* [Verbinding maken met Amazon Kinesis en gegevens activeren met de Flow Service API](../../api/streaming-destinations.md)
>* [Azure Event Hubs-bestemming](./azure-event-hubs.md)
>* [Doeltypen en -categorieën](../../destination-types.md)
