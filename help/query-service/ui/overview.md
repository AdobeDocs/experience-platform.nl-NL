---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;vraag;vraagredacteur;de redacteur van de vraag;de redacteur van de Vraag;
solution: Experience Platform
title: UI-gids voor zoekservice
description: Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt om query's te schrijven en uit te voeren, eerder uitgevoerde query's weer te geven en query's te openen die zijn opgeslagen door gebruikers binnen uw organisatie.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# [!DNL Query Service] UI-hulplijn

De Adobe Experience Platform [!DNL Query Service] verstrekt een gebruikersinterface die kan worden gebruikt om vragen te schrijven en uit te voeren, eerder uitgevoerde vragen, en toegangsvragen te bekijken die door gebruikers binnen uw organisatie worden bewaard. Om tot UI binnen toegang te hebben [Adobe Experience Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Queries]** in de linkernavigatie.

## [!DNL Query Editor]

De [!DNL Query Editor] laat u toe om vragen te schrijven en uit te voeren zonder een externe cliënt te gebruiken. Selecteren **[!UICONTROL Create Query]** om de [!DNL Query Editor] en maak een nieuwe query. U hebt ook toegang tot de [!DNL Query Editor] door een query te selecteren in het menu **[!UICONTROL Log]** of **[!UICONTROL Templates]** tabs. Als u een eerder uitgevoerde of opgeslagen query selecteert, wordt het dialoogvenster [!DNL Query Editor] en geeft u de SQL voor de geselecteerde query weer.

![Het dashboard Vragen met de markering Query maken.](../images/ui/overview/overview.png)

[!DNL Query Editor] biedt bewerkruimte waarin u een query kunt typen. Terwijl u typt, voltooit de redacteur automatisch SQL gereserveerde woorden, lijsten, en gebiedsnamen binnen lijsten. Wanneer u klaar bent met het schrijven van uw query, selecteert u de opdracht **Afspelen** om de query uit te voeren. De **[!UICONTROL Console]** onder de editor ziet u wat [!DNL Query Service] doet momenteel, erop wijst die wanneer een vraag is teruggekeerd. De **[!UICONTROL Result]** naast de Console worden de resultaten van de query weergegeven. Zie de [Handleiding voor Query-editor](./user-guide.md) voor meer informatie over het gebruik van de [!DNL Query Editor].

![Een ingezoomd object met het oog op de [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Geplande query&#39;s {#scheduled-queries}

Vragen die al als een sjabloon zijn opgeslagen, kunnen worden gepland voor uitvoering op een normale agenda. Wanneer het plannen van een vraag, kunt u de frequentie van looppas, de begin en einddatum, de dag van de week kiezen de geplande vraaglooppas, evenals de dataset om de vraag naar uit te voeren. De programma&#39;s van de vraag worden geplaatst gebruikend de Redacteur van de Vraag.

Leren hoe te om een vraag door UI te plannen, zie [Gids voor geplande query&#39;s](./user-guide.md#scheduled-queries). Lees de [de geplande gids van het vraageindpunt](../api/scheduled-queries.md).

Zodra een vraag is gepland verschijnt het in de lijst van geplande vragen op [!UICONTROL Scheduled Queries] tab. De volledige details betreffende de vraag, de looppas, de schepper, en de tijdopnemers kunnen worden gevonden door een geplande vraag van de lijst te selecteren.

![De werkruimte van Vragen met het Geplande lusje van Vragen benadrukte en tonende rijen van vraagprogramma&#39;s.](../images/ui/overview/scheduled-queries.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | Het naamveld is de sjabloonnaam of de eerste paar tekens van uw SQL-query. Om het even welke vraag die door UI met de Redacteur van de Vraag wordt gecreeerd wordt genoemd bij aanvang. Als de query via de API is gemaakt, is de naam van de query een fragment van de eerste SQL die is gebruikt om de query te maken. |
| **[!UICONTROL Template]** | De sjabloonnaam van de query. Selecteer een sjabloonnaam om naar de Query-editor te navigeren. Het vraagmalplaatje wordt getoond in de Redacteur van de Vraag voor gemak. Als er geen malplaatjenaam is, wordt de rij duidelijk met een koppelteken en er is geen capaciteit om aan de Redacteur van de Vraag om de vraag te bekijken opnieuw te richten. |
| **[!UICONTROL SQL]** | Een fragment van de SQL-query. |
| **[!UICONTROL Run frequency]** | Dit is de kadentie waarbij uw vraag wordt geplaatst om te lopen. De beschikbare waarden zijn `Run once` en `Scheduled`. U kunt query&#39;s filteren op basis van hun uitvoeringsfrequentie. |
| **[!UICONTROL Created by]** | De naam van de gebruiker die de query heeft gemaakt. |
| **[!UICONTROL Created]** | De tijdstempel in UTC-indeling waarin de query is gemaakt. |
| **[!UICONTROL Last run timestamp]** | De meest recente tijdstempel toen de query werd uitgevoerd. Deze kolom benadrukt of een vraag volgens zijn huidig programma is uitgevoerd. |
| **[!UICONTROL Last run status]** | De status van de meest recente queryuitvoering. De drie statuswaarden zijn: `successful` `failed` of `in progress`. |

Raadpleeg de documentatie voor meer informatie over hoe u [controleert vragen door de Dienst UI van de Vraag](./monitor-queries.md).

## Sjablonen {#browse}

De **[!UICONTROL Templates]** tabblad geeft query&#39;s weer die zijn opgeslagen door gebruikers in uw organisatie. Het is nuttig om van deze als vraagprojecten te denken, aangezien de vragen hier worden bewaard nog onder bouw kunnen zijn. Vragen weergegeven op de **[!UICONTROL Templates]** tabblad wordt ook weergegeven als query&#39;s in het dialoogvenster **[!UICONTROL Log]** tab als ze eerder zijn uitgevoerd door [!DNL Query Service].

![Een ingezoomd in mening van het lusje van Malplaatjes van het Dashboard van Vragen tonend verscheidene bewaarde vragen.](../images/ui/overview/templates.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | Het naamveld is de naam van de query die door de gebruiker is gemaakt, of de eerste paar tekens van uw SQL-query. Om het even welke vraag die door UI met de Redacteur van de Vraag wordt gecreeerd wordt genoemd bij aanvang. Als de query via de API is gemaakt, is de naam van de query een fragment van de eerste SQL die is gebruikt om de query te maken. U kunt de naam van de query selecteren om de query te openen in het dialoogvenster [!DNL Query Editor]. U kunt ook de zoekbalk gebruiken om te zoeken naar de [!UICONTROL Name] van een query. Zoekopdrachten zijn hoofdlettergevoelig. |
| **[!UICONTROL SQL]** | De eerste paar tekens van de SQL-query. Als u de muis boven de code houdt, wordt de volledige query weergegeven. |
| **[!UICONTROL Modified by]** | De laatste gebruiker die de query heeft gewijzigd. Elke gebruiker in uw organisatie die toegang heeft tot [!DNL Query Service] kan query&#39;s wijzigen. |
| **[!UICONTROL Last modified]** | De datum en de tijd van de laatste wijziging in de query, in de tijdzone van de browser. |

Zie de [querysjablonen](./query-templates.md) documentatie voor meer informatie over malplaatjes in de UI van het Platform.

## Logboek {#log}

De **[!UICONTROL Log]** bevat een lijst met query&#39;s die eerder zijn uitgevoerd. Door gebrek, maakt een lijst van het logboek van de vragen in omgekeerde chronologie.

![Een ingezoomd in mening van het lusje van het Logboek van het Dashboard van Vragen die een lijst van vragen in omgekeerde chronologische orde toont.](../images/ui/overview/log.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | De naam van de query, die bestaat uit de eerste verschillende tekens van de SQL-query. Selecteer de sjabloonnaam om het dialoogvenster [!UICONTROL Query log details] voor die uitvoering. U kunt de zoekbalk gebruiken om te zoeken op de naam van een query. Zoekopdrachten zijn hoofdlettergevoelig. |
| **[!UICONTROL Start time]** | De tijd dat de query werd uitgevoerd. |
| **[!UICONTROL Complete time]** | De tijd dat de vraag voltooide. |
| **[!UICONTROL Status]** | De huidige status van de query. |
| **[!UICONTROL Dataset]** | De inputdataset die door de vraag wordt gebruikt. Selecteer de dataset om naar het scherm van de details van de inputdataset te gaan. |
| **[!UICONTROL Client]** | De client die voor de query wordt gebruikt. |
| **[!UICONTROL Created by]** | De naam van de persoon die de query heeft gemaakt. |

>!![Note]
Selecteer het potloodpictogram (![Een potloodpictogram.](../images/ui/overview/edit-icon.png)) van om het even welke rij van het vraaglogboek om aan [!DNL Query Editor]. De query is vooraf ingevuld voor handige bewerking.

Zie de [documentatie met querylogbestanden](./query-logs.md) voor meer informatie over de logboekdossiers die automatisch door een vraaggebeurtenis worden geproduceerd.

## Credentials

De **[!UICONTROL Credentials]** geeft zowel uw vervallende als niet-vervallende referenties weer. Voor meer informatie over hoe u deze referenties kunt gebruiken om verbinding te maken met externe clients, leest u de [aanmeldingsgids](../clients/overview.md).

![Het dashboard Vragen met het tabblad Referenties gemarkeerd.](../images/ui/overview/credentials.png)

## Volgende stappen

Nu bent u bekend met [!DNL Query Service] gebruikersinterface op [!DNL Platform], kunt u [!DNL Query Editor] beginnen uw eigen vraagprojecten te creëren om met andere gebruikers in uw organisatie te delen. Voor meer informatie over creatie en het runnen van vragen in [!DNL Query Editor], zie de [[!DNL Query Editor] gebruikershandleiding](./user-guide.md).
