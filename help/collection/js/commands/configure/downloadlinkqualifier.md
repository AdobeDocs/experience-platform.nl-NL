---
title: downloadLinkQualifier
description: Hiermee kunt u bepalen hoe automatische koppelingen bijhouden downloadkoppelingen kwalificeert.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

Als u automatische koppeling bijhouden inschakelt met [`clickCollectionEnabled`](clickcollectionenabled.md) , kunt u aan de hand van de eigenschap `downloadLinkQualifier` bepalen aan welke criteria een URL als downloadkoppeling moet worden beschouwd.

Deze eigenschap is een regex-tekenreeks. Als de aangeklikte URL overeenkomt met deze regex, wordt `xdm.web.webInteraction.type` ingesteld op `"download"` . Koppelingen worden ook direct geclassificeerd als een downloadkoppeling als ze een `download` HTML-kenmerk bevatten. Wanneer `clickCollectionEnabled` niet is ingeschakeld, doet deze eigenschap niets.

Stel de tekenreeks `downloadLinkQualifier` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat, wordt standaard de volgende waarde gebruikt:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Als u verschillende criteria wilt gebruiken om downloadverbindingen te kwalificeren, plaats dit bezit aan de gewenste regex waarde.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## Koppelingskwalificatie downloaden met de Web SDK-tagextensie

Het de markeringsequivalent van SDK van het Web van dit gebied is onder [&#x200B; de configuratiemontages van de inzamelingsconfiguratie van Gegevens &#x200B;](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier) wanneer het vormen van de markeringsuitbreiding.
