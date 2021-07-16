---
title: Bronnen verwijderen
description: Leer hoe u tagbronnen kunt verwijderen in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Bronnen verwijderen

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Als u een bron verwijdert, wordt die bron permanent uit Adobe Experience Platform verwijderd. Als u nog de bron in de UI van de Inzameling van Gegevens wilt verschijnen, maar niet in uw markeringsbibliotheek, zie [Middelen uit een Bibliotheek verwijderen](remove-resources-from-library.md).

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

Nadat het gegevenselement is verwijderd, wordt niet langer de juiste waarde tijdens runtime geretourneerd. Er wordt een lege tekenreeks geretourneerd of de naam van het verwijderde gegevenselement wordt omsloten in %% (voorbeeld: `%data-element-name%`). Dit gedrag kan worden geconfigureerd in Eigenschapinstellingen.

U kunt deze gebiedsdelen oplossen vóór of nadat u het gegevenselement schrapt.

#### Extensies

Alle andere middelen (regels, regelcomponenten, en gegevenselementen) worden verstrekt door uitbreidingen.

De componenten van de regel en gegevenselementen hangen van uitbreidingen voor hun gedrag af, maar ook enkel om in het gebruikersinterface van de Inzameling van Gegevens worden getoond. Als u de extensie verwijdert voordat u afhankelijkheden oplost, kunt u deze zwevende bronnen niet meer weergeven. Deze zwevende bronnen worden weergegeven in de lijstweergaven, maar er wordt een fout weergegeven wanneer u de detailweergave probeert te openen.

Om deze reden, zou u zeer zorgvuldig moeten zijn wanneer het schrappen van uitbreidingen en u gebiedsdelen zou moeten oplossen alvorens u hen schrapt.

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
1. Publiceer de uitgeschakelde bron tot aan Production.
1. Verwijder de bron.

## Een bron verwijderen

Van de aangewezen lijstmening, selecteer het middel u wilt schrappen, dan **[!UICONTROL Delete]** selecteren.
