---
title: Bronobjecten in de gebruikersinterface filteren
description: Leer hoe te door uw bronvoorwerpen zoals rekeningen en dataflows in de UI van het Experience Platform te navigeren.
hide: true
hidefromtoc: true
exl-id: 59c200cc-1be7-45a8-9d7a-55e6f11dbcf2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 0%

---

# Bronobjecten filteren in de gebruikersinterface

Gebruik de gereedschappen voor filteren, zoeken en inline-handelingen in de Adobe Experience Platform-gebruikersinterface om de workflow in de [!UICONTROL Sources] werkruimte

* Het filtreren en onderzoeksmogelijkheden van het gebruik om uw weg door bronrekeningen en dataflows in uw organisatie te navigeren.
* Gebruik inline handelingen om configuratie-instellingen te wijzigen die worden toegepast op uw gegevensstromen en om organisatorische workflows te verbeteren. U kunt inline-handelingen gebruiken om tags toe te passen, waarschuwingen in te stellen of om innemingstaken op aanvraag te maken.

## Aan de slag

Het is handig om inzicht te krijgen in de volgende functies en concepten van Experience Platforms voordat u gaat werken met de gereedschappen voor objectnavigatie in de werkruimte Bronnen:

* [Bronnen](../../home.md): Gebruik bronnen in Experience Platform om gegevens van een Adobe of een gegevensbron van derden in te voeren.
* [Administratieve tags](../../../administrative-tags/overview.md): Gebruik beheertags om trefwoorden voor metagegevens toe te passen op uw objecten en schakel zoekopdracht in om dat object te zoeken in het ecosysteem van het Experience Platform.
* [Waarschuwingen](../../../observability/home.md): Gebruik waarschuwingen om meldingen te ontvangen die een update bevatten van de status van objecten, zoals de gegevensstroom van uw bronnen.
* [Gegevensstromen](../../../dataflows/home.md): Dataflows are representations of data jobs that move data across Experience Platform. U kunt de werkruimte van bronnen gebruiken om gegevensstromen tot stand te brengen die gegevens van een bepaalde bron aan Experience Platform opnemen.
* [Gegevenssets](../../../catalog/datasets/user-guide.md): Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat.
* [Sandboxen](../../../sandboxes/home.md): Gebruik sandboxen in Experience Platform om virtuele partities te maken tussen de exemplaren van uw Experience Platform en om omgevingen te maken die specifiek zijn voor ontwikkeling of productie.

## Gegevensstromen van bronnen filteren {#filter-sources-dataflows}

Selecteer in de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Dataflows]** in de bovenste koptekst.

![De pagina met gegevensstromen in de werkruimte Bronnen](../../images/tutorials/filter/dataflows-page.png)

Standaard wordt het filtermenu links van de interface weergegeven. Selecteer **[!UICONTROL Hide filters]**.

![De geselecteerde filteroptie voor verbergen.](../../images/tutorials/filter/hide-filters.png)

U kunt uw brongegevens filteren op de volgende parameters:

| Filter | Beschrijving |
| --- | --- |
| [Bronplatform](#filter-dataflows-by-source-platform) | Filter de gegevensstromen op basis van de bron waarmee ze zijn gemaakt. |
| [Tags](#filter-dataflows-by-tags) | Filter de gegevensstroom op basis van de tags die erop zijn toegepast. |
| [Status](#filter-dataflows-by-status) | Filter uw gegevensstromen op basis van hun huidige status. |
| [Doelgegevensset](#filter-dataflows-by-target-dataset) | Filter uw gegevensstromen die op de doeldataset worden gebaseerd zij met werden gecreeerd. |
| [Accountnaam](#filter-dataflows-by-account-name) | Filter de gegevensstromen op basis van de naam van de account waarmee ze overeenkomen. |
| [Gemaakt door](#filter-dataflows-by-user) | Filter de gegevensstroom op basis van wie deze heeft gemaakt. |
| [Aanmaakdatum](#filter-dataflows-by-creation-date) | Filter de gegevensstromen op basis van de datum waarop ze zijn gemaakt. |
| [Datum gewijzigd](#filter-dataflows-by-modification-date) | Filter de gegevensstromen op basis van de datum waarop ze voor het laatst zijn bijgewerkt. |

### Gegevens filteren op bronplatform {#filter-dataflows-by-source-platform}

Gebruik de [!UICONTROL Source platform] om de gegevens te filteren op het type bron. U kunt een bepaalde bron typen of het vervolgkeuzemenu gebruiken om een lijst met bronnen in de catalogus weer te geven. U kunt ook filteren op verschillende bronnen voor een bepaalde query. U kunt bijvoorbeeld [!DNL Amazon S3], [!DNL Azure Data Lake Storage Gen2], en [!DNL Google Cloud Storage] om de catalogus bij te werken en alleen de gegevensstromen weer te geven die met de geselecteerde bronnen zijn gemaakt.

### Gegevens filteren op labels {#filter-dataflows-by-tags}

Gebruik het venster Codes om de gegevensstromen te filteren op basis van de respectievelijke codes.

Selecteren **[!UICONTROL Has any tag]** en selecteert u vervolgens de tags die u wilt filteren met het vervolgkeuzemenu. Gebruik deze instelling om te filteren op gegevensstromen met een van de tags die u hebt geselecteerd.

![Een vraag om gegevens te filtreren stroomt door om het even welke markering.](../../images/tutorials/filter/has-any-tag.png)

Selecteren **[!UICONTROL Has all tags]** en selecteert u vervolgens de tags die u wilt filteren met het vervolgkeuzemenu. Gebruik deze instelling om te filteren op gegevensstromen met alle tags die u hebt geselecteerd.

![Een query voor het filteren van gegevens wordt uitgevoerd op alle tags.](../../images/tutorials/filter/has-all-tags.png)

### Gegevens filteren op status {#filter-dataflows-by-status}

U kunt filteren op status met de opdracht [!UICONTROL Status] deelvenster.

| Status | Beschrijving |
| --- | --- |
| Ingeschakeld | Selecteren **[!UICONTROL Enabled]** om de weergave te filteren en alleen actieve gegevensstromen weer te geven. |
| Uitgeschakeld | Selecteren **[!UICONTROL Disabled]** om de weergave te filteren en alleen gedeactiveerde gegevens weer te geven. |
| Concept | Selecteren **[!UICONTROL Draft]** om uw mening te filtreren en slechts gegevens te tonen die op ontwerp wijze zijn. |

### Gegevens filteren op doelgegevensset {#filter-dataflows-by-target-dataset}

Selecteren **[!UICONTROL Target dataset]** om tot een dropdown menu van alle doeldatasets toegang te hebben. Dan, selecteer een doeldataset om uw mening te filtreren en slechts de dataflows te tonen die gebruikend uw gespecificeerde doeldatasets werden gecreeerd.

### Gegevens filteren op accountnaam {#filter-dataflows-by-account-name}

Selecteren **[!UICONTROL Account name]** voor toegang tot een vervolgkeuzemenu van alle accounts. Selecteer vervolgens een account om de weergave te filteren en de gegevensstromen weer te geven die door uw geselecteerde account zijn gemaakt.

### Gegevens filteren op gebruiker {#filter-dataflows-by-user}

Gebruik de [!UICONTROL Created by] om gegevens te filteren door de gebruiker die de gegevensstromen heeft gemaakt of voor het laatst bijgewerkt. Selecteer de vervolgkeuzelijst en selecteer vervolgens de gebruikersnaam waarop u de gegevensstromen wilt filteren.

### Gegevens filteren op aanmaakdatum {#filter-dataflows-by-creation-date}

U kunt de gegevens filteren op de aanmaakdatum. In de [!UICONTROL Created date] een begindatum en einddatum configureren om een tijdframevenster te maken en uw weergave filteren zodat alleen de gegevens worden weergegeven die in dat venster zijn gemaakt.

U kunt uw tijdkader vormen door uw begin en einddatum in te voeren. U kunt ook het kalenderpictogram selecteren en de kalender gebruiken om uw datums te configureren.

U kunt ook dezelfde stappen uitvoeren, maar filtergegevens worden op de laatste wijzigingsdatum toegepast, in tegenstelling tot de aanmaakdatum.

### Gegevens filteren op wijzigingsdatum {#filter-dataflows-by-modification-date}

Op dezelfde manier kunt u dezelfde principes toepassen en de gegevensstroom filteren op de wijzigingsdatum. Gebruik de **[!UICONTROL Modified date]** om een bepaald tijdkader te vormen en uw mening te filtreren om slechts dataflows te tonen die tijdens die periode zijn gewijzigd.

### Filters combineren {#combine-filters}

U kunt verschillende filters combineren om uw zoekopdracht te verbreden of te verkleinen. In het onderstaande voorbeeld wordt een filter toegepast op het zoeken naar:

* Gegevensstromen die zijn gemaakt met de [!DNL Amazon S3] bron.
* Gegevensstromen die de **[!DNL ACME]** -tag.
* Datalfows die momenteel zijn ingeschakeld.
* Gegevensstromen die zijn gemaakt met de [!DNL Loyalty Dataset B2C] dataset.
* Dataflows die tussen 19-4-2024 en 19-4-2024 zijn gemaakt.

![Een vervolgkeuzevenster waarin alle toegepaste filters worden weergegeven.](../../images/tutorials/filter/combine-filters.png)

Selecteer **[!UICONTROL Clear all]**.

![Alle geselecteerde opties wissen.](../../images/tutorials/filter/clear-all.png)

## Bronaccounts filteren {#filter-sources-accounts}

Selecteer in de gebruikersinterface van het Experience Platform de optie [!UICONTROL Sources] in de linkernavigatie en selecteer vervolgens **[!UICONTROL Accounts]** in de bovenste koptekst. U kunt uw bronrekeningen filtreren die op de bron worden gebaseerd dat zij met of de gebruiker werden gecreeerd die hen creeerde.

![De pagina Accounts in de werkruimte Bronnen](../../images/tutorials/filter/accounts.png)

## Zoeken naar accounts en gegevensstromen {#search-for-accounts-and-dataflows}

U kunt de efficiëntie versnellen door met de zoekbalk onmiddellijk naar een bepaalde account of gegevensstroom te navigeren.

>[!BEGINTABS]

>[!TAB Zoeken naar gegevens]

Gebruik de zoekbalk in het dialoogvenster [!UICONTROL Dataflows] pagina om een specifieke gegevensstroom te zoeken. U kunt naar een gegevensstroom zoeken gebruikend zijn naam of beschrijving.

![Een zoekquery voor een ACME-gegevensstroom](../../images/tutorials/filter/search-dataflow.png)

>[!TAB Zoeken naar accounts]

Gebruik de zoekbalk in het dialoogvenster [!UICONTROL Accounts] pagina om een specifieke account te zoeken. U kunt een account zoeken op basis van de naam of beschrijving.

![Een zoekquery voor een april-account](../../images/tutorials/filter/search-account.png)

>[!ENDTABS]

## Inline-handelingen voor gegevensstromen van bronnen {#inline-actions-for-sources-dataflows}

De ovalen selecteren (`...`) naast de naam van een gegevensstroom voor een lijst van gealigneerde acties die u kunt gebruiken om wijzigingen in uw gegevensstroom aan te brengen.

![De selectie van inline-handelingen waaruit u kunt kiezen voor een bepaalde gegevensstroom.](../../images/tutorials/filter/inline-actions.png)

| Inline-handelingen | Beschrijving |
| --- | --- |
| [!UICONTROL Edit schedule] | Selecteren **[!UICONTROL Edit schedule]** om het schema voor inname van uw gegevensstroom bij te werken. Een gegevensstroom die is geplaatst aan éénmalige ingestie kan niet worden uitgegeven. |
| [!UICONTROL Disable dataflow] | Selecteren **[!UICONTROL Disable dataflow]** om een dataflow-run te deactiveren. Met deze optie wordt de gegevensstroom niet verwijderd. |
| [!UICONTROL View in monitoring] | Selecteren **[!UICONTROL View in monitoring]** om de metriek en de status van uw gegevensstroom in het controledashboard te bekijken. Lees voor meer informatie de handleiding op [gegevensstromen van bronnen controleren](../../../dataflows/ui/monitor-sources.md). |
| [!UICONTROL Delete] | Selecteren **[!UICONTROL Delete]** om uw gegevensstroom te verwijderen. |
| [!UICONTROL Run on-demand] | Selecteren **[!UICONTROL Run on-demand]** om één enkele herhaling van een dataflow looppas teweeg te brengen. Lees voor meer informatie de handleiding op [het creëren van een runtime van de gegevensstroom op bestelling](../ui/on-demand-ingestion.md). |
| [!UICONTROL Subscribe to alerts] | Selecteren **[!UICONTROL Subscribe to alerts]** om een pop-upvenster weer te geven met waarschuwingen waarop u zich kunt abonneren: <ul><li>Het Begin van de Looppas van Gegevensstroom van bronnen: Selecteer dit alarm om een bericht te ontvangen wanneer uw dataflow looppas op bestelling begint.</li><li>Bronnen Dataflow Run Success: selecteer dit alarm om een bericht te ontvangen wanneer uw runtime op bestelling met succes voltooit.</li><li>Bronnen Dataflow Run mislukt: selecteer deze waarschuwing wanneer de uitvoering van de gegevensstroom op aanvraag mislukt als gevolg van fouten.</li></ul> Lees voor meer informatie de handleiding op [abonneren op waarschuwingen voor gegevensstromen van bronnen](../ui/alerts.md). |
| [!UICONTROL Add to package] | Selecteren **[!UICONTROL Add to package]** om de gegevensstroom toe te voegen aan een pakket en deze te exporteren voor gebruik in een andere sandbox. Tijdens deze stap kunt u een nieuw pakket maken of de gegevensstroom toevoegen aan een bestaand pakket. Voor meer informatie raadpleegt u de handleiding [sandbox, gereedschap](../../../sandboxes/ui/sandbox-tooling.md). |
| [!UICONTROL Manage tags] | Selecteren **[!UICONTROL Manage tags]** om tags toe te voegen aan of te verwijderen uit uw gegevensstroom. Gebruik labels voor het beheer van metagegevenstaxonomieën en het classificeren van bedrijfsobjecten, zodat u deze eenvoudiger kunt herkennen en indelen. Lees voor meer informatie de handleiding op [tags beheren](../../../administrative-tags/ui/managing-tags.md). |

## Volgende stappen

Door dit document te lezen hebt u geleerd hoe u door de pagina&#39;s met bronaccounts en gegevensstromen kunt navigeren. Lees voor meer informatie over bronnen de [overzicht van bronnen](../../home.md).
