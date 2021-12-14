---
title: Verizon MediaYahoo DataX-verbinding
description: DataX is een geaggregeerde Verizon Media/Yahoo-infrastructuur die verschillende componenten host die Verizon Media/Yahoo in staat stellen gegevens met zijn externe partners op een veilige, geautomatiseerde en schaalbare manier uit te wisselen.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
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

DataX is tariefbeperkt binnen de quota voor taxonomie en publieksposten die in [DataX-documentatie](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Foutcode | Foutbericht | Beschrijving |
|---------|----------|---------|
| 429 Te veel verzoeken | Snelheidslimiet overschreden per uur **(Limiet: 100)** | Aantal toegestane verzoeken in een uur per leverancier. |

{style=&quot;table-layout:auto&quot;}

**Metagegevens over taxonomie**

De bron Taxonomy definieert een extensie via de structuur van Base DataX-metagegevens

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Meer informatie over [Metagegevens over taxonomie](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) in de documentatie voor ontwikkelaars van DataX.

## Ondersteunde identiteiten {#supported-identities}

Verizon Media ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |

{style=&quot;table-layout:auto&quot;}

## Exporttype {#export-type}

**Segment exporteren** - u exporteert alle leden van een segment (publiek) met de id&#39;s (e-mail) die worden gebruikt in de bestemming Verizon Media.

## Gevallen gebruiken {#use-cases}

DataX-API&#39;s zijn beschikbaar voor adverteerders die een specifieke doelgroep willen kiezen met e-mailadressen die in VMG (Verizon Media) zijn uitgeschakeld, zodat ze snel een nieuw segment kunnen maken en de gewenste doelgroep kunnen duwen met de bijna-real-time API van VMG.

## Verbinden met doel {#connect}

![Yahoo DataX-doelkaart in gebruikersinterface van Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL MDM ID]**: Dit is een unieke id in Yahoo DataX en het is een verplicht veld voor het instellen van gegevensexport naar dit doel. Als u deze ID niet kent, neemt u contact op met uw Yahoo Data X accountmanager.  Met MDM IDs, kunnen de gegevens voor gebruik slechts met een bepaalde reeks exclusieve gebruikers (zoals eerste partijgegevens voor adverteerders) worden beperkt.

## Segmenten naar dit doel activeren {#activate}

Lezen [Profielen en segmenten naar een doel activeren](../../ui/activate-segment-streaming-destinations.md) voor instructies over het activeren van publiekssegmenten aan bestemmingen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen {#additional-resources}

Lees voor meer informatie de Yahoo/Verizon-media [documentatie over DataX](https://developer.verizonmedia.com/datax/guide/).
