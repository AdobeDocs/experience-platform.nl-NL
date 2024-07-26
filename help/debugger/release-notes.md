---
title: Opmerkingen bij de release Adobe Experience Platform Debugger
description: De nieuwste aanvullende informatie voor Adobe Experience Platform Debugger.
keywords: foutopsporing;ervaring met de extensie Foutopsporing in platform;chroom;extensie;releaseopmerkingen
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 877e38154f6959d50bd0620290c2dce9decfc2b5
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Opmerkingen bij de release Adobe Experience Platform Debugger

## Versie 1.6.1 - 25 juli 2024

### Oplossingen en verbeteringen

* Probleem verholpen waarbij gebruikers geen nieuwe tags konden toevoegen die codes insloten op pagina&#39;s zonder deze codes.

## Versie 1.6.0 - 11 juli 2024

### Nieuwe functies

* Gebruikers de mogelijkheid bieden om zich aan te melden of te weigeren bij het verzamelen van technische en persoonlijke gegevens.

### Oplossingen en verbeteringen

* Firefox-scriptinjectie en link naar privacybeleid herstellen.
* Ontbrekende analytische aanvragen vastleggen.
* Vastlopen op pagina&#39;s met veel complexe consoleberichten corrigeren.
* Werk het Adobe Experience Platform Debugger bij naar een Manifest v3-extensie.

## Versie 1.5.4 - 19 december 2023

### Oplossingen en verbeteringen

* Probleem verholpen waarbij instellingen niet werden behouden.
* Probleem verholpen waarbij Foutopsporing vastliep tijdens het bekijken van Analytics Nabewerkte hits.

## Versie 1.5.3 - 6 december 2023

### Nieuwe functies

* Er is een vergrendeling toegevoegd op het actieve tabblad bij het openen van de instelling Foutopsporing.

### Oplossingen en verbeteringen

* Probleem verholpen waarbij verzoeken om Analytics op privédomeinen ontbraken.
* Probleem verholpen waarbij Activity Map gegevens zouden ontbreken in de tabel met analyseverzoeken.
* Probleem verholpen waarbij het weergeven van het doelspoor ertoe zou leiden dat het programma vastloopt.
* Er is een waarschuwing toegevoegd wanneer Foutopsporing geen infrastructuur op pagina in Firefox kan instellen.

## Versie 1.5.2 - 10 november 2023

(alleen Firefox)

### Oplossingen en verbeteringen

* De indeling van bestanden is bijgewerkt.

## Versie 1.5.1 - 2 november 2023

### Oplossingen en verbeteringen

* Gebeurtenissen Analytics werden genegeerd of gedupliceerd. Dit probleem is nu opgelost.
* Probleem verholpen waarbij de maximale opslaggrootte van de status werd overschreden.
* Probleem verholpen waarbij het zoeken naar Edge Logs geen gebeurtenissen zou filteren.

## Versie 1.5.0 - 19 oktober 2023

### Nieuwe functies

* Koppelingen naar eigenschappen, omgeving en regels weergeven in het overzicht en logbestand van tags.

### Oplossingen en verbeteringen

* Probleem verholpen waarbij geen gegevens van het overzicht van tags werden verzonden.
* Betrouwbaarheidssessies zouden een CORS-fout veroorzaken. Dit probleem is nu opgelost.
* Probleem verholpen waardoor Doelovertrekken niet kon worden weergegeven.
* De knop Feedback verzenden is nu opgelost.
* Probleem verholpen met de ontbrekende &quot;DataStream-id&quot; in de samenvatting van de SDK van het web voor versie ≥ 2.18.0.
* Probleem verholpen waarbij Edge-logbestanden niet konden worden doorzocht.
* Een opmerking toegevoegd over extra profielen voor bepaalde accounttypen.

## Versie 1.4.1 - 1 november 2022

* Verbeterde prestaties op pagina&#39;s met veel Adobe Experience Platform Assurance-gebeurtenissen.

## Versie 1.4.0 - 3 oktober 2022

* Toegevoegde AEP Assurance debugging support for Web SDK hybride implementaties.
* Toegevoegde steun veelvoudige lusjes binnen de zelfde zitting van de Verzekering AEP.
* Gebruikers konden na het aanmelden niet van profiel/organisatie wisselen. Dit probleem is nu opgelost.
   * Voor sommige rekeningen, wordt het programma openen en het programma openen vereist om organisaties te schakelen.
* Foutbericht toegevoegd wanneer het inschakelen van Doelovertrek mislukt.
* Bijgewerkte afhankelijkheden.

## Versie 1.3.3 - 20 juni 2022

* Oplossing voor een probleem waardoor popups niet konden worden geopend in netwerkgebeurtenistabellen.
* Probleem opgelost waarbij gegevens op de pagina niet konden worden geladen.

## Versie 1.3.2 - 9 juni 2022

* Er is een standaardavatar toegevoegd wanneer de gebruiker is aangemeld.
* Er is syntaxismarkering toegevoegd aan JSON-objecten in logbestanden.

## Versie 1.3.1 - 24 mei 2022

* Bijgewerkte afhankelijkheden.
* Correctie van het probleem met Analytics waarbij resultaten na het proces niet konden worden ingeschakeld.
* Foutopsporingsprogramma bood verbinding met aanmeldvenster voor Adobe. Dit probleem is nu opgelost.
* Het probleem met AT.js waarbij logberichten niet werden weergegeven in Foutopsporing, is opgelost.

## Versie 1.3.0 - 28 januari 2022

* Koppeling Informatie toegevoegd om huidige releaseversie en notities weer te geven.
* Toegevoegde schakeloptie voor het weergeven van uitgevoerde resultaten voor analytische aanvragen. De schakeloptie is beschikbaar in de sectie Analytics.
* Probleem met externe foutopsporingssessie verholpen toen de sessie buiten foutopsporing werd gesloten.
* Melding van fout is gecorrigeerd die werd weergegeven op het tabblad Transacties van de Web SDK Edge.
* Tags voor vaste Adobe op de pagina-afbrekingswaarschuwing wanneer de foutopsporing het object _satelliet heeft geopend.
* Probleem verholpen waarbij een AppMeasurement-instantie niet op de pagina werd gevonden.
* Probleem met paginaverbinding verholpen die optrad bij de eerste opening van het foutopsporingsvenster.

## Versie 1.2.0 - 26 oktober 2021

* Gebeurtenissen weergeven vanaf alle browsertabbladen in de netwerkweergave. Als u alleen de gebeurtenissen vanaf het huidige tabblad wilt zien, selecteert u het vergrendelingspictogram in de rechterbenedenhoek van het foutopsporingsprogramma.
* Bijgewerkte branding.

## Versie 1.1.0 - 5 oktober 2021

* Visualisatie van foutopsporing op afstand - Organiseer de gebeurtenissen voor foutopsporing op afstand in een visueel stroomdiagram in het gedeelte Adobe Experience Platform Web SDK > Edge Transactions.
* Vereisen de organisatie van SDK van het Web van Adobe Experience Platform die op de pagina wordt gebruikt de het programma geopende org wanneer het beginnen van een nieuwe verre het zuiveren zitting aanpast.
* Alleen de randtransacties voor het verbonden tabblad weergeven. Logbestanden met doelsporen zijn nog steeds beschikbaar in de sectie Logs > Edge.
* Sta afzonderlijke de configuratieopheffing van identiteitskaart van de gegevensstroom voor elke instantie van het Web SDK van Adobe Experience Platform op de pagina toe. Schakel foutopsporing in.
* Probleem verholpen waarbij het Adobe Target-traceringstoken niet altijd werd verzonden met foutopsporingssessies op afstand voor de Adobe Experience Platform Web SDK.

## Versie 1.0.0 5 mei 2021

* Eerste hoofdrelease van foutopsporing van Experience Platform. Bedoeld om het Experience Cloud Debugger te vervangen.
