---
title: Opmerkingen bij de release Adobe Client Data Layer Extension
description: De recentste versienota's voor de de markeringsuitbreiding van de Laag van Gegevens van de Adobe Cliënt in Adobe Experience Platform.
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 1%

---

# Opmerkingen bij de release Adobe Client Data Layer-extensie

## Versie 2.0.2

* De ACDL-kernbibliotheek laden (versie 2.0.2)
* Versie 2.0.0 van de ACDL-kernbibliotheek heeft de mogelijkheid verwijderd om event.beforeState en event.afterState te benutten. Daarom hebben we deze objecten gewijzigd en altijd lege objecten geretourneerd. Implementaties die op deze functionaliteit vertrouwen, moeten worden bijgewerkt wanneer u naar deze versie gaat.

## Versie 1.1.3

* De ACDL-kernbibliotheek laden (versie 1.1.3)

## Versie 1.1.2

De volgende functionaliteit wordt bij de eerste release door de extensie geboden:

* De ACDL-kernbibliotheek laden (versie 1.1.1)
* De naam van de gegevenslaag Adobe wijzigen
* Gebeurtenissen:
   * Luisteren naar alle gebeurtenissen
   * Luisteren naar alle geduwde gegevens
   * Luisteren naar een specifieke geduwde gebeurtenis
   * Er kan naar alle gebeurtenissen worden geluisterd bij verschillende bereiken
* Gegevenselementen:
   * Berekende status: Algemene of specifieke staat
   * Grootte gegevenslaag
* Acties:
   * De grootte van de gegevenslaag opnieuw instellen (de nieuwste computerstatus behouden)
   * Object naar gegevenslaag duwen
