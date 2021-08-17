---
keywords: streaming;
title: HTTP-verbinding
description: Met de HTTP-bestemming in Adobe Experience Platform kunt u profielgegevens naar HTTP-eindpunten van derden verzenden.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# (Alpha) [!DNL HTTP] verbinding

>[!IMPORTANT]
>
>De [!DNL HTTP] bestemming in Platform is momenteel in alpha. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

De [!DNL HTTP] bestemming is een [!DNL Adobe Experience Platform] het stromen bestemming die u profielgegevens naar derde [!DNL HTTP] eindpunten helpt verzenden.

Als u profielgegevens naar [!DNL HTTP] eindpunten wilt verzenden, moet u eerst verbinding maken met het doel in [[!DNL Adobe Experience Platform]](#connect-destination).

## Gebruiksscenario’s {#use-cases}

Het doel [!DNL HTTP] is gericht op klanten die XDM profielgegevens en publiekssegmenten naar generische [!DNL HTTP] eindpunten moeten uitvoeren.

[!DNL HTTP] de eindpunten kunnen of de systemen van klanten of derdeoplossingen zijn.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL httpEndpoint]**: de waarde  [!DNL URL] van het HTTP-eindpunt waarnaar u de profielgegevens wilt verzenden.
   * Naar keuze, kunt u vraagparameters aan [!UICONTROL httpEndpoint] [!DNL URL] toevoegen.
* **[!UICONTROL authEndpoint]**: het  [!DNL URL] eindpunt van HTTP dat voor  [!DNL OAuth2] authentificatie wordt gebruikt.
* **[!UICONTROL Client ID]**: de  [!DNL clientID] parameter die in de  [!DNL OAuth2] cliëntgeloofsbrieven wordt gebruikt.
* **[!UICONTROL Client Secret]**: de  [!DNL clientSecret] parameter die in de  [!DNL OAuth2] cliëntgeloofsbrieven wordt gebruikt.

   >[!NOTE]
   >
   >Momenteel worden alleen [!DNL OAuth2] clientreferenties ondersteund.

* **[!UICONTROL Name]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Custom Headers]**: Ga om het even welke douanekopballen in die u in de bestemmingsvraag, volgend dit formaat wilt worden omvat:  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >Voor de huidige implementatie is ten minste één aangepaste header vereist. Deze beperking wordt opgelost in een toekomstige update.

## Segmenten naar dit doel activeren {#activate}

Zie [Profielen en segmenten activeren aan een doel](../ui/activate-destinations.md#select-attributes) voor instructies bij het activeren van publiekssegmenten aan bestemmingen.

## Doelkenmerken {#attributes}

In de [[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes) stap, wanneer [het activeren van segmenten](../ui/activate-destinations.md) aan een [!DNL HTTP] bestemming, adviseert Adobe dat u een uniek herkenningsteken van uw [union schema](../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren.

## Geëxporteerde gegevens {#exported-data}

Uw geëxporteerde [!DNL Experience Platform]-gegevens worden in JSON-indeling in uw [!DNL HTTP]-doel geplaatst. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn [!DNL ECID] en e-mail.

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
