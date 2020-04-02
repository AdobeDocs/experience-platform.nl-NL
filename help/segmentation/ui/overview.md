---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor de gebruikersinterface van Segment Builder
topic: ui guide
translation-type: tm+mt
source-git-commit: 91792f81a50d5752e46236d61b6ad645e3fda86c

---


# Gebruikershandleiding voor Segment Builder

De Adobe Experience Platform Segmentation Service biedt een RESTful API en gebruikersinterface voor het maken van segmentdefinities van gegevens van het Klantprofiel in real time.

## Aan de slag

Het werken met segmentdefinities vereist een begrip van de diverse diensten van het Platform van de Ervaring betrokken bij segmentatie. Lees vóór het lezen van deze gebruikershandleiding de documentatie voor de volgende services:

- [Segmenteringsservice](../home.md): De Dienst van de segmentatie staat u gegevens toe die in het Platform van de Ervaring worden opgeslagen dat op individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) betrekking heeft in kleinere groepen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.
- [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Identiteitsservice](../../identity-service/home.md): Laat het Profiel van de Klant in real time toe door identiteiten van ongelijke gegevensbronnen te overbruggen die in Platform worden opgenomen.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.

Het is ook belangrijk om twee belangrijke termen te kennen die in dit document worden gebruikt en het verschil tussen hen te begrijpen:
- **Segmentdefinitie**: De regelreeks die wordt gebruikt om zeer belangrijke eigenschappen of gedrag van een doelpubliek te beschrijven.
- **Publiek**: De resulterende set profielen die voldoen aan de criteria van een segmentdefinitie.

## Toegang tot segmentdefinities

Als u wilt gaan werken met segmentdefinities in het Adobe Experience Platform, klikt u op **Segmenten** in de linkernavigatie. Om alle segmentdefinities voor uw organisatie te zien, klik op het *Browse* lusje. Deze mening maakt een lijst van informatie over de segmentdefinitie met inbegrip van de evaluatiemethode, gecreeerd datum, en laatst gewijzigde datum.

De evaluatiemethode kan streaming of batch zijn. Streaming segmenten worden voortdurend geëvalueerd terwijl gegevens in het systeem worden ingevoerd. De segmenten van de partij worden geëvalueerd volgens een vastgesteld programma.

De segmenten van de partij hebben extra informatie getoond, die zowel de laatste evaluatiedatum als de volgende evaluatiedatum voor de partij tonen.

Als u in de rechterbovenhoek op Segment maken klikt, wordt de werkruimte Segment Builder geopend. Hier kunt u een segmentdefinitie maken. ****

![](../images/segment-builder/segment-browse.png)

## De werkruimte van Segment Builder

De Bouwer van het segment verstrekt een rijke werkruimte die u toestaat om met de gegevenselementen van het Profiel in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.

![](../images/segment-builder/segment-builder.png)

## Bouwstenen voor segmentdefinitie

De basisbouwstenen van segmentdefinities zijn **Attributen** en **Gebeurtenissen**. Daarnaast kunnen de kenmerken en gebeurtenissen in het bestaande **publiek** ook worden gebruikt als componenten voor nieuwe definities.

U kunt deze bouwstenen in de sectie van *Gebieden* op de linkerkant van de werkruimte van de Bouwer van het Segment zien. *De gebieden* bevatten een lusje voor elk van de belangrijkste bouwstenen: **Kenmerken**, **Gebeurtenissen** en **Soorten publiek**.

![](../images/segment-builder/segment-fields.png)

### Attributen

Op het tabblad **Kenmerken** kunt u door de profielkenmerken bladeren die horen bij de XDM-klasse Individueel profiel. Elke map kan worden uitgevouwen om extra kenmerken weer te geven. Elk kenmerk is een tegel die naar het canvas voor regelbuilders in het midden van de werkruimte kan worden gesleept. Het canvas van de [regelbouwer](#rule-builder-canvas) wordt meer in detail besproken later in deze gids.

![](../images/segment-builder/attributes.png)

### Gebeurtenissen

Op het tabblad **Gebeurtenissen** kunt u een publiek maken op basis van gebeurtenissen of acties die hebben plaatsgevonden met XDM ExperienceEvent-gegevenselementen. U kunt gebeurtenistypen ook vinden op het tabblad **Gebeurtenissen** . Dit is een verzameling veelgebruikte gebeurtenissen waarmee u uw segmenten sneller kunt maken.

U kunt niet alleen bladeren naar ExperienceEvent-elementen, maar u kunt ook zoeken naar gebeurtenistypen. Gebeurtenistypen gebruiken dezelfde coderingslogica als ExperienceEvents, zonder dat u door de XDM ExperienceEvent-klasse hoeft te zoeken op zoek naar de juiste gebeurtenis. Als u bijvoorbeeld met de zoekbalk zoekt naar &quot;winkelwagentje&quot;, worden de gebeurtenistypen &quot;AddCart&quot; en &quot;RemoveCart&quot; geretourneerd. Dit zijn twee veelgebruikte tekenacties bij het samenstellen van segmentdefinities.

Elk type component kan worden gezocht door zijn naam in de onderzoeksbar te typen, die de onderzoekssyntaxis [van](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene gebruikt. De zoekresultaten beginnen te vullen wanneer hele woorden worden ingevoerd. Als u bijvoorbeeld een regel wilt maken die is gebaseerd op het XDM-veld, `ExperienceEvent.commerce.productViews`typt u &quot;productweergaven&quot; in het zoekveld. Nadat u het woord &quot;product&quot; hebt getypt, worden de zoekresultaten weergegeven. Elk resultaat bevat de objecthiërarchie waartoe het behoort.

>[!NOTE] De het schemagebieden van de douane die door uw organisatie worden bepaald kunnen tot 24 uren aan verschijnen en beschikbaar voor gebruik in het bouwen van regels vergen.

U kunt ExperienceEvents en de Types van Gebeurtenis dan gemakkelijk slepen en in uw segmentdefinitie laten vallen.

![](../images/segment-builder/events-eventTypes.png)

Standaard worden alleen gevulde schemavelden uit de gegevensopslag weergegeven. Dit geldt ook voor gebeurtenistypen. Als de lijst Gebeurtenistypen niet zichtbaar is, of u alleen &quot;Enige&quot;als Type Gebeurtenis kunt selecteren, klik het tandwielpictogram naast *Gebieden*, dan uitgezocht **toon volledig XDM schema** onder *Beschikbare Gebieden*. Klik nogmaals op het tandwielpictogram om terug te keren naar het tabblad *Velden* en u moet nu meerdere gebeurtenistypen en schemavelden kunnen weergeven, ongeacht of deze gegevens bevatten of niet.

![](../images/segment-builder/show-populated.png)

### Soorten publiek

Op het tabblad **Soorten publiek** worden alle soorten publiek weergegeven die zijn geïmporteerd uit externe bronnen, zoals Adobe Audience Manager, en ook het publiek dat is gemaakt in het Experience Platform.

Op het tabblad Soorten publiek kunt u alle beschikbare bronnen weergeven als een groep mappen. Terwijl u in deze mappen klikt, zijn de beschikbare submappen en doelgroepen zichtbaar. Bovendien kunt u op het mappictogram (zoals getoond in uiterst rechtse beeld) klikken om de omslagstructuur (een vinkje wijst op de omslag u momenteel in bent) en gemakkelijk terug door omslagen te navigeren door op de naam van een omslag in de boom te klikken.

U kunt de muisaanwijzer boven de ⓘ naast een doelgroep houden om informatie over het publiek weer te geven, zoals de id, beschrijving en maphiërarchie, om het publiek te zoeken.

![](../images/segment-builder/audience-folder-structure.png)

U kunt ook naar Soorten publiek zoeken met de zoekbalk, die de zoeksyntaxis [van](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene gebruikt. Als u op het tabblad *Soorten publiek* een map op hoofdniveau selecteert, wordt de zoekbalk weergegeven, zodat u in die map kunt zoeken. Zoekresultaten beginnen pas te worden gevuld wanneer hele woorden zijn ingevoerd. Als u bijvoorbeeld een publiek wilt zoeken met de naam `Online Shoppers`, typt u &quot;Online&quot; in de zoekbalk. Nadat het woord &quot;Online&quot; volledig is getypt, worden zoekresultaten met het woord &quot;Online&quot; weergegeven.

## Rule builder canvas

Een segmentdefinitie is een inzameling van regels die worden gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Deze regels worden gecreeerd gebruikend het canvas *van de* regelbouwer, dat in het centrum van de Bouwer van het Segment wordt gevestigd.

Als u een nieuwe regel wilt toevoegen aan de segmentdefinitie, sleept u een tegel van het tabblad *Velden* en zet u deze neer op het canvas van de regelbuilder. Vervolgens krijgt u contextspecifieke opties, afhankelijk van het type gegevens dat u wilt toevoegen. Beschikbare gegevenstypen zijn: tekenreeksen, datums, ExperienceEvents, gebeurtenistypen en Soorten publiek.

![](../images/segment-builder/rule-builder-canvas.png)

### Soorten publiek toevoegen

U kunt een publiek van het lusje van het *Publiek* op het canvas van de regelbouwer slepen en laten vallen om publiekslidmaatschap in de nieuwe segmentdefinitie te verwijzen. Dit staat u toe om publiekslidmaatschap als attribuut in de nieuwe segmentregel te omvatten of uit te sluiten.

Voor het publiek van het Platform dat gebruikend de Bouwer van het Segment wordt gecreeerd, wordt u gegeven de optie om het publiek in de reeks regels om te zetten die in de segmentdefinitie voor dat publiek werden gebruikt. Deze omzetting maakt een exemplaar van de regellogica, die dan kan worden gewijzigd zonder de originele segmentdefinitie te beïnvloeden.

>[!NOTE] Wanneer u een publiek uit een externe bron toevoegt, wordt alleen verwezen naar het publiekslidmaatschap. U kunt het publiek niet in regels omzetten, en daarom kunnen de regels die worden gebruikt om het originele publiek tot stand te brengen niet in de nieuwe segmentdefinitie worden gewijzigd.

![](../images/segment-builder/add-audience-to-segment.png)

## Containers

Segmentregels worden geëvalueerd in de volgorde waarin ze worden weergegeven. De containers staan controle over de orde van uitvoering door het gebruik van genestelde vragen toe.

Zodra u minstens één tegel aan het canvas van de regelbouwer hebt toegevoegd, kunt u beginnen om containers toe te voegen. Als u een nieuwe container wilt maken, klikt u op de ovalen (...) in de rechterbovenhoek van de tegel en klikt u op Container **** toevoegen.

![](../images/segment-builder/add-container.png)

Een nieuwe container wordt weergegeven als het onderliggende element van de eerste container, maar u kunt de hiërarchie aanpassen door de containers te slepen en te verplaatsen. Het standaardgedrag van een container is om het kenmerk, de gebeurtenis of het publiek dat wordt verschaft, op te nemen. U kunt de regel instellen op Profielen uitsluiten die voldoen aan de containercriteria door op **Opnemen** in de linkerbovenhoek van de tegel te klikken en op Uitsluiten te klikken.

Een onderliggende container kan ook inline worden geëxtraheerd en toegevoegd aan de bovenliggende container door op de onderliggende container op de knop &#39;container opheffen&#39; te klikken. Klik op de ovalen (...) in de rechterbovenhoek van de onderliggende container om deze optie te openen.

![](../images/segment-builder/include-exclude.png)

Nadat u op **Omloopcontainer** ongedaan maken hebt geklikt, wordt de onderliggende container verwijderd en worden de criteria inline weergegeven.

>[!NOTE] Wanneer het unwrapping containers, zorg ervoor dat de logica de gewenste segmentdefinitie blijft ontmoeten.

![](../images/segment-builder/unwrapped-container-inline.png)

## Beleid samenvoegen

Het Platform van de ervaring laat u toe om gegevens uit veelvoudige bronnen te brengen en het te combineren om een volledige mening van elk van uw individuele klanten te zien. Wanneer het samenbrengen van deze gegevens, zijn het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om een profiel tot stand te brengen.

U kunt een samenvoegbeleid selecteren dat uw marketing doel voor dit publiek aanpast of het standaardsamenvoegbeleid gebruiken dat door Platform wordt verstrekt. U kunt meerdere samenvoegbeleidsregels maken die uniek zijn voor uw organisatie, waaronder het maken van uw eigen standaardbeleid voor samenvoegen. Voor geleidelijke instructies bij het creëren van fusiebeleid voor uw organisatie, te zien gelieve de zelfstudie over het [werken met fusiebeleid gebruikend UI](../../profile/ui/merge-policies.md).

Als u een samenvoegbeleid voor uw segmentdefinitie wilt selecteren, klikt u op het tandwielpictogram op het tabblad *Velden* en gebruikt u het vervolgkeuzemenu *Beleid voor* samenvoegen om het samenvoegbeleid te selecteren dat u wilt gebruiken.

![](../images/segment-builder/merge-policy-selector.png)

## Segmenteigenschappen

Wanneer het bouwen van een segmentdefinitie, toont de sectie van de Eigenschappen *van het* Segment op de rechterkant van de werkruimte een schatting van de grootte van het resulterende segment, toestaand u om uw segmentdefinitie zonodig aan te passen alvorens het publiek zelf te bouwen.

In de sectie *Segmenteigenschappen* kunt u ook belangrijke informatie over de segmentdefinitie opgeven, zoals de *naam* en de *beschrijving*. De definitienamen van het segment worden gebruikt om uw segment onder die te identificeren die door uw organisatie worden bepaald en zouden daarom beschrijvend, beknopt, en uniek moeten zijn.

Terwijl u de segmentdefinitie verder ontwikkelt, kunt u een gepagineerde voorvertoning van het publiek weergeven door Profielen **** weergeven te selecteren.

![](../images/segment-builder/segment-properties.png)

>[!NOTE] De schattingen van het publiek worden geproduceerd door een steekproefgrootte van de steekproefgegevens van die dag te gebruiken. Als uw profielarchief minder dan 1 miljoen entiteiten bevat, wordt de volledige gegevensset gebruikt. voor tussen 1 en 20 miljoen entiteiten worden 1 miljoen entiteiten gebruikt; en voor meer dan 20 miljoen entiteiten wordt 5 % van de totale entiteiten gebruikt . Meer informatie over het produceren van segmentramingen kan in de sectie [van de de](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) schattingsproductie van de sectievan de segmentverwezenlijking worden gevonden.

## Geplande segmentatie inschakelen

Zodra de segmentdefinities zijn gecreeerd, kunt u hen door op bestelling of geplande (ononderbroken) evaluatie dan evalueren. Evaluatie houdt in dat de gegevens van het Profiel van de Klant in real time door segmentdefinities worden verplaatst om het overeenkomstige publiek te produceren. Nadat het publiek is gemaakt, wordt het opgeslagen en opgeslagen zodat het kan worden geëxporteerd met de API&#39;s van het Experience Platform.

De evaluatie op bestelling impliceert het gebruiken van API om evaluatie uit te voeren en publiek te bouwen zoals nodig, terwijl de geplande evaluatie (die ook als &quot;geplande segmentatie&quot;wordt bekend) u toestaat om een terugkerend programma tot stand te brengen om segmentdefinities op een specifieke tijd (bij een maximum, eenmaal per dag) te evalueren.

Het toelaten van uw segmentdefinities voor geplande evaluatie kan worden gedaan gebruikend UI of API. In UI, terugkeer naar het *Browse* lusje binnen **Segmenten** en knevel op **Evaluate alle segmenten**. Dit zal ertoe leiden dat alle segmenten worden geëvalueerd gebaseerd op het programma dat door uw organisatie wordt geplaatst.

>[!NOTE] De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor Individueel Profiel XDM worden toegelaten. Als uw organisatie meer dan vijf samenvoegingsbeleid voor Individueel Profiel XDM binnen één enkele zandbakmilieu heeft, zult u geen geplande evaluatie kunnen gebruiken.

Planningen kunnen momenteel alleen worden gemaakt met behulp van de API. Voor gedetailleerde stappen bij het creëren van, het uitgeven van, en het werken met programma&#39;s die API gebruiken, te volgen gelieve de leerprogramma&#39;s voor het evalueren van en de toegang tot van segmentresultaten, specifiek de sectie over [geplande evaluatie gebruikend API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Segmentering voor streaming inschakelen

>[!NOTE] Streaming segmentatie is een bètafunctie en is op verzoek beschikbaar.

Bovendien, kan een segmentdefinitie voor het stromen segmentatie vóór of na het worden toegelaten. Streaming segmentatie evalueert direct een klant zodra een gebeurtenis in een bepaalde segmentgroep komt. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in Platform worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden. Lees de documentatie over de [streamingsegmentatie](../api/streaming-segmentation.md)voor meer informatie over streamingsegmentatie.

Het toelaten van uw segmentdefinities voor het stromen kan worden gedaan gebruikend UI of API. Om een nieuwe of bestaande segmentdefinitie voor het stromen in UI toe te laten, moet u de *Streaming* optie aan **VERSCHAKELEN**.

![](../images/segment-builder/enable-streaming-segmentation.png)

Zodra het stromen segmentatie is toegelaten, moet een basislijn worden gevestigd (dit is de aanvankelijke looppas waarna het segment altijd bijgewerkt zal zijn). Het systeem behandelt automatisch baselining, echter dit is slechts mogelijk als de geplande segmentatie is toegelaten. Raadpleeg voor meer informatie over het inschakelen van geplande segmentatie [de vorige sectie in deze gebruikershandleiding](#enable-scheduled-segmentation).

## Beleidsovertredingen DULE

>[!NOTE] De DULE beleidsschendingen zijn slechts van toepassing als u een segment creeert dat aan een bestemming is toegewezen.

Zodra u wordt gedaan creërend uw segment, zal het segment door de Governance van Gegevens worden geanalyseerd om ervoor te zorgen dat er geen beleidsschendingen binnen het segment zijn. Voor meer informatie over DULE en beleidsovertredingen raadpleegt u het overzicht [van de](../../data-governance/labels/overview.md)gegevensgebruikslabel.

![](../images/segment-builder/segment-dule-policy-violations.png)

## Volgende stappen

De Bouwer van het segment verstrekt een rijk werkschema toelatend u om verhandelbare toehoorden van de gegevens van het Profiel van de Klant in real time te isoleren. Na het lezen van deze handleiding moet u nu in staat zijn om:

- Maak segmentdefinities met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
- Gebruik het canvas en de containers van de regelbouwer om de orde te controleren waarin de segmentregels worden uitgevoerd.
- De schattingen van de mening van uw potentiële publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
- Schakel alle segmentdefinities in voor geplande segmentatie.
- Hiermee kunt u opgegeven segmentdefinities voor streaming segmentatie inschakelen.

Voor geleidelijke instructies bij het werken met de Dienst van de Segmentatie die in real time API van het Profiel van de Klant gebruikt, zie het [creëren publiekssegmenten gebruikend APIs](../tutorials/create-a-segment.md) leerprogramma.