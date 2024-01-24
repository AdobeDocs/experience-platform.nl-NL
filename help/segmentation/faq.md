---
title: Publiek Veelgestelde vragen
description: Ontdek antwoorden op veelgestelde vragen over publiek en andere op segmentatie betrekking hebbende concepten.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 762a7fc7dd00657e4e710eb763c5bb63b210593a
workflow-type: tm+mt
source-wordcount: '2726'
ht-degree: 0%

---

# Veelgestelde vragen

Adobe Experience Platform [!DNL Segmentation Service] verstrekt een gebruikersinterface en RESTful API die u toestaat om publiek door segmentdefinities of andere bronnen van uw te creëren [!DNL Real-Time Customer Profile] gegevens. Dit publiek wordt centraal gevormd en gehandhaafd op Platform, en gemakkelijk toegankelijk door om het even welke oplossing van de Adobe. Hieronder volgt een lijst met veelgestelde vragen over publiek en segmentatie.

## Poort publiek

De volgende sectie maakt een lijst van vragen met betrekking tot de Portaal van de Publiek.

### Heb ik toegang tot het Portaal van het Publiek en de Samenstelling van het Publiek?

Poort van publiek en Audience Composition zijn beschikbaar voor alle klanten van Real-Time CDP Premier en Ultimate (B2C, B2B en B2P Editions) en Journey Optimizer Select, Prime, Ultimate Starter en Ultimate.

Op dit moment worden alleen op profielen gebaseerde soorten publiek ondersteund. Ondersteuning voor publiek op basis van account wordt in een latere release toegevoegd.

### Worden extern geproduceerd vooraf gebouwd publiek gesteund met het Portaal van het Publiek?

Ja, extern gegenereerde, vooraf gebouwde doelgroepen worden ondersteund met Poorten publiek. Op dit moment kunt u een extern gegenereerd publiek importeren via een CSV-bestand. In de toekomst kunt u een publiek toevoegen via batch- of streaminggebaseerde bronconnectors.

### Welke toestemmingen moet ik hebben om extern geproduceerd publiek te uploaden?

Als u extern gegenereerde soorten publiek wilt uploaden, hebt u zowel de machtigingen &quot;Beheren publiek/segmenten&quot; als &quot;Gegevenssets beheren&quot; nodig. Er zijn geen specifieke op rol-gebaseerde controles vereist om extern geproduceerd publiek te uploaden.

### Wat gebeurt er als ik een extern gegenereerd publiek upload?

Wanneer u een extern gegenereerd publiek uploadt, worden de volgende items gemaakt:

- Gegevensset
   - De dataset zal binnen de datasetinventaris zichtbaar zijn, en de naam van de dataset zal zijn **zelfde** als de naam van het extern gegenereerde publiek dat u hebt geüpload.
- Batchtaak
   - Een batchtaak zal **automatisch** uitgevoerd wanneer u een extern gegenereerd publiek uploadt. Dit betekent dat je dat doet **niet** moet wachten tot de dagelijkse segmentatietaak wordt uitgevoerd om het extern gegenereerde publiek te activeren.
- Ad-hocschema
   - A **new** XDM-schema wordt gemaakt voor gebruik met het extern gegenereerde publiek. De velden in dit XDM-schema worden benoemd voor gebruik met de gegevensset die ook is gemaakt.

### Wat is een extern gegenereerd publiek dat bestaat uit deze gegevens en wat gebeurt er met deze gegevens als het wordt geïmporteerd naar Platform?

Tijdens de workflow voor het importeren van externe doelgroepen moet u opgeven welke kolom in het CSV-bestand overeenkomt met **Primaire identiteit**. Een voorbeeld van een primaire identiteit is e-mailadres, ECID of een naamruimte die specifiek is voor de organisatie.

De gegevens die aan deze primaire identiteitskolom zijn gekoppeld, **alleen** gegevens die aan het profiel zijn gekoppeld. Als er geen bestaande profielen zijn die overeenkomen met de gegevens in de primaire identiteitskolom, wordt een nieuw profiel gemaakt. Dit profiel is echter in wezen een zwevend profiel, aangezien **nee** attributen of ervaringsgebeurtenissen worden aan dit profiel gekoppeld.

Alle andere gegevens binnen het extern gegenereerde publiek worden in aanmerking genomen **payload-kenmerken**. Deze kenmerken kunnen **alleen** worden gebruikt voor personalisatie en verrijking tijdens activering, en **niet** gekoppeld aan een profiel. Deze kenmerken worden echter opgeslagen in het datumpigment.

Terwijl naar het extern gegenereerde publiek kan worden verwezen bij het maken van soorten publiek met de Segment Builder, kunnen de afzonderlijke profielkenmerken **kan** worden gebruikt.

### Kan ik extern gegenereerde publieksgegevens combineren met een bestaand profiel in Platform?

Ja, het extern gegenereerde publiek wordt samengevoegd met het bestaande profiel in Platform als de primaire id&#39;s overeenkomen. Het kan 24 uur duren voordat deze gegevens met elkaar in overeenstemming zijn. Als profielgegevens nog niet bestaan, wordt een nieuw profiel gemaakt wanneer de gegevens worden ingevoerd.

### Kan ik een extern gegenereerd publiek gebruiken om andere soorten publiek op te bouwen?

Ja, elk extern gegenereerd publiek wordt weergegeven in de publieksinventaris en kan worden gebruikt bij het opbouwen van publiek binnen het [Segment Builder](./ui/segment-builder.md).

### Kan ik extern geüploade kenmerken gebruiken als onderdeel van segmentatie?

Nee, dat kan niet. Profielkenmerken moeten langetermijnkenmerken zijn, terwijl extern gegenereerde publieksgegevens die worden geüpload alleen contextuele gegevens bevatten die aan dat extern gegenereerde publiek zijn gekoppeld.

De extern gegenereerde contextafhankelijke gegevens van het publiek, of verrijkingskenmerken, zijn **niet** duurzaam, omdat hun levenscyclus aan het geüploade publiek is gebonden. Als gevolg hiervan zijn deze verrijkingskenmerken vanwege hun voorbijgaande aard **niet** beschikbaar voor gebruik in segmentatie.

Wanneer u uw publiek echter toewijst aan batchbestemmingen of op bestanden gebaseerde bestemmingen, kunt u deze extern gegenereerde verrijkingskenmerken gebruiken om uw publiek en verdere downstreamactiveringen te verhogen.

Lees de handleiding voor meer informatie over deze mogelijkheid [publieksgegevens activeren om exportdoelen voor batchprofielen te maken](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Bestaat er een specifiek fusiebeleid voor extern gegenereerde doelgroepen?

Het organisatiespecifieke standaard samenvoegingsbeleid wordt automatisch toegepast wanneer het uploaden van extern geproduceerd publiek. U kunt echter wel het samenvoegbeleid wijzigen dat wordt toegepast op het extern gegenereerde publiek tijdens de workflow voor het importpubliek.

### Waar kan ik extern gegenereerde publiek activeren?

Een extern gegenereerd publiek kan aan elke RTCDP-bestemming worden toegewezen en kan in Adobe Journey Optimizer-campagnes worden gebruikt.

### Hoe snel zijn extern gegenereerde doelgroepen klaar voor activering?

Als de gegevens van het extern gegenereerde publiek worden geactiveerd voor een streamingdoel, zijn deze binnen twee uur beschikbaar.

Als de gegevens worden geactiveerd voor een batchbestemming, worden de gegevens van het extern gegenereerde publiek gesynchroniseerd met de volgende segmentatietaak van 24 uur.

### Kan ik een extern gegenereerd publiek verwijderen?

Op dit moment kunt u alleen een extern gegenereerd publiek deactiveren. In deze status worden profielen **zal** actief blijven voor gebruik in downstreamtoepassingen. Ondersteuning voor het verwijderen van extern gegenereerde soorten publiek wordt toegevoegd aan een volgende release.

### Wat moet ik doen als ik per ongeluk een extern gegenereerd publiek heb geüpload?

Als u per ongeluk een extern gegenereerd publiek hebt geüpload en u de gegevens wilt verwijderen, kunt u de aan het publiek gekoppelde profielen wissen door een CSV-bestand met één rij en geen gegevens te uploaden.

### Hoe lang duurt het extern gegenereerde publiek?

De huidige gegevensvervaldatum voor extern gegenereerd publiek is **dertig dagen**. Deze gegevensvervaldatum is gekozen om de hoeveelheid overtollige gegevens te verminderen die binnen uw organisatie worden opgeslagen.

Nadat de gegevensvervalperiode overgaat, zal de bijbehorende dataset nog zichtbaar binnen de datasetinventaris zijn, maar u zult **niet** kan het publiek activeren en het aantal profielen wordt weergegeven als nul.

### Wat vertegenwoordigen de verschillende levenscyclusstaten?

In het volgende diagram worden de verschillende levenscyclusstatussen beschreven, wat ze vertegenwoordigen, waar publiek met die status kan worden gebruikt, en het effect op segmentatiegeleidingen.

| Staat | Definitie | Zichtbaar in Audience Portal? | Zichtbaar in Doelen? | Heeft invloed op segmentatielimieten? | Gevolgen voor het publiek | Gevolgen voor de publieksevaluatie | Kan worden gebruikt bij andere doelgroepen? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Concept | Een publiek in de **Concept** de staat is een publiek dat nog in ontwikkeling is en nog niet klaar is om in andere diensten te worden gebruikt . | Ja, maar kan verborgen zijn. | Nee | Ja | Kan tijdens het verfproces worden geïmporteerd of bijgewerkt. | Kan worden geëvalueerd voor een nauwkeurige telling van het aantal uitgeverijen. | Ja, maar het wordt niet aanbevolen dit te gebruiken. |
| Gepubliceerd | Een publiek in de **Gepubliceerd** staat is een publiek dat klaar voor gebruik over alle stroomafwaartse diensten is. | Ja | Ja | Ja | Kan worden geïmporteerd of bijgewerkt. | Evalueerd met batch-, streaming- of randsegmentatie. | Ja |
| Inactief | Een publiek in de **Inactief** state is een publiek dat momenteel niet in gebruik is. Het bestaat nog steeds binnen Platform, maar het zal **niet** kan worden gebruikt totdat het als concept wordt gemarkeerd of gepubliceerd. | Nee, maar kan wel worden weergegeven. | Nee | Nee | Niet meer bijgewerkt. | Niet meer geëvalueerd of bijgewerkt door Platform. | Ja |
| Verwijderd | Een publiek in de **Verwijderd** status is een publiek dat is verwijderd. Het kan enkele minuten duren voordat de gegevens daadwerkelijk zijn verwijderd. | Nee | Nee | Nee | Onderliggende gegevens worden verwijderd. | Er vindt geen gegevensevaluatie of -uitvoering plaats nadat de verwijdering is voltooid. | Nee |
| Actief | Deze status is **verouderd** en wordt vervangen door **Gepubliceerd** status. | N.v.t. | N.v.t. | N.v.t. | N.v.t. | N.v.t. | N.v.t. |

### Hoe zal het Portaal van het Publiek en de Samenstelling van het Publiek met de versie van de Gegevens van de Partner van Real-Time CDP in wisselwerking staan?

Het Portaal van het publiek en de Samenstelling van het Publiek zullen met de Gegevens van de Partner op twee manieren in wisselwerking staan:

1. Als u een partner-verstrekte lijst van het Vooruitzicht gebruikend de klasse en het werkschema van het Profiel van het Vooruitzicht ingaat, zullen de vooruitzichten worden bewaard **apart** vanuit profielen van klanten samenvoegen in de profielservice. Dit betekent dat er lijsten met perspectieven worden opgesteld **niet** verschijnt in of het Portaal van de Poorten van de Publiek of de Samenstelling van de Publiek voor gebruik.
2. Als u partner-Geleverde attributen leveraging om te verrijken **bestaand** first-party profielen, die partner-gegeven-verrijkt publiek **zal** verschijnen in zowel Portaal van het Publiek als Samenstelling van het Publiek voor gebruik.

### Hoe kan ik extra attributen met mijn publiek gebruiken?

Bij het publiek zijn er **twee** verschillende typen extra kenmerken die u kunt toevoegen: (contextafhankelijke) payload-kenmerken en verrijkingskenmerken.

Payload-kenmerken zijn kenmerken die worden opgenomen als onderdeel van de CSV-upload van een extern gegenereerd publiek. Deze kenmerken zijn **niet** In het Real-Time Profiel van de Klant opgenomen, maar kan als deel van een stroomafwaartse bestemming worden gebruikt.

De attributen van de verrijking zijn attributen die uit een dataset komen en met een publiek in de Samenstelling van het Publiek worden verbonden. Deze kenmerken kunnen momenteel alleen worden gebruikt in Adobe Journey Optimizer-campagnes. De steun voor Adobe Journey Optimizer-reizen komt binnenkort, met steun voor downstreambestemmingen in afwachting van de toekomstige vrijlating.

| Activeringskanaal | Soorten publiek van aangepaste CSV-upload | Soorten publiek uit publiekscompositie |
| --- | --- | --- |
| Real-Time CDP-doelen | U kunt zowel de payload-kenmerken als het publiek activeren. | Alleen het publiek kan worden geactiveerd. Verrijkingskenmerken **kan** worden geactiveerd. |
| Adobe Journey Optimizer Campaigns | U kunt het publiek en de payload-kenmerken niet activeren. | U kunt zowel het publiek als de verrijkingskenmerken activeren. |

## Overzicht van het publiek

De volgende secties maken een lijst van vragen met betrekking tot publieksinventaris binnen het Portaal van de Publiek.

### Heb ik extra toestemmingen nodig om de eigenschappen van de publieksinventaris te gebruiken?

Nee, dat doe je niet. Als u over bewerkingsmachtigingen voor het publiek beschikt, kunt u uw mappen en tags maken, bijwerken en beheren in het Poortpubliek van het publiek. Voor meer informatie over het beheren van toestemmingen, gelieve te lezen [machtigingengids beheren](../access-control/ui/permissions.md).

### Is er een limiet voor het aantal mappen dat ik kan maken?

Nee, er is geen limiet voor het aantal mappen dat u kunt maken. Lees voor meer informatie over mappen de [overzichtssectie voor publiek](./ui/overview.md#folders) van het overzicht van de gebruikersinterface van de segmentatieservice.

### Is er een limiet voor het aantal tags dat aan een publiek kan worden toegevoegd?

Nee, er is geen limiet voor het aantal tags dat aan een publiek kan worden toegevoegd. Lees voor meer informatie over tags de [overzichtssectie voor publiek](./ui/overview.md#tags) van het overzicht van de gebruikersinterface van de segmentatieservice.

### Is er een limiet aan het aantal tags dat ik kan maken?

Nee, er is geen limiet aan het aantal tags dat u kunt maken. U kunt echter maximaal **100** categorieën die moeten worden toegepast voor de codes. Voor meer informatie over tagbeheer raadpleegt u de [Handleiding voor tags beheren](../administrative-tags/ui/managing-tags.md).

### Wanneer ik naar een publiek door naam of markering in een ouderomslag zoek, kan ik door de verwante kindomslagen ook zoeken?

Nee, dit gedrag wordt niet ondersteund. U kunt echter de overzichtsweergave van het publiek wijzigen om naar **Alle soorten publiek** en doorzoek vervolgens alle mappen. Lees voor meer informatie over het gebruik van zoekopdrachten in publieksoverzicht de [zoeksectie](./ui/overview.md#search) van het overzicht van de gebruikersinterface van de segmentatieservice.

### Kan ik een publiek automatisch toewijzen aan een map op het moment van het maken?

Op dit moment, nee. Deze mogelijkheid kan echter in de toekomst beschikbaar zijn.

### Kan ik meerdere soorten publiek tegelijk naar een map verplaatsen?

Op dit moment, nee. Deze mogelijkheid kan echter in de toekomst beschikbaar zijn.

## Samenstelling publiek

In de volgende sectie worden vragen over Audience Composition weergegeven.

### Wanneer zou ik de Samenstelling van het Publiek in tegenstelling tot het gebruiken van de Bouwer van het Segment moeten gebruiken?

Zowel de Samenstelling van het publiek als de Bouwer van het Segment hebben belangrijke rollen in de verwezenlijking van het gebouwpubliek in Platform.

De Segment Builder is geschikter voor het publiek **creatie** (voor het opbouwen van een volledig publiek), terwijl Audience Composition geschikter is voor het publiek **curatele en personalisatie** (voor het maken van nieuwe doelgroepen op basis van een bestaand publiek).

De volgende tabel illustreert het verschil tussen de twee services:

| Segment Builder | Samenstelling publiek |
| --------------- | -------------------- |
| <ul><li>Eenmalige doelgroep</li><li>Creeert de basisblokken van publiek van profiel, tijdreeksen, en multi-entiteitsgegevens</li><li>Gebruikt om te maken **één** publiek</li></ul> | <ul><li>Multi-stage publiek genereren, met gebruik van op set gebaseerde bewerkingen</li><li>Gebruikt het publiek dat door de Bouwer van de Segment wordt gecreeerd en past opties van de gegevensverrijking zoals het rangschikken van profielattributen en het verdelen in sub-publiek toe</li><li>Gebruikt om te maken **meerdere** publiek in één keer</li></ul> |

Voor meer informatie over de Segment Builder leest u de [Handleiding Segment Builder](./ui/segment-builder.md). Voor meer informatie over Audience Composition leest u de [Hulplijn Audience Composition](./ui/audience-composition.md).

### Kan ik extern gegenereerd publiek gebruiken in Audience Composition?

Op dit moment, nee. Deze mogelijkheid moet echter in de nabije toekomst beschikbaar zijn.

### Kan ik publiek van de Samenstelling van het Publiek naar alle stroomafwaartse bestemmingen en kanalen verzenden?

Op dit moment, nee. Momenteel kunt u soorten publiek van Audience Composition gebruiken in Adobe Journey Optimizer-campagnes en Real-Time CDP-bestemmingen. Adobe Journey Optimizer-reizen worden in een toekomstige release ondersteund.

### Zijn er aanwijzingen voor het aantal composities?

Op dit moment kunt u alleen **10** gepubliceerde samenstellingen per sandbox. Deze guardrail zal naar verwachting in een toekomstige release worden verhoogd.

### Wat zijn de werkstroominstructies voor Audience Composition?

De compositiecomponent die als volgt plaatst volgt een stijve structuur:

1. U **altijd** beginnen met de [!UICONTROL Audience] blokkeren om uw startactiviteit te selecteren. U kunt maximaal **één** [!UICONTROL Audience] blokkeren.
2. U kunt desgewenst een [!UICONTROL Exclude] blok dat volgt op het [!UICONTROL Audience] blokkeren.
3. U kunt desgewenst een [!UICONTROL Enrich] blok dat volgt op het [!UICONTROL Exclude] blokkeren. U kunt alleen **één** [!UICONTROL Enrich] blok per compositie.
4. U kunt desgewenst een [!UICONTROL Rank] of [!UICONTROL Split] blokkeren. U kunt **alleen** hebben één van deze blokken per samenstelling.
5. U **altijd** met een [!UICONTROL Save] blokkeren om uw publiek op te slaan.

Daarnaast zijn de volgende beperkingen (?) toepassen bij het gebruik van deze blokken:

- Blok splitsen
   - Alleen dit blok ondersteunt **String** gegevenstypen. Het blok Splitsen doet dit **niet** ondersteuning bieden voor het gegevenstype date of boolean.
   - Bovendien doet dit blok **niet** verrijkingskenmerken ondersteunen.
- Blok uitsluiten
   - Dit blok doet **niet** ondersteuning bieden voor het gegevenstype date of boolean.
- Rank blok
   - Dit blok doet **niet** verrijkingskenmerken ondersteunen.

Lees voor meer informatie over het gebruik van Audience Composition de [Handleiding voor compositie van publiek](./ui/audience-composition.md).

### Wanneer wordt het publiek gecreeerd gebruikend de Samenstelling van het Publiek bewaard en geëvalueerd?

Soorten publiek worden automatisch opgeslagen tijdens het maken ervan in Audience Composition. De aanmaaktijd van het publiek is de eerste keer dat deze automatische opslag plaatsvindt.

Nadat het publiek is gemaakt, kan het tot 24 uur duren om te worden geëvalueerd.

### Wanneer kan ik het publiek gebruiken dat ik heb gemaakt?

De doelgroep die is gemaakt in Audience Composition zal **onmiddellijk** verschijnt in het Portaal van het Publiek. Als u het echter in Adobe Journey Optimizer wilt gebruiken, moet u minstens 24 uur wachten na de evaluatie.

### Zijn evaluatietaken zichtbaar in de sectie monitoring?

Momenteel zijn evaluatietaken **niet** weergegeven in de besturingsinterface.

### Kan ik een Samenstelling van het Publiek in een andere samenstelling gebruiken?

Nee, publiek gemaakt met Audience Composition **kan** worden gebruikt als input in een andere publiekssamenstelling.

### Hoe werkt splitsen in Audience Composition?

Door het publiek te splitsen kunt u het publiek verder onderbrengen in kleinere groepen.

Bij splitsing naar kenmerk is er sprake van wederzijdse exclusiviteit tussen de groepen. Dit betekent dat als een record voldoet aan de criteria van meerdere gesplitste paden, de record de opdracht **first** pad van links en **niet** toegewezen aan een van de andere paden.

Bij splitsen op percentage zijn splitsingen **willekeurig** gereed. Dit betekent dat de profielen willekeurig worden toegewezen aan elk pad. De splitsing is **niet** blijvend, zodat zou het profiel in een verschillende sub-publiek op elke evaluatie kunnen zijn.

Lees voor meer informatie over het blok Splitsen de [Handleiding voor compositie van publiek](./ui/audience-composition.md#split).

### Kan ik alle segmentatietypen in het werkschema van de Samenstelling van het Publiek gebruiken?

Ja, alle segmentatietypen ([batchsegmentatie, streamingsegmentatie en randsegmentatie](./home.md#evaluate-segments)) worden ondersteund in de workflow Audience Composition. Aangezien composities momenteel echter maar één keer per dag worden uitgevoerd, zelfs als streaming- of Edge-publiek wordt opgenomen, wordt het resultaat gebaseerd op het lidmaatschap van het publiek op het moment dat de compositie werd uitgevoerd.

## Hoe kan ik het lidmaatschap van een profiel in een publiek bevestigen?

Ga naar de pagina met profieldetails van het profiel dat u wilt bevestigen om het publiekslidmaatschap van een profiel te bevestigen. Selecteren **[!UICONTROL Attributes]**, gevolgd door **[!UICONTROL View JSON]** en u kunt bevestigen dat de `segmentMembership` bevat de id van het publiek.
