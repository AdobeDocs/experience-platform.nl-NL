---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;klasse;klassen;
solution: Experience Platform
title: Klassen maken en bewerken in de gebruikersinterface
description: Leer hoe u klassen maakt en bewerkt in de gebruikersinterface van het Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 4214339c4a661c6bca2cd571919ae205dcb47da1
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---

# Klassen maken en bewerken in de gebruikersinterface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Standaardfilter of aangepast klassenfilter"
>abstract="De lijst met beschikbare klassen wordt vooraf gefilterd op basis van de manier waarop ze zijn gemaakt. Selecteer het keuzerondje dat u wilt kiezen tussen de opties Standaard en Aangepast. De optie Standaard toont entiteiten die zijn gemaakt door Adobe en bevat zowel de klassen Afzonderlijk XDM profiel als Gebeurtenis voor XDM-ervaring. De optie Aangepast geeft entiteiten weer die binnen uw organisatie zijn gemaakt. Raadpleeg de documentatie voor meer informatie over het maken en bewerken van klassen."

In Adobe Experience Platform definieert de klasse van een schema de gedragsaspecten van de gegevens die het schema zal bevatten (record of tijdreeks). Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

Adobe biedt verschillende standaard (&quot;core&quot;) Experience Data Model (XDM)-klassen, waaronder [!DNL XDM Individual Profile] en [!DNL XDM ExperienceEvent]. Naast deze kernklassen kunt u ook uw eigen aangepaste klassen maken om specifieke gebruiksgevallen voor uw organisatie te beschrijven.

Dit document biedt een overzicht van het maken, bewerken en beheren van aangepaste klassen in de gebruikersinterface van het Experience Platform.

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Zie de [XDM-overzicht](../../home.md) voor een inleiding op de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van de schemacompositie](../../schema/composition.md) om te leren hoe de klassen tot schema&#39;s XDM bijdragen.

Hoewel dit niet nodig is voor deze handleiding, wordt u aangeraden de zelfstudie ook op te volgen [samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) om vertrouwd te maken met de verschillende mogelijkheden van de [!DNL Schema Editor].

## Aan de slag

Selecteer in de interface Platform de optie **[!UICONTROL Schemas]** in de linkernavigatie om de [!UICONTROL Schemas] werkruimte selecteert u vervolgens de **[!UICONTROL Classes]** tab. Er wordt een lijst met beschikbare klassen weergegeven.

## Filterklassen {#filter}

De lijst met klassen wordt automatisch gefilterd op basis van de manier waarop ze zijn gemaakt. Met de standaardinstelling worden de klassen weergegeven die door Adobe worden gedefinieerd. U kunt de lijst ook filteren om de lijsten weer te geven die door uw organisatie zijn gemaakt. Selecteer het keuzerondje dat u wilt kiezen tussen de [!UICONTROL Standard] en [!UICONTROL Custom] opties. De [!UICONTROL Standard] toont entiteiten die zijn gemaakt door Adobe en de optie [!UICONTROL Custom] geeft entiteiten weer die binnen uw organisatie zijn gemaakt.

![De [!UICONTROL Classes] tabblad van het [!UICONTROL Schemas] werkruimte met [!UICONTROL Standard] en [!UICONTROL Custom] gemarkeerd.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>U kunt de zoekmogelijkheden van de werkruimte gebruiken om het schema gemakkelijker te vinden. Zie de handleiding op [XDM-bronnen verkennen](../explore.md) voor meer informatie .

## Een nieuwe klasse maken {#create}

Er zijn twee methoden om een klasse te maken in de gebruikersinterface van het platform. Van om het even welk lusje in **[!UICONTROL Schemas]** werkruimte, selecteert u **[!UICONTROL Create schema]** of van de [!UICONTROL Classes] tab selecteren **[!UICONTROL Create class]**.

![De [!UICONTROL Classes] tabblad van het [!UICONTROL Schemas] werkruimte met [!UICONTROL Create schema] en [!UICONTROL Create class] gemarkeerd](../../images/ui/resources/classes/create-class-methods.png)

Als u **[!UICONTROL Create class]** de [!UICONTROL Create class] wordt weergegeven. Voer een [!UICONTROL Name] en [!UICONTROL Description] voor de klasse en kies het bedoelde gedrag van de klasse met de keuzerondjes. Klassen kunnen recordreeksen of tijdreeksen zijn. Selecteren **[!UICONTROL Create]** om je keuzes te bevestigen.

![De [!UICONTROL Create class] dialoog met [!UICONTROL Create] gemarkeerd.](../../images/ui/resources/classes/create-class-dialog.png)

De [!DNL Schema Editor] wordt weergegeven en ziet u een nieuw schema in het canvas dat is gebaseerd op de aangepaste klasse die u zojuist hebt gemaakt. Aangezien er nog geen velden aan de klasse zijn toegevoegd, bevat het schema alleen een `_id` veld, dat de door het systeem gegenereerde unieke id vertegenwoordigt die automatisch wordt toegepast op alle bronnen in het [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Wanneer het bouwen van een schema dat een klasse uitvoert die door uw organisatie wordt bepaald, herinner dat de groepen van het schemagebied voor gebruik slechts met compatibele klassen beschikbaar zijn. Aangezien de klasse die u hebt gedefinieerd nieuw is, worden er geen compatibele veldgroepen weergegeven in het dialoogvenster **[!UICONTROL Add field group]** in. In plaats daarvan moet u [nieuwe veldgroepen maken](./field-groups.md#create) voor gebruik met die klasse. De volgende keer dat u een schema samenstelt dat de nieuwe klasse implementeert, worden de gedefinieerde veldgroepen weergegeven en beschikbaar voor gebruik.

### Een klasse maken of bewerken {#create-or-edit}

Als u **[!UICONTROL Create schema]** de [!UICONTROL Create schema] wordt weergegeven. In de [!UICONTROL Schema details] sectie, selecteert u **[!UICONTROL Other]**. Er wordt een lijst met beschikbare klassen weergegeven. Vanaf dit punt kunt u door bestaande klassen bladeren en filteren waarop u de nieuwe klasse wilt baseren.

>[!NOTE]
>
>Alleen aangepaste klassen die door uw organisatie zijn gedefinieerd, kunnen volledig worden bewerkt en aangepast. Voor kernklassen die door Adobe worden gedefinieerd, kunnen alleen de weergavenamen voor hun velden worden bewerkt binnen de context van afzonderlijke schema&#39;s. Zie de sectie over [weergavenamen voor schemavelden bewerken](./schemas.md#display-names) voor meer informatie.
>
>Als een aangepaste klasse eenmaal is opgeslagen en in gegevensinvoer is gebruikt, kunnen er daarna alleen additieve wijzigingen in worden aangebracht. Zie de [regels voor schemaontwikkeling](../../schema/composition.md#evolution) voor meer informatie .

![De [!UICONTROL Create schema] workflow met [!UICONTROL Other] in de [!UICONTROL Schema details] sectie.](../../images/ui/resources/classes/other-schema-details.png)

Selecteer een keuzerondje om de klassen te filteren op basis van het feit of ze aangepaste of standaardklassen zijn. U kunt de beschikbare resultaten ook filteren op basis van hun industrie of naar een specifieke klasse zoeken met het zoekveld.

![De [!UICONTROL Create schema] werkschema met de zoekbalk, [!UICONTROL Custom], en [!UICONTROL Industries] gemarkeerd.](../../images/ui/resources/classes/filter-and-search.png)

Om u te helpen bij het kiezen van de juiste klasse, zijn er info (![Een info-pictogram.](../../images/ui/resources/classes/info.png)) en voorvertoning (![Een voorvertoningspictogram.](../../images/ui/resources/classes/preview.png)) voor elke klasse. Het infopictogram opent een dialoogvenster met een beschrijving van de klasse en de industrie waaraan deze is gekoppeld. Het voorproefpictogram opent een voorproefdialoog voor de klasse die een schemadiagram en zijn eigenschappen bevat.

![Een voorvertoning van de geselecteerde klasse met het schema en de klasseneigenschappen gemarkeerd.](../../images/ui/resources/classes/class-preview.png)

Selecteer een willekeurige rij om een klasse te kiezen en selecteer vervolgens **[!UICONTROL Next]** om uw keuze te bevestigen.

![De [!UICONTROL Create schema] een werkschema met een klasse die uit de lijst van beschikbare klassen wordt geselecteerd en [!UICONTROL Next] gemarkeerd.](../../images/ui/resources/classes/select-class.png)

De [!UICONTROL Name and describe] wordt weergegeven. Geef in deze sectie een naam en beschrijving op om uw schema te identificeren. &#x200B;De basisstructuur van het schema (verstrekt door de klasse) wordt getoond in het canvas voor u om uw geselecteerde klasse en schemastructuur te herzien en te verifiëren.

Voer een korte, beschrijvende, unieke en gebruikersvriendelijke naam in voor de klasse in het dialoogvenster [!UICONTROL Schema display name] tekstveld. Voer vervolgens een geschikte beschrijving in om het gedrag te identificeren van de gegevens die in het schema worden gedefinieerd. Wanneer u de schemastructuur hebt herzien en met uw montages gelukkig bent **[!UICONTROL Finish]** om uw schema te maken.

![De [!UICONTROL Name and review] van de [!UICONTROL Create schema] met de [!UICONTROL Schema display name], [!UICONTROL Description], en [!UICONTROL Finish] gemarkeerd.](../../images/ui/resources/classes/name-and-review-class.png)

De [!DNL Schema Editor] verschijnt, terwijl de structuur van het schema op het canvas wordt weergegeven. U kunt nu beginnen [toevoegen van velden aan de klasse](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Velden aan een klasse toevoegen {#add-fields}

Als u een schema hebt waarin een aangepaste klasse wordt gebruikt die is geopend in het dialoogvenster [!UICONTROL Schema Editor], kunt u beginnen gebieden aan de klasse toe te voegen. Als u een nieuw veld wilt toevoegen, selecteert u de **plus (+)** naast de naam van het schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Onthoud dat alle velden die u aan een klasse toevoegt, worden gebruikt in alle schema&#39;s waarin die klasse wordt gebruikt. Daarom moet u zorgvuldig overwegen welke velden handig zijn in alle gevallen waarin het schema wordt gebruikt. Als u van plan bent een gebied toe te voegen dat slechts gebruik in sommige schema&#39;s onder deze klasse kan zien, kunt u het aan die schema&#39;s willen toevoegen door [een veldgroep maken](./field-groups.md#create) in plaats daarvan.

An **[!UICONTROL Untitled Field]** wordt de tijdelijke aanduiding weergegeven in het canvas en wordt de rechterrails bijgewerkt om besturingselementen weer te geven waarmee de eigenschappen van het veld worden geconfigureerd. Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Class]**.

![](../../images/ui/resources/classes/assign-to-class.png)

![](../../images/ui/resources/classes/assign-to-class.png)

Zie de handleiding op [velden definiëren in de gebruikersinterface](../fields/overview.md#define) voor specifieke stappen op om het gebied aan de klasse te vormen en toe te voegen. Ga door met het toevoegen van zoveel velden als nodig zijn voor de klasse. Selecteer **[!UICONTROL Save]** om zowel het schema als de klasse op te slaan.

![](../../images/ui/resources/classes/save.png)

Als u eerder schema&#39;s hebt gecreeerd die deze klasse gebruiken, zullen de onlangs toegevoegde gebieden automatisch in die schema&#39;s verschijnen.

## De klasse van een schema wijzigen {#schema}

U kunt de klasse van het schema op elk gewenst moment tijdens het eerste ontwerpproces wijzigen voordat het is opgeslagen. Zie de handleiding op [schema&#39;s maken en bewerken](./schemas.md#change-class) voor meer informatie .

## Volgende stappen

In dit document wordt beschreven hoe u klassen kunt maken en bewerken met de gebruikersinterface van het platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie de [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).

Leren hoe u klassen kunt beheren met de opdracht [!DNL Schema Registry] API, zie [hulplijn voor klassen eindpunt](../../api/classes.md).
