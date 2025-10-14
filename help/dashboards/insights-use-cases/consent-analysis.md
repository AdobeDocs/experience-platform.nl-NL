---
title: Constante analyse en tracering
description: Leer hoe u een dashboard voor de toestemmingsanalyse kunt maken om te controleren hoe de toestemming van de gebruiker in de loop der tijd is verlopen.
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 0%

---

# Analyse en reeksspatiëring van toestemming

In het huidige marketinglandschap moet u de voorkeuren voor toestemming van klanten begrijpen en respecteren. Adobe Real-Time Customer Data Platform biedt marketers de mogelijkheid om de toestemming van klanten te analyseren om vertrouwen op te bouwen, privacyregels na te leven en meer persoonlijke ervaringen te bieden.

In dit document wordt beschreven hoe u een toestemmingsdashboard kunt maken voor verschillende gevallen van marketinggebruik voor Real-Time CDP-gegevens. Specifiek, concentreert het zich op hoe te om een publiek met de aangewezen attributen voor uw bedrijfsbehoeften tot stand te brengen, en dan de inzichten te verbruiken door het gebruik van pre-gevormde widgets in Adobe Experience Platform UI. Er wordt ook een alternatieve methode voorgesteld om uw eigen aangepaste widget samen te stellen met de door de gebruiker gedefinieerde dashboardfunctie.

## Gebruiksscenario’s {#use-cases}

De in deze handleiding behandelde gevallen van gebruik zijn het trenderen van de toestemming en het overlappen van de toestemming.

- **Consent trending** volgt hoe de gebruikerstoestemming in tijd is getrand. Het analyseren van toestemmingsvoorkeursveranderingen helpt marketers campagnes te plannen en campagnes uit te voeren die zich aan die veranderingen van de gebruikersvoorkeur aanpassen. U kunt bijvoorbeeld gerichte educatieve campagnes, transparantie- en vertrouwenscampagnes of stimulerende campagnes voor het aansturen van toestemmingskeuzes voeren. U zou ook campagnes kunnen correleren die negatieve gevolgen kunnen hebben gehad voor de toestemming om de frequentie van die campagnes proactief te verminderen.
- **overlap van de Goedkeuring** gebruikt de overlapping onder toestemmingskanalen om verenigbaar gepersonaliseerd overseinen op veelvoudige kanalen voor uw klanten te leveren die met veelvoudige kanalen hebben ingestemd. De verkopers kunnen aan bepaalde kanalen voorrang geven en middelen toewijzen waar een hogere graad van toestemming en gepersonaliseerd overseinen met klanten zou kunnen resoneren en hogere reactieaantallen produceren.

## Goedgekeurd publiek maken {#create-consent-audiences}

Om een toestemmingsdashboard te bouwen, moet u eerst een publiek van alle profielen tot stand brengen die aan contact hebben goedgekeurd. Als u naar de Real-Time Customer Data Platform Segment Builder wilt navigeren, selecteert u **[!UICONTROL Audiences]** in de linkernavigatie van de gebruikersinterface van Experience Platform. Selecteer op het tabblad [!UICONTROL Customer] van het [!UICONTROL Audiences] dashboard **[!UICONTROL Create audience]** in de rechterbovenhoek van de weergave en vervolgens **[!UICONTROL Build rules]** .

![&#x200B; het [!UICONTROL Audiences] dashboard met [!UICONTROL Customer], [!UICONTROL Audiences], en [!UICONTROL Create segment] benadrukte.](../images/insights-use-cases/consent-analysis/create-audience.png)

De Segment Builder wordt weergegeven. Selecteer vervolgens **[!UICONTROL XDM Individual Profile]** uit de beschikbare opties. Zie de documentatie voor meer informatie over het [&#x200B; canvas van de regelbouwer &#x200B;](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![&#x200B; de Bouwer van het Segment met de [!UICONTROL XDM Individual Profile] benadrukte attributenomslag.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Zoek uw toestemmingskenmerken uit de beschikbare opties. Selecteer **[!UICONTROL Consents and Preferences]**.

>[!NOTE]
>
>Als u de toestemming van de gebruiker hebt behouden voor een ander kenmerk dan de door Adobe aanbevolen veldgroep, moet u die kenmerken selecteren in plaats van de hieronder getoonde kenmerken.

Meer informatie kan op de [&#x200B; behandeling van toestemming in segmentatie &#x200B;](../../segmentation/tutorials/consents.md#handling-consent-in-segmentation) documentatie worden gevonden.

![&#x200B; de Bouwer van het Segment met de [!UICONTROL Consent and Preferences] benadrukte attributenomslag.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

De verschillende toestemmings en voorkeursopties worden getoond. Aangezien deze demonstratie zich richt op toestemming om via verschillende marketingkanalen contact te maken, selecteert u **[!UICONTROL Marketing Preferences]** .

![&#x200B; de Bouwer van het Segment met de [!UICONTROL Marketing Preferences] benadrukte omslag.](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

De lijst met marketingvoorkeuren wordt weergegeven. Hoewel in dit voorbeeld gebruik wordt gemaakt van hoofdletters en kleine letters, richt u zich op e-mail, SMS en aanroepen, maar kunt u ook inzichten maken voor elke andere combinatie of voor alle opties. Voer voor elk kanaal de onderstaande stappen uit om een publiek te maken.

Selecteer **[!UICONTROL Receive SMS]** / **[!UICONTROL Receive email]** / **[!UICONTROL Receive calls]** om een publiek te configureren.

![&#x200B; de beschikbare contactkanalen voor marketing worden benadrukt in de publieksbouwer.](../images/insights-use-cases/consent-analysis/channels.png)

De map [!UICONTROL Subscriptions] wordt weergegeven. Selecteer en sleep het kenmerk **[!UICONTROL Choice Value]** vanuit de beschikbare opties naar het middelste venster en selecteer vervolgens de gewenste waarde in het keuzemenu. In dit geval, uitgezochte **ja (opt binnen)**. Geef het publiek vervolgens een naam op basis van uw zakelijke behoeften en geef een gebruikersvriendelijke beschrijving.

>[!NOTE]
>
>Er geldt een zachte limiet voor het aantal soorten publiek dat u kunt maken. De meer informatie kan in de [&#x200B; documentatie van de segmentgidsen &#x200B;](../../profile/guardrails.md#segmentation-guardrails) worden gevonden.

![&#x200B; het [!UICONTROL Choice Value] attribuut met de [!UICONTROL Yes (opt-in)] waarde die in de segmentbouwer wordt benadrukt. De naam en beschrijving van het publiek worden ook benadrukt.](../images/insights-use-cases/consent-analysis/choice-value.png)

Nadat u het vereiste publiek hebt gemaakt, worden deze weergegeven op het tabblad [!UICONTROL Audiences] [!UICONTROL Browse] .

>[!NOTE]
>
>Wanneer u een publiek maakt, moet u wachten tot de batchsegmentatietaak is voltooid voordat de gegevens beschikbaar zijn om uw toestemmingsdashboard te gaan bouwen. De segmentatie van de partij beschrijft het proces om al uw profielgegevens in één keer door uw segmentdefinities te bewegen om het overeenkomstige publiek te veroorzaken. Als u deze doelgroep eenmaal hebt gemaakt, wordt deze opgeslagen en opgeslagen zodat u deze kunt exporteren en gebruiken. De segmenten van de partij worden automatisch geëvalueerd om de 24 uur.

## Inzichten consumeren {#consume-insights}

Adobe heeft verschillende inzichten gemaakt die automatisch voor u beschikbaar zijn in de dashboards Profielen, Soorten publiek en Doelen. Elk publiek dat u maakt, is dan automatisch bruikbaar met deze vooraf geconfigureerde inzichten. Zie de standaardwidgetdocumentatie voor een lijst van de inzichten beschikbaar in [&#x200B; Profielen &#x200B;](../guides/profiles.md#standard-widgets), [&#x200B; Soorten publiek &#x200B;](../guides/audiences.md#standard-widgets), en [&#x200B; Doelen &#x200B;](../guides/destinations.md) dashboards van Doelen.

## Audioverlap {#audience-overlap}

Als u de overlapping tussen twee toestemmingssoorten wilt controleren, voegt u de [!UICONTROL Audience overlap by merge policy] toe aan het dashboard Profielen en selecteert u het gewenste publiek in de vervolgkeuzemenu&#39;s. Zie de documentatie voor instructies op hoe te om een widget aan uw dashboard toe te voegen de [*overlap van het Publiek door beleid van de fusie*](../guides/profiles.md#audience-overlap-by-merge-policy) voor meer informatie over insight.

<!-- Image needs updating to night mode -->

![&#x200B; het dashboard van Profielen met het publiek overlapt door benadrukte widget van het fusiebeleid. De widgetvisulaizes overlapt tussen twee toestemmingspubliek.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

U kunt de overlapping van alle publiek bekijken waar de gebruikers hebben goedgekeurd om vraag over alle andere publiek te ontvangen, met het Publiek overlappend rapport in het Publiek dashboard. Navigeer eerst naar de tab [!UICONTROL Audiences] [!UICONTROL Overview] om de overlapping van het toestemmingspubliek weer te geven. Vanaf dat punt kunt u de [!UICONTROL Audience overlap report] -widget toevoegen aan het dashboard Soorten publiek. Nadat de widget is gemaakt, selecteert u het **[!UICONTROL User consented to calls]** -publiek in het overzicht van het vervolgkeuzemenu voor het publiek boven aan de pagina. Selecteer vervolgens **[!UICONTROL View more]** in de widget Audience overlap rapport om maximaal 50 van de bovenste overlap en maximaal 50 van de minst overeenkomende overlap voor het geselecteerde segment weer te geven.

<!-- Image needs updating to night mode -->

![&#x200B; het dashboard van het publiek met de getoonde het overlappende het rapportwidget van het publiek. De Gebruiker stemde aan vraagpubliek als vergelijkend publiek toe, en de Mening meer verbinding wordt allebei benadrukt.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

Het dialoogvenster Audience overlap in rapporten wordt uitgebreid om extra publiek overlappende gegevens weer te geven.

<!-- Image needs updating to night mode -->

![&#x200B; het publiek overlapt rapport, met de Gebruikers stemden aan benadrukt e-mailpubliek.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Trends voor de omvang van het publiek {#audience-size-trends}

Wanneer u een op toestemming-gebaseerd publiek creeert, ontwikkelt het automatisch tot 12 maanden vanaf de datum u het publiek creeerde. Voor een volledig functionele trend in de toestemming van de klant voegt u de volgende widgets toe aan de pagina [!UICONTROL Segments] [!UICONTROL Overview] . Deze inzichten bieden een krachtig middel om te volgen hoe uw toestemming in de loop der tijd verandert. Ze correleren zelfs met campagnes die je parallel voert en die positieve of negatieve gevolgen kunnen hebben voor de toestemming. De beschrijvingen die voor deze widgets worden aangeboden, zijn van toepassing op een kwestie van het toestemmingsgebruik.

- [&#x200B; trend van de grootte van het publiek &#x200B;](../guides/audiences.md#audience-size-trend): Deze widget biedt een manier aan om te volgen hoe uw respectieve toestemming in tijd is veranderd.
- [&#x200B; trend van de de veranderingsverandering van de grootte van het publiek &#x200B;](../guides/audiences.md#audience-size-change-trend): Deze widget volgt hoe uw klantentoestemming op een dagelijkse basis is veranderd. Bijvoorbeeld, als het aantal van uw klantentoestemming door 100.000 daalde, dan kunt u zien hoe die verandering over een dagelijkse basis voorkwam.
- [&#x200B; trend van de grootte van het publiek door identiteit &#x200B;](../guides/audiences.md#audience-size-trend-by-identity): Met deze widget kunt u volgen hoe uw respectieve toestemming in tijd is veranderd, maar verder gefilterd door een specifieke identiteit zoals e-mail.

<!-- Image needs updating to night mode -->

![&#x200B; het dashboard van het publiek met de de formaattrend van het Publiek, de trend van de grootte van het Publiek door identiteit en de getoonde de de veranderingstrend van de Poortverandering van het Publiek. De gebruikers stemden in met e-mailpubliek wordt gemarkeerd.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Het overzichtdashboard voor soorten publiek {#audiences-overview-dashboard}

Nadat u een publiek met betrekking tot toestemming zoals &quot;Gebruikers met toestemming voor SMS&quot;hebt gecreeerd, kunt u zeer belangrijke gepersonaliseerde toestemmingsinformatie over uw publiek bekijken door de aangewezen widgets aan uw het overzichtdashboard van het Overzicht van Soorten van publiek toe te voegen. Navigeer naar [!UICONTROL Audiences] [!UICONTROL Overview] en voeg de widgets toe die u hebt gekozen in de widgetbibliotheek. Elke widget die aan uw weergave van het dashboard wordt toegevoegd, kan met de functie [!UICONTROL Modify dashboard] worden vergroot of verkleind en verplaatst. Uw gepersonaliseerde mening kan inzichten zoals de trend in tijd (tot 12 maanden), de overlappingen met andere publiek, en de identiteitssamenstelling van het publiek bevatten. Hieronder ziet u een voorbeeldweergave.

![&#x200B; het publiek dashboard met de Gebruikers stemde aan het publiek van SMS toe dat in het globale die publieksdropdown menu wordt benadrukt.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Door gebruiker gedefinieerde dashboards {#usr-defined-dashboards}

U kunt ook uw eigen widgets maken met door de gebruiker gedefinieerde dashboards. Door uw eigen widget te maken hebt u volledige controle over het type widget, samen met de flexibiliteit om filters en nog veel meer rechtstreeks in Adobe Real-Time CDP toe te voegen.

Bijvoorbeeld, als u veelvoudige toestemmingspubliek in de zelfde grafiek wilt trenderen zodat u in tijd kunt zien hoe elk van uw toestemmingsvoorkeur is veranderd. Dit soort visualisatie is mogelijk met door de gebruiker gedefinieerde dashboards in minimale stappen en een eenmalige instelling. Selecteer eerst **[!UICONTROL Dashboards]** in de linkernavigatie. De werkruimte van [!UICONTROL Dashboards] wordt weergegeven. Selecteer vervolgens **[!UICONTROL Create dashboard]** . De volledige instructies op hoe te om [&#x200B; tot een dashboard en douane widget &#x200B;](../standard-dashboards.md) te leiden kunnen in de user-defined dashboardgids worden gevonden.

![&#x200B; de dashboardwerkruimte met benadrukte dashboards en creeer dashboard.](../images/standard-dashboards/create-dashboard.png)

Wanneer u [&#x200B; uw gegevensmodel &#x200B;](../standard-dashboards.md#select-data-model) in widgetcomposer selecteert, selecteer `CDPInsights` gevolgd door **[!UICONTROL Next]**. Het dialoogvenster [!UICONTROL Select table] wordt weergegeven.

![&#x200B; de Uitgezochte dialoog van het gegevensmodel met het getoonde model CDPInsights.](../images/standard-dashboards/select-data-model-dialog.png)

In de volgende weergave wordt een lijst weergegeven met de beschikbare tabellen in de linkertrack. Selecteer `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![&#x200B; de Uitgezochte lijst dialoog met &quot;adwh_fact_profile_by_segment_and_namespace_trendlines&quot;benadrukte lijst.](../images/insights-use-cases/consent-analysis/select-table.png)

Voer de onderstaande stappen uit nadat de widgetcomposer is gevuld met gegevens uit uw gekozen tabel:

- [&#x200B; Onderzoek [!UICONTROL Attributes]](../standard-dashboards.md#add-filter-attributes) voor `[!UICONTROL date]`, dan gebruik + pictogram om het `[!UICONTROL date]` attribuut aan de X-as van het dropdown menu toe te voegen.
  ![&#x200B; Widget composer met toe:voegen-pictogram en dropdown benadrukt menu.](../images/standard-dashboards/attributes-dropdown.png)
- Zoek [!UICONTROL Attributes] naar `[!UICONTROL count_of_profiles]` en gebruik vervolgens het pictogram + om het kenmerk `[!UICONTROL count_of_profiles]` toe te voegen aan de Y-as vanuit het vervolgkeuzemenu.
- Selecteer het pictogram `...` (ellipsen) in het [!UICONTROL Y-axis] veld en selecteer vervolgens de [!UICONTROL SUM] functie voor aggregatie in het vervolgkeuzemenu.
  ![&#x200B; De widget composer stuurt de tendensen van de Toestemming met het gegevensmodel, de lijst, en de y-as dropdown menu en de benadrukte eigenschap van SUM. &#x200B;](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Selecteer het vervolgkeuzemenu [!UICONTROL Marks] en wijzig het diagramtype in [!UICONTROL Line] .
- Zoek [!UICONTROL Attributes] naar `[!UICONTROL segment_name]` en gebruik vervolgens het pictogram + om de `segment_name` als een [!UICONTROL Filter] waarde in het vervolgkeuzemenu toe te voegen. Het dialoogvenster [!UICONTROL Filter: Segment_name] wordt weergegeven. Selecteer de eerder gemaakte soorten publiek die betrekking hebben op toestemming. Selecteer in dit voorbeeld **[!UICONTROL Users Consented to Calls]** , **[!UICONTROL Users Consented to SMS]** en **[!UICONTROL Users Consented to Email]** , gevolgd door **[!UICONTROL Apply]** .
- Zoek [!UICONTROL Attributes] naar `[!UICONTROL segment_name]` en selecteer vervolgens het pictogram + om `segment_name` als een [!UICONTROL Color] toe te voegen in het vervolgkeuzemenu.
- Open [&#x200B; het [!UICONTROL Properties] paneel &#x200B;](../standard-dashboards.md#widget-properties) en verstrek aangewezen [!UICONTROL Widget title] en [!UICONTROL Axis label].
  ![&#x200B; Widget composer met het eigenschappen pictogram en de benadrukte titel van Widget.](../images/standard-dashboards/properties-panel.png)
- Selecteer **[!UICONTROL Save and close]** om uw instellingen te bevestigen.

>[!TIP]
>
>U kunt de widget nu vergroten of verkleinen of naar de gewenste grootte en positie verplaatsen voordat u het dashboard opslaat.


In de onderstaande afbeelding ziet u hoe de voltooide widget er uitziet en andere mogelijke aangepaste inzichten. Voor meer details op de types van widgets die kunnen worden gecreeerd, verwijs naar de [&#x200B; documentatie van het gegevensmodel &#x200B;](../data-models/cdp-insights-data-model-b2c.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![&#x200B; de gebeëindigde widget van de tendensen van de douanetoestemming.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Beleid voor het bijhouden van toestemming {#consent-policies}

De toestemmingsdashboards die u creeert vangen de **distributie van toestemmings en voorkeurattributen slechts**.

>[!NOTE]
>
>Voor klanten van **het Schild van de Gezondheidszorg van Adobe** of **de Privacy &amp; het Schild van de Veiligheid van Adobe**, wijzen deze dashboards **niet** op het volgen van toestemmingsbeleid. Beschikbaar volgen omvat het aantal gecreeerd, toegelaten beleid, en de invloed op publiekslidmaatschap.

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u dashboards kunt maken voor een uitgebreide weergave van uw voorkeuren voor toestemming van klanten met behulp van Real-Time CDP-inzichten. Dit document laat zien hoe Real-Time CDP een robuuste oplossing biedt voor het hedendaagse privacygerichte landschap, waar verzameling, segmentering, analyse en gepersonaliseerde marketingcampagnes op basis van toestemmingsgegevens van cruciaal belang zijn voor marketeers.
