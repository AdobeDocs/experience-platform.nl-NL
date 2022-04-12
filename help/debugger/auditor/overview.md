---
title: Tabblad Auditor
description: Leer hoe u het tabblad Audit in Adobe Experience Platform Debugger kunt gebruiken om uw Adobe Experience Cloud-implementaties te testen.
keywords: foutopsporing;ervaring met platformfoutopsporingsextensie;chroom;extensie;auditor;dtm;target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 9%

---

# Tabblad Auditor

In Adobe Experience Platform Debugger kunt u de opdracht **[!UICONTROL Auditor]** om een reeks controletests op uw pagina uit te voeren.

Deze functie gebruiken:

1. Selecteren **[!UICONTROL Auditor]** in de linkernavigatie.
1. Selecteer **[!UICONTROL Run Auditor Tests]**. Zodra de tests zijn voltooid, worden de resultaten hieronder weergegeven.

![Screenshot van testresultaten op het tabblad Auditor](../images/auditor-results.png)

In de resultatenlijst worden de test en het resultaat weergegeven en staan suggesties om eventuele problemen op te lossen.

## Testresultaten interpreteren

Elke test is gewogen en uw testscore is gelijk aan het toegewezen gewicht. Als u een test met een gewicht van 5 slaagt, krijgt u vijf punten.

| Score | Beschrijving |
| --- | --- |
| 0 | Hiermee wordt u gewaarschuwd voor problemen waarvan u op de hoogte moet zijn, maar die geen invloed hebben op uw score. |
| 1 | adviseert een optimalisering. Geen invloed op de gegevensnauwkeurigheid. |
| 2 | Als u deze test niet uitvoert, hebt u geen toegang tot de nieuwste functies en oplossingen in Adobe Experience Cloud. |
| 3 | Test op efficiëntie en of de implementatie de beste praktijken volgt. |
| 4 | Als dit mislukt, worden mogelijk onbetrouwbare gegevens verzameld. |
| 5 | Als dit mislukt, ziet u mogelijk gegevensverlies. |

Alle tests slagen of mislukken. Zij testen of aan de testvoorwaarden wordt voldaan of niet aan de testvoorwaarden wordt voldaan, zodat er geen gedeeltelijke scores voor gedeeltelijke naleving zijn. Bijvoorbeeld, als de test op de recentste versie van een oplossing van de Adobe controleert en u slechts één versie achter bent, krijgt u de zelfde score alsof u vijf versies terug bent. De meest recente versies bevatten prestatieverbeteringen en foutoplossingen. Daarom wordt aangeraden de meest recente versie te gebruiken.

Het wordt **ten zeerste aanbevolen** om resultaten van niveau 4 of 5 te corrigeren.

Het wordt **aanbevolen** om resultaten van niveau 1 tot 3 te corrigeren.

## Ondersteunde Adobe-technologieën

De controleeigenschap kan de volgende technologieën van Adobe beoordelen:

* Adobe Advertising Cloud DSP
* Adobe Advertising Cloud Search
* Adobe Analytics
* Adobe Experience Cloud Identity Service
* Adobe Target
* Tags (voorheen Adobe Experience Platform Launch)

## Testpuin

Raadpleeg de volgende documenten voor meer informatie over de testrubrics die door deze functie worden geleverd:

* [Codeconsistentie](./tag-consistency.md)
* [Tagaanwezigheid](./tag-presence.md)
* [Configuratie](./configuration.md)
* [Waarschuwingen](./alerts.md)
