---
keywords: Azure-gebeurtenishub-bestemming;azure-gebeurtenishub;azure-eventhub
title: Azure Event Hubs-verbinding
description: Creeer een uitgaande verbinding in real time aan uw [!DNL Azure Event Hubs] opslag naar streamgegevens van Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
> Deze bestemming is alleen beschikbaar voor [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

[!DNL Azure Event Hubs] is een groot platform voor gegevensstreaming en service voor het opnemen van gebeurtenissen. Het kan miljoenen gebeurtenissen per seconde ontvangen en verwerken. Gegevens die naar een gebeurtenishub worden verzonden, kunnen worden getransformeerd en opgeslagen met behulp van een realtime analyseprovider of batchadapters.

U kunt een uitgaande verbinding in real time aan uw creëren [!DNL Azure Event Hubs] opslag om gegevens uit Adobe Experience Platform te streamen.

* Meer informatie over [!DNL Azure Event Hubs], zie de [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Verbinding maken met [!DNL Azure Event Hubs] programmatically, zie [Zelfstudie voor Streaming doelen-API](../../api/streaming-destinations.md).
* Verbinding maken met [!DNL Azure Event Hubs] in de gebruikersinterface van het Platform raadpleegt u de onderstaande secties.

![AWS Kinesis in de gebruikersinterface](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Gevallen gebruiken {#use-cases}

Door streamingdoelen zoals [!DNL Azure Event Hubs]kunt u bovendien gemakkelijk hoogwaardige segmentatiegebeurtenissen en de bijbehorende profielkenmerken in uw eigen systemen importeren.

Met een vooruitzicht downloadde u bijvoorbeeld een witboek dat hen kwalificeert tot een segment met een &quot;hoge neiging om te converteren&quot;. Door het segment in kaart te brengen dat het vooruitzicht binnen aan [!DNL Azure Event Hubs] doel, ontvangt u deze gebeurtenis in [!DNL Azure Event Hubs]. Daar, kunt u een doe-het-zelf benadering gebruiken en bedrijfslogica bovenop de gebeurtenis beschrijven, aangezien u denkt het beste met uw systemen van bedrijfsIT zou werken.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## IP adres lijst van gewenste personen {#ip-address-allowlist}

Om klanten&#39; veiligheid en nalevingsvereisten te ontmoeten, verstrekt het Experience Platform een lijst van statische IPs die u lijst van gewenste personen voor kunt [!DNL Azure Event Hubs] bestemming. Zie [IP adres lijst van gewenste personen voor het stromen bestemmingen](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor de volledige lijst van IPs aan lijst van gewenste personen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Wanneer u verbinding maakt met dit doel, moet u de volgende informatie opgeven:

### Verificatiegegevens {#authentication-information}

#### Standaardverificatie {#standard-authentication}

![Afbeelding van het UI-scherm met de voltooide velden voor de standaardverificatiegegevens van de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Als u **[!UICONTROL Standard authentication]** type om met uw eindpunt van HTTP te verbinden, ga hieronder de gebieden in en selecteer **[!UICONTROL Connect to destination]**:

* **[!UICONTROL SAS Key Name]**: De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd.
* **[!UICONTROL SAS Key]**: De primaire sleutel van de Gebeurtenishubs namespace. De `sasPolicy` de `sasKey` komt overeen met **beheren** rechten die worden geconfigureerd om de lijst Gebeurtenishubs te vullen. Meer informatie over verifiëren bij [!DNL Azure Event Hubs] met SAS-toetsen in de [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Vul uw [!DNL Azure Event Hubs] naamruimte. Meer informatie over [!DNL Azure Event Hubs] naamruimten in het dialoogvenster [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Shared Access Signature (SAS)-verificatie {#sas-authentication}

![Afbeelding van het UI-scherm met de voltooide velden voor de standaardverificatiegegevens van de Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Als u **[!UICONTROL Standard authentication]** type om met uw eindpunt van HTTP te verbinden, ga hieronder de gebieden in en selecteer **[!UICONTROL Connect to destination]**:

* **[!UICONTROL SAS Key Name]**: De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd.
* **[!UICONTROL SAS Key]**: De primaire sleutel van de Gebeurtenishubs namespace. De `sasPolicy` de `sasKey` komt overeen met **beheren** rechten die worden geconfigureerd om de lijst Gebeurtenishubs te vullen. Meer informatie over verifiëren bij [!DNL Azure Event Hubs] met SAS-toetsen in de [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Vul uw [!DNL Azure Event Hubs] naamruimte. Meer informatie over [!DNL Azure Event Hubs] naamruimten in het dialoogvenster [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Namespace]**: Vul uw [!DNL Azure Event Hubs] naamruimte. Meer informatie over [!DNL Azure Event Hubs] naamruimten in het dialoogvenster [Microsoft-documentatie](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Segmentnamen opnemen"
>abstract="Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen van de segmenten worden opgenomen die u exporteert. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Tijdstempels segment opnemen"
>abstract="Schakel deze optie in als u wilt dat de gegevensexport de UNIX-tijdstempel bevat wanneer de segmenten zijn gemaakt en bijgewerkt, evenals de UNIX-tijdstempel wanneer de segmenten voor activering aan de bestemming zijn toegewezen. Bekijk de documentatie voor een voorbeeld van de gegevensuitvoer met deze optie geselecteerd."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Beeld van het scherm UI die voltooide gebieden voor de Azure de bestemmingsdetails van de Hubs van de Gebeurtenis tonen](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Name]**: Geef een naam op voor de verbinding met [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Geef een beschrijving van de verbinding op.  Voorbeelden: &quot;Klanten met de hoogste rang&quot;, &quot;Klanten die geïnteresseerd zijn in keuzen&quot;.
* **[!UICONTROL eventHubName]**: Geef een naam op voor de stream aan uw [!DNL Azure Event Hubs] bestemming.
* **[!UICONTROL Include Segment Names]**: Schakel deze optie in als u wilt dat bij het exporteren van de gegevens de namen van de segmenten worden opgenomen die u exporteert. Voor een voorbeeld van een gegevensexport waarbij deze optie is geselecteerd, raadpleegt u de [Geëxporteerde gegevens](#exported-data) hieronder.
* **[!UICONTROL Include Segment Timestamps]**: Schakel deze optie in als u wilt dat de gegevensexport de UNIX-tijdstempel bevat wanneer de segmenten zijn gemaakt en bijgewerkt, evenals de UNIX-tijdstempel wanneer de segmenten voor activering aan de bestemming zijn toegewezen. Voor een voorbeeld van een gegevensexport waarbij deze optie is geselecteerd, raadpleegt u de [Geëxporteerde gegevens](#exported-data) hieronder.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](../../ui/activate-streaming-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw [!DNL Azure Event Hubs] doel, om gegevens naar uw bestemming slechts uit te voeren wanneer de relevante updates aan een profiel na segmentkwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een verandering in segmentlidmaatschap voor minstens één van de segmenten in kaart gebracht aan de bestemming. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is bepaald door een wijziging in het dialoogvenster [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten van *wat bepalend is voor het exporteren van gegevens naar uw [!DNL Azure Event Hubs] doel* en *welke gegevens in de uitvoer worden opgenomen*.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als om het even welke in kaart gebrachte segmenten staten (van ongeldig aan gerealiseerd of van gerealiseerde/bestaande aan het weggaan) veranderen of om het even welke in kaart gebrachte attributen worden bijgewerkt, een bestemmingsuitvoer zou worden weggeduwd.</li><li>Omdat identiteiten momenteel niet kunnen worden toegewezen aan [!DNL Azure Event Hubs] doelen, wijzigingen in een identiteit in een bepaald profiel bepalen ook de export van de bestemming.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Alle segmenten (met de nieuwste lidmaatschapsstatus), ongeacht of ze in de dataflow zijn toegewezen of niet, worden opgenomen in de `segmentMembership` object.</li><li>Alle identiteiten in de `identityMap` object wordt ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de [!DNL Azure Event Hubs] bestemming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Neem bijvoorbeeld deze gegevensstroom naar een [!DNL Azure Event Hubs] doel waar drie segmenten in dataflow worden geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![Amazon Kinesis-doeldatabase](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de *drie toegewezen segmenten*. Bij de gegevensexport moet u `segmentMembership` object (zie [Geëxporteerde gegevens](#exported-data) (zie hieronder), zouden andere niet in kaart gebrachte segmenten kunnen verschijnen, als dat bepaalde profiel een lid van hen is. Als een profiel in aanmerking komt voor de klant met het segment DeLorean Cars, maar ook lid is van de segmenten &quot;Terug naar de toekomst&quot; film en science fiction, dan zullen deze andere twee segmenten ook aanwezig zijn in de `segmentMembership` -object van de gegevensexport, ook al worden deze niet toegewezen in de gegevensstroom.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

## Back-up van historische gegevens {#historical-data-backfill}

Wanneer u een nieuw segment aan een bestaande bestemming toevoegt, of wanneer u een nieuwe bestemming en kaartsegmenten aan het creeert, voert het Experience Platform historische segmentkwalificatiegegevens naar de bestemming uit. Profielen die in aanmerking komen voor het segment *voor* het segment werd toegevoegd aan de bestemming wordt uitgevoerd naar de bestemming binnen ongeveer één uur.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform] gegevensterreinen in uw [!DNL Azure Event Hubs] doel in JSON-indeling. Bijvoorbeeld, bevat de hieronder uitvoer een profiel dat voor een bepaald segment heeft gekwalificeerd, een lid van andere twee segmenten is, en een ander segment verliet. Het exporteren bevat ook de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

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

Hieronder vindt u meer voorbeelden van geëxporteerde gegevens, afhankelijk van de UI-instellingen die u hebt geselecteerd in de doelstroom voor het verbinden van **[!UICONTROL Include Segment Names]** en **[!UICONTROL Include Segment Timestamps]** opties:

+++ In de onderstaande voorbeeldweergave voor gegevensexport worden segmentnamen opgenomen in `segmentMembership` sectie

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
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

+++ In het onderstaande voorbeeld voor gegevensuitvoer zijn tijdstempels voor segmenten opgenomen in de `segmentMembership` sectie

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
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
>* [Verbind met Azure Event Hubs en activeer gegevens gebruikend de Dienst API van de Stroom](../../api/streaming-destinations.md)
>* [AWS Kinesis-bestemming](./amazon-kinesis.md)
>* [Doeltypen en -categorieën](../../destination-types.md)

