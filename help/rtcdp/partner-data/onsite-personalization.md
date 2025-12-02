---
title: Onsite ervaringen voor onbekende bezoekers personaliseren met de erkenning van bezoekers met hulp van partners
description: Leer hoe u bezoekerserkenning met ondersteuning van partners kunt gebruiken om uw bezoekers op de site een persoonlijke ervaring te bieden.
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 1%

---

# Onsite ervaringen voor onbekende bezoekers personaliseren met de erkenning van bezoekers met hulp van partners

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten met een licentie voor Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Lees meer over deze pakketten in de [&#x200B; productbeschrijvingen &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions.html) en contacteer uw vertegenwoordiger van Adobe voor meer informatie.

Leer hoe u met partnerondersteunde erkenning persoonlijke ervaringen kunt bieden aan bezoekers van webeigenschappen. Gebruik deze zelfstudie om inzicht te krijgen in de implementatiereeks van verschillende elementen in Experience Platform en andere Experience Cloud-oplossingen en om een persoonlijke ervaring weer te geven voor geverifieerde en niet-geverifieerde bezoekers.

![&#x200B; een infographic die beschrijft hoe te om partner-verstrekte attributen te gebruiken om gepersonaliseerde ervaringen aan uw bezoekers te leveren.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## Waarom dit gebruiksgeval overwegen {#why-this-use-case}

De versnippering van digitale ervaringen als consumenten op allerlei manieren met merken communiceren, is zeer reëel en wordt steeds moeilijker op te lossen. De beste strategieën van de klantenovereenkomst voor samenhangende ervaringen, gerichte aanbevelingen, en op maat-gemaakte interactie worden allen beperkt door gebruikerserkenning.

Dit is waar partnergerichte erkenning in real time een zinvol verschil kan maken. Adobe staat identiteitspartners toe om in ons verfijnde cliënt-zijgegevensinzameling en de markt-leidende aanbiedingen van de ervaringsuitoptimalisering te stoppen, om de bar op ervaringslevering vanaf het eerste bezoek effectief te verhogen, zonder vroegere geschiedenis of authentificatie.

Dit is vooral waardevol aan toppen die lage authentificatiecijfers, zoals de Verpakte Goederen van de Consumenten, online kleinhandel, en meer hebben.

## Voorbeeld van industrie {#industry-example}

Als voorbeeld, overweeg een merk van de huisverbetering dat lage authentificatiecijfers heeft. Dit merk zou gepersonaliseerde ervaringen aan de eerste bezoekers, zonder vroegere geschiedenis of authentificatie, en zonder het vervagen vertrouwen op derdekoekjes willen leveren.

Dit merk kiest ervoor om partnerherkenningstechnologie te gebruiken om de bezoeker waarschijnlijk te herkennen en een meer gepersonaliseerde ervaring te dienen. Dit is handig als de bezoeker de marketing-funnel omlaag beweegt. Het merk kan bijvoorbeeld demografische signalen van partners gebruiken voor on-site content die aantrekkelijk is voor mensen die onlangs zijn verhuisd en die een korting bieden op populaire DIY-producten.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer het van plan zijn om partner-verstrekte attributen te gebruiken om gepersonaliseerde ervaringen aan uw voor authentiek verklaarde en niet voor authentiek verklaarde bezoekers te leveren, overweeg de volgende eerste vereisten in uw planningsproces:

* Welke input wordt verwacht door de herkenningstechnologie van uw partner zodat kunnen zij op extra attributen laag?
* In hoeverre bent u comfortabel om personalisatie op verschillende kanalen en voor verschillende gebruiksgevallen te leveren die op voorwaardelijk afgeleide datasets, tegenover deterministisch bevestigde attributen worden gebaseerd?
* Hoe moet de ervaring van een vooraf geverifieerde maar herkende bezoeker veranderen wanneer ze worden geverifieerd?

### UI-functionaliteit, Experience Platform-componenten en Experience Cloud-producten die u wilt gebruiken {#ui-functionality-and-elements}

Als u dit geval wilt gebruiken, moet u meerdere gebieden van Real-Time Customer Data Platform en andere Experience Cloud-oplossingen gebruiken. Zorg ervoor dat u de noodzakelijke [&#x200B; op attributen-gebaseerde toegangsbeheertoestemmingen &#x200B;](/help/access-control/abac/overview.md) voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* Dataverzameling
   * [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md)
   * [Tags](/help/tags/home.md)
   * [Gegevensstromen](/help/datastreams/overview.md)
* Gegevensbeheer in Real-Time CDP
   * [Identiteiten](/help/identity-service/features/namespaces.md)
   * [Schema&#39;s](/help/xdm/home.md)
   * [Labels voor gegevensgebruik](/help/data-governance/labels/overview.md)
   * [Gegevenssets](/help/catalog/datasets/overview.md)
* Webeigenschappen aanpassen
   * [Edge-segmentatie](/help/segmentation/methods/edge-segmentation.md)
   * [Edge Personalization-bestemmingen](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [&#x200B; Adobe Target &#x200B;](/help/destinations/catalog/personalization/adobe-target-connection.md) (of een verpersoonlijkingsplatform van uw keus. In deze zelfstudie wordt Adobe Target gemarkeerd als een personalisatie-engine.

## Video doorloopt {#video-walkthrough}

Bekijk de videozelfstudie hieronder voor een analyse van hoe u onsite ervaringen kunt personaliseren voor onbekende bezoekers:

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

![&#x200B; een infographic die beschrijft hoe te om partner-verstrekte attributen te gebruiken om gepersonaliseerde ervaringen aan uw bezoekers te leveren.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Als a **klant**, vergunning u van de **gegevenspartner** de capaciteit om inzichten in real time op anders anonieme websitebezoekers te halen.
2. Als a **klant**, stelt u cliënt-zijbibliotheken op uw eigenschappen op om **partner** APIs te roepen en u vormt SDK van het Web of Mobiele SDK om partner-Geleide signalen naar Real-Time CDP te verzenden.
3. Wanneer het doorbladeren van uw website of app, wordt de **bezoeker** waarschijnlijk erkend door de **partner**, die attributen samen met een identiteitskaart terugkeert.
4. Real-Time CDP stelt randsegmentatie in werking om inkomende gebeurtenisklappen te evalueren en handhaaft resultaten tegen het [&#x200B; ECID herkenningsteken &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL).
5. Adobe Target gebruikt de uitvoer van de randsegmentatie om de ervaring terug naar de **bezoeker** voor in-zittingsverpersoonlijking terug te geven.
6. De gebeurtenis wordt in zijn geheel voor stroomafwaartse werkschema&#39;s zoals analyse en heroriëntering voortgezet.

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien.

### Gegevensbeheer - Maak een naamruimte, schema en gegevensset voor identiteiten om gegevenskenmerken te beheren {#data-management}

Voordat u het gebruiksgeval kunt gebruiken om de ervaring van niet-geregistreerde bezoekers te personaliseren, moet u eerst de gegevensbeheerstructuur in Real-Time CDP instellen om de inkomende real-time gegevens over gebeurtenissen en publiekskwalificaties te ontvangen.

#### Identiteitsnaamruimte van partner-id maken

Eerst, moet u een identiteitsnaamruimte van partnerIdentiteit tot stand brengen. Navigeer naar **[!UICONTROL Customer]** > **[!UICONTROL Identities]** in de linkertrack en selecteer vervolgens **[!UICONTROL Create identity namespace]** in de rechterbovenhoek van het scherm.

![&#x200B; Create de dialoog van identiteitskaart namespace met benadrukte partneridentiteitskaart.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Lees meer over hoe te [&#x200B; tot een identiteit van partneridentiteitskaart te leiden namespace &#x200B;](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Een schema maken

Maak vervolgens een [!UICONTROL Experience Event] -schema voor de tijdreeksgegevens die u later wilt verzamelen van uw wegeigenschappen en gebruik [!UICONTROL XDM ExperienceEvent] als basisklasse voor het schema. Lees over hoe te [&#x200B; een schema creëren gebruikend Experience Platform UI &#x200B;](/help/xdm/ui/resources/schemas.md#create).

![&#x200B; de werkruimte van Schema&#39;s met Create schema, en de benadrukte gebeurtenis van de Ervaring XDM.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Aangezien u uw schema creeert en [&#x200B; gebiedsgroepen aan uw schema &#x200B;](/help/xdm/ui/resources/schemas.md#add-field-groups) toevoegt, denk na toevoegend de [&#x200B; Web-pagina van het Bezoek &#x200B;](/help/xdm/field-groups/event/web-details.md) en [&#x200B; Identiteitskaart &#x200B;](/help/xdm/field-groups/profile/identitymap.md) gebiedsgroepen. Dit is een aanvulling op andere veldgroepen die van toepassing zijn op uw digitale eigenschap en praktijken van de gegevensinzameling.

Bovendien, kunt u een bestaande gebiedsgroep tot stand brengen of hergebruiken en het toevoegen aan uw schema, om partner-verstrekte inzichten over de bezoeker te vangen. Lees hoe te [&#x200B; om een gebiedsgroep &#x200B;](/help/xdm/ui/resources/field-groups.md) tot stand te brengen en hoe te [&#x200B; gebieden &#x200B;](/help/xdm/ui/resources/field-groups.md) aan de gebiedsgroep toevoegen. Als u bijvoorbeeld verwacht te personaliseren tegen door partners verschafte inzichten zoals leeftijd, werkgelegenheidsstatus, macht voor maandelijkse uitgaven of gedrag, moet u uw veldgroep geschikte velden laten opnemen.

Ervan uitgaande dat de gegevenspartner een stabiele id voor de bezoeker verstrekt en u dat in Real-Time CDP wilt brengen, zeker ben om een geschikt genoemd gebied voor het herkenningsteken in uw groep van het douanegebied te hebben. U moet het veld ook als een identiteit markeren in de naamruimte die u eerder hebt gemaakt. Herinner me ook om [&#x200B; toe te laten om het schema in Profiel &#x200B;](/help/xdm/ui/resources/schemas.md#profile) worden omvat.

#### Een gegevensset maken

Daarna, moet u een dataset tot stand brengen om de tijd-reeksgegevens te houden die u van uw bezoekers van het Web bezit verzamelt en die u voor onsite verpersoonlijking zult gebruiken.

Lees het leerprogramma op [&#x200B; hoe te om een dataset &#x200B;](/help/catalog/datasets/user-guide.md#create) tot stand te brengen en te herinneren om de optie te selecteren om de dataset van een schema tot stand te brengen. Creeer de dataset die op het schema wordt gebaseerd dat u in de vorige stap creeerde.

Net als bij de stap bij het maken van een schema moet u ervoor zorgen dat de gegevensset wordt opgenomen in de [!UICONTROL Real-Time Customer Profile] . Voor meer informatie over het toelaten van de dataset voor gebruik in [!UICONTROL Real-Time Customer Profile], leest [&#x200B; schema tot leerprogramma.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Verzameling van gebeurtenisgegevens implementeren in uw webeigenschap {#implement-data-collection}

Na vestiging moet uw configuratie van het gegevensbeheer, u nu gebeurtenis in real time [&#x200B; gegevensinzameling &#x200B;](/help/collection/home.md) op uw Webbezit uitvoeren. U moet de Adobe-bibliotheek voor gegevensverzameling ( [!UICONTROL Web SDK] ) gebruiken om realtime-gebeurtenisaanroepen te verzamelen en deze terug te sturen naar Real-Time CDP. Dit item bestaat uit een paar afzonderlijke taken voor een paar componenten van gegevensverzameling.

>[!IMPORTANT]
>
>Om partner-verstrekte attributen terug te winnen, moet u uw Webbezit met partner APIs of andere methodes ook *integreren om attributen van gegevenspartners in real time* te roepen en terug te winnen. Bespreek dit aspect met uw partner van keuze, omdat het niet onderwerp is van deze zelfstudie.

Gebruik eerst de toepassingsschakeloptie rechtsboven in het scherm om naar de sectie **[!UICONTROL Data Collection]** te navigeren.

>[!TIP]
>
>Neem contact op met de systeembeheerder om toegang te vragen als u [!UICONTROL Data Collection] niet kunt zien in de toepassingsschakelaar.

![&#x200B; App schakelaar om aan de sectie van de Inzameling van Gegevens te krijgen.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

Het gedeelte **[!UICONTROL Data Collection]** van de gebruikersinterface ziet er ongeveer zo uit als de onderstaande afbeelding.

![&#x200B; sectie van de inzameling van Gegevens van Experience Platform UI.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Gegevensstroom maken

Als eerste stap in de sectie van de gegevensinzameling, [&#x200B; creeer een nieuwe datastream &#x200B;](/help/datastreams/configure.md). De gegevensstroom vormt de basis voor de manier waarop gegevens worden verzameld en correct worden gerouteerd naar de juiste Adobe-app, in dit geval Experience Platform.

Terwijl u de gegevensstroom maakt, selecteert u in het veld **[!UICONTROL Event schema]** het schema dat u eerder hebt gemaakt.

![&#x200B; benadrukte het schemaselector van de Gebeurtenis wanneer het vormen van een nieuwe gegevensstroom.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[&#x200B; selecteer de gebeurtenisdataset &#x200B;](/help/datastreams/configure.md#aep) die u vroeger van dropdown creeerde, controleer de vakjes naast **[!UICONTROL Edge Segmentation]** en **[!UICONTROL Personalization Destinations]**, en selecteer **[!UICONTROL Save]**.

Merk op dat u geen profieldataset in dit scenario moet selecteren aangezien u in op gebeurtenis-gebaseerde tijdreeksgegevens brengt.

#### Tag-eigenschap maken

Beschouw een eigenschap als een container die u vult met extensies, regels, gegevenselementen en bibliotheken wanneer u tags op uw site implementeert.

Ga naar **[!UICONTROL Tags]** en selecteer **[!UICONTROL New property]** .

![&#x200B; creeer een nieuw markeringsbezit.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Vul de vereiste velden in en selecteer **[!UICONTROL Save]** .

![&#x200B; Vul vereiste gebieden voor uw nieuw bezit in.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Krijg volledige informatie over hoe te [&#x200B; tot een markeringsbezit &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=nl-NL) leiden.

Vervolgens moet u verschillende extensies installeren in de eigenschap. Selecteer de eigenschap tag en ga naar de sectie [!UICONTROL Extensions] .

![&#x200B; selecteer uw nieuw markeringsbezit.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

De extensie [!UICONTROL Core] is al geïnstalleerd. U moet nog twee extensies installeren, zoals in de volgende secties wordt beschreven.

![&#x200B; Mening geïnstalleerde uitbreidingen.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Web SDK-extensie installeren

In deze zelfstudie wordt aangegeven hoe u uw website kunt besturen met Web SDK. U kunt [&#x200B; Mobiele SDK &#x200B;](https://developer.adobe.com/client-sdks/documentation/) op uw app ook gebruiken om de ervaring aan uw toepassingsbezoekers te personaliseren.

![&#x200B; Mening van de uitbreiding van SDK van het Web in de uitbreidingscatalogus.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Navigeer in het scherm om Web SDK te configureren naar de sectie **[!UICONTROL Datastreams]** en geef informatie over de Experience Platform-sandbox die u gebruikt. Selecteer de desbetreffende sandbox en de gegevensstroom die u in de vorige stappen van de volgende vervolgkeuzelijst hebt gemaakt. U kunt dezelfde sandbox- en gegevensstroomwaarden kiezen voor alle andere omgevingen. Laat de andere instellingen ongewijzigd en selecteer **[!UICONTROL Save]** .

Krijg volledige informatie over [&#x200B; hoe te om het Web SDK &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html?lang=nl-NL) te installeren.

#### ID-serviceversie installeren

Gebruik de [&#x200B; uitbreiding van de Dienst van identiteitskaart van Experience Cloud &#x200B;](/help/tags/extensions/client/id-service/overview.md) om een unieke op apparaat-gebaseerde eerste-partijidentiteit voor bezoekers over alle oplossingen van Experience Cloud tot stand te brengen. Zoek naar **[!UICONTROL ID Service]** in de extensiecatalogus en installeer deze. Houd alle standaardinstellingen wanneer u de extensie installeert.

![&#x200B; Mening van de uitbreiding van de Dienst van identiteitskaart in de uitbreidingscatalogus.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Omgevingen instellen

Ga vervolgens over naar de sectie **[!UICONTROL Environments]** van de linkernavigatie. In deze stap moet u uw website verbinden met het Adobe Edge-netwerk om bezoekersinformatie in real-time op te halen en te leveren.

Selecteer het vakpictogram rechts voor de ontwikkelomgeving en kopieer de standaardversie van het JavaScript-codefragment dat in een modaal venster wordt weergegeven.

![&#x200B; Uitgezochte vakje pictogram dat in de sectie van Milieu&#39;s van UI van de Inzameling van Gegevens wordt benadrukt.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

U moet dit codefragment helemaal boven aan uw website toevoegen. Als gevolg hiervan belt uw website naar Adobe Edge Network om JavaScript-logica op te halen die op de pagina wordt geladen en uitgevoerd. Dit staat voor functionaliteit zoals de generatie van bezoekersidentiteitskaart, gegevensinzameling, en de ervarings in real time verpersoonlijking toe om te werken.

#### Gegevenselementen instellen

Gegevenselementen zijn de bouwstenen voor uw gegevenswoordenboek (of gegevenskaart). Eén gegevenselement is een variabele waarvan de waarde kan worden toegewezen aan querytekenreeksen, URL&#39;s, cookie-waarden, JavaScript-variabelen enzovoort. Lees meer over [&#x200B; gegevenselementen &#x200B;](/help/tags/ui/managing-resources/data-elements.md).

In dit geval moet u twee gegevenselementen instellen.

Stel eerst een `partnerData` -element in. Navigeer naar de sectie **[!UICONTROL Data Elements]** en selecteer **[!UICONTROL Create New Data Element]** .

![&#x200B; creeer een nieuw gegevenselement.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Geef het gegevenselement een naam `partnerData` , laat de [!UICONTROL extension] waarde als [!UICONTROL Core] en stel **[!UICONTROL Data Element Type]** in als **[!UICONTROL JavaScript Variable]** . Typ `partnerData` in het veld met de naam **[!UICONTROL JavaScript variable name]** en selecteer **[!UICONTROL Save]** .

![&#x200B; Gemarkeerde selecties om het partnerData gegevenselement correct te vormen.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Als u het tweede gegevenselement wilt instellen, geeft u de nieuwe variabele `pageVisit` een naam, stelt u de variabele **[!UICONTROL Extension]** in op **[!UICONTROL Adobe Experience Platform]** en kiest u **[!UICONTROL XDM Object]** als gegevenstype.

![&#x200B; Gemarkeerde selecties om het pageVisit gegevenselement correct te vormen.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Van het schema, selecteer de derdeattributen die aan de waarden beantwoorden die u van de gegevenspartner verwacht. Selecteer vervolgens het keuzerondje met de naam **[!UICONTROL Provide entire object]** . Selecteer het pictogram dat er als een database uitziet en kies het gegevenselement `partnerData` dat u eerder hebt gemaakt.

#### Regels instellen

In de sectie **[!UICONTROL Rules]** kunt u uw website zo configureren dat deze een aanvraag voor een personalisatie naar Adobe verzendt met de kenmerken die zijn geladen in de gegevenselementen die u zojuist hebt gemaakt. Lees meer over [&#x200B; het creëren van regels &#x200B;](/help/tags/ui/managing-resources/rules.md).

Selecteer **[!UICONTROL Create new Rule]**. Noem deze regel **[!UICONTROL Personalize]** en selecteer + teken naast **[!UICONTROL Events]**. Selecteer **[!UICONTROL Page Bottom]** als de gebeurtenis en sla deze op.

![&#x200B; Selecties voor het gebeurtenistype deel van een regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Selecteer het plusteken (+) naast **[!UICONTROL Actions]** . Werk de extensie bij naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stel **[!UICONTROL Action Type]** in op **[!UICONTROL Send event]** .

![&#x200B; Selecties voor het actietype deel van een regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Selecteer **[!UICONTROL Type]** als gebeurtenistype in de `web.webpagedetails.pageViews` -vervolgkeuzelijst aan de rechterkant.

![&#x200B; Uitgezochte gebeurtenistype.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Selecteer het databasepictogram naast XDM-gegevens en selecteer het gegevenselement `pageVisit` .

Blader omlaag in de lijst met actieconfiguraties en controleer het selectievakje **[!UICONTROL Render visual personalization decisions]** . Dit is belangrijk om ervoor te zorgen dat ervaringen die via Adobe Target of andere vergelijkbare producten worden geleverd, visueel op de webpagina worden weergegeven. Selecteer **[!UICONTROL Keep Changes]** en **[!UICONTROL Save]** de regel.

![&#x200B; uitgezocht geef visuele verpersoonlijkingsbesluiten checkbox terug.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Publicatieworkflow instellen

Als u deze configuratie op de webpagina wilt implementeren, moet u eerst een bibliotheek maken die de bronnen bevat die u zojuist hebt gemaakt. Lees meer over [&#x200B; vestiging een het publiceren stroom &#x200B;](/help/tags/ui/publishing/publishing-flow.md).

Selecteer **[!UICONTROL Publishing Flow]** en vervolgens **[!UICONTROL Add Library]** .

Selecteer **[!UICONTROL Add all Changed Resources]** , geef de bibliotheek een naam, stel de omgeving in op **[!UICONTROL Development]** en selecteer **[!UICONTROL Save & Build to Development]** .

![&#x200B; creeer bibliotheek en stel aan ontwikkelomgeving &#x200B;](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif) op

#### Uw website testen

Op dit moment moet uw website volledig van instrumenten zijn voorzien met Web SDK. Om te testen dat de gegevensinzameling zoals verwacht werkt, kunt u aan uw website navigeren en de ontwikkelaarshulpmiddelen van uw browser gebruiken om netwerkverkeer te inspecteren.

Voer `interact` in het zoekvak in, vernieuw de pagina en u ziet netwerkaanroepen van uw website naar het Adobe Edge-netwerk dat gevuld is.

![&#x200B; Mening van netwerkgebeurtenissen die in ontwikkelaarshulpmiddelen bevolken.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalisatie {#personalization}

U bent nu klaar om publiek voor verpersoonlijking tot stand te brengen en te activeren.

#### Het publiek maken en segmentatie van randen instellen

Navigeer in de gebruikersinterface van Experience Platform naar **[!UICONTROL Customer]** > **[!UICONTROL Audiences]** en maak een publiek om uw websitebezoekers vast te leggen.

![&#x200B; Mening van hoe te aan publiek te navigeren.](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

U moet opstelling uw publiek met [&#x200B; randsegmentatie &#x200B;](/help/segmentation/methods/edge-segmentation.md) zodat wordt het publieksenlidmaatschap van uw bezoekers geëvalueerd in real time, aangezien zij uw Webbezit bezoeken.

Zorg ervoor aan opstelling ook een [&#x200B; actief-op-rand samenvoegbeleid &#x200B;](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) voor het randpubliek.

#### Integreren met Adobe Target of een andere aangepaste personalisatiebestemming

U kunt nu integreren met een aanpassingsengine om persoonlijke inhoud weer te geven voor uw website of app-bezoekers. Adobe adviseert het gebruiken van de [&#x200B; bestemming van Adobe Target &#x200B;](/help/destinations/catalog/personalization/adobe-target-connection.md) voor dit doel.

>[!IMPORTANT]
>
>Lees het leerprogramma op [&#x200B; activerend publiek aan de bestemmingen van de randverpersoonlijking &#x200B;](/help/destinations/ui/activate-edge-personalization-destinations.md) voor een volledige mening van stappen noodzakelijk om uw publiek te activeren.

## Beperkingen en problemen oplossen {#limitations-and-troubleshooting}

Houd rekening met de volgende beperkingen wanneer u het op deze pagina beschreven gebruiksgeval bekijkt:

* Als u Partner IDs gebruikt, ben zich ervan bewust dat deze IDs niet wanneer het bouwen van uw [&#x200B; identiteitsgrafiek &#x200B;](/help/identity-service/features/identity-graph-viewer.md) wordt gebruikt.

## Andere gebruiksgevallen die worden bereikt via ondersteuning van partnergegevens {#other-use-cases}

Verken verdere gebruiksgevallen die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

* [&#x200B; Supplement eerste-partijprofielen met attributen van vertrouwde op gegevenspartners &#x200B;](/help/rtcdp/partner-data/supplement-first-party-profiles.md) om uw gegevensstichting te verbeteren en nieuwe inzichten in uw klantenbasis te verkrijgen en betere publieksoptimalisering te bereiken.
* De steun van de derdegegevens van het gebruik in Real-Time CDP om [&#x200B; uw profielbasis met perspectiefprofielen van gegevenspartners uit te breiden en met hen in gesprek te gaan om nieuwe klanten &#x200B;](/help/rtcdp/partner-data/prospecting.md) te verwerven of te bereiken.
* [&#x200B; Uitgebreide activering van perspectiefprofielen en perspectiefpubliek &#x200B;](/help/destinations/ui/activate-prospect-audiences.md) om bestemmingen te selecteren.
