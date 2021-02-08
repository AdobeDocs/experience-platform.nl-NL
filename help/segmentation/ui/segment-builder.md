---
keywords: Experience Platform;huis;populaire onderwerpen;de Dienst van de segmentatie;segmentatie;segmenteringsdienst;gebruikersgids;ui gids;segmentation ui gids;segmentbouwer;de bouwer van het segment;
solution: Experience Platform
title: UI-gids voor segmentBuilder
topic: ui guide
description: 'De segmentbouwer in Adobe Experience Platform UI verstrekt een rijke werkruimte die u toestaat om met de gegevenselementen van het Profiel in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen. '
translation-type: tm+mt
source-git-commit: 8fc1c5414f38e84ed1700ee95b1c382007ff2c27
workflow-type: tm+mt
source-wordcount: '1928'
ht-degree: 0%

---


# [!DNL Segment Builder] UI-hulplijn

[!DNL Segment Builder] biedt een rijke werkruimte waarmee u kunt werken met  [!DNL Profile] gegevenselementen. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.

![](../images/ui/segment-builder/segment-builder.png)

## Bouwstenen voor segmentdefinitie

De basisbouwstenen van segmentdefinities zijn attributen en gebeurtenissen. Daarnaast kunnen de kenmerken en gebeurtenissen in bestaande doelgroepen ook worden gebruikt als componenten voor nieuwe definities.

U kunt deze bouwstenen in de **[!UICONTROL sectie van Gebieden]** op de linkerkant van [!DNL Segment Builder] werkruimte zien. **[!UICONTROL De velden]** bevatten een tab voor elk van de belangrijkste bouwstenen: &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; en &quot;[!UICONTROL Audiences]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Attributen

Met het tabblad **[!UICONTROL Kenmerken]** kunt u door [!DNL Profile]-kenmerken bladeren die horen bij de klasse [!DNL XDM Individual Profile]. Elke map kan worden uitgevouwen om extra kenmerken weer te geven. Elk kenmerk is een tegel die naar het canvas voor regelbuilders in het midden van de werkruimte kan worden gesleept. Het [regelbuildercanvas](#rule-builder-canvas) wordt later in deze handleiding uitgebreid besproken.

![](../images/ui/segment-builder/attributes.png)

### Gebeurtenissen

Met het tabblad **[!UICONTROL Gebeurtenissen]** kunt u een publiek maken op basis van gebeurtenissen of acties die hebben plaatsgevonden met behulp van [!DNL XDM ExperienceEvent] gegevenselementen. U kunt de Types van Gebeurtenis op **[!UICONTROL Gebeurtenissen]** lusje ook vinden, die een inzameling van algemeen gebruikte gebeurtenissen zijn om u toe te laten om uw segmenten sneller tot stand te brengen.

Naast het kunnen naar [!DNL ExperienceEvent] elementen doorbladeren, kunt u ook naar de Types van Gebeurtenis zoeken. Gebeurtenistypen gebruiken dezelfde coderingslogica als [!DNL ExperienceEvents], zonder dat u door de klasse [!DNL XDM ExperienceEvent] hoeft te zoeken om de juiste gebeurtenis te zoeken. Als u bijvoorbeeld met de zoekbalk zoekt naar &quot;winkelwagentje&quot;, worden de gebeurtenistypen &quot;[!UICONTROL AddCart]&quot; en &quot;[!UICONTROL RemoveCart]&quot; geretourneerd. Dit zijn twee veelgebruikte tekenacties bij het samenstellen van segmentdefinities.

Om het even welk type van component kan worden gezocht door zijn naam in de onderzoeksbar te typen, die [de onderzoekssyntaxis van Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax) gebruikt. De zoekresultaten beginnen te vullen wanneer hele woorden worden ingevoerd. Als u bijvoorbeeld een regel wilt maken op basis van het XDM-veld `ExperienceEvent.commerce.productViews`, typt u &quot;productweergaven&quot; in het zoekveld. Nadat u het woord &quot;product&quot; hebt getypt, worden de zoekresultaten weergegeven. Elk resultaat bevat de objecthiërarchie waartoe het behoort.

>[!NOTE]
>
>De het schemagebieden van de douane die door uw organisatie worden bepaald kunnen tot 24 uren aan verschijnen en beschikbaar voor gebruik in het bouwen van regels vergen.

Vervolgens kunt u [!DNL ExperienceEvents] en &quot;[!UICONTROL Gebeurtenistypen]&quot; eenvoudig naar uw segmentdefinitie slepen.

![](../images/ui/segment-builder/events-eventTypes.png)

Standaard worden alleen gevulde schemavelden uit de gegevensopslag weergegeven. Dit omvat &quot;[!UICONTROL Gebeurtenistypen]&quot;. Als de lijst &quot;[!UICONTROL Gebeurtenistypen]&quot; niet zichtbaar is of u alleen &quot;[!UICONTROL Willekeurig]&quot; als &quot;[!UICONTROL Gebeurtenistype]&quot; kunt selecteren, selecteert u **tandwielpictogram** naast **[!UICONTROL Velden]**, dan **[!UICONTROL Volledige XDM tonen schema]** onder **[!UICONTROL Beschikbare velden]**. Selecteer nogmaals **tandwielpictogram** om naar **[!UICONTROL Fields]** tabel terug te keren en u zou nu veelvoudige &quot;[!UICONTROL Types van Gebeurtenis]&quot;en schemagebieden moeten kunnen bekijken, ongeacht of zij gegevens bevatten of niet.

![](../images/ui/segment-builder/show-populated.png)

### Doelgroepen

Op het tabblad **[!UICONTROL Soorten publiek]** worden alle soorten publiek weergegeven die zijn geïmporteerd uit externe bronnen, zoals Adobe Audience Manager, en ook het publiek dat is gemaakt in [!DNL Experience Platform].

Op **[!UICONTROL Soorten publiek]** lusje, kunt u alle beschikbare bronnen als groep omslagen zien. Terwijl u de mappen selecteert, zijn de beschikbare submappen en doelgroepen zichtbaar. Bovendien kunt u het mappictogram (zoals weergegeven in de afbeelding uiterst rechts) selecteren om de mapstructuur weer te geven (een vinkje geeft de map aan die u momenteel in hebt) en eenvoudig terug te navigeren door de mappen door de naam van een map in de boomstructuur te selecteren.

U kunt de muisaanwijzer boven de ⓘ naast een doelgroep houden om informatie over het publiek weer te geven, zoals de id, beschrijving en maphiërarchie, om het publiek te zoeken.

![](../images/ui/segment-builder/audience-folder-structure.png)

U kunt naar publiek ook zoeken gebruikend de onderzoeksbar, die [de onderzoekssyntaxis van Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax) gebruikt. Op **[!UICONTROL Soorten publiek]** tabel, zorgt het selecteren van een top-level omslag ervoor dat de onderzoeksbar verschijnt, toestaand u om binnen die omslag te zoeken. Zoekresultaten beginnen pas te worden gevuld wanneer hele woorden zijn ingevoerd. Als u bijvoorbeeld een publiek zoekt met de naam `Online Shoppers`, typt u &quot;Online&quot; in de zoekbalk. Nadat het woord &quot;Online&quot; volledig is getypt, worden zoekresultaten met het woord &quot;Online&quot; weergegeven.

## Rule builder canvas {#rule-builder-canvas}

Een segmentdefinitie is een inzameling van regels die worden gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Deze regels worden gecreeerd gebruikend het canvas van de regelbouwer, dat in het centrum van [!DNL Segment Builder] wordt gevestigd.

Om een nieuwe regel aan uw segmentdefinitie toe te voegen, sleep een tegel van **[!UICONTROL Fields]** lusje en laat vallen het op het canvas van de regelbouwer. Vervolgens krijgt u contextspecifieke opties, afhankelijk van het type gegevens dat u wilt toevoegen. Beschikbare gegevenstypen zijn: tekenreeksen, datums, [!DNL ExperienceEvents], &quot;[!UICONTROL Gebeurtenistypen]&quot; en doelgroepen.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>De meest recente wijzigingen in Adobe Experience Platform hebben het gebruik van de logische operatoren `OR` en `AND` tussen gebeurtenissen bijgewerkt. Deze updates zijn niet van invloed op bestaande segmenten. Deze wijzigingen zijn echter van invloed op alle volgende updates van bestaande segmenten en nieuwe segmentcreaties. Lees de [tijdconstanten bijwerken](./segment-refactoring.md) voor meer informatie.

### Soorten publiek toevoegen

U kunt een publiek van **[!UICONTROL het lusje van het Publiek]** op het canvas van de regelbouwer slepen en laten vallen om publiekslidmaatschap in de nieuwe segmentdefinitie te verwijzen. Dit staat u toe om publiekslidmaatschap als attribuut in de nieuwe segmentregel te omvatten of uit te sluiten.

Voor [!DNL Platform] publiek gecreeerd gebruikend [!DNL Segment Builder], wordt u gegeven de optie om het publiek in de reeks regels om te zetten die in de segmentdefinitie voor dat publiek werden gebruikt. Deze omzetting maakt een exemplaar van de regellogica, die dan kan worden gewijzigd zonder de originele segmentdefinitie te beïnvloeden. Zorg ervoor dat u recente wijzigingen in de segmentdefinitie hebt opgeslagen voordat u deze omzet in regellogica.

>[!NOTE]
>
>Wanneer u een publiek uit een externe bron toevoegt, wordt alleen verwezen naar het publiekslidmaatschap. U kunt het publiek niet in regels omzetten, en daarom kunnen de regels die worden gebruikt om het originele publiek tot stand te brengen niet in de nieuwe segmentdefinitie worden gewijzigd.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Als er conflicten optreden wanneer een publiek wordt omgezet in regels, probeert [!DNL Segment Builder] de bestaande opties zo goed mogelijk te behouden.

### Codeweergave

Alternatief, kunt u een code-gebaseerde versie van een regel bekijken die in [!DNL Segment Builder] wordt gecreeerd. Zodra u uw regel binnen het canvas van de regelbouwer hebt gecreeerd, kunt u **[!UICONTROL de mening van de Code]** selecteren om uw segment als PQL te zien.

![](../images/ui/segment-builder/code-view.png)

De mening van de code verstrekt een knoop die u toestaat om de waarde van het segment in API vraag te kopiëren. Om de recentste versie van het segment te krijgen, zorg ervoor u uw recentste veranderingen in het segment hebt bewaard.

![](../images/ui/segment-builder/copy-code.png)

### Samenvoegingsfuncties

Een samenvoeging in [!DNL Segment Builder] is een berekening op een groep attributen XDM waarvan gegevenstype een aantal (of een dubbel of een geheel) is. De vier gesteunde samenvoegingsfuncties binnen de Bouwer van het Segment zijn SUM, GEMIDDELD, MIN, en MAX.

Als u een aggregatiefunctie wilt maken, selecteert u een gebeurtenis in de linkertrack en voegt u deze in de container [!UICONTROL Gebeurtenissen] in.

![](../images/ui/segment-builder/select-event.png)

Nadat u de gebeurtenis in de container Gebeurtenissen hebt geplaatst, selecteert u het pictogram Ovalen (...), gevolgd door **[!UICONTROL Samenvoegen]**.

![](../images/ui/segment-builder/add-aggregation.png)

De samenvoeging wordt nu toegevoegd. U kunt nu de aggregatiefunctie selecteren, kiezen welk kenmerk wordt geaggregeerd, de gelijkheidsfunctie en de waarde. In het onderstaande voorbeeld zou dit segment elk profiel kwalificeren dat een som aangekochte waarden heeft die groter is dan $100, zelfs als elke afzonderlijke aankoop minder dan $100 is.

![](../images/ui/segment-builder/filled-aggregation.png)

## Containers

Segmentregels worden geëvalueerd in de volgorde waarin ze worden weergegeven. De containers staan controle over de orde van uitvoering door het gebruik van genestelde vragen toe.

Zodra u minstens één tegel aan het canvas van de regelbouwer hebt toegevoegd, kunt u beginnen om containers toe te voegen. Als u een nieuwe container wilt maken, selecteert u de ovalen (...) in de rechterbovenhoek van de tegel en selecteert u **[!UICONTROL Container toevoegen]**.

![](../images/ui/segment-builder/add-container.png)

Een nieuwe container wordt weergegeven als het onderliggende element van de eerste container, maar u kunt de hiërarchie aanpassen door de containers te slepen en te verplaatsen. Het standaardgedrag van een container is aan &quot;[!UICONTROL Include]&quot;de attributen, de gebeurtenis, of het publiek verstrekte. U kunt de regel instellen op &quot;[!UICONTROL Exclude]&quot;-profielen die voldoen aan de containercriteria door **[!UICONTROL Include]** in de linkerbovenhoek van de tegel te selecteren en &quot;[!UICONTROL Exclude]&quot; te selecteren.

Een onderliggende container kan ook inline worden geëxtraheerd en toegevoegd aan de bovenliggende container door &quot;container opheffen&quot; te selecteren in de onderliggende container. Selecteer de ellipsen (...) in de hoger-juiste hoek van de kindcontainer om tot deze optie toegang te hebben.

![](../images/ui/segment-builder/include-exclude.png)

Als u **[!UICONTROL Container]** opheffen selecteert, wordt de onderliggende container verwijderd en worden de criteria inline weergegeven.

>[!NOTE]
>
>Wanneer het unwrapping containers, zorg ervoor dat de logica de gewenste segmentdefinitie blijft ontmoeten.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Beleid samenvoegen

[!DNL Experience Platform] laat u toe om gegevens uit veelvoudige bronnen te brengen en het te combineren om een volledige mening van elk van uw individuele klanten te zien. Wanneer het samenbrengen van deze gegevens, is het fusiebeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om een profiel tot stand te brengen.

U kunt een samenvoegbeleid selecteren dat uw marketing doel voor dit publiek aanpast of het standaardsamenvoegbeleid gebruiken dat door [!DNL Platform] wordt verstrekt. U kunt meerdere samenvoegbeleidsregels maken die uniek zijn voor uw organisatie, waaronder het maken van uw eigen standaardbeleid voor samenvoegen. Voor geleidelijke instructies bij het creëren van fusiebeleid voor uw organisatie, te zien gelieve de zelfstudie over [het werken met fusiebeleid gebruikend UI](../../profile/ui/merge-policies.md).

Als u een samenvoegbeleid voor uw segmentdefinitie wilt selecteren, selecteert u het tandwielpictogram op het tabblad **[!UICONTROL Velden]** en gebruikt u het vervolgkeuzemenu **[!UICONTROL Beleid samenvoegen]** om het samenvoegbeleid te selecteren dat u wilt gebruiken.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Segmenteigenschappen

Wanneer het bouwen van een segmentdefinitie, **[!UICONTROL de sectie van Eigenschappen van het Segment]** op de rechterkant van de werkruimte toont een schatting van de grootte van het resulterende segment, toestaand u om uw segmentdefinitie zonodig aan te passen alvorens het publiek zelf te bouwen.

In de sectie **[!UICONTROL Segmenteigenschappen]** kunt u ook belangrijke informatie over de segmentdefinitie opgeven, inclusief de naam en beschrijving. De definitienamen van het segment worden gebruikt om uw segment onder die te identificeren die door uw organisatie worden bepaald en zouden daarom beschrijvend, beknopt, en uniek moeten zijn.

Terwijl u de segmentdefinitie verder ontwikkelt, kunt u een gepagineerde voorvertoning van het publiek weergeven door **[!UICONTROL Profielen weergeven]** te selecteren.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>De schattingen van het publiek worden geproduceerd door een steekproefgrootte van de steekproefgegevens van die dag te gebruiken. Als uw profielarchief minder dan 1 miljoen entiteiten bevat, wordt de volledige gegevensset gebruikt. voor tussen 1 en 20 miljoen entiteiten worden 1 miljoen entiteiten gebruikt; en voor meer dan 20 miljoen entiteiten wordt 5 % van de totale entiteiten gebruikt . Meer informatie over het produceren van segmentramingen kan in [schattingsgeneratiesectie](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) van het de schepingsleerprogramma van het segment worden gevonden.

## Volgende stappen en extra bronnen {#next-steps}

De Bouwer van het segment verstrekt een rijk werkschema toelatend u om verhandelbare doelgroepen van [!DNL Real-time Customer Profile] gegevens te isoleren. Na het lezen van deze handleiding moet u nu in staat zijn om:

- Maak segmentdefinities met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
- Gebruik het canvas en de containers van de regelbouwer om de orde te controleren waarin de segmentregels worden uitgevoerd.
- De schattingen van de mening van uw potentiële publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
- Schakel alle segmentdefinities in voor geplande segmentatie.
- Hiermee kunt u opgegeven segmentdefinities voor streaming segmentatie inschakelen.

Als u meer wilt weten over [!DNL Segmentation Service], leest u de documentatie en vult u deze aan door de onderstaande video&#39;s te bekijken. Voor meer informatie over de andere onderdelen van de interface [!DNL Segmentation Service] leest u de [[!DNL Segmentation Service] gebruikershandleiding](./overview.md)

>[!WARNING]
>
> De interface [!DNL Platform] die in de volgende video&#39;s wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

**Een segment maken:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**Een dynamisch segment maken:**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)