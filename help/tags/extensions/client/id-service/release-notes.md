---
title: Opmerkingen bij de release Adobe Experience Cloud Identity Service Extension
description: De meest recente release bevat informatie over de extensie van de Adobe Experience Cloud Identity Service in Adobe Experience Platform.
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# Opmerkingen bij de release Adobe Experience Cloud Identity Service

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In dit document worden de opmerkingen bij de release voor de extensie van de Adobe Experience Cloud Identity Service besproken. Raadpleeg voor opmerkingen bij de release over de Experience Cloud Identity Service zelf de [Identiteitsdocumentatie](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html).

## 17 okt. 2022

### Experience Cloud ID-extensie 5.5.0

* De extensie ondersteunt nu versie 5.5.0 van de [Bezoeker JS Client](https://github.com/Adobe-Marketing-Cloud/id-service). Zie de [Opmerkingen bij de release van bezoekers](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0) voor specifieke updates.

## 9 mrt. 2022

### Experience Cloud ID Extension 5.4.0

* Deze versie bevat de nieuwste versie van Visitor 5.4.0, die de volgende updates bevat:

   * Mogelijkheid om de levensduur van de `s_ecid` cookie met cookieLifetime config
   * Update voor een browserprobleem van Firefox dat optreedt wanneer een pagina in een onderliggend iFrame wordt geladen

## 10 okt. 2021

### Experience Cloud ID-extensie 5.3.1

* Deze versie bevat de nieuwste versie van Visitor 5.3.0, die de volgende nieuwe updates heeft:

   * Bijgewerkt algoritme om lokale ECID te produceren
   * Meest recente opt-in met `Secure` en `SameSite` vlaggen voor het privacycookie
   * Probleem met een Firefox-browser verhelpen wanneer een pagina in een onderliggend iFrame wordt geladen

## 12 jan. 2021

### Experience Cloud ID Extension 5.2.0

* Het bijwerken naar de VisitorJS 5.2.0-patch met een oplossing voor ECID DataElement kon niet worden bijgewerkt wanneer u toestemming kreeg.

## 3 nov. 2020

### Experience Cloud ID Extension 5.2.1

* Deze patch bevat een correctie voor het schrijven van cookies van een iFrame met kenmerk `SameSite=None` in Google Chrome-browser.

## 27 okt. 2020

### Experience Cloud ID Extension 5.1.0

* Toevoegen `sameSiteCookie` config om te specificeren `SameSite` kenmerk van de `AMCV` cookie.
Deze config steunt de volgende waarden voor `SameSite` kenmerk:

   * `Strict`
   * `Lax`
   * `None`

Details van deze kenmerkwaarden zijn ingeschakeld [web.dev](https://web.dev/samesite-cookies-explained/) en [chroom](https://www.chromium.org/updates/same-site)


## 13 augustus 2020

### Experience Cloud ID-extensie 5.0.1

* Bijwerken naar de VisitorJS 5.0.1-patch met een correctie voor het toevoegen van de d_cf-markering wanneer de IAB-toestemmingstekenreeks is gewijzigd.

## 15 juni 2020

### Experience Cloud ID-extensie 5.0.0

* Ondersteuning toevoegen voor `IAB TCF` - Transparantie en instemming - `Version 2.0`.

## 13 april 2020

### Experience Cloud ID-extensie 4.6.0

* Made `loadSSL` markering is standaard ingeschakeld. Alle vraag aan de Dienst van de Identiteit zal zijn `https` standaard. De klanten kunnen het aan vals plaatsen als zij de Diensten van de Identiteit op http van hun niet-ssl pagina&#39;s willen roepen.
* Bijgewerkt de functie die wordt gebruikt om Internet-Explorer (IE) versie te ontdekken, om een kwestie te bevestigen die door ESLint wordt gemeld.
* Opgeloste problemen voor een prestatieprobleem in Internet Explorer (IE) 11 wanneer ECID vooraf is goedgekeurd en later wordt bijgewerkt.

## 22 januari 2020

### Experience Cloud ID-extensie 4.5.2

* Bijgewerkte bezoeker.js aan 4.5.2
* Bezoeker 4.5.1 bevat een foutopsporing voor IAB-insteekmodule voor Optin
* Bijgewerkt `setCustomerIDs` methode om lege verzonden id&#39;s af te wijzen.

## 7 januari 2020

### Experience Cloud ID-extensie 4.4.2

* Bijgewerkte bezoeker.js aan 4.4.2
* Verbeteringen voor `getVisitorValues` methode om waarden sneller op te halen


## 19 september 2019

### Experience Cloud ID-extensie 4.4.1

* Bijgewerkte bezoeker.js aan 4.4.1
* Correctie van een fout voor invoer van Opt-In-voorkeuren
* De naam van VIDEO_ANALYTICS is gewijzigd in MEDIA_ANALYTICS in preOptInApproval als

   ![](../../../images/ecid-media-analytics.png)

## 17 juli 2019

### Experience Cloud ID-extensie 4.4.0

* Bijgewerkte bezoeker.js aan 4.4.0
* Toegevoegde SHA256-hashingondersteuning voor setCustomerID&#39;s

   ![](../../../images/ecid-setCustomerIDs-hash.png)

## 13 mei 2019

### Experience Cloud ID-extensie 4.3.1

* Bijgewerkte bezoeker.js aan 4.3
* Type gegevenselement toegevoegd voor ECID als onderdeel van de tagextensie

   ![](../../../images/ecid-data-element.png)

## 9 april 2019

### Experience Cloud ID Extension 4.2.0

* Bijgewerkte bezoeker.js aan 4.2 die steun voor Audience Manager IAB TCF Plug-in omvatte

## 25 februari 2019

### Experience Cloud ID-extensie 4.1.0

* Bijgewerkte bezoeker.js aan 4.1 die publishDestures per nieuwe API verandering bijwerkte. Met deze update kan de referentie-informatie van de pagina desgewenst worden weergegeven tijdens de id - synchronisatie.

## 15 februari 2019

### Experience Cloud ID-extensie 4.0.0

* Bijgewerkte bezoeker.js aan 4.0
* Er zijn configuratieopties toegevoegd voor het nieuwe ingebouwde Opt-In-object. Opti-In montages kunnen worden gebruikt om koekje en bakenvraag van de Oplossingen van Adobe te onderdrukken om betere steunverordeningen zoals GDPR te steunen

   ![](../../../images/ext-mcid-opt-in.png)

## 20 maart 2018

### Experience Cloud ID Extension 3.1.0

* Bijgewerkte bezoeker.js aan 3.1
* Voegt twee configuratie-eigenschappen toe: `resetBeforeVersion` en `serverState`
