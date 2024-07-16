---
title: Bronnen verwijderen
description: Leer hoe u tagbronnen kunt verwijderen in Adobe Experience Platform.
exl-id: c8e26720-1976-48ec-8490-3d4ce587831e
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Bronnen verwijderen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Als u een bron verwijdert, wordt die bron permanent uit Adobe Experience Platform verwijderd. Als u een middel uit een specifieke markeringsbibliotheek wilt verwijderen, maar nog dat middel beschikbaar voor gebruik in andere bibliotheken wilt zijn, zie de gids op [ verwijderend middelen uit een bibliotheek ](remove-resources-from-library.md).

U kunt gegevenselementen, regels, extensies, hosts, omgevingen en eigenschappen verwijderen. Zodra geschrapt, zijn deze middelen niet terugvorderbaar.

De middelen die aan bibliotheken (gegevenselementen, regels, en uitbreidingen) worden toegevoegd hebben speciale overwegingen wanneer u hen schrapt.

## Een bron voorbereiden voor verwijdering

De middelen bestaan in verschillende staten en zij hangen van elkaar af. Voordat u een bron verwijdert, moet u ervoor zorgen dat deze zich in een toestand bevindt waarin deze kan worden verwijderd.

Het voorbereiden van een middel voor schrapping bestaat uit twee basisstappen:

1. Los gebiedsdelen op.
1. Verwijderen uit bibliotheken.

### Afhankelijkheden oplossen

Regels, gegevenselementen en extensies zijn onderling afhankelijk. Wanneer u een regel verwijdert, is er meestal een trapsgewijs effect en hebt u andere dingen die u moet opruimen.

#### Regels

De regels hangen van andere middelen (uitbreidingen en gegevenselementen) af, maar zij hebben geen middelen die van hen afhangen. Als u een regel verwijdert, kunt u deze niet meer gebruiken in een bibliotheek of zelfs maar weergeven, maar hebt u daarna geen afhankelijkheden om op te schonen.

#### Gegevenselementen

De elementen van gegevens hangen van uitbreidingen af, maar in tegenstelling tot regels, kunnen de gegevenselementen regels en uitbreidingen hebben die van hen afhangen. Als u een gegevenselement verwijdert, worden alle regels of extensies die van dit gegevenselement afhankelijk zijn, beïnvloed.

Nadat het gegevenselement is verwijderd, wordt niet langer de juiste waarde tijdens runtime geretourneerd. Er wordt een lege tekenreeks geretourneerd of de naam van het verwijderde gegevenselement wordt omsloten in %% (bijvoorbeeld: `%data-element-name%`). Dit gedrag kan worden geconfigureerd in Eigenschapinstellingen.

U kunt deze gebiedsdelen oplossen vóór of nadat u het gegevenselement schrapt.

#### Extensies

Alle andere middelen (regels, regelcomponenten, en gegevenselementen) worden verstrekt door uitbreidingen.

De componenten van de regel en gegevenselementen hangen van uitbreidingen voor hun gedrag af, maar ook enkel om in het gebruikersinterface van de Inzameling van Gegevens worden getoond. Als u de extensie verwijdert voordat u afhankelijkheden oplost, kunt u deze zwevende bronnen niet meer weergeven. Deze zwevende bronnen worden weergegeven in de lijstweergaven, maar er wordt een fout weergegeven wanneer u de detailweergave probeert te openen.

Daarom moet u zeer voorzichtig zijn wanneer u extensies verwijdert en afhankelijkheden moet oplossen voordat u ze verwijdert.

### Verwijderen uit bibliotheken

Voordat u een bron kunt verwijderen, moet u deze verwijderen uit alle bibliotheken die deze bevatten. Dit proces is afhankelijk van de status van de bibliotheek.

#### Ontwikkeling

1. Open de bibliotheek.
1. Verwijder de bron.
1. Sla de bibliotheek op.
1. Verwijder de bron.

#### Ingediend of goedgekeurd

1. Weiger de bibliotheek (verplaats deze terug naar Development).
1. Voer de bovenstaande stappen uit om een bron uit een ontwikkelingsbibliotheek te verwijderen.

#### Productie

1. Schakel de resource uit.
1. Publish the disabled resource through to Production.
1. Verwijder de bron.

## Een bron verwijderen

Selecteer in de toepasselijke lijstweergave de bron die u wilt verwijderen en selecteer vervolgens **[!UICONTROL Delete]** .
