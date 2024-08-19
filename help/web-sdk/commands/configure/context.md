---
title: context
description: Automatisch apparaat-, omgeving- of locatiegegevens verzamelen.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 1%

---

# `context`

De eigenschap `context` is een array van tekenreeksen die bepaalt wat de Web SDK automatisch kan verzamelen. Hoewel deze gegevens een grote waarde kunnen hebben, kan het nuttig zijn om sommige van deze gegevens weg te laten, zodat u zich kunt houden aan het privacybeleid van uw organisatie.

## Contexttrefwoorden en XDM-elementen

Als u een bepaald contextsleutelwoord omvat, bevolkt SDK van het Web automatisch al zijn bijbehorende elementen XDM. Als u een specifiek XDM-element wilt weglaten terwijl u andere elementen toestaat, kunt u waarden wissen met [`onBeforeEventSend`](onbeforeeventsend.md) . Als u veelvoudige gebeurtenissen op een pagina verzendt, omvat SDK van het Web deze gebieden op elke `SendEvent` vraag.

### Web

Het trefwoord `"web"` verzamelt informatie over de huidige pagina.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Pagina-URL | De URL van de huidige pagina. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referrer-URL | De URL van de vorige bezochte pagina. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Apparaat

Het trefwoord `"device"` verzamelt informatie over het apparaat van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Schermhoogte | De hoogte van het scherm in pixels. | `xdm.device.screenHeight` | `900` |
| Schermbreedte | De breedte van het scherm in pixels. | `xdm.device.screenWidth` | `1440` |
| Schermoriëntatie | De oriëntatie van het scherm. | `xdm.device.screenOrientation` | `landscape` of `portrait` |

{style="table-layout:auto"}

### Omgeving

Het trefwoord `"environment"` verzamelt informatie over de browser van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Type omgeving | Het type omgeving waardoor de ervaring optrad. De Web SDK plaatst altijd dit gebied aan `browser`. | `xdm.environment.type` | `browser` |
| Viewporthoogte | De hoogte van het inhoudsgebied van de browser in pixels. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Viewportbreedte | De breedte van het inhoudsgebied van de browser in pixels. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Context plaatsen

Het trefwoord `"placeContext"` verzamelt informatie over de locatie van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Lokale tijd | Lokale timestamp voor het eind - gebruiker in het vereenvoudigde uitgebreide [ formaat van ISO 8601 ](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Verschuiving lokale tijdzone | Het aantal minuten dat de gebruiker wordt verschoven ten opzichte van GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Landcode | De landcode van de eindgebruiker. | `xdm.placeContext.geo.countryCode` | `US` |
| Provincie | De provinciecode van de eindgebruiker. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Breedte | De breedte van de locatie van de eindgebruiker. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Lengtegraad | De lengtegraad van de eindgebruikerlocatie. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### Tijdstempel

Het trefwoord `timestamp` verzamelt informatie over de tijdstempel van de gebeurtenis. Dit gedeelte van context kan niet worden verwijderd.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Tijdstempel van de gebeurtenis | UTC timestamp voor het eind - gebruiker in het vereenvoudigde uitgebreide [ formaat van ISO 8601 ](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### Implementatiedetails

Het trefwoord `implementationDetails` verzamelt informatie over de SDK-versie die wordt gebruikt om de gebeurtenis te verzamelen.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Naam | De id van de Software Development Kit (SDK). In dit veld wordt een URI gebruikt om de unieke id&#39;s van verschillende softwarebibliotheken te verbeteren. | `xdm.implementationDetails.name` | Wanneer de zelfstandige bibliotheek wordt gebruikt, is de waarde `https://ns.adobe.com/experience/alloy`. Wanneer de bibliotheek wordt gebruikt als onderdeel van de tagextensie, is de waarde `https://ns.adobe.com/experience/alloy+reactor` . |
| Versie | De versie van de Software Development Kit (SDK). | `xdm.implementationDetails.version` | Wanneer de zelfstandige bibliotheek wordt gebruikt, is de waarde de bibliotheekversie. Wanneer de bibliotheek wordt gebruikt als onderdeel van de tagextensie, is de waarde de bibliotheekversie en wordt de versie van de tagextensie gekoppeld aan een `+` . Als de bibliotheekversie bijvoorbeeld `2.1.0` is en de versie van de tagextensie `2.1.3` is, is de waarde `2.1.0+2.1.3` . |
| Omgeving | De omgeving waarin de gegevens zijn verzameld. Deze wordt altijd ingesteld op `browser` . | `xdm.implementationDetails.environment` | `browser` |


### Hoog entropieclienthints {#high-entropy-client-hints}

>[!TIP]
>
>Zie de documentatie over [ de wenken van de gebruikersagent ](../../use-cases/client-hints.md) voor gedetailleerde informatie over hoe te om hen te vormen.

Het trefwoord `"highEntropyUserAgentHints"` verzamelt gedetailleerde informatie over het apparaat van de gebruiker. Deze gegevens worden opgenomen in de HTTP-header van het verzoek dat naar de Adobe wordt verzonden. Nadat de gegevens binnen het netwerk van Edge zijn aangekomen, bevolkt het voorwerp XDM zijn respectieve weg XDM. Als u het respectieve pad XDM in uw `sendEvent` vraag plaatst, neemt het belangrijkheid over de kopbalwaarde van HTTP.

Als u apparatenraadplegingen gebruikt wanneer [ vormend uw datastream ](/help/datastreams/configure.md), kunnen de gegevens worden ontruimd ten gunste van de waarden van de apparatenraadpleging. Bepaalde velden voor client-hint en opzoekvelden van apparaten kunnen niet bestaan in dezelfde hit.

| Eigenschap | Beschrijving | HTTP-header | XDM-pad | Voorbeeld |
| --- | --- | --- | --- | --- |
| Versie besturingssysteem | De versie van het besturingssysteem. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Architectuur | De onderliggende CPU-architectuur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Apparaatmodel | De naam van het gebruikte apparaat. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Bitsheid | Het aantal beetjes dat de onderliggende architectuur van cpu steunt. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Browserleverancier | Het bedrijf dat de browser heeft gemaakt. Dit element wordt ook verzameld door de lage entropiehint `Sec-CH-UA` . | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Browsernaam | De gebruikte browser. Dit element wordt ook verzameld door de lage entropiehint `Sec-CH-UA` . | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Browserversie | De significante versie van de browser. Dit element wordt ook verzameld door de lage entropiehint `Sec-CH-UA` . Exacte browserversie wordt niet automatisch verzameld. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

{style="table-layout:auto"}

## Verzamel contextinformatie gebruikend de de markeringsuitbreiding van SDK van het Web

Het plaatsen van contextinformatie is een combinatie radioknopen en controledozen wanneer [ het vormen van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Elk selectievakje verwijst naar een contexttrefwoord.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Blader omlaag naar de sectie [!UICONTROL Data Collection] en selecteer vervolgens **[!UICONTROL All default context information]** of **[!UICONTROL Specific context information]** .
1. Als u **[!UICONTROL Specific context information]** selecteert, schakelt u het selectievakje in naast elk gewenst element met contextgegevens.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Verzamel contextinformatie gebruikend de bibliotheek van SDK van het Web JavaScript

Stel de array `context` van tekenreeksen in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de SDK, worden standaard alle contextgegevens behalve `"highEntropyUserAgentHints"` verzameld. Stel deze eigenschap in als u hoge entropieclientiptips wilt verzamelen of als u andere contextgegevens uit gegevensverzameling wilt weglaten. Tekenreeksen kunnen in elke willekeurige volgorde worden opgenomen.

>[!NOTE]
>
>Als u alle contextinformatie wilt verzamelen, inclusief hoge entropieclienthints, moet u elke waarde in de array-tekenreeks `context` opnemen. Bij de standaardwaarde van `context` wordt `highEntropyUserAgentHints` weggelaten en bij de instelling van de eigenschap `context` worden geen gegevens verzameld door weggelaten waarden.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
