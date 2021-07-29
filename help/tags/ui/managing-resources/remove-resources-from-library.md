---
title: Bronnen uit een bibliotheek verwijderen
description: Leer hoe u bronnen uit een tagbibliotheek kunt verwijderen.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Bronnen uit een bibliotheek verwijderen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Wanneer u niet meer een middel een effect binnen een bouwstijl wilt hebben, moet u het uit de bibliotheek verwijderen die dat middel bevat en een nieuwe bouwstijl creëren.

>[!IMPORTANT]
>
>De middelen in bibliotheken zijn onderling afhankelijk. Het verwijderen van een middel uit een bouwstijl kan het gedrag van andere middelen in de bouwstijl veranderen.

Het verwijderingsproces werkt iets anders, afhankelijk van de status van de bibliotheek.

## Ontwikkelingsbibliotheken

De middelen in de bibliotheken van de Ontwikkeling kunnen direct worden gemanipuleerd.

1. Open de bibliotheek.
1. Verwijder de bron.
1. Sla de bibliotheek op.
1. De bibliotheek samenstellen.

## Verzonden en goedgekeurde bibliotheken

De middelen die in Voorgelegde of Goedgekeurde bibliotheken zijn kunnen niet direct worden gemanipuleerd. U moet de bibliotheek terugzetten naar de ontwikkelingsstatus.

1. Wijs de bibliotheek af (verplaats de bibliotheek terug naar Development).
1. Voer de stappen in &quot;Ontwikkelingsbibliotheken&quot; hierboven uit om bronnen uit Ontwikkelingsbibliotheken te verwijderen.

## Productiebibliotheken

Het is het meest complexe geval om bronnen uit een productiebibliotheek te verwijderen. U kunt de bibliotheekbronnen in deze status niet bewerken en u kunt deze bibliotheken ook niet terugzetten naar de ontwikkelingsstatus.

In plaats daarvan moet u de resource uitschakelen. Dit het onbruikbaar maken is een verandering die u dan aan een bibliotheek van de Ontwikkeling enkel als een andere verandering toevoegt. Zodra deze verandering in Productie wordt gezet, wordt het middel verplaatst van uw bibliotheek van de Productie.

1. Schakel de resource uit.
   1. Selecteer de bron in de lijstweergave.
   1. Selecteer **[!UICONTROL Disable]**.
1. Maak een nieuwe ontwikkelingsbibliotheek.
1. Voeg de `latest`-versie van de uitgeschakelde bron toe.
1. Opslaan en samenstellen.
1. Volg uw normale proces voor het promoten van bibliotheken naar Productie.
1. Publiceren naar productie om de bron te verwijderen.
