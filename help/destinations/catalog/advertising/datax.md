---
title: Verizon MediaYahoo DataX-verbinding
description: DataX is een geaggregeerde Verizon Media/Yahoo-infrastructuur die verschillende componenten host die Verizon Media/Yahoo in staat stellen gegevens met zijn externe partners op een veilige, geautomatiseerde en schaalbare manier uit te wisselen.
source-git-commit: 09bae0d24eead5f0b6533ba5b89e1fc87c8c71b5
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 1%

---


# Verizon Media/Yahoo DataX-verbinding

## Overzicht {#overview}

DataX is een geaggregeerde Verizon Media/Yahoo-infrastructuur die verschillende componenten host die Verizon Media/Yahoo in staat stellen gegevens met zijn externe partners op een veilige, geautomatiseerde en schaalbare manier uit te wisselen.

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door het DataX-team van Verizon Media/Yahoo. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Vereisten {#prerequisites}

**MDM-id**

Dit is een unieke id in Yahoo DataX en het is een verplicht veld voor het instellen van gegevensexport naar dit doel. Als u deze id niet kent, neemt u contact op met uw Yahoo Data X-accountmanager.

**Snelheidslimiet**

DataX is tarief-beperkt binnen de quotagrenzen voor taxonomie en publieksposten die in de [documentatie DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/) worden geschetst.


| Foutcode | Foutbericht | Beschrijving |
|---------|----------|---------|
| 429 Te veel verzoeken | Snelheidslimiet overschreden per uur **(Limiet: 100)** | Aantal toegestane verzoeken in een uur per leverancier. |

{style=&quot;table-layout:auto&quot;}

**Metagegevens over taxonomie**

De bron Taxonomy definieert een extensie via de structuur van Base DataX-metagegevens

```
{

  >>(Base DataX Metadata)<<

        "extensions" : { "action" :
        {string}, "incrementalData" :
        {
                "taxonomyId": {string}
                },
                "links" : [{
                "rel"   : "https://datax.yahooapis.com/rels/fullTaxonomy", "title" : "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Meer informatie over [Taxonomy Metadata](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) vindt u in de documentatie voor ontwikkelaars van DataX.

## Ondersteunde identiteiten {#supported-identities}

Verizon Media ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering. |
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple ID for Advertisers | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |

{style=&quot;table-layout:auto&quot;}

## Exporttype {#export-type}

**Segmentexport** : u exporteert alle leden van een segment (publiek) met de id&#39;s (e-mail) die worden gebruikt in de bestemming Verizon Media.

## Gevallen gebruiken {#use-cases}

DataX-API&#39;s zijn beschikbaar voor adverteerders die een specifieke doelgroep willen kiezen met e-mailadressen die in VMG (Verizon Media) zijn uitgeschakeld, zodat ze snel een nieuw segment kunnen maken en de gewenste doelgroep kunnen duwen met de bijna-real-time API van VMG.

## Verbinden met doel {#connect}

![Yahoo DataX-doelkaart in gebruikersinterface van Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL MDM ID]**: Dit is een unieke id in Yahoo DataX en het is een verplicht veld voor het instellen van gegevensexport naar dit doel. Als u deze ID niet kent, neemt u contact op met uw Yahoo Data X accountmanager.  Met MDM IDs, kunnen de gegevens voor gebruik slechts met een bepaalde reeks exclusieve gebruikers (zoals eerste partijgegevens voor adverteerders) worden beperkt.

## Segmenten naar dit doel activeren {#activate}

Lees [Activate profielen en segmenten aan een bestemming](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiekssegmenten aan bestemmingen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.

## Aanvullende bronnen {#additional-resources}

Lees de [documentatie bij Yahoo/Verizon Media over DataX](https://developer.verizonmedia.com/datax/guide/) voor meer informatie.