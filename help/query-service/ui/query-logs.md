---
title: Query-logbestanden
description: Logboeken van de vraag worden automatisch geproduceerd telkens als een vraag wordt uitgevoerd en beschikbaar door UI om met het oplossen van problemen te helpen. Dit document schetst hoe te om de sectie van de Logboeken van de Dienst van de Vraag van UI te gebruiken en te navigeren.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---

# Zoekopdrachtlogs

>[!IMPORTANT]
>
>Bepaalde functies voor querylogbestanden bevinden zich momenteel in een beperkte versie en zijn niet beschikbaar voor alle klanten. De gebruikersinterface kan er anders uitzien zonder een bewerkingspictogram. Het selecteren van een querynaam kan ook naar de Query Editor gaan in plaats van naar de weergave [!UICONTROL Query log details] .

Adobe Experience Platform houdt een logboek bij van alle vraaggebeurtenissen die door zowel API als UI voorkomen. Deze informatie is beschikbaar in de gebruikersinterface van de Query-service op het tabblad [!UICONTROL Logs] .

De logboekdossiers worden geproduceerd automatisch door om het even welke vraaggebeurtenis en bevatten informatie met inbegrip van gebruikte SQL, de status van de vraag, hoe lang het duurde, en laatste runtime. U kunt de gegevens van het vraaglogboek als krachtig hulpmiddel voor het oplossen van problemeninefficiënt of probleemvragen gebruiken. De uitvoerigere logboekinformatie wordt gehouden als deel van de eigenschap van het controlelogboek en kan in de [ documentatie van het controlelogboek ](../../landing/governance-privacy-security/audit-logs/overview.md) worden gevonden.

## Zoeklogs controleren {#check-query-logs}

Als u de querylogs wilt controleren, selecteert u [!UICONTROL Queries] om naar de werkruimte van de Query-service te navigeren en selecteert u [!UICONTROL Log] in de beschikbare opties.

>[!NOTE]
>
>Zowel worden de systeemvragen als de dashboardvragen uitgesloten door gebrek. Zie de [ filters ](#filter-logs) sectie voor informatie over hoe te om de getoonde logboeken te verfijnen die op uw montages worden gebaseerd.

![ Platform UI met de Vragen en het Logboek benadrukte.](../images/ui/query-log/logs.png)

## Aanpassen en zoeken {#customize-and-search}

Logboeken van de Dienst van de vraag worden voorgesteld in een klantgerichte lijstformaat. Om de lijstkolommen aan te passen, selecteer het montagespictogram (![ A montagespictogram.](/help/images/icons/column-settings.png) ) rechts van het scherm. Er wordt een dialoogvenster [!UICONTROL Customize Table] weergegeven waarin u de selectie van elke kolom kunt opheffen.

U kunt ook naar logboeken zoeken die betrekking hebben op specifieke vraagmalplaatjes door de malplaatjenaam in het onderzoeksgebied te typen.

![ de werkruimte van het Logboek van Vragen met de onderzoeksbar en beheert benadrukte dropdown van de kolomlijst.](../images/ui/query-log/customize-logs.png)

A [ beschrijving voor elk van de kolommen van de logboeklijst ](./overview.md#log) kan in de sectie van het Logboek van het overzicht van de Dienst van de Vraag worden gevonden.

## Loggegevens detecteren

Elke rij vertegenwoordigt logboekgegevens voor een vraaglooppas verbonden aan een vraagmalplaatje. Selecteer een rij in de tabel om de rechterzijbalk te vullen met loggegevens voor die uitvoering.

![ de werkruimte van het Logboek van Vragen met een geselecteerde rij en de logboekgegevens in juiste benadrukte sidebar.](../images/ui/query-log/log-details.png)

In het deelvenster met loggegevens kunt u allerlei handelingen uitvoeren. U kunt de vraag als CTAS in werking stellen, die tot een nieuwe outputdataset leidt, de volledige SQL vraag zien of kopiëren die in de looppas werd gebruikt, of de vraag schrappen.

>[!NOTE]
>
>De optie voor [!UICONTROL Run as CTAS] is alleen beschikbaar voor een SELECT-query.

![ de werkruimte van het Logboek van Vragen met een geselecteerde rij, Looppas als CTAS, de vraag van de Schrapping en het benadrukte pictogram van exemplaar SQL.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Bepaalde functies voor querylogbestanden bevinden zich momenteel in een beperkte versie en zijn niet beschikbaar voor alle klanten.

U kunt ook een naam voor een querysjabloon selecteren in de kolom [!UICONTROL Name] om rechtstreeks naar de weergave [!UICONTROL Query log details] te navigeren.

>[!NOTE]
>
>Als de query is gemaakt met de API en er tijdens de initialisatie geen sjabloonnaam is opgegeven, worden in plaats daarvan de eerste tientallen tekens van de SQL-query weergegeven.

![ de mening van de het logboekdetails van de Vraag.](../images/ui/query-log/query-log-details.png)

## Logboeken bewerken {#edit-logs}

Naast de het malplaatjenaam van elke rij of SQL fragment is een potloodpictogram (![ het potloodpictogram van A.](/help/images/icons/edit.png)) die u kunt gebruiken om naar de Redacteur van de Vraag te navigeren. De vraag wordt dan pre-bevolkt in de redacteur voor het uitgeven.

![ de werkruimte van het Logboek van Vragen met een benadrukt potloodpictogram.](../images/ui/query-log/edit-query.png)

## Filterlogs {#filter-logs}

U kunt de lijst met querylogbestanden filteren op basis van verschillende instellingen. Selecteer het filterpictogram (![ het filterpictogram.](/help/images/icons/filter.png) ) linksboven in de werkruimte om een set filteropties te openen in de linkerrails.

![ de werkruimte van het Logboek van Vragen met het benadrukte filterpictogram.](../images/ui/query-log/log-filter.png)

De lijst met beschikbare filters wordt weergegeven.

![ de werkruimte van het Logboek van Vragen met de getoonde en benadrukte filteropties.](../images/ui/query-log/log-filter-settings.png)

In de volgende tabel vindt u een beschrijving van elk filter.

| Filter | Beschrijving |
| ------ | ----------- |
| [!UICONTROL Exclude dashboard queries] | Dit checkbox wordt toegelaten door gebrek en sluit logboeken uit die door de vragen worden geproduceerd die voor het produceren van inzichten worden gebruikt. Deze vragen zijn systeem geproduceerd en bedekken de verslagen van gebruiker geproduceerde logboeken noodzakelijk voor controle, het beheer en het oplossen van problemen. Schakel het selectievakje uit als u door het systeem gegenereerde logbestanden wilt weergeven. |
| [!UICONTROL Exclude system queries] | Dit selectievakje is standaard ingeschakeld en sluit logbestanden uit die door het systeem zijn gegenereerd. Door het systeem gegenereerde query&#39;s omvatten vaak achtergrondtaken of onderhoudsbewerkingen die niet relevant kunnen zijn voor gebruikersbewaking, beheer of probleemoplossing. Als u door het systeem gegenereerde logboeken moet inspecteren, schakelt u dit selectievakje uit om deze in de logweergave op te nemen. |
| [!UICONTROL Start date] | Als u de logs wilt filteren op query&#39;s die tijdens een bepaalde periode zijn gemaakt, stelt u de datums [!UICONTROL Start] en [!UICONTROL End] in de sectie [!UICONTROL Start date] in. |
| [!UICONTROL Completed date] | Als u de logbestanden wilt filteren op query&#39;s die tijdens een bepaalde periode zijn voltooid, stelt u de datums [!UICONTROL Start] en [!UICONTROL End] in de sectie [!UICONTROL Completed date] in. |
| [!UICONTROL Status] | Als u logbestanden wilt filteren op basis van de [!UICONTROL Status] van de query, selecteert u het desbetreffende keuzerondje. De beschikbare opties zijn [!UICONTROL Submitted] , [!UICONTROL In progress] , [!UICONTROL Success] en [!UICONTROL Failed] . U kunt logbestanden alleen filteren op basis van één statusvoorwaarde tegelijk. |
| [!UICONTROL Client] | Als u logbestanden wilt filteren op basis van de gebruikte queryclient, voert u een van de volgende toegestane waarden in het vrije tekstveld in: `API`, `Adobe Query Service UI` of `QsAccel` . |
| [!UICONTROL My queries] | Gebruik de schakeloptie [!UICONTROL My queries] om de logbestanden te filteren voor query&#39;s die door u worden uitgevoerd. |
| [!UICONTROL query log ID] | Als u wilt filteren op basis van de unieke log-id van een query, voert u de log-id in het vrije tekstveld in. Deze informatie vindt u in [!UICONTROL Log details] . |

Alle toegepaste filters worden weergegeven boven de gefilterde logresultaten.

![ het lusje van het Logboek van de werkruimte van Vragen, met de lijst van toegepaste benadrukte filters.](../images/ui/query-log/applied-log-filters.png)

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in hoe de vraaglogboeken in de Dienst van de Vraag UI worden betreden en worden gebruikt.

Zie het [ overzicht UI ](./overview.md), of de [ gids van de Dienst API van de Vraag ](../api/getting-started.md) om meer over de mogelijkheden van de Dienst van de Vraag te leren.

Zie het [ document van monitorvragen ](./monitor-queries.md) leren hoe de Dienst van de Vraag de zichtbaarheid van geplande vraaglooppas verbetert.
