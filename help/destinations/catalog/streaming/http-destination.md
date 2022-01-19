---
keywords: streaming;
title: HTTP API-verbinding
description: Met de HTTP API-bestemming in Adobe Experience Platform kunt u profielgegevens naar HTTP-eindpunten van derden verzenden.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: f098df9df2baa971db44a6746949f021e212ae3e
workflow-type: tm+mt
source-wordcount: '820'
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

## Exportgedrag profiel {#profile-export-behavior}

Experience Platform optimaliseert het gedrag van de profieluitvoer naar uw bestemming van HTTP API, om gegevens naar uw API eindpunt slechts uit te voeren wanneer de relevante updates aan een profiel na segmentkwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd teweeggebracht door een verandering in segmentlidmaatschap voor minstens één van de segmenten die aan de bestemming in kaart werden gebracht. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is geactiveerd door een wijziging in de [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate werd geactiveerd door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform] gegevensterreinen in uw [!DNL HTTP] doel in JSON-indeling. De onderstaande exportbewerking bevat bijvoorbeeld een profiel dat is gekwalificeerd voor een bepaald segment en dat een ander segment heeft verlaten. Het bevat de voornaam, achternaam, geboortedatum en het persoonlijke e-mailadres van het profielkenmerk. De identiteiten voor dit profiel zijn ECID en e-mail.

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
