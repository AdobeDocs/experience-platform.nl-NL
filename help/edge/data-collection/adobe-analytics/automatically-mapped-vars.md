---
title: Automatisch toegewezen Adobe Analytics-variabelen in de Adobe Experience Platform Web SDK
description: Leer welke Variabelen automatisch in Adobe Analytics met het Web SDK van het Experience Platform worden toegewezen
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 4%

---

# Variabelen worden automatisch toegewezen in [!DNL Analytics]

Hieronder volgt een lijst met variabelen die Adobe Experience Platform Edge Network automatisch in Adobe Analytics toewijst. Gedetailleerde informatie over de parameters van de de vraagvraag van de gegevensinzameling van Adobe Analytics kan in worden gevonden [Handleiding voor analytische implementatie](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html).

>[!NOTE]
>De informatie op deze pagina is ook van toepassing op Adobe Mobile SDK.

| XDM-veldpad | [!DNL Analytics Query String] / HTTP-koptekst | Beschrijving |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Contextgegevens van AppMeasurement `c.a.appid` toewijzing. |
| application.launches.value | c.a.launches | Contextgegevens van AppMeasurement `c.a.launches` toewijzing. |
| commerce.checkouts.id | events | `scCheckout` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| commerce.checkouts.value | gebeurtenissen | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_SC_CHECKOUT, met behulp van scheidingsteken `,`. |
| commerce.order.currencyCode | cc | Toewijzing van de query voor de parameter CURRENCY voor AppMeasurement. |
| commerce.order.purchaseID | pi | PURCHASEID-toewijzing voor queryparameter AppMeturement. |
| commerce.productListAdds.id | gebeurtenissen | `scAdd` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| commerce.productListAdds.value | gebeurtenissen | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_SC_ADD, met behulp van scheidingsteken `,`. |
| commerce.productListOpens.id | gebeurtenissen | `scOpen` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| commerce.productListOpens.value | gebeurtenissen | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_SC_OPEN, met scheidingsteken `,`. |
| commerce.productListRemovals.id | gebeurtenissen | `scRemove` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| commerce.productListRemovals.value | gebeurtenissen | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_SC_REMOVE, met behulp van scheidingsteken `,`. |
| commerce.productListViews.id | gebeurtenissen | `scView` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| commerce.productListViews.value | gebeurtenissen | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_SC_VIEW, met scheidingsteken `,`. |
| commerce.productViews.id | gebeurtenissen | `prodView` gebeurtenisserialisatie. Als dit veld wordt uitgesloten (d.w.z. voor gebeurtenissen zonder serienummering), genereert het systeem een eigen id-waarde en wijst het deze toe aan de entiteit. |
| commerce.productViews.value | gebeurtenissen | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_PROD_VIEW, met scheidingsteken `,`. |
| commerce.purchases.value | gebeurtenissen | Toepassingsmetingqueryparameter EVENT_LIST_FULL-toewijzing met conversie COMMERCE_PURCHASE, met scheidingsteken `,`. |
| device.colorDepth | c | Query-parameter C_COLOR voor AppMeasurement. |
| device.screenHeight | s | Schermresolutie toepassingsparameters. |
| device.screenWidth | s | Schermresolutie toepassingsparameters. |
| environment.browserDetails.acceptLanguage | Accept-Language | Dit is een HTTP-kopteksttoewijzing, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | AppMeasurement-queryparameter COOKIES-toewijzing met conversie BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | v | AppMeasurement query parameter JAVA_ENABLED mapping met conversie BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | AppMeasurement-queryparameter J_JSCRIPT-toewijzing. |
| environment.browserDetails.userAgent | Gebruikersagent | Dit is een HTTP-kopteksttoewijzing, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | AppMeasurement-queryparameter BROWSER_HEIGHT-toewijzing. |
| environment.browserDetails.viewportWidth | bw | Query-parameter BROWSER_WIDTH voor AppMeasurement. |
| environment.connectionType | ct | Toepassingsmetingqueryparameter CT_CONNECT_TYPE-toewijzing. |
| environment.ipV4 | X-Forwarded-For | Dit is een HTTP-koptekstoewijzing, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | midden | MID-toewijzing van queryparameter voor AppMeturement. |
| marketing.trackingCode | v0 | CAMPAIGN-toewijzing voor queryparameter voor AppMeasurement. |
| media.mediaTimed.completes.value | c.a.media.complete | Contextgegevens van AppMeasurement. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | Contextgegevens van AppMeasurement. |
| media.mediaTimed.federated.value | c.a.media.federated | Contextgegevens van AppMeasurement `c.a.media.federated` toewijzing. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | Contextgegevens van AppMeasurement. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | Contextgegevens van AppMeasurement. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | Contextgegevens van AppMeasurement. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | Contextgegevens van AppMeasurement `c.a.media.pauseTime` toewijzing. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | Contextgegevens van AppMeasurement `c.a.media.pauseCount` toewijzing. |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | Contextgegevens van AppMeasurement. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | Contextgegevens van AppMeasurement `c.a.media.friendlyName` toewijzing. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | Contextgegevens van AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | Contextgegevens van AppMeasurement `c.a.media.episode` toewijzing. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | Contextgegevens van AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | Contextgegevens van AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | Contextgegevens van AppMeasurement `c.a.media.season` toewijzing. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | Contextgegevens van AppMeasurement `a.media.name` toewijzing. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | Contextgegevens van AppMeasurement `c.a.media.show` toewijzing. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Contextgegevens van AppMeasurement `c.a.media.type` omzetten met VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Contextgegevens van AppMeasurement `c.a.media.type` toewijzen met conversie VIDEO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | Contextgegevens van AppMeasurement `c.a.media.length` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | Contextgegevens van AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | Contextgegevens van AppMeasurement `c.a.media.channel` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | Contextgegevens van AppMeasurement `c.a.contentType` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | Contextgegevens van AppMeasurement `c.a.media.network` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | Contextgegevens van AppMeasurement `c.a.media.segment` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | Contextgegevens van AppMeasurement `c.a.media.playerName` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | Contextgegevens van AppMeasurement `c.a.media.sdkVersion` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | Contextgegevens van AppMeasurement `c.a.media.feed` toewijzing. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | Contextgegevens van AppMeasurement `c.a.media.format` toewijzing. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | Contextgegevens van AppMeasurement. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | Contextgegevens van AppMeasurement. |
| media.mediaTimed.resumes.value | c.a.media.resume | Contextgegevens van AppMeasurement `c.a.media.resume` toewijzing. |
| media.mediaTimed.starts.value | c.a.media.view | Contextgegevens van AppMeasurement. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | Contextgegevens van AppMeasurement. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | Contextgegevens van AppMeasurement `c.a.media.timePlayed` toewijzing. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | Contextgegevens van AppMeasurement `c.a.media.totalTimePlayed` toewijzing. |
| placeContext.geo.latitude | lat | Toewijzing LATITUDE-queryparameter voor AppMeasurement. |
| placeContext.geo.longitude | lon | Toewijzing LONGITUDE-queryparameter voor AppMeasurement. |
| placeContext.geo.postalCode | zip | Zoekparameter ZIP-toewijzing voor AppMeasurement-query. |
| placeContext.geo.stateProvince | state | STATE-toewijzing voor queryparameter AppMeturement. |
| productListItems[N].lineItemId | products | Toewijzing van de categorie Producten van de vraagparameter AppMeasurement. |
| productlistitems[N].name | producten | Toewijzing van naam van toepassingsparameter voor queryparameter voor producten. |
| productlistitems[N].priceTotal | producten | AppMeasurement-queryparameter Products Price mapping. |
| productlistitems[N].quantity | producten | AppMeasurement de parameterproducten van de vraagparameterProducts Quantity mapping. |
| web.webInteraction.URL | pev1 | Toepassingsmetingqueryparameter PAGE_EVENT_VAR1-toewijzing. |
| web.webInteraction.name | pev2 | Toepassingsmetingqueryparameter PAGE_EVENT_VAR2-toewijzing. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` tot `pe=lnk_o`; `web.webInteraction.type=download` tot `pe=lnk_d`; `web.webInteraction.type=exit` tot `pe=lnk_e` |
| web.webPageDetails.URL | g | Toewijzing PAGE_URL-queryparameter voor AppMeturement. |
| web.webPageDetails.errorPage | pageType | Toepassingsmetingqueryparameter PAGE_TYPE_FULL-toewijzing met conversiefout_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | Toepassingsmetingqueryparameter HOMEPAGE-toewijzing met conversie BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | PAGENAME-toewijzing voor queryparameter AppMeasurement. |
| web.webPageDetails.server | sv | Toepassingsmetingqueryparameter USER_SERVER-toewijzing. |
| web.webPageDetails.siteSection | ch | CHANNEL-toewijzing voor queryparameter voor AppMeasurement. |
| web.webReferrer.URL | r | REFERRER-toewijzing voor query-parameter voor AppMeasurement. |

{style=&quot;table-layout:auto&quot;}
