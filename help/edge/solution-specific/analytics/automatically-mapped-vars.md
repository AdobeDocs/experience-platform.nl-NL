---
title: Variabelen worden automatisch toegewezen in Analytics
seo-title: Variabelen worden automatisch toegewezen in Analyses met Adobe Experience Platform Web SDK
description: Leer welke Variabelen automatisch in Analytics met het Web SDK van het Platform van de Ervaring worden toegewezen
seo-description: Leer welke Variabelen automatisch in Analytics met het Web SDK van het Platform van de Ervaring worden toegewezen
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bèta) Variabelen worden automatisch toegewezen in Analytics

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Hieronder volgt een lijst met variabelen die het Adobe Experience Platform Edge Network automatisch toewijst aan Analytics.

| XDM-veldpad | Tekenreeks analytische query / HTTP-header | Beschrijving |
| ---------- | ------------------------- | -------- |
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
| `application.id` | `c.a.appid` | Contextgegevenstoewijzing `c.a.appid` voor AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Contextgegevenstoewijzing `c.a.launches` voor AppMeasurement. |
| `marketing.trackingCode` | `v0` | CAMPAIGN-toewijzing voor queryparameter voor AppMeasurement. |
| `commerce.purchaseID` | `pi` | PURCHASEID-toewijzing voor queryparameter AppMeturement. |
| `commerce.currencyCode` | `cc` | Toewijzing van de query voor de parameter CURRENCY voor AppMeasurement. |
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
| `identitymap.ecid.[0].id` | `mid` | MID-toewijzing van queryparameter voor AppMeturement. |
