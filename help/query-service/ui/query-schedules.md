---
title: Zoekplanningen
description: Leer hoe te om geplande vraaglooppas te automatiseren, een vraagprogramma te schrappen of onbruikbaar te maken, en de beschikbare het plannen opties door de UI van Adobe Experience Platform te gebruiken.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 75ef9c58aa7c5f1cc628d1f13b6c5f56b362458a
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Zoekprogramma&#39;s

U kunt vraaglooppas automatiseren door vraagprogramma&#39;s te creëren. Geplande vragen lopen op een douanecadence om uw gegevens te beheren die op frequentie, datum, en tijd worden gebaseerd. U kunt een outputdataset voor uw resultaten ook kiezen indien vereist. De vragen die als malplaatje zijn bewaard kunnen van de Redacteur van de Vraag worden gepland.

>[!IMPORTANT]
>
>U kunt alleen een schema toevoegen aan een query die al is gemaakt, opgeslagen en uitgevoerd.

Alle geplande query&#39;s worden toegevoegd aan de lijst in de [!UICONTROL Scheduled queries] tab. Van die werkruimte kunt u het statuut van alle geplande vraagbanen door UI controleren. Op de [!UICONTROL Scheduled queries] kunt u belangrijke informatie over uw vraaglooppas vinden en aan alarm intekenen. De beschikbare informatie omvat de status, de planningsdetails, en foutenmeldingen/codes als een looppas ontbreekt. Zie de [Geplande query&#39;s controleren](./monitor-queries.md) voor meer informatie .

## Creeer een vraagprogramma&#39;s {#create-schedule}

Om een programma aan een vraag toe te voegen, selecteer een vraagmalplaatje van of [!UICONTROL Templates] of de [!UICONTROL Scheduled Queries] om naar de Redacteur van de Vraag te navigeren.

Lees de [de geplande gids van het vraageindpunt](../api/scheduled-queries.md).

Wanneer een opgeslagen query wordt benaderd vanuit de Query-editor, wordt [!UICONTROL Schedules] onder de naam van de query. Selecteer **[!UICONTROL Schedules]**.

![De Query-editor met het tabblad Planningen gemarkeerd.](../images/ui/query-schedules/schedules-tab.png)

De werkruimte Planningen wordt weergegeven. Selecteren **[!UICONTROL Add Schedule]** om een schema te maken.

![De werkruimte van het Programma van de Redacteur van de Vraag met Add benadrukt programma.](../images/ui/query-schedules/add-schedule.png)

De pagina met planningsdetails wordt weergegeven. Op deze pagina, kunt u de frequentie van de geplande vraag, de begin en einddatum, de dag van de week kiezen de geplande vraag zal lopen, evenals welke dataset om de vraag naar uit te voeren.

![Het venster Schema-details is gemarkeerd.](../images/ui/query-schedules/schedule-details.png)

U kunt de volgende opties kiezen voor **[!UICONTROL Frequency]**:

- **[!UICONTROL Hourly]**: De geplande vraag zal elk uur voor de datumperiode lopen u selecteerde.
- **[!UICONTROL Daily]**: De geplande query wordt elke X dagen uitgevoerd op het moment en de datumperiode die u hebt geselecteerd. Houd er rekening mee dat de geselecteerde tijd binnen is **UTC** en niet uw lokale tijdzone.
- **[!UICONTROL Weekly]**: De geselecteerde query wordt uitgevoerd op de dagen van de week, tijd en de datumperiode die u hebt geselecteerd. Houd er rekening mee dat de geselecteerde tijd binnen is **UTC** en niet uw lokale tijdzone.
- **[!UICONTROL Monthly]**: De geselecteerde vraag zal elke maand op de dag, de tijd, en de datumperiode lopen u selecteerde. Houd er rekening mee dat de geselecteerde tijd binnen is **UTC** en niet uw lokale tijdzone.
- **[!UICONTROL Yearly]**: De geselecteerde vraag zal elk jaar op de dag, de maand, de tijd, en de datumperiode lopen u selecteerde. Houd er rekening mee dat de geselecteerde tijd binnen is **UTC** en niet uw lokale tijdzone.

Voor de outputdataset, hebt u de optie om of een bestaande dataset te gebruiken of een nieuwe dataset tot stand te brengen.

>[!IMPORTANT]
>
> Aangezien u of bestaand gebruikt of een nieuwe dataset creeert, doet u **niet** de noodzaak om `INSERT INTO` of `CREATE TABLE AS SELECT` als deel van de vraag, aangezien de datasets reeds worden geplaatst. Met inbegrip van `INSERT INTO` of `CREATE TABLE AS SELECT` als onderdeel van uw geplande query&#39;s resulteert in een fout.

Als u geen toegang tot geparameterized vragen hebt, ga op [een schema verwijderen of uitschakelen](#delete-schedule) sectie.

### Parameters instellen voor een geplande geparametereerde query {#set-parameters}

>[!IMPORTANT]
>
>De parameterized eigenschap van vraag UI is momenteel beschikbaar in een **alleen beperkte release** en is niet beschikbaar voor alle klanten.

Als u een geplande vraag voor een parameterized vraag creeert, moet u de parameterwaarden voor deze vraaglooppas nu plaatsen.

![De sectie van de Details van het Programma van de werkstroom van de programmaverwezenlijking met de benadrukte sectie van de Parameters van de Vraag.](../images/ui/query-schedules/scheduled-query-parameter.png)

Nadat u al deze details hebt bevestigd, selecteert u **[!UICONTROL Save]** om een schema te maken. U bent teruggekeerd aan de planningswerkruimte die details van het onlangs gecreeerde programma, met inbegrip van planningsidentiteitskaart, het programma zelf, en de de outputdataset van het programma toont. U kunt programmaidentiteitskaart gebruiken om meer informatie over de looppas van de geplande vraag zelf te zoeken. Lees voor meer informatie de [Geplande de eindpuntgids van vraaglooppas](../api/runs-scheduled-queries.md).

![De werkruimte van programma&#39;s met het onlangs gecreeerde programma benadrukt.](../images/ui/query-schedules/schedules-workspace.png)

## Een schema verwijderen of uitschakelen {#delete-schedule}

U kunt een programma van de plannenwerkruimte van een bepaalde vraag of van schrappen [!UICONTROL Scheduled Queries] werkruimte die van alle geplande vragen een lijst maakt.

Om toegang te krijgen tot [!UICONTROL Schedules] tabblad van de gekozen query, moet u de naam van een querysjabloon selecteren in het menu [!UICONTROL Templates] of de [!UICONTROL Scheduled Queries] tab. Dit navigeert aan de Redacteur van de Vraag voor die vraag. Vorm de Redacteur van de Vraag, selecteer **[!UICONTROL Schedules]** voor toegang tot de werkruimte voor schema&#39;s.

Selecteer een schema in de rijen met beschikbare schema&#39;s. U kunt de knevel gebruiken om de geplande vraag onbruikbaar te maken of toe te laten.

>[!IMPORTANT]
>
>U moet het programma onbruikbaar maken alvorens u een programma voor een vraag kunt schrappen.

Selecteren **[!UICONTROL Delete a schedule]** om het uitgeschakelde schema te verwijderen.

![De planningswerkruimte met Uitschakelen programma en Schrapping benadrukt programma.](../images/ui/query-schedules/delete-schedule.png)

Als alternatief kan de [!UICONTROL Scheduled Queries] het lusje biedt een inzameling van gealigneerde acties voor elke geplande vraag aan. Tot de beschikbare inline-acties behoren: [!UICONTROL Disable schedule] of [!UICONTROL Enable schedule], [!UICONTROL Delete schedule], en [!UICONTROL Subscribe] aan alarm voor de geplande vraag. Voor volledige instructies op hoe te om een geplande vraag door het geplande lusje van Vragen te schrappen of onbruikbaar te maken, te zien gelieve [geplande query-hulplijn controleren](./monitor-queries.md#inline-actions).
