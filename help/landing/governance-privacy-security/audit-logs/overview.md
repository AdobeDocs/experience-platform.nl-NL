---
title: Overzicht controlelogboeken
description: Leer hoe u met controlelogboeken kunt zien wie welke acties in Adobe Experience Platform heeft uitgevoerd.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d4beb7691c8fb38359425509a40572ea9b09fd26
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 2%

---

# Controlelogboeken (bèta)

>[!IMPORTANT]
>
>De functie voor auditlogs in Adobe Experience Platform is momenteel in bèta en uw organisatie heeft er wellicht nog geen toegang toe. De functionaliteit die in deze documentatie wordt beschreven, kan worden gewijzigd.

Om de transparantie en zichtbaarheid van de in het systeem uitgevoerde activiteiten te vergroten, kunt u in Adobe Experience Platform gebruikersactiviteiten voor verschillende services en mogelijkheden controleren in de vorm van &quot;auditlogs&quot;. Deze logboeken vormen een auditspoor dat met het oplossen van problemenkwesties op Platform kan helpen, en uw zaken helpen effectief aan het beleid en de regelgevende vereisten van het collectieve gegevensbeheer voldoen.

Eenvoudig gezegd, vertelt een controlelogboek **Who** uitgevoerde **wat** actie, en **when**. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Dit document behandelt controlelogboeken in Platform, met inbegrip van hoe te om hen in UI of API te bekijken en te beheren.

## Gebeurtenistypen die zijn vastgelegd in auditlogboeken {#category}

In de volgende tabel wordt aangegeven op welke acties de middelen in de auditlogboeken worden vastgelegd:

| Resource | Acties |
| --- | --- |
| [Gegevensset](../../../catalog/datasets/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen voor [Real-time klantprofiel](../../../profile/home.md)</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Klasse](../../../xdm/schema/composition.md#class) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Veldgroep](../../../xdm/schema/composition.md#field-group) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Gegevenstype](../../../xdm/schema/composition.md#data-type) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Herstellen</li><li>Verwijderen</li></ul> |
| [Bestemming](../../../destinations/home.md) | <ul><li>Activeren</li></ul> |

## Toegang tot auditlogboeken

Wanneer de eigenschap voor uw organisatie wordt toegelaten, worden de controlelogboeken automatisch verzameld aangezien de activiteit voorkomt. U te hoeven niet om logboekinzameling manueel toe te laten.

Als u controlelogboeken wilt weergeven en exporteren, moet u de toegangsbeheermachtiging &quot;Auditlogboeken weergeven&quot; hebben (gevonden onder de categorie &quot;Gegevensbeheer&quot;). Raadpleeg de [documentatie voor toegangsbeheer](../../../access-control/home.md) voor meer informatie over het beheren van individuele machtigingen voor functies van Platforms.

## Het beheren van controlelogboeken in UI

U kunt controlelogboeken voor verschillende eigenschappen van het Experience Platform binnen de **[!UICONTROL Audits]** werkruimte in Platform UI bekijken. De werkruimte bevat een lijst met opgenomen logbestanden, die standaard van de meest recente naar de minst recente logbestanden worden gesorteerd.

![Het dashboard voor controlelogboeken](../../images/audit-logs/audits.png)

Het systeem geeft alleen auditlogboeken van het laatste jaar weer. Logboeken die deze limiet overschrijden, worden automatisch uit het systeem verwijderd.

Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven.

![Gebeurtenisdetails](../../images/audit-logs/select-event.png)

Selecteer het trechter-pictogram (![Filterpictogram](../../images/audit-logs/icon.png)) om een lijst met filterbesturingselementen weer te geven voor een kleiner resultaat.

![Filters](../../images/audit-logs/filters.png)

De volgende filters zijn beschikbaar voor controlegebeurtenissen in UI:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Category] | Gebruik het vervolgkeuzemenu om de weergegeven resultaten te filteren op [category](#category). |
| [!UICONTROL Action] | Filteren op handeling. Momenteel kunnen alleen [!UICONTROL Create]- en [!UICONTROL Delete]-handelingen worden gefilterd. |
| [!UICONTROL Access Control Status] | Filter door of de actie was toegestaan (voltooid) of wegens gebrek aan [toegangsbeheer](../../../access-control/home.md) toestemmingen werd ontkend. |
| [!UICONTROL Date] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |

Als u een filter wilt verwijderen, selecteert u de X op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** om alle filters te verwijderen.

![Filters wissen](../../images/audit-logs/clear-filters.png)

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
