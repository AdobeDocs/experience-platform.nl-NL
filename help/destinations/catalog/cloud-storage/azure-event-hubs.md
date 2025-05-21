---
keywords: Azure-gebeurtenishub-bestemming;azure-gebeurtenishub;azure-eventhub
title: Azure Event Hubs-verbinding
description: Creeer een uitgaande verbinding in real time aan uw  [!DNL Azure Event Hubs]  opslag aan stroomgegevens van Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 678f80445212edc1edd3f4799999990ddcc2a039
workflow-type: tm+mt
source-wordcount: '2029'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
> Deze bestemming is beschikbaar slechts aan [ Adobe Real-Time Customer Data Platform Ultimate ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

[!DNL Azure Event Hubs] is een groot platform voor gegevensstreaming en de service voor het opnemen van gebeurtenissen. Het kan miljoenen gebeurtenissen per seconde ontvangen en verwerken. Gegevens die naar een gebeurtenishub worden verzonden, kunnen worden getransformeerd en opgeslagen met behulp van een realtime analyseprovider of batchadapters.

U kunt een real-time uitgaande verbinding maken met uw [!DNL Azure Event Hubs] -opslag om gegevens vanuit Adobe Experience Platform te streamen.

* Voor meer informatie over [!DNL Azure Event Hubs], zie de [ documentatie van Microsoft ](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Om met [!DNL Azure Event Hubs] programmatically te verbinden, zie de [ Streaming bestemmingen API leerprogramma ](../../api/streaming-destinations.md).
* Zie de volgende secties als u verbinding wilt maken met [!DNL Azure Event Hubs] via de Experience Platform-gebruikersinterface.

![ Kinesis van AWS in UI ](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Gebruiksscenario’s {#use-cases}

Door het stromen bestemmingen zoals [!DNL Azure Event Hubs] te gebruiken, kunt u high-value segmenteringsgebeurtenissen en bijbehorende profielattributen in uw systemen van keus gemakkelijk invoeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Als u het publiek in kaart brengt dat het vooruitzicht naar het [!DNL Azure Event Hubs] -doel valt, ontvangt u deze gebeurtenis in [!DNL Azure Event Hubs] . Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [ werkschema van de bestemmingsactivering ](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#ip-address-allowlist}

Experience Platform biedt een lijst met statische IP&#39;s die u kunt lijsten van gewenste personen voor de [!DNL Azure Event Hubs] -bestemming om aan de beveiligings- en compatibiliteitsvereisten van klanten te voldoen. Verwijs naar [ IP adreslijst van gewenste personen voor het stromen bestemmingen ](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor de volledige lijst van IPs aan lijst van gewenste personen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. Wanneer u verbinding maakt met dit doel, moet u de volgende informatie opgeven:

### Verificatiegegevens {#authentication-information}

#### Standaardverificatie {#standard-authentication}

![ Beeld van het scherm UI die voltooide gebieden voor de de standaardauthentificatiedetails van de Hubs van de Azure Gebeurtenis tonen ](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Als u het type **[!UICONTROL Standard authentication]** selecteert om verbinding te maken met het HTTP-eindpunt, voert u de onderstaande velden in en selecteert u **[!UICONTROL Connect to destination]** :

* **[!UICONTROL SAS Key Name]**: De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd.
* **[!UICONTROL SAS Key]**: De primaire sleutel van de naamruimte Gebeurtenishubs. `sasPolicy` dat `sasKey` beantwoordt om **te hebben** rechten leiden die worden gevormd opdat de lijst van de Hubs van de Gebeurtenis wordt bevolkt. Leer over voor authentiek verklaren aan [!DNL Azure Event Hubs] met de sleutels van SAS in de [ documentatie van Microsoft ](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: vul de naamruimte [!DNL Azure Event Hubs] in. Leer over [!DNL Azure Event Hubs] namespaces in de [ documentatie van Microsoft ](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Shared Access Signature (SAS)-verificatie {#sas-authentication}

![ Beeld van het scherm UI die voltooide gebieden voor de de standaardauthentificatiedetails van de Hubs van de Azure Gebeurtenis tonen ](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Als u het type **[!UICONTROL Standard authentication]** selecteert om verbinding te maken met het HTTP-eindpunt, voert u de onderstaande velden in en selecteert u **[!UICONTROL Connect to destination]** :

* **[!UICONTROL SAS Key Name]**: De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd.
* **[!UICONTROL SAS Key]**: De primaire sleutel van de naamruimte Gebeurtenishubs. `sasPolicy` dat `sasKey` beantwoordt om **te hebben** rechten leiden die worden gevormd opdat de lijst van de Hubs van de Gebeurtenis wordt bevolkt. Leer over voor authentiek verklaren aan [!DNL Azure Event Hubs] met de sleutels van SAS in de [ documentatie van Microsoft ](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: vul de naamruimte [!DNL Azure Event Hubs] in. Leer over [!DNL Azure Event Hubs] namespaces in de [ documentatie van Microsoft ](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Event Hub Name]**: vul de naam [!DNL Azure Event Hub] in. Leer over [!DNL Azure Event Hubs] namen in de [ documentatie van Microsoft ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Segmentnamen opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen worden opgenomen van het publiek dat u exporteert. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Tijdstempels segment opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de UNIX-tijdstempel wordt opgenomen wanneer het publiek is gemaakt en bijgewerkt, en ook de UNIX-tijdstempel wanneer het publiek voor activering aan de bestemming is toegewezen. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ Beeld van het scherm UI die voltooide gebieden voor de Azure de bestemmingsdetails van de Hubs van de Gebeurtenis tonen ](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Name]**: vul een naam in voor de verbinding met [!DNL Azure Event Hubs] .
* **[!UICONTROL Description]**: geef een beschrijving van de verbinding.  Voorbeelden: &quot;Klanten met de hoogste levensstandaard&quot;, &quot;Klanten die geïnteresseerd zijn in keuzen.&quot;
* **[!UICONTROL eventHubName]**: geef een naam voor de stream op naar het [!DNL Azure Event Hubs] -doel.
* **[!UICONTROL Include Segment Names]**: in-/uitschakelen als u wilt dat bij het exporteren van de gegevens de namen worden opgenomen van het publiek dat u exporteert. Voor een voorbeeld van een gegevens die met deze geselecteerde optie uitvoeren, verwijs naar de [ Uitgevoerde gegevens ](#exported-data) sectie verder hieronder.
* **[!UICONTROL Include Segment Timestamps]**: Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de UNIX-tijdstempel wordt gebruikt wanneer het publiek is gemaakt en bijgewerkt, en ook de UNIX-tijdstempel wanneer het publiek voor activering is toegewezen aan het doel. Voor een voorbeeld van een gegevens die met deze geselecteerde optie uitvoeren, verwijs naar de [ Uitgevoerde gegevens ](#exported-data) sectie verder hieronder.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* [ de toestemmings beleidsevaluatie ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wordt momenteel niet gesteund in de uitvoer naar de Azure bestemming van de Hubs van de Gebeurtenis. [Meer informatie](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Zie [ publieksgegevens aan het stromen van profieluitvoer bestemmingen ](../../ui/activate-streaming-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw [!DNL Azure Event Hubs] -doel, zodat alleen gegevens naar uw doel worden geëxporteerd wanneer relevante updates naar een profiel zijn opgetreden na een kwalificatie van het publiek of andere belangrijke gebeurtenissen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een wijziging in het publiekslidmaatschap voor ten minste een van de doelgroepen. Het profiel is bijvoorbeeld gekwalificeerd voor een van de soorten publiek die aan de bestemming zijn toegewezen of heeft een van de soorten publiek afgesloten die aan de bestemming zijn toegewezen.
* De profielupdate werd bepaald door een verandering in de [ identiteitskaart ](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de soorten publiek dat aan de bestemming is toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een publiek dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot het gegeven dat voor een bepaald profiel wordt uitgevoerd, is het belangrijk om de twee verschillende concepten *te begrijpen wat een gegevensuitvoer aan uw [!DNL Azure Event Hubs] bestemming* en *bepaalt welke gegevens in de uitvoer* inbegrepen zijn.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als de `segmentMembership` -status van een profiel verandert in `realized` of `exiting` of als toegewezen kenmerken worden bijgewerkt, een doelexport wordt uitgeschakeld.</li><li>Omdat identiteiten momenteel niet aan [!DNL Azure Event Hubs] bestemmingen kunnen worden in kaart gebracht, bepalen de veranderingen in om het even welke identiteit op een bepaald profiel ook bestemmingsuitvoer.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Het `segmentMembership` -object bevat het segment dat is toegewezen in de activeringsgegevensstroom, waarvoor de status van het profiel is gewijzigd na een kwalificatie- of segmentafsluitgebeurtenis. Merk op dat andere unmapped segmenten waarvoor het profiel dat voor wordt gekwalificeerd deel van de bestemmingsuitvoer kan uitmaken, als deze segmenten tot het zelfde [ fusiebeleid ](/help/profile/merge-policies/overview.md) behoren zoals het segment in kaart gebracht in activeringsdataflow. </li><li>Alle identiteiten in het `identityMap` -object worden ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in het [!DNL Azure Event Hubs] -doel).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style="table-layout:fixed"}

Neem bijvoorbeeld deze gegevensstroom naar een [!DNL Azure Event Hubs] -bestemming waar drie soorten publiek in de gegevensstroom zijn geselecteerd en vier kenmerken aan de bestemming worden toegewezen.

![ de bestemmingsdataflow van Amazon Kinesis ](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profieluitvoer naar de bestemming kan door een profiel worden bepaald dat voor of het weggaan van één van *drie in kaart gebrachte segmenten* in aanmerking komt. Nochtans, in de gegevensuitvoer, in het `segmentMembership` voorwerp (zie [ Uitgevoerde Gegevens ](#exported-data) sectie hieronder), zouden andere niet in kaart gebrachte toehoorders kunnen verschijnen, als dat bepaalde profiel een lid van hen is en als deze het zelfde fusiebeleid zoals het publiek delen dat de uitvoer teweegbracht. Als een profiel voor de **Klant met de Auto&#39;s van DeLorean** maar ook een lid van het **Gecontroleerde &quot;Terug naar de Toekomstige&quot;** film en **de de fictiefondsen van de Wetenschap** segmenten kwalificeert, dan zullen deze andere twee publiek ook in het `segmentMembership` voorwerp van de gegevensuitvoer aanwezig zijn, alhoewel deze niet in dataflow, als deze zelfde samenvoegingsbeleid delen met de **Klant met het segment van de AutoAuto&#39;s van DeLorean**.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

## Back-up van historische gegevens {#historical-data-backfill}

Wanneer u een nieuw publiek aan een bestaande bestemming toevoegt, of wanneer u een nieuw doel creeert en een publiek in kaart brengt aan het, exporteert Experience Platform historische publiekskwalificatiegegevens naar de bestemming. Profielen die voor het publiek *kwalificeerden alvorens* het publiek aan de bestemming werd toegevoegd worden uitgevoerd naar de bestemming binnen ongeveer één uur.

## Geëxporteerde gegevens {#exported-data}

De geëxporteerde [!DNL Experience Platform] gegevens worden in JSON-indeling in uw [!DNL Azure Event Hubs] -doel geplaatst. Bijvoorbeeld, bevat de hieronder uitvoer een profiel dat voor een bepaald segment heeft gekwalificeerd, een lid van andere twee segmenten is, en een ander segment verliet. Het exporteren bevat ook de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

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
>* [ verbind met Azure de Hubs van de Gebeurtenis en activeer gegevens gebruikend de Dienst API van de Stroom ](../../api/streaming-destinations.md)
>* [ bestemming van AWS Kinesis ](./amazon-kinesis.md)
>* [ de types en de categorieën van de Bestemming ](../../destination-types.md)
