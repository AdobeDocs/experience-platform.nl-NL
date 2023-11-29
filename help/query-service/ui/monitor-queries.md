---
title: Geplande query's controleren
description: Leer hoe te om vragen door de Dienst UI van de Vraag te controleren.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 37aeff5131b9f67dbc99f6199918403e699478c8
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 0%

---

# Geplande query&#39;s controleren

Adobe Experience Platform biedt een verbeterde zichtbaarheid voor de status van alle querytaken via de gebruikersinterface. Van de [!UICONTROL Scheduled Queries] tabblad, kunt u nu belangrijke informatie over uw query-uitvoering vinden die de status, planningsdetails en foutberichten/codes bevat als deze mislukken. U kunt aan alarm voor vragen ook intekenen die op hun status door UI voor om het even welk van deze vragen worden gebaseerd door [!UICONTROL Scheduled Queries] tab.

## [!UICONTROL Scheduled Queries]

De [!UICONTROL Scheduled Queries] verstrekt een overzicht van al uw geplande vragen CTAS en ITAS. De details van de looppas kunnen voor alle geplande vragen evenals foutencodes en berichten voor om het even welke ontbroken vragen worden gevonden.

Ga naar de [!UICONTROL Scheduled Queries] tab, selecteert u **[!UICONTROL Queries]** van de linkernavigatiebalk, gevolgd door **[!UICONTROL Scheduled Queries]**

![Het Geplande lusje van Vragen in de werkruimte van Vragen met Gepland benadrukte Vragen en Vragen.](../images/ui/monitor-queries/scheduled-queries.png)

In de onderstaande tabel wordt elke beschikbare kolom beschreven.

>[!NOTE]
>
>Het waarschuwingspictogram voor abonnementen staat in elke rij in een kolom zonder naam. Zie de [waarschuwingsabonnementen](#alert-subscription) voor meer informatie.

| Kolom | Beschrijving |
|---|---|
| **[!UICONTROL Name]** | Het naamveld is de sjabloonnaam of de eerste paar tekens van uw SQL-query. Om het even welke vraag die door UI met de Redacteur van de Vraag wordt gecreeerd wordt genoemd bij aanvang. Als de query via de API is gemaakt, wordt de naam ervan een fragment van de eerste SQL die wordt gebruikt om de query te maken. Als u een lijst wilt zien met alle regels die aan de query zijn gekoppeld, selecteert u een item in het menu [!UICONTROL Name] kolom. Zie de klasse [de loopdienstdetails van de vraaglooppas](#query-runs) sectie. |
| **[!UICONTROL Template]** | De sjabloonnaam van de query. Selecteer een sjabloonnaam om naar de Query-editor te navigeren. Het vraagmalplaatje wordt getoond in de Redacteur van de Vraag voor gemak. Als er geen malplaatjenaam is, wordt de rij duidelijk met een koppelteken en er is geen capaciteit om aan de Redacteur van de Vraag om de vraag te bekijken opnieuw te richten. |
| **[!UICONTROL SQL]** | Een fragment van de SQL-query. |
| **[!UICONTROL Run frequency]** | De frequentie waarmee de query is ingesteld op uitvoeren. De beschikbare waarden zijn `Run once` en `Scheduled`. U kunt query&#39;s filteren op basis van hun uitvoeringsfrequentie. |
| **[!UICONTROL Created by]** | De naam van de gebruiker die de query heeft gemaakt. |
| **[!UICONTROL Created]** | De tijdstempel in UTC-indeling waarin de query is gemaakt. |
| **[!UICONTROL Last run timestamp]** | De meest recente tijdstempel toen de query werd uitgevoerd. Deze kolom benadrukt of een vraag volgens zijn huidig programma is uitgevoerd. |
| **[!UICONTROL Last run status]** | De status van de meest recente queryuitvoering. De statuswaarden zijn: `Success`, `Failed`, `In progress`, en `No runs`. |
| **[!UICONTROL Schedule Status]** | De huidige status van de geplande query. Er zijn vijf potentiële waarden. [!UICONTROL Registering], [!UICONTROL Active], [!UICONTROL Inactive], [!UICONTROL Deleted]en een afbreekstreepje. <ul><li>Het koppelteken geeft aan dat de geplande query een eenmalige, niet-terugkerende query is.</li><li>De [!UICONTROL Registering] de status wijst erop dat het systeem nog de verwezenlijking van het nieuwe programma voor de vraag verwerkt. Opmerking: u kunt een geplande query tijdens de registratie niet uitschakelen of verwijderen.</li><li>De [!UICONTROL Active] status geeft aan dat de geplande query **nog niet geslaagd** de datum en het tijdstip van voltooiing.</li><li>De [!UICONTROL Inactive] status geeft aan dat de geplande query **passeren** de datum en het tijdstip van voltooiing.</li><li>De [!UICONTROL Deleted] de status wijst erop dat het vraagprogramma is geschrapt.</li></ul> |

>[!TIP]
>
>Als u naar de Query-editor navigeert, kunt u **[!UICONTROL Queries]** om terug te keren naar de [!UICONTROL Templates] tab.

## Tabelinstellingen aanpassen voor geplande query&#39;s {#customize-table}

U kunt de kolommen op de [!UICONTROL Scheduled Queries] op uw behoeften. Als u het dialoogvenster [!UICONTROL Customize table] het instellingenvenster en de beschikbare kolommen bewerken, selecteert u het instellingenpictogram (![Een instellingenpictogram.](../images/ui/monitor-queries/settings-icon.png)) van de rechterbovenhoek van het scherm.

>[!NOTE]
>
>De [!UICONTROL Created] kolom die verwijst naar de datum waarop het schema is gemaakt, is standaard verborgen.

![Het tabblad Geplande query&#39;s met het pictogram Tabelinstellingen aanpassen gemarkeerd.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Schakel de desbetreffende selectievakjes in of uit om een tabelkolom te verwijderen of toe te voegen. Selecteer vervolgens **[!UICONTROL Apply]** om je keuzes te bevestigen.

>[!NOTE]
>
>Om het even welke vraag die door UI werd gecreeerd wordt een genoemd malplaatje als deel van het creatieproces. De sjabloonnaam wordt weergegeven in de sjabloonkolom. Als de query via de API is gemaakt, is de sjabloonkolom leeg.

![Het dialoogvenster Tabelinstellingen aanpassen.](../images/ui/monitor-queries/customize-table-dialog.png)

## Geplande query&#39;s beheren met inlinehandelingen {#inline-actions}

De [!UICONTROL Scheduled Queries] de mening biedt diverse gealigneerde acties aan om al uw geplande vragen van één plaats te beheren. Inline-handelingen worden aangegeven in elke rij met ovaal. Selecteer de ellips van een geplande vraag die u wilt leiden om de beschikbare opties in een pop-up menu te zien. Tot de beschikbare opties behoren [[!UICONTROL Disable schedule]](#disable) of [!UICONTROL Enable schedule], [[!UICONTROL Delete schedule]](#delete), en [[!UICONTROL Subscribe]](#alert-subscription) om waarschuwingen te vragen.

![Het tabblad Geplande query&#39;s met de ellips van de inline-handeling en het pop-upmenu gemarkeerd.](../images/ui/monitor-queries/disable-inline.png)

### Een geplande query in- of uitschakelen {#disable}

Om een geplande vraag onbruikbaar te maken, selecteer de ellips van een geplande vraag u wilt leiden, dan selecteren **[!UICONTROL Disable schedule]** van de opties in het pop-upmenu. Er wordt een dialoogvenster weergegeven waarin uw handeling wordt bevestigd. Selecteren **[!UICONTROL Disable]** om uw instelling te bevestigen.

Zodra een geplande vraag gehandicapt is, kunt u het programma door het zelfde proces toelaten. Selecteer de ellips en selecteer vervolgens **[!UICONTROL Enable schedule]** uit de beschikbare opties.

### Een geplande query verwijderen {#delete}

Om een geplande vraag te schrappen, selecteer de ellips van een geplande vraag u wilt leiden, dan selecteren **[!UICONTROL Delete schedule]** van de opties in het pop-upmenu. Er wordt een dialoogvenster weergegeven waarin uw handeling wordt bevestigd. Selecteren **[!UICONTROL Delete]** om uw instelling te bevestigen.

Zodra een geplande vraag wordt geschrapt, is het **niet** verwijderd uit de lijst met geplande query&#39;s. De inline-acties die door de ovalen worden geboden, worden verwijderd en vervangen door het pictogram voor het toevoegen van waarschuwingen met grijstinten. U kunt zich niet abonneren op waarschuwingen voor het verwijderde schema. De rij blijft in UI om informatie over looppas te verstrekken die als deel van de geplande vraag wordt geleid.

![Het Geplande lusje van Vragen met een geschrapte geplande vraag en grayed uit benadrukt waarschuwingspictogram.](../images/ui/monitor-queries/post-delete.png)

Als u looppas voor dat vraagmalplaatje wilt plannen, selecteer de malplaatjenaam van de aangewezen rij om aan de Redacteur van de Vraag te navigeren, dan volg [instructies om een programma aan een vraag toe te voegen](./query-schedules.md#create-schedule) zoals beschreven in de documentatie.

### Abonneren op waarschuwingen {#alert-subscription}

Om aan alarm voor geplande vraaglooppas in te tekenen, selecteer de ellips van een geplande vraag u wilt leiden, dan selecteren **[!UICONTROL Subscribe]** van de opties in het pop-upmenu.

De [!UICONTROL Alerts] wordt geopend. De [!UICONTROL Alerts] Hiermee meldt u zich aan zowel UI-meldingen als e-mailwaarschuwingen. Waarschuwingen zijn gebaseerd op de status van de query. Er zijn drie opties beschikbaar: `start`, `success`, en `failure`. Vak of vakken invullen en **[!UICONTROL Save]** om in te schrijven. Je kunt je abonneren op berichten zolang ze geen [!UICONTROL Last Run Timestamp] waarde.

![Het dialoogvenster voor abonnementen.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Zie de [API-documentatie voor abonnementen](../api/alert-subscriptions.md) voor meer informatie .

### De query-details weergeven {#query-details}

Selecteer het informatiepictogram (![Een informatiepictogram.](../images/ui/monitor-queries/information-icon.png)) om het deelvenster Details voor de query weer te geven. Het detailspaneel bevat alle relevante informatie over de vraag voorbij de feiten inbegrepen in de geplande vraaglijst. De extra informatie omvat vraagidentiteitskaart, de laatste gewijzigde datum, SQL van de vraag, planningsidentiteitskaart, en het huidige vastgestelde programma.

![Het tabblad Geplande query&#39;s met het informatiepictogram en het deelvenster Details gemarkeerd.](../images/ui/monitor-queries/details-panel.png)

## Filterquery&#39;s {#filter}

U kunt vragen filteren op runtime frequentie. Van de [!UICONTROL Scheduled Queries] tab, selecteer het filterpictogram (![Een filterpictogram](../images/ui/monitor-queries/filter-icon.png)) om de filterzijbalk te openen.

![Het tabblad Geplande query&#39;s met het filterpictogram gemarkeerd.](../images/ui/monitor-queries/filter-queries.png)

Als u de lijst met query&#39;s wilt filteren op basis van de runtimefrequentie, selecteert u de optie **[!UICONTROL Scheduled]** of **[!UICONTROL Run once]** filterselectievakjes.

>[!NOTE]
>
>Om het even welke vraag die is uitgevoerd maar niet gepland kwalificeert als [!UICONTROL Run once].

![Het tabblad Geplande query&#39;s met de filterzijbalk gemarkeerd.](../images/ui/monitor-queries/filter-sidebar.png)

Als u de filtercriteria hebt ingeschakeld, selecteert u **[!UICONTROL Hide Filters]** om het filterdeelvenster te sluiten.

## De loopplandetails van de vraag {#query-runs}

Als u de pagina met planningsdetails wilt openen, selecteert u een querynaam in het menu [!UICONTROL Scheduled Queries] tab. Deze mening verstrekt een lijst van alle looppas die als deel van die geplande vraag wordt uitgevoerd. De verstrekte informatie omvat de begin en eindtijd, status, en gebruikte dataset.

![De pagina met planningsdetails.](../images/ui/monitor-queries/schedule-details.png)

Deze informatie wordt verstrekt in een vijf-kolomlijst. Elke rij geeft een query-uitvoering aan.

| Kolomnaam | Beschrijving |
|---|---|
| **[!UICONTROL Query run ID]** | ID van de vraaglooppas voor de dagelijkse uitvoering. Selecteer de **[!UICONTROL Query run ID]** om naar de [!UICONTROL Query run overview]. |
| **[!UICONTROL Query run start]** | De tijdstempel wanneer de query werd uitgevoerd. De tijdstempel heeft de UTC-indeling. |
| **[!UICONTROL Query run complete]** | De tijdstempel wanneer de query is voltooid. De tijdstempel heeft de UTC-indeling. |
| **[!UICONTROL Status]** | De status van de meest recente queryuitvoering. De drie statuswaarden zijn: `successful` `failed` of `in progress`. |
| **[!UICONTROL Dataset]** | De dataset betrokken bij de uitvoering. |

De details van de vraag die kunnen worden gepland in worden gezien [!UICONTROL Properties] deelvenster. Dit deelvenster bevat de initiële query-id, het type client, de sjabloonnaam, de query-SQL en het corresponderende schema.

![De pagina met planningsdetails met het deelvenster Eigenschappen gemarkeerd.](../images/ui/monitor-queries/properties-panel.png)

Selecteer een id voor een query om naar de pagina met uitvoerdetails te navigeren en query-informatie weer te geven.

![Het scherm met planningsdetails met een runtime-id gemarkeerd.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Overzicht van query-uitvoering {#query-run-overview}

De [!UICONTROL Query run overview] verstrekt informatie over individuele looppas voor deze geplande vraag en een meer gedetailleerde specificatie van de looppasstatus. Deze pagina omvat ook de cliëntinformatie en details van om het even welke fouten die de vraag kunnen hebben veroorzaakt om te ontbreken.

![Het scherm met de overzichtssectie gemarkeerd.](../images/ui/monitor-queries/query-run-details.png)

De sectie met de querystatus bevat de foutcode en het foutbericht als de query is mislukt.

![Het scherm met de foutensectie is gemarkeerd.](../images/ui/monitor-queries/failed-query.png)

U kunt de SQL-query van deze weergave naar het klembord kopiëren. Als u de query wilt kopiëren, selecteert u het kopieerpictogram rechtsboven in het SQL-fragment. Een pop-upbericht bevestigt dat de code is gekopieerd.

![Het scherm met details van de uitvoering waarin het SQL-kopieerpictogram is gemarkeerd.](../images/ui/monitor-queries/copy-sql.png)

### Details uitvoeren voor query&#39;s met anoniem blok {#anonymous-block-queries}

Vragen die anonieme blokken gebruiken om uit hun SQL-instructies te bestaan, worden gescheiden in hun individuele subquery&#39;s. De scheiding in subquery staat u toe om de looppasdetails voor elk vraagblok individueel te inspecteren.

>[!NOTE]
>
>De loopingdetails van een anoniem blok dat het bevel DROP gebruikt zullen **niet** worden gerapporteerd als een aparte subquery. De afzonderlijke looppasdetails zijn beschikbaar voor vragen CTAS, vragen ITAS, en verklaringen van de KOPIE die als anonieme die bloksubquery&#39;s worden gebruikt. Details uitvoeren voor de opdracht DROP wordt momenteel niet ondersteund.

Anonieme blokken worden aangeduid door het gebruik van een `$$` voor de query. Om meer over anonieme blokken in de vraagdienst te weten te komen, zie [anoniem blokdocument](../key-concepts/anonymous-block.md).

Anonieme subquery&#39;s voor blokken hebben tabs links van de status van de run. Selecteer een tabblad om de uitvoergegevens weer te geven.

![Het overzicht van de looppas van de Vraag die een anonieme blokvraag toont. De veelvoudige vraaglusjes worden benadrukt.](../images/ui/monitor-queries/anonymous-block-overview.png)

Als een anonieme blokquery mislukt, kunt u de foutcode voor dat specifieke blok vinden via deze UI.

![Het overzicht van de looppas van de Vraag die een anonieme blokvraag met de foutencode voor één benadrukt blok toont.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Selecteren **[!UICONTROL Query]** om terug te keren naar het scherm met planningsdetails, of **[!UICONTROL Scheduled Queries]** om terug te keren naar de [!UICONTROL Scheduled Queries] tab.

![Het scherm met details van de looppas met benadrukte Vraag.](../images/ui/monitor-queries/return-navigation.png)

<!-- Details required to complete this section below:
### Run details for queries with parameterized queries {#parameterized-queries}

Queries that use parameterized values to make up the SQL statement are ... 
-->
