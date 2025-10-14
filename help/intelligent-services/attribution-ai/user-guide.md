---
keywords: Experience Platform;gebruikershandleiding;attributie ai;populaire onderwerpen;regio
feature: Attribution AI
title: Handleiding voor AI-gebruikersinterface voor kenmerken
description: Dit document fungeert als richtlijn voor interactie met Attribution AI in de Intelligent Services-gebruikersinterface.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2393'
ht-degree: 0%

---

# Handleiding voor AI-gebruikersinterface voor kenmerken

Attribution AI, als onderdeel van Intelligent Services is een meerkanaals, algoritmische attributiedienst die de invloed en incrementele impact van klanteninteractie tegen gespecificeerde resultaten berekent. Met Attribution AI kunnen marketers marketing- en advertentieuitgaven meten en optimaliseren door inzicht te krijgen in de impact van elke afzonderlijke interactie van de klant in elke fase van de reizen van de klant.

Dit document fungeert als richtlijn voor interactie met Attribution AI in de Intelligent Services-gebruikersinterface.

## Een model maken

Selecteer in de gebruikersinterface van [!DNL Adobe Experience Platform] de optie **[!UICONTROL Services]** in de linkernavigatie. De browser **[!UICONTROL Services]** wordt weergegeven en geeft beschikbare intelligente Adobe-services weer. Selecteer **[!UICONTROL Open]** in de container for Attribution AI.

![&#x200B; Toegang hebbend tot uw model &#x200B;](./images/user-guide/open_Attribution_ai.png)

De pagina van de dienst van AI van de Attributie verschijnt. Deze pagina bevat servicemodellen van Attribution AI en geeft informatie over deze modellen, zoals de naam van het model, conversiegebeurtenissen, hoe vaak het model wordt uitgevoerd en de status van de laatste update.

U kunt de metrische waarde van **[!UICONTROL Total conversion events scored]** in de bodem-juiste kant van de **[!UICONTROL Create model]** container vinden. Deze metrische waarde houdt het totale aantal omzettingsgebeurtenissen bij die door Attribution AI voor het huidige kalenderjaar met inbegrip van alle zandbakmilieu&#39;s en om het even welke geschrapte de dienstmodellen worden gescoord.

![&#x200B; totale omzettingen &#x200B;](./images/user-guide/total_conversions.png)

De modellen van de dienst kunnen worden uitgegeven, worden gekloond, en worden geschrapt door de controles op de rechterkant van UI te gebruiken. Selecteer een model in uw bestaande **[!UICONTROL Service models]** om deze besturingselementen weer te geven. De besturingselementen bevatten de volgende informatie:

- **[!UICONTROL Edit]**: als u **[!UICONTROL Edit]** selecteert, kunt u een bestaand servicemodel wijzigen. U kunt de naam, de beschrijving, de status, het scoren frequentie van het model, en de extra kolommen van de scoredataset uitgeven.
- **[!UICONTROL Clone]**: als u **[!UICONTROL Clone]** selecteert, wordt het geselecteerde servicemodel gekopieerd. Vervolgens kunt u de workflow wijzigen om kleine wijzigingen aan te brengen en de naam ervan wijzigen in een nieuw model.
- **[!UICONTROL Delete]**: U kunt een servicemodel verwijderen, inclusief alle historische regels. De corresponderende uitvoergegevensset wordt uit Experience Platform verwijderd. De scores die zijn gesynchroniseerd met Real-Time Klantprofiel worden echter niet verwijderd.
- **[!UICONTROL Data source]**: Een koppeling naar de gegevensset die wordt gebruikt. Als meer dan één dataset door Attribution AI wordt gebruikt, &quot;Veelvoud&quot;die door het aantal datasets wordt gevolgd wordt getoond. Als u de hyperlink selecteert, wordt de voorvertoning van de datasets weergegeven.
- **[!UICONTROL Last run details]**: dit wordt alleen weergegeven wanneer een uitvoering mislukt. Hier wordt informatie weergegeven over waarom de uitvoering is mislukt, zoals foutcodes.

![&#x200B; Kant ruit &#x200B;](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL Conversion events]**: een kort overzicht van de conversiegebeurtenissen die voor dit model zijn geconfigureerd.
- **[!UICONTROL Lookback window]**: Het tijdkader dat u hebt gedefinieerd om aan te geven hoeveel dagen vóór de aanraakpunten voor conversiegebeurtenissen worden opgenomen.
- **[!UICONTROL Touchpoints]**: Een lijst met alle aanraakpunten die u tijdens het maken van dit model hebt gedefinieerd.

![](./images/user-guide/side_panel_2.png)

Selecteer **[!UICONTROL Create model]** om te beginnen.

![&#x200B; creeer model &#x200B;](./images/user-guide/landing_page.png)

Vervolgens wordt de instellingspagina voor Kenmerken AI weergegeven waar u een naam en een optionele beschrijving voor uw servicemodel kunt opgeven.

![&#x200B; noemend een model &#x200B;](./images/user-guide/naming_instance.png)

## Gegevens selecteren {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

Door ontwerp, kan de AI van de Attributie Adobe Analytics, de gebeurtenis van de Ervaring, en de gegevens van de Gebeurtenis van de Consumentenervaring gebruiken om attributiescore te berekenen. Als u een gegevensset selecteert, worden alleen de gegevenssets weergegeven die compatibel zijn met Kenmerk AI. Om een dataset te selecteren, selecteer (**+**) symbool naast de datasetnaam of checkbox selecteren om veelvoudige datasets meteen toe te voegen. U kunt de onderzoeksoptie ook gebruiken om de datasets snel te vinden u in geinteresseerd bent.

Nadat u de gegevenssets hebt geselecteerd die u wilt gebruiken, selecteert u de knop **[!UICONTROL Add]** om de gegevenssets toe te voegen aan het voorbeeldvenster van de gegevensset.

![&#x200B; Uitgezochte datasets &#x200B;](./images/user-guide/select-datasets.png)

Het selecteren van het infopictogram ![&#x200B; infopictogram &#x200B;](/help/images/icons/info.png) naast een dataset opent de datasetvoorproefpopover.

![&#x200B; Uitgezocht en onderzoek naar dataset &#x200B;](./images/user-guide/dataset-preview.png)

De voorproef van de dataset bevat gegevens zoals de laatste updatetijd, bronschema, en een voorproef van de eerste tien kolommen.

Selecteer **[!UICONTROL Save]** om uw concepten op te slaan terwijl u de workflow beweegt. U kunt ook conceptmodelconfiguraties opslaan en naar de volgende stap in de workflow gaan. Gebruik **[!UICONTROL Save and continue]** om concepten te maken en op te slaan tijdens modelconfiguraties. De eigenschap laat u toe om concepten van de modelconfiguratie tot stand te brengen en te bewaren en is bijzonder nuttig wanneer u vele gebieden in het configuratiewerkschema moet bepalen.

![&#x200B; creeer werkschema van de Attributie AI van de Diensten van de Wetenschap van Gegevens lusje met sparen en sparen en blijven benadrukt.](./images/user-guide/aai-save-save-&-exit.png)

### Volledige gegevensset {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

In de voorproef van de dataset is een het percentagewaarde van de volledigheid van de dataset. Deze waarde verstrekt een snelle momentopname van hoeveel kolommen in uw dataset leeg/ongeldig zijn. Als een dataset veel ontbrekende waarden bevat en deze waarden elders worden vastgelegd, wordt u ten zeerste aangeraden de dataset met de ontbrekende waarden op te nemen.

>[!NOTE]
>
>De volledigheid van de gegevensset wordt berekend gebruikend het maximum trainingsvenster voor Attribution AI (één jaar). Dit betekent dat gegevens die meer dan een jaar oud zijn niet in aanmerking worden genomen bij het weergeven van de volledigheidswaarde van de gegevensset.

![&#x200B; volledigheid van de Dataset &#x200B;](./images/user-guide/dataset-completeness.png)

### Een identiteit selecteren {#identity}

U kunt zich nu bij veelvoudige datasets aan elkaar aansluiten die op de identiteitskaart (gebied) worden gebaseerd. U moet een identiteitstype (ook wel een naamruimte genoemd) en een identiteitswaarde binnen die naamruimte selecteren. Als u meerdere velden als een identiteit hebt toegewezen binnen uw schema onder dezelfde naamruimte, worden alle toegewezen identiteitswaarden weergegeven in het keuzemenu voor identiteit, dat wordt voorafgegaan door de naamruimte `EMAIL (personalEmail.address)` of `EMAIL (workEmail.address)` .

>[!IMPORTANT]
>
>Het zelfde identiteitstype (namespace) moet voor elke dataset worden gebruikt u selecteert. Een groen vinkje verschijnt naast het identiteitstype binnen de identiteitskolom erop wijst dat datasets compatibel zijn. Wanneer u bijvoorbeeld de naamruimte Telefoon en `mobilePhone.number` als id gebruikt, moeten alle id&#39;s voor de resterende datasets de naamruimte Telefoon bevatten en gebruiken.

Als u een identiteit wilt selecteren, selecteert u de onderstreepte waarde in de kolom Identiteit. De keuzelijst Selecteer een identiteit wordt weergegeven.

![&#x200B; selecteer zelfde namespace &#x200B;](./images/user-guide/aai-identity-map-save-and-exit.png)

Als er meer dan één identiteit beschikbaar is binnen een naamruimte, selecteert u het juiste identiteitsveld voor uw gebruik. Er zijn bijvoorbeeld twee e-mailidentiteiten beschikbaar binnen de naamruimte van de e-mail, een werk en persoonlijke e-mail. Afhankelijk van het gebruiksgeval, zal een persoonlijke e-mail eerder worden ingevuld en nuttiger in individuele voorspellingen zijn. Dit betekent dat u `EMAIL (personalEmail.address)` selecteert als uw identiteit.

![&#x200B; niet geselecteerde sleutel van Dataset &#x200B;](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> Als geen geldig identiteitstype (namespace) voor een dataset bestaat, moet u een primaire identiteit plaatsen en het toewijzen aan een identiteit namespace gebruikend de [&#x200B; schemaredacteur &#x200B;](../../xdm/schema/composition.md#identity). Meer over namespaces en identiteiten leren, bezoek de [&#x200B; namespaces van de Dienst van de Identiteit &#x200B;](../../identity-service/features/namespaces.md) documentatie.

## Media-kanaal en campagnevelden toewijzen {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

Nadat u het selecteren en het toevoegen van datasets hebt gebeëindigd, verschijnt de **de configuratiestappen van de Kaart**. Kenmerk AI vereist dat u het het kanaalgebied van Media voor elke dataset in kaart brengt u in de vorige stap selecteerde. Dit is omdat zonder de het kanaalafbeelding van Media tussen datasets, kunnen de inzichten die uit Attributie AI worden afgeleid niet behoorlijk tonen makend de inzichten pagina moeilijk te interpreteren maken. Hoewel alleen het Media-kanaal vereist is, wordt u ten zeerste aangeraden een aantal optionele velden zoals Media-actie, Campagnenaam, Campagnegroep en Campagne-tag toe te wijzen. Hierdoor biedt Attribution AI duidelijkere inzichten en optimale resultaten.

![&#x200B; afbeelding &#x200B;](./images/user-guide/mapping-save-&-exit.png)

## Gebeurtenissen definiëren {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

Er zijn drie verschillende typen invoergegevens die worden gebruikt voor het definiëren van gebeurtenissen:

- **de gebeurtenissen van de Omzetting:** Bedrijfs doelstellingen die het effect van marketing activiteiten, zoals, e-commerceorden, in-store aankopen, en websitebezoeken identificeren.
- **venster van de Lookback:** verstrekt een tijdkader erop wijst dat hoeveel dagen voorafgaand aan de omzettingsgebeurtenis touchpoints zouden moeten worden omvat.
- **Touchpoints:** ontvanger, individu, en of op koekjesniveau marketing gebeurtenissen die worden gebruikt om het numerieke of op opbrengst-gebaseerde effect van omzettingen te evalueren.

### Conversiegebeurtenissen definiëren {#define-conversion-events}

Om een omzettingsgebeurtenis te bepalen, moet u de gebeurtenis een naam geven en het gebeurtenistype selecteren door de dataset en het gebied van **te selecteren selecteer een dataset en gebied** dropdown menu.

![&#x200B; ja dropdown &#x200B;](./images/user-guide/define-conversion-events.png)

Zodra een gebeurtenis wordt geselecteerd, verschijnt een nieuw drop-down aan zijn recht. Het tweede vervolgkeuzemenu wordt gebruikt om verdere context aan uw gebeurtenis door het gebruik van verrichtingen te verstrekken. Voor deze omzettingsgebeurtenis, bestaat de standaardverrichting ** wordt gebruikt.

>[!NOTE]
>
>Een koord onder uw *omzetnaam* wordt bijgewerkt aangezien u uw gebeurtenis bepaalt.

![&#x200B; geen dropdown &#x200B;](./images/user-guide/conversion_event_1.png)

Daarna, kunt u een gecombineerde dataset selecteren die door alle inputdatasets in de vorige stap te combineren wordt geproduceerd. Alternatief, kunt u een kolom selecteren die op individuele datasets van **wordt gebaseerd een dataset en gebied** dropdown menu selecteren.

Met de knoppen **[!UICONTROL Add event]** en **[!UICONTROL Add Group]** kunt u de conversie verder definiëren. Afhankelijk van de conversie die u definieert, moet u mogelijk de knoppen **[!UICONTROL Add event]** en **[!UICONTROL Add group]** gebruiken voor verdere context.

![&#x200B; voeg gebeurtenis &#x200B;](./images/user-guide/add_event.png) toe

Als u **[!UICONTROL Add event]** selecteert, worden aanvullende velden gemaakt die met dezelfde methode kunnen worden gevuld als hierboven beschreven. Hiermee voegt u een AND-instructie toe aan de tekenreeksdefinitie onder de conversienaam. Selecteer **x** om een gebeurtenis te verwijderen die is toegevoegd.

![&#x200B; voeg gebeurtenismenu &#x200B;](./images/user-guide/add_event_result.png) toe

Als u **[!UICONTROL Add Group]** selecteert, kunt u extra velden maken die los staan van het origineel. Met de toevoeging van groepen, verschijnt een blauwe *en* knoop. Het selecteren **en** geeft een optie om de parameter te veranderen om &quot;of&quot;te bevatten. &quot;Of&quot; wordt gebruikt om meerdere succesvolle conversiepaden te definiëren. &quot;En&quot; breidt het conversiepad uit om aanvullende voorwaarden op te nemen.

![&#x200B; gebruiken en of &#x200B;](./images/user-guide/and_or.png)

Als u meer dan één omzetting vereist, uitgezochte **voegt omzetting** toe om een nieuwe omzettingstekaart tot stand te brengen. U kunt het bovenstaande proces herhalen om meerdere conversies te definiëren.

![&#x200B; voeg omzetting &#x200B;](./images/user-guide/add_conversion.png) toe

### Opzoekvenster definiëren {#lookback-window}

Nadat u de conversie hebt gedefinieerd, moet u het terugzoekvenster bevestigen. Geef met de pijltoetsen of door de standaardwaarde (56) te selecteren op hoeveel dagen vóór de conversiegebeurtenis u aanraakpunten wilt opnemen. Aanraakpunten worden gedefinieerd in de volgende stap.

![&#x200B; lookback &#x200B;](./images/user-guide/lookback_window.png)

### Aanraakpunten definiëren

Het bepalen van touchpoints volgt een gelijkaardige werkschema aan [&#x200B; bepalend omzettingen &#x200B;](#define-conversion-events). Aanvankelijk moet u uw touchpoint noemen en een touchpoint waarde van *selecteren gaat het drop-down menu van de Naam van het Gebied* binnen. Als deze optie is geselecteerd, wordt het vervolgkeuzemenu met de standaardwaarde &quot;exists&quot; weergegeven. Selecteer de vervolgkeuzelijst om een lijst met operatoren weer te geven.

![&#x200B; exploitanten &#x200B;](./images/user-guide/operators.png)

Voor dit aanraakpunt, selecteert **evenaart**.

![&#x200B; stap 1 &#x200B;](./images/user-guide/touchpoint_step1.png)

Zodra een exploitant voor een touchpoint wordt geselecteerd, *gaat de Waarde van het Gebied* ter beschikking wordt gesteld. De dropdown waarden voor *gaan de Waarde van het Gebied* bevolken die op de exploitant en touchpoint waarde wordt gebaseerd u eerder selecteerde. Als een waarde niet in de vervolgkeuzelijst wordt gevuld, kunt u die waarde handmatig invoeren. Selecteer dropdown en selecteer **KLIK**.

>[!NOTE]
>
>Aan de operatoren &quot;bestaat&quot; en &quot;niet bestaat&quot; zijn geen veldwaarden gekoppeld.

![&#x200B; touchpoint dropdown &#x200B;](./images/user-guide/touchpoint_dropdown.png)

**voegt gebeurtenis** toe en **voegt de knopen van de Groep** toe worden gebruikt om uw touchpoint verder te bepalen. Vanwege de complexe aard van de omringende aanraakpunten is het niet ongebruikelijk om voor één aanraakpunt meerdere gebeurtenissen en groepen te hebben.

Wanneer geselecteerd, **voegt gebeurtenis** toe staat voor extra gebieden toe om worden toegevoegd. Selecteer **x** om een gebeurtenis te verwijderen die is toegevoegd.

![&#x200B; voeg gebeurtenis &#x200B;](./images/user-guide/touchpoint_add_event.png) toe

Het selecteren **voegt groep** toe geeft u de optie om extra gebieden los van origineel tot stand te brengen. Met de toevoeging van groepen, verschijnt een blauwe *en* knoop. Selecteer **en** om de parameter te veranderen, wordt de nieuwe parameter &quot;of&quot;gebruikt om veelvoudige succesvolle wegen te bepalen. Dit specifieke aanraakpunt heeft slechts één succesvol pad, dus &quot;Of&quot; is niet nodig.

![&#x200B; touchpoint overzicht &#x200B;](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Gebruik het koord onder *Naam van het Aanraakpunt* voor een snel overzicht van uw aanraakpunt. De tekenreeks komt overeen met de naam van het aanraakpunt.

![](./images/user-guide/touchpoint_string.png)

U kunt extra touchpoints toevoegen door **te selecteren voeg toe touchpoint** en herhalend het proces hierboven.

![&#x200B; voeg touchpoint toe &#x200B;](./images/user-guide/add_touchpoint.png)

Zodra u klaar bent met het bepalen van alle noodzakelijke aanraakpunten, scrol omhoog en selecteer **daarna** in de hoger-juiste hoek om aan de definitieve stap te werk te gaan.

![&#x200B; gebeëindigd bepaalt &#x200B;](./images/user-guide/define_event_save_and_exit.png)

## Geavanceerde instellingen voor training en scores

De laatste pagina in Attribution AI is de **[!UICONTROL Advanced]** -pagina die wordt gebruikt voor het instellen van training en scoring.

![&#x200B; nieuwe pagina vastgestelde opties &#x200B;](./images/user-guide/advanced_settings_set_options.png)

### Training plannen

Gebruikend het *Programma*, kunt u een dag en een tijd van de week selecteren u het scoren wilt plaatsvinden.

Selecteer dropdown onder *het Schetsen Frequentie* tussen dagelijks, wekelijks, en maandelijks het scoren te selecteren. Selecteer vervolgens de dagen van de week waarop u de scoring wilt toepassen. U kunt meerdere dagen selecteren. Als u dezelfde dag opnieuw selecteert, wordt de selectie opgeheven.

![&#x200B; opleiding van het Programma &#x200B;](./images/user-guide/schedule_training.png)

Selecteer het klokpictogram om de tijd van de dag te wijzigen waarop u wilt scoren. Voer in de nieuwe overlay die wordt weergegeven de tijd in van de dag die u wilt scoren. Selecteer buiten de bedekking om deze te sluiten.

>[!NOTE]
>
>Het kan tot 24 uur duren voor elk scoringsproces wordt voltooid.

![&#x200B; klokpictogram &#x200B;](./images/user-guide/time_of_day.png)

### Aanvullende kolommen met scoregegevens (optioneel)

Door gebrek, wordt een score dataset gecreeerd voor elk de dienstmodel in een standaardschema. U kunt desgewenst extra kolommen toevoegen op basis van uw Conversion-gebeurtenis en aanraakpuntconfiguraties aan de uitvoer van de scoredataset. Begin door kolommen te selecteren uit uw inputdataset, kunt u hen dan slepen en laten vallen om de orde te veranderen door de linkermuisknoop over het hamburgerpictogram te onderdrukken.

![&#x200B; de kolomtoevoeging van de score dataset &#x200B;](./images/user-guide/Add-score-dataset.png)

### Regionaal modelleren (optioneel) {#region-based-modeling-optional}

Het gedrag van uw klanten kan per land en geografische regio aanzienlijk verschillen. Voor globale ondernemingen, die op land-gebaseerde of op regio-gebaseerde modellen gebruiken kan attributienauwkeurigheid verhogen. Elk toegevoegd gebied leidt tot een nieuw model met de gegevens van dat gebied.

Als u een nieuw gebied wilt definiëren, selecteert u eerst **[!UICONTROL Add region]** . Geef in de container die wordt weergegeven een naam voor het gebied op. Slechts één waarde (&quot;placeContext.geo.countryCode&quot;) wordt gevuld vanuit het vervolgkeuzemenu **[!UICONTROL Enter Field Name]** . Selecteer deze waarde.

![&#x200B; Uitgezochte gebied bij &#x200B;](./images/user-guide/select_region_att.png)

Selecteer vervolgens een operator.

![&#x200B; gebiedexploitant &#x200B;](./images/user-guide/region_operators.png)

Typ ten slotte de landcode in de vervolgkeuzelijst **[!UICONTROL Enter Field Value]** .

>[!NOTE]
>
>Landcodes zijn twee tekens lang. Een volledige lijst kan hier [&#x200B; worden gevonden ISO 3166-1 alpha-2 &#x200B;](https://datahub.io/core/country-list).

![&#x200B; gebied &#x200B;](./images/user-guide/region-based.png)

### Trainingsvenster {#training-window}

Om ervoor te zorgen dat u het meest nauwkeurige model mogelijk krijgt, is het belangrijk om uw model te trainen met historische gegevens die uw zaken vertegenwoordigen. Standaard wordt het model getraind met twee kwartalen (zes maanden) aan conversiegebeurtenisgegevens. Selecteer het vervolgkeuzemenu om de standaardinstelling te wijzigen. U kunt kiezen om met één tot vier kwart van gegevens (3-12 maanden) te trainen.

>[!NOTE]
>
>Een korter trainingsvenster is gevoeliger voor recente trends, terwijl een langer trainingsvenster een robuuster model creëert en minder gevoelig is voor recente trends.

![&#x200B; trainingsvenster &#x200B;](./images/user-guide/training_window.png)

Nadat u het trainingsvenster hebt geselecteerd, selecteert u **[!UICONTROL Finish]** in de rechterbovenhoek. Zorg ervoor dat de gegevens enige tijd duren. Na voltooiing, lijkt een popover dialoog bevestigend dat de instantie opstelling volledig is. Selecteer **[!UICONTROL Ok]** om te worden omgeleid naar de **[!UICONTROL Service instances]** -pagina waar u de serviceversie kunt zien.

![&#x200B; volledige opstelling &#x200B;](./images/user-guide/instance_setup_complete.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een service-instantie gemaakt in Attribution AI. Zodra de instantie gebeëindigd het scoren (sta tot 24 uren toe), bent u bereid om de Inzichten van AI van de Attributie [&#128279;](./discover-insights.md) te ontdekken.  Bovendien, als u wenst om uw het sorteren resultaten te downloaden, bezoek de [&#x200B; downloadende scores &#x200B;](./download-scores.md) documentatie.

## Aanvullende bronnen

In de volgende video wordt een end-to-end workflow beschreven voor het maken van een nieuwe instantie in Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
