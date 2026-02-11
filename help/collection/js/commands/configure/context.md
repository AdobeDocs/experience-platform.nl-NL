---
title: context
description: Automatisch apparaat-, omgeving- of locatiegegevens verzamelen.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# `context`

De eigenschap `context` is een array van tekenreeksen die bepaalt wat de Web SDK automatisch kan verzamelen. Hoewel deze gegevens een grote waarde kunnen hebben, kan het nuttig zijn om sommige van deze gegevens weg te laten, zodat u zich kunt houden aan het privacybeleid van uw organisatie.

## Contexttrefwoorden en XDM-elementen

Als u een bepaald contextsleutelwoord omvat, bevolkt het Web SDK automatisch al zijn bijbehorende elementen XDM. Als u een specifiek XDM-element wilt weglaten terwijl u andere elementen toestaat, kunt u waarden wissen met [`onBeforeEventSend`](onbeforeeventsend.md) . Als u meerdere gebeurtenissen op een pagina verzendt, bevat de Web SDK deze velden voor elke `SendEvent` -aanroep.

### Web

Het trefwoord `"web"` verzamelt informatie over de huidige pagina.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Pagina-URL | De URL van de huidige pagina. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referrer-URL | De URL van de vorige bezochte pagina. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

### Apparaat

Het trefwoord `"device"` verzamelt informatie over het apparaat van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Schermhoogte | De hoogte van het scherm in pixels. | `xdm.device.screenHeight` | `900` |
| Schermbreedte | De breedte van het scherm in pixels. | `xdm.device.screenWidth` | `1440` |
| Schermoriëntatie | De oriëntatie van het scherm. | `xdm.device.screenOrientation` | `landscape` of `portrait` |

### Omgeving

Het trefwoord `"environment"` verzamelt informatie over de browser van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Type omgeving | Het type omgeving waardoor de ervaring optrad. Dit veld wordt altijd ingesteld door de Web SDK op `browser` . | `xdm.environment.type` | `browser` |
| Viewporthoogte | De hoogte van het inhoudsgebied van de browser in pixels. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Viewportbreedte | De breedte van het inhoudsgebied van de browser in pixels. | `xdm.environment.browserDetails.viewportWidth` | `642` |

### Context plaatsen

Het trefwoord `"placeContext"` verzamelt informatie over de locatie van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Lokale tijd | Lokale timestamp voor het eind - gebruiker in het vereenvoudigde uitgebreide [&#x200B; formaat van ISO 8601 &#x200B;](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Verschuiving lokale tijdzone | Het aantal minuten dat de gebruiker wordt verschoven ten opzichte van GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Landcode | De landcode van de eindgebruiker. | `xdm.placeContext.geo.countryCode` | `US` |
| Provincie | De provinciecode van de eindgebruiker. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Breedte | De breedte van de locatie van de eindgebruiker. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Lengtegraad | De lengtegraad van de eindgebruikerlocatie. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

### Tijdstempel

Het trefwoord `"timestamp"` verzamelt informatie over de tijdstempel van de gebeurtenis. Deze context is altijd inbegrepen en kan niet worden verwijderd.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Tijdstempel van de gebeurtenis | UTC timestamp voor het eind - gebruiker in het vereenvoudigde uitgebreide [&#x200B; formaat van ISO 8601 &#x200B;](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |

### Implementatiedetails

Het trefwoord `implementationDetails` verzamelt informatie over de SDK-versie die wordt gebruikt om de gebeurtenis te verzamelen.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Naam | De id van de Software Development Kit (SDK). In dit veld wordt een URI gebruikt om de unieke id&#39;s van verschillende softwarebibliotheken te verbeteren. | `xdm.implementationDetails.name` | Wanneer de zelfstandige bibliotheek wordt gebruikt, is de waarde `https://ns.adobe.com/experience/alloy`. Wanneer de bibliotheek wordt gebruikt als onderdeel van de tagextensie, is de waarde `https://ns.adobe.com/experience/alloy+reactor` . |
| Versie | De versie van de Software Development Kit (SDK). | `xdm.implementationDetails.version` | Wanneer de zelfstandige bibliotheek wordt gebruikt, is de waarde de bibliotheekversie. Wanneer de bibliotheek wordt gebruikt als onderdeel van de tagextensie, is de waarde de bibliotheekversie en wordt de versie van de tagextensie gekoppeld aan een `+` . Als de bibliotheekversie bijvoorbeeld `2.1.0` is en de versie van de tagextensie `2.1.3` is, is de waarde `2.1.0+2.1.3` . |
| Omgeving | De omgeving waarin de gegevens zijn verzameld. Dit veld wordt altijd ingesteld op `browser` wanneer de JavaScript-bibliotheek wordt gebruikt. | `xdm.implementationDetails.environment` | `browser` |

### Hoog entropieclienthints {#high-entropy-client-hints}

Het trefwoord `"highEntropyUserAgentHints"` verzamelt gedetailleerde informatie over het apparaat van de gebruiker. Deze gegevens worden opgenomen in de HTTP-header van het verzoek dat naar Adobe wordt verzonden. Nadat de gegevens naar het Edge-netwerk zijn gearriveerd, vult het XDM-object het desbetreffende XDM-pad. Als u het respectieve pad XDM in uw `sendEvent` vraag plaatst, neemt het belangrijkheid over de kopbalwaarde van HTTP.

Als u apparatenraadplegingen gebruikt wanneer [&#x200B; vormend uw datastream &#x200B;](/help/datastreams/configure.md), kunnen de gegevens worden ontruimd ten gunste van de waarden van de apparatenraadpleging. Bepaalde velden voor client-hint en opzoekvelden van apparaten kunnen niet bestaan in dezelfde hit.

| Eigenschap | Beschrijving | HTTP-header | XDM-pad | Voorbeeld |
| --- | --- | --- | --- | --- |
| Versie besturingssysteem | De versie van het besturingssysteem. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Architectuur | De onderliggende CPU-architectuur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Apparaatmodel | De naam van het gebruikte apparaat. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Bitsheid | Het aantal bits dat de onderliggende CPU-architectuur ondersteunt. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Browserleverancier | Het bedrijf dat de browser heeft gemaakt. Dit element wordt ook verzameld door de lage entropiehint `Sec-CH-UA` . | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Browsernaam | De gebruikte browser. Dit element wordt ook verzameld door de lage entropiehint `Sec-CH-UA` . | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Browserversie | De significante versie van de browser. Dit element wordt ook verzameld door de lage entropiehint `Sec-CH-UA` . Exacte browserversie wordt niet automatisch verzameld. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

Zie [&#x200B; de wenken van de de agentencliënt van de Gebruiker &#x200B;](/help/collection/use-cases/client-hints.md) voor meer informatie.

### One-time Analytics-referentie {#one-time-analytics-referrer}

Het trefwoord `"oneTimeAnalyticsReferrer"` verzendt alleen een verwijzingswaarde naar Adobe Analytics bij de eerste aanroep van `sendEvent` zonder beslissing naar een pagina. Het primaire gebruiksgeval voor dit contextsleutelwoord moet de [&#x200B; dimensie van de Verwijzer &#x200B;](https://experienceleague.adobe.com/nl/docs/analytics/components/dimensions/referrer) in Adobe Analytics verhinderen door klappen worden opgeblazen die hoofdzakelijk in Analytics en de integratie van het Doel worden gebruikt.

Als een bepaalde opdracht `sendEvent` een gebeurtenistype voor beslissingen gebruikt ( `decisioning.propositionFetch` , `decisioning.propositionDisplay` , `decisioning.propositionInteract` ), wordt dit genegeerd bij het berekenen van de eerste `sendEvent` op een pagina. Als de verwijzende waarde op de pagina verandert en een andere `sendEvent` wordt teweeggebracht, wordt de nieuwe verwijzende waarde omvat in de lading. Met deze voorwaarde kan de functie worden gebruikt in toepassingen van één pagina.

Wanneer een dubbele verwijzingswaarde wordt ontdekt, plaatst de bibliotheek `data.__adobe.analytics.referrer` aan een leeg koord (`""`).
Als u dit gegevensobjectveld instelt op een lege tekenreeks, wordt de waarde gewist wanneer een treffer naar Adobe Analytics aankomt, aangezien het gegevensobject een equivalent veld voor XDM-objecten overschrijft. Het heeft geen invloed op het XDM-object, zodat die gegevens naar een Experience Platform-gegevensset kunnen worden verzonden als u meerdere services in een gegevensstroom opneemt.

## Implementatie

Stel de array `context` van tekenreeksen in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de SDK, worden standaard alle contextgegevens verzameld, behalve `"highEntropyUserAgentHints"` en `"oneTimeAnalyticsReferrer"` . Stel deze eigenschap in als u hoge entropieclientiptips wilt verzamelen of als u andere contextgegevens uit gegevensverzameling wilt weglaten. Tekenreeksen kunnen in elke willekeurige volgorde worden opgenomen.

>[!TIP]
>
>Als u alle contextinformatie wilt verzamelen, inclusief hoge entropieclienthints, moet u elke waarde in de array-tekenreeks `context` opnemen. De standaardwaarde van `context` is `"highEntropyUserAgentHints"` en `"oneTimeAnalyticsReferrer"` weggelaten. Wanneer u de eigenschap `context` instelt, worden bij weggelaten waarden geen gegevens verzameld.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints", "oneTimeAnalyticsReferrer"]
});
```

## Verzamel contextinformatie met de Web SDK-tagextensie

Zie [&#x200B; montages van de Context &#x200B;](/help/tags/extensions/client/web-sdk/configure/data-collection.md#context-settings) onder de configuratiemontages van de gegevensinzameling in de de markeringsuitbreidingsdocumentatie van SDK van het Web.
