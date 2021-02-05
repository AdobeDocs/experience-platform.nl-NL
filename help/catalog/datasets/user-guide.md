---
keywords: Experience Platform;huis;populaire onderwerpen;laat dataset toe;Dataset;dataset
solution: Experience Platform
title: UI-gids voor gegevensbestanden
topic: datasets
description: Leer hoe u algemene handelingen uitvoert wanneer u werkt met gegevenssets in de Adobe Experience Platform-gebruikersinterface.
translation-type: tm+mt
source-git-commit: 2b8c08dad34bcd69368c00050323835f05379c82
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 0%

---


# UI-gids voor gegevensbestanden

Deze gebruikershandleiding bevat instructies voor het uitvoeren van veelvoorkomende handelingen bij het werken met gegevenssets in de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze gebruikershandleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Gegevenssets](overview.md): De opslag- en beheerconstructie voor gegevenspersistentie in  [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Schema-editor](../../xdm/tutorials/create-schema-ui.md): Leer hoe u uw eigen aangepaste XDM-schema&#39;s maakt met behulp van de  [!DNL Schema Editor]   [!DNL Platform] gebruikersinterface.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Ervoor zorgen dat de regels, beperkingen en beleidsregels betreffende het gebruik van klantgegevens worden nageleefd.

## Gegevensbestanden weergeven

In [!DNL Experience Platform] UI, klik **[!UICONTROL Datasets]** in linkernavigatie om **[!UICONTROL Datasets]** dashboard te openen. Het dashboard maakt een lijst van alle beschikbare datasets voor uw organisatie. De details worden getoond voor elke vermelde dataset, met inbegrip van zijn naam, het schema de dataset zich aan, en status van de meest recente versiereeks houdt.

![](../images/datasets/user-guide/browse_datasets.png)

Klik de naam van een dataset om tot zijn **[!UICONTROL Dataset activiteit]** scherm toegang te hebben en details van de dataset te zien u selecteerde. Het activiteitenlusje omvat een grafiek die het tarief visualiseert van berichten die worden verbruikt evenals een lijst van succesvolle en ontbroken partijen.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Een voorbeeld van een gegevensset bekijken

Klik in het scherm **[!UICONTROL Datasetactiviteit]** op **[!UICONTROL Gegevensset voorvertonen]** in de rechterbovenhoek van het scherm om een voorvertoning weer te geven van maximaal 100 rijen met gegevens. Als de dataset leeg is, zal de voorproefverbinding worden gedeactiveerd en in plaats daarvan zal zeggen dat de voorproef niet beschikbaar is.

![](../images/datasets/user-guide/click_to_preview.png)

In het voorproefvenster, wordt de hiërarchische mening van het schema voor de dataset getoond op het recht.

![](../images/datasets/user-guide/preview_dataset.png)

[!DNL Experience Platform] biedt downstreamservices zoals [!DNL Query Service] en [!DNL JupyterLab] voor het verkennen en analyseren van gegevens voor robuustere methoden voor toegang tot uw gegevens. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van Query Service](../../query-service/home.md)
* [Gebruikershandleiding voor JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Een gegevensset {#create} maken

Als u een nieuwe gegevensset wilt maken, klikt u op **[!UICONTROL Gegevensset maken]** in het **[!UICONTROL Datasets]**-dashboard.

![](../images/datasets/user-guide/click_to_create.png)

In het volgende scherm, wordt u voorgesteld met de volgende twee opties om een nieuwe dataset tot stand te brengen:

* [Gegevensset maken van schema](#schema)
* [Gegevensset maken van CSV-bestand](#csv)

### Maak een dataset met een bestaand schema {#schema}

Klik in het scherm **[!UICONTROL Gegevensset maken]** op **[!UICONTROL Gegevensset maken van schema]** om een nieuwe lege gegevensset te maken.

![](../images/datasets/user-guide/create_dataset_schema.png)

De stap **[!UICONTROL Selecteer schema]** wordt weergegeven. Blader door het schema en selecteer het schema waaraan de dataset zich zal houden alvorens **[!UICONTROL Next]** te klikken.

![](../images/datasets/user-guide/select_schema.png)

De stap **[!UICONTROL Gegevensset configureren]** wordt weergegeven. Geef de gegevensset een naam en een optionele beschrijving en klik vervolgens op **[!UICONTROL Voltooien]** om de gegevensset te maken.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Een gegevensset maken met een CSV-bestand {#csv}

Wanneer een dataset gebruikend een Csv- dossier wordt gecreeerd, wordt een ad hoc schema gecreeerd om de dataset van een structuur te voorzien die het verstrekte Csv- dossier aanpast. Klik in het scherm **[!UICONTROL Gegevensset maken]** op het vakje **[!UICONTROL Gegevensset maken van CSV-bestand]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

De stap **[!UICONTROL Configure]** verschijnt. Geef de gegevensset een naam en een optionele beschrijving en klik op **[!UICONTROL Volgende]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

De stap **[!UICONTROL Gegevens toevoegen]** wordt weergegeven. Upload het CSV-bestand door het naar het midden van het scherm te slepen of klik op **[!UICONTROL Bladeren]** om de bestandsmap te verkennen. Het bestand kan maximaal tien gigabyte groot zijn. Nadat het CSV-bestand is geüpload, klikt u op **[!UICONTROL Opslaan]** om de gegevensset te maken.

>[!NOTE]
>
>CSV-kolomnamen moeten beginnen met alfanumerieke tekens en mogen alleen letters, cijfers en onderstrepingstekens bevatten.

![](../images/datasets/user-guide/add_csv_data.png)

## Een gegevensset inschakelen voor realtime klantprofiel

Elke dataset heeft de capaciteit om klantenprofielen met zijn ingebedde gegevens te verrijken. Om dit te doen, moet het schema dat de dataset hanteert voor gebruik in [!DNL Real-time Customer Profile] compatibel zijn. Een compatibel schema voldoet aan de volgende vereisten:

* Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
* Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.

Voor meer informatie bij het toelaten van een schema voor [!DNL Profile], zie [de gebruikersgids van de Redacteur van het Schema](../../xdm/tutorials/create-schema-ui.md).

Als u een gegevensset voor Profiel wilt inschakelen, opent u het scherm **[!UICONTROL Datasetactiviteit]** en klikt u op de schakeloptie **[!UICONTROL Profiel]** in de kolom **[!UICONTROL Eigenschappen]**. Zodra toegelaten, zullen de gegevens die in de dataset worden opgenomen ook worden gebruikt om klantenprofielen te bevolken.

>[!NOTE]
>
>Als een dataset reeds gegevens bevat en dan voor [!DNL Profile] wordt toegelaten, worden de bestaande gegevens niet automatisch verbruikt door [!DNL Profile]. Nadat een dataset voor [!DNL Profile] wordt toegelaten, adviseert men dat u om het even welke bestaande gegevens opnieuw inneemt om het aan klantenprofielen te hebben bijdragen.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## Beheer van gegevens beheren en afdwingen op een gegevensset

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Zie [Overzicht gegevensbeheer](../../data-governance/home.md) om meer over etiketten te leren, of naar [de gebruikersgids van de etiketten van het gegevensgebruik te verwijzen ](../../data-governance/labels/overview.md) voor instructies op hoe te om etiketten op datasets toe te passen.

## Een gegevensset verwijderen

U kunt een dataset schrappen door tot zijn **[!UICONTROL Dataset activiteit]** scherm eerst toegang te hebben. Klik vervolgens op **[!UICONTROL Gegevensset verwijderen]** om deze te verwijderen.

>[!NOTE]
>
>Datasets die zijn gemaakt en gebruikt door Adobe-toepassingen en -services (zoals Adobe Analytics, Adobe Audience Manager of [!DNL Offer Decisioning]) kunnen niet worden verwijderd.

![](../images/datasets/user-guide/delete_dataset.png)

Er verschijnt een bevestigingsvak. Klik **[!UICONTROL Delete]** om de schrapping van de dataset te bevestigen.

![](../images/datasets/user-guide/confirm_delete.png)

## Een voor profiel ingeschakelde gegevensset verwijderen

Als een dataset voor [!DNL Profile] wordt toegelaten, zal het schrappen van die dataset door UI het van zowel het meer van Gegevens als de opslag van het Profiel binnen Platform schrappen.

U kunt een dataset van [!DNL Profile] opslag slechts schrappen (verlatend de gegevens in het meer van Gegevens) gebruikend Real-time API van het Profiel van de Klant. Voor meer informatie, zie [API eindgids van de banen van het profielsysteem van banenAPI](../../profile/api/profile-system-jobs.md).

## Gegevens bijhouden

In [!DNL Experience Platform] UI, klik **[!UICONTROL Controle]** in de linkernavigatie. Met het dashboard **[!UICONTROL Monitoring]** kunt u de status van binnenkomende gegevens van batch- of streaming opname bekijken. Als u de status van afzonderlijke batches wilt weergeven, klikt u op **[!UICONTROL Batch end-to-end]** of **[!UICONTROL Streaming end-to-end]**. De dashboards maakt een lijst van alle partij of het stromen ingangen, met inbegrip van die die succesvol zijn, ontbroken, of nog lopend. Elke lijst verstrekt details van de partij, met inbegrip van partijidentiteitskaart, de naam van de doeldataset, en het aantal verslagen die worden opgenomen. Als de doeldataset voor [!DNL Profile] wordt toegelaten, wordt het aantal ingebedde identiteit en profielverslagen ook getoond.

![](../images/datasets/user-guide/batch_listing.png)

U kunt op een individuele **[!UICONTROL Batch ID]** klikken om tot **[!UICONTROL Batch overzicht]** dashboard toegang te hebben en details voor de partij, met inbegrip van foutenlogboeken te zien als de partij er niet in slaagt op te nemen.

![](../images/datasets/user-guide/batch_overview.png)

Als u de batch wilt verwijderen, kunt u dit doen door te klikken op **[!UICONTROL Batch verwijderen]** boven aan het dashboard. Dit zal ook zijn verslagen uit de dataset verwijderen de partij oorspronkelijk aan werd opgenomen.

![](../images/datasets/user-guide/delete_batch.png)

## Volgende stappen

Deze gebruikershandleiding bevat instructies voor het uitvoeren van algemene handelingen bij het werken met gegevenssets in de gebruikersinterface [!DNL Experience Platform]. Raadpleeg de volgende zelfstudies voor stappen voor het uitvoeren van algemene [!DNL Platform]-workflows met datasets:

* [Een gegevensset maken met behulp van API&#39;s](create.md)
* [De gegevens van de dataset van de vraag gebruikend de Toegang API van Gegevens](../../data-access/home.md)
* [Een gegevensset configureren voor realtime profiel en identiteitsservice van klanten met behulp van API&#39;s](../../profile/tutorials/dataset-configuration.md)