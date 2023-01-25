---
title: Query-logbestanden
description: Logboeken van de vraag worden automatisch geproduceerd telkens als een vraag wordt uitgevoerd en beschikbaar door UI om met het oplossen van problemen te helpen. Dit document schetst hoe te om de sectie van de Logboeken van de Dienst van de Vraag van UI te gebruiken en te navigeren.
source-git-commit: 22deca5f9bcf6bcf97cca01b97fce9d22800b767
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---

# Zoekopdrachtlogs

Adobe Experience Platform houdt een logboek bij van alle vraaggebeurtenissen die door zowel API als UI voorkomen. Deze informatie is beschikbaar in de gebruikersinterface van de Query-service via de [!UICONTROL Logs] tab.

De logboekdossiers worden geproduceerd automatisch door om het even welke vraaggebeurtenis en bevatten informatie met inbegrip van gebruikte SQL, de status van de vraag, hoe lang het duurde, en laatste runtime. U kunt de gegevens van het vraaglogboek als krachtig hulpmiddel voor het oplossen van problemeninefficiënt of probleemvragen gebruiken. Meer uitvoerige logboekinformatie wordt gehouden als deel van de eigenschap van het controlelogboek en kan in worden gevonden [documentatie van auditlogboek](../../landing/governance-privacy-security/audit-logs/overview.md).

## Zoeklogs controleren

Selecteer [!UICONTROL Queries] om naar de werkruimte van de Dienst van de Vraag te navigeren en te selecteren [!UICONTROL Log] uit de beschikbare opties.

![De gebruikersinterface van het Platform met query&#39;s en log gemarkeerd.](../images/ui/query-log/logs.png)

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

U kunt ook een naam voor een querysjabloon selecteren in het menu [!UICONTROL Name] om rechtstreeks naar de [!UICONTROL Query log details] weergeven.

>[!NOTE]
>
>Als de query is gemaakt met de API en er tijdens de initialisatie geen sjabloonnaam is opgegeven, worden in plaats daarvan de eerste tientallen tekens van de SQL-query weergegeven.

![De gedetailleerde weergave van het logboek Query.](../images/ui/query-log/query-log-details.png)

Naast de sjabloonnaam van elke rij of het SQL-fragment bevindt zich een potloodpictogram (![Een potloodpictogram.](../images/ui/query-log/edit-icon.png)) die u kunt gebruiken om naar de Redacteur van de Vraag te navigeren. De vraag wordt dan pre-bevolkt in de redacteur voor het uitgeven.

![De werkruimte van het Logboek van Vragen met een benadrukt potloodpictogram.](../images/ui/query-log/edit-query.png)

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in hoe de vraaglogboeken in de Dienst van de Vraag UI worden betreden en worden gebruikt.

Zie de [Overzicht van gebruikersinterface](./overview.md)of de [API-handleiding voor query-service](../api/getting-started.md) om meer over de mogelijkheden van de Dienst van de Vraag te leren.

Zie de [document met query&#39;s controleren](./monitor-queries.md) leren hoe de Dienst van de Vraag de zichtbaarheid van geplande vraaglooppas verbetert.
