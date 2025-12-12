---
title: Opmerkingen bij de release Adobe Experience Cloud Identity Service Extension
description: De meest recente release bevat informatie over de extensie van de Adobe Experience Cloud Identity Service in Adobe Experience Platform.
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Cloud Identity Service

In dit document worden de opmerkingen bij de release voor de extensie van de Adobe Experience Cloud Identity Service besproken. Voor versienota&#39;s op de Dienst van de Identiteit van Experience Cloud zelf, gelieve te verwijzen naar de [ documentatie van de Dienst van de Identiteit ](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html).

## 17 okt. 2022

### Experience Cloud ID Extension 5.5.0

* De uitbreiding steunt nu versie 5.5.0 van de [ Cliënt JS van de Bezoeker ](https://github.com/Adobe-Marketing-Cloud/id-service). Verwijs naar de [ de versienota&#39;s van de Bezoeker ](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0) voor specifieke updates.

## 9 mrt. 2022

### Experience Cloud ID Extension 5.4.0

* Deze versie bevat de nieuwste versie van Visitor 5.4.0, die de volgende updates bevat:

   * Mogelijkheid om de levensduur van het `s_ecid` -cookie te configureren met behulp van cookieLifetime config
   * Update voor een browserprobleem van Firefox dat optreedt wanneer een pagina in een onderliggend iFrame wordt geladen

## 10 okt. 2021

### Experience Cloud ID Extension 5.3.1

* Deze versie bevat de nieuwste versie van Visitor 5.3.0, die de volgende nieuwe updates heeft:

   * Bijgewerkt algoritme om lokale ECID te produceren
   * Laatste plug-in met `Secure` - en `SameSite` -markeringen voor het privacycookie
   * Probleem met een Firefox-browser verhelpen wanneer een pagina in een onderliggend iFrame wordt geladen

## 12 jan. 2021

### Experience Cloud ID Extension 5.2.0

* Het bijwerken naar de VisitorJS 5.2.0-patch met een oplossing voor ECID DataElement kon niet worden bijgewerkt wanneer u toestemming kreeg.

## 3 nov. 2020

### Experience Cloud ID Extension 5.2.1

* Deze patch bevat een correctie voor het schrijven van cookies van een iFrame met kenmerk `SameSite=None` in Google Chrome browser.

## 27 okt. 2020

### Experience Cloud ID Extension 5.1.0

* `sameSiteCookie` config toevoegen om het `SameSite` -kenmerk van het `AMCV` cookie op te geven.
Deze config ondersteunt de volgende waarden voor het kenmerk `SameSite` :

   * `Strict`
   * `Lax`
   * `None`

De details van deze attributenwaarden zijn op [ web.dev ](https://web.dev/samesite-cookies-explained/) en [ chroom ](https://www.chromium.org/updates/same-site)


## 13 augustus 2020

### Experience Cloud ID Extension 5.0.1

* Bijwerken naar de VisitorJS 5.0.1-patch met een correctie voor het toevoegen van de d_cf-markering wanneer de IAB-toestemmingstekenreeks is gewijzigd.

## dinsdag 15 juni 2020

### Experience Cloud ID Extension 5.0.0

* Ondersteuning toevoegen voor `IAB TCF` - Transparency &amp; Consent Framework - `Version 2.0` .

## dinsdag 13 april 2020

### Experience Cloud ID Extension 4.6.0

* Markering `loadSSL` is standaard ingeschakeld. Alle aanroepen naar Identiteitsservice zijn standaard ingeschakeld in `https` . De klanten kunnen het aan vals plaatsen als zij de Diensten van de Identiteit op http van hun niet-ssl pagina&#39;s willen roepen.
* Bijgewerkt de functie die wordt gebruikt om Internet-Explorer (IE) versie te ontdekken, om een kwestie te bevestigen die door ESLint wordt gemeld.
* Opgeloste problemen voor een prestatieprobleem in Internet Explorer (IE) 11 wanneer ECID vooraf is goedgekeurd en later wordt bijgewerkt.

## donderdag 22 januari 2020

### Experience Cloud ID Extension 4.5.2

* Bijgewerkte bezoeker.js aan 4.5.2
* Bezoeker 4.5.1 bevat een foutopsporing voor IAB-insteekmodule voor Optin
* Bijgewerkte `setCustomerIDs` -methode om lege verzonden id&#39;s af te wijzen.

## woensdag 7 januari 2020

### Experience Cloud ID Extension 4.4.2

* Bijgewerkte bezoeker.js aan 4.4.2
* Verbeteringen voor de methode `getVisitorValues` om waarden sneller op te halen


## vrijdag 19 september 2019

### Experience Cloud ID Extension 4.4.1

* Bijgewerkte bezoeker.js aan 4.4.1
* Correctie van een fout voor invoer van Opt-In-voorkeuren
* De naam van VIDEO_ANALYTICS is gewijzigd in MEDIA_ANALYTICS in preOptInApproval als

  ![](../../../images/ecid-media-analytics.png)

## donderdag 17 juli 2019

### Experience Cloud ID Extension 4.4.0

* Bijgewerkte bezoeker.js aan 4.4.0
* Toegevoegde SHA256-hashingondersteuning voor setCustomerID&#39;s

  ![](../../../images/ecid-setCustomerIDs-hash.png)

## dinsdag 13 mei 2019

### Experience Cloud ID Extension 4.3.1

* Bijgewerkte bezoeker.js aan 4.3
* Type gegevenselement toegevoegd voor ECID als onderdeel van de tagextensie

  ![](../../../images/ecid-data-element.png)

## 9 april 2019

### Experience Cloud ID Extension 4.2.0

* Bijgewerkte bezoeker.js aan 4.2 die steun voor de Plug-in van Audience Manager IAB TCF omvatte

## dinsdag 25 februari 2019

### Experience Cloud ID Extension 4.1.0

* Bijgewerkte bezoeker.js aan 4.1 die publishDestures per nieuwe API verandering bijwerkte. Met deze update kan de referentie-informatie van de pagina desgewenst worden weergegeven tijdens de id - synchronisatie.

## zaterdag 15 februari 2019

### Experience Cloud ID Extension 4.0.0

* Bijgewerkte bezoeker.js aan 4.0
* Er zijn configuratieopties toegevoegd voor het nieuwe ingebouwde Opt-In-object. Opti-In-instellingen kunnen worden gebruikt om cookie- en baken-aanroepen van Adobe Solutions te onderdrukken om betere ondersteuningsregels zoals GDPR te ondersteunen

  ![](../../../images/ext-mcid-opt-in.png)

## woensdag 20 maart 2018

### Experience Cloud ID Extension 3.1.0

* Bijgewerkte bezoeker.js aan 3.1
* Voegt twee configuratie-eigenschappen toe: `resetBeforeVersion` en `serverState`
