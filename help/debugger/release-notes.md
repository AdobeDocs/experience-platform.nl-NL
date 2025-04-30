---
title: Aanvullende informatie over Adobe Experience Platform Debugger
description: De nieuwste aanvullende informatie voor Adobe Experience Platform Debugger.
keywords: foutopsporing;Experience Platform Debugger-extensie;Chrome;extensie;aanvullende informatie
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: f32c4bbf48fce2ada7cf7b75efc82e28d1ec26ff
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 93%

---

# Aanvullende informatie over Adobe Experience Platform Debugger

## Versie 1.6.3 - 30 april 2025

### Oplossingen en verbeteringen

* Probleem verholpen waarbij Foutopsporing DTM- en Launch-functies verhindert te werken.
* Probleem verholpen waarbij Analytics Post-Processors Hits niet in logs zou worden weergegeven.
* Probleem verholpen waarbij gegevens in niet-ASCII-talen zoals Japans niet correct worden weergegeven in logboeken.

## Versie 1.6.2 - woensdag 1 oktober 2024

### Oplossingen en verbeteringen

* Foutopsporing was te gevoelig voor alle CSP-fouten. Dit probleem is nu opgelost.

## Versie 1.6.1 - 25 juli 2024

### Oplossingen en verbeteringen

* Er is een probleem opgelost waarbij gebruikers geen nieuwe Tags-insluitcodes konden toevoegen op pagina&#39;s zonder deze codes.

## Versie 1.6.0 - 11 juli 2024

### Nieuwe functies

* Gebruikers hebben de mogelijkheid om zich aan of af te melden voor het delen van technische en persoonlijke gegevens.

### Oplossingen en verbeteringen

* Firefox-scriptinjectie en koppeling naar privacybeleid opgelost.
* Er zijn ontbrekende aanvragen van Analytics vastgelegd.
* Vastlopen op pagina&#39;s met veel complexe consoleberichten is opgelost.
* De Adobe Experience Platform Debugger is bijgewerkt naar een Manifest v3-extensie.

## Versie 1.5.4 - 19 december 2023

### Oplossingen en verbeteringen

* Er is een probleem opgelost waarbij instellingen niet werden behouden.
* Er is een probleem opgelost waarbij de Debugger vastliep tijdens het bekijken van verwerkte resultaten van Analytics.

## Versie 1.5.3 - 6 december 2023

### Nieuwe functies

* De instelling Actief tabblad vergrendelen bij het openen van de Debugger is toegevoegd.

### Oplossingen en verbeteringen

* Er is een probleem opgelost waarbij verzoeken van Analytics ontbraken op privédomeinen.
* Er is een probleem opgelost waarbij Activity Map-gegevens ontbraken in de verzoekentabel van Analytics.
* Er is een probleem opgelost waarbij het weergeven van de Target Trace ertoe zou leiden dat het programma vastloopt.
* Er is een waarschuwing toegevoegd voor als de Debugger geen on-page-infrastructuur kan instellen in Firefox.

## Versie 1.5.2 - 10 november 2023

(alleen Firefox)

### Oplossingen en verbeteringen

* De ordening van bestanden is bijgewerkt.

## Versie 1.5.1 - 2 november 2023

### Oplossingen en verbeteringen

* Er zijn problemen opgelost waarbij Analytics-gebeurtenissen werden genegeerd of gedupliceerd.
* Er is een probleem opgelost waarbij waarbij de maximale opslaggroottestatus werd overschreden.
* Er is een probleem opgelost waarbij de Edge Logs-zoekopdracht geen gebeurtenissen filterde.

## Versie 1.5.0 - 19 oktober 2023

### Nieuwe functies

* Koppelingen naar eigenschappen, omgeving en regels worden weergeven in het overzicht en logbestand van Tags.

### Oplossingen en verbeteringen

* Er is een probleem opgelost waarbij de samenvattingsgegevens van Tags niet werden verzonden.
* Er is een probleem opgelost waarbij Assurance-sessies een CORS-fout konden opleveren
* Er is een probleem opgelost waardoor Target Trace niet kon worden weergegeven.
* Er is een probleem opgelost met de knop Feedback verzenden.
* Er is een probleem opgelost met de ontbrekende Datastream ID in het Web SDK-overzicht voor versie ≥ 2.18.0.
* Er is een probleem opgelost waarbij Edge-logboekbestanden niet konden worden doorzocht.
* Een opmerking toegevoegd over extra profielen voor bepaalde accounttypen.

## Versie 1.4.1 - 1 november 2022

* Prestaties zijn verbeterd op pagina&#39;s met veel Adobe Experience Platform Assurance-gebeurtenissen.

## Versie 1.4.0 - 3 oktober 2022

* Ondersteuning voor AEP Assurance-foutopsporing toegevoegd voor hybride implementaties van Web SDK.
* Ondersteuning toegevoegd voor meerdere tabbladen binnen dezelfde AEP Assurance-sessie.
* Er is een probleem opgelost waarbij gebruikers na het aanmelden niet van profiel/organisatie konden wisselen.
   * Voor sommige accounts is afmelden en opnieuw aanmelden vereist om van organisatie te wisselen.
* Foutbericht toegevoegd voor wanneer het inschakelen van Target Trace mislukt.
* Bijgewerkte afhankelijkheden.

## Versie 1.3.3 - 20 juni 2022

* Er is een probleem opgelost waarbij pop-ups niet konden worden geopend in netwerkgebeurtenistabellen.
* Er is een probleem opgelost waarbij de Alloy-gegevens op de pagina niet konden worden geladen.

## Versie 1.3.2 - 9 juni 2022

* Er is een standaardavatar toegevoegd voor wanneer de gebruiker zich aanmeldt.
* Er is syntaxismarkering toegevoegd aan JSON-objecten in logbestanden.

## Versie 1.3.1 - 24 mei 2022

* Bijgewerkte afhankelijkheden.
* Er is een probleem opgelost met Analytics waarbij verwerkte resultaten niet konden worden ingeschakeld.
* Er is een probleem opgelost waarbij het foutopsporingsprogramma werd gekoppeld aan het aanmeldvenster voor Adobe.
* Er is een probleem opgelost met AT.js waarbij logberichten in Foutopsporing niet werden weergegeven.

## Versie 1.3.0 - 28 januari 2022

* Koppeling Informatie toegevoegd om huidige releaseversie en notities weer te geven.
* Er is een schakeloptie toegevoegd voor het weergeven van verwerkte resultaten voor Analytics-verzoeken. De schakeloptie is beschikbaar in de sectie Analytics.
* Er is een probleem opgelost met sessies voor foutopsporing op afstand wanneer de sessie buiten het foutopsporingsprogramma werd gesloten.
* Er is een probleem opgelost met een foutmelding die werd weergegeven op het tabblad Web SDK Edge-transacties.
* Er is een probleem opgelost met Adobe Tags op de pagina-afbrekingswaarschuwing wanneer de foutopsporing toegang kreeg tot het object _satellite.
* Er is een probleem opgelost waarbij een AppMeasurement-instantie niet op de pagina werd gevonden.
* Er is een probleem opgelost met paginaverbinding dat optrad bij het voor het eerst openen van het foutopsporingsvenster.

## Versie 1.2.0 - 26 oktober 2021

* Geef gebeurtenissen weer vanaf alle browsertabbladen in de netwerkweergave. Als u alleen de gebeurtenissen vanaf het huidige tabblad wilt zien, selecteert u het vergrendelingspictogram in de rechterbenedenhoek van het foutopsporingsprogramma.
* Branding bijgewerkt.

## Versie 1.1.0 - 5 oktober 2021

* Visualisatie van foutopsporing op afstand - ordening van de gebeurtenissen voor foutopsporing op afstand in een visueel stroomdiagram in de sectie Adobe Experience Platform Web SDK > Edge Transactions.
* Vereiste dat de Adobe Experience Platform Web SDK-organisatie die op de pagina wordt gebruikt, overeenkomt met de aangemelde organisatie bij het starten van een nieuwe sessie voor foutopsporing op afstand.
* Alleen de Edge-transacties voor het verbonden tabblad worden weergegeven. Target Trace-logbestanden zijn nog steeds beschikbaar in de sectie Logbestanden > Edge.
* Afzonderlijke configuratieopheffing van de gegevensstroom-ID worden toegestaan voor elke instantie van de Adobe Experience Platform Web SDK op de pagina. Er is een schakeloptie voor foutopsporing toegevoegd.
* Er is een probleem opgelost waarbij de Adobe Target Trace-token soms niet werd verzonden tijdens foutopsporingssessies op afstand voor de Adobe Experience Platform Web SDK.

## Versie 1.0.0 5 mei 2021

* Eerste hoofdrelease van de Experience Platform Debugger. Bedoeld ter vervanging van de Experience Cloud Debugger.
