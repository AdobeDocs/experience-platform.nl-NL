---
keywords: streaming;
title: HTTP API-verbinding
description: Met de HTTP API-bestemming in Adobe Experience Platform kunt u profielgegevens naar HTTP-eindpunten van derden verzenden.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: c2e726a7e66267bf8f301014ae30dedd7472c693
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---

# (Bèta) HTTP API-verbinding

>[!IMPORTANT]
>
>De HTTP API-bestemming in Platform staat momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

De HTTP API-bestemming is een [!DNL Adobe Experience Platform] streamingbestemming waarmee u profielgegevens naar externe HTTP-eindpunten kunt verzenden.

Als u profielgegevens naar HTTP-eindpunten wilt verzenden, moet u eerst [verbinden met de bestemming](#connect-destination) in [!DNL Adobe Experience Platform].

## Gebruiksscenario’s {#use-cases}

De bestemming van HTTP wordt gericht op klanten die XDM profielgegevens en publiekssegmenten naar generische eindpunten van HTTP moeten uitvoeren.

De eindpunten van HTTP kunnen of de systemen van klanten of derdeoplossingen zijn.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Neem contact op met uw Adobe-vertegenwoordigers of de klantenservice van Adobe als u de bètefunctionaliteit van de HTTP API-bestemming voor uw bedrijf wilt inschakelen.

Als u de HTTP API-bestemming wilt gebruiken om gegevens uit Experience Platform te exporteren, moet u aan de volgende voorwaarden voldoen:

* U moet een eindpunt van HTTP hebben dat REST API steunt.
* Uw eindpunt van HTTP moet het het profielschema van het Experience Platform steunen. Transformatie naar een extern payload-schema wordt niet ondersteund in de HTTP API-bestemming. Zie de [geëxporteerde gegevens](#exported-data) voor een voorbeeld van het uitvoerschema van het Experience Platform.
* Uw eindpunt van HTTP moet kopballen steunen.
* Uw eindpunt van HTTP moet steunen [OAuth 2.0-clientreferenties](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) verificatie. Deze vereiste is geldig zolang de HTTP API-bestemming zich in de bètafase bevindt.
* De cliëntreferentie moet in het lichaam van de verzoeken van de POST aan uw eindpunt worden omvat, zoals aangetoond in het hieronder voorbeeld.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```


U kunt ook [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) aan opstelling een integratie en verzendt de profielgegevens van het Experience Platform naar een eindpunt van HTTP.

## Verbinden met de bestemming {#connect-destination}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL httpEndpoint]**: de [!DNL URL] van het HTTP-eindpunt waarnaar u de profielgegevens wilt verzenden.
   * U kunt optioneel queryparameters toevoegen aan de [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: de [!DNL URL] van het HTTP-eindpunt gebruikt voor [!DNL OAuth2] verificatie.
* **[!UICONTROL Client ID]**: de [!DNL clientID] in de [!DNL OAuth2] clientreferenties.
* **[!UICONTROL Client Secret]**: de [!DNL clientSecret] in de [!DNL OAuth2] clientreferenties.

   >[!NOTE]
   >
   >Alleen [!DNL OAuth2] clientreferenties worden momenteel ondersteund.

* **[!UICONTROL Name]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Custom Headers]**: Ga om het even welke douanekopballen in die u in de bestemmingsvraag, volgend dit formaat wilt worden omvat: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >Voor de huidige implementatie is ten minste één aangepaste header vereist. Deze beperking wordt opgelost in een toekomstige update.

## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](../../ui/activate-streaming-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Doelkenmerken {#attributes}

In de [[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes) stap, raadt Adobe u aan een unieke id te selecteren in uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren.

## Productoverwegingen {#product-considerations}

Het Experience Platform stroomt uit geen gegevens aan eindpunten van HTTP door een vaste reeks statische IPs. Daarom kan Adobe geen lijst van statische IPs verstrekken die u lijst van gewenste personen voor de bestemming van HTTP API kunt.

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag van de profieluitvoer naar uw bestemming van HTTP API, om gegevens naar uw API eindpunt slechts uit te voeren wanneer de relevante updates aan een profiel na segmentkwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een verandering in segmentlidmaatschap voor minstens één van de segmenten in kaart gebracht aan de bestemming. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is bepaald door een wijziging in het dialoogvenster [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export? {#what-determines-export-what-is-included}

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten van *wat een gegevensexport naar uw HTTP API-bestemming bepaalt* en *welke gegevens in de uitvoer worden opgenomen*.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als om het even welke in kaart gebrachte segmenten staten (van ongeldig aan gerealiseerd of van gerealiseerde/bestaande aan het weggaan) veranderen of om het even welke in kaart gebrachte attributen worden bijgewerkt, een bestemmingsuitvoer zou worden weggeduwd.</li><li>Omdat identiteiten momenteel niet aan de bestemmingen van HTTP kunnen worden in kaart gebracht API, bepalen de veranderingen in om het even welke identiteit op een bepaald profiel ook bestemmingsuitvoer.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Alle segmenten (met de nieuwste lidmaatschapsstatus), ongeacht of ze in de dataflow zijn toegewezen of niet, worden opgenomen in de `segmentMembership` object.</li><li>Alle identiteiten in de `identityMap` -object worden ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de HTTP API-bestemming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Bijvoorbeeld, overweeg dit dataflow aan een bestemming van HTTP waar drie segmenten in dataflow worden geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![HTTP API-doeldatabase](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de *drie toegewezen segmenten*. Bij de gegevensexport moet u `segmentMembership` object (zie [Geëxporteerde gegevens](#exported-data) (zie hieronder), zouden andere niet in kaart gebrachte segmenten kunnen verschijnen, als dat bepaalde profiel een lid van hen is. Als een profiel in aanmerking komt voor de klant met het segment DeLorean Cars, maar ook lid is van de segmenten &quot;Terug naar de toekomst&quot; film en science fiction, dan zullen deze andere twee segmenten ook aanwezig zijn in de `segmentMembership` -object van de gegevensexport, ook al worden deze niet toegewezen in de gegevensstroom.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform] gegevensterreinen in uw [!DNL HTTP] doel in JSON-indeling. Bijvoorbeeld, bevat de hieronder uitvoer een profiel dat voor een bepaald segment heeft gekwalificeerd, een lid van andere twee segmenten is, en een ander segment verliet. Het exporteren bevat ook de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

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
