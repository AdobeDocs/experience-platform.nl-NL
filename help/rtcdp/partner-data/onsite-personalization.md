---
title: Erkenning door Partner-Aided Visitor gebruiken om onsite ervaringen aan te passen
description: Leer hoe u bezoekerserkenning met ondersteuning van partners kunt gebruiken om uw bezoekers op de site een persoonlijke ervaring te bieden.
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 1%

---

# Door partners ondersteunde bezoekersherkenning gebruiken om ervaringen op de site te personaliseren

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die een licentie hebben verkregen voor Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Premiere, Real-Time CDP Ultimate. Meer informatie over deze pakketten vindt u in de [productbeschrijvingen](https://helpx.adobe.com/legal/product-descriptions.html) en neem contact op met uw Adobe voor meer informatie.

Leer hoe u met partnerondersteunde erkenning persoonlijke ervaringen kunt bieden aan bezoekers van webeigenschappen. Gebruik deze zelfstudie om inzicht te krijgen in de implementatiereeks van verschillende elementen in Experience Platform en andere oplossingen voor Experiencen Cloud en om een gepersonaliseerde ervaring weer te geven voor geverifieerde en niet-geverifieerde bezoekers.

![Een infografisch die beschrijft hoe te om partner-verstrekte attributen te gebruiken om gepersonaliseerde ervaringen aan uw bezoekers te leveren.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Voorbeeld van industrie {#industry-example}

Als voorbeeld, overweeg een merk van de huisverbetering dat lage authentificatiecijfers heeft. Dit merk zou gepersonaliseerde ervaringen aan de eerste bezoekers, zonder vroegere geschiedenis of authentificatie, en zonder het vervagen vertrouwen op derdekoekjes willen leveren.

Dit merk kiest ervoor om partnerherkenningstechnologie te gebruiken om de bezoeker waarschijnlijk te herkennen en een meer gepersonaliseerde ervaring te dienen. Dit helpt om verder na te denken, aangezien de bezoeker zich onderaan de marketing trechter beweegt. Het merk kan bijvoorbeeld demografische signalen van partners gebruiken voor on-site content die aantrekkelijk is voor mensen die onlangs zijn verhuisd en die een korting bieden op populaire DIY-producten.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer het van plan zijn om partner-verstrekte attributen te gebruiken om gepersonaliseerde ervaringen aan uw voor authentiek verklaarde en niet voor authentiek verklaarde bezoekers te leveren, overweeg de volgende eerste vereisten in uw planningsproces:

* Welke input wordt verwacht door de herkenningstechnologie van uw partner zodat kunnen zij op extra attributen laag?
* In hoeverre bent u comfortabel om personalisatie op verschillende kanalen en voor verschillende gebruiksgevallen te leveren die op voorwaardelijk afgeleide attributen, tegenover deterministisch bevestigde attributen worden gebaseerd?
* Hoe moet de ervaring van een vooraf geverifieerde maar herkende bezoeker veranderen wanneer ze worden geverifieerd?

### UI-functionaliteit, platformcomponenten en Experiencen Cloud die u wilt gebruiken {#ui-functionality-and-elements}

Als u dit geval met succes wilt implementeren, moet u meerdere gebieden van Real-time Customer Data Platform en andere oplossingen voor Experiencen Cloud gebruiken. Zorg ervoor dat u de benodigde [attribuut-gebaseerde toegangsbeheertoestemmingen](/help/access-control/abac/overview.md) voor al deze gebieden, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* Gegevensverzameling
   * [Adobe Experience Platform Web SDK](/help/edge/home.md)
   * [Tags](/help/tags/home.md)
   * [Gegevensstromen](/help/datastreams/overview.md)
* Gegevensbeheer in Real-Time CDP
   * [Identiteiten](/help/identity-service/namespaces.md)
   * [Schema&#39;s](/help/xdm/home.md)
   * [Labels voor gegevensgebruik](/help/data-governance/labels/overview.md)
   * [Gegevenssets](/help/catalog/datasets/overview.md)
* Webeigenschappen aanpassen
   * [Randsegmentatie](/help/segmentation/ui/edge-segmentation.md)
   * [Edge-aanpassingsdoelen](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (of een persoonlijk platform van uw keuze. In deze zelfstudie wordt Adobe Target gemarkeerd als een personalisatie-engine.

## Video doorloopt {#video-walkthrough}

Bekijk de videozelfstudie hieronder voor een analyse van hoe u onsite ervaringen kunt personaliseren voor onbekende bezoekers:

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

![Een infografisch die beschrijft hoe te om partner-verstrekte attributen te gebruiken om gepersonaliseerde ervaringen aan uw bezoekers te leveren.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Als **klant**, geeft u een licentie van de **gegevenspartner** de mogelijkheid om in real-time inzichten op anderszins anonieme websitebezoekers op te halen.
2. Als **klant**, stelt u cliënt-zijbibliotheken op uw eigenschappen op om te roepen **partner** APIs en u vormt Web SDK of Mobiele SDK om partner-Geleide signalen naar Real-Time CDP te verzenden.
3. Wanneer u door uw website of app bladert, **bezoeker** wordt waarschijnlijk erkend door de **partner**, die kenmerken samen met een id retourneert.
4. Real-Time CDP voert randsegmentatie uit om inkomende gebeurtenisklappen te evalueren en handhaaft resultaten tegen de [ECID-id](https://experienceleague.adobe.com/docs/id-service/using/home.html).
5. Adobe Target gebruikt de uitvoer van de randsegmentatie om de ervaring terug te brengen naar de **bezoeker** voor personalisatie tijdens de sessie.
6. De gebeurtenis wordt in zijn geheel voor stroomafwaartse werkschema&#39;s zoals analyse en heroriëntering voortgezet.

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien.

### Gegevensbeheer - Maak een naamruimte, schema en gegevensset voor identiteiten om gegevenskenmerken te beheren {#data-management}

Voordat u het gebruiksgeval kunt gebruiken om de ervaring van niet-geregistreerde bezoekers te personaliseren, moet u eerst de gegevensbeheerstructuur in Real-Time CDP instellen om de inkomende real-time gegevens over gebeurtenissen en publiekskwalificaties te ontvangen.

#### Identiteitsnaamruimte van partner-id maken

Eerst, moet u een identiteitsnaamruimte van partnerIdentiteit tot stand brengen. Navigeren naar **[!UICONTROL Customer]** > **[!UICONTROL Identities]** in het linkerspoor en selecteer vervolgens **[!UICONTROL Create identity namespace]** rechtsboven in het scherm.

![Het dialoogvenster Naamruimte maken met de partner-id is gemarkeerd.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Meer informatie over hoe [een naamruimte voor de partner-id maken](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Een schema maken

Maak vervolgens een [!UICONTROL Experience Event] schema om de tijdreeksgegevens te houden die u later van uw Web-eigenschappen zult verzamelen, en zorg ervoor te gebruiken [!UICONTROL XDM ExperienceEvent] als de basisklasse voor het schema. Meer informatie over hoe [een schema maken met de interface van het Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![De werkruimte Schema&#39;s met schema maken en de gebeurtenis XDM Experience zijn gemarkeerd.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Tijdens het maken van uw schema en [veldgroepen toevoegen aan uw schema](/help/xdm/ui/resources/schemas.md#add-field-groups), kunt u overwegen de [Webpagina bezoeken](/help/xdm/field-groups/event/web-details.md) en [Identiteitskaart](/help/xdm/field-groups/profile/identitymap.md) veldgroepen. Dit is een aanvulling op andere veldgroepen die van toepassing zijn op uw digitale eigenschap en praktijken van de gegevensinzameling.

Bovendien, kunt u een bestaande gebiedsgroep tot stand brengen of hergebruiken en het toevoegen aan uw schema, om partner-verstrekte inzichten over de bezoeker te vangen. Lees hoe te [een veldgroep maken](/help/xdm/ui/resources/field-groups.md) en hoe [velden toevoegen](/help/xdm/ui/resources/field-groups.md) naar de veldgroep. Als u bijvoorbeeld verwacht te personaliseren tegen door partners verschafte inzichten zoals leeftijd, werkgelegenheidsstatus, macht voor maandelijkse uitgaven of gedrag, moet u uw veldgroep geschikte velden laten opnemen.

Ervan uitgaande dat de gegevenspartner een stabiele id voor de bezoeker verstrekt en u dat in Real-Time CDP wilt brengen, zeker ben om een geschikt genoemd gebied voor het herkenningsteken in uw groep van het douanegebied te hebben. U moet het veld ook als een identiteit markeren in de naamruimte die u eerder hebt gemaakt. Vergeet ook niet om [het schema opnemen in profiel inschakelen](/help/xdm/ui/resources/schemas.md#profile).

#### Een gegevensset maken

Daarna, moet u een dataset tot stand brengen om de tijd-reeksgegevens te houden die u van uw bezoekers van het Web bezit verzamelt en die u voor onsite verpersoonlijking zult gebruiken.

Lees de zelfstudie aan [hoe te om een dataset te creëren](/help/catalog/datasets/user-guide.md#create) en vergeet niet de optie te selecteren om de gegevensset te maken op basis van een schema. Creeer de dataset die op het schema wordt gebaseerd dat u in de vorige stap creeerde.

Gelijkaardig aan de stap wanneer het creëren van een schema, moet u toelaten dat de dataset in wordt omvat [!UICONTROL Real-Time Customer Profile]. Voor meer informatie over het toelaten van de dataset voor gebruik binnen [!UICONTROL Real-Time Customer Profile], lees de [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Verzameling van gebeurtenisgegevens implementeren in uw webeigenschap {#implement-data-collection}

Nadat u de configuratie van uw gegevensbeheer hebt ingesteld, moet u nu realtime-gebeurtenis implementeren [gegevensverzameling](/help/collection/home.md) op uw webeigenschap. U moet uw bezit met de bibliotheek van de de gegevensinzameling van de Adobe instrumenten - [!UICONTROL Web SDK] - real-time oproepen van gebeurtenissen verzamelen en terugsturen naar Real-Time CDP. Dit item bestaat uit een paar afzonderlijke taken voor een paar componenten van gegevensverzameling.

>[!IMPORTANT]
>
>Om partner-verstrekte attributen terug te winnen, moet u ook *integreer uw Webbezit met partner APIs of andere methodes om attributen van gegevenspartners in real time te roepen en terug te winnen*. Bespreek dit aspect met uw partner van keuze, omdat het niet onderwerp is van deze zelfstudie.

Gebruik eerst de toepassingsschakelaar in de rechterbovenhoek van het scherm om naar de **[!UICONTROL Data Collection]** sectie.

>[!TIP]
>
>Contacteer uw systeembeheerder om toegang te vragen als u niet kunt zien [!UICONTROL Data Collection] in de toepassingsschakelaar.

![App-schakeloptie om de sectie Gegevensverzameling te openen.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

De **[!UICONTROL Data Collection]** lijkt op de onderstaande afbeelding.

![Sectie voor gegevensverzameling van de gebruikersinterface van het platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Gegevensstroom maken

Als eerste stap in het gedeelte Gegevensverzameling [een nieuwe gegevensstroom maken](/help/datastreams/configure.md). De gegevensstroom is de basis van hoe gegevens worden verzameld en correct worden gerouteerd naar de juiste Adobe-app, in dit geval Experience Platform.

Terwijl u de gegevensstroom maakt, kunt u in het dialoogvenster **[!UICONTROL Event schema]** selecteert u het schema dat u eerder hebt gemaakt.

![Selector voor een gebeurtenisschema gemarkeerd tijdens het configureren van een nieuwe gegevensstroom.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Selecteer de gebeurtenisdataset](/help/datastreams/configure.md#aep) die u eerder hebt gemaakt in het vervolgkeuzemenu, schakelt u de selectievakjes in naast **[!UICONTROL Edge Segmentation]** en **[!UICONTROL Personalization Destinations]** en selecteert u **[!UICONTROL Save]**.

Merk op dat u geen profieldataset in dit scenario moet selecteren aangezien u in op gebeurtenis-gebaseerde tijdreeksgegevens brengt.

#### Tag-eigenschap maken

Beschouw een eigenschap als een container die u vult met extensies, regels, gegevenselementen en bibliotheken wanneer u tags op uw site implementeert.

Navigeren naar **[!UICONTROL Tags]** en selecteert u **[!UICONTROL New property]**.

![Maak een nieuwe eigenschap voor tags.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Vul de vereiste velden in en selecteer **[!UICONTROL Save]**.

![Vul de vereiste velden voor de nieuwe eigenschap in.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Volledige informatie ophalen over hoe [een tag-eigenschap maken](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Vervolgens moet u verschillende extensies installeren in de eigenschap. Selecteer de eigenschap tag en navigeer naar de [!UICONTROL Extensions] sectie.

![Selecteer de nieuwe eigenschap tag.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Let erop dat de [!UICONTROL Core] is al geïnstalleerd. U moet nog twee extensies installeren, zoals in de volgende secties wordt beschreven.

![Geïnstalleerde extensies weergeven.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Web SDK-extensie installeren

In deze zelfstudie wordt aangegeven hoe u uw website kunt voorzien van een Web SDK. U kunt ook [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) op uw app om de ervaring aan te passen aan uw App-bezoekers.

![Weergave van de Web SDK-extensie in de catalogus Extensies.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

In het scherm om Web SDK te vormen, navigeer neer aan het **[!UICONTROL Datastreams]** en geef informatie over de sandbox van het Experience Platform die u gebruikt. Selecteer de desbetreffende sandbox en de gegevensstroom die u in de vorige stappen van de volgende vervolgkeuzelijst hebt gemaakt. U kunt dezelfde sandbox- en gegevensstroomwaarden kiezen voor alle andere omgevingen. Laat de andere instellingen ongewijzigd en selecteer **[!UICONTROL Save]**.

Volledige informatie ophalen over [hoe te om SDK van het Web te installeren](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### ID-serviceversie installeren

Gebruik de [Experience Cloud ID Service-extensie](/help/tags/extensions/client/id-service/overview.md) om een unieke, op apparaten gebaseerde identiteit van de eerste partij te maken voor bezoekers in alle oplossingen van het Experience Cloud. Zoeken naar **[!UICONTROL ID Service]** in de extensiecatalogus en installeer deze. Houd alle standaardinstellingen wanneer u de extensie installeert.

![Bekijk de extensie Id-service in de catalogus Extensies.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Omgevingen instellen

Ga vervolgens door naar de **[!UICONTROL Environments]** van de linkernavigatie. In deze stap moet u uw website verbinden met het Adobe Edge-netwerk om bezoekersinformatie in real-time op te halen en te leveren.

Selecteer het vakpictogram rechts voor de ontwikkelomgeving en kopieer de standaardversie van het JavaScript-codefragment dat in een modaal venster wordt weergegeven.

![Selectiepictogram gemarkeerd in de sectie Omgevingen van de gebruikersinterface voor gegevensverzameling.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

U moet dit codefragment helemaal boven aan uw website toevoegen. Als gevolg hiervan roept uw website het Adobe Edge Network aan om JavaScript-logica op te halen die op de pagina wordt geladen en uitgevoerd. Dit staat voor functionaliteit zoals de generatie van bezoekersidentiteitskaart, gegevensinzameling, en de ervarings in real time verpersoonlijking toe om te werken.

#### Gegevenselementen instellen

Gegevenselementen zijn de bouwstenen voor uw gegevenswoordenboek (of gegevenskaart). Eén gegevenselement is een variabele waarvan de waarde kan worden toegewezen aan querytekenreeksen, URL&#39;s, cookie-waarden, JavaScript-variabelen enzovoort. Meer informatie over [gegevenselementen](/help/tags/ui/managing-resources/data-elements.md).

In dit geval moet u twee gegevenselementen instellen.

Stel eerst een `partnerData` element. Ga naar de **[!UICONTROL Data Elements]** en selecteert u **[!UICONTROL Create New Data Element]**.

![Maak een nieuw gegevenselement.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Geef het gegevenselement een naam `partnerData`, laat de [!UICONTROL extension] waarde als [!UICONTROL Core], en instellen **[!UICONTROL Data Element Type]** als **[!UICONTROL JavaScript Variable]**. Enter `partnerData` in het veld met de titel **[!UICONTROL JavaScript variable name]** en selecteert u **[!UICONTROL Save]**.

![Gemarkeerde selecties om het partnerData gegevenselement correct te vormen.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Geef de nieuwe variabele een naam om het tweede gegevenselement in te stellen `pageVisit`, stelt u de **[!UICONTROL Extension]** tot **[!UICONTROL Adobe Experience Platform]** en kiest u **[!UICONTROL XDM Object]** als het gegevenstype.

![Gemarkeerde selecties om het pageVisit gegevenselement correct te vormen.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Van het schema, selecteer de derdeattributen die aan de waarden beantwoorden die u van de gegevenspartner verwacht. Selecteer vervolgens het keuzerondje met de naam **[!UICONTROL Provide entire object]**. Selecteer het pictogram dat er als een database uitziet en kies de optie `partnerData` gegevenselement dat u eerder hebt gemaakt.

#### Regels instellen

In de **[!UICONTROL Rules]** kunt u uw website configureren om een verzoek tot aanpassing te verzenden naar een Adobe met de kenmerken die zijn geladen in de gegevenselementen die u net hebt gemaakt. Meer informatie over [regels maken](/help/tags/ui/managing-resources/rules.md).

Selecteer **[!UICONTROL Create new Rule]**. Geef deze regel een naam **[!UICONTROL Personalize]** en selecteer + teken naast **[!UICONTROL Events]**. Selecteren **[!UICONTROL Page Bottom]** als de gebeurtenis en save.

![Selecties voor het gebeurtenistype deel van een regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Selecteer + teken naast **[!UICONTROL Actions]**. De extensie bijwerken naar **[!UICONTROL Adobe Experience Platform Web SDK]** en instellen **[!UICONTROL Action Type]** tot **[!UICONTROL Send event]**.

![Selecties voor het actietype deel van een regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Van de **[!UICONTROL Type]** vervolgkeuzelijst rechts, selecteert u `web.webpagedetails.pageViews` als het gebeurtenistype.

![Selecteer gebeurtenistype.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Selecteer het databasepictogram naast XDM-gegevens en selecteer de optie `pageVisit` gegevenselement.

Blader omlaag in de lijst met actieconfiguraties en controleer het selectievakje met de titel **[!UICONTROL Render visual personalization decisions]**. Dit is belangrijk om ervoor te zorgen dat ervaringen die via Adobe Target of andere vergelijkbare producten worden geleverd, visueel op de webpagina worden weergegeven. Selecteren **[!UICONTROL Keep Changes]** en vervolgens **[!UICONTROL Save]** de regel.

![Schakel het selectievakje Weergeven van beslissingen voor visuele personalisatie in.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Publicatieworkflow instellen

Als u deze configuratie op de webpagina wilt implementeren, moet u eerst een bibliotheek maken die de bronnen bevat die u zojuist hebt gemaakt. Meer informatie over [publicatiestroom instellen](/help/tags/ui/publishing/publishing-flow.md).

Selecteren **[!UICONTROL Publishing Flow]** en vervolgens **[!UICONTROL Add Library]**.

Selecteren **[!UICONTROL Add all Changed Resources]**, geef de bibliotheek een naam, stel de omgeving in op **[!UICONTROL Development]** en selecteert u **[!UICONTROL Save & Build to Development]**.

![Bibliotheek maken en implementeren in de ontwikkelomgeving](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Uw website testen

Op dit punt, zou uw website volledig van instrumenten voorzien met Web SDK moeten zijn. Om te testen dat de gegevensinzameling zoals verwacht werkt, kunt u aan uw website navigeren en de ontwikkelaarshulpmiddelen van uw browser gebruiken om netwerkverkeer te inspecteren.

Invoer `interact` vernieuwt u de pagina in het zoekvak en bekijkt u de netwerkaanroepen van uw website naar het Adobe Edge-netwerk dat wordt gevuld.

![Weergave van netwerkgebeurtenissen die worden gevuld met ontwikkelaarsgereedschappen.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalisatie {#personalization}

U bent nu klaar om publiek voor verpersoonlijking tot stand te brengen en te activeren.

#### Segmentatie van rand instellen

Instellen [randsegmentatie](/help/segmentation/ui/edge-segmentation.md) Het publiekslidmaatschap van uw bezoekers wordt dus in real-time geëvalueerd wanneer ze uw webeigenschap bezoeken.

Zorg ervoor dat u ook een [actief-op-rand samenvoegbeleid](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) voor het randpubliek.

#### Integreren met Adobe Target of een andere aangepaste personalisatiebestemming

U kunt nu integreren met een aanpassingsengine om persoonlijke inhoud weer te geven voor uw website of app-bezoekers. Adobe raadt u aan de [Adobe Target-bestemming](/help/destinations/catalog/personalization/adobe-target-connection.md) daartoe.

>[!IMPORTANT]
>
>Lees de zelfstudie aan [het activeren van publiek aan de bestemmingen van de randverpersoonlijking](/help/destinations/ui/activate-edge-personalization-destinations.md) voor een volledige weergave van de stappen die nodig zijn om uw publiek te activeren.

## Beperkingen en problemen oplossen {#limitations-and-troubleshooting}

Houd rekening met de volgende beperkingen wanneer u het op deze pagina beschreven gebruiksgeval bekijkt:

* Als u Partner IDs gebruikt, ben zich ervan bewust dat deze IDs niet wanneer het bouwen van uw wordt gebruikt [identiteitsgrafiek](/help/identity-service/ui/identity-graph-viewer.md).

## Andere gebruiksgevallen die worden bereikt via ondersteuning van partnergegevens {#other-use-cases}

Verken verdere gebruiksgevallen die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

* [Eerste-partijprofielen met attributen van vertrouwde op gegevenspartners aanvullen](/help/rtcdp/partner-data/supplement-first-party-profiles.md) om uw gegevensstichting te verbeteren en nieuwe inzichten in uw klantenbasis te krijgen en betere publieksoptimalisering te bereiken.
* Gebruik gegevensondersteuning van derden in Real-Time CDP voor [breid uw profielbasis met perspectiefprofielen van gegevenspartners uit en verbind met hen om nieuwe klanten te verwerven of te bereiken](/help/rtcdp/partner-data/prospecting.md).
* [Uitgebreide activering van perspectiefprofielen en perspectiefpubliek](/help/destinations/ui/activate-prospect-audiences.md) om doelen te selecteren.
