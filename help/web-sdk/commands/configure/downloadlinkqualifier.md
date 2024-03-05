---
title: downloadLinkQualifier
description: Hiermee kunt u bepalen hoe automatische koppelingen bijhouden downloadkoppelingen kwalificeert.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# `downloadLinkQualifier`

Als u automatische koppeling bijhouden inschakelt met [`clickCollectionEnabled`](clickcollectionenabled.md)de `downloadLinkQualifier` helpt bij het bepalen van de criteria voor een URL die als een downloadkoppeling moet worden beschouwd.

Deze eigenschap is een regex-tekenreeks. Als de aangeklikte URL met deze regex overeenkomt, `xdm.web.webInteraction.type` is ingesteld op `"download"`. Koppelingen worden ook direct geclassificeerd als een downloadlink als ze een `download` HTML, kenmerk. Indien `clickCollectionEnabled` is niet ingeschakeld, heeft deze eigenschap geen effect.

## Koppelingskwalificatie downloaden met de webSDK-tagextensie

De optie **[!UICONTROL Enable click data collection]** selectievakje en voer vervolgens de gewenste tekst in onder **[!UICONTROL Download link qualifier]** wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens het selectievakje **[!UICONTROL Enable click data collection]**.
1. Wanneer deze optie is ingeschakeld, wordt de **[!UICONTROL Download link qualifier]** wordt weergegeven. Voer de gewenste waarde in. Er zijn ook knoppen beschikbaar om de regex te testen en de standaardwaarde te herstellen.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Koppelingskwalificatie downloaden met de Web SDK JavaScript-bibliotheek

Stel de `downloadLinkQualifier` tekenreeks bij het uitvoeren van de `configure` gebruiken. Als u deze eigenschap weglaat, wordt standaard de volgende waarde gebruikt:

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
