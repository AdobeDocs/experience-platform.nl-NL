---
keywords: Experience Platform;huis;populaire onderwerpen;laat dataset toe;Dataset;dataset
solution: Experience Platform
title: UI-gids voor gegevensbestanden
description: Leer hoe u algemene handelingen uitvoert wanneer u werkt met gegevenssets in de Adobe Experience Platform-gebruikersinterface.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2896'
ht-degree: 0%

---

# UI-gids voor gegevensbestanden

Deze gebruikershandleiding bevat instructies voor het uitvoeren van veelvoorkomende handelingen bij het werken met gegevenssets in de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze gebruikershandleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Gegevenssets](overview.md): De opslag- en beheerconstructie voor gegevenspersistentie in [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Schema-editor](../../xdm/tutorials/create-schema-ui.md): Leer hoe u uw eigen aangepaste XDM-schema&#39;s kunt maken met de [!DNL Schema Editor] binnen de [!DNL Platform] gebruikersinterface.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Zorg ervoor dat de regels, beperkingen en beleidsregels met betrekking tot het gebruik van klantgegevens worden nageleefd.

## Gegevensbestanden weergeven {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Negatieve getallen in gegevenssetactiviteit"
>abstract="Negatieve getallen in geneste records betekenen dat een gebruiker bepaalde batches in een geselecteerd tijdbereik heeft verwijderd."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="Vervaldatum gegevensset"
>abstract="Deze kolom wijst op het aantal dagen dat de doeldataset heeft verlaten alvorens het automatisch verloopt."

In de [!DNL Experience Platform] UI, selecteer **[!UICONTROL Datasets]** in de linkernavigatie om het dialoogvenster **[!UICONTROL Datasets]** dashboard. Het dashboard maakt een lijst van alle beschikbare datasets voor uw organisatie. De details worden getoond voor elke vermelde dataset, met inbegrip van zijn naam, het schema de dataset zich aan, en status van de meest recente versiereeks houdt.

![De interface Platform met het item Datasets gemarkeerd in de linkernavigatiebalk.](../images/datasets/user-guide/browse-datasets.png)

Selecteer de naam van een gegevensset in het menu [!UICONTROL Browse] tabblad voor toegang tot **[!UICONTROL Dataset activity]** scherm en zie details van de dataset u selecteerde. Het activiteitenlusje omvat een grafiek die het tarief visualiseert van berichten die worden verbruikt evenals een lijst van succesvolle en ontbroken partijen.

![De metriek en de visualisaties van uw geselecteerde dataset worden benadrukt.](../images/datasets/user-guide/dataset-activity-1.png)
![De steekproefpartijen die op uw geselecteerde dataset betrekking hebben worden benadrukt.](../images/datasets/user-guide/dataset-activity-2.png)

## Meer handelingen {#more-actions}

U kunt [!UICONTROL Delete] of [!UICONTROL Enable a dataset for Profile] van de [!UICONTROL Dataset] gedetailleerde weergave. Selecteer **[!UICONTROL ... More]** in de rechterbovenhoek van de gebruikersinterface. Het vervolgkeuzemenu wordt weergegeven.

![De werkruimte Datasets met de [!UICONTROL ... More] vervolgkeuzemenu gemarkeerd.](../images/datasets/user-guide/more-actions.png)

Als u **[!UICONTROL Enable a dataset for Profile]** verschijnt er een bevestigingsvenster. Selecteren **[!UICONTROL Enable]** om uw keuze te bevestigen.

>[!NOTE]
>
>Om een dataset voor Profiel toe te laten, moet het schema dat de dataset zich aan voor gebruik in het Profiel van de Klant in real time aansluit compatibel zijn. Zie de [Een gegevensset voor profiel inschakelen](#enable-profile) voor meer informatie.

![Het bevestigingsdialoogvenster Gegevensset inschakelen.](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

Als u **[!UICONTROL Delete]** de [!UICONTROL Delete dataset] bevestigingsvenster verschijnt. Selecteren **[!UICONTROL Delete]** om uw keuze te bevestigen.

>[!NOTE]
>
>U kunt geen systeemdatasets schrappen.

U kunt een dataset of een dataset voor gebruik met het Profiel van de Klant in real time van de gealigneerde acties ook schrappen die op worden gevonden [!UICONTROL Browse] tab. Zie de [sectie inline-handelingen](#inline-actions) voor meer informatie .

![Het dialoogvenster Gegevensset verwijderen.](../images/datasets/user-guide/delete-confirmation-dialog.png)

## Handelingen voor inline-gegevenssets {#inline-actions}

De datasets UI biedt nu een inzamelingen van gealigneerde acties voor elke beschikbare dataset aan. Selecteer de ellips (...) van een dataset die u wilt leiden om de beschikbare opties in een pop-up menu te zien. De beschikbare acties omvatten:

* [[!UICONTROL Preview dataset]](#preview),
* [[!UICONTROL Manage data and access labels]](#manage-and-enforce-data-governance)
* [[!UICONTROL Enable unified profile]](#enable-profile)
* [[!UICONTROL Manage tags]](#manage-tags)
* [[!UICONTROL Move to folders]](#move-to-folders)
* [[!UICONTROL Delete]](#delete).

Meer informatie over deze beschikbare acties vindt u in de desbetreffende secties. Leren hoe te om grote aantallen datasets gelijktijdig te beheren, verwijs naar [bulkacties](#bulk-actions) sectie.

### Een voorbeeld van een gegevensset bekijken {#preview}

U kunt voorbeeldgegevens van gegevenssets voorvertonen met de inline-opties van het dialoogvenster [!UICONTROL Browse] en ook de [!UICONTROL Dataset activity] weergeven. Van de [!UICONTROL Browse] selecteert u de ovalen (...) naast de naam van de gegevensset waarvan u een voorvertoning wilt weergeven. Er wordt een menulijst met opties weergegeven. Selecteer vervolgens **[!UICONTROL Preview dataset]** in de lijst met beschikbare opties. Als de dataset leeg is, zal de voorproefverbinding worden gedeactiveerd en in plaats daarvan zal zeggen dat de voorproef niet beschikbaar is.

![Het Browse lusje van de werkruimte van Datasets met de ellips en de optie van de dataset van de Voorproef die voor de gekozen dataset wordt benadrukt.](../images/datasets/user-guide/preview-dataset-option.png)

Dit opent het voorproefvenster, waar de hiërarchische mening van het schema voor de dataset op het recht wordt getoond.

![De de voorproefdialoog van de dataset met informatie over de structuur, evenals steekproefwaarden, voor de dataset wordt getoond.](../images/datasets/user-guide/preview-dataset.png)

Alternatief, van **[!UICONTROL Dataset activity]** scherm, selecteren **[!UICONTROL Preview dataset]** in de rechterbovenhoek van het scherm om maximaal 100 rijen met gegevens voor te vertonen.

![De knoop van de dataset van de Voorproef wordt benadrukt.](../images/datasets/user-guide/select-preview.png)

Voor robuustere methoden voor toegang tot uw gegevens, [!DNL Experience Platform] levert downstreamdiensten, zoals [!DNL Query Service] en [!DNL JupyterLab] gegevens te verkennen en te analyseren. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van Query Service](../../query-service/home.md)
* [Gebruikershandleiding voor JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

### Beheer van gegevens beheren en afdwingen op een gegevensset {#manage-and-enforce-data-governance}

U kunt de labels voor gegevensbeheer voor een dataset beheren door de inlineopties van het dialoogvenster [!UICONTROL Browse] tab. Selecteer de ovalen (...) naast de naam van de gegevensset die u wilt beheren, gevolgd door **[!UICONTROL Manage data and access labels]** in het vervolgkeuzemenu.

Met labels voor gegevensgebruik, toegepast op schemaniveau, kunt u gegevenssets en velden categoriseren volgens het gebruiksbeleid dat van toepassing is op die gegevens. Zie de [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie over labels, of raadpleegt u de [gebruikershandleiding voor gegevensgebruikslabels](../../data-governance/labels/overview.md) voor instructies op hoe te om etiketten op schema&#39;s voor propagatie op datasets toe te passen.

## Een gegevensset inschakelen voor realtime-klantprofiel {#enable-profile}

Elke dataset heeft de capaciteit om klantenprofielen met zijn ingebedde gegevens te verrijken. Om dit te doen, moet het schema dat de dataset hanteert voor gebruik binnen compatibel zijn [!DNL Real-Time Customer Profile]. Een compatibel schema voldoet aan de volgende vereisten:

* Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
* Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.

Voor meer informatie over het inschakelen van een schema voor [!DNL Profile], zie de [Gebruikershandleiding voor Schema-editor](../../xdm/tutorials/create-schema-ui.md).

U kunt een dataset voor Profiel van zowel de gealigneerde opties van toelaten [!UICONTROL Browse] en ook de [!UICONTROL Dataset activity] weergeven. Van de [!UICONTROL Browse] tabblad van het [!UICONTROL Datasets] de werkruimte, selecteer de ellips van een dataset die u voor Profiel wilt toelaten. Er wordt een menulijst met opties weergegeven. Selecteer vervolgens **[!UICONTROL Enable unified profile]** in de lijst met beschikbare opties.

![Het tabblad Bladeren van de werkruimte Datasets met de ovalen en het verenigde profiel inschakelen gemarkeerd.](../images/datasets/user-guide/enable-for-profile.png)

Alternatief, van de dataset **[!UICONTROL Dataset activity]** scherm, selecteert u de **[!UICONTROL Profile]** schakelen binnen de **[!UICONTROL Properties]** kolom. Zodra toegelaten, zullen de gegevens die in de dataset worden opgenomen ook worden gebruikt om klantenprofielen te bevolken.

>[!NOTE]
>
>Als een dataset reeds gegevens bevat en dan toegelaten voor [!DNL Profile], worden de bestaande gegevens niet automatisch verbruikt door [!DNL Profile]. Nadat een dataset wordt toegelaten voor [!DNL Profile], wordt u aangeraden alle bestaande gegevens opnieuw in te voeren om ervoor te zorgen dat deze bijdragen aan de profielen van klanten.

![De schakeloptie Profiel wordt gemarkeerd in de detailpagina van de gegevensset.](../images/datasets/user-guide/enable-dataset-profiles.png)

Datasets die voor Profiel zijn ingeschakeld, kunnen ook op deze criteria worden gefilterd. Zie de sectie over hoe te [gegevenssets waarvoor filterprofiel is ingeschakeld](#filter-profile-enabled-datasets) voor meer informatie .

### Gegevenssetcodes beheren {#manage-tags}

Voeg aangepaste gemaakte tags toe om gegevenssets te ordenen en zoek-, filter- en sorteermogelijkheden te verbeteren. Van de [!UICONTROL Browse] tabblad van het [!UICONTROL Datasets] werkruimte, selecteer de ellips van een dataset die u wilt leiden gevolgd door **[!UICONTROL Manage tags]** in het vervolgkeuzemenu.

![Het Browse lusje van de werkruimte van Datasets met de ellips en de Manage markeringsoptie die voor de gekozen dataset wordt benadrukt.](../images/datasets/user-guide/manage-tags.png)

De [!UICONTROL Manage tags] wordt weergegeven. Voer een korte beschrijving in om een aangepaste tag te maken of kies een reeds bestaande tag om uw gegevensset een label te geven. Selecteren **[!UICONTROL Save]** om uw instellingen te bevestigen.

![Het dialoogvenster Tags beheren met aangepaste tags gemarkeerd.](../images/datasets/user-guide/manage-tags-dialog.png)

De [!UICONTROL Manage tags] kan de dialoog ook bestaande markeringen uit een dataset verwijderen. Selecteer gewoon de &#39;x&#39; naast de tag die u wilt verwijderen en selecteer **[!UICONTROL Save]**.

Zodra een markering aan een dataset is toegevoegd, kunnen de datasets worden gefiltreerd gebaseerd op de overeenkomstige markering. Zie de sectie over hoe te [filteren, gegevenssets op tags](#enable-profile) voor meer informatie .

Voor meer informatie over hoe te om bedrijfsvoorwerpen voor gemakkelijkere ontdekking en categorisering te classificeren, zie de gids over [beheren, taxonomieën van metagegevens](../../administrative-tags/ui/managing-tags.md). In deze handleiding wordt beschreven hoe een gebruiker met de juiste machtigingen vooraf gedefinieerde tags kan maken, categorieën aan tags kan toewijzen en alle gerelateerde CRUD-bewerkingen kan uitvoeren op tags en tagcategorieën in de gebruikersinterface van het platform.

### Verplaatsen naar mappen {#move-to-folders}

U kunt datasets binnen omslagen voor beter gegevenssetbeheer plaatsen. Om een dataset in een omslag te bewegen, selecteer de ellipsen (...) naast de datasetnaam u wenst te leiden, die door wordt gevolgd **[!UICONTROL Move to folder]** in het vervolgkeuzemenu.

![De [!UICONTROL Datasets] dashboard met de ellipsen en [!UICONTROL Move to folder] gemarkeerd.](../images/datasets/user-guide/move-to-folder.png)

De [!UICONTROL Move] dataset aan omslagdialoog verschijnt. Selecteer de map waarnaar u het publiek wilt verplaatsen en selecteer **[!UICONTROL Move]**. Een popup bericht deelt u mee dat de datasetbeweging succesvol is geweest.

![De [!UICONTROL Move] dialoogvenster Gegevensset met [!UICONTROL Move] gemarkeerd.](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>U kunt mappen ook rechtstreeks maken vanuit het dialoogvenster Gegevensset verplaatsen. Als u een map wilt maken, selecteert u het pictogram Map maken (![Het pictogram Map maken.](../images/datasets/user-guide/create-folder-icon.png)) in de rechterbovenhoek van het dialoogvenster.
>
>![De [!UICONTROL Move] de dialoog van de dataset met creeer omslagpictogram benadrukte.](/help/catalog/images/datasets/user-guide/create-folder.png)

Zodra de dataset in een omslag is, kunt u verkiezen om datasets slechts te tonen die tot een specifieke omslag behoren. Als u de mappenstructuur wilt openen, selecteert u het pictogram voor het weergeven van mappen (![Het pictogram voor de weergavemappen](../images/datasets/user-guide/show-folders-icon.png)). Vervolgens selecteert u de gekozen map om alle bijbehorende gegevenssets weer te geven.

![De [!UICONTROL Datasets] dashboards met de getoonde de de omslagstructuur van datasets, het pictogram van showomslagen, en een geselecteerde benadrukte omslag.](../images/datasets/user-guide/folder-structure.png)

### Een gegevensset verwijderen {#delete}

U kunt een dataset van of de dataset gealigneerde acties in schrappen [!UICONTROL Browse] of de rechterbovenhoek van de [!UICONTROL Dataset activity] weergeven. Van de [!UICONTROL Browse] Selecteer de ovalen (...) naast de naam van de gegevensset die u wilt verwijderen. Er wordt een menulijst met opties weergegeven. Selecteer vervolgens **[!UICONTROL Delete]** in het vervolgkeuzemenu.

![Het Browse lusje van de werkruimte van Datasets met de ellips en de optie van de Schrapping die voor de gekozen dataset wordt benadrukt.](../images/datasets/user-guide/inline-delete-dataset.png)

Er wordt een bevestigingsvenster weergegeven. Selecteren **[!UICONTROL Delete]** ter bevestiging.

U kunt ook **[!UICONTROL Delete dataset]** van de **[!UICONTROL Dataset activity]** scherm.

>[!NOTE]
>
>Datasets die zijn gemaakt en gebruikt door Adobe-toepassingen en -services (zoals Adobe Analytics, Adobe Audience Manager of [!DNL Offer Decisioning]) kan niet worden verwijderd.

![De knoop van de dataset van de Schrapping wordt benadrukt binnen de datasetdetails pagina.](../images/datasets/user-guide/delete-dataset.png)

Er verschijnt een bevestigingsvak. Selecteren **[!UICONTROL Delete]** om de schrapping van de gegevensset te bevestigen.

![De bevestigingsmodus voor verwijdering wordt weergegeven met de knop Verwijderen gemarkeerd.](../images/datasets/user-guide/confirm-delete.png)

### Een voor profiel ingeschakelde gegevensset verwijderen

Als een dataset voor Profiel wordt toegelaten, zal het schrappen van die dataset door UI het van het gegevensmeer, de Dienst van de Identiteit, en ook om het even welke profielgegevens verbonden aan die dataset in de opslag van het Profiel schrappen.

U kunt profielgegevens die aan een dataset zijn gekoppeld, verwijderen uit de [!DNL Profile] de opslag (het verlaten van de gegevens in het gegevensmeer) gebruikend Real-Time API van het Profiel van de Klant. Zie de klasse [API-eindgids voor profielsysteemtaken](../../profile/api/profile-system-jobs.md).

## Gegevensbestanden zoeken en filteren {#search-and-filter}

Om de lijst van beschikbare datasets te zoeken of te filtreren, selecteer het filterpictogram (![Het filterpictogram.](../images/datasets/user-guide/icon.png)) linksboven in de werkruimte. Er wordt een set filteropties weergegeven in de linkertrack. Er zijn verscheidene methodes om uw beschikbare datasets te filtreren. Deze omvatten: [[!UICONTROL Show System Datasets]](#show-system-datasets), [[!UICONTROL Included in profile]](#filter-profile-enabled-datasets), [[!UICONTROL Tags]](#filter-by-tag), [[!UICONTROL Creation date]](#filter-by-creation-date), [[!UICONTROL Modified date], [!UICONTROL Created by]](#filter-by-creation-date), en [[!UICONTROL Schema]](#filter-by-schema).

De lijst met toegepaste filters wordt boven de gefilterde resultaten weergegeven.

![Het tabblad Bladeren van de werkruimte Datasets met de lijst met toegepaste filters gemarkeerd.](../images/datasets/user-guide/applied-filters.png)

### Systeemgegevenssets tonen {#show-system-datasets}

Door gebrek, slechts worden de datasets die u gegevens hebt ingebed in getoond. Als u de systeem-geproduceerde datasets wilt zien, selecteer **[!UICONTROL Yes]** Selectievakje in het dialoogvenster [!UICONTROL Show system datasets] sectie. Door het systeem gegenereerde gegevenssets worden alleen gebruikt om andere componenten te verwerken. De door het systeem gegenereerde profielexportgegevensset wordt bijvoorbeeld gebruikt om het profieldashboard te verwerken.

![De filteropties van de werkruimte Datasets met de [!UICONTROL Show system datasets] gemarkeerd.](../images/datasets/user-guide/show-system-datasets.png)

### Gegevenssets voor filterprofiel {#filter-profile-enabled-datasets}

De datasets die voor de gegevens van het Profiel zijn toegelaten worden gebruikt om klantenprofielen te bevolken nadat de gegevens zijn opgenomen. Zie de sectie over [gegevenssets inschakelen voor profiel](#enable-profile) voor meer informatie.

Om uw dataset te filtreren die op of zij voor Profiel zijn toegelaten, selecteer [!UICONTROL Yes] van de filteropties.

![De filteropties van de werkruimte Datasets met de [!UICONTROL Included in Profile] gemarkeerd.](../images/datasets/user-guide/included-in-profile.png)

### Gegevenssets filteren op tag {#filter-by-tag}

Voer in het dialoogvenster [!UICONTROL Tags] invoer, dan selecteer uw markering van de lijst van beschikbare opties aan onderzoek en filterdatasets die aan die markering beantwoorden.

![De filteropties van de werkruimte Datasets met de [!UICONTROL Tags] invoer- en filterpictogram gemarkeerd.](../images/datasets/user-guide/filter-tags.png)

### Gegevensbestanden filteren op aanmaakdatum {#filter-by-creation-date}

Datasets kunnen worden gefilterd op aanmaakdatum over een aangepaste tijdsperiode. Dit kan worden gebruikt om historische gegevens uit te sluiten of specifieke chronologische gegevens en rapportage te genereren. Kies een [!UICONTROL Start date] en [!UICONTROL End date] door het kalenderpictogram voor elk gebied te selecteren. Daarna, slechts datasets die aan die criteria voldoen zullen op het Browse lusje verschijnen.

### Gegevenssets filteren op gewijzigde datum {#filter-by-modified-date}

Net als bij het filter voor de aanmaakdatum kunt u de gegevenssets filteren op basis van de datum waarop deze voor het laatst zijn gewijzigd. In de [!UICONTROL Modified date] sectie, kies een [!UICONTROL Start date] en [!UICONTROL End date] door het kalenderpictogram voor elk gebied te selecteren. Daarna, slechts zullen de datasets die tijdens die periode werden gewijzigd in het Browse lusje verschijnen.

### Filteren op schema {#filter-by-schema}

U kunt datasets filtreren die op het schema worden gebaseerd dat hun structuur bepaalt. Selecteer het vervolgkeuzepictogram of voer de schemanaam in het tekstveld in. Er wordt een lijst weergegeven met mogelijke overeenkomsten. Selecteer het gewenste schema in de lijst.

## Bulkacties {#bulk-actions}

De bulkacties van het gebruik om uw operationele efficiency te verbeteren en veelvoudige acties op talrijke datasets gelijktijdig uit te voeren. U kunt tijd besparen en een geordende gegevensstructuur onderhouden met acties als [Verplaatsen naar map](#move-to-folders), [Codes bewerken](#manage-tags), en [Verwijderen](#delete) datasets.

Om op meer dan één dataset tezelfdertijd te handelen, selecteer individuele datasets met checkbox op elke rij, of selecteer een volledige pagina met het vakje van de kolomkopbal. Als deze optie is geselecteerd, wordt de algemene actiebalk weergegeven.

![De Datasets doorbladeren lusje met talrijke geselecteerde datasets en de bulk benadrukte actiebar.](../images/datasets/user-guide/bulk-actions.png)

Wanneer u bulkacties op datasets toepast, zijn de volgende voorwaarden van toepassing:

* U kunt datasets van verschillende pagina&#39;s van UI selecteren.
* Als u een filter selecteert, worden de geselecteerde datasets opnieuw ingesteld.

## Gegevenssets sorteren op gemaakte datum {#sort}

Gegevensbestanden in het dialoogvenster [!UICONTROL Browse] kan worden gesorteerd op oplopende of aflopende datums. Selecteer de [!UICONTROL Created] of [!UICONTROL Last updated] kolomkoppen die u wilt afwisselen tussen oplopend en aflopend. Als deze optie is geselecteerd, geeft de kolom dit aan met een pijl-omhoog of een pijl-omlaag naar de zijkant van de kolomkop.

![Het tabblad Bladeren van de werkruimte Datasets met de kolommen Gemaakt en Laatst bijgewerkt gemarkeerd.](../images/datasets/user-guide/ascending-descending-columns.png)

## Een gegevensset maken {#create}

Als u een nieuwe gegevensset wilt maken, selecteert u **[!UICONTROL Create dataset]** in de **[!UICONTROL Datasets]** dashboard.

![De knop Gegevensset maken is gemarkeerd.](../images/datasets/user-guide/select-create.png)

In het volgende scherm, wordt u voorgesteld met de volgende twee opties om een nieuwe dataset tot stand te brengen:

* [Gegevensset maken van schema](#schema)
* [Gegevensset maken van CSV-bestand](#csv)

### Creeer een dataset met een bestaand schema {#schema}

In de **[!UICONTROL Create dataset]** scherm, selecteren **[!UICONTROL Create dataset from schema]** om een nieuwe lege dataset te creëren.

![De Create dataset van schemaknoop wordt benadrukt.](../images/datasets/user-guide/create-dataset-schema.png)

De **[!UICONTROL Select schema]** wordt weergegeven. Blader door de schemalijst en selecteer het schema dat de dataset alvorens zal volgen te selecteren **[!UICONTROL Next]**.

![Er wordt een lijst met schema&#39;s weergegeven. Het schema dat zal worden gebruikt om de dataset tot stand te brengen wordt benadrukt.](../images/datasets/user-guide/select-schema.png)

De **[!UICONTROL Configure dataset]** wordt weergegeven. Geef de gegevensset een naam en een optionele beschrijving en selecteer **[!UICONTROL Finish]** om de dataset te creëren.

![De details van de configuratie van de dataset worden opgenomen. Dit omvat details zoals de naam en beschrijving van de dataset.](../images/datasets/user-guide/configure-dataset-schema.png)

Datasets kunnen van de lijst van beschikbare datasets in UI met de schemafilter worden gefiltreerd. Zie de sectie over hoe te [filterdatasets per schema](#filter-by-schema) voor meer informatie .

### Een gegevensset maken met een CSV-bestand {#csv}

Wanneer een dataset gebruikend een Csv- dossier wordt gecreeerd, wordt een ad hoc schema gecreeerd om de dataset van een structuur te voorzien die het verstrekte Csv- dossier aanpast. In de **[!UICONTROL Create dataset]** scherm, selecteren **[!UICONTROL Create dataset from CSV file]**.

![De Create dataset van Csv- dossierknoop wordt benadrukt.](../images/datasets/user-guide/create-dataset-csv.png)

De **[!UICONTROL Configure]** wordt weergegeven. Geef de gegevensset een naam en een optionele beschrijving en selecteer **[!UICONTROL Next]**.

![De details van de configuratie van de dataset worden opgenomen. Dit omvat details zoals de naam en beschrijving van de dataset.](../images/datasets/user-guide/configure-dataset-csv.png)

De **[!UICONTROL Add data]** wordt weergegeven. Upload het CSV-bestand door het naar het midden van het scherm te slepen of selecteer **[!UICONTROL Browse]** om uw bestandsmap te verkennen. Het bestand kan maximaal tien gigabyte groot zijn. Selecteer **[!UICONTROL Save]** om de dataset te creëren.

>[!NOTE]
>
>CSV-kolomnamen moeten beginnen met alfanumerieke tekens en mogen alleen letters, cijfers en onderstrepingstekens bevatten.

![Het gegevensscherm Toevoegen wordt weergegeven. De plaats waar u het Csv- dossier voor de dataset kunt uploaden wordt benadrukt.](../images/datasets/user-guide/add-csv-data.png)

## Gegevens bijhouden

In de [!DNL Experience Platform] UI, selecteer **[!UICONTROL Monitoring]** in de linkernavigatie. De **[!UICONTROL Monitoring]** in het dashboard kunt u de status van binnenkomende gegevens van batch- of streaming invoer bekijken. Als u de status van afzonderlijke batches wilt weergeven, selecteert u **[!UICONTROL Batch end-to-end]** of **[!UICONTROL Streaming end-to-end]**. De dashboards maken een lijst van alle partij of het stromen ingangen, met inbegrip van die die succesvol zijn, ontbroken, of nog lopend. Elke lijst verstrekt details van de partij, met inbegrip van partijidentiteitskaart, de naam van de doeldataset, en het aantal verslagen die worden opgenomen. Als de doeldataset wordt toegelaten voor [!DNL Profile], wordt ook het aantal opgenomen identiteits- en profielrecords weergegeven.

![Het controlebatch-end-to-end scherm wordt weergegeven. Zowel controle als partij-aan-partij worden benadrukt.](../images/datasets/user-guide/batch-listing.png)

U kunt op een individu selecteren **[!UICONTROL Batch ID]** toegang tot **[!UICONTROL Batch overview]** dashboard en zie details voor de partij, met inbegrip van foutenlogboeken als de partij niet opneemt.

![Details van de geselecteerde batch worden weergegeven. Dit omvat het aantal verslagen die worden opgenomen, het aantal verslagen ontbrak, de partijstatus, de dossiergrootte, de ingangsbegin en eindtijden, de dataset en partij IDs, organisatie identiteitskaart, de datasetnaam, en de toegangsinformatie.](../images/datasets/user-guide/batch-overview.png)

Als u de batch wilt verwijderen, selecteert u **[!UICONTROL Delete batch]** rechts boven in het dashboard. Als u een batch verwijdert, verwijdert u ook de records uit de gegevensset waarin de batch oorspronkelijk was opgenomen.

>[!NOTE]
>
>Als de ingesloten gegevens zijn ingeschakeld voor Profiel en zijn verwerkt, worden deze gegevens niet verwijderd wanneer u een batch verwijdert uit het archief Profiel.

![De de partijknoop van de Schrapping wordt benadrukt op de datasetdetails pagina.](../images/datasets/user-guide/delete-batch.png)

## Volgende stappen

Deze gebruikershandleiding bevat instructies voor het uitvoeren van algemene handelingen bij het werken met gegevenssets in het dialoogvenster [!DNL Experience Platform] gebruikersinterface. Voor stappen om gemeenschappelijk uit te voeren [!DNL Platform] de werkschema&#39;s die datasets impliceren, te verwijzen naar de volgende leerprogramma&#39;s:

* [Een gegevensset maken met behulp van API&#39;s](create.md)
* [De gegevens van de dataset van de vraag gebruikend de Toegang API van Gegevens](../../data-access/home.md)
* [Een gegevensset configureren voor realtime profiel en identiteitsservice van klanten met behulp van API&#39;s](../../profile/tutorials/dataset-configuration.md)
