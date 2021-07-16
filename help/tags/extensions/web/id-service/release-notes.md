---
title: Opmerkingen bij de release Adobe Experience Cloud Identity Service Extension
description: De meest recente release bevat informatie over de extensie van de Adobe Experience Cloud Identity Service in Adobe Experience Platform.
source-git-commit: 1d3415146335d3011963c969d5b6aeea1f1a51d0
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 5%

---

# Opmerkingen bij de release Adobe Experience Cloud Identity Service

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Raadpleeg voor opmerkingen bij de release de Experience Cloud Identity Service zelf en niet alleen de Adobe Experience Platform-tagextensie: [https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html)

## 3 nov. 2020

### Experience Cloud ID Extension 5.2.1

#### **Functies**

* Deze patch bevat een correctie voor het schrijven van cookies van een iFrame met kenmerk `SameSite=None` in Google Chrome-browser.

## 12 jan. 2021

### Experience Cloud ID Extension 5.2.0

#### **Functies**

* Het bijwerken naar de VisitorJS 5.2.0-patch met een oplossing voor ECID DataElement kon niet worden bijgewerkt wanneer u toestemming kreeg.

## 27 okt. 2020

### Experience Cloud ID Extension 5.1.0

#### **Functies**

* `sameSiteCookie` config toevoegen om het `SameSite` attribuut van `AMCV` koekje te specificeren.
Deze config steunt de volgende waarden voor `SameSite` attributen:

   * `Strict`
   * `Lax`
   * `None`

Details van deze kenmerkwaarden vindt u op [web.dev](https://web.dev/samesite-cookies-explained/) en [chroom](https://www.chromium.org/updates/same-site)


## 13 augustus 2020

### Experience Cloud ID-extensie 5.0.1

#### **Functies**

* Bijwerken naar de VisitorJS 5.0.1-patch met een correctie voor het toevoegen van de d_cf-markering wanneer de IAB-toestemmingstekenreeks is gewijzigd.

## 15 juni 2020

### Experience Cloud ID-extensie 5.0.0

#### **Functies**

* Ondersteuning toevoegen voor `IAB TCF` - Transparency &amp; Consent Framework - `Version 2.0`.

## 13 april 2020

### Experience Cloud ID-extensie 4.6.0

#### **Functies**

* Markering `loadSSL` is standaard ingeschakeld. Alle oproepen aan de Dienst van de Identiteit zullen `https` door gebrek zijn. De klanten kunnen het aan vals plaatsen als zij de Diensten van de Identiteit op http van hun niet-ssl pagina&#39;s willen roepen.
* Bijgewerkt de functie die wordt gebruikt om Internet-Explorer (IE) versie te ontdekken, om een kwestie te bevestigen die door ESLint wordt gemeld.
* Opgeloste problemen voor een prestatieprobleem in Internet Explorer (IE) 11 wanneer ECID vooraf is goedgekeurd en later wordt bijgewerkt.

## 22 januari 2020

### Experience Cloud ID-extensie 4.5.2

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.5.2
* Bezoeker 4.5.1 bevat een foutopsporing voor IAB-insteekmodule voor Optin
* Bijgewerkte methode `setCustomerIDs` om het even welke lege verzonden IDs te verwerpen.

## 7 januari 2020

### Experience Cloud ID-extensie 4.4.2

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.4.2
* Verbeteringen voor de methode `getVisitorValues` om waarden sneller op te halen


## 19 september 2019

### Experience Cloud ID-extensie 4.4.1

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.4.1
* Correctie van een fout voor invoer van Opt-In-voorkeuren
* De naam van VIDEO_ANALYTICS is gewijzigd in MEDIA_ANALYTICS in preOptInApproval als

   ![](../../../images/ecid-media-analytics.png)

## 17 juli 2019

### Experience Cloud ID-extensie 4.4.0

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.4.0
* Toegevoegde SHA256-hashingondersteuning voor setCustomerID&#39;s

   ![](../../../images/ecid-setCustomerIDs-hash.png)

## 13 mei 2019

### Experience Cloud ID-extensie 4.3.1

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.3
* Type gegevenselement toegevoegd voor ECID als onderdeel van de tagextensie

   ![](../../../images/ecid-data-element.png)

## 9 april 2019

### Experience Cloud ID Extension 4.2.0

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.2 die steun voor Audience Manager IAB TCF Plug-in omvatte

## 25 februari 2019

### Experience Cloud ID-extensie 4.1.0

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.1 die publishDestures per nieuwe API verandering bijwerkte. Met deze update kan de referentie-informatie van de pagina desgewenst worden weergegeven tijdens de id - synchronisatie.

## 15 februari 2019

### Experience Cloud ID-extensie 4.0.0

#### **Functies**

* Bijgewerkte bezoeker.js aan 4.0
* Er zijn configuratieopties toegevoegd voor het nieuwe ingebouwde Opt-In-object. Opti-In montages kunnen worden gebruikt om koekje en bakenvraag van de Oplossingen van Adobe te onderdrukken om betere steunverordeningen zoals GDPR te steunen

   ![](../../../images/ext-mcid-opt-in.png)

## 20 maart 2018

### Experience Cloud ID Extension 3.1.0

#### **Functies**

* Bijgewerkte bezoeker.js aan 3.1
* Voegt twee configuratie-eigenschappen toe: `resetBeforeVersion` en `serverState`
