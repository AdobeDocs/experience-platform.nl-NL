---
title: downloadLinkQualifier
description: Hiermee kunt u bepalen hoe automatische koppelingen bijhouden downloadkoppelingen kwalificeert.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# `downloadLinkQualifier`

Als u automatische koppeling bijhouden inschakelt met [`clickCollectionEnabled`](clickcollectionenabled.md) , kunt u aan de hand van de eigenschap `downloadLinkQualifier` bepalen aan welke criteria een URL als downloadkoppeling moet worden beschouwd.

Deze eigenschap is een regex-tekenreeks. Als de aangeklikte URL overeenkomt met deze regex, wordt `xdm.web.webInteraction.type` ingesteld op `"download"` . Koppelingen worden ook direct geclassificeerd als een downloadkoppeling als deze het kenmerk `download` HTML bevatten. Wanneer `clickCollectionEnabled` niet is ingeschakeld, doet deze eigenschap niets.

## Koppelingskwalificatie downloaden met de webSDK-tagextensie

Laat **[!UICONTROL Enable click data collection]** checkbox toe, dan ga de gewenste tekst onder **[!UICONTROL Download link qualifier]** in wanneer [ het vormen van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie [!UICONTROL Data Collection] en schakel vervolgens het selectievakje **[!UICONTROL Enable click data collection]** in.
1. Zodra deze optie is ingeschakeld, wordt het tekstvak **[!UICONTROL Download link qualifier]** weergegeven. Voer de gewenste waarde in. Er zijn ook knoppen beschikbaar om de regex te testen en de standaardwaarde te herstellen.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Koppelingskwalificatie downloaden met de Web SDK JavaScript-bibliotheek

Stel de tekenreeks `downloadLinkQualifier` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat, wordt standaard de volgende waarde gebruikt:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Als u verschillende criteria wilt gebruiken om downloadverbindingen te kwalificeren, plaats dit bezit aan de gewenste regex waarde.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
