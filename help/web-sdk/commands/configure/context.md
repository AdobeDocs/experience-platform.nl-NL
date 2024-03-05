---
title: context
description: Automatisch apparaat-, omgeving- of locatiegegevens verzamelen.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# `context`

De `context` eigenschap is een array van tekenreeksen die bepaalt wat de SDK van het Web automatisch kan verzamelen. Hoewel deze gegevens een grote waarde kunnen hebben, kan het nuttig zijn om sommige van deze gegevens weg te laten, zodat u zich kunt houden aan het privacybeleid van uw organisatie.

## Contexttrefwoorden en XDM-elementen

Als u een bepaald contextsleutelwoord omvat, bevolkt SDK van het Web automatisch al zijn bijbehorende elementen XDM. Als u een specifiek XDM-element wilt weglaten terwijl u andere elementen toestaat, kunt u waarden uit het gebruik wissen [`onBeforeEventSend`](onbeforeeventsend.md). Als u veelvoudige gebeurtenissen op een pagina verzendt, omvat SDK van het Web deze gebieden op elke `SendEvent` vraag.

### Web

De `"web"` trefwoord verzamelt informatie over de huidige pagina.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Pagina-URL | De URL van de huidige pagina. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referrer-URL | De URL van de vorige bezochte pagina. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Apparaat

De `"device"` het sleutelwoord verzamelt informatie over het apparaat van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Schermhoogte | De hoogte van het scherm in pixels. | `xdm.device.screenHeight` | `900` |
| Schermbreedte | De breedte van het scherm in pixels. | `xdm.device.screenWidth` | `1440` |
| Schermoriëntatie | De oriëntatie van het scherm. | `xdm.device.screenOrientation` | `landscape` of `portrait` |

{style="table-layout:auto"}

### Omgeving

De `"environment"` het sleutelwoord verzamelt informatie over browser van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Type omgeving | Het type omgeving waardoor de ervaring optrad. De Web SDK plaatst altijd dit gebied aan `browser`. | `xdm.environment.type` | `browser` |
| Viewporthoogte | De hoogte van het inhoudsgebied van de browser in pixels. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Viewportbreedte | De breedte van het inhoudsgebied van de browser in pixels. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Context plaatsen

De `"placeContext"` het sleutelwoord verzamelt informatie over de plaats van de gebruiker.

| Dimension | Beschrijving | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- |
| Lokale tijd | Lokale tijdstempel voor de eindgebruiker in vereenvoudigde uitgebreide versie [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) gebruiken. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Verschuiving lokale tijdzone | Het aantal minuten dat de gebruiker wordt verschoven ten opzichte van GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### Hoog entropieclienthints

De `"highEntropyUserAgentHints"` het sleutelwoord verzamelt gedetailleerde informatie over het apparaat van de gebruiker. Deze gegevens worden opgenomen in de HTTP-header van het verzoek dat naar de Adobe wordt verzonden. Nadat de gegevens binnen het netwerk van de Rand zijn aangekomen, bevolkt het voorwerp XDM zijn respectieve weg XDM. Als u het respectievelijke XDM-pad instelt in uw `sendEvent` aanroepen heeft deze voorrang op de HTTP-headerwaarde.

Als u apparaatlookups gebruikt wanneer [configureren, gegevensstroom](/help/datastreams/configure.md)gegevens kunnen worden gewist ten gunste van de opzoekwaarden van het apparaat. Bepaalde velden voor client-hint en opzoekvelden van apparaten kunnen niet bestaan in dezelfde hit.

| Dimension | Beschrijving | HTTP-header | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- | --- |
| Versie besturingssysteem | De versie van het besturingssysteem. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Architectuur | De onderliggende CPU-architectuur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Apparaatmodel | De naam van het gebruikte apparaat. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| Bitsheid | Het aantal beetjes dat de onderliggende architectuur van cpu steunt. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Browserleverancier | Het bedrijf dat de browser heeft gemaakt. De lage entropiehint `Sec-CH-UA` verzamelt dit element ook. | `Sec-CH-UA-Full-Version-List` | | |
| Browsernaam | De gebruikte browser. De lage entropiehint `Sec-CH-UA` verzamelt dit element ook. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Browserversie | De significante versie van de browser. De lage entropiehint `Sec-CH-UA` verzamelt dit element ook. Exacte browserversie wordt niet automatisch verzameld. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Verzamel contextinformatie gebruikend de de markeringsuitbreiding van SDK van het Web

De instelling voor contextinformatie is een combinatie van keuzerondjes en selectievakjes wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Elk selectievakje verwijst naar een contexttrefwoord.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens een van de **[!UICONTROL All default context information]** of **[!UICONTROL Specific context information]**.
1. Als u **[!UICONTROL Specific context information]** schakelt u het selectievakje in naast elk gewenst element met contextgegevens.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Informatie over context verzamelen met de Web SDK JavaScript-bibliotheek

Stel de `context` array van tekenreeksen wanneer de `configure` gebruiken. Als u deze eigenschap weglaat tijdens het configureren van de SDK, wordt alle contextinformatie weergegeven, behalve `"highEntropyUserAgentHints"` wordt standaard verzameld. Stel deze eigenschap in als u hoge entropieclientiptips wilt verzamelen of als u andere contextgegevens uit gegevensverzameling wilt weglaten. Tekenreeksen kunnen in elke willekeurige volgorde worden opgenomen.

>[!NOTE]
>
>Als u alle contextinformatie wilt verzamelen, inclusief hoge entropieclienthints, moet u elke waarde in de `context` array string. De standaardwaarde `context` waarde weglaten `highEntropyUserAgentHints`en als u de `context` eigenschap, worden geen gegevens verzameld door weggelaten waarden.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
