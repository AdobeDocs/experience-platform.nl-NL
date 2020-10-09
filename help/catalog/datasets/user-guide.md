---
keywords: Experience Platform;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: Gebruikershandleiding voor gegevensbestanden
topic: datasets
description: Deze gebruikershandleiding voor gegevenssets bevat instructies voor het uitvoeren van algemene handelingen bij het werken met gegevenssets in de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 79dca07d3e6ecf998a6278fa49178a7fa8cc0e8c
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---


# Gebruikershandleiding voor gegevensbestanden

Deze gebruikershandleiding bevat instructies voor het uitvoeren van veelvoorkomende handelingen bij het werken met gegevenssets in de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze gebruikershandleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Gegevenssets](overview.md): De opslag- en beheerconstructie voor gegevenspersistentie in [!DNL Experience Platform].
* [[!DNL-ervaringsgegevensmodel (XDM)-systeem]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Schema-editor](../../xdm/tutorials/create-schema-ui.md): Leer hoe u uw eigen aangepaste XDM-schema&#39;s maakt met behulp van de [!DNL Schema Editor] [!DNL Platform] gebruikersinterface.
* [[!DNL Real-time klantprofiel]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Ervoor zorgen dat de regels, beperkingen en beleidsregels betreffende het gebruik van klantgegevens worden nageleefd.

## Gegevensbestanden weergeven

In [!DNL Experience Platform] UI, klik **[!UICONTROL Datasets]** in de linkernavigatie om het dashboard van **[!UICONTROL Datasets]** te openen. Het dashboard maakt een lijst van alle beschikbare datasets voor uw organisatie. De details worden getoond voor elke vermelde dataset, met inbegrip van zijn naam, het schema de dataset zich aan, en status van de meest recente versiereeks houdt.

![](../images/datasets/user-guide/browse_datasets.png)

Klik de naam van een dataset om tot zijn de activiteitenscherm van de **[!UICONTROL Dataset]** toegang te hebben en details van de dataset te zien u selecteerde. Het activiteitenlusje omvat een grafiek die het tarief visualiseert van berichten die worden verbruikt evenals een lijst van succesvolle en ontbroken partijen.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Een voorbeeld van een gegevensset bekijken

Klik in het scherm **[!UICONTROL Dataset-activiteit]** op Gegevensset **[!UICONTROL voorvertonen]** in de rechterbovenhoek van het scherm om maximaal 100 rijen gegevens voor te vertonen. Als de dataset leeg is, zal de voorproefverbinding worden gedeactiveerd en in plaats daarvan zal zeggen dat de voorproef niet beschikbaar is.

![](../images/datasets/user-guide/click_to_preview.png)

In het voorproefvenster, wordt de hiërarchische mening van het schema voor de dataset getoond op het recht.

![](../images/datasets/user-guide/preview_dataset.png)

Voor robuustere methodes om tot uw gegevens toegang te hebben, [!DNL Experience Platform] verleent de stroomafwaartse diensten zoals [!DNL Query Service] en [!DNL JupyterLab] om gegevens te onderzoeken en te analyseren. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van Query Service](../../query-service/home.md)
* [Gebruikershandleiding voor JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Een gegevensset maken {#create}

Om een nieuwe dataset tot stand te brengen, begin door **[!UICONTROL Create dataset]** in het dashboard van **[!UICONTROL Datasets]** te klikken.

![](../images/datasets/user-guide/click_to_create.png)

In het volgende scherm, wordt u voorgesteld met de volgende twee opties om een nieuwe dataset tot stand te brengen:

* [Gegevensset maken van schema](#schema)
* [Gegevensset maken van CSV-bestand](#csv)

### Creeer een dataset met een bestaand schema {#schema}

In het **[!UICONTROL Create scherm van de dataset]** , leidt de klik **[!UICONTROL dataset van schema]** tot om een nieuwe lege dataset tot stand te brengen.

![](../images/datasets/user-guide/create_dataset_schema.png)

De stap Schema **** selecteren wordt weergegeven. Blader door het schema en selecteer het schema waaraan de dataset zich zal houden voordat u op **[!UICONTROL Volgende]** klikt.

![](../images/datasets/user-guide/select_schema.png)

De stap Gegevensset **** configureren wordt weergegeven. Geef de gegevensset een naam en een optionele beschrijving en klik op **[!UICONTROL Voltooien]** om de gegevensset te maken.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Een gegevensset maken met een CSV-bestand {#csv}

Wanneer een dataset gebruikend een Csv- dossier wordt gecreeerd, wordt een ad hoc schema gecreeerd om de dataset van een structuur te voorzien die het verstrekte Csv- dossier aanpast. Klik in het scherm **[!UICONTROL Gegevensset]** maken op het vakje Gegevensset **[!UICONTROL maken van CSV-bestand]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

De stap **[!UICONTROL Configureren]** wordt weergegeven. Geef de gegevensset een naam en een optionele beschrijving en klik op **[!UICONTROL Volgende]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

De stap Gegevens **** toevoegen wordt weergegeven. Upload het CSV-bestand door het naar het midden van het scherm te slepen of klik op **[!UICONTROL Bladeren]** om de bestandsmap te verkennen. Het bestand kan maximaal tien gigabyte groot zijn. Nadat het CSV-bestand is geüpload, klikt u op **[!UICONTROL Opslaan]** om de gegevensset te maken.

>[!NOTE]
>
>CSV-kolomnamen moeten beginnen met alfanumerieke tekens en mogen alleen letters, cijfers en onderstrepingstekens bevatten.

![](../images/datasets/user-guide/add_csv_data.png)

## Een gegevensset inschakelen voor realtime klantprofiel

Elke dataset heeft de capaciteit om klantenprofielen met zijn ingebedde gegevens te verrijken. Om dit te doen, moet het schema dat de dataset hanteert voor gebruik binnen compatibel zijn [!DNL Real-time Customer Profile]. Een compatibel schema voldoet aan de volgende vereisten:

* Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
* Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.

Voor meer informatie bij het toelaten van een schema voor [!DNL Profile], zie de de gebruikersgids [van de Redacteur van het](../../xdm/tutorials/create-schema-ui.md)Schema.

Als u een gegevensset voor Profiel wilt inschakelen, opent u het **[!UICONTROL scherm Gegevensset-activiteit]** en klikt u op de schakeloptie **[!UICONTROL Profiel]** in de kolom **[!UICONTROL Eigenschappen]** . Zodra toegelaten, zullen de gegevens die in de dataset worden opgenomen ook worden gebruikt om klantenprofielen te bevolken.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Als een dataset reeds gegevens bevat en dan toegelaten voor [!DNL Profile], worden de bestaande gegevens niet verbruikt door [!DNL Profile]. Nadat een dataset voor wordt toegelaten [!DNL Profile], adviseert men dat u om het even welke bestaande gegevens opnieuw inneemt om hen te hebben klantenprofielen bevolken.

## Beheer van gegevens beheren en afdwingen op een gegevensset

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Zie het overzicht [van het Beheer van](../../data-governance/home.md) Gegevens om meer over etiketten te leren, of naar de de etiketteringsgebruikersgids [van het](../../data-governance/labels/overview.md) gegevensgebruik voor instructies te verwijzen over hoe te om etiketten op datasets toe te passen.

## Een gegevensset verwijderen

U kunt een dataset schrappen door tot zijn de activiteitenscherm van de **[!UICONTROL Dataset eerst toegang te hebben]** . Klik vervolgens op Gegevensset **** verwijderen om deze te verwijderen.

>[!NOTE]
>
>Datasets die zijn gemaakt en gebruikt door Adobe-toepassingen en -services (zoals Adobe Analytics, Adobe Audience Manager of [!DNL Decisioning Service]) kunnen niet worden verwijderd.

![](../images/datasets/user-guide/delete_dataset.png)

Er verschijnt een bevestigingsvak. Klik **[!UICONTROL Schrapping]** om de schrapping van de dataset te bevestigen.

![](../images/datasets/user-guide/confirm_delete.png)

## Een voor profiel ingeschakelde gegevensset verwijderen

Als een dataset voor wordt toegelaten [!DNL Profile], schrappend het door UI maakt de dataset voor opname onbruikbaar, maar schrapt automatisch niet de dataset in het achterste eind. Om de dataset met inbegrip van het profiel en de identiteitsgegevens volledig te schrappen die het verstrekt, moet een extra schrappingsverzoek worden gedaan. Zie de [!DNL Profile] API- [!DNL Real-time Customer Profile] subhandleiding over profielsysteemtaken, ook wel &quot;verwijderaanvragen&quot; [genoemd, voor informatie over het correct verwijderen van gegevens uit de](../../profile/api/profile-system-jobs.md)winkel.

## Gegevens bijhouden

In [!DNL Experience Platform] UI, klik **[!UICONTROL Controle]** in de linkernavigatie. Met het **[!UICONTROL dashboard Bewaking]** kunt u de status van binnenkomende gegevens van batch- of streaming invoer bekijken. Als u de status van afzonderlijke batches wilt weergeven, klikt u op Van begin tot eind **** batch of op Van begin tot eind **** streaming. De dashboards maakt een lijst van alle partij of het stromen ingangen, met inbegrip van die die succesvol zijn, ontbroken, of nog lopend. Elke lijst verstrekt details van de partij, met inbegrip van partijidentiteitskaart, de naam van de doeldataset, en het aantal verslagen die worden opgenomen. Als de doeldataset voor wordt toegelaten [!DNL Profile], wordt het aantal ingebedde identiteit en profielverslagen ook getoond.

![](../images/datasets/user-guide/batch_listing.png)

U kunt op een individuele identiteitskaart **[!UICONTROL van de]** Partij klikken om tot het **[!UICONTROL Batch overzichtdashboard]** toegang te hebben en details voor de partij zien, met inbegrip van foutenlogboeken als de partij er niet in slaagt op te nemen.

![](../images/datasets/user-guide/batch_overview.png)

Als u de batch wilt verwijderen, kunt u dit doen door te klikken op batch **** verwijderen rechtsboven in het dashboard. Dit zal ook zijn verslagen uit de dataset verwijderen de partij oorspronkelijk aan werd opgenomen.

![](../images/datasets/user-guide/delete_batch.png)

## Volgende stappen

Deze gebruikersgids verstrekte instructies voor het uitvoeren van gemeenschappelijke acties wanneer het werken met datasets in het [!DNL Experience Platform] gebruikersinterface. Raadpleeg de volgende zelfstudies voor informatie over het uitvoeren van algemene [!DNL Platform] workflows met datasets:

* [Een gegevensset maken met behulp van API&#39;s](create.md)
* [De gegevens van de dataset van de vraag gebruikend de Toegang API van Gegevens](../../data-access/home.md)
* [Een gegevensset configureren voor realtime profiel en identiteitsservice van klanten met behulp van API&#39;s](../../profile/tutorials/dataset-configuration.md)