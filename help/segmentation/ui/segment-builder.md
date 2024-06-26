---
solution: Experience Platform
title: UI-gids voor segmentBuilder
description: De segmentbouwer in Adobe Experience Platform UI verstrekt een rijke werkruimte die u toestaat om met de gegevenselementen van het Profiel in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 305aa7f44cd64d9a0ae704fe9aa01d2d1c536ade
workflow-type: tm+mt
source-wordcount: '3664'
ht-degree: 0%

---

# [!DNL Segment Builder] UI-hulplijn

>[!NOTE]
>
>In deze handleiding wordt uitgelegd hoe u een publiek kunt maken **segmentdefinities** met de Segment Builder. Als u wilt leren hoe u publiek kunt maken met Audience Composition, leest u de [Handleiding voor compositie van publiek](./audience-composition.md).

[!DNL Segment Builder] biedt een rijke werkruimte waarmee u kunt werken met [!DNL Profile] gegevenselementen. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.

![De gebruikersinterface van Segment Builder wordt weergegeven.](../images/ui/segment-builder/segment-builder.png)

## Bouwstenen voor segmentdefinitie {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="Velden"
>abstract="De drie veldtypen waaruit een segmentdefinitie bestaat, zijn kenmerken, gebeurtenissen en doelgroepen. Met kenmerken kunt u Profielkenmerken gebruiken die horen bij de klasse Individueel profiel XDM, gebeurtenissen kunt u een publiek maken op basis van handelingen of gebeurtenissen die plaatsvinden met XDM ExperienceEvent-gegevenselementen en publiek kunt geïmporteerde soorten publiek uit externe bronnen gebruiken."

De basisbouwstenen van segmentdefinities zijn attributen en gebeurtenissen. Daarnaast kunnen de kenmerken en gebeurtenissen in bestaande doelgroepen worden gebruikt als componenten voor nieuwe definities.

U kunt deze bouwstenen zien in de **[!UICONTROL Fields]** aan de linkerkant van het dialoogvenster [!DNL Segment Builder] werkruimte. **[!UICONTROL Fields]** bevat een tab voor elk van de belangrijkste bouwstenen : &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot;, en &quot;[!UICONTROL Audiences]&quot;.

![De sectie met velden van de Segment Builder wordt gemarkeerd.](../images/ui/segment-builder/segment-fields.png)

### Attributen

De **[!UICONTROL Attributes]** kunt u bladeren [!DNL Profile] kenmerken van de [!DNL XDM Individual Profile] klasse. Elke map kan worden uitgevouwen om extra kenmerken weer te geven. Elk kenmerk is een tegel die naar het canvas voor regelbuilders in het midden van de werkruimte kan worden gesleept. De [regelbouwcanvas](#rule-builder-canvas) wordt later in deze handleiding gedetailleerder besproken.

![De sectie met kenmerken van de velden Segment Builder wordt gemarkeerd.](../images/ui/segment-builder/attributes.png)

### Gebeurtenissen

De **[!UICONTROL Events]** kunt u een publiek maken op basis van gebeurtenissen of acties die hebben plaatsgevonden via [!DNL XDM ExperienceEvent] gegevenselementen. U kunt gebeurtenistypen ook vinden op het tabblad **[!UICONTROL Events]** tab, die een verzameling veelgebruikte gebeurtenissen zijn om u in staat te stellen sneller uw segmentdefinities te maken.

Niet alleen kunnen bladeren naar [!DNL ExperienceEvent] U kunt ook naar gebeurtenistypen zoeken. Gebeurtenistypen gebruiken dezelfde coderingslogica als [!DNL ExperienceEvents], zonder dat u door de [!DNL XDM ExperienceEvent] klasse die de juiste gebeurtenis zoekt. Als u bijvoorbeeld op de zoekbalk zoekt naar &quot;winkelwagentje&quot;, worden de gebeurtenistypen &quot;[!UICONTROL AddCart]&quot; en &quot;[!UICONTROL RemoveCart]&quot;, die twee zeer vaak gebruikte acties van het karretje zijn wanneer het bouwen van segmentdefinities.

Elk type component kan worden gezocht door zijn naam in de onderzoeksbar te typen, die gebruikt [Zoeksyntaxis van Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). De zoekresultaten beginnen te vullen wanneer hele woorden worden ingevoerd. Bijvoorbeeld, om een regel te bouwen die op het XDM gebied wordt gebaseerd `ExperienceEvent.commerce.productViews`typt u &quot;productweergaven&quot; in het zoekveld. Nadat u het woord &quot;product&quot; hebt getypt, worden de zoekresultaten weergegeven. Elk resultaat bevat de objecthiërarchie waartoe het behoort.

>[!NOTE]
>
>De het schemagebieden van de douane die door uw organisatie worden bepaald kunnen tot 24 uren aan verschijnen en beschikbaar voor gebruik in het bouwen van regels vergen.

Vervolgens kunt u eenvoudig slepen en neerzetten [!DNL ExperienceEvents] en &quot;[!UICONTROL Event Types]&quot; in uw segmentdefinitie.

![De gebeurtenissensectie van de gebruikersinterface van Segment Builder wordt gemarkeerd.](../images/ui/segment-builder/events.png)

Standaard worden alleen gevulde schemavelden uit de gegevensopslag weergegeven. Dit omvat &quot;[!UICONTROL Event Types]&quot;. Als &quot;[!UICONTROL Event Types]De lijst is niet zichtbaar of u kunt alleen &quot;[!UICONTROL Any]&quot; als een &quot;[!UICONTROL Event Type]&quot;, selecteert u de **tandwielpictogram** naast **[!UICONTROL Fields]** selecteert u vervolgens **[!UICONTROL Show full XDM schema]** krachtens **[!UICONTROL Available Fields]**. Selecteer de **tandwielpictogram** nogmaals om terug te keren naar de **[!UICONTROL Fields]** en u moet nu meerdere bestanden kunnen bekijken &quot;[!UICONTROL Event Types]&quot; en schema-velden, ongeacht of deze gegevens bevatten of niet.

![Keuzerondjes waarmee u alleen velden met gegevens of alle XDM-velden kunt weergeven, worden gemarkeerd.](../images/ui/segment-builder/show-populated.png)

#### Gegevenssets van Adobe Analytics-rapportsuite

U kunt gegevens uit één of meerdere Adobe Analytics-rapportreeksen gebruiken als gebeurtenissen binnen de segmentatie.

Wanneer het gebruiken van gegevens van één enkele het rapportreeks van Analytics, zal Platform automatisch beschrijvers en vriendschappelijke namen aan Vars toevoegen, die het gemakkelijker maken om die gebieden binnen te vinden [!DNL Segment Builder].

![Een afbeelding die aangeeft hoe generieke variabelen (eVars) worden toegewezen met een gebruikersvriendelijke naam.](../images/ui/segment-builder/single-report-suite.png)

Bij gebruik van gegevens uit meerdere Analytics-rapportreeksen, Platform **kan** Voeg automatisch beschrijvingen of vriendelijke namen toe aan Vars. Dientengevolge, alvorens de gegevens van Analytics rapportreeksen te gebruiken, moet u aan XDM gebieden in kaart brengen. Meer informatie over het toewijzen van variabelen van de Analytics aan XDM kan in worden gevonden [Adobe Analytics-bronverbindingsgids](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping).

Neem bijvoorbeeld een situatie waarin u twee rapportsuites met de volgende variabelen had:

| Veld | Report Suite Schema A | Report Suite Schema B |
| ----- | --------------------- | --------------------- |
| eVar1 | Referentiedomein | Aangemeld in Y/N |
| eVar2 | Paginanaam | Lidmaatschap-ID |
| eVar3 | URL | Paginanaam |
| eVar4 | Zoekvoorwaarden | Productnaam |
| event1 | Klikken | Paginaweergaven |
| event2 | Paginaweergaven | Extra winkelwagentjes |
| event3 | Extra winkelwagentjes | Afbeeldingen |
| event4 | Aankopen | Aankopen |

In dit geval, kon u de twee rapportreeksen met het volgende schema in kaart brengen:

![Een afbeelding die aangeeft hoe twee rapportsuites kunnen worden toegewezen aan één samenvoegingsschema.](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>Terwijl de generieke waarden van eVar nog worden bevolkt, zou u moeten **niet** gebruik ze in de segmentdefinities (indien mogelijk), aangezien de waarden verschillende dingen kunnen betekenen dan wat ze oorspronkelijk in hun rapporten stonden.

Zodra de rapportsuites in kaart zijn gebracht, kunt u deze onlangs in kaart gebrachte gebieden binnen uw op profiel-betrekking hebbende werkschema&#39;s en segmentatie gebruiken.

| Scenario | Unieschema-ervaring | Segmentatie generieke variabele | Aan segment toegewezen variabele |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| Single-rapportenpakket | Beschrijvende naam wordt opgenomen in algemene variabelen. <br><br>**Voorbeeld:** Paginanaam (eVar2) | <ul><li>Beschrijvende naam opgenomen met algemene variabelen</li><li>De vraag gebruikt gegevens van de specifieke dataset, aangezien het de enige is</li></ul> | Query&#39;s kunnen gebruikmaken van Adobe Analytics-gegevens en mogelijk andere bronnen. |
| Meerdere rapportsuites | Bij generieke variabelen worden geen beschrijvingen van vriendelijke namen opgenomen. <br><br>**Voorbeeld:** eVar2 | <ul><li>Elk veld met meerdere beschrijvingen wordt algemeen weergegeven. Dit betekent dat er geen vriendelijke namen worden weergegeven in de gebruikersinterface.</li><li>De vragen kunnen gegevens van om het even welke datasets gebruiken die de eVar bevatten, die in gemengde of onjuiste resultaten kunnen resulteren.</li></ul> | De vraag gebruikt correct gecombineerde resultaten van veelvoudige datasets. |

### Soorten publiek

>[!NOTE]
>
>Voor publiek dat is gemaakt in Platform, alleen publiek dat de **zelfde** het samenvoegbeleid wordt weergegeven.

De **[!UICONTROL Audiences]** worden alle soorten publiek weergegeven die zijn geïmporteerd uit externe bronnen, zoals Adobe Audience Manager of Customer Journey Analytics, en alle soorten publiek die zijn gemaakt in [!DNL Experience Platform].

Op de **[!UICONTROL Audiences]** kunt u alle beschikbare bronnen weergeven als een groep mappen. Terwijl u de mappen selecteert, zijn de beschikbare submappen en doelgroepen zichtbaar. Bovendien kunt u het mappictogram (zoals weergegeven in de afbeelding uiterst rechts) selecteren om de mapstructuur weer te geven (een vinkje geeft de map aan die u momenteel in hebt) en eenvoudig terug te navigeren door de mappen door de naam van een map in de boomstructuur te selecteren.

U kunt de muisaanwijzer boven de ⓘ naast een doelgroep houden om informatie over het publiek weer te geven, zoals de id, beschrijving en maphiërarchie, om het publiek te zoeken.

![Een afbeelding die aangeeft hoe de maphiërarchie werkt voor het publiek.](../images/ui/segment-builder/audience-folder-structure.png)

U kunt ook naar soorten publiek zoeken met de zoekbalk, die [Zoeksyntaxis van Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Op de **[!UICONTROL Audiences]** als u een map op hoofdniveau selecteert, wordt de zoekbalk weergegeven, zodat u in die map kunt zoeken. Zoekresultaten beginnen pas te worden gevuld wanneer hele woorden zijn ingevoerd. Als u bijvoorbeeld een publiek wilt zoeken met de naam `Online Shoppers`typt u &quot;Online&quot; in de zoekbalk. Nadat het woord &quot;Online&quot; volledig is getypt, worden zoekresultaten met het woord &quot;Online&quot; weergegeven.

## Rule builder canvas {#rule-builder-canvas}

>[!IMPORTANT]
>
>Vanaf de release van juni 2024 vertegenwoordigen de tijdbeperkingen &quot;Deze maand&quot; en &quot;Dit jaar&quot; respectievelijk &quot;maand-tot-datum&quot; en &quot;jaar-tot-datum&quot;. Als u bijvoorbeeld op 18 juli een publiek hebt gemaakt dat op zoek was naar &quot;alle klanten van wie de verjaardag deze maand plaatsvindt&quot;, krijgt het publiek alle klanten van wie de verjaardagen tussen 1 juli en 31 juli hebben plaatsgevonden. Op 1 augustus, zou dit publiek alle klanten krijgen van wie verjaardag van 1 augustus aan 31 augustus voorkomt.
>
>Eerder vertegenwoordigden &quot;Deze maand&quot; en &quot;dit jaar&quot; respectievelijk 30 dagen en 365 dagen, die geen rekening hielden voor maanden met 31 dagen en schrikkeljaren.
>
>Als u de logica van uw publiek wilt bijwerken, slaat u het eerder gemaakte publiek opnieuw op.

Een segmentdefinitie is een inzameling van regels die worden gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Deze regels worden gecreeerd gebruikend het canvas van de regelbouwer, dat in het centrum van wordt gevestigd [!DNL Segment Builder].

Als u een nieuwe regel wilt toevoegen aan de segmentdefinitie, sleept u een tegel uit de **[!UICONTROL Fields]** en laat vallen het op het canvas van de regelbouwer. Vervolgens krijgt u contextspecifieke opties, afhankelijk van het type gegevens dat u wilt toevoegen. Beschikbare gegevenstypen zijn: tekenreeksen, datums, [!DNL ExperienceEvents], &quot;[!UICONTROL Event Types]&quot;, en het publiek.

![Het lege canvas van de regelbouwer.](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>De meest recente wijzigingen in Adobe Experience Platform hebben het gebruik van de `OR` en `AND` logische operatoren tussen gebeurtenissen. Deze updates zijn niet van invloed op bestaande segmentdefinities. Nochtans, zullen alle verdere updates aan bestaande segmentdefinities en pas gecreëerde segmentdefinities door deze veranderingen worden beïnvloed. Lees de [tijdconstanten bijwerken](./segment-refactoring.md) voor meer informatie .

Wanneer u een waarde voor het kenmerk selecteert, wordt een lijst met opsommingswaarden weergegeven die het kenmerk kan bevatten.

![Een afbeelding die de lijst weergeeft met opsommingswaarden die een kenmerk kan hebben.](../images/ui/segment-builder/enum-list.png)

Als u een waarde in deze lijst met nummers selecteert, krijgt de waarde een effen rand. Voor velden die `meta:enum` (soft) opsommingen, kunt u ook een waarde selecteren die **niet** in de lijst van opsommingen. Als u uw eigen waarde maakt, krijgt deze de omtrek met een gestippelde rand en een waarschuwing dat deze waarde niet in de opsommingslijst voorkomt.

![Een waarschuwing die wordt weergegeven als u een waarde invoegt die geen deel uitmaakt van de opsommingslijst.](../images/ui/segment-builder/enum-warning.png)

Als u meerdere waarden maakt, kunt u deze allemaal tegelijk toevoegen door de bulkupload te gebruiken. Selecteer de ![pluspictogram](../images/ui/segment-builder/plus-icon.png) om de **[!UICONTROL Add values in bulk]** popover.

![Het pluspictogram wordt gemarkeerd en geeft de knop weer die u kunt selecteren voor toegang tot de bulkupload.](../images/ui/segment-builder/add-bulk-values.png)

Op de **[!UICONTROL Add values in bulk]** kunt u een CSV- of TSV-bestand uploaden.

![De waarden voor Toevoegen in de bulkpop-up worden weergegeven. Het dialoogvenster dat u kunt selecteren om een CSV- of TSV-bestand te uploaden, wordt gemarkeerd.](../images/ui/segment-builder/bulk-values-popover.png)

U kunt ook handmatig door komma&#39;s gescheiden waarden toevoegen.

![De waarden voor Toevoegen in de bulkpop-up worden weergegeven. Zowel het dialoogvenster waarin u waarden kunt invoegen als de toegevoegde waarden worden gemarkeerd.](../images/ui/segment-builder/bulk-values-comma-separated.png)

Er zijn maximaal 250 waarden toegestaan. Als u deze hoeveelheid overschrijdt, moet u enkele waarden verwijderen voordat u meer waarden toevoegt.

![Er wordt een waarschuwing weergegeven die aangeeft dat u het maximumaantal waarden hebt bereikt.](../images/ui/segment-builder/maximum-values.png)

### Soorten publiek toevoegen

U kunt een publiek slepen en neerzetten vanuit het deelvenster **[!UICONTROL Audience]** tab op het canvas van de regelbouwer om te verwijzen naar het lidmaatschap van het publiek in de nieuwe segmentdefinitie. Dit staat u toe om publiekslidmaatschap als attribuut in de nieuwe regels van de segmentdefinitie te omvatten of uit te sluiten.

Voor [!DNL Platform] publiek gemaakt met [!DNL Segment Builder], krijgt u de optie om het publiek in de reeks regels om te zetten die in de segmentdefinitie voor dat publiek werden gebruikt. Deze omzetting maakt een exemplaar van de regellogica, die dan kan worden gewijzigd zonder de originele segmentdefinitie te beïnvloeden. Zorg ervoor dat u recente wijzigingen in de segmentdefinitie hebt opgeslagen voordat u deze omzet in regellogica.

>[!NOTE]
>
>Wanneer u een publiek uit een externe bron toevoegt, wordt alleen verwezen naar het publiekslidmaatschap. U kunt het publiek niet in regels omzetten, en daarom kunnen de regels die worden gebruikt om het originele publiek tot stand te brengen niet in de nieuwe segmentdefinitie worden gewijzigd.

![In deze afbeelding ziet u hoe u een publiekskenmerk omzet in regels.](../images/ui/segment-builder/add-audience-to-segment.png)

Als er conflicten optreden wanneer een publiek wordt omgezet in regels, [!DNL Segment Builder] zal proberen de bestaande opties zo goed mogelijk te behouden.

### Codeweergave

U kunt ook een op code gebaseerde versie weergeven van een regel die is gemaakt in het dialoogvenster [!DNL Segment Builder]. Zodra u uw regel binnen het canvas van de regelbouwer hebt gecreeerd, kunt u selecteren **[!UICONTROL Code view]** om uw segmentdefinitie als PQL te zien.

![De knop voor de codeweergave is gemarkeerd, zodat u de segmentdefinitie kunt zien als PQL.](../images/ui/segment-builder/code-view.png)

De mening van de code verstrekt een knoop die u toestaat om de waarde van de segmentdefinitie aan gebruik in API vraag te kopiëren. Om de recentste versie van de segmentdefinitie te krijgen, zorg ervoor u uw recentste veranderingen in de segmentdefinitie hebt bewaard.

![De knop Copy code is gemarkeerd, zodat u ](../images/ui/segment-builder/copy-code.png)

### Samenvoegingsfuncties

Een aggregatie in [!DNL Segment Builder] is een berekening voor een groep XDM-kenmerken waarvan het gegevenstype een getal is (een getal of een geheel getal). De vier gesteunde samenvoegingsfuncties binnen de Bouwer van het Segment zijn SUM, GEMIDDELD, MIN, en MAX.

Als u een aggregatiefunctie wilt maken, selecteert u een gebeurtenis in de linkertrack en voegt u deze in de [!UICONTROL Events] container.

![De sectie Gebeurtenissen wordt gemarkeerd.](../images/ui/segment-builder/events.png)

Nadat u de gebeurtenis in de container Gebeurtenissen hebt geplaatst, selecteert u het pictogram Ovalen (...), gevolgd door **[!UICONTROL Aggregate]**.

![De totale tekst wordt gemarkeerd. Als u dit selecteert, kunt u aggregatiefuncties selecteren.](../images/ui/segment-builder/add-aggregation.png)

De samenvoeging wordt nu toegevoegd. U kunt nu de aggregatiefunctie selecteren, kiezen welk kenmerk wordt geaggregeerd, de gelijkheidsfunctie en de waarde. In het onderstaande voorbeeld zou deze segmentdefinitie elk profiel kwalificeren dat een som aangekochte waarden heeft die groter is dan $100, zelfs als elke afzonderlijke aankoop minder dan $100 is.

![De gebeurtenisregels, die een samenvoegingsfunctie weergeven.](../images/ui/segment-builder/filled-aggregation.png)

### Telfuncties {#count-functions}

De functies van de telling in de Bouwer van het Segment worden gebruikt om gespecificeerde gebeurtenissen te zoeken en het aantal tijden te tellen zij worden gedaan. De gesteunde telfuncties in de Bouwer van het Segment zijn &quot;minstens&quot;, &quot;hoogstens&quot;, &quot;Precies&quot;, &quot;tussen&quot;, en &quot;allen&quot;.

Om een telfunctie tot stand te brengen, selecteer een gebeurtenis van de linkerspoorstaaf en neem het in in [!UICONTROL Events] container.

![De gebeurtenisvelden worden gemarkeerd.](../images/ui/segment-builder/events.png)

Nadat u de gebeurtenis in de gebeurtenissencontainer hebt geplaatst, selecteert u de knop [!UICONTROL At least 1] knop.

![De optie Minstens wordt gemarkeerd en geeft het gebied weer dat moet worden geselecteerd om een volledige lijst met telfuncties weer te geven.](../images/ui/segment-builder/add-count.png)

De telfunctie wordt nu toegevoegd. U kunt nu de telfunctie en de waarde van de functie selecteren. In het onderstaande voorbeeld ziet u hoe u elke gebeurtenis met ten minste één klik opneemt.

![Er wordt een lijst met telfuncties weergegeven en gemarkeerd.](../images/ui/segment-builder/select-count.png)

## Containers

Segmentregels worden geëvalueerd in de volgorde waarin ze worden weergegeven. De containers staan controle over de orde van uitvoering door het gebruik van genestelde vragen toe.

Zodra u minstens één tegel aan het canvas van de regelbouwer hebt toegevoegd, kunt u beginnen om containers toe te voegen. Als u een nieuwe container wilt maken, selecteert u de ovalen (...) in de rechterbovenhoek van het element en selecteert u vervolgens **[!UICONTROL Add container]**.

![De knop voor het toevoegen van containers is gemarkeerd. Hiermee kunt u een container toevoegen als een onderliggend item van de eerste container.](../images/ui/segment-builder/add-container.png)

Een nieuwe container wordt weergegeven als het onderliggende element van de eerste container, maar u kunt de hiërarchie aanpassen door de containers te slepen en te verplaatsen. Het standaardgedrag van een container is &quot;[!UICONTROL Include]&quot; het kenmerk, de gebeurtenis of het publiek dat wordt opgegeven. U kunt de regel instellen op &quot;[!UICONTROL Exclude]&quot;-profielen die voldoen aan de containercriteria door **[!UICONTROL Include]** in de linkerbovenhoek van de tegel en selecteert u &quot;[!UICONTROL Exclude]&quot;.

Een onderliggende container kan ook inline worden geëxtraheerd en toegevoegd aan de bovenliggende container door &quot;container opheffen&quot; te selecteren in de onderliggende container. Selecteer de ellipsen (...) in de hoger-juiste hoek van de kindcontainer om tot deze optie toegang te hebben.

![Opties waarmee u de container kunt opheffen of verwijderen, worden gemarkeerd.](../images/ui/segment-builder/include-exclude.png)

Zodra u **[!UICONTROL Unwrap container]** de onderliggende container wordt verwijderd en de criteria worden inline weergegeven.

>[!NOTE]
>
>Wanneer het unwrapping containers, zorg ervoor dat de logica de gewenste segmentdefinitie blijft ontmoeten.

![De container wordt weergegeven nadat deze is losgekoppeld.](../images/ui/segment-builder/unwrapped-container.png)

## Beleid samenvoegen

>[!CONTEXTUALHELP]
>id="platform_segmentation_createSegment_segmentBuilder_mergePolicies"
>title="Beleid samenvoegen"
>abstract="Met een samenvoegbeleid kunt u verschillende gegevenssets samenvoegen tot uw profiel. Platform heeft een standaardbeleid voor samenvoeging verschaft of u kunt een nieuw standaardbeleid voor samenvoegen maken in profielen. Kies een samenvoegbeleid dat overeenkomt met uw marketingdoel voor dit publiek."

[!DNL Experience Platform] laat u toe om gegevens uit veelvoudige bronnen te brengen en het te combineren om een volledige mening van elk van uw individuele klanten te zien. Bij het samenvoegen van deze gegevens gelden als samenvoegbeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe gegevens voorrang krijgen en welke gegevens worden gecombineerd om een profiel te maken.

U kunt een samenvoegbeleid selecteren dat overeenkomt met uw marketingdoel voor dit publiek of het standaardsamenvoegbeleid gebruiken dat wordt geboden door [!DNL Platform]. U kunt meerdere samenvoegbeleidsregels maken die uniek zijn voor uw organisatie, waaronder het maken van uw eigen standaardbeleid voor samenvoegen. Voor stapsgewijze instructies voor het maken van een samenvoegbeleid voor uw organisatie, moet u eerst de [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md).

Als u een samenvoegbeleid voor uw segmentdefinitie wilt selecteren, selecteert u het tandwielpictogram in het dialoogvenster **[!UICONTROL Fields]** gebruikt u vervolgens de **[!UICONTROL Merge Policy]** vervolgkeuzelijst om het samenvoegbeleid te selecteren dat u wilt gebruiken.

![De kiezer voor het samenvoegbeleid wordt gemarkeerd. Hiermee kunt u kiezen welk samenvoegbeleid moet worden geselecteerd voor uw segmentdefinitie.](../images/ui/segment-builder/merge-policy-selector.png)

## Eigenschappen voor segmentdefinitie {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="Eigenschappen voor segmentdefinitie"
>abstract="In de sectie Eigenschappen van segmentdefinitie wordt een schatting weergegeven van de grootte van de resulterende segmentdefinitie, waarbij het aantal gekwalificeerde profielen wordt weergegeven in vergelijking met het totale aantal profielen. Dit staat u toe om uw segmentdefinitie zonodig aan te passen alvorens het publiek zelf te bouwen."

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="Ramingen vernieuwen"
>abstract="U kunt de ramingen van uw segmentdefinitie verfrissen om onmiddellijk een voorproef van te zien hoeveel profielen voor de voorgestelde segmentdefinitie zouden kwalificeren. De schattingen van het publiek worden geproduceerd door een steekproefgrootte van de steekproefgegevens van die dag te gebruiken."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html#estimate-and-preview-an-audience" text="Een publiek schatten en voorvertonen"

Bij het samenstellen van een segmentdefinitie worden de **[!UICONTROL Audience properties]** aan de rechterkant van de werkruimte wordt een schatting weergegeven van de grootte van de resulterende segmentdefinitie, zodat u de segmentdefinitie naar wens kunt aanpassen voordat u het publiek zelf gaat maken.

**[!UICONTROL Qualified Profiles]** Hiermee wordt de **werkelijk** aantal profielen die de regels van de segmentdefinitie aanpassen. Dit aantal werkt om de 24 uur bij, nadat de baan van de segmentevaluatie is gelopen.

De tijdstempel voor gekwalificeerde profielen geeft de meest recente **partij** segmentevaluatietaak en is **niet** weergegeven voor segmentdefinities die zijn geëvalueerd met behulp van streaming of randsegmentatie. Als u de segmentdefinitie uitgeeft, zal het aantal gekwalificeerde profielen het zelfde blijven tot de volgende baan van de segmentevaluatie in werking wordt gesteld.

**[!UICONTROL Estimated Profiles]** geeft een **benaderen** aantal profielen gebaseerd op **voorbeeldtaak**. U kunt een bijgewerkte versie van deze waarde zien nadat u de nieuwe regels of voorwaarden hebt toegevoegd en **[!UICONTROL Refresh estimate]**. Als u de informatiballon selecteert, krijgt u de foutdrempel en de meest recente tijd van de voorbeeldtaak.

![Gekwalificeerde profielen en geschatte profielen worden gemarkeerd in de sectie Eigenschappen van publiek.](../images/ui/segment-builder/audience-estimates.png)

De **[!UICONTROL Audience properties]** de sectie is ook waar u belangrijke informatie over uw segmentdefinitie, met inbegrip van zijn naam, beschrijving, en evaluatietype kunt specificeren. De definitienamen van het segment worden gebruikt om uw segmentdefinitie onder die te identificeren die door uw organisatie worden bepaald en zouden daarom beschrijvend, beknopt, en uniek moeten zijn.

Terwijl u de segmentdefinitie blijft maken, kunt u een gepagineerde voorvertoning van het publiek weergeven door **[!UICONTROL View Profiles]**.

![De sectie met segmentdefinitie-eigenschappen wordt gemarkeerd. De eigenschappen van de segmentdefinitie omvatten, maar zijn niet beperkt tot, de naam, beschrijving, en evaluatiemethode van de segmentdefinitie.](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>De schattingen van het publiek worden geproduceerd door een steekproefgrootte van de steekproefgegevens van die dag te gebruiken. Als uw profielarchief minder dan 1 miljoen entiteiten bevat, wordt de volledige gegevensset gebruikt; voor 1 tot 20 miljoen entiteiten worden 1 miljoen entiteiten gebruikt; en voor meer dan 20 miljoen entiteiten wordt 5% van de totale entiteiten gebruikt.
>
>Bovendien is deze schatting gebaseerd op het tijdstip waarop de laatste voorbeeldtaak voor het profiel is uitgevoerd. Dit betekent dat als u een relatieve datumfunctie zoals &quot;Vandaag&quot;of &quot;Deze week&quot;gebruikt, de schatting zijn berekeningen van de laatste runtime van de profielsteekproefbaan zal baseren. Als vandaag bijvoorbeeld 24 januari is en de laatste voorbeeldtaak voor het profiel op 22 januari is uitgevoerd, wordt de relatieve datumfunctie &#39;Gisteren&#39; gebaseerd op 21 januari en niet op 23 januari.
>
>Meer informatie over het genereren van schattingen voor segmentdefinities vindt u in de [schatting van generatiesectie](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) van de zelfstudie voor het maken van segmentdefinities.

U kunt ook uw evaluatiemethode selecteren. Als u weet welke evaluatiemethode u wilt gebruiken, kunt u de gewenste evaluatiemethode selecteren of gebruikend dropdown lijst. Als u wilt weten welke evaluatietypen deze segmentdefinitie voor kwalificeert, kunt u het doorbladerpictogram selecteren ![mappictogram met een vergrootglas](../images/ui/segment-builder/segment-evaluation-select-icon.png) om een lijst van de beschikbare evaluatiemethodes van de segmentdefinitie te zien.

De [!UICONTROL Evaluation method eligibility] wordt weergegeven. Deze popover toont de beschikbare evaluatiemethodes, die partij, het stromen, en rand zijn. Uit de pop-up blijkt welke evaluatiemethoden subsidiabel en niet-subsidiabel zijn. Afhankelijk van de parameters u in uw segmentdefinitie gebruikte, kan het niet voor bepaalde evaluatiemethodes kwalificeren. Voor meer informatie over de vereisten voor elke evaluatiemethode, gelieve te lezen [streamingsegmentatie](./streaming-segmentation.md#query-types) of de [randsegmentatie](./edge-segmentation.md#query-types) overzichten.

U kunt de evaluatiemethode van de segmentdefinitie ook veranderen nadat u klaar bent met het creëren van het. Als u de evaluatiemethode wijzigt van Edge of Streaming in Batch, **niet** in staat zijn om deze weer te wijzigen in Edge of Streaming. De wijziging van de evaluatiemethode zal **alleen** van kracht worden zodra u **[!UICONTROL Save]** in de popover. Het dialoogvenster wordt geannuleerd **handhaven** de oorspronkelijke evaluatiemethode.

![Het pop-upvenster Selectie voor de evaluatiemethode wordt weergegeven. Hieruit blijkt welke evaluatiemethoden in aanmerking komen en niet in aanmerking komen voor de segmentdefinitie.](../images/ui/segment-builder/select-evaluation-method.png)

Als u een ongeldige evaluatiemethode selecteert, zult u worden ertoe aangezet om of uw regels van de segmentdefinitie te veranderen of de evaluatiemethode te veranderen.

![De evaluatiemethode pop - op. Als u een niet-subsidiabele evaluatiemethode selecteert, wordt in het pop-upvenster uitgelegd waarom deze niet in aanmerking komt.](../images/ui/segment-builder/ineligible-evaluation-method.png)

Meer informatie over de verschillende evaluatiemethodes van de segmentdefinitie kan in worden gevonden [segmentatieoverzicht](../home.md#evaluate-segments).

## Volgende stappen {#next-steps}

De Bouwer van het segment verstrekt een rijk werkschema toelatend u om verhandelbare doelgroepen van te isoleren [!DNL Real-Time Customer Profile] gegevens. Na het lezen van deze handleiding moet u nu in staat zijn om:

- Maak segmentdefinities met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
- Gebruik het canvas en de containers van de regelbouwer om de orde te controleren waarin de segmentregels worden uitgevoerd.
- De schattingen van de mening van uw potentiële publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
- Schakel alle segmentdefinities in voor geplande segmentatie.
- Hiermee kunt u opgegeven segmentdefinities voor streaming segmentatie inschakelen.

Meer informatie over [!DNL Segmentation Service], kunt u de documentatie blijven lezen en uw kennis aanvullen door de verwante video&#39;s te bekijken. Meer informatie over de andere delen van het dialoogvenster [!DNL Segmentation Service] UI, gelieve te lezen [[!DNL Segmentation Service] gebruikershandleiding](./overview.md)
