---
title: Aanvullende informatie van oktober 2024 voor Adobe Experience Platform
description: Aanvullende informatie van oktober 2024 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f30a124a40928abf69366d311131e353c2779191
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 79%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: 29 oktober 2024**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Dataverzameling](#data-collection-)
- [Bestemmingen](#destinations)
- [Segmentatieservice](#segmentation-service)
- [Sandboxes](#sandboxes)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten krijgt in de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnames.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Distiller-sjablonen voor gegevens | Verken meerdere sjablonen om gestructureerde inzichten in de gegevens van het publiek te verkrijgen. Gebruik dashboards zoals **Geavanceerd[!UICONTROL Audience Overlaps]**, **[!UICONTROL Audience Comparison]**, **[!UICONTROL Audience Trends]**, en **[!UICONTROL Audience Identity Overlaps]** om gegevensgestuurde besluiten te nemen, segmentatie te optimaliseren en betrokkenheidsstrategieën te verbeteren. Zie de [ gids van de Malplaatjes van Distiller van Gegevens ](../../dashboards/sql-insights-query-pro-mode/templates/overview.md) voor meer details. |
| Geavanceerde publieksoverlap | Analyseer snel de snijpunten van de doelgroep voor specifieke doelgroepen of bekijk alle overlappingen om waardevolle inzichten in de gehele doelgroep aan het licht te brengen. Gebruik deze inzichten om segmentatie te verfijnen, overtollig overseinen te verminderen, en gerichtere campagnes voor betere marketing efficiency te creëren. Zie de [ Geavanceerde gids van de Overlappingen van de Publiek ](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md) voor meer details. |
| Verbeteringen in de vergelijkingsmodus Publiek | Bekijk een zij-aan-zij vergelijking van zeer belangrijke metriek tussen verschillende publieksgroepen gebruikend het **dashboard van de Vergelijking van het publiek 0}.** Met dit dashboard kunt u specifieke tijdkaders en KPIs, zoals publieksgrootte en identiteitssamenstelling selecteren, om meer geïnformeerde besluiten over publiekssegmentatie en het richten van strategieën te nemen. Lees de [ gids van de Vergelijking van het Publiek ](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) voor meer informatie. |
| Visualisatie van trends bij het publiek | Analyseer in de loop der tijd publieksmetriek met het **[!UICONTROL Audience Trends]** dashboard. Tendensen visualiseren voor de grootte van het publiek, het aantal identiteiten en het aantal afzonderlijke identiteitsprofielen om u te helpen de evolutie van het publiek volgen, de groei meten en uw betrokkenheidsstrategieën verfijnen. Zie de [ gids van de Trends van de Volheid ](../../dashboards/sql-insights-query-pro-mode/templates/trends.md) voor meer details. |
| Analyse van overlappingen van identiteiten | Analyseer identiteitsoverlap in geselecteerde soorten publiek met het dashboard **[!UICONTROL Audience Identity Overlaps]** . Bekijk identiteitstendensen en onderverdelingen om te begrijpen hoe de verschillende identiteitstypes binnen uw publiek betrekking hebben, verbeterend identiteit het stitching en verbeterend klantensegmenteringsnauwkeurigheid. Verwijs naar de [ gids van de Overlappingen van de Identiteit van het publiek ](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md) voor meer details. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, inclusief het verlenen van toegangsrechten en het maken van aangepaste widgets, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Tags en extensies | Adobe Analytics JSON-weergave | U kunt nu de Adobe Analytics-tagextensie gebruiken om eVars, props en gebeurtenisinstellingen als JSON te onderzoeken. Deze kunnen nu worden opgenomen in de Web SDK-extensie en worden geëxporteerd voor bewerking. U kunt deze gegevens ook uploaden of kopiëren en op uw apparaat opslaan. Raadpleeg de [documentatie voor Adobe Analytics-extensies](../../tags/extensions/client/analytics/overview.md) voor meer informatie. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie het [overzicht van dataverzameling](../../collection/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| ----------- | ----------- |
| [Ondersteuning voor het exporteren van arrays is algemeen beschikbaar](../../destinations/ui/export-arrays-calculated-fields.md) | Alle klanten kunnen nu de optie **[!UICONTROL Add calculated field]** gebruiken bij het activeren van doelgroepen *naar op bestanden gebaseerde bestemmingen* om hele arrays of elementen van arrays te exporteren. Houd er rekening mee dat u nog steeds de functie `array_to_string` moet gebruiken om de array in het doelbestand af te vlakken tot een tekenreeks. <br> ![Voeg berekende veldselectie toe met functies en velden.](../2024/assets/october/array-export.gif "Voeg een berekend veld toe met een selectie van de functie array_to_string en de organisatie-array."){width="250" align="center" zoomable="yes"} |
| [Verbeterde rapportagenauwkeurigheid voor streamingbestemmingen](/help/destinations/ui/export-datasets.md) | Vanaf oktober 2024 brengt Adobe een update uit om de rapportagenauwkeurigheid voor streamingbestemmingen te verbeteren. Deze verbetering zorgt voor een betere afstemming tussen het Experience Platform en de rapportage van de bestemmingsplatforms. <br> Vóór deze update werden alle activeringspogingen in **[!UICONTROL Identities failed]** opgenomen. Na deze update wordt alleen de laatste activeringspoging opgenomen in het totale aantal. <br> Deze verbetering is momenteel van toepassing op de [Google Customer Match-bestemming](../../destinations/catalog/advertising/google-customer-match.md), maar wordt geleidelijk uitgerold naar andere Experience Platform-streamingbestemmingen. Na deze verbetering kunnen de gebruikers van de [Google Customer Match-bestemming](../../destinations/catalog/advertising/google-customer-match.md) een verwachte daling in hun totale aantal **[!UICONTROL Identities failed]** zien. |
| Flexibele implicaties voor doelgroepevaluatie bij [activering van batchdoelgroepen](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Als u [flexibele doelgroepevaluatie](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) uitvoert op doelgroepen die al zijn ingesteld om te worden geactiveerd na segmentevaluatie, worden de doelgroepen geactiveerd zodra de flexibele doelgroepevaluatietaak is voltooid, ongeacht eventuele eerdere dagelijkse activeringstaken. <br> Dit kan ertoe leiden dat een doelgroep meerdere keren per dag wordt geëxporteerd, op basis van uw handelingen. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| [!BADGE Beperkte beschikbaarheid]{type=Informative} Flexibele doelgroepevaluatie | Dankzij flexibele doelgroepevaluatie kunt u snel en op aanvraag nieuwe doelgroepen creëren voor tijdgevoelige communicatie. Meer informatie over deze nieuwe functie vindt u in de [documentatie voor Audience Portal](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service] raadpleegt u het [segmentatieoverzicht](../../segmentation/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen, biedt Experience Platform sandboxes die één Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verder ontwikkeld.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Sandbox-toolpakket delen | U kunt nu sandbox-tools gebruiken om eenvoudig sandbox-configuraties te exporteren en importeren tussen sandboxen in verschillende organisaties. Er zijn nu twee categorieën van gedeelde pakketten beschikbaar:<br><ul><li>**[Privépakket](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** gebruik het delen van privépakketten met organisaties die de aanvraag tot delen van de bronorganisatie hebben goedgekeurd.</li><li>**[Openbaar pakket](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** openbare pakketten kunnen worden gedeeld zonder aanvullende goedkeuringen en kunnen eenvoudig worden geïmporteerd met behulp van de payload van het pakket.</li></ul><br>Raadpleeg de handleiding over [het delen van pakketten tussen organisaties](../../sandboxes/ui/sharing-packages-across-orgs.md) voor meer informatie over deze functies. |
| [Pakket delen](https://experienceleague.adobe.com/nl/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) in de sandbox-tool-API | Gebruik de sandbox-tool-API om verzoeken in te dienen bij twee nieuwe eindpunten, `/handshake` en `/transfer`, voor het delen tussen organisaties, ophalen en maken van verzoeken voor het delen van pakketten. Er is een extra aanvraag toegevoegd aan het `/packages`-eindpunt om de payload van een pakket op te halen. |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, raadpleegt u het [ overzicht van sandboxes](../../sandboxes/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het filteren van entiteiten met standaardactiviteit in [!DNL Marketo Engage] | U kunt de [!DNL Flow Service]-API gebruiken om voor het filteren van entiteiten met standaardactiviteit bij het opnemen van gegevens uit uw [!DNL Marketo Engage]-bron. Raadpleeg de gids over het [filteren [!DNL Marketo]  van standaardactiviteitsgegevens](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).