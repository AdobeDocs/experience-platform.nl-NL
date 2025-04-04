---
keywords: Experience Platform;gebruikershandleiding;klantenservice;populaire onderwerpen;instantie configureren;instantie maken;
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Een AI-instantie van een klant configureren
description: AI/ML-services bieden Klantenservice aan als een eenvoudig te gebruiken Adobe Sensei-service die voor verschillende gebruiksgevallen kan worden geconfigureerd. De volgende secties bevatten stappen voor het configureren van een exemplaar van Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2742'
ht-degree: 0%

---


# Een AI-instantie van een klant configureren

AI van de klant, als deel van AI/de Diensten van ML laat u toe om de scores van de douanedichtheid te produceren zonder het moeten zich over machine het leren ongerust maken.

AI/ML-services bieden Klantenservice aan als een eenvoudig te gebruiken Adobe Sensei-service die voor verschillende gebruiksgevallen kan worden geconfigureerd. De volgende secties bevatten stappen voor het configureren van een exemplaar van Customer AI.

## Een instantie maken {#set-up-your-instance}

Selecteer **[!UICONTROL Services]** in de gebruikersinterface van Experience Platform in de linkernavigatie. De browser van **[!UICONTROL Services]** wordt weergegeven en geeft alle beschikbare services weer. Selecteer **[!UICONTROL Open]** in de container voor AI van klant.

![](../images/user-guide/navigate-to-service.png)

De **AI van de Klant** UI verschijnt en toont al uw de dienstinstanties.

- U kunt de metrische waarde van **[!UICONTROL Total profiles scored]** in de bodem-juiste kant van de **[!UICONTROL Create instance]** container vinden. Deze metrische waarde houdt het totale aantal profielen bij dat door de AI van de Klant voor het lopende kalenderjaar wordt genoteerd, met inbegrip van alle zandbakmilieu&#39;s en om het even welke geschrapte de dienstinstanties.

![](../images/user-guide/total-profiles.png)

De instanties van de dienst kunnen worden uitgegeven, worden gekloond, en worden geschrapt door de controles op de rechterkant van UI te gebruiken. Selecteer een instantie in uw bestaande **[!UICONTROL Service instances]** om deze besturingselementen weer te geven. De besturingselementen bevatten het volgende:

- **[!UICONTROL Edit]**: als u **[!UICONTROL Edit]** selecteert, kunt u een bestaande service-instantie wijzigen. U kunt de naam, de beschrijving en de scorefrequentie van de instantie bewerken.
- **[!UICONTROL Clone]**: als u **[!UICONTROL Clone]** selecteert, wordt de momenteel geselecteerde service-instantie gekopieerd. Vervolgens kunt u de workflow wijzigen om kleine tweaks te maken en deze een nieuwe naam te geven.
- **[!UICONTROL Delete]**: U kunt een de dienstinstantie met inbegrip van om het even welke historische looppas schrappen. De corresponderende uitvoergegevensset wordt uit Experience Platform verwijderd. De scores die zijn gesynchroniseerd met Real-Time Klantprofiel worden echter niet verwijderd.
- **[!UICONTROL Data source]**: Een koppeling naar de gegevensset die door dit exemplaar wordt gebruikt. Als de veelvoudige datasets worden gebruikt, opent het selecteren van de hyperlinktekst de datasetvoorproefpopover.
- **[!UICONTROL Last run details]**: dit wordt alleen weergegeven wanneer een uitvoering mislukt. Hier wordt informatie weergegeven over waarom de uitvoering is mislukt, zoals foutcodes.
- **[!UICONTROL Score definition]**: Een kort overzicht van het doel dat u voor deze instantie hebt geconfigureerd.

![](../images/user-guide/service-instance-panel.png)

Selecteer **[!UICONTROL Create instance]** als u een nieuwe instantie wilt maken.

![](../images/user-guide/dashboard.png)

## Instellen

De workflow voor het maken van instanties wordt weergegeven, vanaf de stap **[!UICONTROL Set up]** .

Hieronder vindt u belangrijke informatie over waarden die u aan het exemplaar moet doorgeven:

- **[!UICONTROL Name]:** De naam van de instantie wordt gebruikt op alle plaatsen waar de AI-scores van de Klant worden weergegeven. Namen moeten daarom beschrijven wat de voorspellingsscores vertegenwoordigen. Bijvoorbeeld &#39;Waarschijnlijkheid om tijdschriftabonnement te annuleren&#39;.

- **[!UICONTROL Description]:** een beschrijving die aangeeft wat u probeert te voorspellen.

- **[!UICONTROL Propensity type]:** het type van dichtheid bepaalt de intentie van de score en metrische polariteit. U kunt **[!UICONTROL Churn]** of **[!UICONTROL Conversion]** kiezen. Gelieve te zien de nota onder [ het scoren samenvatting ](./discover-insights.md#scoring-summary) in het ontdekkende inzichten document voor meer informatie over hoe het type van neiging uw instantie beïnvloedt.

![ het scherm van de Opstelling ](../images/user-guide/create-instance.png)

Geef de vereiste waarden op en selecteer vervolgens **[!UICONTROL Next]** om door te gaan.

## Gegevens selecteren {#select-data}

Door het ontwerp gebruikt de AI van de Klant Adobe Analytics, Adobe Audience Manager, Experience Events in het algemeen, en Consumer Experience Event-gegevens om de eigenschapscores te berekenen. Bij het selecteren van een gegevensset worden alleen gegevenssets weergegeven die compatibel zijn met Customer AI. Om een dataset te selecteren, selecteer (**+**) symbool naast de datasetnaam of checkbox selecteren om veelvoudige datasets meteen toe te voegen. Gebruik de onderzoeksoptie om de datasets snel te vinden u in geinteresseerd bent.

![ Uitgezocht en onderzoek naar dataset ](../images/user-guide/configure-dataset-page-save-and-exit-cai.png)

Nadat u de gegevenssets hebt geselecteerd die u wilt gebruiken, selecteert u de knop **[!UICONTROL Add]** om de gegevenssets toe te voegen aan het voorbeeldvenster van de gegevensset.

![ Uitgezochte datasets ](../images/user-guide/select-datasets.png)

Het selecteren van het infopictogram ![ infopictogram ](/help/images/icons/info.png) naast de dataset opent de datasetvoorproefpopover.

![ Uitgezocht en onderzoek naar dataset ](../images/user-guide/dataset-info.png)

De voorproef van de dataset bevat gegevens zoals de laatste updatetijd, bronschema, en een voorproef van de eerste tien kolommen.

Selecteer **[!UICONTROL Save]** om uw concepten op te slaan terwijl u de workflow beweegt. U kunt ook conceptmodelconfiguraties opslaan en naar de volgende stap in de workflow gaan. Gebruik **[!UICONTROL Save and continue]** om concepten te maken en op te slaan tijdens modelconfiguraties. De eigenschap laat u toe om concepten van de modelconfiguratie tot stand te brengen en te bewaren en is bijzonder nuttig wanneer u vele gebieden in het configuratiewerkschema moet bepalen.

![ creeer werkschema van de Klant AI van de Diensten van de Wetenschap van Gegevens met sparen en sparen en blijven benadrukt.](../images/user-guide/cai-save-and-exit.png)

### Volledige gegevensset {#dataset-completeness}

De voorvertoning van de gegevensset bevat een percentage voor het volledigheidspercentage van de gegevensset. Deze waarde verstrekt een snelle momentopname van hoeveel kolommen in uw dataset leeg/ongeldig zijn. Als een dataset veel ontbrekende waarden bevat en deze waarden elders worden vastgelegd, wordt u ten zeerste aangeraden de dataset met de ontbrekende waarden op te nemen. In dit voorbeeld is de persoon-id leeg, maar de persoon-id wordt vastgelegd in een aparte gegevensset die kan worden opgenomen.

>[!NOTE]
>
>De volledigheid van de gegevensset wordt berekend aan de hand van het maximale trainingsvenster voor de AI van de Klant (één jaar). Dit betekent dat gegevens die meer dan een jaar oud zijn, niet in aanmerking worden genomen bij het weergeven van de volledigheidswaarde van de gegevensset.

![ volledigheid van de Dataset ](../images/user-guide/dataset-info-2.png)

### Een identiteit selecteren {#identity}

U kunt zich nu bij veelvoudige datasets aan elkaar aansluiten die op de identiteitskaart (gebied) worden gebaseerd. U moet een identiteitstype (ook wel een naamruimte genoemd) en een identiteitswaarde binnen die naamruimte selecteren. Als u meerdere velden als een identiteit hebt toegewezen binnen uw schema onder dezelfde naamruimte, worden alle toegewezen identiteitswaarden weergegeven in het keuzemenu voor identiteit, dat wordt voorafgegaan door de naamruimte `EMAIL (personalEmail.address)` of `EMAIL (workEmail.address)` .

[zelfde naamruimte selecteren](../images/user-guide/cai-identity-map.png)

>[!IMPORTANT]
>
>Het zelfde identiteitstype (namespace) moet voor elke dataset worden gebruikt u selecteert. Een groen vinkje verschijnt naast het identiteitstype binnen de identiteitskolom erop wijst dat datasets compatibel zijn. Wanneer u bijvoorbeeld de naamruimte Telefoon en `mobilePhone.number` als id gebruikt, moeten alle id&#39;s voor de resterende datasets de naamruimte Telefoon bevatten en gebruiken.

Als u een identiteit wilt selecteren, selecteert u de onderstreepte waarde in de kolom Identiteit. De keuzelijst Selecteer een identiteit wordt weergegeven.

<!-- ![select same namespace](../images/user-guide/identity-type.png) -->
[zelfde naamruimte selecteren](../images/user-guide/cai-identity-namespace.png)

Als er meer dan één identiteit beschikbaar is binnen een naamruimte, selecteert u het juiste identiteitsveld voor uw gebruik. Er zijn bijvoorbeeld twee e-mailidentiteiten beschikbaar binnen de naamruimte van de e-mail, een werk en persoonlijke e-mail. Afhankelijk van het gebruiksgeval, zal een persoonlijke e-mail eerder worden ingevuld en nuttiger in individuele voorspellingen zijn. Dit betekent dat `EMAIL (personalEmail.address)` wordt geselecteerd als de identiteit.

![ niet geselecteerde sleutel van Dataset ](../images/user-guide/select-identity.png)

>[!NOTE]
>
> Als geen geldig identiteitstype (namespace) voor een dataset bestaat, moet u een primaire identiteit plaatsen en het toewijzen aan een identiteit namespace gebruikend de [ schemaredacteur ](../../../xdm/schema/composition.md#identity). Meer over namespaces en identiteiten leren, bezoek de [ namespaces van de Dienst van de Identiteit ](../../../identity-service/features/namespaces.md) documentatie.

## Doel definiëren {#define-a-goal}

<!-- https://www.adobe.com/go/cai-define-a-goal -->

De stap **[!UICONTROL Define goal]** wordt weergegeven en biedt een interactieve omgeving waarin u visueel een voorspellingsdoel kunt definiëren. Een doel bestaat uit een of meer gebeurtenissen, waarbij het voorkomen van elke gebeurtenis is gebaseerd op de voorwaarde die deze bevat. Het doel van een AI-instantie van een klant is na te gaan of het waarschijnlijk is dat het doel binnen een bepaald tijdsbestek wordt bereikt.

Als u een doel wilt maken, selecteert u **[!UICONTROL Enter Field Name]** en volgt u een veld in de vervolgkeuzelijst. Selecteer de tweede invoer, een clausule voor de voorwaarde van de gebeurtenis, dan naar keuze verstrekken de doelwaarde om de gebeurtenis te voltooien. Aanvullende gebeurtenissen kunnen worden geconfigureerd door **[!UICONTROL Add event]** te selecteren. Voltooi ten slotte het doel door een voorspelling in een aantal dagen toe te passen en selecteer vervolgens **[!UICONTROL Next]** .

<!-- ![](../images/user-guide/define-a-goal.png) -->
![](../images/user-guide/cai-define-a-goal.png)

### Wordt uitgevoerd en wordt niet uitgevoerd

Wanneer u het doel definieert, kunt u **[!UICONTROL Will occur]** of **[!UICONTROL Will not occur]** selecteren. Als u **[!UICONTROL Will occur]** selecteert, moet aan de door u gedefinieerde gebeurtenisvoorwaarden worden voldaan voordat de gebeurtenisgegevens van een klant worden opgenomen in de gebruikersinterface voor inzichten.

Bijvoorbeeld, als u opstelling een app zou willen om te voorspellen of een klant een aankoop zal maken, kunt u **[!UICONTROL Will occur]** selecteren dat door **[!UICONTROL All of]** wordt gevolgd en dan **commerce.purchase.id** (of een gelijkaardig gebied) ingaan en **[!UICONTROL exists]** als exploitant.

<!-- ![will occur](../images/user-guide/occur.png) -->
![ zal voorkomen ](../images/user-guide/cai-will-occur.png)

Er kunnen zich echter gevallen voordoen waarin u wilt voorspellen of een gebeurtenis zich niet binnen een bepaald tijdsbestek zal voordoen. Als u een doel wilt configureren met deze optie, selecteert u **[!UICONTROL Will not occur]** in de vervolgkeuzelijst op hoofdniveau.

Als u bijvoorbeeld wilt voorspellen welke klanten zich minder engageren en de aanmeldingspagina van uw account de volgende maand niet meer bezoeken. Selecteer **[!UICONTROL Will not occur]** die door **[!UICONTROL All of]** wordt gevolgd en ga dan **web.webInteraction.URL** (of een gelijkaardig gebied) en **[!UICONTROL equals]** als exploitant met **rekening-login** als waarde in.

![ zal niet voorkomen ](../images/user-guide/not-occur.png)

### Alle

In sommige gevallen wilt u misschien voorspellen of een combinatie van gebeurtenissen zal plaatsvinden en in andere gevallen wilt u mogelijk voorspellen hoe een gebeurtenis zich uit een vooraf gedefinieerde set voordoet. Als u wilt voorspellen of een klant een combinatie van gebeurtenissen zal hebben, selecteert u de optie **[!UICONTROL All of]** in de vervolgkeuzelijst op het tweede niveau op de pagina **[!UICONTROL Define Goal]** .

U kunt bijvoorbeeld voorspellen of een klant een bepaald product koopt. Dit vooruitgangsdoel wordt bepaald door twee voorwaarden: a `commerce.order.purchaseID` **bestaat** en `productListItems.SKU` **evenaart** één of andere specifieke waarde.

![ allen van voorbeeld ](../images/user-guide/all-of.png)

Om te voorspellen of een klant om het even welke gebeurtenis van een bepaalde reeks zal hebben, kunt u de **[!UICONTROL Any of]** optie gebruiken.

U kunt bijvoorbeeld voorspellen of een klant een bepaalde URL of een webpagina met een bepaalde naam bezoekt. Dit vooruitgangsdoel wordt bepaald door twee voorwaarden: `web.webPageDetails.URL` **begint met** een bepaalde waarde en `web.webPageDetails.name` **begint met** een bepaalde waarde.

![ om het even welk van voorbeeld ](../images/user-guide/any-of.png)

### In aanmerking komende populatie *(facultatief)*

Standaard worden voor alle profielen densiteitsscores gegenereerd, tenzij een in aanmerking komende populatie is opgegeven. U kunt een in aanmerking komende populatie opgeven door voorwaarden te definiëren voor het opnemen of uitsluiten van profielen op basis van gebeurtenissen.

![ in aanmerking komende bevolking ](../images/user-guide/eligible-population.png)

### De gebeurtenissen van de douane (*facultatief*) {#custom-events}

Als u extra informatie naast de [ standaardgebeurtenisgebieden ](../data-requirements.md#standard-events) hebt die door Klant AI worden gebruikt om aandrijvingsscores te produceren, wordt een optie van de douanegebeurtenissen verstrekt. Met deze optie kunt u aanvullende gebeurtenissen toevoegen die u van belang acht. Hierdoor kan de kwaliteit van het model verbeteren en kunnen nauwkeurigere resultaten worden verkregen. Als de dataset u selecteerde douanegebeurtenissen omvat die in uw schema worden bepaald, kunt u hen aan uw instantie toevoegen.

>[!NOTE]
>
> Voor een diepgaande verklaring op hoe de het scoren van AI van het effect van douanegebeurtenissen de resultaten van de Klant beïnvloeden, bezoek de [ sectie van het de gebeurtenisvoorbeeld van de Douane ](#custom-event).

![ gebeurteniseigenschap ](../images/user-guide/event-feature.png)

Selecteer **[!UICONTROL Add custom event]** als u een aangepaste gebeurtenis wilt toevoegen. Voer vervolgens een aangepaste naam voor de gebeurtenis in en wijs deze toe aan het gebeurtenisveld in uw schema. Aangepaste gebeurtenisnamen worden weergegeven in plaats van de veldwaarde wanneer wordt gekeken naar invloedrijke factoren en andere inzichten. Dit betekent dat de naam van de aangepaste gebeurtenis wordt gebruikt in plaats van de id/waarde van de gebeurtenis. Voor meer informatie over hoe de douanegebeurtenissen worden getoond, zie de [ sectie van het het voorbeeldvoorbeeld van de douanegebeurtenis ](#custom-event). Deze extra aangepaste gebeurtenissen worden door de AI van de Klant gebruikt om de kwaliteit van uw model te verbeteren en nauwkeurigere resultaten te bieden.

![ gebied van de Gebeurtenis van de Douane ](../images/user-guide/custom-event.png)

Selecteer vervolgens de gewenste operator in de vervolgkeuzelijst met beschikbare operatoren. Alleen operatoren die compatibel zijn met de gebeurtenis worden weergegeven.

![ de exploitant van de Gebeurtenis van de Douane ](../images/user-guide/custom-operator.png)

Voer ten slotte de veldwaarde(n) in als de geselecteerde operator er een nodig heeft. In dit voorbeeld hoeven we alleen maar te kijken of er een hotel- of restaurantreservering bestaat. Als we echter nauwkeuriger willen zijn, kunnen we de equals-operator gebruiken en een exacte waarde invoeren in de value prompt.

![ het gebiedswaarde van de Gebeurtenis van de Douane ](../images/user-guide/custom-value.png)

Selecteer **[!UICONTROL Next]** in de rechterbovenhoek als u wilt doorgaan.

### De profielattributen van de douane (*facultatief*)

U kunt belangrijke de gegevenssetgebieden van het Profiel (met timestamps) in uw gegevens naast de [ standaardgebeurtenisgebieden ](../data-requirements.md#standard-events) bepalen die door Klant AI worden gebruikt om aandrijvingsscores te produceren. Met deze optie kunt u aanvullende profielkenmerken toevoegen die u van belang acht. Hierdoor kan de kwaliteit van het model worden verbeterd en kunnen de resultaten nauwkeuriger worden weergegeven. Bovendien kunnen door het toevoegen van kenmerken voor aangepaste profielen AI van de Klant beter laten zien hoe bepaalde profielen in een eigenschapssemmer zijn terechtgekomen.

>[!NOTE]
>
>Het toevoegen van een attribuut van het Aangepast Profiel volgt het zelfde werkschema zoals het toevoegen van een douanegebeurtenis. Net als aangepaste gebeurtenissen hebben kenmerken van aangepaste profielen hetzelfde effect op de score van uw model. Voor een diepgaande verklaring, bezoek de [ sectie van het de gebeurtenisvoorbeeld van de Douane ](#custom-event).

![ voeg een attribuut van het douaneprofiel ](../images/user-guide/profile-attributes.png) toe

#### Profielkenmerken selecteren in de opname van Profiel exporteren

U kunt er ook voor kiezen om profielkenmerken op te nemen uit de dagelijkse geëxporteerde momentopname van profiel. Deze kenmerken worden gesynchroniseerd met het exporteren van de profielmomentopname en geven de laatst beschikbare waarde weer. Zij verschijnen automatisch en vereisen geen dataset om in de configuratiestap worden geselecteerd.

>[!WARNING]
>
> Selecteer geen profielkenmerk dat is bijgewerkt als resultaat van het voorspellingsdoel of dat sterk is gecorreleerd met het voorspellingsdoel. Dit leidt tot gegevenslekken en overmaat van het model. `total_purchases_in_the_last_3_months` is bijvoorbeeld een kenmerk dat de conversie van aankopen voorspelt.

### Een voorbeeld van een aangepaste gebeurtenis toevoegen {#custom-event}

In het volgende voorbeeld worden een aangepast gebeurtenis- en profielkenmerk toegevoegd aan een Customer AI-instantie. Het doel van de AI-instantie van de klant is te voorspellen hoe waarschijnlijk het is dat een klant in de komende 60 dagen een ander Luma-product zal kopen. Doorgaans zijn productgegevens gekoppeld aan een SKU van het product. In dit geval is de SKU `prd1013` . Nadat het AI-model van de Klant is opgeleid/gecodeerd, kan deze SKU worden gekoppeld aan een gebeurtenis en worden weergegeven als een invloedrijke factor voor een aandrijfsegment.

Klant AI past automatisch eigenschapgeneratie zoals &quot;Dagen toe sinds&quot;of &quot;Tellingen van&quot;tegen douanegebeurtenissen zoals **de aankoop van het Horloge**. Als deze gebeurtenis werd beschouwd als een invloedrijke factor voor de reden waarom klanten een hoge, gemiddelde of lage dichtheid hebben, geeft de AI van de Klant deze weer als `Days since prd1013 purchase` of `Count of prd1013 purchase` . Door deze gebeurtenis als een aangepaste gebeurtenis te maken, kunt u de gebeurtenis een nieuwe naam geven, waardoor de resultaten veel beter leesbaar worden. Bijvoorbeeld `Days since Watch purchase` . Daarnaast gebruikt de AI van de Klant deze gebeurtenis in zijn training en scoring, zelfs als de gebeurtenis geen standaardgebeurtenis is. Dit betekent dat u meerdere gebeurtenissen kunt toevoegen die volgens u van invloed kunnen zijn en uw model verder kunt aanpassen door gegevens zoals reserveringen, bezoekerslogboeken en andere gebeurtenissen op te nemen. Door deze gegevenspunten toe te voegen, vergroot u de nauwkeurigheid en nauwkeurigheid van uw AI-model van de klant.

![ voorbeeld van een douanegebeurtenis ](../images/user-guide/custom-event-name.png)

## Opties instellen

Met de stap Opties instellen kunt u een schema configureren om voorspelling te automatiseren, voorspellingsuitsluitingen definiëren om bepaalde gebeurtenissen te filteren en **[!UICONTROL Profile]** in- en uitschakelen.

### Een schema configureren *(optioneel)* {#configure-a-schedule}

Als u een scoreschema wilt instellen, moet u eerst de **[!UICONTROL Scoring Frequency]** configureren. De geautomatiseerde predikings kunnen worden gepland om of wekelijks of maandelijks te lopen.

![](../images/user-guide/schedule.png)

### Uitsluitingen op voorspelling *(optioneel)*

Als uw dataset kolommen bevatte die als testgegevens werden toegevoegd, kunt u die kolom of gebeurtenis toevoegen aan een uitsluitingslijst door **[!UICONTROL Add Exclusion]** te selecteren gevolgd door het gebied in te gaan u wenst om uit te sluiten. Zo voorkomt u dat gebeurtenissen die aan bepaalde voorwaarden voldoen, worden geëvalueerd wanneer u scores genereert. Deze functie kan worden gebruikt om irrelevante gegevensinvoer of -promoties uit te filteren.

Als u een gebeurtenis wilt uitsluiten, selecteert u **[!UICONTROL Add exclusion]** en definieert u de gebeurtenis. Als u een uitsluiting wilt verwijderen, selecteert u eerst de ovalen (**[!UICONTROL ...]**) rechtsboven in de gebeurteniscontainer en vervolgens **[!UICONTROL Remove Container]** .

![](../images/user-guide/exclusion.png)

### Schakelen tussen profielen

Met de schakeloptie Profiel kan de Klant-AI de resultaten van de scoring exporteren naar het realtime-klantprofiel. Als u deze schakeloptie uitschakelt, worden de resultaten van de modelscoring niet toegevoegd aan Profiel. De resultaten van AI-scoring van de klant zijn nog steeds beschikbaar met deze functie uitgeschakeld.

Wanneer u voor het eerst een AI van de Klant gebruikt, kunt u deze functie uitschakelen totdat u tevreden bent met de resultaten van de modeluitvoer. Dit verhindert u veelvoudige het scoren datasets aan uw Profielen van de Klant te uploaden terwijl het verfijnen van uw model. Zodra u klaar bent met het kalibreren van uw model, kunt u het model klonen gebruikend de [ kloonoptie ](#set-up-your-instance) van de **instanties van de Dienst** pagina. Op deze manier kunt u een kopie van uw model maken en het profiel in- en uitschakelen.

![ knevel van het Profiel ](../images/user-guide/advanced-workflow-save.png)

Wanneer u uw scoreschema hebt ingesteld, hebt u ook voorspellingsuitsluitingen en de profielschakelaar op de gewenste locatie opgenomen, selecteert u **[!UICONTROL Finish]** rechtsboven om uw AI-exemplaar voor de klant te maken.

Als de instantie met succes wordt gecreeerd, wordt een voorspelling onmiddellijk teweeggebracht en de verdere looppas volgens uw bepaald programma uitvoeren.

>[!NOTE]
>
>Afhankelijk van de grootte van de invoergegevens kan het voltooien van de voorspelling 24 uur duren.

Door deze sectie te volgen, hebt u een geval van AI van de Klant gevormd en een voorspelling in werking gesteld. Als de profielschakeloptie is ingeschakeld, worden profielen met ingesneden inzichten automatisch met voorspelde scores gevuld. Wacht tot 24 uur voordat u doorgaat naar de volgende sectie van deze zelfstudie.

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes een exemplaar van de AI van de Klant en geproduceerde bezitsscores gevormd. U kunt nu verkiezen om de bouwer van het Segment te gebruiken [ klantensegmenten met voorspelde scores ](./create-segment.md) tot stand te brengen of [ inzichten met Klant AI ](./discover-insights.md) ontdekken.

## Aanvullende bronnen

De volgende video is ontworpen ter ondersteuning van uw begrip van de configuratieworkflow voor AI van de klant. Daarnaast worden aanbevolen procedures en praktijkvoorbeelden gegeven.

>[!IMPORTANT]
>
> De volgende video is verouderd. Raadpleeg de documentatie voor de meest actuele informatie.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

<!-- comment -->
