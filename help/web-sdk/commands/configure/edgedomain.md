---
title: edgeDomain
description: Bepaal het basisdomein waarnaar u gegevens wilt verzenden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---

# `edgeDomain`

De `edgeDomain` bezit staat u toe om het domein te veranderen waar het Web SDK gegevens verzendt. Deze eigenschap wordt vaak gebruikt door organisaties die [cookies van eerste partij](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html). Het gegeven wordt verzonden naar het eigen domein van de organisatie, dan een verslag CNAME door:sturen die gegevens aan Adobe.

Uw organisatie bepaalt de correcte waarde voor dit bezit wanneer vestiging [cookies van eerste partij](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html). Een organisatie gebruikt voor dit doel doorgaans een speciaal subdomein. Als u bijvoorbeeld het domein gebruikt `example.com`, kunt u cookies van eerste partijen instellen op `data.example.com`.

## Een Edge-domein configureren met de webSDK-tagextensie

Stel de **[!UICONTROL Edge domain]** tekstveld wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Het tekstveld zoeken **[!UICONTROL Edge domain]** Voer vervolgens de gewenste waarde in.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Een Edge-domein configureren met de Web SDK JavaScript-bibliotheek

Stel de `edgeDomain` tekenreeks bij het uitvoeren van de `configure` gebruiken. Als u deze eigenschap weglaat bij het configureren van de SDK, wordt standaard ingesteld op `edge.adobedc.net`. Plaats deze waarde als u het domein zou willen met voeten treden dat SDK van het Web gegevens naar verzendt.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
