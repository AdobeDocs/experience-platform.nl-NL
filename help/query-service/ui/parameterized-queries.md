---
title: Parameterized Vragen
description: Leer hoe u geparametereerde query's kunt gebruiken in de gebruikersinterface van Adobe Experience Platform.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# Parameterized vragen {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Parameterized vragen"
>abstract="Gebruik geparametereerde query&#39;s om parameterwaarden toe te voegen op het moment van uitvoering. Op deze manier kunt u met dynamische gegevens werken en query&#39;s hergebruiken voor verschillende gebruiksgevallen. Gebruik de voorkeuren van `'$'` om een queryparameter in te voeren in uw query in de teksteditor. Voeg vervolgens een waarde voor de sleutel toe in de sectie met zoekparameters onder de editor."

De Dienst van de vraag steunt het gebruik van parameterized vragen in de Redacteur van de Vraag. Met parameterized vragen, kunt u placeholders voor parameters nu gebruiken en de parameterwaarden bij uitvoeringstijd toevoegen. Plaatsaanduidingen maken het mogelijk om met dynamische gegevens te werken als u niet weet wat de waarden zijn totdat de instructie wordt uitgevoerd. U kunt uw vragen ook vooraf voorbereiden en opnieuw gebruiken voor gelijkaardige doeleinden. Het hergebruiken van vragen bespaart aanzienlijke inspanning aangezien u vermijdt creërend duidelijke SQL vragen voor elk gebruiksgeval.

## Vereisten

Alvorens met deze gids verder te gaan, lees de [&#x200B; gids UI van de Redacteur van de Vraag &#x200B;](./user-guide.md). De gids van de Redacteur van de Vraag verstrekt gedetailleerde informatie over hoe te schrijven, te bevestigen, en vragen voor klantenervaringsgegevens in het gebruikersinterface van Experience Platform in werking te stellen.

>[!NOTE]
>
>Binnen Adobe Experience Platform UI, wordt de parameter bepaalde vragen slechts gesteund op het ouderniveau van gealigneerde malplaatjes. Dit betekent dat de parameters bepaalde vragen slechts werken wanneer gebruikt in het originele malplaatje. De malplaatjes van het kind moeten een statisch malplaatje zijn en kunnen geen dynamische parameters hebben. Zie de [&#x200B; gealigneerde sjabloondocumentatie &#x200B;](../key-concepts/inline-templates.md) om meer te leren.

## Parameterized vraagsyntaxis {#syntax}

Gemarkeerde query&#39;s gebruiken de indeling `'$YOUR_PARAMETER_NAME'` en kunnen worden samengevoegd met puntnotatie. Een voorbeeldSQL verklaring die geparametereerde vragen gebruikt kan hieronder worden gezien.

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## Een query met parameters maken {#create}

Navigeer naar de Query-editor om de geparametereerde query in de UI te maken. Zie de sectie op [&#x200B; die tot de Redacteur van de Vraag &#x200B;](./user-guide.md#accessing-query-editor) voor meer instructies toegang hebben.

Gebruik de voorkeuren van `'$'` om een queryparameter in te voeren in uw query in de teksteditor. Selecteer vervolgens het tabblad **[!UICONTROL Query parameters]** naast [!UICONTROL Console] de ontbrekende waarde voor de toets toevoegen. De query kan niet worden uitgevoerd als u geen waarde toevoegt aan een van de vereiste toetsen. Een waakzaam pictogram (![&#x200B; een waakzaam pictogram.](/help/images/icons/alert.png)) wordt weergegeven in de sectie Query Parameters naast lege [!UICONTROL Value] -invoervelden.

>[!NOTE]
>
>Als uw vraag geen parameters neemt, kunt u onnodige parameters binnen de Redacteur van de Vraag nog ingaan. De redacteur van de Vraag negeert alle onnodige sleutel-waarde paren en zij hebben geen effect op de uitvoering of de resultaten van de vraag.

![&#x200B; de Redacteur van de Vraag met een parameterized vraag en de benadrukte sectie van de parameters van de Vraag.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Wijzig tabbladen van [!UICONTROL Query parameters] in [!UICONTROL Console] om de uitvoer van de console van de query weer te geven.

## Gegevens over querylogbestanden gebruiken om parameterwaarden te controleren {#check-parameter-values}

U kunt geen parameters opslaan binnen sjablonen omdat de gebruikte waarden niet blijvend zijn. U kunt de pagina [!UICONTROL Query log details] echter wel controleren om te zoeken naar de parameterwaarden die worden gebruikt in een query. In dit geval, wijzen de logboeken niet erop dat de vraag een parameterized vraag was. Zie de [&#x200B; documentatie van vraaglogboeken &#x200B;](./query-logs.md) voor instructies op hoe te om de gebruikte waarden te vinden.

![&#x200B; de mening van vraaglogboeken met SQL van een parameterized vraag die in de detailssectie wordt benadrukt.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Plan een geparameterialiseerde vraag {#schedule}

Parameterwaarden worden opgeslagen wanneer u een geparametriseerde query plant. Om een bepaalde bepaalde vraag te plannen, volg het typische proces om een geplande vraag tot stand te brengen zoals die in de gids wordt beschreven [&#x200B; tot een vraagprogramma &#x200B;](./query-schedules.md#create-schedule) leidt, dan de parameterwaarden ingaan die in de vraaglooppas moeten worden gebruikt. Deze UI-sectie wordt alleen weergegeven voor query&#39;s met parameters. Zie de sectie over [&#x200B; plaatsende parameters voor een geplande geparameterized vraag &#x200B;](./query-schedules.md#set-parameters) voor specifieke instructies.

>[!TIP]
>
>De Dienst van de vraag steunt voorbereide verklaringen door het gebruik van parameterized vragen. Zie de [&#x200B; voorbereide gids van de verklaringensyntaxis &#x200B;](../sql/prepared-statements.md) voor meer informatie over de SQL betrokken syntaxis.

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe te om vragen in Adobe Experience Platform UI parameters te bepalen en hen in geplande vraaglooppas te gebruiken. Het document benadrukte ook hoe te om de logboeken voor de parameterwaarden te controleren die in vraaguitvoeringen worden gebruikt.

Daarna, wordt u geadviseerd om de gids te lezen over [&#x200B; die geplande vragen &#x200B;](./monitor-queries.md) controleert om een beter inzicht in het statuut van alle vraagbanen door Experience Platform UI te krijgen.
