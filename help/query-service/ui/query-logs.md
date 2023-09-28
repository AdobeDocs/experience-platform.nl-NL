---
title: Query-logbestanden
description: Logboeken van de vraag worden automatisch geproduceerd telkens als een vraag wordt uitgevoerd en beschikbaar door UI om met het oplossen van problemen te helpen. Dit document schetst hoe te om de sectie van de Logboeken van de Dienst van de Vraag van UI te gebruiken en te navigeren.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 88498a1382202bed057b8dc52d09359ba02748ea
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Zoekopdrachtlogs

>[!IMPORTANT]
>
>Bepaalde functies voor querylogbestanden bevinden zich momenteel in een beperkte versie en zijn niet beschikbaar voor alle klanten. De gebruikersinterface kan er anders uitzien zonder een bewerkingspictogram. Ook, kan het proces om een vraagnaam te selecteren aan de Redacteur van de Vraag in plaats van het [!UICONTROL Query log details] weergeven.

Adobe Experience Platform houdt een logboek bij van alle vraaggebeurtenissen die door zowel API als UI voorkomen. Deze informatie is beschikbaar in de gebruikersinterface van de Query-service via de [!UICONTROL Logs] tab.

De logboekdossiers worden geproduceerd automatisch door om het even welke vraaggebeurtenis en bevatten informatie met inbegrip van gebruikte SQL, de status van de vraag, hoe lang het duurde, en laatste runtime. U kunt de gegevens van het vraaglogboek als krachtig hulpmiddel voor het oplossen van problemeninefficiënt of probleemvragen gebruiken. Meer uitvoerige logboekinformatie wordt gehouden als deel van de eigenschap van het controlelogboek en kan in worden gevonden [documentatie van auditlogboek](../../landing/governance-privacy-security/audit-logs/overview.md).

## Zoeklogs controleren

Selecteer [!UICONTROL Queries] om naar de werkruimte van de Dienst van de Vraag te navigeren en te selecteren [!UICONTROL Log] uit de beschikbare opties.

![De platforminterface met query&#39;s en log gemarkeerd.](../images/ui/query-log/logs.png)

## Aanpassen en zoeken {#customize-and-search}

Logboeken van de Dienst van de vraag worden voorgesteld in een klantgerichte lijstformaat. Als u de tabelkolommen wilt aanpassen, selecteert u het pictogram Instellingen (![Een instellingenpictogram.](../images/ui/query-log/settings-icon.png)) rechts van het scherm. A [!UICONTROL Customize Table] wordt weergegeven waar u elke kolom kunt uitschakelen.

U kunt ook naar logboeken zoeken die betrekking hebben op specifieke vraagmalplaatjes door de malplaatjenaam in het onderzoeksgebied te typen.

![De werkruimte van het Logboek van Vragen met de onderzoeksbar en beheert benadrukte dropdown van de kolomlijst.](../images/ui/query-log/customize-logs.png)

A [beschrijving voor elk van de kolommen van de logboeklijst](./overview.md#log) vindt u in het gedeelte Logboek van het overzicht van de Query-service.

## Loggegevens detecteren

Elke rij vertegenwoordigt logboekgegevens voor een vraaglooppas verbonden aan een vraagmalplaatje. Selecteer een rij in de tabel om de rechterzijbalk te vullen met loggegevens voor die uitvoering.

![De werkruimte van het Logboek van Vragen met een geselecteerde rij en de logboekgegevens in juiste sidebar benadrukt.](../images/ui/query-log/log-details.png)

In het paneel van logboekdetails, kunt u een nieuwe outputdataset selecteren en de volledige SQL vraag zien of kopiëren die in de looppas werd gebruikt.

![De werkruimte van het Logboek van Vragen met een geselecteerde rij en de benadrukte outputdataset en SQL vraag.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Bepaalde functies voor querylogbestanden bevinden zich momenteel in een beperkte versie en zijn niet beschikbaar voor alle klanten.

U kunt ook een naam voor een querysjabloon selecteren in het menu [!UICONTROL Name] om rechtstreeks naar de [!UICONTROL Query log details] weergeven.

>[!NOTE]
>
>Als de query is gemaakt met de API en er tijdens de initialisatie geen sjabloonnaam is opgegeven, worden in plaats daarvan de eerste tientallen tekens van de SQL-query weergegeven.

![De gedetailleerde weergave van het logboek Query.](../images/ui/query-log/query-log-details.png)

## Logboeken bewerken {#edit-logs}

Naast de sjabloonnaam van elke rij of het SQL-fragment bevindt zich een potloodpictogram (![Een potloodpictogram.](../images/ui/query-log/edit-icon.png)) die u kunt gebruiken om naar de Redacteur van de Vraag te navigeren. De vraag wordt dan pre-bevolkt in de redacteur voor het uitgeven.

![De werkruimte van het Logboek van Vragen met een benadrukt potloodpictogram.](../images/ui/query-log/edit-query.png)

## Filterlogs {#filter-logs}

U kunt de lijst met querylogbestanden filteren op basis van verschillende instellingen. Selecteer het filterpictogram (![Het filterpictogram.](../images/ui/query-log/filter-icon.png)) linksboven in de werkruimte om een set filteropties te openen in de linkertrack.

![De werkruimte van het Logboek van Vragen met het benadrukte filterpictogram.](../images/ui/query-log/log-filter.png)

De lijst met beschikbare filters wordt weergegeven.

![De werkruimte van het Logboek van Vragen met de getoonde en benadrukte filteropties.](../images/ui/query-log/log-filter-settings.png)

In de volgende tabel is een beschrijving van elk filter weergegeven.

| Filter | Beschrijving |
| ------ | ----------- |
| [!UICONTROL Exclude dashboard queries] | Dit checkbox wordt toegelaten door gebrek en sluit logboeken uit die door de vragen worden geproduceerd die voor het produceren van inzichten worden gebruikt. Deze vragen zijn systeem geproduceerd en bedekken de verslagen van gebruiker geproduceerde logboeken noodzakelijk voor controle, het beheer en het oplossen van problemen. Schakel het selectievakje uit als u door het systeem gegenereerde logbestanden wilt weergeven. |
| [!UICONTROL Start date] | Om de logboeken voor vragen te filtreren die tijdens een specifieke periode werden gecreeerd, plaats [!UICONTROL Start] en [!UICONTROL End] in de [!UICONTROL Start date] sectie. |
| [!UICONTROL Completed date] | Om de logboeken voor vragen te filtreren die tijdens een specifieke periode werden voltooid, plaats [!UICONTROL Start] en [!UICONTROL End] in de [!UICONTROL Completed date] sectie. |
| [!UICONTROL Status] | Filterlogboeken op basis van de [!UICONTROL Status] Selecteer het juiste keuzerondje in de query. Tot de beschikbare opties behoren [!UICONTROL Submitted], [!UICONTROL In progress], [!UICONTROL Success], en [!UICONTROL Failed]. U kunt logbestanden alleen filteren op basis van één statusvoorwaarde tegelijk. |
| [!UICONTROL Client] | Als u logboeken wilt filteren op basis van de gebruikte queryclient, voert u een van de volgende toegestane waarden in het vrije tekstveld in: `API`, `Adobe Query Service UI`, of `QsAccel`. |
| [!UICONTROL My queries] | Gebruik de [!UICONTROL My queries] knevel om de logboeken voor vragen te filtreren die door u worden uitgevoerd. |
| [!UICONTROL query log ID] | Als u wilt filteren op basis van de unieke log-id van een query, voert u de log-id in het vrije tekstveld in. Deze informatie is te vinden in het [!UICONTROL Log details]. |

Alle toegepaste filters worden weergegeven boven de gefilterde logresultaten.

![Het tabblad Logboek van de werkruimte Query&#39;s, met de lijst met toegepaste filters gemarkeerd.](../images/ui/query-log/applied-log-filters.png)

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in hoe de vraaglogboeken in de Dienst van de Vraag UI worden betreden en worden gebruikt.

Zie de [Overzicht van gebruikersinterface](./overview.md)of de [API-handleiding voor query-service](../api/getting-started.md) om meer over de mogelijkheden van de Dienst van de Vraag te leren.

Zie de [document met query&#39;s controleren](./monitor-queries.md) leren hoe de Dienst van de Vraag de zichtbaarheid van geplande vraaglooppas verbetert.
