---
keywords: reclame; criterium;
title: Criteverbinding
description: Criteo biedt vertrouwde en ondoordachte reclame de mogelijkheid om meer ervaring op te doen voor elke consument op het open internet. With the world's largest commerce data set and best-in-class AI, Criteo ensures each touchpoint across the shopping journey is personalized to reach customers with the right ad, at the right time.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 36da42b184450cfaf12b097f982234d628681430
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 2%

---

# (bèta) Criteo-verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door de website. Dit is momenteel een bètaproduct en de functionaliteit kan worden gewijzigd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de Commissie [hier](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo powers trusted and impactful advertising to bring richer experiences to every consumer across the open internet. Met &#39;s werelds grootste set handelsgegevens en de best-in-class AI zorgt Criteo ervoor dat elk touchpoint over de winkelreis gepersonaliseerd is om klanten met de juiste en juiste advertentie op het juiste moment te bereiken.

## Vereisten {#prerequisites}

* U moet een beheerdersgebruikersaccount hebben op [Centrum voor systeembeheer](https://marketing.criteo.com).
* U hebt uw advertentie-id voor de website nodig (vraag uw contactpersoon voor de website als u deze id niet hebt).

## Beperkingen {#limitations}

* Criteo biedt momenteel geen ondersteuning voor het verwijderen van gebruikers uit het publiek.
* Criteuse accepteert alleen [!DNL SHA-256]-hashed en onbewerkte e-mails (om te zetten in [!DNL SHA-256] vóór verzending). Please do not send any PII (Personal Identifiable Information, such as individual&#39;s names or phone numbers).

![Vereisten](../../assets/catalog/advertising/criteo/prerequisites.png)

## Supported identities {#supported-identities}

Criteo ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Learn more about [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target Identity | Beschrijving | Overwegingen |
| --- | --- | --- |
| `email_sha256` | E-mailadressen die met het algoritme SHA-256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA-256-gehashte e-mailadressen. When your source field contains unhashed attributes, check the [!UICONTROL Apply transformation] option, to have Platform automatically hash the data on activation. |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| --- | --- | --- |
| Exporttype | Segment exporteren | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster [!DNL Criteo] bestemming. |
| Uitvoerfrequentie | Streaming | Streaming destinations are &quot;always on&quot; API-based connections. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Read more about [streaming destinations](../../destination-types.md#streaming-destinations). |

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe te gebruiken [!DNL Criteo] doel, hier zijn sommige doelstellingen die de klanten van Adobe Experience Platform kunnen bereiken met [!DNL Criteo]:

### Hoofdlettergebruik 1: Verkeer ophalen

Showcase your business with relevant product offers and flexible creatives. Met intelligente productaanbevelingen zullen uw advertenties automatisch de producten bevatten die het meest waarschijnlijk bezoeken en betrokkenheid zullen veroorzaken. Flexible targeting allows you to build audiences from Criteo&#39;s commerce data set or from your own prospect lists and Adobe CDP segments.

### Use case 2 : Increase website conversions

Wanneer bezoekers uw website verlaten, herinner hen wat zij met het herrichten van advertenties missen die omzettingen door speciale overeenkomsten en hyper-relevante aanbiedingen te tonen verhogen, waar zij ook gaan. Verbind uw Adobe CDP segment om bestaande klanten opnieuw in dienst te nemen of consumenten te richten gelijkend op uw meest loyale kopers.

## Verbinding maken met website {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

### Verifiëren voor commissie

De stappen om te verbinden zijn als volgt:

1. Meld u aan bij Adobe Experience Platform en maak verbinding met het doel Computer.

   ![Aanmelden](../../assets/catalog/advertising/criteo/connect-destination.png)

1. You will be redirected to Criteo to authorize the connection. You may need to first log in with your Criteo credentials:

   ![Criteo login](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Aanmelden bij website](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Aanmelden bij website](../../assets/catalog/advertising/criteo/log-in-3.png)


### Verbindingsparameters {#connection-parameters}

After authenticating to the destination, please fill in the following connection parameters.

![Connection parameters](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Veld | Beschrijving | Vereist |
| --- | --- | --- |
| Naam | A name to help you recognize this destination in the future. De naam die u hier kiest, is [!DNL Audience] naam in het Centrum van het Beheer van de Nota en kan niet in later stadium worden gewijzigd. | Ja |
| Beschrijving | Een beschrijving waarmee u deze bestemming in de toekomst kunt identificeren. | Nee |
| API Version | Criteo API Version. Selecteer Voorvertoning. | Ja |
| Adverteerder-id | Identiteitskaart van Adverteerder van de website van uw organisatie. Neem contact op met uw accountmanager van de website voor deze informatie. | Ja |

## Segmenten naar dit doel activeren {#activate-segments}

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

You can see the exported segments in the [Criteo management center](https://marketing.criteo.com/audience-manager/dashboard).

The request body received by the [!DNL Criteo] connection looks similar to this:

```json
{ 
  "data": { 
    "type": "ContactlistWithUserAttributesAmendment", 
    "attributes": { 
      "operation": "add", 
      "identifierType": "sha256email", 
      "identifiers": [ 
        { 
          "identifier": "1c8494bbc4968277345133cca6ba257b9b3431b8a84833a99613cf075a62a16d", 
          "attributes": [{ "key": "customValue", "value": "1" }] 
        } 
      ] 
    } 
  } 
} 
```

## Gegevensgebruik en -beheer {#data-usage}

Alle Adobe Experience Platform-doelen zijn bij het verwerken van uw gegevens compatibel met het beleid voor gegevensgebruik. For detailed information on how Adobe Experience Platform enforces data governance, read the [Data Governance overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## Aanvullende bronnen

* [Criteo Help Center](https://help.criteo.com/kb/en)
* [Criteo Developer Portal](https://developers.criteo.com/marketing-solutions/v2022.04/reference/modifyaudienceuserswithattributes)
