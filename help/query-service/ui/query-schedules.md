---
title: Zoekplanningen
description: Leer hoe te om geplande vraaglooppas te automatiseren, een vraagprogramma te schrappen of onbruikbaar te maken, en de beschikbare het plannen opties door de UI van Adobe Experience Platform te gebruiken.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 41c069ef1c0a19f34631e77afd7a80b8967c5060
workflow-type: tm+mt
source-wordcount: '1741'
ht-degree: 0%

---

# Zoekprogramma&#39;s

U kunt vraaglooppas automatiseren door vraagprogramma&#39;s te creëren. Geplande vragen lopen op een douanecadence om uw gegevens te beheren die op frequentie, datum, en tijd worden gebaseerd. U kunt een outputdataset voor uw resultaten ook kiezen indien vereist. De vragen die als malplaatje zijn bewaard kunnen van de Redacteur van de Vraag worden gepland.

>[!IMPORTANT]
>
>U kunt alleen een schema toevoegen aan een query die al is gemaakt en opgeslagen.

Alle geplande query&#39;s worden toegevoegd aan de lijst in de [!UICONTROL Scheduled queries] tab. Van die werkruimte kunt u het statuut van alle geplande vraagbanen door UI controleren. Op de [!UICONTROL Scheduled queries] kunt u belangrijke informatie over uw vraaglooppas vinden en aan alarm intekenen. De beschikbare informatie omvat de status, de planningsdetails, en foutenmeldingen/codes als een looppas ontbreekt. Zie de [Geplande query&#39;s controleren](./monitor-queries.md) voor meer informatie .

Dit werkschema behandelt het het plannen proces in de Dienst UI van de Vraag. Als u wilt weten hoe u planningen toevoegt met de API, leest u de [de geplande gids van het vraageindpunt](../api/scheduled-queries.md).

## Een queryschema maken {#create-schedule}

Om een vraag te plannen, selecteer een vraagmalplaatje van of [!UICONTROL Templates] of de [!UICONTROL Template] kolom van de [!UICONTROL Scheduled Queries] tab. Als u de sjabloonnaam selecteert, gaat u naar de Query Editor.

Als u tot een bewaarde vraag van de Redacteur van de Vraag toegang hebt, kunt u een programma voor de vraag tot stand brengen of het programma van de vraag van het detailspaneel bekijken.

>[!TIP]
>
>Selecteren **[!UICONTROL View schedule]** om aan de planningswerkruimte te navigeren en om het even welke geplande vraaglooppas in een blik te zien.

![De Query-editor met [!UICONTROL View schedule] en [!UICONTROL Add schedule] gemarkeerd.](../images/ui/query-schedules/view-add-schedule.png)

Selecteren **[!UICONTROL Add schedule]** om naar de [detailpagina plannen](#schedule-details).

U kunt ook de **[!UICONTROL Schedules]** onder de naam van de query.

![De Query-editor met het tabblad Planningen gemarkeerd.](../images/ui/query-schedules/schedules-tab.png)

De werkruimte Planningen wordt weergegeven. UI toont een lijst van om het even welke geplande looppas die het malplaatje met wordt geassocieerd. Selecteren **[!UICONTROL Add Schedule]** om een schema te maken.

![De werkruimte van het Programma van de Redacteur van de Vraag met Add benadrukt programma.](../images/ui/query-schedules/add-schedule.png)

### Plan-details toevoegen {#schedule-details}

De pagina met planningsdetails wordt weergegeven. Op deze pagina kunt u diverse details voor de geplande query bewerken. De details omvatten [frequentie en weekdag van de geplande query](#scheduled-query-frequency) uitvoeren, de begin- en einddatum, de dataset waarnaar de resultaten worden geëxporteerd, en [querystatuswaarschuwingen](#alerts-for-query-status).

![Het venster Schema-details is gemarkeerd.](../images/ui/query-schedules/schedule-details.png)

#### Geplande queryfrequentie {#scheduled-query-frequency}

U kunt de volgende opties kiezen voor **[!UICONTROL Frequency]**:

- **[!UICONTROL Hourly]**: De geplande query wordt elk uur uitgevoerd voor de datumperiode die u hebt geselecteerd.
- **[!UICONTROL Daily]**: De geplande query wordt elke X dagen uitgevoerd op het moment en de datumperiode die u hebt geselecteerd. Houd er rekening mee dat de geselecteerde tijd in **UTC** en niet uw lokale tijdzone.
- **[!UICONTROL Weekly]**: De geselecteerde query wordt uitgevoerd op de dagen van de week, tijd en de datumperiode die u hebt geselecteerd. Houd er rekening mee dat de geselecteerde tijd in **UTC** en niet uw lokale tijdzone.
- **[!UICONTROL Monthly]**: De geselecteerde query wordt elke maand uitgevoerd op de dag, tijd en de datumperiode die u hebt geselecteerd. Houd er rekening mee dat de geselecteerde tijd in **UTC** en niet uw lokale tijdzone.
- **[!UICONTROL Yearly]**: De geselecteerde query wordt elk jaar uitgevoerd op de dag, maand, tijd en de datumperiode die u hebt geselecteerd. Houd er rekening mee dat de geselecteerde tijd in **UTC** en niet uw lokale tijdzone.

### Gegevenssetgegevens opgeven {#dataset-details}

U kunt de queryresultaten beheren door de gegevens aan een bestaande gegevensset toe te voegen of door een nieuwe gegevensset te maken en de gegevens eraan toe te voegen.

Selecteren **[!UICONTROL Create and append into new dataset]** om een gegevensreeks tot stand te brengen wanneer u een vraag voor het eerst uitvoert. De volgende uitvoeringen blijven gegevens in die gegevensreeks opnemen. Geef ten slotte een naam en een beschrijving voor de gegevensset.

>[!IMPORTANT]
>
> Aangezien u of bestaand gebruikt of een nieuwe dataset creeert, doet u **niet** de noodzaak om `INSERT INTO` of `CREATE TABLE AS SELECT` als deel van de vraag, aangezien de datasets reeds worden geplaatst. Met inbegrip van: `INSERT INTO` of `CREATE TABLE AS SELECT` als onderdeel van uw geplande query&#39;s resulteert in een fout.

![Het venster Schema-details met de gegevens in de gegevensset en het dialoogvenster [!UICONTROL Create and append into new dataset] gemarkeerde opties.](../images/ui/query-schedules/dataset-details-create-and-append.png)

U kunt ook **[!UICONTROL Append into existing dataset]** gevolgd door het pictogram van de dataset (![Het pictogram Gegevensset.](../images/ui/query-schedules/dataset-icon.png)).

![Het paneel van de Details van het Programma met de details van de Dataset en voegt in bestaande benadrukte dataset toe.](../images/ui/query-schedules/dataset-details-existing.png)

De **[!UICONTROL Select output dataset]** wordt weergegeven.

Daarna, of doorblader de bestaande datasets of gebruik het onderzoeksgebied om de opties te filtreren. Selecteer de rij van de dataset die u wenst te gebruiken. De gegevens van de dataset worden getoond in het paneel op het recht. Selecteren **[!UICONTROL Done]** om uw keuze te bevestigen.

![De Uitgezochte dialoog van de outputdataset met het onderzoeksgebied, een datasetrij, en Gemaakt benadrukte.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Quarantine vraagt of ze ononderbroken falen {#quarantine}

Wanneer het creëren van een programma, kunt u uw vraag in de quarantaineeigenschap inschrijven om systeemmiddelen te beschermen en potentiële verstoringen te verhinderen. De quarantainefunctie identificeert en isoleert automatisch vragen die herhaaldelijk ontbreken door hen in te plaatsen [!UICONTROL Quarantined] status. Door vragen na tien opeenvolgende mislukkingen in quarantining te plaatsen, kunt u tussenbeide komen, kwesties herzien en verbeteren alvorens verdere executies toe te staan. Hierdoor blijven uw operationele efficiëntie en gegevensintegriteit behouden.

![De werkruimte Queries met [!UICONTROL Query Quarantine] gemarkeerd en Ja geselecteerd.](../images/ui/query-schedules/quarantine-enroll.png)

Zodra een vraag voor de quarantaineeigenschap wordt ingeschreven, kunt u aan alarm voor deze verandering van de vraagstatus intekenen. Als een geplande vraag niet in quarantaine wordt ingeschreven, verschijnt het niet als optie op [het dialoogvenster Waarschuwingen](./monitor-queries.md#alert-subscription).

U kunt een geplande vraag in de quarantaineeigenschap van de gealigneerde acties van ook inschrijven [!UICONTROL Scheduled Queries] tab. Zie de [documentatie over query&#39;s controleren](./monitor-queries.md#alert-subscription) voor meer informatie .

### Waarschuwingen instellen voor de status van een geplande query {#alerts-for-query-status}

U kunt zich ook abonneren op querywaarschuwingen als onderdeel van uw geplande queryinstellingen. U kunt uw instellingen zodanig configureren dat meldingen voor verschillende situaties worden ontvangen. Het alarm kan voor een quarantined staat, vertragingen in vraagverwerking, of een verandering in status van uw vraag worden geplaatst. De beschikbare vraag-staat waakzame opties omvatten begin, succes, en mislukking. Waarschuwingen kunnen als pop-upberichten of e-mails worden ontvangen. Schakel het selectievakje in om u te abonneren op waarschuwingen voor die status van de geplande query.

![Het deelvenster Planningsdetails met de waarschuwingsopties gemarkeerd.](../images/ui/query-editor/alerts.png)

In de onderstaande tabel worden de ondersteunde typen querywaarschuwingen beschreven:

| Type waarschuwing | Beschrijving |
|---|---|
| `start` | Deze waarschuwing brengt u op de hoogte wanneer een geplande vraaglooppas in werking wordt gesteld of begint te verwerken. |
| `success` | Deze waarschuwing geeft aan wanneer een geplande query correct is uitgevoerd en geeft aan dat de query zonder fouten is uitgevoerd. |
| `failed` | Deze waarschuwing treedt op wanneer een geplande query een fout aantreft of niet met succes wordt uitgevoerd. Hiermee kunt u problemen snel identificeren en verhelpen. |
| `quarantine` | Dit alarm wordt geactiveerd wanneer een geplande vraaglooppas in quarantined staat wordt gezet. Zodra een vraag is [ingeschreven bij het quarantaineonderdeel](#quarantine), om het even welke geplande vraag die tien opeenvolgende looppas ontbreekt wordt automatisch gezet in een [!UICONTROL Quarantined] status. Een quarantined vraag vereist dan uw interventie alvorens om het even welke verdere uitvoeringen kunnen plaatsvinden. Opmerking: de quarantainevoorziening kan alleen worden geactiveerd als de query&#39;s zijn ingeschreven voor een abonnement op quarantainewaarschuwingen. |
| `delay` | Deze waarschuwing geeft een melding als er een [vertraging in het resultaat van een geplande query-uitvoering](./monitor-queries.md#query-run-delay) boven een bepaalde drempel. U kunt een douanetijd plaatsen die de alarm teweegbrengt wanneer de vraag voor die duur zonder of het voltooien of het ontbreken loopt. Het standaardgedrag plaatst een alarm voor 150 min nadat de vraag begint verwerking. |

>[!NOTE]
>
>Als u een [!UICONTROL Query Run Delay] waarschuwing, moet u uw gewenste vertragingstijd in notulen in de UI van het Platform plaatsen. Voer de duur in minuten in. De maximale vertraging is 24 uur (1440 minuten).

Voor een overzicht van waarschuwingen in Adobe Experience Platform, waaronder de structuur van de wijze waarop waarschuwingsregels worden gedefinieerd, raadpleegt u de [waarschuwingsoverzicht](../../observability/alerts/overview.md). Raadpleeg voor hulp bij het beheren van waarschuwingen en waarschuwingsregels in de gebruikersinterface van Adobe Experience Platform de [Handleiding Waarschuwingsinterface](../../observability/alerts/ui.md).

### Parameters instellen voor een geplande geparametereerde query {#set-parameters}

>[!IMPORTANT]
>
>De parameterized eigenschap van vraag UI is momenteel beschikbaar in een **alleen beperkte release** en is niet beschikbaar voor alle klanten. Als u geen toegang tot geparameterized vragen hebt, ga op [een schema verwijderen of uitschakelen](#delete-schedule) sectie.

Als u een geplande vraag voor een parameterized vraag creeert, moet u de parameterwaarden voor deze vraaglooppas nu plaatsen.

![De sectie van de Details van het Programma van de werkschema creatie met de benadrukte sectie van de Parameters van de Vraag.](../images/ui/query-schedules/scheduled-query-parameter.png)

Nadat u de planningsdetails hebt bevestigd, selecteert u **[!UICONTROL Save]** om een schema te maken. Je wordt teruggestuurd naar het tabblad Abonnementen van je template. Deze werkruimte toont details van het nieuwe gemaakte programma, met inbegrip van planningsidentiteitskaart, het programma zelf, en de de outputdataset van het programma.

## Geplande query-uitvoering weergeven {#scheduled-query-runs}

Uit de sjablonen [!UICONTROL Schedules] tabblad, selecteert u de planning-id om naar de lijst met query-uitvoeringen voor uw nieuwe geplande query te navigeren.

![De werkruimte van programma&#39;s met het onlangs gecreeerde programma benadrukt.](../images/ui/query-schedules/schedules-workspace.png)

Alternatief, om een lijst van de geplande looppas van een vraagmalplaatje te bekijken, navigeer aan **[!UICONTROL Scheduled queries]** en selecteert u een sjabloonnaam in de beschikbare lijst.

![Het Geplande vraaglusje met een genoemd benadrukt malplaatje.](../images/ui/query-schedules/view-scheduled-runs.png)

De lijst van vraaglooppas voor die geplande vraag verschijnt.

![De detailssectie van de Geplande werkruimte van Vragen met een lijst van vraaglooppas die voor een geplande vraag wordt benadrukt.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Zie de [geplande query-hulplijn controleren](./monitor-queries.md#inline-actions) voor volledige informatie over hoe te om het statuut van alle vraagbanen door UI te controleren.

Selecteer een **[!UICONTROL Query run ID]** van de lijst om aan het overzicht van de vraaglooppas te navigeren. Voor een volledige uitsplitsing van de beschikbare informatie over de [overzicht van queryuitvoering](./monitor-queries.md#query-run-overview)Raadpleeg de documentatie met geplande query&#39;s voor de monitor.

Om geplande vragen te controleren gebruikend de Dienst API van de Vraag, zie [Geplande de eindpuntgids van vraaglooppas](../api/runs-scheduled-queries.md).

## Een schema inschakelen, uitschakelen of verwijderen {#delete-schedule}

U kunt, een programma van de plannenwerkruimte van een bepaalde vraag toelaten onbruikbaar maken of schrappen of van [!UICONTROL Scheduled Queries] werkruimte die van alle geplande vragen een lijst maakt.

Als u toegang wilt krijgen tot [!UICONTROL Schedules] tabblad van de gekozen query, moet u de naam van een querysjabloon selecteren in het menu [!UICONTROL Templates] of de [!UICONTROL Scheduled Queries] tab. Dit navigeert aan de Redacteur van de Vraag voor die vraag. Vorm de Redacteur van de Vraag, selecteer **[!UICONTROL Schedules]** voor toegang tot de werkruimte voor schema&#39;s.

Selecteer een schema in de rijen met beschikbare schema&#39;s om het deelvenster Details te vullen. Gebruik de knevel om de geplande vraag onbruikbaar te maken (of toe te laten).

### Uitgeschakelde query&#39;s verwijderen

>[!IMPORTANT]
>
>U moet het programma onbruikbaar maken alvorens u een programma voor een vraag kunt schrappen.

![De lijst met de schema&#39;s van een sjabloon met het deelvenster Details gemarkeerd.](../images/ui/query-schedules/schedule-details-panel.png)

Er wordt een bevestigingsvenster weergegeven. Selecteren **[!UICONTROL Disable]** om de actie te bevestigen.

![Het bevestigingsvenster voor schema uitschakelen.](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Selecteren **[!UICONTROL Delete a schedule]** om het uitgeschakelde schema te verwijderen.

![De werkruimte van de programma&#39;s met benadrukt programma van de Schrapping.](../images/ui/query-schedules/delete-schedule.png)

Als alternatief kan de [!UICONTROL Scheduled Queries] tab biedt een verzameling inline-handelingen voor elke geplande query aan. Tot de beschikbare inline-acties behoren: [!UICONTROL Disable schedule] of [!UICONTROL Enable schedule], [!UICONTROL Delete schedule], en [!UICONTROL Subscribe] aan alarm voor de geplande vraag. Voor volledige instructies op hoe te om een geplande vraag door het geplande lusje van Vragen te schrappen of onbruikbaar te maken, te zien gelieve [geplande query-hulplijn controleren](./monitor-queries.md#inline-actions).
