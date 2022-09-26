---
title: Verizon MediaYahoo DataX-verbinding
description: DataX is een geaggregeerde Verizon Media/Yahoo-infrastructuur die verschillende componenten host die Verizon Media/Yahoo in staat stellen gegevens met zijn externe partners op een veilige, geautomatiseerde en schaalbare manier uit te wisselen.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 0580816c471400ba17eddcb6b1a9dfbf01797938
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 1%

---

# [!DNL Verizon Media/Yahoo DataX] verbinding

## Overzicht {#overview}

[!DNL DataX] is een aggregaat [!DNL Verizon Media/Yahoo] infrastructuur die gastheren diverse componenten die toelaten [!DNL Verizon Media/Yahoo] gegevens op een veilige, geautomatiseerde en schaalbare manier met haar externe partners uit te wisselen.

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door [!DNL Verizon Media/Yahoo]s [!DNL DataX] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Vereisten {#prerequisites}

**MDM-id**

Dit is een unieke id in [!DNL Yahoo DataX] en het is een verplicht veld voor het instellen van gegevensexport naar deze bestemming . Neem contact op met uw [!DNL Yahoo DataX] accountmanager.

**Metagegevens over taxonomie**

Het middel Taxonomy bepaalt een uitbreiding over de Basis [!DNL DataX] Metagegevensstructuur

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

Meer informatie over [Metagegevens over taxonomie](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) in de [!DNL DataX] ontwikkelaarsdocumentatie.

## Snelheidslimieten en guardrails {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Bij het activeren van meer dan 100 segmenten naar [!DNL Verizon Media/Yahoo DataX], zou u tarief beperkende fouten van de bestemming kunnen ontvangen. Wanneer het activeren van segmenten aan deze bestemming, probeer om minder dan 100 segmenten in één activeringsdataflow te activeren. Als u meer segmenten moet activeren, maakt u een nieuw doel op hetzelfde account.

[!DNL DataX] is tariefbeperkt binnen de limieten voor taxonomie en publieksposten die in de [DataX-documentatie](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Foutcode | Foutbericht | Beschrijving |
|---------|----------|---------|
| 429 Te veel verzoeken | Snelheidslimiet overschreden per uur **(Limiet: 100)** | Aantal toegestane verzoeken in een uur per leverancier. |

{style=&quot;table-layout:auto&quot;}

## Ondersteunde identiteiten {#supported-identities}

[!DNL Verizon Media] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (E-mail, GAID, IDFA) die worden gebruikt in de bestemming Verizon Media. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Gevallen gebruiken {#use-cases}

[!DNL DataX] API&#39;s zijn beschikbaar voor adverteerders die zich willen richten op een specifieke doelgroep die e-mailadressen heeft verwijderd in [!DNL Verizon Media] (VMG) kan snel een nieuw segment maken en de gewenste doelgroep duwen met VMG&#39;s bijna-real-time API.

## Verbinden met doel {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

![Yahoo DataX-doelkaart in gebruikersinterface van Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL MDM ID]**: Dit is een unieke id in [!DNL Yahoo DataX] en het is een verplicht veld voor het instellen van gegevensexport naar deze bestemming . Neem contact op met uw [!DNL Yahoo DataX] accountmanager.  Met MDM IDs, kunnen de gegevens voor gebruik slechts met een bepaalde reeks exclusieve gebruikers (zoals eerste partijgegevens voor adverteerders) worden beperkt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten naar een doel activeren](../../ui/activate-segment-streaming-destinations.md) voor instructies over het activeren van publiekssegmenten aan bestemmingen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen {#additional-resources}

Lees voor meer informatie de [!DNL Yahoo/Verizon Media] [documentatie over [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
