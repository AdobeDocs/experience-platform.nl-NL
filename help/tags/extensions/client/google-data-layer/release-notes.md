---
title: Opmerkingen bij de release Google Data Layer Extension
description: De meest recente releaseopmerkingen voor de tagextensie Google Data Layer in Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: c1bad7d5414e62f4d77f7d5903f4b2bf4d9081f8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Opmerkingen bij de release Google Data Layer

## Versie 1.0.4

* Openbare bètaversie van de extensie.

## Versie 1.0.6

* Toevoeging van handeling om de gegevenslaag opnieuw in te stellen op de berekende status.
* Fouten in gegevenselement corrigeren die het ophalen van waarden uit de berekende status verhinderen.

## Versie 1.1.1

Een belangrijke verbetering en oplossing voor problemen die het resultaat zijn van feedback van bètatests.

* Hiermee wordt een probleem verholpen waarbij het gegevenselement Google Data Layer Extension dat wordt gebruikt in een niet-gegevenslaagregel (bijv. Bibliotheek geladen), het gegevenslaagobject retourneert, niet de berekende status.
* Hiermee wordt een probleem verholpen waarbij de berekende status van de gegevenslaag niet vanuit de hulplijn werd doorgegeven in gebeurtenissen op het moment dat de gebeurtenis werd geactiveerd, maar eerder op het moment dat de regel werd uitgevoerd.
* Voegt een knevel aan het dialoog van het gegevenselement toe dat een gebruiker toestaat om te kiezen als slechts waarden van gebeurtenissen zouden moeten zijn teruggekeerd.
* Hiermee wordt een probleem opgelost waarbij de gebeurtenisgeschiedenis niet correct is afgevangen door gebeurtenislisteners.
* Minder duidelijke code.

## Versie 1.2.0

* Voegt een actie toe om aan de gegevenslaag te duwen gebruikend een zeer belangrijk-waarde multifield dialoog.
* Hiermee corrigeert u een fout die ervoor zorgde dat de extensie niet kon worden geladen wanneer tags synchroon werden geïmplementeerd.
* Hiermee wordt een fout verholpen die een fout heeft veroorzaakt wanneer een gegevenselement in bepaalde omstandigheden wordt opgeslagen.
* Voegt documentatie toe aan het gebeurtenisdialoogvenster waarin het gebruik van het gebeurtenisobject Tags wordt uitgelegd.
* Voegt een waarschuwing over oneindige lijnen aan gebeurtenisdialoog toe.

## Versie 1.2.2

* Voegt ondersteuning toe voor Googles Analytics gtag()-gebeurtenissen.
