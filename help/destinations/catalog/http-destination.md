---
keywords: streaming;
title: HTTP-verbinding
description: Met de HTTP-bestemming in Adobe Experience Platform kunt u profielgegevens naar HTTP-eindpunten van derden verzenden.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# (Alpha) [!DNL HTTP] verbinding

>[!IMPORTANT]
>
>De [!DNL HTTP] bestemming in Platform is momenteel in alpha. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

De [!DNL HTTP] bestemming is een [!DNL Adobe Experience Platform] het stromen bestemming die u profielgegevens naar derde [!DNL HTTP] eindpunten helpt verzenden.

Als u profielgegevens naar [!DNL HTTP] eindpunten wilt verzenden, moet u eerst verbinding maken met het doel in [[!DNL Adobe Experience Platform]](#connect-destination).

## Gevallen {#use-cases} gebruiken

Het doel [!DNL HTTP] is gericht op klanten die XDM profielgegevens en publiekssegmenten naar generische [!DNL HTTP] eindpunten moeten uitvoeren.

[!DNL HTTP] de eindpunten kunnen of de systemen van klanten of derdeoplossingen zijn.

## Verbinden met Doel {#connect-destination}

Selecteer [!DNL HTTP API] in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer **[!UICONTROL Configure]**.

![HTTP-bestemming activeren](../assets/catalog/http/activate.png)

Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

![HTTP-bestemming activeren](../assets/catalog/http/connect.png)

In de stap [!UICONTROL Account] moet u de details van de HTTP-eindpuntverbinding definiëren. Selecteer **[!UICONTROL New account]** en ga de verbindingsdetails voor het eindpunt van HTTP in dat u wilt verbinden met.
- **[!UICONTROL httpEndpoint]**: de volledige voltooiing  [!DNL URL] van het eindpunt van HTTP dat u de profielgegevens wilt verzenden naar.
   - Naar keuze kunt u vraagparameters aan [!UICONTROL httpEndpoint] [!DNL URL] toevoegen.
- **[!UICONTROL authEndpoint]**: het volledige eindpunt  [!DNL URL] van HTTP dat voor  [!DNL OAuth2] authentificatie wordt gebruikt.
- **[!UICONTROL Client ID]**: de  [!DNL clientID] parameter die in de  [!DNL OAuth2] cliëntgeloofsbrieven wordt gebruikt.
- **[!UICONTROL Client Secret]**: de  [!DNL clientSecret] parameter die in de  [!DNL OAuth2] cliëntgeloofsbrieven wordt gebruikt.

>[!NOTE]
>
>Momenteel worden alleen [!DNL OAuth2] clientreferenties ondersteund.

![HTTP-eindpuntverbinding](../assets/catalog/http/connect.png)

Klik op **[!UICONTROL Connect to destination]**. Klik op **[!UICONTROL Next]** nadat de verbinding tot stand is gebracht.

Voer in de stap [!UICONTROL Authentication] de verificatiereferenties van de account in:
- **[!UICONTROL Name]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
- **[!UICONTROL Description]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
- **[!UICONTROL Custom Headers]**: Ga om het even welke douanekopballen in die u in de bestemmingsvraag, volgend dit formaat wilt worden omvat:  `header1:value1,header2:value2,...headerN:valueN`.
- **[!UICONTROL Marketing actions]**: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie de pagina [Gegevensbeheer in Adobe Experience Platform](/help/data-governance/policies/overview.md) voor meer informatie over marketingacties. Zie [Overzicht van beleidsregels voor gegevensgebruik](/help/data-governance/policies/overview.md) voor informatie over de afzonderlijke door Adobe gedefinieerde marketingacties.

>[!IMPORTANT]
>
>Voor de huidige implementatie is ten minste één aangepaste header vereist. Deze beperking wordt opgelost in een toekomstige update.

![HTTP-verificatie](../assets/catalog/http/authenticate.png)

**[!UICONTROL Marketing action]**: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../data-governance/policies/overview.md).

Klik op **[!UICONTROL Create destination]**.

## Segmenten activeren

Zie [Profielen en segmenten activeren naar een doel](../ui/activate-destinations.md#select-attributes) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken

Tijdens de [[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes) stap, wanneer [het activeren van segmenten](../ui/activate-destinations.md) aan een [!DNL HTTP] bestemming, adviseren wij dat u een uniek herkenningsteken van uw [union schema](../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren.

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
