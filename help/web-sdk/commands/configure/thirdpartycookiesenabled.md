---
title: thirdPartyCookiesEnabled
description: Het gebruik van cookies van derden toestaan om bezoekers te identificeren.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [heeft aangekondigd](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) is van plan de Chrome-ondersteuning voor cookies van derden in de tweede helft van 2024 te beëindigen. Daarom worden cookies van derden niet meer ondersteund in de belangrijkste browsers.
>
>Wanneer deze wijziging wordt doorgevoerd, zal de Adobe de steun voor de `demdex` cookie die momenteel wordt ondersteund in de Web SDK.


De `thirdPartyCookiesEnabled` eigenschap is een Booleaanse waarde die bepaalt of de Web SDK cookies instelt in een context van derden. Het inschakelen van deze optie is handig als u bezoekers wilt identificeren tussen subdomeinen of domeinen die eigendom zijn van uw organisatie. Veel moderne browsers beperken echter de instelling en vervaldatum van cookies van derden.

Als deze optie is ingeschakeld, gebruikt de Web SDK Adobe Audience Manager om een bezoeker te identificeren. Wanneer deze optie is uitgeschakeld, wordt de aanroep naar de Audience Manager uitgeschakeld. Zie [Het begrip vraag aan het domein van de Index](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html) in de gebruikershandleiding van de Audience Manager voor meer informatie.

## Cookies van andere bedrijven inschakelen met de webSDK-tagextensie

Selecteer de **[!UICONTROL Use third-party cookies]** selectievakje wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Identity] en selecteert u vervolgens het selectievakje **[!UICONTROL Use third-party cookies]**.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Cookies van derden inschakelen met de Web SDK JavaScript-bibliotheek

Stel de `thirdPartyCookiesEnabled` boolean wanneer de `configure` gebruiken. Als u dit bezit weglaat wanneer het vormen van het Web SDK, blijft het in gebreke aan `true`. Deze waarde instellen op `false` als u niet de SDK van het Web Audience Manager wilt gebruiken helpen bezoekers identificeren.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
