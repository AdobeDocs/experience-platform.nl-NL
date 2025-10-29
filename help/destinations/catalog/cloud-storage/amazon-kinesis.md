---
keywords: Amazon Kinesis;kinesis, doel;kinesis
title: Amazon Kinesis-verbinding
description: Maak een real-time uitgaande verbinding met uw Amazon Kinesis-opslag om gegevens vanuit Adobe Experience Platform te streamen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 0%

---

# [!DNL Amazon Kinesis]-verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
> Deze bestemming is beschikbaar slechts aan [&#x200B; Adobe Real-Time Customer Data Platform Ultimate &#x200B;](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

Met de [!DNL Kinesis Data Streams] -service van [!DNL Amazon Web Services] kunt u grote stromen gegevensrecords in real-time verzamelen en verwerken.

U kunt een real-time uitgaande verbinding maken met uw [!DNL Amazon Kinesis] -opslag om gegevens vanuit Adobe Experience Platform te streamen.

* Voor meer informatie over [!DNL Amazon Kinesis], zie de [&#x200B; documentatie van Amazon &#x200B;](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Om met [!DNL Amazon Kinesis] programmatically te verbinden, zie de [&#x200B; Streaming bestemmingen API leerprogramma &#x200B;](../../api/streaming-destinations.md).
* Zie de volgende secties als u verbinding wilt maken met [!DNL Amazon Kinesis] via de Experience Platform-gebruikersinterface.

![&#x200B; Kinesis van Amazon in UI &#x200B;](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Gebruiksscenario’s {#use-cases}

Door het stromen bestemmingen zoals [!DNL Amazon Kinesis] te gebruiken, kunt u high-value segmenteringsgebeurtenissen en bijbehorende profielattributen in uw systemen van keus gemakkelijk invoeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Als u het publiek in kaart brengt dat het vooruitzicht naar het [!DNL Amazon Kinesis] -doel valt, ontvangt u deze gebeurtenis in [!DNL Amazon Kinesis] . Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#ip-address-allowlist}

Experience Platform biedt een lijst met statische IP&#39;s die u kunt lijsten van gewenste personen voor de [!DNL Amazon Kinesis] -bestemming om aan de beveiligings- en compatibiliteitsvereisten van klanten te voldoen. Verwijs naar [&#x200B; IP adreslijst van gewenste personen voor het stromen bestemmingen &#x200B;](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor de volledige lijst van IPs aan lijst van gewenste personen.

## Vereiste [!DNL Amazon Kinesis] machtigingen {#required-kinesis-permission}

Experience Platform heeft machtigingen nodig voor de volgende handelingen om gegevens te kunnen verbinden en exporteren naar uw [!DNL Amazon Kinesis] -streams:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Deze machtigingen worden gerangschikt via de [!DNL Kinesis] -console en worden gecontroleerd door Experience Platform nadat u uw Kinesis-bestemming hebt geconfigureerd in de Experience Platform-gebruikersinterface.

In het onderstaande voorbeeld worden de minimale toegangsrechten weergegeven die zijn vereist om gegevens te kunnen exporteren naar een [!DNL Kinesis] -doel.

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
| `kinesis:PutRecord` | Een handeling die één gegevensrecord naar een Kinesis-gegevensstroom schrijft. |
| `kinesis:PutRecords` | Een actie die veelvoudige gegevensverslagen in een de gegevensstroom van Kinesis in één enkele vraag schrijft. |

{style="table-layout:auto"}

Voor meer informatie bij het controleren van toegang voor [!DNL Kinesis] gegevensstromen, lees het volgende [[!DNL Kinesis]  document &#x200B;](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. Wanneer u verbinding maakt met dit doel, moet u de volgende informatie opgeven:

### Verificatiegegevens {#authentication-information}

Voer de onderstaande velden in en selecteer **[!UICONTROL Connect to destination]** :

![&#x200B; Beeld van het scherm UI die voltooide gebieden voor de de authentificatiedetails van Kinesis van Amazon tonen &#x200B;](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]toegangstoets en geheime sleutel** : genereer in [!DNL Amazon Web Services] een `access key - secret access key` paar om Experience Platform toegang te verlenen tot uw [!DNL Amazon Kinesis] -account. Leer meer in de [&#x200B; documentatie van Amazon Web Services &#x200B;](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Region]**: geef aan naar welk [!DNL Amazon Web Services] -gebied gegevens moeten worden gestreamd.

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

![&#x200B; Beeld van het scherm UI die voltooide gebieden voor de bestemmingsdetails van Amazon Kinesis tonen &#x200B;](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL Name]**: Geef een naam op voor uw verbinding met [!DNL Amazon Kinesis]
* **[!UICONTROL Description]**: geef een beschrijving op voor de verbinding met [!DNL Amazon Kinesis] .
* **[!UICONTROL Stream]**: geef de naam op van een bestaande gegevensstroom in uw [!DNL Amazon Kinesis] -account. Experience Platform exporteert gegevens naar deze stream.
* **[!UICONTROL Include Segment Names]**: in-/uitschakelen als u wilt dat bij het exporteren van de gegevens de namen worden opgenomen van het publiek dat u exporteert. Voor een voorbeeld van een gegevens die met deze geselecteerde optie uitvoeren, verwijs naar de [&#x200B; Uitgevoerde gegevens &#x200B;](#exported-data) sectie verder hieronder.
* **[!UICONTROL Include Segment Timestamps]**: Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de UNIX-tijdstempel wordt gebruikt wanneer het publiek is gemaakt en bijgewerkt, en ook de UNIX-tijdstempel wanneer het publiek voor activering is toegewezen aan het doel. Voor een voorbeeld van een gegevens die met deze geselecteerde optie uitvoeren, verwijs naar de [&#x200B; Uitgevoerde gegevens &#x200B;](#exported-data) sectie verder hieronder.

<!--

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* [&#x200B; de beleidsevaluatie van de toestemming &#x200B;](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wordt momenteel niet gesteund in de uitvoer naar de bestemming van Amazon Kinesis. [Meer informatie](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Zie [&#x200B; publieksgegevens aan het stromen van profieluitvoer bestemmingen &#x200B;](../../ui/activate-streaming-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw [!DNL Amazon Kinesis] -doel, zodat alleen gegevens naar uw doel worden geëxporteerd wanneer relevante updates naar een profiel zijn opgetreden na een kwalificatie van het publiek of andere belangrijke gebeurtenissen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een wijziging in het publiekslidmaatschap voor ten minste een van de doelgroepen. Het profiel is bijvoorbeeld gekwalificeerd voor een van de soorten publiek die aan de bestemming zijn toegewezen of heeft een van de soorten publiek afgesloten die aan de bestemming zijn toegewezen.
* De profielupdate werd bepaald door een verandering in de [&#x200B; identiteitskaart &#x200B;](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de soorten publiek dat aan de bestemming is toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een publiek dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot het gegeven dat voor een bepaald profiel wordt uitgevoerd, is het belangrijk om de twee verschillende concepten *te begrijpen wat een gegevensuitvoer aan uw [!DNL Amazon Kinesis] bestemming* en *bepaalt welke gegevens in de uitvoer* inbegrepen zijn.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als de `segmentMembership` -status van een profiel verandert in `realized` of `exiting` of als toegewezen kenmerken worden bijgewerkt, een doelexport wordt uitgeschakeld.</li><li>Omdat identiteiten momenteel niet aan [!DNL Amazon Kinesis] bestemmingen kunnen worden in kaart gebracht, bepalen de veranderingen in om het even welke identiteit op een bepaald profiel ook bestemmingsuitvoer.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Het `segmentMembership` -object bevat het segment dat is toegewezen in de activeringsgegevensstroom, waarvoor de status van het profiel is gewijzigd na een kwalificatie- of segmentafsluitgebeurtenis. Merk op dat andere unmapped segmenten waarvoor het profiel dat voor wordt gekwalificeerd deel van de bestemmingsuitvoer kan uitmaken, als deze segmenten tot het zelfde [&#x200B; fusiebeleid &#x200B;](/help/profile/merge-policies/overview.md) behoren zoals het segment in kaart gebracht in activeringsdataflow. </li><li>Alle identiteiten in het `identityMap` -object worden ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in het [!DNL Amazon Kinesis] -doel).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style="table-layout:fixed"}

>[!BEGINSHADEBOX]

Neem bijvoorbeeld deze gegevensstroom naar een [!DNL Amazon Kinesis] -bestemming waar drie soorten publiek in de gegevensstroom zijn geselecteerd en vier kenmerken aan de bestemming worden toegewezen.

![&#x200B; de bestemmingsdataflow van Amazon Kinesis &#x200B;](../../assets/catalog/http/profile-export-example-dataflow.png)

Een profieluitvoer naar de bestemming kan door een profiel worden bepaald dat voor of het weggaan van één van *drie in kaart gebrachte segmenten* in aanmerking komt. In de gegevensuitvoer, in het `segmentMembership` voorwerp (zie [&#x200B; Uitgevoerde Gegevens &#x200B;](#exported-data) sectie hieronder), zouden andere in kaart gebrachte toehoorders kunnen verschijnen, als dat bepaalde profiel een lid van hen is en als deze het zelfde fusiebeleid zoals het publiek delen dat de uitvoer teweegbracht. Als een profiel voor de **Klant met DeLorean Cars** segment kwalificeert en ook een lid van de **Basis Actieve Plaats en Stad - Dallas** segmenten is, dan zullen deze andere twee publiek ook aanwezig zijn in het `segmentMembership` voorwerp van de gegevensuitvoer, omdat deze in dataflow in kaart worden gebracht, als deze het zelfde fusiebeleid met de **Klant met DeLorean Codes delen ars** segment.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

>[!ENDSHADEBOX]

## Back-up van historische gegevens {#historical-data-backfill}

Wanneer u een nieuw publiek aan een bestaande bestemming toevoegt, of wanneer u een nieuw doel creeert en een publiek in kaart brengt aan het, exporteert Experience Platform historische publiekskwalificatiegegevens naar de bestemming. Profielen die voor het publiek *kwalificeerden alvorens* het publiek aan de bestemming werd toegevoegd worden uitgevoerd naar de bestemming binnen ongeveer één uur.

## Geëxporteerde gegevens {#exported-data}

De geëxporteerde [!DNL Experience Platform] gegevens worden in JSON-indeling in uw [!DNL Amazon Kinesis] -doel geplaatst. Bijvoorbeeld, bevat de hieronder uitvoer een profiel dat voor een bepaald segment heeft gekwalificeerd, een lid van andere twee segmenten is, en een ander segment verliet. Het exporteren bevat ook de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

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

Hieronder vindt u meer voorbeelden van geëxporteerde gegevens, afhankelijk van de UI-instellingen die u hebt geselecteerd in de doelstroom voor verbinden voor de opties **[!UICONTROL Include Segment Names]** en **[!UICONTROL Include Segment Timestamps]** :

+++ In het onderstaande voorbeeld voor het exporteren van gegevens worden publieksnamen opgenomen in de sectie `segmentMembership`

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

+++ Het onderstaande voorbeeld voor het exporteren van gegevens bevat tijdstempels voor het publiek in de sectie `segmentMembership`

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

In 95 percent van de tijd, probeert Experience Platform om een productietolerantie van minder dan 10 minuten voor met succes verzonden berichten met een tarief van minder dan 10.000 verzoeken per seconde voor elke dataflow aan een bestemming van HTTP aan te bieden.

In het geval van mislukte verzoeken aan uw bestemming van HTTP API, slaat Experience Platform de ontbroken verzoeken op en probeert tweemaal om de verzoeken naar uw eindpunt te verzenden.

>[!MORELIKETHIS]
>
>* [&#x200B; verbind met Amazon Kinesis en activeer gegevens gebruikend de Dienst API van de Stroom &#x200B;](../../api/streaming-destinations.md)
>* [&#x200B; Azure de bestemming van de Hubs van de Gebeurtenis &#x200B;](./azure-event-hubs.md)
>* [&#x200B; de types en de categorieën van de Bestemming &#x200B;](../../destination-types.md)
