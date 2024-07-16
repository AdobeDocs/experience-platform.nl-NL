---
title: Client-tips voor gebruikersagent
description: Leer hoe de wenken van de gebruikersagentencliënt in Web SDK werken. Met clienttips hebben eigenaars van websites toegang tot veel van dezelfde gegevens die beschikbaar zijn in de userAgent-tekenreeks, maar op een meer privacyvriendelijke manier.
keywords: user-agent;client hints; tekenreeks; user-agent tekenreeks; lage entropie; hoge entropie
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# Client-tips voor gebruikersagent

## Overzicht {#overview}

Telkens wanneer een webbrowser een aanvraag indient bij een webserver, bevat de header van de aanvraag informatie over de browser en de omgeving waarop de browser wordt uitgevoerd. Al deze gegevens worden samengevoegd in een koord, genoemd het koord van de gebruikersagent.

Hier is een voorbeeld van hoe een userAgent-tekenreeks eruitziet op een aanvraag die afkomstig is van een Chrome-browser die op een [!DNL Mac OS] -apparaat wordt uitgevoerd.

>[!NOTE]
>
>In de loop der jaren is de hoeveelheid browser- en apparaatinformatie die in de userAgent-tekenreeks is opgenomen, meerdere malen toegenomen en gewijzigd. In het onderstaande voorbeeld ziet u een selectie van de meest voorkomende gegevens van de gebruikersagent.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Veld | Waarde |
|---|---|
| Naam software | Chrome |
| Softwareversie | 105 |
| Volledige softwareversie | 105.0.0.0 |
| Naam van lay-outengine | AppleWebKit |
| Versie van lay-outengine | 537,36 |
| Besturingssysteem | MAC OS X |
| Versie besturingssysteem | 10 15,7 |
| Apparaat | Intel Mac OS X 10_15_7 |

## Gebruiksscenario’s {#use-cases}

De agenten van de gebruiker koorden zijn lang gebruikt om marketing en ontwikkelingsteams van belangrijke inzichten van te voorzien hoe browsers, werkende systemen en apparaten plaatsinhoud tonen, evenals hoe de gebruikers met websites in wisselwerking staan.

De agentenkoorden van de gebruiker worden ook gebruikt om spam en filterbots te blokkeren die plaatsen voor een verscheidenheid van extra doeleinden kruipen.

## Tekenreeksen voor gebruikersagent in Adobe Experience Cloud {#user-agent-in-adobe}

Adobe Experience Cloud-oplossingen gebruiken op verschillende manieren de strings van de gebruikersagent.

* Adobe Analytics gebruikt de userAgent-tekenreeks om aanvullende informatie over besturingssystemen, browsers en apparaten die worden gebruikt om een website te bezoeken, te vergroten en af te leiden.
* Adobe Audience Manager en Adobe Target kwalificeren eindgebruikers voor segmentatie- en personalisatiecampagnes, op basis van de informatie die wordt verstrekt door de userAgent-tekenreeks.

## Introductie van client-tips voor gebruikersagent {#ua-ch}

In de afgelopen jaren hebben eigenaars van sites en leveranciers van marketingservices gebruikgemaakt van tekenreeksen voor gebruikersagenten en andere informatie die is opgenomen in aanvraagheaders om digitale vingerafdrukken te maken. Deze vingerafdrukken kunnen worden gebruikt om gebruikers zonder hun medeweten te identificeren.

Ondanks het belangrijke doel dat gebruikersagentenkoorden voor plaatseigenaars dienen, hebben de browser ontwikkelaars besloten om te veranderen hoe de koorden van de gebruikersagent werken, om potentiële privacykwesties voor eind te beperken - gebruikers.

De oplossing zij ontwikkelden wordt genoemd [ de wenken van de gebruikersagent ](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Met behulp van clienttips kunnen websites nog steeds de benodigde informatie over de browser, het besturingssysteem en het apparaat verzamelen, terwijl ze tegelijkertijd een betere bescherming bieden tegen methoden voor geheime tracering, zoals vingerafdrukken.

Met clienttips hebben eigenaars van websites toegang tot veel van dezelfde gegevens die beschikbaar zijn in de userAgent-tekenreeks, maar op een meer privacyvriendelijke manier.

Wanneer moderne browsers een gebruiker naar een webserver sturen, wordt de volledige userAgent-tekenreeks op elke aanvraag verzonden, ongeacht of deze vereist is. De wenken van de cliënt, anderzijds, dwingen een model af waar de server browser om de extra informatie moet vragen het over de cliënt wil weten. Op het ontvangen van dit verzoek, kan browser zijn eigen beleid of gebruikersconfiguratie toepassen om te bepalen welke gegevens zijn teruggekeerd. In plaats van het blootstellen van het volledige userAgent koord door gebrek op alle verzoeken, wordt de toegang nu geleid op een expliciete en controleerbare manier.

## Browserondersteuning {#browser-support}

{de wenken van de de agentencliënt van de Gebruiker 1} werden geïntroduceerd met [!DNL Google Chrome] versie 89.[](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)

Aanvullende op chroom gebaseerde browsers ondersteunen de client Hints-API, zoals:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorieën {#categories}

Er zijn twee categorieën van de cliëntwenken van de gebruikersagent:

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

Hoog de wenken van de entropiecliënt worden onbruikbaar gemaakt door gebrek in Web SDK. Om hen toe te laten moet u SDK van het Web manueel vormen om hoge entropy cliëntwenken te verzoeken.

## Hoog entropclient-tips beïnvloeden de oplossingen van Experiencen Cloud {#impact-in-experience-cloud-solutions}

Sommige Adobe Experience Cloud-oplossingen vertrouwen bij het genereren van rapporten op informatie die is opgenomen in hoge entropietips.

Als u geen hoge entropieclientiptips inschakelt in uw omgeving, werken de Adobe Analytics- en Audience Manager-rapporten en -traits die hieronder worden beschreven niet.

### Adobe Analytics rapporteert op basis van hoge entropclient-hints {#analytics}

De [ dimensie van het Werkende systeem ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) omvat werkende systeemversie die als hoge entropiecliëntwenk wordt opgeslagen. Als de hoge wenken van entropiecliënten niet wordt toegelaten, kan de versie van het werkende systeem voor klappen die van browsers Chromium worden verzameld onnauwkeurig zijn.

### Audience Manager-eigenschappen die afhankelijk zijn van hoge entropieclientiptips {#aam}

[!DNL Google] heeft de browserfunctionaliteit van [!DNL Chrome] bijgewerkt om de informatie die via de header van `User-Agent` wordt verzameld, tot een minimum te beperken. Dientengevolge, zullen de klanten die van de Audience Manager [ DIL ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html) gebruiken geen betrouwbare die informatie voor eigenschappen meer ontvangen op [ platform-vlakke sleutels ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html) worden gebaseerd.

De klanten van de Audience Manager die platform-vlakke sleutels voor het richten gebruiken moeten op ](/help/web-sdk/home.md) in plaats van [ Experience Platform van SDK van het Web ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html) schakelen, en [ Hoge Hints van de Cliënt Entropy ](#enabling-high-entropy-client-hints) toelaten om betrouwbare gegevens van de eigenschap te blijven ontvangen.[

## Hoog entropclient-hints inschakelen {#enabling-high-entropy-client-hints}

Als u hoge entropy client hints wilt inschakelen voor uw Web SDK-implementatie, moet u de extra `highEntropyUserAgentHints` contextoptie opnemen in het veld [`context`](/help/web-sdk/commands/configure/context.md) .

Als u bijvoorbeeld hoge entropientroy-clienthints wilt ophalen van westeigenschappen, ziet uw configuratie er als volgt uit:

`context: ["highEntropyUserAgentHints", "web"]`

## Voorbeeld {#example}

De wenken van de cliënt in de kopballen van het eerste verzoek dat door browser aan een Webserver wordt gemaakt zullen het browser merk, de belangrijkste versie van browser, en een indicator bevatten van of de cliënt een mobiel apparaat is. Elk gegeven zal zijn eigen kopbalwaarde eerder dan in één enkele userAgent koord, zoals hieronder getoond hebben:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

De equivalente header [!DNL User-Agent] voor dezelfde browser ziet er als volgt uit:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Terwijl de informatie gelijkaardig is, bevat het eerste verzoek aan de server cliëntwenken. Deze omvatten slechts een ondergroep van wat in het koord van de gebruikersagent beschikbaar is. Het verzoek heeft geen betrekking op de architectuur van het besturingssysteem, de volledige versie van het besturingssysteem, de naam van de lay-outengine, de versie van de lay-outengine en de volledige browserversie.

Bij volgende aanvragen kunnen webservers echter om aanvullende informatie over het apparaat vragen. [!DNL Client Hints API] Wanneer deze waarden worden gevraagd, afhankelijk van browserbeleid of gebruikersinstellingen, kan de browserreactie die informatie bevatten.

Hieronder ziet u een voorbeeld van het JSON-object dat door de [!DNL Client Hints API] wordt geretourneerd wanneer hoge entropiewaarden worden aangevraagd:


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
