---
title: Verizon MediaYahoo DataX-verbinding
description: DataX is een geaggregeerde Verizon Media/Yahoo-infrastructuur die verschillende componenten host die Verizon Media/Yahoo in staat stellen gegevens met zijn externe partners op een veilige, geautomatiseerde en schaalbare manier uit te wisselen.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# [!DNL Verizon Media/Yahoo DataX] verbinding

## Overzicht {#overview}

[!DNL DataX] is een aggregaat [!DNL Verizon Media/Yahoo] infrastructuur die gastheren diverse componenten die toelaten [!DNL Verizon Media/Yahoo] gegevens op een veilige, geautomatiseerde en schaalbare manier met haar externe partners uit te wisselen.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door [!DNL Verizon Media/Yahoo]s [!DNL DataX] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

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
>Bij activering van meer dan 100 soorten publiek naar [!DNL Verizon Media/Yahoo DataX], zou u tarief beperkende fouten van de bestemming kunnen ontvangen. Wanneer u het publiek activeert op deze bestemming, probeert u minder dan 100 soorten publiek te activeren in één activeringsgegevensstroom. Als u meer segmenten moet activeren, maakt u een nieuw doel op hetzelfde account.

[!DNL DataX] is tariefbeperkt binnen de limieten voor taxonomie en publieksposten die in de [DataX-documentatie](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Foutcode | Foutbericht | Beschrijving |
|---------|----------|---------|
| 429 Te veel verzoeken | Snelheidslimiet overschreden per uur **(Limiet: 100)** | Aantal toegestane verzoeken in een uur per leverancier. |

{style="table-layout:auto"}

## Ondersteunde identiteiten {#supported-identities}

[!DNL Verizon Media] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (E-mail, GAID, IDFA) die worden gebruikt in de bestemming Verizon Media. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Gebruiksscenario’s {#use-cases}

[!DNL DataX] API&#39;s zijn beschikbaar voor adverteerders die zich willen richten op een specifieke doelgroep die e-mailadressen heeft verwijderd in [!DNL Verizon Media] (VMG) kan snel een nieuw publiek creëren en de gewenste publieksgroep duwen gebruikend de bijna-real-time API van VMG.

## Verbinden met doel {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

![Yahoo DataX-doelkaart in platforminterface](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL MDM ID]**: Dit is een unieke id in [!DNL Yahoo DataX] en het is een verplicht veld voor het instellen van gegevensexport naar deze bestemming . Neem contact op met uw [!DNL Yahoo DataX] accountmanager.  Met MDM IDs, kunnen de gegevens voor gebruik slechts met een bepaalde reeks exclusieve gebruikers (zoals eerste partijgegevens voor adverteerders) worden beperkt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar bestemmingen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen {#additional-resources}

Lees voor meer informatie de [!DNL Yahoo/Verizon Media] [documentatie over [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
