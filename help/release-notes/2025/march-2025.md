---
title: Aanvullende informatie van maart 2025 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2025 voor Adobe Experience Platform.
exl-id: 3da1c912-2581-4afa-bd21-0b8303531dcd
source-git-commit: edcdf84a8cb954c15f7dd235fb14cf14e11e22c8
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 26%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:donderdag 26 maart 2025**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [Aanvullende informatie voor Adobe Experience Platform](#adobe-experience-platform-release-notes)
   - [Dashboards](#dashboards)
   - [Bestemmingen](#destinations)
   - [Samenstelling van Federated-doelgroep](#federated-audience-composition)
   - [Segmentatieservice](#segmentation-service)
   - [Bronnen](#sources)

## Dashboards {#dashboards}

Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten krijgt in de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnames.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Dashboard voor licentiegebruik op basis van cijfers | Het dashboard van het vergunningsgebruik omvat nu gestroomlijnde UI met twee lusjes: **Metriek** en **Producten**. Het nieuwe **lusje van Metriek 0} {biedt een geconsolideerde mening van alle trackable vergunningsmetriek over uw gekochte producten aan.** Elke metrische waarde bevat een inline-infopictogram met beschrijvingen en bijbehorende producten. Gebruikers kunnen productie- of ontwikkelingssandboxen selecteren, historische gebruikstrends in interactieve diagrammen bekijken en sandboxspecifieke gegevens exporteren als CSV-bestanden. Deze updates stroomlijnen het bijhouden van licenties en bieden duidelijkere inzichten. Leer meer in de [ handleiding van het dashboard van het vergunningsgebruik ](../../dashboards/guides/license-usage.md) voor meer details. |
| Bijgewerkte voorspellingsfrequentie | Het dashboard van het vergunningsgebruik verstrekt nu nauwkeurigere inzichten in geprojecteerd verbruik door gebruiksvoorspellingen **wekelijks** in plaats van maandelijks bij te werken. Deze prognoses geven een schatting van het gebruik in de komende zes weken aan, op basis van recente trends. Deze wijziging maakt snellere besluitvorming, eerdere interventie en verbeterde licentieplanning mogelijk. Zie de [ handleiding van het dashboard van het vergunningsgebruik ](../../dashboards/guides/license-usage.md#predicted-usage) voor details. |
| Bijgewerkte metrische beschrijvingen in UI | De metrische definities in het gebruiksdashboard voor licenties zijn voor meer duidelijkheid en consistentie herzien. U kunt bijgewerkte beschrijvingen direct in het dashboard nu bekijken gebruikend gealigneerde info pictogrammen naast elke metrisch in **Metriek** tabel. Deze updates maken het gemakkelijker om te begrijpen hoe de metriek worden gevolgd en welke producten zij op van toepassing zijn. Zie de [ handleiding van het dashboard van het vergunningsgebruik ](../../dashboards/guides/license-usage.md#available-metrics) voor meer details. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [ De verbinding van Mensen van de Vereis ](/help/destinations/catalog/advertising/demandbase-people.md) | Gebruik de verbinding [!DNL Demandbase People] om profielen voor uw Demandbase-campagnes voor doelgroepen, personalisatie en onderdrukking te activeren. |
| [ Bombora rekeningsverbinding ](/help/destinations/catalog/advertising/bombora.md) | Gebruik de [!DNL Bombora] verbinding om profielen voor uw campagnes Bombora voor publiek te activeren richtend, verpersoonlijking, en onderdrukking, die op [ wordt gebaseerd rekeningspubliek ](/help/segmentation/types/account-audiences.md). |
| [ Attributen van het Luchtschip ](/help/destinations/catalog/mobile-engagement/airship-attributes.md) verbetering | Vanaf 25 maart 2025 ziet u twee **[!UICONTROL Airship Attributes]** kaarten naast elkaar in de doelcatalogus. Dit is toe te schrijven aan een interne verbetering aan de bestemmingsdienst. De naam van de bestaande **[!UICONTROL Airship Attributes]** doelconnector is gewijzigd in **[!UICONTROL (Deprecated) Airship Attributes]** en u hebt nu een nieuwe kaart met de naam **[!UICONTROL Airship Attributes]** beschikbaar. <br> Gebruik de **[!UICONTROL Airship Attributes]** -verbinding in de catalogus voor nieuwe gegevensstromen voor activering. Als u actieve gegevens naar de [!DNL (Deprecated) Airship Attributes] -bestemming hebt, worden deze automatisch bijgewerkt, zodat u geen actie hoeft te ondernemen. <br> als u dataflows door de [ Dienst API van de Stroom ](https://developer.adobe.com/experience-platform-apis/references/destinations/) creeert, moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] aan de volgende waarden bijwerken: <ul><li> Stroomspecificatie-id: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> Verbindingsspecificatie-id: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| [Verbeterde rapportagenauwkeurigheid voor streamingbestemmingen](../../dataflows/ui/monitor-destinations.md) | Vanaf maart 2025 implementeert Adobe een update om de rapportnauwkeurigheid voor streamingdoelen te verbeteren. Deze verbetering zorgt voor een betere afstemming tussen de rapportage in Experience Platform en de doelplatforms. <br> Vóór deze update werden alle activeringspogingen in **[!UICONTROL Identities failed]** opgenomen. Na deze update wordt alleen de laatste activeringspoging opgenomen in het totale aantal. <br> Deze verbetering is van toepassing op alle streamingdoelen. <br> Na deze verbetering zien gebruikers van streamingdoelen mogelijk een verwachte daling in hun **[!UICONTROL Identities failed]** aantal. |
| [ Kaart-type de uitvoersteun van het gebied voor onderneming en randbestemmingen ](/help/destinations/ui/export-arrays-maps-objects.md) | Wanneer het uitvoeren van gegevens naar de [ Kinesis van Amazon ](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [ HTTP API ](/help/destinations/catalog/streaming/http-destination.md), [ Azure de Hubs van de Gebeurtenis ](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), en [ Adobe Target ](/help/destinations/catalog/personalization/adobe-target-connection.md) bestemmingen, kunt u kaart-type gebieden voor uitvoer in de afbeeldingsstap van het activeringswerkschema nu selecteren. <br> ![ de kaart-type van de Uitvoer gebied aan ondernemingsbestemming.](../2025/assets/march/export-map.png " de uitvoer kaart-type gebied aan ondernemingsbestemming."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Samenstelling van Federated-doelgroep {#federated-audience-composition}

Voor informatie over de recentste updates voor de Federatieve Samenstelling van het Publiek, lees [ specifieke versienota&#39;s ](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes) hier.

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen in de accountAudience Builder | In de Bouwer van de Publiek, kunt u attributen aan slechts vertoning bevolkte attributen nu filtreren evenals meningssummiere gegevens voor deze bevolkte attributen. Meer informatie over deze verhogingen kan in de ](../../rtcdp/segmentation/audience-builder.md) documentatie van de Bouwer van het publiek worden gevonden 0}.[ |
| Flexibele publieksevaluatie algemene beschikbaarheid | De flexibele publieksevaluatie is nu over het algemeen beschikbaar! U kunt flexibele publieksevaluatie gebruiken om nieuwe publiek op bestelling voor tijd-gevoelige mededelingen tot stand te brengen. Meer informatie over flexibele publieksevaluatie kan in het [ flexibele overzicht van de publieksevaluatie ](../../segmentation/methods/flexible-audience-evaluation.md) worden gevonden. |

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Nieuwe bronnen**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Bombora Intent] | De [!DNL Bombora Intent] -bron is nu beschikbaar in de broncatalogus. Gebruik deze bron om: <ul><li>Integreer Bombora&#39;s gegevens van de Intentie van de Vennootschap om rekeningen te identificeren die actief uw producten of de diensten onderzoeken.</li><li>Prioriteit geven aan accounts op de markt om precieze segmenten te maken en ABM-campagnes met hyperlinks uit te voeren. Zo kunt u ervoor zorgen dat uw marketinginspanningen zich richten op die accounts die het meest converteren.</li><li>Gebruik intenties-gedreven strategieën om te optimaliseren en uit te geven, de betrokkenheid te verhogen en het investeringsrendement te maximaliseren.</li></ul> Voor meer informatie, lees de gids op [ verbindend uw  [!DNL Bombora]  rekening met Experience Platform ](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | De [!DNL Demandbase Intent] -bron is nu beschikbaar in de broncatalogus. Gebruik deze bron om: <ul><li>De accountintentiegegevens van de Demandbase integreren om rekening met hoge rente te identificeren op basis van real-time contracten.</li><li>Door de sterkste intentsignalen voorrang te geven, kunt u nauwkeurige segmenten tot stand brengen en hyper-gerichte campagnes leveren om ervoor te zorgen dat uw marketing inspanningen zich op rekeningen concentreren die het meest waarschijnlijk zullen omzetten.</li><li>Activeer intentgestuurde strategieën om optimalisatie van advertentie-uitgaven, verhoogde betrokkenheid en hogere ROI mogelijk te maken.</li></ul> Voor meer informatie, lees de gids op [ verbindend uw  [!DNL Demandbase]  rekening met Experience Platform ](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen aan de bron [!DNL Google Ads] | U kunt de [[!DNL Google Ads]  bron ](../../sources/connectors/advertising/ads.md) nu gebruiken om gezamenlijke gegevens in te voeren. U kunt [!DNL Google Ads Query Builder] gebruiken om de attributen, de segmenten, en de middelen te specificeren die u aan Experience Platform wilt opnemen. Voor meer informatie, lees de gids op [ verbindend uw  [!DNL Google Ads]  rekening met Experience Platform ](../../sources/tutorials/ui/create/advertising/ads.md). |
| Verbeteringen aan de bron [!DNL Microsoft Dynamics] | U kunt nu de primaire sleutel van een bepaalde [!DNL Microsoft Dynamics] lijst specificeren wanneer het onderzoeken van de inhoud en de structuur van uw gegevens. Gebruik deze functie om uw query&#39;s te optimaliseren met de [!DNL Microsoft Dynamics] -bron. Voor meer informatie, lees de gids op [ verbindend uw  [!DNL Microsoft Dynamics]  bron met Experience Platform gebruikend API ](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Ondersteuning voor API-sleutelverificatie in Self-Serve Sources (Batch SDK) | U kunt API zeer belangrijke authentificatie als authentificatietype nu gebruiken wanneer het integreren van een nieuwe bron met Zelfbediening Bronnen (Batch SDK). Voor meer informatie, lees de gids bij [ vormend uw auth specificatie in Partij SDK ](../../sources/sources-sdk/config/authspec.md). |
| Ondersteuning voor op kenmerken gebaseerd toegangsbeheer in bronnen | U kunt attribuut-gebaseerde toegangsbeheerfuncties tegen uw brongegevens nu gebruiken. Lees de volgende hulplijnen voor meer informatie: <ul><li>[ pas etiketten op uw brongegevens toe gebruikend API ](../../sources/tutorials/api/labels.md)</li><li>[ past etiketten op uw brongegevens toe gebruikend UI ](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).
