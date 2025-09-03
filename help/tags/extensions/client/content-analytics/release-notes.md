---
title: Opmerkingen bij de release Adobe Content Analytics Extension
description: De meest recente release bevat informatie over de Content Analytics-tagextensie in Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 77d19ab813f881cd3c48c27ed4a9ac02e268e23f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Opmerkingen bij de release Adobe Content Analytics-extensie

Hieronder volgt een lijst met releaseopmerkingen voor de Content Analytics-tagextensie.

| Versie | Datum | Oplossingen |
|---|---|---|
| 1,0,48 | 25 augustus 2025 | <ul><li>Hiermee voegt u ondersteuning toe voor het bijhouden van elementen in de DOM-elementen van de schaduwhoofdmap van een document.</li></ul> |
| 1,0,47 | 23 jul. 2025 | <ul><li>Het probleem dat optrad wanneer ervaringen niet waren ingeschakeld, is opgelost. Hierdoor is de reguliere-expressiecontrole op ervaringen mislukt. Door dit probleem konden geen Content Analytics-gegevens worden verzameld.</li><li>Probleem opgelost met de standaardtaalinstelling die ervoor zorgde dat de interface voor tags niet kon worden weergegeven voor sommige gebruikers die hun primaire standaardtaal niet in Experience Cloud hadden ingesteld.</li></ul> |
| 1,0,46 | 18 jun. 2025 | <ul><li>Er is een pop-upmelding toegevoegd bij het opslaan van de extensieconfiguratie als er geen productiegegevensstroom aanwezig is.</li><li>Het zichtbaarheidsprobleem van de Content Analytics-lading is tijdelijk opgelost door de stringified payload-inhoud in plaats daarvan in de console te plaatsen.</li><li>Ondersteuning voor lokalisatie toegevoegd aan de gebruikersinterface van Extension.</li><li>Oplossing voor een CSS-probleem dat extra opvulling veroorzaakte rond de inhoud van de Extension UI.</li></ul> |
| 1,0,45 | 14 apr. 2025 | <ul><li>Verschillende bugs in de configuratie-instellingen met betrekking tot het houden van Content Analytics-gebeurtenissen tijdens het wachten op paginaweergavegebeurtenissen zijn opgelost. Content Analytics wacht nu standaard tot de gebeurtenis voor de weergave van de EERSTE pagina plaatsvindt.</li></ul> |
| 1,0,44 | 31 mrt. 2025 | <ul><li>Eerste herhaling van de AppMeasurement-integratie.</li><li>Deze versie biedt nog geen ondersteuning voor het filteren van specifieke aanvragen (bijvoorbeeld paginaweergaven), maar deze functionaliteit kan in een toekomstige update worden toegevoegd. Momenteel wordt het eerste AppMeasurement-exemplaar op de pagina gebruikt.</li></ul> |
| 1,0,43 | 10 mrt. 2025 | <ul><li>Eerste release van extensie.</li></ul> |
