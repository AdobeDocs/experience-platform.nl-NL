---
title: Overzicht controlelogboeken
description: Leer hoe u met controlelogboeken kunt zien wie welke acties in Adobe Experience Platform heeft uitgevoerd.
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 2%

---

# Controlelogboeken (bèta)

>[!IMPORTANT]
>
>De functie voor auditlogs in Adobe Experience Platform is momenteel in bèta. De functionaliteit die in deze documentatie wordt beschreven, kan worden gewijzigd.

Om de transparantie en zichtbaarheid van de in het systeem uitgevoerde activiteiten te vergroten, kunt u in Adobe Experience Platform gebruikersactiviteiten voor verschillende services en mogelijkheden controleren in de vorm van &quot;auditlogs&quot;. Deze logboeken vormen een auditspoor dat met het oplossen van problemenkwesties op Platform kan helpen, en uw zaken helpen effectief aan het beleid en de regelgevende vereisten van het collectieve gegevensbeheer voldoen.

Eenvoudig gezegd, vertelt een controlelogboek **Who** uitgevoerde **wat** actie, en **when**. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Dit document behandelt controlelogboeken in Platform, met inbegrip van hoe te om hen in UI of API te bekijken en te beheren.

## Gebeurtenistypen die zijn vastgelegd in auditlogboeken

In de volgende tabel wordt aangegeven op welke acties de middelen in de auditlogboeken worden vastgelegd:

| Resource | Acties |
| --- | --- |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Herstellen</li><li>Verwijderen</li></ul> |
| [Gegevensset](../../../catalog/datasets/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen voor [Real-time klantprofiel](../../../profile/home.md)</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Veldgroep](../../../xdm/schema/composition.md#field-group) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Bestemming](../../../destinations/home.md) | <ul><li>Activeren</li></ul> |

## Toegang tot auditlogboeken

Wanneer de eigenschap voor uw organisatie wordt toegelaten, worden de controlelogboeken automatisch verzameld aangezien de activiteit voorkomt. U te hoeven niet om logboekinzameling manueel toe te laten.

Om controlelogboeken te bekijken en uit te voeren, moet u de &quot;de toegangsbeheertoestemming van de Controle van de Mening hebben wordt verleend. Raadpleeg de [documentatie voor toegangsbeheer](../../../access-control/home.md) voor meer informatie over het beheren van individuele machtigingen voor functies van Platforms.

## Het beheren van controlelogboeken in UI

U kunt controlelogboeken voor verschillende eigenschappen van het Experience Platform binnen de **[!UICONTROL Audits]** werkruimte in Platform UI bekijken. De werkruimte bevat een lijst met opgenomen logbestanden, die standaard van de meest recente naar de minst recente logbestanden worden gesorteerd.

![Het dashboard voor controlelogboeken](../../images/audit-logs/audits.png)

Het systeem geeft alleen auditlogboeken van het laatste jaar weer. Logboeken die deze limiet overschrijden, worden automatisch uit het systeem verwijderd.

Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven.

![Gebeurtenisdetails](../../images/audit-logs/select-event.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## Controlelogbestanden beheren in de API

Alle acties die u in UI kunt uitvoeren kunnen ook worden gedaan gebruikend API vraag. Zie [API referentiedocument](https://www.adobe.io/experience-platform-apis/references/audit-query/) voor meer informatie.

## Controlelogbestanden voor Adobe Admin Console beheren

Raadpleeg het volgende [document](https://helpx.adobe.com/enterprise/using/audit-logs.html) voor meer informatie over het beheren van auditlogs voor activiteiten in Adobe Admin Console.

## Volgende stappen

Deze gids besprak hoe te om controlelogboeken in Experience Platform te beheren. Zie de documentatie over [Observability Insights](../../../observability/home.md) en [monitoring van gegevensinvoer](../../../ingestion/quality/monitor-data-ingestion.md) voor meer informatie over hoe u de activiteiten van Platforms kunt controleren.