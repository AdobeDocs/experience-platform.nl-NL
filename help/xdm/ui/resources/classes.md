---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;klasse;klassen;
solution: Experience Platform
title: Klassen maken en bewerken in de gebruikersinterface
description: Leer hoe u klassen maakt en bewerkt in de gebruikersinterface van het Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# Klassen maken en bewerken in de gebruikersinterface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Standaardfilter of aangepast klassenfilter"
>abstract="De lijst met beschikbare klassen wordt vooraf gefilterd op basis van de manier waarop ze zijn gemaakt. Selecteer het keuzerondje dat u wilt kiezen tussen de opties Standaard en Aangepast. De optie Standaard toont entiteiten die zijn gemaakt door Adobe en bevat zowel de klassen Afzonderlijk XDM profiel als Gebeurtenis voor XDM-ervaring. De optie Aangepast geeft entiteiten weer die binnen uw organisatie zijn gemaakt. Raadpleeg de documentatie voor meer informatie over het maken en bewerken van klassen."

In Adobe Experience Platform definieert de klasse van een schema de gedragsaspecten van de gegevens die het schema zal bevatten (record of tijdreeks). Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

Adobe biedt verschillende standaard (&quot;core&quot;) XDM-klassen (Experience Data Model), waaronder XDM Individual Profile en XDM ExperienceEvent. Naast deze kernklassen kunt u ook uw eigen aangepaste klassen maken om specifieke gebruiksgevallen voor uw organisatie te beschrijven.

Dit document biedt een overzicht van het maken, bewerken en beheren van aangepaste klassen in de gebruikersinterface van het Experience Platform.

## Vereisten {#prerequisites}

Deze handleiding vereist een goed begrip van XDM System. Verwijs naar het [ XDM overzicht ](../../home.md) voor een inleiding aan de rol van XDM binnen het Experience Platform ecosysteem, en de [ grondbeginselen van schemacompositie ](../../schema/composition.md) om te leren hoe de klassen aan schema&#39;s bijdragen XDM.

Terwijl niet vereist voor deze gids, wordt het geadviseerd dat u ook het leerprogramma volgt op [ samenstellend een schema in UI ](../../tutorials/create-schema-ui.md) om zich met de diverse mogelijkheden van de Redacteur van het Schema vertrouwd te maken.

## Aan de slag {#getting-started}

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Schemas]** in de linkernavigatie om de [!UICONTROL Schemas] -werkruimte te openen en selecteer vervolgens het tabblad **[!UICONTROL Classes]** . Er wordt een lijst met beschikbare klassen weergegeven.

## Filterklassen {#filter}

De lijst met klassen wordt automatisch gefilterd op basis van de manier waarop ze zijn gemaakt. Met de standaardinstelling worden de klassen weergegeven die door Adobe worden gedefinieerd. U kunt de lijst ook filteren om de lijsten weer te geven die door uw organisatie zijn gemaakt. Selecteer het keuzerondje dat u wilt kiezen tussen de opties [!UICONTROL Standard] en [!UICONTROL Custom] . De optie [!UICONTROL Standard] toont entiteiten die zijn gemaakt door Adobe en de optie [!UICONTROL Custom] geeft entiteiten weer die binnen uw organisatie zijn gemaakt.

![ het [!UICONTROL Classes] lusje van de [!UICONTROL Schemas] werkruimte met [!UICONTROL Standard] en [!UICONTROL Custom] benadrukte.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Gebruik de zoekmogelijkheden om een klasse te filteren of te zoeken op basis van de naam ervan. Zie de gids bij [ het onderzoeken van middelen XDM ](../explore.md) voor meer informatie.

## Een nieuwe klasse maken {#create}

Er zijn twee methoden om een klasse te maken in de gebruikersinterface van het platform. Selecteer **[!UICONTROL Create schema]** op een willekeurig tabblad in de [!UICONTROL Classes] -werkruimte of selecteer **[!UICONTROL Create class]** op het tabblad [!UICONTROL Schemas] .

![ het [!UICONTROL Classes] lusje van de [!UICONTROL Schemas] werkruimte met [!UICONTROL Create schema] en [!UICONTROL Create class] benadrukte ](../../images/ui/resources/classes/create-class-methods.png)

Als u **[!UICONTROL Create class]** selecteert, wordt het dialoogvenster [!UICONTROL Create class] weergegeven. Voer een [!UICONTROL Display name] en [!UICONTROL Description] in voor de klasse en kies het bedoelde gedrag van de klasse met de keuzerondjes. Klassen kunnen van het type, de recordreeks of de tijdreeks zijn. Selecteer **[!UICONTROL Create]** om uw keuzes te bevestigen en terug te keren naar het tabblad [!UICONTROL Classes] .

![ de [!UICONTROL Create class] dialoog met [!UICONTROL Create] benadrukte.](../../images/ui/resources/classes/create-class-dialog.png)

De klasse die u hebt gemaakt, is beschikbaar en wordt weergegeven in de weergave [!UICONTROL Classes] .

![ het [!UICONTROL Classes] lusje van de [!UICONTROL Schemas] werkruimte met de onlangs gecreeerd benadrukte klasse.](../../images/ui/resources/classes/new-class-listing.png)

### Een klasse maken of bewerken {#create-or-edit}

Als u **[!UICONTROL Create schema]** selecteert, wordt de [!UICONTROL Create schema] -workflow ook weergegeven. Selecteer **[!UICONTROL Other]** in de sectie [!UICONTROL Schema details] . Er wordt een lijst met beschikbare klassen weergegeven. Vanaf dit punt kunt u door bestaande klassen bladeren en filteren waarop u de nieuwe klasse wilt baseren.

>[!NOTE]
>
>Alleen aangepaste klassen die door uw organisatie zijn gedefinieerd, kunnen volledig worden bewerkt en aangepast. Voor kernklassen die door Adobe worden gedefinieerd, kunnen alleen de weergavenamen voor hun velden worden bewerkt binnen de context van afzonderlijke schema&#39;s. Zie de sectie op [ het uitgeven vertoningsnamen voor schemagebieden ](./schemas.md#display-names) voor details.
>
>Als een aangepaste klasse eenmaal is opgeslagen en in gegevensinvoer is gebruikt, kunnen er daarna alleen additieve wijzigingen in worden aangebracht. Zie de [ regels van schemaevolutie ](../../schema/composition.md#evolution) voor meer informatie.

![ het [!UICONTROL Create schema] werkschema met [!UICONTROL Other] die in de [!UICONTROL Schema details] sectie wordt benadrukt.](../../images/ui/resources/classes/other-schema-details.png)

Selecteer een keuzerondje om de klassen te filteren op basis van het feit of ze aangepaste of standaardklassen zijn. U kunt de beschikbare resultaten ook filteren op basis van hun industrie of naar een specifieke klasse zoeken met het zoekveld.

![ het [!UICONTROL Create schema] werkschema met de onderzoeksbar, [!UICONTROL Custom], en [!UICONTROL Industries] benadrukte.](../../images/ui/resources/classes/filter-and-search.png)

Om u te helpen op de aangewezen klasse beslissen, zijn er info (![ een infopictogram.](../../images/ui/resources/classes/info.png)) en voorproef (![ een voorproefpictogram.](../../images/ui/resources/classes/preview.png) ) voor elke klasse. Het infopictogram opent een dialoogvenster met een beschrijving van de klasse en de industrie waaraan deze is gekoppeld. Het voorproefpictogram opent een voorproefdialoog voor de klasse die een schemadiagram en zijn eigenschappen bevat.

![ een voorproef van de geselecteerde klasse met het schemadiagram en de benadrukte klasseneigenschappen.](../../images/ui/resources/classes/class-preview.png)

Selecteer een willekeurige rij om een klasse te kiezen en selecteer vervolgens **[!UICONTROL Next]** om uw keuze te bevestigen.

![ het [!UICONTROL Create schema] werkschema met een klasse die van de lijst van beschikbare klassen wordt geselecteerd en [!UICONTROL Next] benadrukt.](../../images/ui/resources/classes/select-class.png)

Het gedeelte [!UICONTROL Name and review] van de workflow wordt weergegeven. Geef in deze sectie een naam en beschrijving op om uw schema te identificeren. &#x200B;De basisstructuur van het schema (verstrekt door de klasse) wordt getoond in het canvas voor u om uw geselecteerde klasse en schemastructuur te herzien en te verifiëren.

Voer in het tekstveld [!UICONTROL Schema display name] een korte, beschrijvende, unieke en gebruikersvriendelijke naam in voor de klasse. Voer vervolgens een geschikte beschrijving in om het gedrag te identificeren van de gegevens die in het schema worden gedefinieerd. Wanneer u de schemastructuur hebt herzien en met uw montages gelukkig bent, uitgezocht **[!UICONTROL Finish]** om uw schema tot stand te brengen.

![ de [!UICONTROL Name and review] sectie van het [!UICONTROL Create schema] werkschema met [!UICONTROL Schema display name], [!UICONTROL Description], en [!UICONTROL Finish] benadrukte.](../../images/ui/resources/classes/name-and-review-class.png)

De Schema-editor wordt weergegeven, waarbij de structuur van het schema op het canvas wordt weergegeven. U kunt [ nu beginnen toevoegend gebieden aan de klasse ](#add-fields).

![ de Redacteur van het Schema met de structuur van het schema die in het canvas wordt getoond.](../../images/ui/resources/classes/edit.png)

## Velden aan een klasse toevoegen {#add-fields}

Als u een schema hebt waarin een aangepaste klasse wordt gebruikt die is geopend in [!UICONTROL Schema Editor] , kunt u beginnen met het toevoegen van velden aan de klasse. Om een nieuw gebied toe te voegen, selecteer **plus (+)** pictogram naast de naam van het schema.

>[!IMPORTANT]
>
>Wanneer het bouwen van een schema dat een klasse uitvoert die door uw organisatie wordt bepaald, herinner dat de groepen van het schemagebied voor gebruik slechts met compatibele klassen beschikbaar zijn. Aangezien de klasse die u hebt gedefinieerd nieuw is, worden er geen compatibele veldgroepen weergegeven in het dialoogvenster **[!UICONTROL Add field group]** . In plaats daarvan, zult u nieuwe gebiedsgroepen ](./field-groups.md#create) voor gebruik met die klasse moeten creëren [. De volgende keer dat u een schema samenstelt dat de nieuwe klasse implementeert, worden de gedefinieerde veldgroepen weergegeven en beschikbaar voor gebruik.

![ de Redacteur van het Schema met toevoegt benadrukte knoop.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Onthoud dat alle velden die u aan een klasse toevoegt, worden gebruikt in alle schema&#39;s waarin die klasse wordt gebruikt. Daarom moet u zorgvuldig overwegen welke velden handig zijn in alle gevallen waarin het schema wordt gebruikt. Als u overweegt om een gebied toe te voegen dat slechts gebruik in sommige schema&#39;s onder deze klasse kan zien, kunt u overwegen toevoegend het aan die schema&#39;s door [ te creëren een gebiedsgroep ](./field-groups.md#create) in plaats daarvan.

Er verschijnt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** in het canvas en de rechterrails worden bijgewerkt om besturingselementen weer te geven waarmee de eigenschappen van het veld worden geconfigureerd. Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Class]** .

![ een naamloos gebied op het canvas van de schemaredacteur met Assign aan het gebied van de Klasse wordt geselecteerd en wordt benadrukt die.](../../images/ui/resources/classes/assign-to-class.png)

Zie de gids op [ definiërend gebieden in UI ](../fields/overview.md#define) voor specifieke stappen op om het gebied aan de klasse te vormen en toe te voegen. Ga door met het toevoegen van zoveel velden als nodig zijn voor de klasse. Als u klaar bent, selecteert u **[!UICONTROL Save]** om zowel het schema als de klasse op te slaan.

![ het onlangs gecreeerd schema op het canvas van de Redacteur van het Schema, met [!UICONTROL Save] benadrukte.](../../images/ui/resources/classes/save.png)

Als u eerder schema&#39;s hebt gecreeerd die deze klasse gebruiken, zullen de onlangs toegevoegde gebieden automatisch in die schema&#39;s verschijnen.

## De klasse van een schema wijzigen {#schema}

U kunt de klasse van het schema op elk gewenst moment tijdens het eerste ontwerpproces wijzigen voordat het is opgeslagen. Dit moet echter met voorzichtigheid gebeuren, aangezien veldgroepen alleen met bepaalde klassen compatibel zijn. Als u de klasse wijzigt, worden het canvas en alle toegevoegde velden opnieuw ingesteld.
Zie de gids bij [ het creëren van en het uitgeven van schema&#39;s ](./schemas.md#change-class) voor meer informatie.

## Volgende stappen {#next-steps}

In dit document wordt beschreven hoe u klassen kunt maken en bewerken met de gebruikersinterface van het platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie het [[!UICONTROL Schemas] overzicht van de werkruimte ](../overview.md).

Leren hoe te om klassen te beheren die de Registratie API van het Schema gebruiken, zie de [ gids van het klasseeindpunt ](../../api/classes.md).
