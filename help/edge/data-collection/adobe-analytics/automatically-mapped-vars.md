---
title: Automatisch toegewezen Adobe Analytics-variabelen in de Adobe Experience Platform Web SDK
description: Leer welke Variabelen automatisch in Adobe Analytics met het Web SDK van het Experience Platform worden toegewezen
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: 09c6986fcd3682377725ded389496d5076e9e1e2
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# Variabelen worden automatisch toegewezen in [!DNL Analytics]

Hieronder volgt een lijst met variabelen die Adobe Experience Platform Edge Network automatisch in Adobe Analytics toewijst. Gedetailleerde informatie over de vraagparameters van de de gegevensinzameling van Adobe Analytics kan in [de Gids van de Implementatie van Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html) worden gevonden.

| XDM-veldpad | [!DNL Analytics Query String] / HTTP-koptekst | Beschrijving |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | Contextgegevens `c.a.appid`-toewijzing voor AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Contextgegevens `c.a.launches`-toewijzing voor AppMeasurement. |
| `commerce.checkouts.id` | `events` | `scCheckout` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| `commerce.checkouts.value` | `events` | De vraagparameter EVENT_LIST_FULL van de AppMeasurement van de vraag met omzetting COMMERCE_SC_CHECKOUT, gebruikend afbakening `,`. |
| `commerce.order.currencyCode` | `cc` | Toewijzing van de query voor de parameter CURRENCY voor AppMeasurement. |
| `commerce.order.purchaseID` | `pi` | PURCHASEID-toewijzing voor queryparameter AppMeturement. |
| `commerce.productListAdds.id` | `events` | `scAdd` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| `commerce.productListAdds.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeturement met omzetting COMMERCE_SC_ADD, gebruikend afbakening `,`. |
| `commerce.productListOpens.id` | `events` | `scOpen` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| `commerce.productListOpens.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeturement met omzetting COMMERCE_SC_OPEN, gebruikend afbakening `,`. |
| `commerce.productListRemovals.id` | `events` | `scRemove` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| `commerce.productListRemovals.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeturement met omzetting COMMERCE_SC_REMOVE, gebruikend afbakening `,`. |
| `commerce.productListViews.id` | `events` | `scView` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| `commerce.productListViews.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeturement met omzetting COMMERCE_SC_VIEW, gebruikend afbakening `,`. |
| `commerce.productViews.id` | `events` | `prodView` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| `commerce.productViews.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeturement met omzetting COMMERCE_PROD_VIEW, gebruikend afbakening `,`. |
| `commerce.purchases.value` | `events` | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_PURCHASE, met scheidingsteken `,`. |
| `device.colorDepth` | `c` | Query-parameter C_COLOR voor AppMeasurement. |
| `device.screenHeight` | `s` | Schermresolutie toepassingsparameters. |
| `device.screenWidth` | `s` | Schermresolutie toepassingsparameters. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Dit is een HTTP-kopteksttoewijzing, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement-queryparameter COOKIES-toewijzing met conversie BOOLEAN_TO_YN. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement query parameter JAVA_ENABLED mapping met conversie BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement-queryparameter J_JSCRIPT-toewijzing. |
| `environment.browserDetails.userAgent` | `User-Agent` | Dit is een HTTP-kopteksttoewijzing, HEADER_USER_AGENT. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement-queryparameter BROWSER_HEIGHT-toewijzing. |
| `environment.browserDetails.viewportWidth` | `bw` | Query-parameter BROWSER_WIDTH voor AppMeasurement. |
| `environment.connectionType` | `ct` | Toepassingsmetingqueryparameter CT_CONNECT_TYPE-toewijzing. |
| `environment.ipV4` | `X-Forwarded-For` | Dit is een HTTP-koptekstoewijzing, X-FORWARDED-FOR. |
| `identityMap.ECID.[0].id` | `mid` | MID-toewijzing van queryparameter voor AppMeturement. |
| `marketing.trackingCode` | `v0` | CAMPAIGN-toewijzing voor queryparameter voor AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Contextgegevens `c.a.media.federated`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Contextgegevens `c.a.media.pauseTime`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Contextgegevens `c.a.media.pauseCount`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Contextgegevens `c.a.media.friendlyName`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Contextgegevens `c.a.media.episode`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Contextgegevens `c.a.media.season`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Contextgegevens `a.media.name`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Contextgegevens `c.a.media.show`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Contextgegevens `c.a.media.type` van AppMeasurement met omzetting VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Contextgegevens `c.a.media.type` van AppMeasurement met conversie VIDEO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Contextgegevens `c.a.media.length`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Contextgegevens `c.a.media.channel`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Contextgegevens `c.a.contentType`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Contextgegevens `c.a.media.network`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Contextgegevens `c.a.media.segment`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Contextgegevens `c.a.media.playerName`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Contextgegevens `c.a.media.sdkVersion`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Contextgegevens `c.a.media.feed`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Contextgegevens `c.a.media.format`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Contextgegevens `c.a.media.resume`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Contextgegevens `c.a.media.timePlayed`-toewijzing voor AppMeasurement. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Contextgegevens `c.a.media.totalTimePlayed`-toewijzing voor AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Toewijzing LATITUDE-queryparameter voor AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Toewijzing LONGITUDE-queryparameter voor AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Zoekparameter ZIP-toewijzing voor AppMeasurement-query. |
| `placeContext.geo.stateProvince` | `state` | STATE-toewijzing voor queryparameter AppMeturement. |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | AppMeasurement-queryparameterparameters Products Merchandise Events/Evars mapping. |
| `productListItems[N].lineItemId` | `products` | Toewijzing van naam van toepassingsparameter voor queryparameter voor producten. |
| `productlistitems.[N].name` | `products` | Toewijzing van de categorie Producten van de vraagparameter AppMeasurement. |
| `productlistitems.[N].priceTotal` | `products` | AppMeasurement-queryparameter Products Price mapping. |
| `productlistitems.[N].quantity` | `products` | AppMeasurement de parameterproducten van de vraagparameterProducts Quantity mapping. |
| `web.webInteraction.URL` | `pev1` | Toepassingsmetingqueryparameter PAGE_EVENT_VAR1-toewijzing. |
| `web.webInteraction.name` | `pev2` | Toepassingsmetingqueryparameter PAGE_EVENT_VAR2-toewijzing. |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` naar  `pe=lnk_o`;  `web.webInteraction.type=download` naar  `pe=lnk_d`;  `web.webInteraction.type=exit` tot  `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | Toewijzing PAGE_URL-queryparameter voor AppMeturement. |
| `web.webPageDetails.errorPage` | `pageType` | Toepassingsmetingqueryparameter PAGE_TYPE_FULL-toewijzing met conversiefout_PAGE_TYPE. |
| `web.webPageDetails.homePage` | `hp` | Toepassingsmetingqueryparameter HOMEPAGE-toewijzing met conversie BOOLEAN_TO_YN. |
| `web.webPageDetails.name` | `gn` | PAGENAME-toewijzing voor queryparameter AppMeasurement. |
| `web.webPageDetails.server` | `sv` | Toepassingsmetingqueryparameter USER_SERVER-toewijzing. |
| `web.webPageDetails.siteSection` | `ch` | CHANNEL-toewijzing voor queryparameter voor AppMeasurement. |
| `web.webReferrer.URL` | `r` | REFERRER-toewijzing voor query-parameter voor AppMeasurement. |

{style=&quot;table-layout:auto&quot;}
