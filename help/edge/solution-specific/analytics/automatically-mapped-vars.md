---
title: Variabelen automatisch toegewezen in Analytics
seo-title: Variabelen automatisch toegewezen in Analytics met Web SDK van Adobe Experience Platform
description: Leer welke Variabelen automatisch in Analytics met het Web SDK van het Experience Platform worden toegewezen
seo-description: Leer welke Variabelen automatisch in Analytics met het Web SDK van het Experience Platform worden toegewezen
translation-type: tm+mt
source-git-commit: a7c8830c5c8152b1f21373a506b2fff97d43c40a
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# Variabelen automatisch toegewezen in Analytics

Hieronder volgt een lijst met variabelen die het Edge Network van het Adobe Experience Platform automatisch toewijst aan Analytics.

| XDM-veldpad | Analytics Query String / HTTP Header | Beschrijving |
| ---------- | ------------------------- | -------- |
| `commerce.order.purchaseID` | `pi` | PURCHASEID-toewijzing voor queryparameter AppMeturement. |
| `commerce.order.currencyCode` | `cc` | Toewijzing van de query voor de parameter CURRENCY voor AppMeasurement. |
| `commerce.purchases.value` | `events` | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_PURCHASE, met behulp van scheidingsteken `,`. |
| `commerce.productViews.value` | `events` | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_PROD_VIEW, met behulp van scheidingsteken `,`. |
| `commerce.productListOpens.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeturement met omzetting COMMERCE_SC_OPEN, gebruikend afbakening `,`. |
| `commerce.productListViews.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeasurement met omzetting COMMERCE_SC_VIEW, gebruikend afbakening `,`. |
| `commerce.checkouts.value` | `events` | De vraagparameter EVENT_LIST_FULL van de AppMeasurement van de vraag met omzetting COMMERCE_SC_CHECKOUT, gebruikend afbakening `,`. |
| `commerce.productListAdds.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeasurement met omzetting COMMERCE_SC_ADD, gebruikend afbakening `,`. |
| `commerce.productListRemovals.value` | `events` | De vraagparameter EVENT_LIST_FULL van AppMeasurement met omzetting COMMERCE_SC_REMOVE, gebruikend afbakening `,`. |
| `commerce.productViews.id` | `events` | `prodView` Serienummering van gebeurtenissen. |
| `commerce.productListOpens.id` | `events` | `scOpen` Serienummering van gebeurtenissen. |
| `commerce.productListViews.id` | `events` | `scView` Serienummering van gebeurtenissen. |
| `commerce.productListAdds.id` | `events` | `scAdd` Serienummering van gebeurtenissen. |
| `commerce.productListRemovals.id` | `events` | `scRemove` Serienummering van gebeurtenissen. |
| `commerce.checkouts.id` | `events` | `scCheckout` Serienummering van gebeurtenissen. |
| `device.screenHeight` | `s` | Schermresolutie toepassingsparameters. |
| `device.screenWidth` | `s` | Schermresolutie toepassingsparameters. |
| `productlistitems.[N].lineitemid` | `products` | Toewijzing van de categorie Producten van de vraagparameter AppMeasurement. |
| `productlistitems.[N].name` | `products` | Toewijzing van naam van toepassingsparameter voor queryparameter voor producten. |
| `productlistitems.[N].quantity` | `products` | AppMeasurement de parameterproducten van de vraagparameterProducts Quantity mapping. |
| `productlistitems.[N].pricetotal` | `products` | AppMeasurement-queryparameter Products Price mapping. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Contextgegevens van AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Contextgegevens van AppMeasurement. |
| `environment.browserDetails.userAgent` | `User-Agent` | Dit is een HTTP-kopteksttoewijzing, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Dit is een HTTP-kopteksttoewijzing, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement-queryparameter COOKIES-toewijzing met conversie BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement-queryparameter J_JSCRIPT-toewijzing. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement query parameter JAVA_ENABLED mapping met conversie BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement-queryparameter BROWSER_HEIGHT-toewijzing. |
| `environment.browserDetails.viewportWidth` | `bw` | Query-parameter BROWSER_WIDTH voor AppMeasurement. |
| `environment.connectionType` | `ct` | Toepassingsmetingqueryparameter CT_CONNECT_TYPE-toewijzing. |
| `device.colorDepth` | `c` | Query-parameter C_COLOR voor AppMeasurement. |
| `placeContext.geo.stateProvince` | `state` | STATE-toewijzing voor queryparameter AppMeturement. |
| `placeContext.geo.postalCode` | `zip` | Zoekparameter ZIP-toewijzing voor AppMeasurement-query. |
| `placeContext.geo.latitude` | `lat` | Toewijzing LATITUDE-queryparameter voor AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Toewijzing LONGITUDE-queryparameter voor AppMeasurement. |
| `web.webPageDetails.server` | `sv` | Toepassingsmetingqueryparameter USER_SERVER-toewijzing. |
| `web.webPageDetails.name` | `gn` | PAGENAME-toewijzing voor queryparameter AppMeasurement. |
| `web.webPageDetails.URL` | `g` | Toewijzing PAGE_URL-queryparameter voor AppMeturement. |
| `web.webPageDetails.homePage` | `hp` | Toepassingsmetingqueryparameter HOMEPAGE-toewijzing met conversie BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | REFERRER-toewijzing voor query-parameter voor AppMeasurement. |
| `web.webInteraction.type` | `pe` | Toepassingsmetingqueryparameter PAGE_EVENT-toewijzing met conversie CLICK_MAP_TYPE. |
| `web.webInteraction.URL` | `pev1` | Toepassingsmetingqueryparameter PAGE_EVENT_VAR1-toewijzing. |
| `web.webInteraction.name` | `pev2` | Toepassingsmetingqueryparameter PAGE_EVENT_VAR2-toewijzing. |
| `web.webPageDetails.siteSection` | `ch` | CHANNEL-toewijzing voor queryparameter voor AppMeasurement. |
| `web.webPageDetails.errorPage` | `pageType` | Toepassingsmetingqueryparameter PAGE_TYPE_FULL-toewijzing met conversiefout_PAGE_TYPE. |
| `application.id` | `c.a.appid` | Contextgegevenstoewijzing `c.a.appid` voor AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Contextgegevenstoewijzing `c.a.launches` voor AppMeasurement. |
| `marketing.trackingCode` | `v0` | CAMPAIGN-toewijzing voor queryparameter voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Contextgegevenstoewijzing `a.media.name` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Contextgegevenstoewijzing `c.a.media.length` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Contextgegevenstoewijzing `c.a.contentType` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Contextgegevenstoewijzing `c.a.media.playerName` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Contextgegevenstoewijzing `c.a.media.channel` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Contextgegevenstoewijzing `c.a.media.segment` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Contextgegevenstoewijzing `c.a.media.friendlyName` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Contextgegevenstoewijzing `c.a.media.sdkVersion` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Contextgegevenstoewijzing `c.a.media.show` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Contextgegevenstoewijzing `c.a.media.format` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Contextgegevenstoewijzing `c.a.media.season` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Contextgegevenstoewijzing `c.a.media.episode` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Contextgegevenstoewijzing `c.a.media.network` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Contextgegevens van AppMeasurement- `c.a.media.type` toewijzing met conversie VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Contextgegevenstoewijzing `c.a.media.feed` voor AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Contextgegevenstoewijzing `c.a.media.timePlayed` voor AppMeasurement. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Contextgegevenstoewijzing `c.a.media.totalTimePlayed` voor AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Contextgegevenstoewijzing `c.a.media.federated` voor AppMeasurement. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Contextgegevenstoewijzing `c.a.media.pauseCount` voor AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Contextgegevenstoewijzing `c.a.media.pauseTime` voor AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Contextgegevenstoewijzing `c.a.media.resume` voor AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Contextgegevens van AppMeasurement worden `c.a.media.type` toegewezen met conversie VIDEO_SHOW_TYPE. |
| `identityMap.ECID.[0].id` | `mid` | MID-toewijzing van queryparameter voor AppMeturement. |
