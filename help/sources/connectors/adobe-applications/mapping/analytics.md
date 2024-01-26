---
keywords: Analytische toewijzingsvelden;analytische toewijzing
solution: Experience Platform
title: Toewijzingsvelden voor de Adobe Analytics Source Connector
description: Wijs Adobe Analytics-velden toe aan XDM-velden met behulp van de Analytics Source Connector.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 6cbd902c6a1159d062fb38bf124a09bb18ad1ba8
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# Toewijzingen van analytische velden

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de bron Analytics. Sommige gegevens die via ADC worden ingevoerd, kunnen rechtstreeks van de gebieden van Analytics aan de gebieden van het Gegevensmodel van de Ervaring worden in kaart gebracht (XDM), terwijl andere gegevens transformaties en specifieke functies vereisen om met succes worden in kaart gebracht.

![](../images/analytics-data-experience-platform.png)

## Directe toewijzingsvelden

Bepaalde velden worden rechtstreeks toegewezen vanuit Adobe Analytics naar het XDM-model (Experience Data Model).

| Veld Analyse | XDM-veld | XDM-type | Beschrijving |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | string | Aangepaste analytische variabelen. Elke organisatie kan eVars anders gebruiken. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | string | Aangepaste analytische voorkeuren. Elke organisatie kan eigen principes anders gebruiken. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | integer | De nummer-id van de browser. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | integer | De hoogte van de browser, in pixels. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | integer | De breedte van de browser, in pixels. |
| `m_campaign` | `marketing.trackingCode` | string | De variabele die wordt gebruikt in de dimensie Code bijhouden. |
| `m_channel` | `web.webPageDetails.siteSection` | string | De variabele die wordt gebruikt in de dimensie Site-secties. |
| `m_domain` | `environment.domain` | string | De variabele die wordt gebruikt in de dimensie Domein. Het is gebaseerd op Internet Service Provider (ISP) van de gebruiker. |
| `m_geo_city` | `placeContext.geo.city` | string | De naam van de stad van de hit. Dit is gebaseerd op het IP van de klap adres. |
| `m_geo_dma` | `placeContext.geo.dmaID` | integer | De numerieke id van het demografische gebied voor de hit. Dit is gebaseerd op het IP van de klap adres. |
| `m_geo_region` | `placeContext.geo.stateProvince` | string | De naam van de staat of regio van de treffer. Dit is gebaseerd op het IP van de klap adres. |
| `m_geo_zip` | `placeContext.geo.postalCode` | string | De postcode van de hit. Dit is gebaseerd op het IP van de klap adres. |
| `m_keywords` | `search.keywords` | string | De variabele die in de afmeting van het Sleutelwoord wordt gebruikt. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | integer | De numerieke id die het besturingssysteem van de bezoeker vertegenwoordigt. Dit is gebaseerd op de user_agent kolom. |
| `m_page_url` | `web.webPageDetails.URL` | string | De URL van de paginaklok. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | string | Gelijk aan 1 op treffers die een paginanaam hebben. Dit lijkt op de metrische weergave van Adobe Analytics-paginaweergaven. |
| `m_referrer` | `web.webReferrer.URL` | string | De pagina-URL van de vorige pagina. |
| `m_search_page_num` | `search.pageDepth` | integer | Wordt gebruikt door de afmeting Alle zoekpaginaranalen. Hiermee geeft u aan op welke pagina met zoekresultaten uw site is weergegeven voordat de gebruiker op uw site heeft geklikt. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | string | Staatvariabele. |
| `m_user_server` | `web.webPageDetails.server` | string | Een variabele die in de dimensie van de Server wordt gebruikt. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | string | Een variabele die wordt gebruikt om de dimensie van de Code van het PIT te bevolken. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | string | Hiermee worden alle geaccepteerde talen weergegeven, zoals wordt aangegeven in de HTTP-header van Accept-Language. |
| `homepage` | `web.webPageDetails.isHomePage` | boolean | Niet meer gebruikt. Geeft aan of de huidige URL de homepage van de browser is. |
| `ipv6` | `environment.ipV6` | string |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | string | De versie van JavaScript die door de browser wordt ondersteund. |
| `user_agent` | `environment.browserDetails.userAgent` | string | De userAgent-tekenreeks die in de HTTP-header wordt verzonden. |
| `mobileappid` | `application.name` | string | De mobiele toepassings-id wordt opgeslagen in de volgende indeling: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | string | De naam van het mobiele apparaat. In iOS wordt de notatie opgeslagen als een door komma&#39;s gescheiden tekenreeks van 2 cijfers. Het eerste getal vertegenwoordigt de apparaatgeneratie en het tweede getal vertegenwoordigt de apparaatfamilie. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | string | Wordt gebruikt door mobiele services. Vertegenwoordigt het aandachtspunt. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | getal | Wordt gebruikt door mobiele services. Geeft de afstand van het punt van de belangstelling aan. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | getal | Verzameld van de contextgegevensvariabele a.loc.acc. Geeft de nauwkeurigheid van de GPS in meters aan op het moment van verzameling. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | string | Verzameld van de contextgegevensvariabele a.loc.category. Beschrijft de categorie van een specifieke plaats. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | string | Verzameld van de contextgegevensvariabele a.loc.id. Identificatiecode voor een bepaald aandachtspunt. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | string | De naam van de video. |
| `videoad` | `advertising.adAssetReference._id` | string | Identificatiecode van het advertentie-element. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | string | Het type video-inhoud. Deze wordt automatisch ingesteld op &quot;Video&quot; voor alle videoweergaven. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | string | De pod waarin de video-advertentie zich bevindt. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | integer | De positie van de video-advertentie in de pod. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | string | De naam van de videospeler. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | string | Het kanaal Video. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | string | De naam van de videospeler. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | string | De naam van het hoofdstuk Video |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | string | De videonaam. |
| `videoadname` | `advertising.adAssetReference._dc.title` | string | De naam van de advertentie voor video. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | string | Videoshow. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | string | Videoseizoen. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | string | Video-aflevering. |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | string | Videonetwerk. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | string | Type videoshow. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | string | Video en laden. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | string | Type videofeed. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | getal | Belangrijkste baken voor mobiele services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | getal | Beacon minor mobiele diensten. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | string | Mobile Services-baken UUID. |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | string | Video sessie-id. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | array | Videogenre. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (tekenreeks), meta:xdmField (Object)} |
| `mobileinstalls` | `application.firstLaunches` | Object | Dit wordt geactiveerd bij de eerste uitvoering na installatie of herinstallatie | {id (string), value (number)} |
| `mobileupgrades` | `application.upgrades` | Object | Meldt het aantal upgrades van de app. Triggers bij de eerste looppas na verbetering of om het even welk ogenblik verandert het versieaantal. | {id (string), value (number)} |
| `mobilelaunches` | `application.launches` | Object | Het aantal keren dat de app is gestart. | {id (string), value (number)} |
| `mobilecrashes` | `application.crashes` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videotime` | `media.mediaTimed.timePlayed` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videostart` | `media.mediaTimed.impressions` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videocomplete` | `media.mediaTimed.completes` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoadstart` | `advertising.impressions` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoadcomplete` | `advertising.completes` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoadtime` | `advertising.timePlayed` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoplay` | `media.mediaTimed.starts` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Object | De videokwaliteitstijd die moet worden gestart. | {id (string), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Object | Aantal buffer voor videokwaliteit | {id (string), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Object | Buffertijd videokwaliteit | {id (string), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Object | Aantal wijzigingen in videokwaliteit | {id (string), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Object | Gemiddelde bitsnelheid videokwaliteit | {id (string), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Object | Aantal fouten in videokwaliteit | {id (string), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress10` | `media.mediaTimed.progress10` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress25` | `media.mediaTimed.progress25` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress50` | `media.mediaTimed.progress50` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress75` | `media.mediaTimed.progress75` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress95` | `media.mediaTimed.progress95` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videoresume` | `media.mediaTimed.resumes` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videopausecount` | `media.mediaTimed.pauses` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | Object | <!-- MISSING --> | {id (string), value (number)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | integer |

{style="table-layout:auto"}

## Gekoppelde toewijzingsvelden

Deze velden hebben één bron, maar toewijzen aan **meerdere** XDM-locaties.

| Veld Analyse | XDM-veld | XDM-type | Beschrijving |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | integer | Numerieke id die de resolutie van de monitor vertegenwoordigt. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | string | Versie van mobiel besturingssysteem. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | integer | Lengte van video-advertentie. |

{style="table-layout:auto"}

## Gegenereerde toewijzingsvelden

Selecteer velden die afkomstig zijn van ADC moeten worden getransformeerd, waarbij logica buiten een directe kopie van Adobe Analytics moet worden gegenereerd in XDM.

| Veld Analyse | XDM-veld | XDM-type | Beschrijving |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Object | Props voor aangepaste analyse, geconfigureerd als lijsteigenschappen. Het bevat een lijst met gescheiden waarden. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Object | Wordt gebruikt door hiërarchievariabelen. Het bevat een lijst met gescheiden waarden. | {values (array), delimiter (tekenreeks)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Aangepaste analytische lijstvariabelen. Bevat een lijst met gescheiden waarden. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | integer | De kleurdiepte-id, die is gebaseerd op de waarde van de kolom c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | boolean | Een variabele die in de dimensie van de Steun van het Koekje wordt gebruikt. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Object | De standaard handelgebeurtenissen teweegbrachten op de slag. | {id (string), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Object | Aangepaste gebeurtenissen die worden geactiveerd tijdens de hit. | {id (Object), value (Object)} |
| `m_geo_country` | `placeContext.geo.countryCode` | string | Afkorting van het land waar de treffer vandaan kwam, dat van het OT is gebaseerd. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | getal | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | getal | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | boolean | Een vlag die aangeeft of Java™ is ingeschakeld. |
| `m_latitude` | `placeContext.geo._schema.latitude` | getal | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | getal | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | string | Een variabele die alleen wordt gebruikt in aanvragen voor het bijhouden van koppelingen. Deze variabele bevat de URL van de downloadkoppeling, de afsluitkoppeling of de aangepaste koppeling waarop is geklikt. |
| `m_page_event_var2` | `web.webInteraction.name` | string | Een variabele die alleen wordt gebruikt in aanvragen voor het bijhouden van koppelingen. Hier wordt de aangepaste naam van de koppeling weergegeven, als deze is opgegeven. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | boolean | Een variabele die wordt gebruikt om de pagina&#39;s te vullen die niet worden gevonden. Deze variabele moet leeg zijn of &quot;ErrorPage&quot; bevatten. |
| `m_pagename_no_url` | `web.webPageDetails.name` | getal | De naam van de pagina (indien ingesteld). Als er geen pagina is opgegeven, blijft deze waarde leeg. |
| `m_paid_search` | `search.isPaid` | boolean | Een vlag die wordt geplaatst als de treffer betaalde onderzoeksopsporing aanpast. |
| `m_product_list` | `productListItems[].items` | array | De productlijst, zoals die door de productvariabele wordt overgegaan. | {SKU (tekenreeks), quantity (geheel getal), priceTotal (getal)} |
| `m_ref_type` | `web.webReferrer.type` | string | Een numerieke id die het verwijzingstype voor de treffer vertegenwoordigt.<br/>`1`: In uw site<br/>`2`: Overige websites<br/>`3`: Zoekprogramma&#39;s<br/>`4`: Harde schijf<br/>`5`: USENET<br/>`6`: Typed/Bookmark (geen referentie)<br/>`7`: e-mail<br/>`8`: Geen JavaScript<br/>`9`: Sociale netwerken |
| `m_search_engine` | `search.searchEngine` | string | De numerieke id die staat voor het zoekprogramma waarmee de bezoeker naar uw site is doorverwezen. |
| `post_currency` | `commerce.order.currencyCode` | string | De valutacode die tijdens de transactie werd gebruikt. |
| `post_cust_hit_time_gmt` | `timestamp` | string | Dit wordt slechts gebruikt in timestamp-Toegelaten datasets. Dit is de tijdstempel die met de hit wordt verzonden, op basis van UNIX®-tijd. |
| `post_cust_visid` | `identityMap` | object | De bezoeker-id van de klant. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | boolean | De bezoeker-id van de klant. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | string | De bezoeker-id van de klant. |
| `post_visid_high` + `visid_low` | `identityMap` | object | Een unieke id voor een bezoek. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | string | Een unieke id voor een bezoek. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | boolean | Gebruikt met `visid_low` om een bezoek op unieke wijze te identificeren. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | string | Gebruikt met `visid_low` om een bezoek op unieke wijze te identificeren. |
| `post_visid_low` | `identityMap` | object | Gebruikt met visid_high om een bezoek uniek te identificeren. |
| `hit_time_gmt` | `receivedTimestamp` | string | De tijdstempel van de hit, gebaseerd op UNIX®-tijd. |
| `hitid_high` + `hitid_low` | `_id` | string | Een unieke id om een treffer te identificeren. |
| `hitid_low` | `_id` | string | Wordt gebruikt met hitid_high om een treffer op unieke wijze te identificeren. |
| `ip` | `environment.ipV4` | string | Het IP Adres, dat op de kopbal van HTTP van het beeldverzoek wordt gebaseerd. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | boolean | De gebruikte versie van JavaScript. |
| `mcvisid_high` + `mcvisid_low` | identityMap | object | De bezoeker-id van het Experience Cloud. |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | string | De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt soms gebruikt in naamruimten. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | boolean | De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt soms gebruikt in naamruimten. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | string | De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt soms gebruikt in naamruimten. |
| `mcvisid_low` | `identityMap` | object | De bezoeker-id van het Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | string | Id voor tikken. The analytics field sdid_high and sdid_low is the additional data id used to stitch two (or more) inkomend hits together. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | string | Bandennabijheid mobiele services. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | integer | De naam van het videohoofdstuk. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | integer | De lengte van de video. |

{style="table-layout:auto"}

## Geavanceerde toewijzingsvelden

Selecteer velden (ook wel &quot;postwaarden&quot; genoemd) die gegevens bevatten nadat de Adobe de waarden ervan heeft aangepast met de verwerkingsregels, de VISTA-regels en de opzoektabellen. De meeste postwaarden hebben een vooraf verwerkte tegenhanger. Uw organisatie kan beslissen of u het pre-verwerkte gebied, post-verwerkt gebied, of allebei wilt gebruiken.

Meer leren over het uitvoeren van deze transformaties gebruikend de Dienst van de Vraag, zie [Adobe-gedefinieerde functies](/help/query-service/sql/adobe-defined-functions.md) in de gebruikersgids van de Dienst van de Vraag.

| Veld Analyse | XDM-veld | XDM-type | Beschrijving |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | string | Aangepaste analytische variabelen. Elke organisatie kan eVars anders gebruiken. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | string | Aangepaste analytische voorkeuren. Elke organisatie kan eigen principes anders gebruiken. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | integer | De hoogte van de browser, in pixels. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | integer | De breedte van de browser, in pixels. |
| `post_campaign` | `marketing.trackingCode` | string | De variabele die wordt gebruikt in de dimensie Code bijhouden. |
| `post_channel` | `web.webPageDetails.siteSection` | string | De variabele die wordt gebruikt in de dimensie Site-secties. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | string | De aangepaste bezoeker-id, indien ingesteld. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | string | De URL van de eerste pagina die de bezoeker bereikt. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | string | Een variabele die wordt gebruikt in de oorspronkelijke dimensie van de Pagina van de Ingang. De paginanaam van de ingangspagina van de bezoeker. |
| `post_keywords` | `search.keywords` | string | De trefwoorden die voor de hit zijn verzameld. |
| `post_page_url` | `web.webPageDetails.URL` | string | De URL van de paginaklok. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | string | Gelijk aan 1 op treffers die een paginanaam hebben. Dit lijkt op de metrische weergave van Adobe Analytics-paginaweergaven. |
| `post_purchaseid` | `commerce.order.purchaseID` | string | Variabele die wordt gebruikt om aankopen uniek te identificeren. |
| `post_referrer` | `web.webReferrer.URL` | string | De URL van de vorige pagina. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | string | Staatvariabele. |
| `post_user_server` | `web.webPageDetails.server` | string | Een variabele die in de dimensie van de Server wordt gebruikt. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | string | Een variabele die wordt gebruikt om de dimensie van de Code van het PIT te bevolken. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | integer | De numerieke id van de browser. |
| `domain` | `environment.domain` | string | De variabele die wordt gebruikt in de dimensie Domein. Het is gebaseerd op Internet Service Provider (ISP) van de gebruiker. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | string | De eerste verwijzende URL voor de bezoeker. |
| `geo_city` | `placeContext.geo.city` | string | De naam van de stad van de hit. Dit is gebaseerd op het IP van de klap adres. |
| `geo_dma` | `placeContext.geo.dmaID` | integer | De numerieke id van het demografische gebied voor de hit. Dit is gebaseerd op het IP van de klap adres. |
| `geo_region` | `placeContext.geo.stateProvince` | string | De naam van de staat of regio van de treffer. Dit is gebaseerd op het IP van de klap adres. |
| `geo_zip` | `placeContext.geo.postalCode` | string | De postcode van de hit. Dit is gebaseerd op het IP van de klap adres. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | integer | De numerieke id die het besturingssysteem van de bezoeker vertegenwoordigt. Dit is gebaseerd op de user_agent kolom. |
| `search_page_num` | `search.pageDepth` | integer | Deze variabele wordt gebruikt door de Al dimensie van de Rang van de Pagina van het Onderzoek en wijst op welke pagina van onderzoeksresultaten uw plaats | is weergegeven voordat de gebruiker op uw site heeft geklikt. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | string | Een variabele die wordt gebruikt in de dimensie Trefwoorden zoeken. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | integer | Een variabele die wordt gebruikt in de dimensie Visit Number. Dit begint bij 1, en stijgt telkens als een nieuw bezoek (per gebruiker) begint. |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | integer | Een variabele die wordt gebruikt in de dimensie van de Diepte van het Actief. Deze waarde neemt toe met 1 voor elke hit die de gebruiker genereert en herstelt na elk bezoek. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | string | De eerste referentie van het bezoek. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | integer | De naam van de eerste pagina van het bezoek. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Object | Props voor aangepaste analyse, geconfigureerd als lijsteigenschappen. Het bevat een lijst met gescheiden waarden. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Object | Wordt gebruikt door hiërarchievariabelen en bevat een lijst met waarden die zijn gescheiden door scheidingstekens. | {values (array), delimiter (tekenreeks)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Een lijst met variabelewaarden. Bevat een lijst met gescheiden waarden, afhankelijk van de implementatie. | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | boolean | Variabele die in de dimensie van de Steun van het Koekje wordt gebruikt. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Object | De standaard handelgebeurtenissen teweegbrachten op de slag. | {id (string), value (number)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Object | Aangepaste gebeurtenissen die worden geactiveerd tijdens de hit. | {id (Object), value (Object)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | boolean | Een vlag die aangeeft of Java™ is ingeschakeld. |
| `post_latitude` | `placeContext.geo._schema.latitude` | getal | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | getal | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | string | Het type hit dat wordt verzonden in de afbeeldingsaanvraag (klik op Standaard, Koppeling downloaden, Koppeling afsluiten of Aangepaste koppeling). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | getal | Komt overeen met 1 als de hit een klik op de koppeling is. Dit is vergelijkbaar met de metrische waarde voor Pagina-gebeurtenissen in Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | string | Deze variabele wordt alleen gebruikt in aanvragen voor het bijhouden van koppelingen. Dit is de URL van de downloadkoppeling, de afsluitkoppeling of de aangepaste koppeling waarop is geklikt. |
| `post_page_event_var2` | `web.webInteraction.name` | string | Deze variabele wordt alleen gebruikt in aanvragen voor het bijhouden van koppelingen. Dit is de aangepaste naam van de koppeling. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | boolean | Dit wordt gebruikt om de pagina&#39;s te vullen die niet zijn gevonden. Deze variabele moet leeg zijn of &quot;ErrorPage&quot; bevatten |
| `post_pagename_no_url` | `web.webPageDetails.name` | getal | De naam van de pagina (indien ingesteld). Als er geen pagina is opgegeven, blijft deze waarde leeg. |
| `post_product_list` | `productListItems[].items` | array | De productlijst, zoals die door de productvariabele wordt overgegaan. | {SKU (tekenreeks), quantity (geheel getal), priceTotal (getal)} |
| `post_search_engine` | `search.searchEngine` | string | De numerieke id die staat voor het zoekprogramma waarmee de bezoeker naar uw site is doorverwezen. |
| `mvvar1_instances` | `.list.items[]` | Object | Lijst met variabelewaarden. Bevat een lijst met gescheiden waarden, afhankelijk van de implementatie. |
| `mvvar2_instances` | `.list.items[]` | Object | Lijst met variabelewaarden. Bevat een lijst met gescheiden waarden, afhankelijk van de implementatie. |
| `mvvar3_instances` | `.list.items[]` | Object | Lijst met variabelewaarden. Bevat een lijst met gescheiden waarden, afhankelijk van de implementatie. |
| `color` | `device.colorDepth` | integer | Kleurdiepte-id, gebaseerd op de waarde van de kolom c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | string | De numerieke id die het referentietype van de eerste referentie van de bezoeker vertegenwoordigt. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | integer | Tijdstempel van de eerste hit van de bezoeker in UNIX®-tijd. |
| `geo_country` | `placeContext.geo.countryCode` | string | Afkorting van het land waar de treffer vandaan kwam, op basis van IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | getal | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | getal | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | boolean | Een vlag die wordt geplaatst als de treffer betaalde onderzoeksopsporing aanpast. |
| `ref_type` | `web.webReferrer.type` | string | Een numerieke id die het verwijzingstype voor de treffer vertegenwoordigt. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | boolean | Een vlag (1=betaald, 0=niet betaald) die erop wijst of de eerste klap van het bezoek van een betaalde onderzoekshit was. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | string | Numerieke id die het referentietype van de eerste referentie van het bezoek vertegenwoordigt. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | string | Numerieke id van de eerste zoekfunctie van het bezoek. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | integer | Tijdstempel van de eerste hit van het bezoek in UNIX®-tijd. |

{style="table-layout:auto"}