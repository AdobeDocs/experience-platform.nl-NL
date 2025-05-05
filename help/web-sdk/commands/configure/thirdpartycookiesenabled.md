---
title: thirdPartyCookiesEnabled
description: Het gebruik van cookies van derden toestaan om bezoekers te identificeren.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

De eigenschap `thirdPartyCookiesEnabled` is een Booleaanse waarde die bepaalt of de Web SDK cookies instelt in een context van derden. Het inschakelen van deze optie is handig als u bezoekers wilt identificeren tussen subdomeinen of domeinen die eigendom zijn van uw organisatie. Veel moderne browsers beperken echter de instelling en vervaldatum van cookies van derden.

De eigenschap `thirdPartyCookiesEnabled` bepaalt ook of een [`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk) kan worden opgevraagd voor [`getIdentity`](../getidentity.md) -aanroepen.

Als deze optie is ingeschakeld, gebruikt de Web SDK Adobe Audience Manager om een bezoeker te identificeren. Wanneer deze optie is uitgeschakeld, wordt de aanroep naar de Audience Manager uitgeschakeld. Zie [ Begrip vraag aan het domein van de Index ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=nl-NL) in de gebruikersgids van de Audience Manager voor meer informatie.

## Cookies van andere bedrijven inschakelen met de webSDK-tagextensie

Selecteer **[!UICONTROL Use third-party cookies]** checkbox wanneer [ het vormen van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie [!UICONTROL Identity] en schakel vervolgens het selectievakje **[!UICONTROL Use third-party cookies]** in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Cookies van derden inschakelen met de Web SDK JavaScript-bibliotheek

Stel de Booleaanse waarde `thirdPartyCookiesEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze waarde in op `false` als u niet wilt dat de Web SDK Audience Manager gebruikt om bezoekers te identificeren.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```
