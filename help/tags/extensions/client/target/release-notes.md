---
title: Opmerkingen bij de release Adobe Target Extension
description: De meest recente release bevat informatie over de Adobe Target-tagextensie in Adobe Experience Platform.
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Target

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## 16 september 2021

### Adobe Target Extension 0.11.4

* Bijgewerkt naar at.js v1.8.3
* Toegevoegd `SameSite=None` en `Secure` kenmerken bij het instellen van cookies

## 24 juli 2020

### Adobe Target Extension 0.11.3

* Het probleem waarbij een extensie mislukte als een script of code wordt toegevoegd, is opgelost. `default` aan de `window` of `document`

## 15 juni 2020

### Adobe Target Extension 0.11.2

* Probleem verholpen bij het gebruik van CNAME en randoverschrijving, waarbij at.js 1.x het serverdomein mogelijk onjuist zou maken, wat tot gevolg had dat de aanvraag van het Doel mislukte

## 25 maart 2020

### Adobe Target Extension 0.11.1

* Bijgewerkt om 1.js tot v1.8.1
* Probleem verholpen waarbij params en params voor het laden van pagina&#39;s niet correct werden verwerkt

## 10 oktober 2019

### Adobe Target Extension 0.11.0

* Bijgewerkt om 1.js tot v1.8.
* Verbeterde prestaties voor integratie tussen Experience Cloud ID library (ECID) v4.4 en at.js 1.8.
* Eerder deed de ECID-bibliotheek twee blokkerende oproepen voordat at.js ervaringen kon ophalen. Dit is verminderd tot één enkele vraag, die beduidend prestaties verbetert.

>[!NOTE]
>Upgrade de extensie van de ECID-tag voor Adobe Experience Platform naar v4.4.1 om te profiteren van deze prestatieverbetering.

## 31 juli 2019

### Adobe Target Extension 0.10.1

* Hotfix voor parameters die de markeringsuitbreiding voor Adobe Target behandelen

## 4 mei 2019

### Adobe Target Extension 0.10.0

* Probleem met gegevenselementen verholpen die werd veroorzaakt door de meest recente Google Chrome-wijzigingen

## 14 maart 2019

### Adobe Target Extension 0.9.3

* Bijgewerkte extensie-versie voor gebruik in versie 1.js 1.7.1

## 20 februari 2019

### Adobe Target Extension 0.9.2

* Correctie van zeldzame omstandigheden tussen de extensies Doel en Analyse

## 12 februari 2019

### Adobe Target Extension 0.9.1

#### **Functies**

* Bijgewerkte extensie voor gebruik in versie 1.js 1.7.0 met de functie Inkoopprivacy die wordt ondersteund via tags om te bepalen hoe en wanneer de tag Doel wordt geactiveerd. Raadpleeg de documentatie bij tags over het instellen van de implementatie van Opt-in. Toegevoegde mogelijkheid om aan te passen of een mbox-parameter met een lege waarde al dan niet naar Target moet worden verzonden.

## 23 januari 2019

### Adobe Target Extension 0.8.4

* Bijgewerkt te.js aan versie 1.6.4
* Extension UI is gemigreerd naar Adobe-spectrum

## 15 november 2018

### Adobe Target Extension 0.8.2

* Bijgewerkt te.js aan versie 1.6.3

## 24 oktober 2018

### Adobe Target Extension 0.8.1

* Bijgewerkt te.js aan versie 1.6.2

## 23 augustus 2018

### Adobe Target Extension 0.8.0

* Bijgewerkt te.js aan versie 1.6.0

## 10 augustus 2018

### Adobe Target Extension 0.7.2

* Kleine wijzigingen
* De `exchangeUrl` eigenschap in de `extension.json` file

## 1 augustus 2018

### Adobe Target Extension 0.7.1

* Kleine correcties

## 18 juni 2018

### Adobe Target Extension 0.7.0

* Bijgewerkte versie van at.js naar 1.5.0
* Probleem verholpen waarbij Media Optimizer een null-referentiefout veroorzaakte in IE 11. Dit probleem is nu opgelost.

## 15 juni 2018

### Adobe Target Extension 0.6.0

#### **Functies**

* De doelextensie is bijgewerkt voor gebruik op versie 1.js v1.3.1. Wanneer u Doel met Analytics opstelt, wachten wij nu tot alle vraag van het Doel (met inbegrip van omleidingsaanbiedingen) alvorens Analytics heeft opgelost, die de rasvoorwaarde oplost die eerder bestond.

## 22 februari 2018

### Adobe Target Extension 0.4.1

#### **Functies**

* Aanbieding voor Adobe Exchange toegevoegd aan extension.json
* Er zijn controles toegevoegd om te zien of Doel is uitgeschakeld en of Authoring is ingeschakeld

#### **Bugfixes**

* Oplossing voor een fout in de Adobe Target-extensie die ervoor zorgde dat Visual Experience Composer de pagina niet kon verbergen wanneer deze via tags werd geïmplementeerd.

## 8 februari 2018

### Adobe Target Extension 0.4.0

#### **Functies**

* Bijgewerkte weergaven in extensieconfiguratieschermen
* at.js is bijgewerkt naar versie 1.2.3 (voegt ondersteuning voor JSON-aanbiedingen toe)
