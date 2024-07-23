---
title: edgeDomain
description: Bepaal het basisdomein waarnaar u gegevens wilt verzenden.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---

# `edgeDomain`

Met de eigenschap `edgeDomain` kunt u het domein wijzigen waar de Web SDK gegevens verzendt. Dit bezit wordt vaak gebruikt door organisaties die [ eerste partijkoekjes ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html) gebruiken. Het gegeven wordt verzonden naar het eigen domein van de organisatie, dan een verslag CNAME door:sturen die gegevens aan Adobe.

Uw organisatie bepaalt de correcte waarde voor dit bezit wanneer vestiging [ eerste partijkoekjes ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html). Een organisatie gebruikt voor dit doel doorgaans een speciaal subdomein. Als u bijvoorbeeld het domein `example.com` gebruikt, kunt u cookies van eerste partijen instellen op `data.example.com` .

## Een Edge-domein configureren met de webSDK-tagextensie

Plaats het **[!UICONTROL Edge domain]** tekstgebied wanneer [ vormend de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Zoek het tekstveld **[!UICONTROL Edge domain]** en voer vervolgens de gewenste waarde in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Een Edge-domein configureren met de Web SDK JavaScript-bibliotheek

Stel de tekenreeks `edgeDomain` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de SDK, wordt standaard `edge.adobedc.net` gebruikt. Plaats deze waarde als u het domein zou willen met voeten treden dat SDK van het Web gegevens naar verzendt.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```
