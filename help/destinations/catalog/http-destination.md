---
keywords: streaming;
title: HTTP-verbinding
description: Met de HTTP-bestemming in Adobe Experience Platform kunt u profielgegevens naar HTTP-eindpunten van derden verzenden.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# (Alpha) [!DNL HTTP] verbinding

>[!IMPORTANT]
>
>De [!DNL HTTP] doel in Platform bevindt zich momenteel in alpha. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

De [!DNL HTTP] doel is een [!DNL Adobe Experience Platform] streamingdoel waarmee u profielgegevens naar derden kunt verzenden [!DNL HTTP] eindpunten.

Profielgegevens verzenden naar [!DNL HTTP] eindpunten, moet u eerst met de bestemming binnen verbinden [[!DNL Adobe Experience Platform]](#connect-destination).

## Gebruiksscenario’s {#use-cases}

De [!DNL HTTP] doel is gericht op klanten die XDM-profielgegevens en publiekssegmenten naar generiek moeten exporteren [!DNL HTTP] eindpunten.

[!DNL HTTP] de eindpunten kunnen of de systemen van klanten of derdeoplossingen zijn.

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

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

Zie [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](../ui/activate-streaming-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Doelkenmerken {#attributes}

In de [[!UICONTROL Select attributes]](../ui/activate-streaming-profile-destinations.md#select-attributes) stap, raadt Adobe u aan een unieke id te selecteren in uw [samenvoegingsschema](../../profile/home.md#profile-fragments-and-union-schemas). Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform] gegevensterreinen in uw [!DNL HTTP] doel in JSON-indeling. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteit van dit vooruitzicht is [!DNL ECID] en e-mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
