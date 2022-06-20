---
title: Opmerkingen bij de release Adobe Experience Platform Debugger
description: De meest recente release bevat informatie over Adobe Experience Platform Debugger.
keywords: debugger;ervaar de uitbreiding van Foutopsporing van het Platform;chroom;uitbreiding;versie nota's
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: b4e3b40942390ef183ccb01f65702ae400a5e22f
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# Opmerkingen bij de release Adobe Experience Platform Debugger

## Versie 1.3.3 - 20 juni 2022

* Oplossing voor een probleem waardoor popups niet konden worden geopend in netwerkgebeurtenistabellen.
* Probleem opgelost waarbij gegevens op de pagina niet konden worden geladen.

## Versie 1.3.2 - 9 juni 2022

* Er is een standaardavatar toegevoegd wanneer de gebruiker is aangemeld.
* Er is syntaxismarkering toegevoegd aan JSON-objecten in logbestanden.

## Versie 1.3.1 - 24 mei 2022

* Bijgewerkte afhankelijkheden.
* Correctie van het probleem met Analytics waarbij resultaten na het proces niet konden worden ingeschakeld.
* Foutopsporingsprogramma bood verbinding met aanmeldvenster Adobe. Dit probleem is nu opgelost.
* Het probleem met AT.js waarbij logberichten niet werden weergegeven in Foutopsporing, is opgelost.

## Versie 1.3.0 - 28 januari 2022

* Koppeling Informatie toegevoegd om huidige releaseversie en notities weer te geven.
* Toegevoegde schakeloptie voor het weergeven van uitgevoerde resultaten voor analytische aanvragen. De schakeloptie is beschikbaar in de sectie Analytics.
* Probleem met externe foutopsporingssessie verholpen toen de sessie buiten foutopsporing werd gesloten.
* Het foutbericht dat werd weergegeven op het tabblad Edge Transactions van de Web SDK. Dit probleem is nu opgelost.
* Correctie van Adobe-tags op waarschuwing voor pagina-afdrukking wanneer de foutopsporing het object _satelliet heeft geopend.
* Probleem verholpen waarbij een instantie AppMeasurement niet op de pagina werd gevonden.
* Probleem met paginaverbinding verholpen die optrad bij de eerste keer dat het foutopsporingsvenster werd geopend.

## Versie 1.2.0 - 26 oktober 2021

* Gebeurtenissen weergeven vanaf alle browsertabbladen in de netwerkweergave. Als u alleen de gebeurtenissen vanaf het huidige tabblad wilt zien, selecteert u het vergrendelingspictogram in de rechterbenedenhoek van het foutopsporingsprogramma.
* Bijgewerkte branding.

## Versie 1.1.0 - 5 oktober 2021

* Visualisatie van foutopsporing op afstand - Organiseer de gebeurtenissen voor foutopsporing op afstand in een visueel stroomdiagram in de sectie Adobe Experience Platform Web SDK > Edge Transactions.
* Vereisen de Adobe Experience Platform Web SDK IMS org die op de pagina wordt gebruikt de het programma geopende org wanneer het beginnen van een nieuwe verre het zuiveren zitting aanpast.
* Alleen de randtransacties voor het verbonden tabblad weergeven. Logbestanden met doelsporen zijn nog steeds beschikbaar in de sectie Logs > Edge.
* Sta afzonderlijke de configuratieopheffing van identiteitskaart van de gegevensstroom voor elke instantie van het Web SDK van Adobe Experience Platform op de pagina toe. Schakelen tussen foutopsporing ingeschakeld toevoegen.
* Probleem verholpen waarbij het Adobe Target-traceringstoken niet altijd werd verzonden met foutopsporingssessies op afstand voor de Adobe Experience Platform Web SDK.

## Versie 1.0.0 5 mei 2021

* Eerste hoofdrelease van foutopsporing van Experience Platform. Bedoeld om de Experience Cloud Debugger te vervangen.
