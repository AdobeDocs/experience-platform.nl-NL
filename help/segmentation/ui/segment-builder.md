---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;
solution: Experience Platform
title: Gebruikershandleiding voor Segmentatiesegment Builder
topic: ui guide
description: 'De Bouwer van het segment verstrekt een rijke werkruimte die u toestaat om met de gegevenselementen van het Profiel in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen. '
translation-type: tm+mt
source-git-commit: 761a212abc407fac5bc59c6f5a57c6c17c932230
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 0%

---


# [!DNL Segment Builder] UI-hulplijn

[!DNL Segment Builder] biedt een rijke werkruimte waarmee u kunt werken met [!DNL Profile] gegevenselementen. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.

![](../images/ui/segment-builder/segment-builder.png)

## Bouwstenen voor segmentdefinitie

De basisbouwstenen van segmentdefinities zijn attributen en gebeurtenissen. Daarnaast kunnen de kenmerken en gebeurtenissen in bestaande doelgroepen ook worden gebruikt als componenten voor nieuwe definities.

U kunt deze bouwstenen in de sectie van **[!UICONTROL Gebieden]** op de linkerkant van de [!DNL Segment Builder] werkruimte zien. **[!UICONTROL De gebieden]** bevatten een lusje voor elk van de belangrijkste bouwstenen: &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; en &quot;[!UICONTROL Audiences]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Attributen

Op het tabblad **[!UICONTROL Kenmerken]** kunt u door [!DNL Profile] kenmerken bladeren die tot de [!DNL XDM Individual Profile] klasse behoren. Elke map kan worden uitgevouwen om extra kenmerken weer te geven. Elk kenmerk is een tegel die naar het canvas voor regelbuilders in het midden van de werkruimte kan worden gesleept. Het canvas van de [regelbouwer](#rule-builder-canvas) wordt meer in detail besproken later in deze gids.

![](../images/ui/segment-builder/attributes.png)

### Gebeurtenissen

Op het tabblad **[!UICONTROL Gebeurtenissen]** kunt u een publiek maken op basis van gebeurtenissen of acties die hebben plaatsgevonden met behulp van [!DNL XDM ExperienceEvent] gegevenselementen. U kunt gebeurtenistypen ook vinden op het tabblad **[!UICONTROL Gebeurtenissen]** . Dit is een verzameling veelgebruikte gebeurtenissen waarmee u uw segmenten sneller kunt maken.

U kunt niet alleen naar [!DNL ExperienceEvent] elementen bladeren, maar ook naar gebeurtenistypen zoeken. Gebeurtenistypen gebruiken dezelfde coderingslogica als [!DNL ExperienceEvents], zonder dat u door de [!DNL XDM ExperienceEvent] klasse hoeft te zoeken om de juiste gebeurtenis te zoeken. Als u bijvoorbeeld met de zoekbalk zoekt naar &quot;winkelwagentje&quot;, worden de gebeurtenistypen &quot;[!UICONTROL AddCart]&quot; en &quot;[!UICONTROL RemoveCart]&quot; geretourneerd. Dit zijn twee veelgebruikte tekenacties bij het samenstellen van segmentdefinities.

Elk type component kan worden gezocht door zijn naam in de onderzoeksbar te typen, die de onderzoekssyntaxis [van](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene gebruikt. De zoekresultaten beginnen te vullen wanneer hele woorden worden ingevoerd. Als u bijvoorbeeld een regel wilt maken die is gebaseerd op het XDM-veld, `ExperienceEvent.commerce.productViews`typt u &quot;productweergaven&quot; in het zoekveld. Nadat u het woord &quot;product&quot; hebt getypt, worden de zoekresultaten weergegeven. Elk resultaat bevat de objecthiërarchie waartoe het behoort.

>[!NOTE]
>
>De het schemagebieden van de douane die door uw organisatie worden bepaald kunnen tot 24 uren aan verschijnen en beschikbaar voor gebruik in het bouwen van regels vergen.

U kunt dan gemakkelijk slepen en laten vallen [!DNL ExperienceEvents] en &quot;de Types[!UICONTROL van]Gebeurtenis&quot;in uw segmentdefinitie.

![](../images/ui/segment-builder/events-eventTypes.png)

Standaard worden alleen gevulde schemavelden uit de gegevensopslag weergegeven. Dit geldt ook voor &quot;[!UICONTROL gebeurtenistypen]&quot;. Als de lijst &quot;[!UICONTROL Gebeurtenistypen]&quot; niet zichtbaar is of u alleen &quot;[!UICONTROL Willekeurig]&quot; kunt selecteren als &quot;[!UICONTROL Gebeurtenistype]&quot;, selecteert u het **tandwielpictogram** naast **[!UICONTROL Velden]****** **** en selecteert u vervolgens de optie Volledig XDM-schema weergeven onder Beschikbare velden. Selecteer opnieuw het **tandwielpictogram** om naar het lusje van **[!UICONTROL Gebieden]** terug te keren en u zou veelvoudige &quot;Types[!UICONTROL van]Gebeurtenis&quot;en schemagebieden nu moeten kunnen bekijken, ongeacht of zij gegevens bevatten of niet.

![](../images/ui/segment-builder/show-populated.png)

### Doelgroepen

Op het tabblad **[!UICONTROL Soorten publiek]** worden alle soorten publiek weergegeven die zijn geïmporteerd uit externe bronnen, zoals Adobe Audience Manager, en ook het publiek dat binnen is gemaakt [!DNL Experience Platform].

Op het tabblad **[!UICONTROL Soorten publiek]** ziet u alle beschikbare bronnen als een groep mappen. Terwijl u de mappen selecteert, zijn de beschikbare submappen en doelgroepen zichtbaar. Bovendien kunt u het mappictogram (zoals weergegeven in de afbeelding uiterst rechts) selecteren om de mapstructuur weer te geven (een vinkje geeft de map aan die u momenteel in hebt) en eenvoudig terug te navigeren door de mappen door de naam van een map in de boomstructuur te selecteren.

U kunt de muisaanwijzer boven de ⓘ naast een doelgroep houden om informatie over het publiek weer te geven, zoals de id, beschrijving en maphiërarchie, om het publiek te zoeken.

![](../images/ui/segment-builder/audience-folder-structure.png)

U kunt ook naar publiek zoeken met de zoekbalk, die de zoeksyntaxis [van](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene gebruikt. Als u op het tabblad **[!UICONTROL Soorten publiek]** een map op hoofdniveau selecteert, wordt de zoekbalk weergegeven, zodat u in die map kunt zoeken. Zoekresultaten beginnen pas te worden gevuld wanneer hele woorden zijn ingevoerd. Als u bijvoorbeeld een publiek zoekt met de naam `Online Shoppers`, typt u &quot;Online&quot; in de zoekbalk. Nadat het woord &quot;Online&quot; volledig is getypt, worden zoekresultaten met het woord &quot;Online&quot; weergegeven.

## Rule builder canvas {#rule-builder-canvas}

Een segmentdefinitie is een inzameling van regels die worden gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Deze regels worden gecreeerd gebruikend het canvas van de regelbouwer, dat in het centrum van wordt gevestigd [!DNL Segment Builder].

Als u een nieuwe regel wilt toevoegen aan de segmentdefinitie, sleept u een tegel van het tabblad **[!UICONTROL Velden]** en zet u deze neer op het canvas van de regelbuilder. Vervolgens krijgt u contextspecifieke opties, afhankelijk van het type gegevens dat u wilt toevoegen. Beschikbare gegevenstypen zijn: tekenreeksen, datums, [!DNL ExperienceEvents]&#39;[!UICONTROL Gebeurtenistypen]&#39; en doelgroepen.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>De meest recente wijzigingen in Adobe Experience Platform hebben het gebruik van de `OR` en `AND` logische operatoren tussen gebeurtenissen bijgewerkt. Deze updates zijn niet van invloed op bestaande segmenten. Deze wijzigingen zijn echter van invloed op alle volgende updates van bestaande segmenten en nieuwe segmentcreaties. Lees de update [van de](./segment-refactoring.md) tijdconstanten voor meer informatie.

### Soorten publiek toevoegen

U kunt een publiek van het lusje van het **[!UICONTROL Publiek]** op het canvas van de regelbouwer slepen en laten vallen om publiekslidmaatschap in de nieuwe segmentdefinitie te verwijzen. Dit staat u toe om publiekslidmaatschap als attribuut in de nieuwe segmentregel te omvatten of uit te sluiten.

Voor [!DNL Platform] publiek dat gebruikend [!DNL Segment Builder]wordt gecreeerd, wordt u gegeven de optie om het publiek in de reeks regels om te zetten die in de segmentdefinitie voor dat publiek werden gebruikt. Deze omzetting maakt een exemplaar van de regellogica, die dan kan worden gewijzigd zonder de originele segmentdefinitie te beïnvloeden. Zorg ervoor dat u recente wijzigingen in de segmentdefinitie hebt opgeslagen voordat u deze omzet in regellogica.

>[!NOTE]
>
>Wanneer u een publiek uit een externe bron toevoegt, wordt alleen verwezen naar het publiekslidmaatschap. U kunt het publiek niet in regels omzetten, en daarom kunnen de regels die worden gebruikt om het originele publiek tot stand te brengen niet in de nieuwe segmentdefinitie worden gewijzigd.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Als er conflicten optreden wanneer een publiek wordt omgezet in regels, [!DNL Segment Builder] wordt geprobeerd de bestaande opties zo goed mogelijk te behouden.

### Codeweergave

U kunt ook een op code gebaseerde versie weergeven van een regel die in de [!DNL Segment Builder]code is gemaakt. Zodra u uw regel binnen het canvas van de regelbouwer hebt gecreeerd, kunt u de mening **[!UICONTROL van de]** Code selecteren om uw segment als PQL te zien.

![](../images/ui/segment-builder/code-view.png)

De mening van de code verstrekt een knoop die u toestaat om de waarde van het segment in API vraag te kopiëren. Om de recentste versie van het segment te krijgen, zorg ervoor u uw recentste veranderingen in het segment hebt bewaard.

![](../images/ui/segment-builder/copy-code.png)

## Containers

Segmentregels worden geëvalueerd in de volgorde waarin ze worden weergegeven. De containers staan controle over de orde van uitvoering door het gebruik van genestelde vragen toe.

Zodra u minstens één tegel aan het canvas van de regelbouwer hebt toegevoegd, kunt u beginnen om containers toe te voegen. Als u een nieuwe container wilt maken, selecteert u de ovalen (...) in de rechterbovenhoek van de tegel en selecteert u Container **** toevoegen.

![](../images/ui/segment-builder/add-container.png)

Een nieuwe container wordt weergegeven als het onderliggende element van de eerste container, maar u kunt de hiërarchie aanpassen door de containers te slepen en te verplaatsen. Het standaardgedrag van een container is om het kenmerk, de gebeurtenis of het publiek dat wordt geleverd, op te[!UICONTROL nemen]. U kunt de regel instellen op Profielen[!UICONTROL uitsluiten]die voldoen aan de containercriteria door **[!UICONTROL Opnemen]** in de linkerbovenhoek van de tegel te selecteren en &quot;[!UICONTROL Uitsluiten]&quot; te selecteren.

Een onderliggende container kan ook inline worden geëxtraheerd en toegevoegd aan de bovenliggende container door &quot;container opheffen&quot; te selecteren in de onderliggende container. Selecteer de ellipsen (...) in de hoger-juiste hoek van de kindcontainer om tot deze optie toegang te hebben.

![](../images/ui/segment-builder/include-exclude.png)

Nadat u de **[!UICONTROL container]** opheffen hebt geselecteerd, wordt de onderliggende container verwijderd en worden de criteria inline weergegeven.

>[!NOTE]
>
>Wanneer het unwrapping containers, zorg ervoor dat de logica de gewenste segmentdefinitie blijft ontmoeten.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Beleid samenvoegen

[!DNL Experience Platform] laat u toe om gegevens uit veelvoudige bronnen te brengen en het te combineren om een volledige mening van elk van uw individuele klanten te zien. Wanneer het samenbrengen van deze gegevens, is het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om een profiel tot stand te brengen.

U kunt een samenvoegbeleid selecteren dat overeenkomt met uw marketingdoel voor dit publiek of het standaardsamenvoegbeleid gebruiken dat wordt geboden door [!DNL Platform]. U kunt meerdere samenvoegbeleidsregels maken die uniek zijn voor uw organisatie, waaronder het maken van uw eigen standaardbeleid voor samenvoegen. Voor geleidelijke instructies bij het creëren van fusiebeleid voor uw organisatie, te zien gelieve de zelfstudie over het [werken met fusiebeleid gebruikend UI](../../profile/ui/merge-policies.md).

Als u een samenvoegbeleid voor uw segmentdefinitie wilt selecteren, selecteert u het tandwielpictogram op het tabblad **[!UICONTROL Velden]** en selecteert u het samenvoegbeleid **[!UICONTROL dat u wilt gebruiken in het vervolgkeuzemenu]** Samenvoegen.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Segmenteigenschappen

Wanneer het bouwen van een segmentdefinitie, toont de sectie van de Eigenschappen **[!UICONTROL van het]** Segment op de rechterkant van de werkruimte een schatting van de grootte van het resulterende segment, toestaand u om uw segmentdefinitie zonodig aan te passen alvorens het publiek zelf te bouwen.

In de sectie **[!UICONTROL Segmenteigenschappen]** kunt u ook belangrijke informatie over de segmentdefinitie opgeven, zoals de naam en beschrijving. De definitienamen van het segment worden gebruikt om uw segment onder die te identificeren die door uw organisatie worden bepaald en zouden daarom beschrijvend, beknopt, en uniek moeten zijn.

Terwijl u de segmentdefinitie verder ontwikkelt, kunt u een gepagineerde voorvertoning van het publiek weergeven door Profielen **** weergeven te selecteren.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>De schattingen van het publiek worden geproduceerd door een steekproefgrootte van de steekproefgegevens van die dag te gebruiken. Als uw profielarchief minder dan 1 miljoen entiteiten bevat, wordt de volledige gegevensset gebruikt. voor tussen 1 en 20 miljoen entiteiten worden 1 miljoen entiteiten gebruikt; en voor meer dan 20 miljoen entiteiten wordt 5 % van de totale entiteiten gebruikt . Meer informatie over het produceren van segmentramingen kan in de sectie [van de de](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) schattingsproductie van de sectievan de segmentverwezenlijking worden gevonden.

## Volgende stappen en extra bronnen {#next-steps}

De Bouwer van het segment verstrekt een rijk werkschema toelatend u om verhandelbare doelgroepen van [!DNL Real-time Customer Profile] gegevens te isoleren. Na het lezen van deze handleiding moet u nu in staat zijn om:

- Maak segmentdefinities met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
- Gebruik het canvas en de containers van de regelbouwer om de orde te controleren waarin de segmentregels worden uitgevoerd.
- De schattingen van de mening van uw potentiële publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
- Schakel alle segmentdefinities in voor geplande segmentatie.
- Hiermee kunt u opgegeven segmentdefinities voor streaming segmentatie inschakelen.

Voor meer informatie [!DNL Segmentation Service]leest u de documentatie en vult u deze aan door de onderstaande video&#39;s te bekijken. Lees voor meer informatie over de andere onderdelen van de [!DNL Segmentation Service] gebruikersinterface de [[!DNL Segmentation Service] gebruikershandleiding](./overview.md)

>[!WARNING]
>
> De [!DNL Platform] UI die in de volgende video&#39;s wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

**Een segment maken:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**Een dynamisch segment maken:**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)