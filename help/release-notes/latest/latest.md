---
title: Opmerkingen bij de release van Adobe Experience Platform, oktober 2024
description: Aanvullende informatie voor de versie van oktober 2024 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f30a124a40928abf69366d311131e353c2779191
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 36%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: woensdag 29 oktober 2024**

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
| Tags en extensies | Adobe Analytics JSON View | U kunt nu de extensie Adobe Analytics-tags gebruiken om eVars, props en gebeurtenisinstellingen te controleren als JSON. Deze kan nu worden opgenomen in de SDK-extensie van Web en worden geëxporteerd voor bewerking. U kunt deze gegevens ook uploaden of kopiëren en opslaan op uw apparaat. Lees de [ de uitbreidingsdocumentatie van Adobe Analytics ](../../tags/extensions/client/analytics/overview.md) voor meer informatie. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie het [overzicht van dataverzameling](../../collection/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| ----------- | ----------- |
| [ de uitvoersteun van de Serie algemeen beschikbaar ](../../destinations/ui/export-arrays-calculated-fields.md) | Alle klanten kunnen de **[!UICONTROL Add calculated field]** optie nu gebruiken wanneer het activeren van publiek *aan op dossier-gebaseerde bestemmingen* om volledige series of elementen van series uit te voeren. U moet de functie `array_to_string` nog steeds gebruiken om de array af te vlakken in een tekenreeks in het doelbestand. <br> ![ voeg berekende gebiedsselectie met functies en gebieden toe.](../2024/assets/october/array-export.gif " voeg berekend gebied met een selectie van de serie_to_string functie en de organisatieserie toe."){width="250" align="center" zoomable="yes"} |
| [ Meldend nauwkeurigheidsverhogingen voor het stromen bestemmingen ](/help/destinations/ui/export-datasets.md) | Vanaf oktober 2024 wordt door Adobe een update uitgevoerd om de rapportnauwkeurigheid voor streamingdoelen te verbeteren. Deze verbetering zorgt voor een betere afstemming tussen het Experience Platform en de doelplatforms die rapporteren. <br> Vóór deze update heeft **[!UICONTROL Identities failed]** alle activeringspogingen opgenomen. Na deze update wordt alleen de laatste activeringspoging opgenomen in het totale aantal. <br> Deze verhoging is momenteel op de [ bestemming van de Gelijke van de Klant van Google ](../../destinations/catalog/advertising/google-customer-match.md) van toepassing maar zal geleidelijk aan andere Experience Platform die bestemmingen stromen worden uitgevoerd. Na deze verhoging, kunnen de gebruikers van de [ bestemming van de Gelijke van de Klant van Google ](../../destinations/catalog/advertising/google-customer-match.md) een verwachte daling in hun **[!UICONTROL Identities failed]** telling zien. |
| De flexibele implicaties van de publieksevaluatie op [ activering van het partijpubliek ](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Als u [ flexibele publieksevaluatie ](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) op publiek in werking stelt die reeds om na segmentevaluatie worden geactiveerd, zal het publiek worden geactiveerd zodra de flexibele baan van de publieksevaluatie, ongeacht om het even welke vorige dagelijkse activeringstaken eindigt. <br> Dit kan ertoe leiden dat een publiek meerdere keren per dag wordt geëxporteerd, op basis van uw handelingen. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| [!BADGE  Beperkte Beschikbaarheid ] {type=Informatieve} Flexibele publieksevaluatie | De flexibele publieksevaluatie laat u snel nieuw publiek op bestelling voor tijd-gevoelige mededelingen tot stand brengen. Meer informatie over deze nieuwe eigenschap kan binnen de [ Poortdocumentatie van het Poort van het Publiek ](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) worden gevonden. |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service] raadpleegt u het [segmentatieoverzicht](../../segmentation/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen, biedt Experience Platform sandboxes die één Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verder ontwikkeld.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gereedschapspakket met sandbox delen | U kunt sandboxgereedschappen nu gebruiken om sandboxconfiguraties tussen sandboxen in verschillende organisaties gemakkelijk te exporteren en te importeren. Er zijn nu twee categorieën van gedeelde pakketten beschikbaar:<br><ul><li>**[Privé pakket ](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** Gebruik privé pakket delend met organisaties die het delen verzoek van de bronorganisatie hebben goedgekeurd.</li><li>**[Openbaar pakket ](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** de Openbare pakketten kunnen zonder extra goedkeuringen worden gedeeld en gemakkelijk worden ingevoerd gebruikend de lading van het pakket.</li></ul><br> voor meer informatie over deze eigenschappen, lees de gids over [ delend pakketten over organisaties ](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [ Pakket delend ](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) in het zandbak tooling API | Met de API voor gereedschappen voor sandboxen kunt u aanvragen indienen bij twee nieuwe eindpunten `/handshake` en `/transfer` voor het delen tussen organisaties, het ophalen en het maken van aanvragen voor het delen van pakketten. Er is een extra aanvraag toegevoegd aan het eindpunt van `/packages` om de lading van een pakket op te halen. |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het filteren van entiteiten met standaardactiviteit in [!DNL Marketo Engage] | U kunt de API van [!DNL Flow Service] gebruiken om entiteiten met standaardactiviteit te filteren wanneer u gegevens uit uw [!DNL Marketo Engage] -bron opneemt. Lees de gids over [ het filtreren  [!DNL Marketo]  standaardactiviteitengegevens ](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).