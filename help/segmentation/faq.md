---
title: Publiek Veelgestelde vragen
description: Ontdek antwoorden op veelgestelde vragen over publiek en andere op segmentatie betrekking hebbende concepten.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: a55272e3124c3fceedcadc33883445132bfec6bd
workflow-type: tm+mt
source-wordcount: '4853'
ht-degree: 0%

---

# Veelgestelde vragen

Adobe Experience Platform [!DNL Segmentation Service] biedt een gebruikersinterface en de RESTful-API waarmee u een publiek kunt maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze soorten publiek zijn centraal geconfigureerd en onderhouden op Experience Platform en zijn gemakkelijk toegankelijk voor alle Adobe-oplossingen. Hieronder volgt een lijst met veelgestelde vragen over publiek en segmentatie.

## Poort publiek

De volgende sectie maakt een lijst van vragen met betrekking tot de Portaal van de Publiek.

### Heb ik toegang tot het Portaal van het Publiek en de Samenstelling van het Publiek?

Poort van publiek en Audience Composition zijn beschikbaar voor alle Real-Time CDP Prime- en Ultimate-klanten (B2C, B2B en B2P Editions) en Journey Optimizer Select-, Prime-, Ultimate Starter- en Ultimate-klanten.

Op dit moment worden alleen op profielen gebaseerde soorten publiek ondersteund. Ondersteuning voor publiek op basis van account wordt in een latere release toegevoegd.

### Worden extern geproduceerd vooraf gebouwd publiek gesteund met het Portaal van het Publiek?

Ja, extern gegenereerde, vooraf gebouwde doelgroepen worden ondersteund met Poorten publiek. Op dit moment kunt u een extern gegenereerd publiek importeren via een CSV-bestand. In de toekomst kunt u een publiek toevoegen via batch- of streaminggebaseerde bronconnectors.

### Welke toestemmingen moet ik hebben om extern geproduceerd publiek te uploaden?

Als u extern gegenereerde soorten publiek wilt uploaden, hebt u de machtigingen Weergavesegmenten, Segmenten beheren en Soorten publiek importeren nodig. Er zijn geen specifieke op rol-gebaseerde controles vereist om extern geproduceerd publiek te uploaden.

### Wat gebeurt er als ik een extern gegenereerd publiek upload?

Wanneer u een extern geproduceerd publiek uploadt, zal een dataset worden gecreeerd en binnen de datasetinventaris zichtbaar zijn. De naam van de dataset zal **het zelfde** zijn zoals de naam van het extern geproduceerde publiek u uploadde.

### Wat is een extern gegenereerd publiek dat bestaat en wat gebeurt er met deze gegevens als het naar Experience Platform wordt geïmporteerd?

Tijdens de invoer externe publiekswerkschema, moet u specificeren welke kolom in het Csv- dossier met de **Primaire Identiteit** beantwoordt. Een voorbeeld van een primaire identiteit is e-mailadres, ECID of een naamruimte die specifiek is voor de organisatie.

De gegevens verbonden aan deze primaire identiteitskolom zijn **slechts** gegevens die aan het profiel in bijlage zijn. Als er geen bestaande profielen zijn die overeenkomen met de gegevens in de primaire identiteitskolom, wordt een nieuw profiel gemaakt. Nochtans, is dit profiel hoofdzakelijk een weeshuis profiel aangezien **geen** attributen of ervaringsgebeurtenissen met dit profiel worden geassocieerd.

Alle andere gegevens binnen het extern geproduceerde publiek worden beschouwd als **ladingsattributen**. Deze attributen kunnen **slechts** voor verpersoonlijking en verrijking tijdens activering worden gebruikt, en zijn **** niet verbonden aan een profiel. Deze kenmerken worden echter opgeslagen in het datumpigment.

Terwijl het extern geproduceerde publiek kan worden van verwijzingen voorzien wanneer het creëren van publiek gebruikend de Bouwer van het Segment, kunnen de individuele profielattributen **niet** worden gebruikt.

### Kan ik extern gegenereerde publieksgegevens combineren met een bestaand profiel in Experience Platform?

Ja, het extern gegenereerde publiek wordt samengevoegd met het bestaande profiel in Experience Platform als de primaire id&#39;s overeenkomen. Het kan 24 uur duren voordat de gegevens met elkaar in overeenstemming zijn. Als profielgegevens nog niet bestaan, wordt een nieuw profiel gemaakt wanneer de gegevens worden ingevoerd.

### Hoe worden de voorkeur van de klantentoestemming voor extern geproduceerd publiek geëerd dat in het Portaal van het Publiek wordt ingevoerd?{#consent}

Aangezien de klantengegevens van veelvoudige kanalen worden gevangen, staat het identiteit stitching en verenigingsbeleid deze gegevens toe om in één enkel Real-Time Profiel van de Klant te worden geconsolideerd. Informatie over de voorkeuren voor toestemming van klanten wordt opgeslagen en geëvalueerd op profielniveau.

De stroomafwaartse bestemmingen controleren elk profiel toestemmingsinformatie voorafgaand aan activering. De toestemmingsinformatie van elk profiel wordt vergeleken met de toestemmingsvereisten voor een bepaalde bestemming. Als het profiel niet aan de vereisten voldoet, wordt dat profiel niet verzonden naar een bestemming.

Wanneer een extern publiek in het Portaal van de Publiek wordt opgenomen, worden zij aangesloten bij bestaande profielen gebruikend primaire identiteitskaart zoals e-mail of ECID. Als gevolg daarvan zal het bestaande beleid inzake instemming gedurende de hele activering van kracht blijven.

Gelieve te merken op u **** toestemmingsinformatie met een extern geproduceerd publiek niet zou moeten omvatten, aangezien de ladingsvariabelen **niet** in de opslag van het Profiel maar in het gegevensmeer worden opgeslagen. In plaats daarvan, moet u **** een innamekanalen van Adobe Experience Platform gebruiken waar de profielgegevens worden ingevoerd.

### Kan ik een extern gegenereerd publiek gebruiken om andere soorten publiek op te bouwen?

Ja, zal om het even welk extern geproduceerd publiek binnen de publieksinventaris verschijnen en kan worden gebruikt wanneer het bouwen van publiek binnen de [ Bouwer van het Segment ](./ui/segment-builder.md).

### Hoe vaak worden extern gegenereerde doelgroepen geëvalueerd?

Extern geproduceerd publiek wordt **slechts** geëvalueerd tijdens de tijd van de invoer. Aangezien de bijbehorende attributen aan deze de invoersoorten publiek niet-duurzaam zijn en **** geen deel van de opslag van het Profiel zijn, zal de enige tijd een extern geproduceerd publiek worden bijgewerkt zijn als het bestaande publiek manueel wordt bijgewerkt.

### Kan ik extern geüploade kenmerken gebruiken als onderdeel van segmentatie?

Nee, dat kan niet. Profielkenmerken moeten langetermijnkenmerken zijn, terwijl extern gegenereerde publieksgegevens die worden geüpload alleen contextuele gegevens bevatten die aan dat extern gegenereerde publiek zijn gekoppeld.

De extern geproduceerde contextafhankelijke gegevens van het publiek, of verrijkingsattributen, zijn **niet** duurzaam, aangezien hun levenscyclus aan het geuploade publiek wordt gebonden. Dientengevolge, wegens zijn voorbijgaande aard, zijn deze verrijkingsattributen **niet** beschikbaar voor gebruik in segmentatie.

Wanneer u uw publiek echter toewijst aan batchbestemmingen of op bestanden gebaseerde bestemmingen, kunt u deze extern gegenereerde verrijkingskenmerken gebruiken om uw publiek en verdere downstreamactiveringen te verhogen.

Om meer over dit vermogen te leren, te lezen gelieve de gids op [ activerende publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Bestaat er een specifiek fusiebeleid voor extern gegenereerde doelgroepen?

Het organisatiespecifieke standaard samenvoegingsbeleid wordt automatisch toegepast wanneer het uploaden van extern geproduceerd publiek. U kunt echter wel het samenvoegbeleid wijzigen dat wordt toegepast op het extern gegenereerde publiek tijdens de workflow voor het importpubliek.

### Waar kan ik extern gegenereerde publiek activeren?

Een extern gegenereerd publiek kan aan elke bestemming worden toegewezen en kan worden gebruikt in Adobe Journey Optimizer-campagnes en -reizen.

### Kan ik een extern gegenereerd publiek verwijderen?

Ja! Extern gegenereerde doelgroepen kunnen worden verwijderd uit Audience Portal.

### Wat moet ik doen als ik per ongeluk een extern gegenereerd publiek heb geüpload?

Als u per ongeluk een extern gegenereerd publiek hebt geüpload en u de gegevens wilt verwijderen, kunt u de aan het publiek gekoppelde profielen wissen door een CSV-bestand met één rij en geen gegevens te uploaden.

### Hoe lang duurt het extern gegenereerde publiek?

De huidige gegevensvervaldatum voor extern geproduceerd publiek is **30 dagen**. Deze gegevensvervaldatum is gekozen om de hoeveelheid overtollige gegevens te verminderen die binnen uw organisatie worden opgeslagen.

Na de periode van de gegevensvervalsing gaat over, zal de bijbehorende dataset nog binnen de datasetinventaris zichtbaar zijn, maar u **** zal niet het publiek kunnen activeren en de profieltelling zal als nul tonen.

### Is er een maximum aantal extern gegenereerde soorten publiek dat ik kan importeren?

Er is geen limiet voor het aantal extern gegenereerde soorten publiek dat u kunt importeren. Nochtans, gelieve nota te nemen dat het ingevoerde publiek **** tegen de algemene publieksgrens doet tellen.

### Hoe zal het Portaal van het Publiek en de Samenstelling van het Publiek met de versie van de Gegevens van de Partner van Real-Time CDP in wisselwerking staan?

Het Portaal van het publiek en de Samenstelling van het Publiek zullen met de Gegevens van de Partner op twee manieren in wisselwerking staan:

1. Als u een partner-verstrekte perspectieflijst gebruikend de klasse en het werkschema van het Profiel van het Vooruitzicht opneemt, zullen de vooruitzichten **** gescheiden van fusieklantenprofielen in de Dienst van het Profiel worden gehouden. Dientengevolge, betekent dit dat de perspectieflijsten **** niet in of het Portaal van het Publiek of de Samenstelling van het Publiek voor gebruik zullen verschijnen.
2. Als u partner-verstrekte attributen leveraging om **bestaande** eerste-partijprofielen te verrijken, zullen die partner-gegeven-verrijkt publiek **** in zowel het Portaal van het Publiek als de Samenstelling van het Publiek voor gebruik verschijnen.

### Hoe kan ik extra attributen met mijn publiek gebruiken?

Met publiek, zijn er **twee** verschillende soorten extra attributen u kunt toevoegen - (contextafhankelijke) attributen en verrijkingsattributen van de lading.

Payload-kenmerken zijn kenmerken die worden opgenomen als onderdeel van de CSV-upload van een extern gegenereerd publiek. Deze attributen worden **niet** opgenomen in het Real-Time Profiel van de Klant, maar kunnen als deel van een stroomafwaartse bestemming worden gebruikt.

De attributen van de verrijking zijn attributen die uit een dataset komen en met een publiek in de Samenstelling van het Publiek worden verbonden. Deze kenmerken kunnen momenteel alleen worden gebruikt in Adobe Journey Optimizer-campagnes. De steun voor Adobe Journey Optimizer-reizen komt binnenkort, met steun voor downstreambestemmingen in afwachting van de toekomstige vrijlating.

| Activeringskanaal | Soorten publiek van aangepaste CSV-upload | Soorten publiek uit publiekscompositie |
| --- | --- | --- |
| Real-Time CDP-doelen | U kunt zowel de payload-kenmerken als het publiek activeren. | Alleen het publiek kan worden geactiveerd. De attributen van de verrijking **kunnen** niet worden geactiveerd. |
| Adobe Journey Optimizer Campaigns | U kunt het publiek en de payload-kenmerken niet activeren. | U kunt zowel het publiek als de verrijkingskenmerken activeren. |

## Levenscyclusstatussen {#lifecycle-states}

In de volgende sectie worden vragen over de levenscyclusstatus en het beheer van de levenscyclusstatus in de portal Publiek weergegeven.

### Wat vertegenwoordigen de verschillende levenscyclusstaten?

In het volgende diagram worden de verschillende levenscyclusstatussen beschreven, wat ze vertegenwoordigen, waar publiek met die status kan worden gebruikt, en het effect op segmentatiegeleidingen.

| Staat | Definitie | Zichtbaar in Audience Portal? | Zichtbaar in Doelen? | Heeft invloed op segmentatielimieten? | Gevolgen voor het publiek | Gevolgen voor de publieksevaluatie | Kan worden gebruikt bij andere doelgroepen? | Bewerkbaar |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Concept | Een publiek in de **staat van het Ontwerp** is een publiek dat nog in ontwikkeling is en nog niet klaar om in andere diensten te worden gebruikt. | Ja, maar kan verborgen zijn. | Nee | Ja | Kan tijdens het verfproces worden geïmporteerd of bijgewerkt. | Evalueerd voor een nauwkeurige telling van het aantal uitgeverijen. | Ja, maar het wordt niet aanbevolen dit te gebruiken. | Ja |
| Gepubliceerd | Een publiek in de **Gepubliceerde** staat is een publiek dat voor gebruik over alle stroomafwaartse diensten klaar is. | Ja | Ja | Ja | Kan worden geïmporteerd of bijgewerkt. | Evalueerd met batch-, streaming- of randsegmentatie. | Ja | Ja |
| Inactief | Een publiek in de **Inactieve** staat is een publiek dat momenteel niet in gebruik is. Het bestaat nog binnen Experience Platform, maar het zal **niet** bruikbaar zijn tot het als ontwerp of gepubliceerd duidelijk is. | Nee, maar kan wel worden weergegeven. | Nee | Nee | Niet meer bijgewerkt. | Niet meer geëvalueerd of bijgewerkt door Experience Platform. | Nee | Ja |
| Verwijderd | Een publiek in de **Geschrapte** staat is een publiek dat is geschrapt. Het kan enkele minuten duren voordat de gegevens daadwerkelijk zijn verwijderd. | Nee | Nee | Nee | Onderliggende gegevens worden verwijderd. | Er vindt geen gegevensevaluatie of -uitvoering plaats nadat de verwijdering is voltooid. | Nee | Nee |

### In welke staten kan ik mijn publiek bewerken?

Soorten publiek kan in de volgende levenscyclusstaten worden bewerkt:

- **Ontwerp**: Als een publiek in de ontwerpstaat wordt uitgegeven, zal het in de ontwerpstaat blijven tenzij het uitdrukkelijk wordt gepubliceerd.
- **Gepubliceerd**: Als een publiek in de gepubliceerde staat wordt uitgegeven, zal het gepubliceerd blijven, en het publiek zal automatisch worden bijgewerkt.
- **Inactief**: Als een publiek in de inactieve staat wordt uitgegeven, zal het inactief blijven. Dit betekent dat het niet zal worden geëvalueerd of bijgewerkt. Als u het publiek moet bijwerken, moet u het publiek publiceren.

Zodra een publiek wordt geschrapt, kan het **niet** worden uitgegeven.

### Naar welke levenscyclusstaten kan ik een publiek verplaatsen?

De mogelijke levenscyclus bepaalt dat een publiek kan worden verplaatst, afhankelijk van de huidige status van het publiek.

![ A diagram dat de mogelijke overgangen van de levenscyclusstaat schetst die voor publiek beschikbaar zijn.](./images/faq/lifecycle-state-transition.png)

Als de doelgroep zich in de conceptstatus bevindt, kunt u de doelgroep publiceren of verwijderen als de doelgroep geen afhankelijke personen heeft.

Als het publiek zich in de gepubliceerde status bevindt, kunt u het item deactiveren of verwijderen als het publiek geen afhankelijke personen heeft.

Als uw publiek zich in de inactieve staat bevindt, kunt u het opnieuw publiceren of schrappen als het publiek geen gebiedsdelen heeft.

### Zijn er voorbehouden voor het publiek in bepaalde levenscyclusstaten?

Het publiek in de gepubliceerde staat kan slechts naar een andere staat worden verplaatst als het publiek **** geen gebiedsdelen heeft. Dit betekent dat als uw publiek in een stroomafwaartse dienst wordt gebruikt, het niet kan worden gedeactiveerd of worden geschrapt.

Als een publiek dat gebruikend partijsegmentatie wordt geëvalueerd wordt opnieuw gepubliceerd, dat is wanneer een publiek van inactief aan gepubliceerd gaat, zal het publiek **na** de dagelijkse partijbaan verfrissen. Wanneer het eerst opnieuw gepubliceerd wordt, zullen de profielen en de gegevens **het zelfde** zijn zoals toen het publiek inactief werd gemaakt.

### Hoe zet ik een publiek in de ontwerpstaat?

De methode om een publiek in de ontwerpstaat te zetten hangt van de oorsprong van het publiek af.

Voor publiek dat gebruikend de Bouwer van het Segment wordt gecreeerd, kunt u het publiek aan de ontwerpstaat plaatsen door &quot;[!UICONTROL Save as draft]&quot;in de Bouwer van het Segment te selecteren.

Voor publiek dat in de Samenstelling van het Publiek wordt gecreeerd, worden het publiek automatisch opgeslagen als ontwerp tot gepubliceerd.

Voor publiek dat extern wordt gemaakt, wordt het publiek automatisch gepubliceerd.

Zodra een publiek in de gepubliceerde staat is, kunt u **niet** het originele publiek terug in de ontwerpstaat veranderen. Als u echter het publiek kopieert, bevindt het nieuwe publiek zich in de conceptstatus.

### Hoe zet ik een publiek in de gepubliceerde staat?

Voor publiek dat gebruikend de Bouwer van de Segment of Samenstelling van het Publiek wordt gecreeerd, kunt u het publiek aan de gepubliceerde staat plaatsen door &quot;[!UICONTROL Publish]&quot;in hun respectieve UIs te selecteren.

De soorten publiek die extern worden gecreeerd worden automatisch geplaatst aan gepubliceerd.

### Hoe zet ik een publiek in de inactieve staat?

U kunt een gepubliceerd publiek in de inactieve staat zetten door het snelle actiemenu in het Portaal van de Publiek te openen en &quot;[!UICONTROL Deactivate]&quot;te selecteren.

### Hoe kan ik een publiek opnieuw publiceren?

>[!NOTE]
>
>De staat &quot;opnieuw gepubliceerd&quot;is het zelfde als de gepubliceerde staat voor publieksgedrag.

U kunt een publiek opnieuw publiceren door een publiek te selecteren dat in de inactieve staat is, het snelle actiemenu op de Portaal van de Publiek te openen en [!UICONTROL Publish] te selecteren.

### Hoe zet ik een publiek in de verwijderde staat?

>[!IMPORTANT]
>
>U kunt publiek slechts schrappen dat **niet** wordt gebruikt in om het even welke stroomafwaartse activiteiten. Bovendien, kunt u geen publiek schrappen dat in een ander publiek van verwijzingen wordt voorzien. Als u uw publiek niet kunt schrappen, gelieve te verzekeren u **niet** het in om het even welke stroomafwaartse diensten of als bouwsteen van een ander publiek gebruikt.

U kunt een publiek in de schrappingsstaat zetten door het snelle actiemenu in de Portaal van de Publiek te openen en [!UICONTROL Delete] te selecteren.

### Zijn er voorbehouden voor de overgangen van de levenscyclusstatus?

Ja, er zijn sommige bedenkingen om zich van bewust te zijn wanneer u publiek in de stroomafwaartse diensten zoals Adobe Journey Optimizer of niet-klant-gebaseerd publiek zoals op rekening-gebaseerd publiek gebruikt.

Op dit ogenblik, moet u **** manueel controleren als het publiek in Adobe Journey Optimizer stroomafwaarts wordt gebruikt, aangezien deze status momenteel niet automatisch gecontroleerd is.

Bovendien, moet u **** manueel controleren als het publiek als component van een op rekening-gebaseerd publiek wordt gebruikt, aangezien deze status ook niet momenteel automatisch wordt gecontroleerd.

### Wat gebeurt er als ik een publiek kopieer? {#copy}

Wanneer u een publiek kopieert, bevindt het nieuwe publiek zich in de conceptstatus en behoudt het dezelfde mappen, tags en labels die op het oorspronkelijke publiek zijn toegepast.

### Heeft het gebruik van een publiek als een onderliggend publiek invloed op overgangen in de levenscyclusstatus?

>[!NOTE]
>
>Een ouderpubliek is een publiek dat **** een ander publiek als gebiedsdeel voor het publiek gebruikt.
>
>Een kindpubliek is een publiek dat **als** een gebiedsdeel voor het publiek wordt gebruikt.

Ja, het gebruik van een publiek als een onderliggend publiek beïnvloedt wel welke levenscyclusstaten het kind en het bovenliggende publiek kunnen doorvoeren.

Opdat een kindpubliek aan de gepubliceerde staat moet worden verplaatst, moet elk van zijn ouderpubliek **** in de gepubliceerde staat zijn. Het bovenliggende publiek kan worden gepubliceerd voordat het onderliggende publiek wordt gepubliceerd of, als de gebruiker dit bevestigt, automatisch worden gepubliceerd wanneer het onderliggende publiek wordt gepubliceerd.

Opdat het ouderpubliek aan de inactieve of geschrapte staat moet worden verplaatst, moet elk van zijn kindpubliek **** worden gedeactiveerd of worden geschrapt.

### Kan ik verwijzen naar een publiek dat zich in een andere levenscyclusstaat bevindt?

Ja! Als uw publiek zich momenteel in de ontwerpstaat bevindt, kunt u naar publiek in of het ontwerp of de gepubliceerde staat verwijzen. Nochtans, om dit publiek te publiceren, moet u **** het andere ouderpubliek publiceren.

## Overzicht van het publiek

De volgende sectie geeft een overzicht van vragen die betrekking hebben op de publieksinventarisatie in het Poort publiek.

### Heb ik extra toestemmingen nodig om de eigenschappen van de publieksinventaris te gebruiken?

Nee, dat doe je niet. Als u over bewerkingsmachtigingen voor het publiek beschikt, kunt u uw mappen en tags maken, bijwerken en beheren in het Poortpubliek van het publiek. Voor meer informatie over het beheren van toestemmingen, te lezen gelieve [ toestemmingengids ](../access-control/ui/permissions.md) beheren.

### Is er een limiet voor het aantal mappen dat ik kan maken?

Nee, er is geen limiet voor het aantal mappen dat u kunt maken. Voor meer informatie over omslagen, te lezen gelieve de [ sectie van de publieksinventaris ](./ui/audience-portal.md#folders) van het overzicht UI van de Dienst van de Segmentatie.

### Is er een limiet voor het aantal tags dat aan een publiek kan worden toegevoegd?

Nee, er is geen limiet voor het aantal tags dat aan een publiek kan worden toegevoegd. Voor meer informatie over markeringen, te lezen gelieve de [ sectie van de publieksinventaris ](./ui/audience-portal.md#tags) van het overzicht UI van de Dienst van de Segmentatie.

### Is er een limiet aan het aantal tags dat ik kan maken?

Nee, er is geen limiet aan het aantal tags dat u kunt maken. Nochtans, kunt u tot een maximum van **100** categorieën leiden om voor de markeringen van toepassing te zijn. Voor meer informatie over markeringsbeheer, te lezen gelieve de [ Leidende gids van Markeringen ](../administrative-tags/ui/managing-tags.md).

### Wanneer ik naar een publiek door naam of markering in een ouderomslag zoek, kan ik door de verwante kindomslagen ook zoeken?

Nee, dit gedrag wordt niet ondersteund. Nochtans, kunt u de mening van de publieksinventaris veranderen om **Alle Soorten publiek** te bekijken, dan onderzoek over alle omslagen. Voor meer informatie bij het gebruiken van onderzoek in publieksinventaris, te lezen gelieve de [ onderzoekssectie ](./ui/audience-portal.md#search) van het overzicht van de Dienst UI van de Segmentatie.

### Kan ik een publiek automatisch toewijzen aan een map op het moment van het maken?

Op dit moment, nee. Deze mogelijkheid kan echter in de toekomst beschikbaar zijn.

### Kan ik meerdere soorten publiek tegelijk naar een map verplaatsen?

Op dit moment, nee. Deze mogelijkheid kan echter in de toekomst beschikbaar zijn.

## Samenstelling publiek

In de volgende sectie worden vragen over Audience Composition weergegeven.

### Wanneer zou ik de Samenstelling van het Publiek in tegenstelling tot het gebruiken van de Bouwer van het Segment moeten gebruiken?

Zowel Audience Composition als Segment Builder hebben een belangrijke rol bij het creëren van publiek in Experience Platform.

De Bouwer van het Segment is geschikter voor publiek **verwezenlijking** (voor de bouw van een publiek van kras), terwijl de Samenstelling van het Publiek geschikter is voor publiek **curatie en verpersoonlijking** (voor het creëren van nieuw publiek dat op een bestaand publiek wordt gebaseerd).

De volgende tabel illustreert het verschil tussen de twee services:

| Segment Builder | Samenstelling publiek |
| --------------- | -------------------- |
| <ul><li>Eenmalige doelgroep</li><li>Creeert de basisblokken van publiek van profiel, tijdreeksen, en multi-entiteitsgegevens</li><li>Gebruikt om **één** publiek te creëren</li></ul> | <ul><li>Multi-stage publiek genereren, met gebruik van op set gebaseerde bewerkingen</li><li>Gebruikt het publiek dat door de Bouwer van de Segment wordt gecreeerd en past opties van de gegevensverrijking zoals het rangschikken van profielattributen en het verdelen in sub-publiek toe</li><li>Gebruikt om **veelvoud** publiek in één keer te creëren</li></ul> |

Om meer over de Bouwer van het Segment te leren, te lezen gelieve de [ gids van de Bouwer van het Segment ](./ui/segment-builder.md). Meer over de Samenstelling van het Publiek leren, gelieve de [ gids van de Samenstelling van het Publiek ](./ui/audience-composition.md) te lezen.

### Kan ik extern gegenereerd publiek gebruiken in Audience Composition?

Op dit moment, nee. Deze mogelijkheid moet echter in de nabije toekomst beschikbaar zijn.

### Kan ik publiek van de Samenstelling van het Publiek naar alle stroomafwaartse bestemmingen en kanalen verzenden?

Ja! U kunt publiek van de Samenstelling van het Publiek in de Campagnes van Adobe Journey Optimizer, de bestemmingen van Real-Time CDP, en de Reizen van Adobe Journey Optimizer gebruiken.

### Zijn er aanwijzingen voor het aantal composities?

>[!IMPORTANT]
>
>Deze guardrail is slechts op samenstellingen van toepassing die met de Samenstelling van het Publiek worden gecreeerd en **** is niet op samenstellingen van toepassing die met de Federatieve Samenstelling van het Publiek worden gecreeerd.

Op dit punt in tijd, kunt u **10** gepubliceerde samenstellingen per zandbak slechts hebben. Deze guardrail zal naar verwachting in een toekomstige release worden verhoogd.

### Wat zijn de werkstroominstructies voor Audience Composition?

De compositiecomponent die als volgt plaatst volgt een stijve structuur:

1. U **altijd** begint met het [!UICONTROL Audience] blok om uw beginnende activiteit te selecteren. U kunt een maximum van **één** [!UICONTROL Audience] blok hebben.
2. U kunt optioneel een blok [!UICONTROL Exclude] toevoegen dat volgt op het blok [!UICONTROL Audience] .
3. U kunt optioneel een blok [!UICONTROL Enrich] toevoegen dat volgt op het blok [!UICONTROL Exclude] . U kunt **slechts één** [!UICONTROL Enrich] blok per samenstelling gebruiken.
4. U kunt optioneel een blok [!UICONTROL Rank] of [!UICONTROL Split] toevoegen. U kunt **slechts** één van deze blokken per samenstelling hebben.
5. U **altijd** eind met a [!UICONTROL Save] blok om uw publiek te bewaren.

Bovendien gelden de volgende beperkingen bij het gebruik van deze blokken:

- Blok splitsen
   - Dit blok steunt slechts **gegevenstypes van 0} Koord {.** Het gesplitste blok steunt **** niet het datum of booleaanse gegevenstype.
   - Bovendien, steunt dit blok **** geen verrijkingsattributen.
- Blok uitsluiten
   - Dit blok steunt **** niet het datum of booleaanse gegevenstype.
- Rank blok
   - Dit blok steunt **** geen verrijkingsattributen.

Voor meer details over het gebruiken van de Samenstelling van het Publiek, gelieve de [ gids UI van de Samenstelling van het Publiek ](./ui/audience-composition.md) te lezen.

### Wanneer wordt het publiek gecreeerd gebruikend de Samenstelling van het Publiek bewaard en geëvalueerd?

Soorten publiek worden automatisch opgeslagen tijdens het maken ervan in Audience Composition. De aanmaaktijd van het publiek is de eerste keer dat deze automatische opslag plaatsvindt.

Nadat de publiekssamenstelling is gecreeerd, kan het tot 48 uren voor het worden geëvalueerd en geactiveerd voor gebruik in stroomafwaartse diensten zoals een bestemming van Real-Time CDP of een kanaal van Adobe Journey Optimizer.

### Wanneer kan ik het publiek gebruiken dat ik heb gemaakt?

Het publiek dat in de Samenstelling van het Publiek wordt gecreeerd zal **onmiddellijk** in het Portaal van het Publiek verschijnen. Als u het echter wilt gebruiken in downstreamdiensten zoals Adobe Journey Optimizer, moet u minstens 24 uur wachten na evaluatie.

### Zijn evaluatietaken zichtbaar in de sectie monitoring?

Op dit ogenblik, worden de evaluatietaken **niet** getoond binnen de controle UI.

### Kan ik een Samenstelling van het Publiek in een andere samenstelling gebruiken?

Nr, kan het publiek dat gebruikend de Samenstelling van het Publiek **wordt gecreeerd niet** als input in een andere publiekssamenstelling worden gebruikt.

### Hoe werkt splitsen in Audience Composition?

Door het publiek te splitsen kunt u het publiek verder onderbrengen in kleinere groepen.

Bij splitsing naar kenmerk is er sprake van wederzijdse exclusiviteit tussen de groepen. Dit betekent dat als een verslag aan de criteria van veelvoudige gespleten wegen voldoet, het **eerste** weg van de linkerzijde zal worden toegewezen en **niet** toegewezen aan om het even welke andere wegen.

Wanneer het splitsen door percentage, worden de spleten **willekeurig** gedaan. Dit betekent dat de profielen willekeurig worden toegewezen aan elk pad.

Voor meer informatie over het Gesplitste blok, te lezen gelieve de [ gids UI van de Samenstelling van het publiek ](./ui/audience-composition.md#split).

### Kan ik alle segmentatietypen in het werkschema van de Samenstelling van het Publiek gebruiken?

Ja, worden alle segmentatietypen ([ partijsegmentatie, het stromen segmentatie, en randsegmentatie ](./home.md#evaluate-segments)) gesteund in het werkschema van de Samenstelling van het Publiek. Aangezien composities momenteel echter maar één keer per dag worden uitgevoerd, zelfs als streaming- of Edge-publiek wordt opgenomen, wordt het resultaat gebaseerd op het lidmaatschap van het publiek op het moment dat de compositie werd uitgevoerd.

## Publiek lidmaatschap

In de volgende sectie worden vragen over het lidmaatschap voor het publiek weergegeven.

### Hoe kan ik het lidmaatschap van een profiel in een publiek bevestigen?

Ga naar de pagina met profieldetails van het profiel dat u wilt bevestigen om het publiekslidmaatschap van een profiel te bevestigen. Selecteer **[!UICONTROL Attributes]** , gevolgd door **[!UICONTROL View JSON]** , en u kunt bevestigen dat het `segmentMembership` -object de id van het publiek bevat.

### Kan het lidmaatschap van het publiek verschuiven tussen ideaal en daadwerkelijk lidmaatschap?

Ja, kan het publiekslidmaatschap tussen ideaal en werkelijk lidmaatschap afglijden als een publiek gebruikend het stromen segmentatie **wordt geëvalueerd en** dat het publiek uit een geëvalueerd publiek gebruikend partijsegmentatie gebaseerd is.

Bijvoorbeeld, als het Publiek A van Publiek B wordt gebaseerd, en Publiek B wordt geëvalueerd gebruikend partijsegmentatie, aangezien Publiek B slechts om de 24 uur bijwerkt, zal Publiek A zich verder van de daadwerkelijke gegevens bewegen tot het met de updates van het Publiek B re-synchroniseert.

## Batchsegmentatie {#batch-segmentation}

In de volgende sectie worden vragen over batchsegmentatie weergegeven.

### Hoe verhelpt batchsegmentatie profiellidmaatschap?

De soorten publiek die worden geëvalueerd met behulp van batchsegmentatie worden dagelijks opgelost, waarbij de resultaten van het doellidmaatschap worden opgenomen in het kenmerk `segmentMembership` van het profiel. De raadplegingen van het profiel produceren een verse versie van het profiel in de tijd van de raadpleging, maar het **** verfrist niet de resultaten van de partijsegmentatie.

Dientengevolge, wanneer de veranderingen in het profiel, zoals het samenvoegen van twee profielen samen worden aangebracht, zullen deze veranderingen **** in het profiel verschijnen wanneer opgezocht, maar **** niet `segmentMembership` worden weerspiegeld in het  attribuut tot de baan van de segmentevaluatie opnieuw is gelopen.

Bijvoorbeeld, zeggen u twee wederzijds exclusief publiek hebt gecreeerd: Publiek A is voor mensen die in Washington wonen en Publiek B is voor mensen die **niet** in Washington wonen. Er zijn twee profielen: profiel 1 voor een persoon die in Washington woont en profiel 2 voor een persoon die in Oregon woont.

Wanneer de looppas van de partijsegmenteringsevaluatie, zal profiel 1 naar Publiek A gaan, terwijl profiel 2 naar Publiek B. Later, maar alvorens de de looppas van de de partijsegmenteringsevaluatietaak van de volgende dag zal gaan, een gebeurtenis die de twee profielen aanpast Experience Platform ingaat. Hierdoor wordt één samengevoegd profiel gemaakt dat de profielen 1 en 2 bevat.

Tot de volgende baan van de de segmentbeoordeling van de partij in werking wordt gesteld, zal het nieuwe samengevoegde profiel publiekslidmaatschap in **zowel** profiel 1 als profiel 2 hebben. Dientengevolge, betekent dit het een lid van **zowel** Publiek A als Publiek B zal zijn, ondanks het feit dat deze publiek tegenstrijdige definities heeft. Voor de eindgebruiker, is dit de **nauwkeurige zelfde situatie** zoals alvorens de profielen werden verbonden, aangezien er altijd enkel betrokken één persoon was, en Experience Platform **** had enkel niet genoeg informatie om de twee profielen samen te verbinden.

Als u profielraadpleging gebruikt om het onlangs gecreëerde profiel terug te winnen en zijn publiekslidmaatschap te bekijken, zal het tonen dat het een lid van **zowel** Publiek A als Publiek B is, ondanks het feit dat beide van deze soorten publiek tegenstrijdige definities hebben. Zodra de dagelijkse de evaluatietaak van de partijsegmentatie loopt, zal het publiekslidmaatschap worden bijgewerkt om op deze bijgewerkte staat van profielgegevens te wijzen.

Gebruik streaming of randsegmentatie als u meer realtime publieksresolutie nodig hebt.

### Hoe lang duurt het voordat streaminggegevens beschikbaar zijn in workflows met batchsegmentatie?

Het kan maximaal drie uur duren voordat streaminggegevens beschikbaar zijn in workflows met batchsegmentatie.

Bijvoorbeeld, als een baan van de partijsegmentatie bij 9PM loopt, wordt het gegarandeerd om het stromen ingebedde gegevens **tot** 6PM te bevatten. Het stromen ingebedde gegevens die na 6PM maar vóór 9PM **werden opgenomen kunnen** worden omvat.

## Edge-segmentatie {#edge-segmentation}

In de volgende sectie worden vragen over randsegmentatie weergegeven.

### Hoe lang duurt het voordat een segmentdefinitie beschikbaar is op de Edge Network?

Het duurt maximaal een uur voordat een segmentdefinitie beschikbaar is op de Edge Network.

## Streaming segmentering {#streaming-segmentation}

In de volgende sectie worden vragen over streamingsegmentatie weergegeven.

### Vindt streaming segmentatie ook &#39;onkwalificatie&#39; plaats in real-time?

De segmentatie van het stromen komt voor afhankelijk van de samenstelling van het publiek. Voor op gebeurtenis-gebaseerd publiek, komt de ontzetting in real time voor aangezien het raadplegingsvenster verloopt. Voor op profiel gebaseerde soorten publiek of publiek dat profielkenmerken gebruikt, vindt diskwalificatie plaats wanneer de waarden van de profielkenmerken via een streamingbron of tijdens de dagelijkse batchevaluatietaak worden gewijzigd.

### Aan welke gegevens werkt streaming segmentatie?

Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Gegevens die worden ingevoerd met behulp van een op batch gebaseerde bron worden elke avond geëvalueerd, zelfs als deze in aanmerking komen voor streamingsegmentatie. Gebeurtenissen die naar het systeem worden gestreamd met een tijdstempel die ouder is dan 24 uur, worden verwerkt in de volgende batchtaak.

### Hoe worden segmenten gedefinieerd als batch- of streaming-segmentatie?

Een segmentdefinitie wordt gedefinieerd als batch, streaming of randsegmentatie op basis van een combinatie van het type query en de duur van de gebeurtenisgeschiedenis. Een lijst waarvan de segmenten als het stromen segmentdefinitie zullen worden geëvalueerd kan in de [ het stromen sectie van de segmenteringsvraagtypes ](#query-types) worden gevonden.

Gelieve te merken op dat als een segmentdefinitie **zowel** een `inSegment` uitdrukking als een directe enige-gebeurtenisketting bevat, het niet voor het stromen segmentatie kan kwalificeren. Als u deze segmentdefinitie voor het stromen segmentatie wilt kwalificeren, zou u de directe enige-gebeurtenisketen zijn eigen segment moeten maken.

### Waarom blijft het aantal &quot;totaal gekwalificeerde&quot;segmenten stijgen terwijl het aantal onder &quot;Laatste X dagen&quot;nul binnen de sectie van de segmentdefinitiedetails blijft?

Het aantal in totaal gekwalificeerde segmenten wordt ontleend aan de dagelijkse segmentatietaak, die publiek omvat dat voor zowel partij als het stromen segmenten kwalificeert. Deze waarde wordt weergegeven voor zowel batch- als streaming segmenten.

Het aantal onder de &quot;Laatste dagen van X&quot;**slechts** omvat publiek dat in het stromen segmentatie wordt gekwalificeerd, en **slechts** verhogingen als u gegevens in het systeem hebt gestroomd en het telt naar die het stromen definitie. Deze waarde is **slechts** getoond voor het stromen segmenten. Dientengevolge, kan deze waarde **** als 0 voor partijsegmenten tonen.

Dientengevolge, als u ziet dat het aantal onder &quot;Laatste dagen van X&quot;nul is, en de lijngrafiek ook nul meldt, hebt u **** gestroomd geen profielen in het systeem dat voor dat segment zou kwalificeren.

### Hoe lang duurt het voordat een segmentdefinitie beschikbaar is?

Het duurt tot één uur voordat een segmentdefinitie beschikbaar is.

### Zijn er beperkingen aan de gegevens waarin wordt gestreamd?

Wanneer u segmentatie tussen randen of streams gebruikt, moet u ervoor zorgen dat gebeurtenissen voor elk profiel uit elkaar zijn geplaatst. Als er te veel gebeurtenissen binnen dezelfde seconde worden gestreamd, behandelt Experience Platform deze gebeurtenissen als door beide gegenereerde gegevens en worden ze genegeerd. Als beste praktijken, zou u **minstens** vijf seconden tussen gebeurtenisgegevens moeten hebben om ervoor te zorgen dat het gegeven behoorlijk wordt gebruikt.
