---
keywords: Experience Platform;home;populaire onderwerpen;enable dataset;Dataset;dataset
solution: Experience Platform
title: UI-gids voor gegevensbestanden
description: Leer hoe u algemene handelingen uitvoert wanneer u werkt met gegevenssets in de Adobe Experience Platform-gebruikersinterface.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 9bfad453b74afce848ca3b00cd66a2336edf8479
workflow-type: tm+mt
source-wordcount: '4294'
ht-degree: 0%

---

# UI-gids voor gegevensbestanden

Deze gebruikershandleiding bevat instructies voor het uitvoeren van veelvoorkomende handelingen bij het werken met gegevenssets in de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze gebruikershandleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Datasets ](overview.md): De opslag en beheersconstructie voor gegevenspersistentie in [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
   * [ Grondbeginselen van schemacompositie ](../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ Redacteur van het Schema ](../../xdm/tutorials/create-schema-ui.md): Leer hoe te om uw eigen schema&#39;s te bouwen XDM gebruikend [!DNL Schema Editor] binnen het [!DNL Experience Platform] gebruikersinterface.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): zorg ervoor dat de regels, beperkingen en beleidsregels betreffende het gebruik van klantgegevens worden nageleefd.

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

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_datalakeretention"
>title="Behoud van gegevensopslag"
>abstract="Toont het huidige bewaarbeleid voor elke dataset. Deze waarde kan in de bewaarmontages van elke dataset worden gewijzigd. U kunt retentietijd alleen instellen voor de ExperienceEvent-gegevensset."

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_profileretention"
>title="Behoud van profiel"
>abstract="Toont het huidige bewaarbeleid voor elke dataset. Deze waarde kan in de bewaarmontages van elke dataset worden gewijzigd. U kunt retentietijd alleen instellen voor een ExperienceEvent-gegevensset."

>[!CONTEXTUALHELP]
>id="platform_datasets_datalakesettings_datasetretention"
>title="Bewaring van gegevensset"
>abstract="Datalake bewaart regels voor hoe lang gegevens worden opgeslagen en wanneer het in de verschillende diensten zou moeten worden geschrapt. Dit zorgt voor naleving van de regelgeving, het beheer van opslagkosten en het behoud van de gegevenskwaliteit."

>[!CONTEXTUALHELP]
>id="platform_datasets_orchestratedCampaigns_toggle"
>title="Geordende campagnes"
>abstract="Schakel deze schakeloptie in om het gebruik van de geselecteerde gegevensset in Adobe Journey Optimizer Orchestrated-campagnes toe te staan. De dataset moet een relationeel schema gebruiken en slechts één dataset kan per schema worden gecreeerd."
>additional-url="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/data-configuration/schemas-datasets/manual-schema#enable" text="Dataset inschakelen voor geordende campagnes"

>[!CONTEXTUALHELP]
>id="platform_datasets_enableforlookup_toggle"
>title="Opzoeken inschakelen"
>abstract="Laat deze dataset voor raadpleging toe om zijn gegevens in Journey Optimizer voor verpersoonlijking, Beslissing, en reisorchestratie te gebruiken."
>additional-url="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/data-management/lookup-aep-data" text="Adobe Experience Platform-gegevens gebruiken in Journey Optimizer"

Selecteer in de gebruikersinterface van [!DNL Experience Platform] de optie **[!UICONTROL Datasets]** in de linkernavigatie om het dashboard van **[!UICONTROL Datasets]** te openen. Het dashboard maakt een lijst van alle beschikbare datasets voor uw organisatie. De details worden getoond voor elke vermelde dataset, met inbegrip van zijn naam, het schema de dataset zich aan, en het statuut van de meest recente opnamelooppas aansluit.

![ UI van Experience Platform met het punt van Datasets dat in de linkernavigatiebar wordt benadrukt.](../images/datasets/user-guide/browse-datasets.png)

Selecteer de naam van een gegevensset op het tabblad [!UICONTROL Browse] om het **[!UICONTROL Dataset activity]** -scherm te openen en details weer te geven van de gegevensset die u hebt geselecteerd. Het activiteitenlusje omvat een grafiek die het tarief visualiseert van berichten die worden verbruikt evenals een lijst van succesvolle en ontbroken partijen.

![ Metriek en visualisaties van uw geselecteerde dataset worden benadrukt.](../images/datasets/user-guide/dataset-activity-1.png)
![ de steekproefpartijen die op uw geselecteerde dataset betrekking hebben worden benadrukt.](../images/datasets/user-guide/dataset-activity-2.png)

## Meer acties {#more-actions}

U kunt [!UICONTROL Delete] of [!UICONTROL Enable a dataset for Profile] vanuit de gedetailleerde weergave [!UICONTROL Dataset] . Selecteer **[!UICONTROL ... More]** in de rechterbovenhoek van de gebruikersinterface om de beschikbare acties weer te geven. Het vervolgkeuzemenu wordt weergegeven.

![ de werkruimte van Datasets met [!UICONTROL ... More] benadrukt dropdown menu.](../images/datasets/user-guide/more-actions.png)

Als u **[!UICONTROL Enable a dataset for Profile]** selecteert, verschijnt er een bevestigingsvenster. Selecteer **[!UICONTROL Enable]** om uw keuze te bevestigen.

>[!NOTE]
>
>Om een dataset voor Profiel toe te laten, moet het schema dat de dataset zich aan voor gebruik in het Profiel van de Klant in real time aansluit compatibel zijn. Zie [ een dataset voor profiel ](#enable-profile) sectie voor meer informatie toelaten.

![ de Enable dialoog van de gegevenssetbevestiging.](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

Als u **[!UICONTROL Delete]** selecteert, wordt het bevestigingsvenster van [!UICONTROL Delete dataset] weergegeven. Selecteer **[!UICONTROL Delete]** om uw keuze te bevestigen.

>[!NOTE]
>
>U kunt geen systeemdatasets schrappen.

U kunt een dataset of een dataset voor gebruik met het Profiel van de Klant in real time van de gealigneerde acties ook schrappen die op het [!UICONTROL Browse] lusje worden gevonden. Zie de [ gealigneerde actiessectie ](#inline-actions) voor meer informatie.

![ de dialoog van de de bevestigingsbevestiging van de dataset van de Schrapping.](../images/datasets/user-guide/delete-confirmation-dialog.png)

## Handelingen voor inline-gegevenssets {#inline-actions}

De datasets UI biedt nu een inzamelingen van gealigneerde acties voor elke beschikbare dataset aan. Selecteer de ellips (...) van een dataset die u wilt leiden om de beschikbare opties in een pop-up menu te zien. De beschikbare acties omvatten:

* [[!UICONTROL Preview dataset]](#preview)
* [[!UICONTROL Manage data and access labels]](#manage-and-enforce-data-governance)
* [[!UICONTROL Enable unified profile]](#enable-profile)
* [[!UICONTROL Manage tags]](#manage-tags)
* [[!UICONTROL Set data retention policy]](#data-retention-policy)
* [[!UICONTROL Move to folders]](#move-to-folders)
* [[!UICONTROL Delete]](#delete).

Meer informatie over deze beschikbare acties vindt u in de desbetreffende secties. Leren hoe te om grote aantallen datasets gelijktijdig te beheren, verwijs naar de [ bulkacties ](#bulk-actions) sectie.

### Een voorbeeld van een gegevensset bekijken {#preview}

U kunt een voorvertoning weergeven van maximaal 100 rijen met voorbeeldgegevens voor elke gegevensset, via de inline-opties op het tabblad [!UICONTROL Browse] of vanuit de weergave [!UICONTROL Dataset activity] .

Selecteer op het tabblad [!UICONTROL Browse] de ellips (...) naast de naam van de gegevensset en kies [!UICONTROL Preview dataset] . Als de dataset leeg is, wordt de voorproefoptie gedeactiveerd. U kunt ook **[!UICONTROL Dataset activity]** in de rechterbovenhoek van het scherm selecteren in het **[!UICONTROL Preview dataset]** -scherm.

![ het Browse lusje van de werkruimte van Datasets met de ellips en de optie van de dataset van de Voorproef die voor de gekozen dataset wordt benadrukt.](../images/datasets/user-guide/preview-dataset-option.png)

Dit opent het voorproefvenster, waar de hiërarchische schemamening voor de dataset op de linkerzijde verschijnt.

>[!NOTE]
>
>Het schemadiagram op de linkerzijde toont slechts gebieden die gegevens bevatten. Velden zonder gegevens worden automatisch verborgen om de interface te stroomlijnen en de focus op relevante informatie te richten.

![ de dialoog van de datasetvoorproef met informatie over de structuur, evenals steekproefwaarden, voor de dataset wordt getoond.](../images/datasets/user-guide/preview-dataset.png)

U kunt ook in het scherm **[!UICONTROL Dataset activity]** de optie **[!UICONTROL Preview dataset]** selecteren om het voorvertoningsvenster te openen en een voorbeeld van de structuur en waarden van de gegevensset te bekijken.

![ de knoop van de dataset van de Voorproef wordt benadrukt.](../images/datasets/user-guide/select-preview.png)

Het venster van de datasetvoorproef verstrekt een snelle manier om de structuur en de gegevens van uw dataset te onderzoeken en te bevestigen.


#### Voorvertoningsvenster voor gegevensset {#dataset-preview-window}

De volgende animatie toont het venster van de datasetvoorproef met zijn navigatie en de eigenschappen van de gegevensexploratie:

![ opname die van het Scherm het venster van de datasetvoorproef toont. De opname benadrukt de objecten browser sidebar, gegevenstype indicatoren, SQL vraagvertoning, en geformatteerde gegevenslijst.](../images/datasets/user-guide/dataset-preview-demo.gif)

Het voorvertoningsvenster van de gegevensset bevat:

* Een objectbrowser op de linkerzijde voor het navigeren en filteren van gegevenssetvelden.
* Gegevenstype-indicatoren naast elke kolomnaam voor insight in de structuur van de gegevensset.
* Een SQL vraagvertoning bij de bovenkant van het venster, die de vraag toont die wordt gebruikt om de dataset te produceren.
* Een opgemaakte tabelweergave van maximaal 100 rijen voor efficiënte gegevensrevisie.

Deze functies helpen u navigeren, schemadetails begrijpen en steekproefgegevens efficiënt bevestigen.

#### Sneltoets Geavanceerde zoekeditor {#query-editor-shortcut}

Als uw organisatie een Data Distiller-licentie heeft, hebt u rechtstreeks toegang tot [!UICONTROL Advanced Query Editor] vanuit het voorvertoningsvenster van de gegevensset. Gebruik deze kortere weg om naadloos van het voorvertonen van steekproefgegevens aan het lopen en het raffineren van vragen in de Dienst van de Vraag te bewegen.

>[!AVAILABILITY]
>
>De toegang tot [!UICONTROL Advanced Query Editor] is beperkt tot organisaties met een Data Distiller SKU-licentie. Als uw organisatie niet de vereiste vergunning heeft, verschijnt deze optie niet in het venster van de datasetvoorproef.

Selecteer [!UICONTROL Advanced Query Editor] in de rechterbovenhoek van het voorvertoningsvenster om de Query Service te openen met uw huidige SQL-query vooraf geladen en uitgevoerd. U kunt de SQL blijven analyseren of wijzigen zonder de query opnieuw in te voeren.

![ de voorproefvenster van de Dataset die de Geavanceerde knoop van de Redacteur van de Vraag in het hogere recht tonen.](../images/datasets/user-guide/dataset-preview-advanced-query-editor.png)

Gebruik downstreamservices, zoals [!DNL Query Service] en [!DNL JupyterLab] , voor extra analyse. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van Query Service](../../query-service/home.md)
* [Gebruikershandleiding voor JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

### Beheer van gegevens beheren en afdwingen op een gegevensset {#manage-and-enforce-data-governance}

U kunt de labels voor gegevensbeheer voor een dataset beheren door de inlineopties van het tabblad [!UICONTROL Browse] te selecteren. Selecteer de ovalen (...) naast de naam van de gegevensset die u wilt beheren, gevolgd door **[!UICONTROL Manage data and access labels]** in het vervolgkeuzemenu.

Met labels voor gegevensgebruik, toegepast op schemaniveau, kunt u gegevenssets en velden categoriseren volgens het gebruiksbeleid dat van toepassing is op die gegevens. Zie het [ overzicht van het Beleid van Gegevens ](../../data-governance/home.md) om meer over etiketten te leren, of naar de [ gids van de de etikettengebruiker van het gegevensgebruik ](../../data-governance/labels/overview.md) voor instructies op te verwijzen hoe te om etiketten op schema&#39;s voor propagatie op datasets toe te passen.

## Een gegevensset inschakelen voor realtime-klantprofiel {#enable-profile}

Elke dataset heeft de capaciteit om klantenprofielen met zijn ingebedde gegevens te verrijken. Hiervoor moet het schema dat de dataset naleeft, compatibel zijn voor gebruik in [!DNL Real-Time Customer Profile]. Een compatibel schema voldoet aan de volgende vereisten:

* Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
* Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.

Voor meer informatie bij het toelaten van een schema voor [!DNL Profile], zie de [ gebruikersgids van de Redacteur van het Schema ](../../xdm/tutorials/create-schema-ui.md).

U kunt een dataset voor Profiel van zowel de gealigneerde opties van het [!UICONTROL Browse] lusje als van de [!UICONTROL Dataset activity] mening toelaten. Selecteer op het tabblad [!UICONTROL Browse] van de [!UICONTROL Datasets] -werkruimte de ellips van een gegevensset die u wilt inschakelen voor Profiel. Er wordt een menulijst met opties weergegeven. Selecteer vervolgens **[!UICONTROL Enable unified profile]** in de lijst met beschikbare opties.

![ het Browse lusje van de werkruimte van Datasets met de ellipsen en laat verenigd benadrukt profiel toe.](../images/datasets/user-guide/enable-for-profile.png)

U kunt ook in het scherm **[!UICONTROL Dataset activity]** van de gegevensset de **[!UICONTROL Profile]** -schakeloptie selecteren in de kolom **[!UICONTROL Properties]** . Zodra toegelaten, zullen de gegevens die in de dataset worden opgenomen ook worden gebruikt om klantenprofielen te bevolken.

>[!NOTE]
>
>Als een gegevensset al gegevens bevat en vervolgens is ingeschakeld voor [!DNL Profile] , worden de bestaande gegevens niet automatisch verbruikt door [!DNL Profile] . Nadat een dataset voor [!DNL Profile] wordt toegelaten, adviseert men dat u om het even welke bestaande gegevens opnieuw inneemt om het aan klantenprofielen te hebben bijdragen.

![ de knevel van het Profiel wordt benadrukt binnen de pagina van de datasetdetails.](../images/datasets/user-guide/enable-dataset-profiles.png)

Datasets die voor Profiel zijn ingeschakeld, kunnen ook op deze criteria worden gefilterd. Zie de sectie op hoe te [ toegelaten de datasets van het filterProfiel ](#filter-profile-enabled-datasets) voor meer informatie.

### Gegevenssetcodes beheren {#manage-tags}

Voeg aangepaste gemaakte tags toe om gegevenssets te ordenen en zoek-, filter- en sorteermogelijkheden te verbeteren. Selecteer op het tabblad [!UICONTROL Browse] van de [!UICONTROL Datasets] -werkruimte de ellips van een gegevensset die u wilt beheren, gevolgd door **[!UICONTROL Manage tags]** in het vervolgkeuzemenu.

![ het Browse lusje van de werkruimte van Datasets met de ellips en beheert markeringsoptie die voor de gekozen dataset wordt benadrukt.](../images/datasets/user-guide/manage-tags.png)

Het dialoogvenster [!UICONTROL Manage tags] wordt weergegeven. Voer een korte beschrijving in om een aangepaste tag te maken of kies een reeds bestaande tag om uw gegevensset een label te geven. Selecteer **[!UICONTROL Save]** om uw instellingen te bevestigen.

![ de Manage dialoog van markeringen met benadrukte douanetags.](../images/datasets/user-guide/manage-tags-dialog.png)

Het dialoogvenster [!UICONTROL Manage tags] kan ook bestaande tags uit een gegevensset verwijderen. Selecteer gewoon de &#39;x&#39; naast de tag die u wilt verwijderen en selecteer **[!UICONTROL Save]** .

Zodra een markering aan een dataset is toegevoegd, kunnen de datasets op de overeenkomstige markering worden gefiltreerd. Zie de sectie op hoe te [ filterdatasets door markeringen ](#enable-profile) voor meer informatie.

Voor meer informatie over hoe te om bedrijfsvoorwerpen voor gemakkelijkere ontdekking en categorisering te classificeren, zie de gids op [ het leiden meta-gegevenstaxonomieën ](../../administrative-tags/ui/managing-tags.md). In deze handleiding wordt uitgelegd hoe gebruikers met de juiste machtigingen vooraf gedefinieerde tags kunnen maken, deze aan categorieën kunnen toewijzen en alle gerelateerde CRUD-bewerkingen in de gebruikersinterface van Experience Platform kunnen beheren.

### Beleid voor gegevensbewaring instellen {#data-retention-policy}

U kunt de instellingen voor het verlopen en behouden van de gegevensset beheren met het inlineactiemenu op het tabblad [!UICONTROL Browse] van de werkruimte van [!UICONTROL Datasets] . U kunt deze eigenschap gebruiken om te vormen hoe lang de gegevens in het gegevensmeer en de opslag van het Profiel worden behouden. De vervaldatum is gebaseerd op wanneer de gegevens in Experience Platform werden opgenomen en uw gevormde bewaarperiode.

>[!IMPORTANT]
>
>Als u bewaarregels voor een ExperienceEvent-gegevensset wilt toepassen of bijwerken, moet uw gebruikersrol de machtiging **[!UICONTROL Manage datasets]** bevatten. Dit op rol-gebaseerde toegangsbeheer zorgt ervoor dat slechts de gemachtigde gebruikers montages van het gegevenssetbehoud kunnen wijzigen.
>
>Zie het [ overzicht van de Toegangscontrole ](../../access-control/home.md#platform-permissions) voor meer informatie bij het toewijzen van toestemmingen in Adobe Experience Platform.

>[!TIP]
>
>In het datumpomeer worden onbewerkte, onverwerkte gegevens voor analyse en verwerking opgeslagen, zoals gebeurtenislogboeken, klikstreamgegevens en records met ingeklapte inhoud. De opslag van het Profiel bevat klant-identificeerbare gegevens, met inbegrip van identiteit-gestikte gebeurtenissen en attributeninformatie, om verpersoonlijking en activering in real time te steunen.

Als u de retentieperiode wilt configureren, selecteert u de ellips naast de gegevensset gevolgd door **[!UICONTROL Set data retention policy]** in het vervolgkeuzemenu.

![ het Browse lusje van de werkruimte van Datasets met de ellips en de Vastgestelde benadrukte optie van het beleid van het gegevensbehoud.](../images/datasets/user-guide/set-data-retention-policy-dropdown.png)

Het dialoogvenster [!UICONTROL Set dataset retention] wordt weergegeven. In het dialoogvenster worden gebruiksmaatstaven voor licenties op sandboxniveau, gegevens op gegevensniveau en huidige instellingen voor gegevensbehoud weergegeven. Deze metriek toont uw gebruik in vergelijking met uw rechten en helpt u datasetspecifieke opslag en bewaarconfiguraties beoordelen. De metriek omvat de naam van de dataset, het type, de status van de Activering van het Profiel, en het opslaggebruik van gegevens meer en van het Profiel.

>[!NOTE]
>
>De gegevens voor de opslag van gegevenslagen op het niveau van de zandbak zijn nog in ontwikkeling en worden mogelijk niet weergegeven. Een volledige uitsplitsing van de maatstaven voor het licentiegebruik vindt u op het dashboard Licentiegebruik. Zie de documentatie voor beschrijvingen van deze metriek.
<!-- replace this screenshot with a dataset that enabled unified profile so user can see the Profile TTL settings -->
![ de Vastgestelde dialoog van het gegevenssetbehoud.](../images/datasets/user-guide/set-data-retention-dialog.png)

Configureer de gewenste bewaarperiode in het dialoogvenster met instellingen voor gegevensbehoud. Voer een getal in en selecteer een tijdseenheid (dagen, maanden of jaren) in het vervolgkeuzemenu. U kunt afzonderlijke bewaarinstellingen configureren voor de service voor gegevens in het meer en in het profiel.

>[!NOTE]
> 
>De minimale bewaarperiode voor het datumpeer is 30 dagen. De minimale bewaarperiode voor profielservice is één dag.
>
>Bovendien kunt u de retentieperiode voor profielservice slechts eenmaal om de 30 dagen bijwerken.

Om transparantie en controle te steunen, worden timestamps verstrekt voor **laatste** en **volgende** de baanuitvoeringen van het gegevensbehoud. De tijdstempels helpen u begrijpen wanneer de laatste gegevensopruiming voorkwam en wanneer volgende wordt gepland.

#### Inzichten van opslageffecten {#storage-impact-insights}

Selecteer **[!UICONTROL View Experience Event Data distribution]** om een visuele voorspelling te openen van de invloed van verschillende retentiebeleidsregels op de opslag.

De grafiek toont de distributie van ervaringsgebeurtenissen over diverse bewaartermijnen voor de momenteel geselecteerde dataset. Houd de muisaanwijzer boven elke balk om te zien hoeveel records precies worden verwijderd als de geselecteerde retentieperiode wordt toegepast.

U kunt de visuele voorspelling gebruiken om het effect van verschillende bewaartermijnen te evalueren en geïnformeerde bedrijfsbesluiten te nemen. Als u bijvoorbeeld een bewaarperiode van 30 dagen selecteert en in het diagram wordt aangegeven dat 60% van uw gegevens wordt verwijderd, kunt u de retentie verlengen om meer gegevens voor analyse te behouden.

>[!NOTE]
>
>Het diagram van de distributie van de Gebeurtenis van de Ervaring is specifiek voor de geselecteerde dataset en wijst slechts op zijn gegevens. Zij is uitsluitend van toepassing op gegevens die in het datumpeer zijn opgeslagen.

![ de Vastgestelde dialoog van het gegevensbehoud met de Verspreidingsgrafiek van de Gebeurtenis van de Ervaring getoond.](../images/datasets/user-guide/visual-forecast.png)

Als u tevreden bent met de configuratie, selecteert u **[!UICONTROL Save]** om uw instellingen te bevestigen.

>[!IMPORTANT]
>
>Nadat de regels voor gegevensbewaring zijn toegepast, worden gegevens die ouder zijn dan het aantal dagen dat door de vervalwaarde is gedefinieerd, permanent verwijderd en kunnen deze niet meer worden hersteld.

Na het vormen van uw bewaarmontages, gebruik de Controle UI om te bevestigen dat uw veranderingen door het systeem werden uitgevoerd. De controle UI verstrekt een gecentraliseerde mening van de activiteit van het gegevensbehoud over alle datasets. Daarna kunt u de uitvoering van de taak volgen, controleren hoeveel gegevens zijn verwijderd en controleren of het beleid voor het behoud naar behoren functioneert.

Om te onderzoeken hoe het behoudbeleid over de verschillende diensten van toepassing is, zie de specifieke gidsen op [ het Behoud van de Dataset van de Gebeurtenis van de Ervaring in het Behouden van de Dataset van de Gebeurtenis van het Profiel ](../../profile/event-expirations.md) en [ het Behouden van de Dataset van de Gebeurtenis in het meer van Gegevens ](./experience-event-dataset-retention-ttl-guide.md). Deze zichtbaarheid ondersteunt beheer, naleving en efficiënt beheer van de gegevenslevenscyclus.

Leren hoe te om het controledashboard te gebruiken om brondataflows in Experience Platform UI te volgen, zie de [ dataflows van de Monitor voor bronnen in de UI ](../../dataflows/ui/monitor-sources.md) documentatie.

<!-- Improve the link above. I cannot link to a 100% appropriate document yet. -->

Voor meer informatie over de regels die datareeksen en beste praktijken bepalen van de gegevenssetvervaldatum voor het vormen van uw beleid van het gegevensbehoud, zie de [ vaak gestelde vragen pagina ](../catalog-faq.md).

#### Verbeterde zichtbaarheid van retentieperioden en gegevens over opslag {#retention-and-storage-metrics}

Vier nieuwe kolommen zorgen voor meer zichtbaarheid in uw gegevensbeheer: **[!UICONTROL Data Lake Storage]** , **[!UICONTROL Data Lake Retention]** , **[!UICONTROL Profile Storage]** en **[!UICONTROL Profile Retention]** . Deze gegevens laten zien hoeveel opslagruimte uw gegevens verbruiken en hoe lang deze gegevens bewaard blijven, zowel in de datumpeer- als in de profielservice.

Deze verhoogde zichtbaarheid stelt u in staat geïnformeerde beslissingen te nemen en opslagkosten effectiever te beheren. Sorteer datasets op opslaggrootte om de grootste in uw huidige zandbak te identificeren. Deze inzichten ondersteunen de beste praktijken voor gegevensbeheer en helpen naleving van uw gelicentieerde rechten te verzekeren.

![ het Browse lusje van de werkruimte van Datasets met de vier nieuwe benadrukte opslag en bewaarkolommen.](../images/datasets/user-guide/storage-and-retention-columns.png)

In de volgende tabel vindt u een overzicht van de nieuwe waarden voor retentie en opslag. Het detailleert het doel van elke kolom en hoe het het beheren van gegevensbehoud en opslag steunt.

| Kolomtitel | Beschrijving |
|---|---|
| [!UICONTROL Data Lake Retention] | De huidige bewaarperiode voor elke dataset in het gegevensmeer. Deze waarde kan worden geconfigureerd en bepaalt hoe lang gegevens bewaard blijven voordat ze worden verwijderd. |
| [!UICONTROL Data Lake Storage] | Het huidige opslaggebruik voor elke dataset in het gegevensmeer. Gebruik deze maatstaf om opslaglimieten te beheren en het gebruik te optimaliseren. |
| [!UICONTROL Profile Storage] | Het huidige opslaggebruik voor elke dataset binnen de Dienst van het Profiel. Helpt het opslagverbruik te bewaken en beslissingen voor gegevensbeheer te ondersteunen. |
| [!UICONTROL Profile Retention] | De huidige bewaarperiode voor de datasets van het Profiel. U kunt deze waarde bijwerken om te bepalen hoe lang Profielgegevens behouden blijven. |

{style="table-layout:auto"}

Om op de inzichten van opslag en behoudmetriek te handelen, verwijs naar de [ gids van de de vergunningsrechten van het gegevensbeheer best practices ](../../landing/license-usage-and-guardrails/data-management-best-practices.md). Gebruik het om te beheren welke gegevens u en bewaart, filters en vervalsingsregels toepast, en gegevensgroei controleert om binnen uw vergunning gegeven gebruiksgrenzen te blijven.

### Verplaatsen naar mappen {#move-to-folders}

U kunt datasets binnen omslagen voor beter gegevenssetbeheer plaatsen. Als u een gegevensset naar een map wilt verplaatsen, selecteert u de ovalen (...) naast de naam van de gegevensset die u wilt beheren, gevolgd door **[!UICONTROL Move to folder]** in het keuzemenu.

![ het [!UICONTROL Datasets] dashboard met de ellipsen en [!UICONTROL Move to folder] benadrukte.](../images/datasets/user-guide/move-to-folder.png)

Het dialoogvenster [!UICONTROL Move] Gegevensset naar map wordt weergegeven. Selecteer de map waarnaar u het publiek wilt verplaatsen en selecteer vervolgens **[!UICONTROL Move]** . Een popup bericht deelt u mee dat de datasetbeweging succesvol is geweest.

![ de [!UICONTROL Move] dialoog van de dataset met [!UICONTROL Move] benadrukte.](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>U kunt mappen ook rechtstreeks maken vanuit het dialoogvenster Gegevensset verplaatsen. Om een omslag tot stand te brengen, selecteer het creeer omslagpictogram (![ creeer omslagpictogram.](/help/images/icons/folder-add.png) ) rechtsboven in het dialoogvenster.
>
>![ de [!UICONTROL Move] dialoog van de dataset met creeer benadrukt omslagpictogram.](/help/catalog/images/datasets/user-guide/create-folder.png)

Zodra de dataset in een omslag is, kunt u verkiezen om datasets slechts te tonen die tot een specifieke omslag behoren. Om uw omslagstructuur te openen, selecteer het pictogram van showomslagen (![ het pictogram van showomslagen ](/help/images/icons/rail-left.png)). Vervolgens selecteert u de gekozen map om alle bijbehorende gegevenssets weer te geven.

![ de [!UICONTROL Datasets] dashboards met de getoonde de omslagstructuur van datasets, het pictogram van showomslagen, en een geselecteerde benadrukte omslag.](../images/datasets/user-guide/folder-structure.png)

### Een gegevensset verwijderen {#delete}

U kunt een dataset van of de dataset gealigneerde acties in het [!UICONTROL Browse] lusje of het hoogste recht van de [!UICONTROL Dataset activity] mening schrappen. Selecteer in de weergave [!UICONTROL Browse] de ovalen (...) naast de naam van de gegevensset die u wilt verwijderen. Er wordt een menulijst met opties weergegeven. Selecteer vervolgens **[!UICONTROL Delete]** in het vervolgkeuzemenu.

![ het Browse lusje van de werkruimte van Datasets met de ellips en de optie van de Schrapping die voor de gekozen dataset wordt benadrukt.](../images/datasets/user-guide/inline-delete-dataset.png)

Er wordt een bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Delete]** om te bevestigen.

U kunt ook **[!UICONTROL Delete dataset]** selecteren in het **[!UICONTROL Dataset activity]** -scherm.

>[!NOTE]
>
>Datasets die zijn gemaakt en gebruikt door Adobe-toepassingen en -services (zoals Adobe Analytics, Adobe Audience Manager of [!DNL Offer Decisioning]), kunnen niet worden verwijderd.

![ de knoop van de dataset van de Schrapping wordt benadrukt binnen de pagina van de datasetdetails.](../images/datasets/user-guide/delete-dataset.png)

Er verschijnt een bevestigingsvak. Selecteer **[!UICONTROL Delete]** om de verwijdering van de gegevensset te bevestigen.

![ wordt de bevestigingsmodaal voor schrapping getoond, met de benadrukte knoop van de Schrapping.](../images/datasets/user-guide/confirm-delete.png)

### Een voor profiel ingeschakelde gegevensset verwijderen

Als een dataset voor Profiel wordt toegelaten, zal het schrappen van die dataset door UI het van het gegevensmeer, de Dienst van de Identiteit, en ook om het even welke profielgegevens verbonden aan die dataset in de opslag van het Profiel schrappen.

U kunt profielgegevens die zijn gekoppeld aan een gegevensset verwijderen uit de [!DNL Profile] store (en de gegevens in het datumpomeer laten) met behulp van de Real-Time Customer Profile API. Voor meer informatie, zie de [ API eindpuntgids van de banen van het profielsysteem ](../../profile/api/profile-system-jobs.md).

## Gegevensbestanden zoeken en filteren {#search-and-filter}

Om de lijst van beschikbare datasets te zoeken of te filtreren, selecteer het filterpictogram (![ het filterpictogram.](/help/images/icons/filter.png) ) linksboven in de werkruimte. Er wordt een set filteropties weergegeven in de linkertrack. Er zijn verscheidene methodes om uw beschikbare datasets te filtreren. Deze omvatten: [[!UICONTROL Show System Datasets]](#show-system-datasets), [[!UICONTROL Included in profile]](#filter-profile-enabled-datasets), [[!UICONTROL Tags]](#filter-by-tag), [[!UICONTROL Creation date]](#filter-by-creation-date), [[!UICONTROL Modified date], [!UICONTROL Created by]](#filter-by-creation-date) en [[!UICONTROL Schema]](#filter-by-schema) .

De lijst met toegepaste filters wordt boven de gefilterde resultaten weergegeven.

![ het Browse lusje van de werkruimte van Datasets met de lijst van toegepaste benadrukte filters.](../images/datasets/user-guide/applied-filters.png)

### Systeemgegevenssets tonen {#show-system-datasets}

Door gebrek, slechts worden de datasets die u gegevens hebt ingebed in getoond. Als u de door het systeem gegenereerde gegevenssets wilt zien, schakelt u het selectievakje **[!UICONTROL Yes]** in de sectie [!UICONTROL Show system datasets] in. Door het systeem gegenereerde gegevenssets worden alleen gebruikt om andere componenten te verwerken. De door het systeem gegenereerde profielexportgegevensset wordt bijvoorbeeld gebruikt om het profieldashboard te verwerken.

![ de filteropties van de werkruimte van Datasets met de [!UICONTROL Show system datasets] benadrukte sectie.](../images/datasets/user-guide/show-system-datasets.png)

### Gegevenssets voor filterprofiel {#filter-profile-enabled-datasets}

De datasets die voor de gegevens van het Profiel zijn toegelaten worden gebruikt om klantenprofielen te bevolken nadat de gegevens zijn opgenomen. Zie de sectie op [ toelatend datasets voor Profiel ](#enable-profile) om meer te leren.

Als u uw gegevensset wilt filteren op basis van de vraag of deze zijn ingeschakeld voor Profiel, schakelt u het selectievakje [!UICONTROL Yes] in bij de filteropties.

![ de filteropties van de werkruimte van Datasets met de [!UICONTROL Included in Profile] benadrukte sectie.](../images/datasets/user-guide/included-in-profile.png)

### Gegevenssets filteren op tag {#filter-by-tag}

Voer in de invoer [!UICONTROL Tags] de naam van uw aangepaste tag in en selecteer vervolgens de tag in de lijst met beschikbare opties voor het zoeken naar en filteren van gegevenssets die overeenkomen met die tag.

![ de filteropties van de werkruimte van Datasets met het [!UICONTROL Tags] benadrukte input en filterpictogram.](../images/datasets/user-guide/filter-tags.png)

### Gegevensbestanden filteren op aanmaakdatum {#filter-by-creation-date}

Datasets kunnen worden gefilterd op aanmaakdatum over een aangepaste tijdsperiode. Dit kan worden gebruikt om historische gegevens uit te sluiten of specifieke chronologische gegevens en rapportage te genereren. Kies een [!UICONTROL Start date] en een [!UICONTROL End date] door het kalenderpictogram voor elk veld te selecteren. Daarna, slechts datasets die aan die criteria voldoen zullen op het Browse lusje verschijnen.

### Gegevenssets filteren op gewijzigde datum {#filter-by-modified-date}

Net als bij het filter voor de aanmaakdatum kunt u de gegevenssets filteren op basis van de datum waarop deze voor het laatst zijn gewijzigd. Kies in de sectie [!UICONTROL Modified date] een [!UICONTROL Start date] en een [!UICONTROL End date] door het kalenderpictogram voor elk veld te selecteren. Daarna, slechts zullen de datasets die tijdens die periode werden gewijzigd in het Browse lusje verschijnen.

### Filteren op schema {#filter-by-schema}

U kunt datasets filtreren die op het schema worden gebaseerd dat hun structuur bepaalt. Selecteer het vervolgkeuzepictogram of voer de schemanaam in het tekstveld in. Er wordt een lijst weergegeven met mogelijke overeenkomsten. Selecteer het gewenste schema in de lijst.

## Bulkacties {#bulk-actions}

De bulkacties van het gebruik om uw operationele efficiency te verbeteren en veelvoudige acties op talrijke datasets gelijktijdig uit te voeren. U kunt tijd besparen en een georganiseerde gegevensstructuur met bulkacties zoals [ Beweging aan omslag ](#move-to-folders) handhaven, [ markeringen ](#manage-tags) uitgeven, en [ schrapt ](#delete) datasets.

Om op meer dan één dataset tezelfdertijd te handelen, selecteer individuele datasets met checkbox op elke rij, of selecteer een volledige pagina met het vakje van de kolomkopbal. Als deze optie is geselecteerd, wordt de algemene actiebalk weergegeven.

![ de Datasets doorbladeren lusje met talrijke geselecteerde datasets en de bulkbenadrukte actiebar.](../images/datasets/user-guide/bulk-actions.png)

Wanneer u bulkacties op datasets toepast, zijn de volgende voorwaarden van toepassing:

* U kunt datasets van verschillende pagina&#39;s van UI selecteren.
* Als u een filter selecteert, worden de geselecteerde datasets opnieuw ingesteld.

## Gegevenssets sorteren op gemaakte datum {#sort}

Datasets op het tabblad [!UICONTROL Browse] kunnen worden gesorteerd op oplopende of aflopende datums. Selecteer de kolomkoppen [!UICONTROL Created] of [!UICONTROL Last updated] om te schakelen tussen oplopend en aflopend. Als deze optie is geselecteerd, geeft de kolom dit aan met een pijl-omhoog of een pijl-omlaag naar de zijkant van de kolomkop.

![ het Browse lusje van de werkruimte van Datasets met de Gemaakt en laatst bijgewerkte benadrukte kolom.](../images/datasets/user-guide/ascending-descending-columns.png)

## Een gegevensset maken {#create}

Als u een nieuwe gegevensset wilt maken, selecteert u eerst **[!UICONTROL Create dataset]** in het dashboard van **[!UICONTROL Datasets]** .

![ de Create datasetknoop wordt benadrukt.](../images/datasets/user-guide/select-create.png)

In het volgende scherm, wordt u voorgesteld met de volgende twee opties om een nieuwe dataset tot stand te brengen:

* [Gegevensset maken van schema](#schema)
* [Gegevensset maken van CSV-bestand](#csv)

### Creeer een dataset met een bestaand schema {#schema}

Selecteer in het scherm **[!UICONTROL Create dataset]** de optie **[!UICONTROL Create dataset from schema]** om een nieuwe, lege gegevensset te maken.

![ Create dataset van schemaknoop wordt benadrukt.](../images/datasets/user-guide/create-dataset-schema.png)

De stap **[!UICONTROL Select schema]** wordt weergegeven. Blader door het schema en selecteer het schema waaraan de dataset zich zal houden voordat u **[!UICONTROL Next]** selecteert.

![ een lijst van schema&#39;s wordt getoond. Het schema dat zal worden gebruikt om de dataset tot stand te brengen wordt benadrukt.](../images/datasets/user-guide/select-schema.png)

De stap **[!UICONTROL Configure dataset]** wordt weergegeven. Geef de gegevensset een naam en een optionele beschrijving en selecteer vervolgens **[!UICONTROL Finish]** om de gegevensset te maken.

![ de details van de Configuratie van de dataset worden opgenomen. Dit omvat details zoals de datasetnaam en beschrijving.](../images/datasets/user-guide/configure-dataset-schema.png)

Datasets kunnen van de lijst van beschikbare datasets in UI met de schemafilter worden gefiltreerd. Zie de sectie op hoe te [ filterdatasets door schema ](#filter-by-schema) voor meer informatie.

### Een gegevensset maken met een CSV-bestand {#csv}

Wanneer een dataset gebruikend een Csv- dossier wordt gecreeerd, wordt een ad hoc schema gecreeerd om de dataset van een structuur te voorzien die het verstrekte Csv- dossier aanpast. Selecteer **[!UICONTROL Create dataset]** in het **[!UICONTROL Create dataset from CSV file]** -scherm.

![ Create dataset van Csv- dossierknoop wordt benadrukt.](../images/datasets/user-guide/create-dataset-csv.png)

De stap **[!UICONTROL Configure]** wordt weergegeven. Geef de gegevensset een naam en een optionele beschrijving en selecteer vervolgens **[!UICONTROL Next]** .

![ de details van de Configuratie van de dataset worden opgenomen. Dit omvat details zoals de datasetnaam en beschrijving.](../images/datasets/user-guide/configure-dataset-csv.png)

De stap **[!UICONTROL Add data]** wordt weergegeven. Upload het CSV-bestand door het naar het midden van het scherm te slepen of selecteer **[!UICONTROL Browse]** om de bestandsmap te verkennen. Het bestand kan maximaal tien gigabyte groot zijn. Nadat het CSV-bestand is geüpload, selecteert u **[!UICONTROL Save]** om de gegevensset te maken.

>[!NOTE]
>
>CSV-kolomnamen moeten beginnen met alfanumerieke tekens en mogen alleen letters, cijfers en onderstrepingstekens bevatten.

![ het Add gegevensscherm wordt getoond. De plaats waar u het Csv- dossier voor de dataset kunt uploaden wordt benadrukt.](../images/datasets/user-guide/add-csv-data.png)

## Gegevens bijhouden

Selecteer [!DNL Experience Platform] in de gebruikersinterface van **[!UICONTROL Monitoring]** in de linkernavigatie. Met het dashboard **[!UICONTROL Monitoring]** kunt u de status van binnenkomende gegevens van batch- of streaming invoer bekijken. Als u de status van afzonderlijke batches wilt weergeven, selecteert u **[!UICONTROL Batch end-to-end]** of **[!UICONTROL Streaming end-to-end]** . De dashboards maken een lijst van alle partij of het stromen ingangen, met inbegrip van die die succesvol zijn, ontbroken, of nog lopend. Elke lijst verstrekt details van de partij, met inbegrip van partijidentiteitskaart, de naam van de doeldataset, en het aantal verslagen die worden opgenomen. Als de doeldataset voor [!DNL Profile] wordt toegelaten, wordt het aantal ingebedde identiteit en profielverslagen ook getoond.

![ het controlerende batch scherm van begin tot eind wordt getoond. Zowel worden de controle als partij-aan-partij benadrukt.](../images/datasets/user-guide/batch-listing.png)

U kunt op een individu **[!UICONTROL Batch ID]** selecteren om toegang te krijgen tot het **[!UICONTROL Batch overview]** -dashboard en details voor de batch bekijken, inclusief foutlogboeken als de batch niet wordt opgenomen.

![ Details van de geselecteerde partij worden getoond. Dit omvat het aantal verslagen die worden opgenomen, het aantal verslagen ontbrak, de partijstatus, de dossiergrootte, de het insluiten begin en eindtijden, de dataset en partij IDs, organisatie identiteitskaart, de datasetnaam, en de toegangsinformatie.](../images/datasets/user-guide/batch-overview.png)

Als u de batch wilt verwijderen, selecteert u **[!UICONTROL Delete batch]** rechtsboven in het dashboard. Als u een batch verwijdert, verwijdert u ook de records uit de gegevensset waarin de batch oorspronkelijk was opgenomen.

>[!NOTE]
>
>Als de ingesloten gegevens zijn ingeschakeld voor Profiel en zijn verwerkt, worden deze gegevens niet verwijderd wanneer u een batch verwijdert uit het archief Profiel.

![ de de partijknoop van de Schrapping wordt benadrukt op de pagina van de datasetdetails.](../images/datasets/user-guide/delete-batch.png)

## Volgende stappen

Deze gebruikershandleiding bevat instructies voor het uitvoeren van veelvoorkomende handelingen bij het werken met gegevenssets in de gebruikersinterface van [!DNL Experience Platform] . Raadpleeg de volgende zelfstudies voor informatie over het uitvoeren van veelvoorkomende [!DNL Experience Platform] -workflows met datasets:

* [Een gegevensset maken met behulp van API&#39;s](create.md)
* [De gegevens van de dataset van de vraag gebruikend de Toegang API van Gegevens](../../data-access/home.md)
* [Een gegevensset configureren voor realtime profiel en identiteitsservice van klanten met behulp van API&#39;s](../../profile/tutorials/dataset-configuration.md)

