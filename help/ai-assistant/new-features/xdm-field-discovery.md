---
title: XDM Field Discovery met AI Assistant
description: Lees dit document om te leren hoe u AI Assistant voor XDM-velddetectie (Experience Data Model) kunt gebruiken.
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: 2348001facd7ae3a95254130ae377b4ef3f2a749
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# XDM-velddetectie voor met AI Assistant

>[!AVAILABILITY]
>
>Deze functie is in Alpha en is mogelijk niet beschikbaar voor uw organisatie. Neem contact op met het accountteam van uw Adobe als u wilt deelnemen aan het Alpha-programma en toegang wilt krijgen tot deze functie.

U kunt de Medewerker van AI gebruiken om naar gebieden van de Gegevens van de Ervaring te zoeken en te ontdekken (XDM) die u kunt dan gebruiken om gericht publiek binnen Experience Platform tot stand te brengen.

Lees de volgende tabel voor ondersteunde query- en prompt-patronen voor XDM-velddetectie in AI Assistant.

>[!TIP]
>
>Hoewel query- en promptiepatronen hetzelfde kunnen zijn in verschillende gebruiksgevallen, is de exacte formulering van een vraag afhankelijk van de XDM-velden en -schema&#39;s die voor een bepaalde sandbox worden gebruikt.

| Type query | Patroon query/prompt | Voorbeelden |
| --- | --- | --- |
| XDM-velddetectie door gegevensdomein of -gebied | Toon me de XDM gebieden die worden gebruikt om {DATA_DOMAIN/AREA} te vertegenwoordigen. | <ul><li>Toon me de XDM gebieden die worden gebruikt om toestemmingsgegevens te vertegenwoordigen.</li><li>Toon me de XDM gebieden die worden gebruikt om informatie over e-mailabonnementen te vertegenwoordigen.</li></ul> |
| XDM-velddetectie door algemene veldnaam | <ul><li>Toon me de XDM gebieden met betrekking tot {DATA_DOMAIN/AREA}.</li><li>Welke XDM-velden {GENERAL_FIELD_NAME} bevatten.</li></ul> | <ul><li>Toon me de XDM gebieden met betrekking tot orden.</li><li>Toon me de XDM gebieden met betrekking tot interactiedetails.</li><li>Welk XDM-veld bevat bezoeker-id&#39;s?</li><li>Welk XDM-veld bevat productcategorieën?</li></ul> |
| XDM field discovery by data model lineage | <ul><li>Toon me alle gebieden van {FIELD_GROUP/CLASS_NAME} die {GENERAL_FIELD_NAME} bevatten.</li><li>Wat is {FIELD_GROUP/CLASS_NAME} van het XDM-veld {GENERAL_FIELD_NAME}?</li></ul> | <ul><li>Toon me alle gebieden van de gebiedsgroep die productgegevens bevatten.</li><li>Toon me alle gebieden van de gebiedsgroep die analysegegevens bevat.</li><li>Wat is de klasse van het XDM gebied voornaam?</li><li>Wat is de klasse van de XDM gebied e-mailabonnementen?</li></ul> |
| Vragen om uitgebreide beschrijvingen samen met veldnamen | {FIELD_DISCOVERY_QUERY}. Voeg ook verbeterde beschrijvingen toe. | <ul><li>Toon me de XDM gebieden die worden gebruikt om toestemmingsgegevens te vertegenwoordigen. Neem ook de uitgebreide beschrijving voor het veld op.</li><li>Toon me de XDM gebieden met betrekking tot interactiedetails. Neem ook de uitgebreide beschrijving voor het veld op.</li></ul> |

{style="table-layout:auto"}