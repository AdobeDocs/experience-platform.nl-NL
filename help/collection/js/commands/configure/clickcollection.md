---
title: clickCollection
description: Stel de instellingen van de klikverzameling nauwkeurig in.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

Het `clickCollection` -object bevat verschillende variabelen die u helpen de automatisch verzamelde koppelingsgegevens te beheren. Gebruik deze variabelen als u typen koppelingen wilt opnemen in of uitsluiten van gegevensverzameling. Deze functie wordt ondersteund in SDK 2.25.0 of hoger op het web.

Deze variabele vereist het volgende:

* [`clickCollectionEnabled`](clickcollectionenabled.md) moet zijn ingeschakeld.
* Als u `clickCollection.filterClickDetails` gebruikt, moet de vervangen methode [`onBeforeLinkClickSend`](onbeforelinkclicksend.md) leeg zijn.
* De gebeurtenislading moet een waarde in `xdm.web.webPageDetails.name` op een punt in het bezoek van de bezoeker bevatten.

Als uw implementatie niet aan alle bovenstaande vereisten voldoet, doet dit object niets.

De volgende eigenschappen zijn beschikbaar in het object `clickCollection` :

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | Hiermee wordt bepaald of koppelingen binnen het huidige domein automatisch worden bijgehouden. `https://example.com/index.html` to `https://example.com/product.html` wordt bijvoorbeeld beschouwd als een interne koppeling. |
| **`downloadLinkEnabled`** | `boolean` | Hiermee wordt bepaald of de bibliotheek koppelingen bijhoudt die op basis van de eigenschap [`downloadLinkQualifier`](downloadlinkqualifier.md) als downloads worden gekwalificeerd. |
| **`externalLinkEnabled`** | `boolean` | Hiermee wordt bepaald of koppelingen naar externe domeinen automatisch worden bijgehouden. `https://example.com` to `https://example.net` wordt bijvoorbeeld beschouwd als een externe koppeling. |
| **`eventGroupingEnabled`** | `boolean` | Hiermee bepaalt u of de bibliotheek wacht tot de volgende &quot;paginaweergave&quot;-gebeurtenis gegevens voor het bijhouden van koppelingen verzendt. De bibliotheek beschouwt een gebeurtenis als een &quot;paginaweergave&quot; wanneer de volgende elementen in de payload zijn opgenomen:<ul><li>`xdm.web.webPageDetails.name` bevat een tekenreekswaarde</li><li>`xdm.web.webPageDetails.pageViews.value` is groter dan `0`</li></ul>Wanneer de gebeurtenis &quot;paginaweergave&quot; wordt geladen, combineert de bibliotheek opgeslagen gegevens voor het bijhouden van koppelingen met de overige gegevens in die gebeurtenis. Als u deze optie inschakelt, wordt het totale aantal gebeurtenissen dat u naar Adobe verzendt, verminderd. Als `internalLinkEnabled` is uitgeschakeld, heeft deze variabele geen effect. |
| **`sessionStorageEnabled`** | `boolean` | Hiermee wordt bepaald of gegevens voor het bijhouden van koppelingen worden opgeslagen in sessieopslag in plaats van in lokale variabelen. Als `internalLinkEnabled` of `eventGroupingEnabled` zijn uitgeschakeld, heeft deze variabele geen effect.<br> Adobe adviseert sterk toelatend deze variabele wanneer het gebruiken van `eventGroupingEnabled` buiten enig-paginatoepassingen. Als `eventGroupingEnabled` is ingeschakeld terwijl `sessionStorageEnabled` is uitgeschakeld, leidt het klikken op een nieuwe pagina tot het verlies van gegevens voor het bijhouden van koppelingen, omdat deze gegevens niet behouden blijven in de sessieopslag. Aangezien de enig-paginatoepassingen niet typisch aan een nieuwe pagina navigeren, wordt de zittingsopslag niet vereist voor de pagina&#39;s van het KUUROORD. |
| **`filterClickDetails`** | `function` | Een callback functie die volledige controles over verbinding het volgen gegevens verstrekt die u verzamelt. U kunt deze callback functie gebruiken om het verzenden van verbinding het volgen gegevens te veranderen, te verduisteren of te breken. Deze callback is nuttig wanneer u specifieke informatie, zoals persoonlijk identificeerbare informatie binnen verbindingen wilt weglaten. |

Als u dit object niet instelt in de opdracht [`configure`](overview.md) , zijn de standaardinstellingen voor dit object afhankelijk van de waarde van [`clickCollectionEnabled`](clickcollectionenabled.md) :

* `internalLinkEnabled`: Overeenkomsten `clickCollectionEnabled`
* `downloadLinkEnabled`: Overeenkomsten `clickCollectionEnabled`
* `externalLinkEnabled`: Overeenkomsten `clickCollectionEnabled`
* `eventGroupingEnabled`: is standaard ingesteld op `false` ; moet expliciet zijn ingeschakeld
* `sessionStorageEnabled`: is standaard ingesteld op `false` ; moet expliciet zijn ingeschakeld
* `filterClickDetails`: bevat geen functie; moet expliciet worden geregistreerd

>[!TIP]
>
>Adobe raadt u aan `eventGroupingEnabled` in te schakelen wanneer `internalLinkEnabled` wordt ingeschakeld, aangezien dit het aantal gebeurtenissen vermindert dat telt voor gebruik in een overeenkomst.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```

## Klikverzameling configureren voor de Web SDK-tagextensie

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [&#x200B; de configuratiemontages van de inzameling van Gegevens &#x200B;](/help/tags/extensions/client/web-sdk/configure/data-collection.md).
