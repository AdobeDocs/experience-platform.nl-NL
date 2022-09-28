---
title: Client-tips voor gebruikersagent
description: Leer hoe de gebruikers-agent de Hints van de Cliënt in Web SDK werken
keywords: user-agent;client hints; tekenreeks; user-agent string; lage entropie; hoge entropie
source-git-commit: 6c974d1a646ff1f3a8f7ad9d67a6840391fc739e
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 2%

---


# Client-tips voor gebruikersagent

## Overzicht {#overview}

Telkens wanneer een webbrowser een aanvraag indient bij een webserver, bevat de header van de aanvraag informatie over de browser en de omgeving waarop de browser wordt uitgevoerd. Al deze gegevens worden geaggregeerd in een tekenreeks, de zogenaamde [!DNL User-Agent] tekenreeks.

Hier is een voorbeeld van wat een [!DNL User-Agent] een tekenreeks ziet eruit als op een aanvraag die afkomstig is van een Chrome-browser die op een [!DNL Mac OS] apparaat.

>[!NOTE]
>
>De hoeveelheid browser- en apparaatinformatie die in de [!DNL User-Agent] tekenreeks is meerdere keren gegroeid en gewijzigd. In het onderstaande voorbeeld ziet u een selectie van de meest gangbare [!DNL User-Agent] informatie.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Veld | Waarde |
|---|---|
| Naam software | Chroom |
| Softwareversie | 105 |
| Volledige softwareversie | 105.0.0.0 |
| Naam van lay-outengine | AppleWebKit |
| Versie van lay-outengine | 537,36 |
| Besturingssysteem | Mac OS X |
| Versie besturingssysteem | 10.15.7. |
| Apparaat | Intel Mac OS X 10_15_7 |

## Gebruiksscenario’s {#use-cases}

[!DNL User-Agent] tekenreeksen worden al lang gebruikt om marketing - en ontwikkelingsteams belangrijke inzichten te bieden in de manier waarop browsers , besturingssystemen en apparaten site-inhoud weergeven , en in de manier waarop gebruikers met websites communiceren .

[!DNL User-Agent] tekenreeksen worden ook gebruikt om spam- en filterbots te blokkeren die door sites kruipen voor verschillende extra doeleinden.

## [!DNL User-Agent] tekenreeksen in Adobe Experience Cloud {#user-agent-in-adobe}

Adobe Experience Cloud-oplossingen gebruiken de [!DNL User-Agent] tekenreeksen op verschillende manieren.

* Adobe Analytics gebruikt de [!DNL User-Agent] een tekenreeks om aanvullende informatie over besturingssystemen, browsers en apparaten die worden gebruikt om een website te bezoeken, te vergroten en af te leiden.
* Adobe Audience Manager en Adobe Target kwalificeren eindgebruikers voor segmentatie- en personalisatiecampagnes op basis van de informatie die door de [!DNL User-Agent] tekenreeks.

## Introductie van gebruiker-Agent de wenken van de Cliënt {#ua-ch}

In de afgelopen jaren hebben eigenaren van sites en marketingverkopers [!DNL User-Agent] tekenreeksen samen met andere informatie die is opgenomen in aanvraagheaders om digitale vingerafdrukken te maken. Deze vingerafdrukken kunnen worden gebruikt om gebruikers zonder hun medeweten te identificeren.

Ondanks het belangrijke doel dat [!DNL User-Agent] tekenreeksen dienen voor site-eigenaars, browserontwikkelaars hebben besloten hoe [!DNL User-Agent] -tekenreeksen worden gebruikt om potentiële privacyproblemen voor eindgebruikers te beperken.

De oplossing die zij hebben ontwikkeld, wordt [Client-tips voor gebruikersagent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Met behulp van clienttips kunnen websites nog steeds de benodigde informatie over de browser, het besturingssysteem en het apparaat verzamelen, terwijl ze tegelijkertijd een betere bescherming bieden tegen methoden voor geheime tracering, zoals vingerafdrukken.

Met clienttips hebben websiteeigenaars toegang tot veel van de informatie die in het dialoogvenster [!DNL User-Agent] -tekenreeks, maar op een meer privacyvriendelijke manier.

Wanneer moderne browsers een gebruiker naar een webserver sturen, wordt de volledige [!DNL User-Agent] tekenreeks wordt op elke aanvraag verzonden, ongeacht of deze vereist is. De wenken van de cliënt, anderzijds, dwingen een model af waar de server browser om de extra informatie moet vragen het over de cliënt wil weten. Op het ontvangen van dit verzoek, kan browser zijn eigen beleid of gebruikersconfiguratie toepassen om te bepalen welke gegevens zijn teruggekeerd. In plaats van de volledige [!DNL User-Agent] koord door gebrek op alle verzoeken, wordt de toegang nu geleid op een expliciete en controleerbare manier.

## Browserondersteuning {#browser-support}

[Client-tips voor gebruikersagent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) zijn ingevoerd met [!DNL Google Chrome ]versie 89.

Aanvullende op chroom gebaseerde browsers ondersteunen de client Hints-API, zoals:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorieën {#categories}

Er zijn twee categorieën gebruiker-Agent de Tips van de Cliënt:

* [Lage entropieclienthints](#low-entropy)
* [Hoog entropieclienthints](#high-entropy)

### Lage entropieclienthints {#low-entropy}

Lage entropieclienthints bevatten basisinformatie die niet kan worden gebruikt voor vingerafdrukgebruikers. Informatie zoals het merk van de browser, het platform en of de aanvraag afkomstig is van een mobiel apparaat.

De lage wenken van de entropycliënt worden toegelaten door gebrek in Web SDK, en worden overgegaan op elk verzoek.

| HTTP-header | JavaScript | Standaard opgenomen in gebruikersagent | Standaard opgenomen in clienttips |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Ja | Ja |
| `Sec-CH-UA-Platform` | `platform` | Ja | Ja |
| `Sec-CH-UA-Mobile` | `mobile` | Ja | Ja |

### Hoog entropieclienthints {#high-entropy}

Hoog entropy cliëntwenken zijn meer gedetailleerde informatie over het cliëntapparaat, zoals platformversie, architectuur, model, bitness (met 64 bits of met 32 bits platforms), of volledige werkend systeemversie. Deze informatie kan mogelijk worden gebruikt bij het nemen van vingerafdrukken.

| HTTP-header | JavaScript | Standaard opgenomen in gebruikersagent | Standaard opgenomen in clienttips |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Ja | Nee |
| `Sec-CH-UA-Arc` | `architecture` | Ja | Nee |
| `Sec-CH-UA-Model` | `model` | Ja | Nee |
| `Sec-CH-UA-Bitness` | `Bitness` | Ja | Nee |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Ja | Nee |

Hoog entropy cliëntwenken worden onbruikbaar gemaakt door gebrek in Web SDK. Om hen toe te laten moet u SDK van het Web manueel vormen om hoge entropy cliëntwenken te verzoeken.

## Hoog entropclient-tips beïnvloeden Experience Cloud-oplossingen {#impact-in-experience-cloud-solutions}

Sommige Adobe Experience Cloud-oplossingen vertrouwen bij het genereren van rapporten op informatie die is opgenomen in hoge entropietips.

Als u geen hoge entropieclientiptips inschakelt in uw omgeving, werken de Adobe Analytics- en Audience Manager-rapporten en -traits die hieronder worden beschreven niet.

### Adobe Analytics rapporteert op basis van hoge entropclient-hints {#analytics}

De volgende Adobe Analytics-rapporten werken niet als de hoge entropiecliptips zijn uitgeschakeld.

* [Browser](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser.html)
* [Browsertype](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)
* [Besturingssysteem](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html)
* [Typen besturingssystemen](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)
* [Mobiele afmetingen](https://experienceleague.adobe.com/docs/analytics/components/dimensions/mobile-dimensions.html)

### Audience Manager-eigenschappen die afhankelijk zijn van hoge entropieclientiptips {#aam}

Als de eigenschappen van uw Audience Manager een van de volgende eigenschappen gebruiken, moet u hoge entropiecliëntwenken toelaten. Anders werken de kenmerken niet meer.

* Versie besturingssysteem
* Apparaatmodel
* Apparaatfabrikant
* Apparaatleverancier

## Hoog entropclient-tips inschakelen {#enabling-high-entropy-client-hints}

Om hoge entropy cliëntwenken op uw plaatsing van SDK van het Web toe te laten, moet u extra omvatten `highEntropyUserAgentHints` contextoptie, zoals beschreven in [configuratiedocumentatie](configuring-the-sdk.md#context), naast uw bestaande configuratie.

Als u bijvoorbeeld hoge entropientroy-clienthints wilt ophalen van westeigenschappen, ziet uw configuratie er als volgt uit:

`context: ["highEntropyUserAgentHints", "web"]`

## Voorbeeld {#example}

De wenken van de cliënt in de kopballen van het eerste verzoek dat door browser aan een Webserver wordt gemaakt zullen het browser merk, de belangrijkste versie van browser, en een indicator bevatten van of de cliënt een mobiel apparaat is. Elk gegeven heeft zijn eigen koptekstwaarde in plaats van dat het in één stuk wordt gegroepeerd [!DNL User-Agent] tekenreeks, zoals hieronder wordt getoond:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Het equivalent [!DNL User-Agent] header voor dezelfde browser zou er als volgt uitzien:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Terwijl de informatie gelijkaardig is, bevat het eerste verzoek aan de server cliëntwenken. Deze omvatten slechts een ondergroep van wat in beschikbaar is in [!DNL User-Agent] tekenreeks. Het verzoek heeft geen betrekking op de architectuur van het besturingssysteem, de volledige versie van het besturingssysteem, de naam van de lay-outengine, de versie van de lay-outengine en de volledige browserversie.

Op latere verzoeken echter [!DNL Client Hints API] Hiermee kunnen webservers om aanvullende informatie over het apparaat vragen. Wanneer deze waarden worden gevraagd, afhankelijk van browserbeleid of gebruikersinstellingen, kan de browserreactie die informatie bevatten.

Hieronder ziet u een voorbeeld van het JSON-object dat wordt geretourneerd door de [!DNL Client Hints API] wanneer hoge entropiewaarden worden gevraagd:


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
