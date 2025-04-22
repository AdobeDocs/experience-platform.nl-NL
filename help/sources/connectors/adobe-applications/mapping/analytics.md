---
title: Toewijzingsvelden voor de Adobe Analytics Source Connector
description: Wijs Adobe Analytics-velden toe aan XDM-velden met behulp van de Analytics Source Connector.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 316879afe8c94657156c768cdc14d4710da9fd35
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 0%

---

# Toewijzingen van analytische velden

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de bron Analytics. Sommige gegevens die via ADC worden ingevoerd, kunnen rechtstreeks van de gebieden van Analytics aan de gebieden van het Gegevensmodel van de Ervaring worden in kaart gebracht (XDM), terwijl andere gegevens transformaties en specifieke functies vereisen om met succes worden in kaart gebracht.

![ een illustratie van de gegevenstransport van Adobe Analytics van Analytics aan Experience Platform.](../images/analytics-data-experience-platform.png)

## Streaming media-parameters

Lees de volgende tabel voor informatie over streamingmedia-parameters.

| Gegevensfeed | XDM-veldpad | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | string | De vriendelijke (leesbare) naam van de video. |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | string | De naam van de auteur van de media. |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | string | De naam van de albumartiest of groep die de muziekopname of video uitvoert. |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | string | De naam van het album waartoe de muziekopname of video behoort. |
| `videolength` | `mediaReporting.sessionDetails.length ` | integer | De lengte of runtime van de video. |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | string |
| `video` | `mediaReporting.sessionDetails.name` | string | De id van de video. |
| `videoshow` | `mediaReporting.sessionDetails.show` | string | De naam van het programma of de serie. De naam van het programma/de serie is slechts vereist als de show deel van een reeks uitmaakt. |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | string | Het type streamingmedia zoals &quot;video&quot; of &quot;audio&quot;. |
| `videoseason` | `mediaReporting.sessionDetails.season` | string | Het seizoensnummer waartoe de show behoort. Deze waarde is alleen vereist als de presentatie onderdeel is van een reeks. |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | string | The number of the episode. |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | string[] | Het genre van de video. |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | string | Een id voor een instantie van een inhoudsstroom die uniek is voor een individuele playback. |
| `videoplayername` | `mediaReporting.sessionDetails.playerName ` | string | De naam van de videospeler. |
| `videochannel` | `mediaReporting.sessionDetails.channel` | string | Het distributiekanaal van waar de inhoud werd gespeeld. |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | string | Het type van stroomlevering dat voor de inhoud wordt gebruikt. Deze wordt automatisch ingesteld op &quot;Video&quot; voor alle videoweergaven. Aanbevolen waarden zijn: VOD, Live, Lineair, UGC, DVOD, Radio, Podcast, Audiobook en Song. |
| `videonetwork` | `mediaReporting.sessionDetails.network` | string | De netwerk- of kanaalnaam. |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | string | Het type diervoeder. Dit kan werkelijke gegevens met betrekking tot diervoeders vertegenwoordigen, zoals &quot;East HD&quot; of &quot;SD&quot;, of de bron van de feed, zoals een URL. |
| `videosegment` | `mediaReporting.sessionDetails.segment` | string |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | boolean | Een Booleaanse waarde die aangeeft of de video is gestart of niet. Dit gebeurt wanneer de gebruiker de afspeelknop selecteert en ook wordt geteld wanneer er pre-roladvertenties, buffering, fouten enzovoort zijn. |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | boolean | Een booleaanse waarde die aangeeft of het eerste frame van het medium is gestart. Als de gebruiker tijdens om het even welke advertenties of buffertijd daalt, dan zou &quot;inhoudstart&quot;niet kwalificeren. |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | integer | De duur (in seconden) voor alle gebeurtenissen van `type=PLAY` op de hoofdinhoud. |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | boolean | Een booleaanse waarde die aangeeft of een getimede media-element is gecontroleerd op voltooiing. Deze waarde betekent niet noodzakelijkerwijs dat de viewer de gehele video heeft bekeken omdat deze waarde niet verantwoordelijk is voor de viewer die mogelijk vooruitgaat. |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | integer | De totale hoeveelheid tijd die een gebruiker aan een bepaald getimed media middel, met inbegrip van tijd besteedt het letten van advertenties besteedt. |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | integer | De som van de unieke intervallen die een gebruiker op een getimed media-element ziet. Met andere woorden, de lengte van meermaals bekeken afspeelintervallen wordt slechts één keer geteld. |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | getal | De gemiddelde inhoudstijd die voor een specifiek media punt wordt doorgebracht. Met andere woorden, de totale tijd van de inhoud gedeeld door de lengte voor alle playbackzittingen. |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | boolean | Een booleaanse waarde die aangeeft of de afspeelkop van een bepaalde video de 10%-markering van de totale videolengte heeft bereikt. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | boolean | Een booleaanse waarde die aangeeft of de afspeelkop van een bepaalde video de 25%-markering van de totale videolengte heeft bereikt. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | boolean | Een booleaanse waarde die aangeeft of de afspeelkop van een bepaalde video de 50%-markering van de totale videolengte heeft bereikt. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | boolean | Een booleaanse waarde die aangeeft of de afspeelkop van een bepaalde video de 75%-markering van de totale videolengte heeft bereikt. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | boolean | Een booleaanse waarde die aangeeft of de afspeelkop van een bepaalde video de 95%-markering van de totale videolengte heeft bereikt. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | boolean | Een booleaanse waarde die aangeeft of een of meer pauzes zijn opgetreden tijdens het afspelen van één media-item. |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | integer | Het aantal pauzeperioden dat tijdens het afspelen is opgetreden. |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | integer | De totale duur (in seconden) waarin het afspelen door een gebruiker is gepauzeerd. |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | string | Een MVPD-id die is opgegeven via Adobe-verificatie. |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | string | Definieert dat de gebruiker via Adobe-verificatie is geautoriseerd. |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | Hiermee bepaalt u de tijd van de dag waarop de inhoud werd uitgezonden of afgespeeld. |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | boolean | Een booleaanse waarde die elke playback markeert die na meer dan 30 minuten van buffer, pauze, of een stallperiode werd hervat. |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | boolean | Een Booleaanse waarde die aangeeft dat ten minste één frame is weergegeven. Dit frame hoeft niet het eerste frame te zijn. |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | string | De naam van het recordlabel. |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | string | Het radiostation of de naam waarop de audio wordt afgespeeld. |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | string | De naam van de uitgever van de audio-inhoud. |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | getal | Geeft de hoeveelheid tijd (in seconden) aan die is verstreken tussen de laatst bekende interactie van een gebruiker en het moment waarop de sessie werd gesloten. |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | string | Het type geladen advertentie zoals gedefinieerd door uw eigen interne representatie. |

{style="table-layout:auto"}

## Advertising-parameters

Lees de volgende tabel voor informatie over advertentieparameters.

| Gegevensfeed | XDM-veldpad | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | string | De naam van de advertentie. In de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de eVar. |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | integer | De index van de advertentie binnen het bovenliggende element en het begin. De eerste advertentie heeft bijvoorbeeld index 0 en de tweede advertentie heeft index 1. |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | integer | De lengte van de video en, gemeten in seconden. |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | string | De naam van de speler die wordt gebruikt om de advertentie te renderen. |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | string | De id van het advertentieeinde. |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | string | De vriendelijke (leesbare) naam van het advertentiespoor. |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | string | De onderneming of het merk waarvan het product in de advertentie wordt vermeld. |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | string | De id van de advertentiecampagne. |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | boolean | Een booleaanse waarde die aangeeft of de advertentie is gestart of niet. |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | boolean | Een booleaanse waarde die aangeeft of de bewerking is voltooid of niet. |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | integer | De totale hoeveelheid tijd, gemeten in seconden, die besteed het letten op de advertentie. |

{style="table-layout:auto"}

## Hoofdstukparameters

Lees de volgende lijst voor informatie over hoofdstukparameters.

| Gegevensfeed | XDM-veldpad | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | string | De automatisch gegenereerde id van het hoofdstuk. |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | boolean | Een booleaanse waarde die aangeeft of het hoofdstuk is gestart of niet. |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | boolean | Een booleaanse waarde die aangeeft of het hoofdstuk is voltooid. |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | integer | De tijd, in seconden wordt gemeten, besteed aan het hoofdstuk. |

{style="table-layout:auto"}

## Parameters van de Player-status

Lees de volgende tabel voor informatie over de parameters van de spelerstatus.

| Gegevensfeed | XDM-veldpad | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | boolean | Een booleaanse waarde die aangeeft of de videostatus is ingesteld op volledig scherm. |
| `videostatefullscreencount` | `mediaReporting.states[].count` | integer | Het aantal keren dat een videostaat aan het volledige scherm werd geplaatst. |
| `videostatefullscreentime` | `mediaReporting.states[].time` | integer | De totale duur van het moment waarop de videostatus is ingesteld op volledig scherm. |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | boolean | Een booleaanse waarde die aangeeft of ondertiteling is ingeschakeld. |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | integer | Het aantal keren dat ondertiteling gesloten werd toegelaten. |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | integer | De totale duur van het moment waarop ondertiteling is ingeschakeld. |
| `videostatemute` | `mediaReporting.states[].isSet` | boolean | Een booleaanse waarde die aangeeft of de videostatus is ingesteld op dempen. |
| `videostatemutecount` | `mediaReporting.states[].count` | integer | Het aantal keren dat een video is gedempt. |
| `videostatemutetime` | `mediaReporting.states[].time` | integer | De totale duur van de video in demte. |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | boolean | Een booleaanse waarde die aangeeft of de beeld-in-beeldmodus is ingeschakeld. |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | integer | Het aantal keren dat de beeld-in-beeld modus is ingeschakeld. |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | integer | De totale duur van het inschakelen van de beeld-in-beeldmodus. |
| `videostateinfocus` | `mediaReporting.states[].isSet` | boolean | Een booleaanse waarde die aangeeft of de focusmodus is ingeschakeld |
| `videostateinfocuscount` | `mediaReporting.states[].count` | integer | Het aantal keren dat de modus In beeld is ingeschakeld. |
| `videostateinfocustime` | `mediaReporting.states[].time` | integer | De totale duur van het inschakelen van de focusmodus. |

{style="table-layout:auto"}

## Parameters voor kwaliteit

Lees de volgende tabel voor informatie over kwaliteitsparameters.

| Gegevensfeed | XDM-veldpad | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | getal | De gemiddelde bitsnelheid (in kbps, geheel getal). Deze metrische waarde wordt berekend als gewogen gemiddelde van alle bitsnelheidwaarden met betrekking tot de afspeelduur die tijdens een afspeelsessie plaatsvond. |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | boolean | Een Booleaanse waarde die het aantal streams aangeeft waarin wijzigingen in de bitsnelheid zijn opgetreden. Deze metrische waarde wordt alleen op true ingesteld als tijdens een afspeelsessie ten minste één gebeurtenis voor het wijzigen van de bitsnelheid heeft plaatsgevonden. |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | integer |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | string | Het aantal wijzigingen in bitsnelheid. Deze waarde wordt berekend als de som van alle gebeurtenissen die zich tijdens een afspeelsessie hebben voorgedaan om de bitsnelheid te wijzigen. |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | integer | De duur, gemeten in seconden, die tussen videolading en videobegin ging. |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | boolean | Een Booleaanse waarde die het aantal streams aangeeft waarin frames zijn neergezet. Deze metrische waarde wordt alleen op true ingesteld als tijdens een afspeelsessie ten minste één frame is verwijderd. |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | integer | Het aantal frames dat wordt gedropt tijdens het afspelen van de hoofdinhoud. |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | integer | Het aantal buffergebeurtenissen. Deze metrische waarde wordt berekend als een telling van de verschillende bufferstaten die tijdens een playbackzitting voorkwamen. Dit is een telling van hoeveel keer de speler in een bufferstaat van andere staten, zoals het spelen of het pauzeren ingaat. |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | integer | De totale hoeveelheid tijd, die in seconden wordt gemeten, bestede het bufferen. Deze waarde wordt berekend als de som van alle buffergebeurtenissen tijdens een afspeelsessie. |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | boolean | Een Booleaanse waarde die het aantal streams aangeeft dat wordt beïnvloed door buffering. Deze metrische waarde wordt alleen op true ingesteld als tijdens een afspeelsessie ten minste één buffergebeurtenis heeft plaatsgevonden. |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | boolean | Een Booleaanse waarde die het aantal streams aangeeft waarin een foutgebeurtenis heeft plaatsgevonden. Bijvoorbeeld, als trackError tijdens de playbackzitting werd geroepen, en een type=error hartslagvraag werd geproduceerd. Deze metrische waarde wordt alleen op true ingesteld als er ten minste één fout is opgetreden tijdens het afspelen. |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | integer | Het aantal fouten dat is opgetreden. Deze waarde wordt berekend als de som van alle foutgebeurtenissen die tijdens een afspeelsessie zijn opgetreden. |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | array van tekenreeks | De unieke fout-id&#39;s die worden gegenereerd door de speler SDK. U moet de foutcodes of id&#39;s tijdens de implementatie opgeven via opgegeven fout-API&#39;s. |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | array van tekenreeks | De unieke fout-id&#39;s van externe bronnen, zoals CDN-fouten. U moet de foutcodes of id&#39;s tijdens de implementatie opgeven via opgegeven fout-API&#39;s. |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | boolean | De unieke fout-id&#39;s die tijdens het afspelen door Media SDK worden gegenereerd. |

{style="table-layout:auto"}

## Verouderde velden

Lees deze sectie voor informatie over verouderde analytische toewijzingsvelden.

### Directe toewijzingsvelden

+++Selecteren om een afgekeurde direct-toewijzingsvelden weer te geven

| Gegevensfeed | XDM-veld | XDM-type | Beschrijving |
| --- | --- | --- | --- |
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
| `mobileappid` | `application.name` | string | De mobiele toepassings-id, opgeslagen in de volgende indeling: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | string | De naam van het mobiele apparaat. In iOS wordt de notatie opgeslagen als een door komma&#39;s gescheiden tekenreeks van 2 cijfers. Het eerste getal vertegenwoordigt de apparaatgeneratie en het tweede getal vertegenwoordigt de apparaatfamilie. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | string | Wordt gebruikt door mobiele services. Vertegenwoordigt het aandachtspunt. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | getal | Wordt gebruikt door mobiele services. Geeft de afstand van het punt van de belangstelling aan. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | getal | Verzameld van de contextgegevensvariabele a.loc.acc. Geeft de nauwkeurigheid van de GPS in meters aan op het moment van verzameling. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | string | Verzameld van de contextgegevensvariabele a.loc.category. Beschrijft de categorie van een specifieke plaats. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | string | Verzameld van de contextgegevensvariabele a.loc.id. Identificatiecode voor een bepaald aandachtspunt. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | string | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | getal | Belangrijkste baken voor mobiele services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | getal | Beacon minor mobiele diensten. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | string | Mobile Services-baken UUID. |
| `mobileinstalls` | `application.firstLaunches` | Object | Dit wordt geactiveerd bij de eerste uitvoering na installatie of herinstallatie | {id (string), value (number)} |
| `mobileupgrades` | `application.upgrades` | Object | Meldt het aantal upgrades van de app. Triggers bij de eerste looppas na verbetering of om het even welk ogenblik verandert het versieaantal. | {id (string), value (number)} |
| `mobilelaunches` | `application.launches` | Object | Het aantal keren dat de app is gestart. | {id (string), value (number)} |
| `mobilecrashes` | `application.crashes` | Object |  | {id (string), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Object |  | {id (string), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Object | | {id (string), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Object | | {id (string), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Object | De videokwaliteitstijd die moet worden gestart. | {id (string), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Object | | {id (string), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Object | Aantal buffer voor videokwaliteit | {id (string), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Object | Buffertijd videokwaliteit | {id (string), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Object | Aantal wijzigingen in videokwaliteit | {id (string), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Object | Gemiddelde bitsnelheid videokwaliteit | {id (string), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Object | Aantal fouten in videokwaliteit | {id (string), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Object | | {id (string), value (number)} |

{style="table-layout:auto"}

+++

## Gegenereerde toewijzingsvelden

Selecteer velden die afkomstig zijn van ADC moeten worden getransformeerd, waarbij logica buiten een directe kopie van Adobe Analytics moet worden gegenereerd in XDM.

+++Selecteren om een lijst met afgekeurde gegenereerde toewijzingsvelden weer te geven

| Gegevensfeed | XDM-veld | XDM-type | Beschrijving |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Object | Props voor aangepaste analyse, geconfigureerd als lijsteigenschappen. Het bevat een lijst met gescheiden waarden. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Object | Wordt gebruikt door hiërarchievariabelen. Het bevat een lijst met gescheiden waarden. | {values (array), delimiter (tekenreeks)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Aangepaste analytische lijstvariabelen. Bevat een lijst met gescheiden waarden. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | integer | De kleurdiepte-id, die is gebaseerd op de waarde van de kolom c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | boolean | Een variabele die in de dimensie van de Steun van het Koekje wordt gebruikt. |
| `m_event_list` | `commerce.purchases`, <br/>`commerce.productViews`, <br/>`commerce.productListOpens`, <br/>`commerce.checkouts`, <br/>`commerce.productListAdds`, <br/>`commerce.productListRemovals`, <br/>`commerce.productListViews` | Object | De standaard handelgebeurtenissen teweegbrachten op de slag. | {id (string), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Object | Aangepaste gebeurtenissen die worden geactiveerd tijdens de hit. | {id (Object), value (Object)} |
| `m_geo_country` | `placeContext.geo.countryCode` | string | Afkorting van het land waar de treffer vandaan kwam, dat van het OT is gebaseerd. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | getal | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | getal | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | boolean | Een vlag die aangeeft of Java™ is ingeschakeld. |
| `m_latitude` | `placeContext.geo._schema.latitude` | getal | |
| `m_longitude` | `placeContext.geo._schema.longitude` | getal | |
| `m_page_event_var1` | `web.webInteraction.URL` | string | Een variabele die alleen wordt gebruikt in aanvragen voor het bijhouden van koppelingen. Deze variabele bevat de URL van de downloadkoppeling, de afsluitkoppeling of de aangepaste koppeling waarop is geklikt. |
| `m_page_event_var2` | `web.webInteraction.name` | string | Een variabele die alleen wordt gebruikt in aanvragen voor het bijhouden van koppelingen. Hier wordt de aangepaste naam van de koppeling weergegeven, als deze is opgegeven. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | boolean | Een variabele die wordt gebruikt om de pagina&#39;s te vullen die niet worden gevonden. Deze variabele moet leeg zijn of &quot;ErrorPage&quot; bevatten. |
| `m_pagename_no_url` | `web.webPageDetails.name` | getal | De naam van de pagina (indien ingesteld). Als er geen pagina is opgegeven, blijft deze waarde leeg. |
| `m_paid_search` | `search.isPaid` | boolean | Een vlag die wordt geplaatst als de treffer betaalde onderzoeksopsporing aanpast. |
| `m_product_list` | `productListItems[].items` | array | De productlijst, zoals die door de productvariabele wordt overgegaan. | {SKU (tekenreeks), quantity (geheel getal), priceTotal (getal)} |
| `m_ref_type` | `web.webReferrer.type` | string | Een numerieke id die het verwijzingstype voor de treffer vertegenwoordigt.<br/>`1`: Binnen uw plaats <br/>`2`: Andere websites <br/>`3`: de motoren van het onderzoek <br/>`4`: Harde aandrijving <br/>`5`: USENET <br/>`6`: Typed/Bladwijzer (geen verwijzer) <br/>`7`: E-mail <br/>`8`: Geen JavaScript <br/>`9`: Sociale Netwerken |
| `m_search_engine` | `search.searchEngine` | string | De numerieke id die staat voor het zoekprogramma waarmee de bezoeker naar uw site is doorverwezen. |
| `post_currency` | `commerce.order.currencyCode` | string | De valutacode die tijdens de transactie werd gebruikt. |
| `post_cust_hit_time_gmt` | `timestamp` | string | Dit wordt slechts gebruikt in timestamp-Toegelaten datasets. Dit is de tijdstempel die met de hit wordt verzonden, op basis van UNIX®-tijd. |
| `post_cust_visid` | `identityMap` | object | De bezoeker-id van de klant. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | boolean | De bezoeker-id van de klant. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | string | De bezoeker-id van de klant. |
| `post_visid_high` + `visid_low` | `identityMap` | object | Een unieke id voor een bezoek. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | string | Een unieke id voor een bezoek. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | boolean | Wordt samen met `visid_low` gebruikt om een bezoek op unieke wijze te identificeren. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | string | Wordt samen met `visid_low` gebruikt om een bezoek op unieke wijze te identificeren. |
| `post_visid_low` | `identityMap` | object | Gebruikt met visid_high om een bezoek uniek te identificeren. |
| `hit_time_gmt` | `receivedTimestamp` | string | De tijdstempel van de hit, gebaseerd op UNIX®-tijd. |
| `hitid_high` + `hitid_low` | `_id` | string | Een unieke id om een treffer te identificeren. |
| `hitid_low` | `_id` | string | Wordt gebruikt met hitid_high om een treffer op unieke wijze te identificeren. |
| `ip` | `environment.ipV4` | string | Het IP Adres, dat op de kopbal van HTTP van het beeldverzoek wordt gebaseerd. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | boolean | De gebruikte versie van JavaScript. |
| `mcvisid_high` + `mcvisid_low` | identityMap | object | De Experience Cloud-bezoeker-id. |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | string | De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt soms gebruikt in naamruimten. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | boolean | De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt soms gebruikt in naamruimten. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | string | De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt soms gebruikt in naamruimten. |
| `mcvisid_low` | `identityMap` | object | De Experience Cloud-bezoeker-id. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | string | Id voor tikken. The analytics field sdid_high and sdid_low is the additional data id used to stitch two (or more) inkomend hits together. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | string | Bandennabijheid mobiele services. |

{style="table-layout:auto"}

+++

## Gekoppelde toewijzingsvelden

Deze gebieden hebben één enkele bron, maar kaart aan **veelvoudige** plaatsen XDM.

+++Selecteren om een afgekeurde gesplitste toewijzingsvelden weer te geven

| Gegevensfeed | XDM-veld | XDM-type | Beschrijving |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`, <br/>`device.screenHeight` | integer | Numerieke id die de resolutie van de monitor vertegenwoordigt. |
| `mobileosversion` | `environment.operatingSystem`, <br/>`environment.operatingSystemVersion` | string | Versie van mobiel besturingssysteem. |

{style="table-layout:auto"}

+++

## Geavanceerde toewijzingsvelden

Selecteer velden (ook wel &quot;postwaarden&quot; genoemd) die gegevens bevatten nadat Adobe de waarden ervan heeft aangepast met de verwerkingsregels, de VISTA-regels en de opzoektabellen. De meeste postwaarden hebben een vooraf verwerkte tegenhanger.

De bronschakelaar van de Analyse verzendt pre-verwerkte gegevens naar een dataset in Experience Platform. U kunt deze gegevens met transformaties omzetten in de nabewerkte tegenhanger. Meer leren over het uitvoeren van deze transformaties gebruikend de Dienst van de Vraag, zie [ Adobe-bepaalde functies ](/help/query-service/sql/adobe-defined-functions.md) in de de gebruikersgids van de Dienst van de Vraag.

Meer leren over het uitvoeren van deze transformaties gebruikend de Dienst van de Vraag, zie [ Adobe-bepaalde functies ](/help/query-service/sql/adobe-defined-functions.md) in de de gebruikersgids van de Dienst van de Vraag.

+++Selecteren om een afgekeurde geavanceerde toewijzingsvelden weer te geven

| Gegevensfeed | XDM-veld | XDM-type | Beschrijving |
| — | — | — | — ||
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
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | string |  Staatvariabele. |
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
| `post_event_list` | `commerce.purchases`, <br/>`commerce.productViews`, <br/>`commerce.productListOpens`, <br/>`commerce.checkouts`, <br/>`commerce.productListAdds`, <br/>`commerce.productListRemovals`, <br/>`commerce.productListViews` | Object | De standaard handelgebeurtenissen teweegbrachten op de slag. | {id (string), value (number)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Object | Aangepaste gebeurtenissen die worden geactiveerd tijdens de hit.| {id (Object), value (Object)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | boolean | Een vlag die aangeeft of Java™ is ingeschakeld. |
| `post_latitude` | `placeContext.geo._schema.latitude` | getal |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | getal |   |
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
| `geo_latitude` | `placeContext.geo._schema.latitude` | getal |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | getal |  |
| `paid_search` | `search.isPaid` | boolean | Een vlag die wordt geplaatst als de treffer betaalde onderzoeksopsporing aanpast. |
| `ref_type` | `web.webReferrer.type` | string | Een numerieke id die het verwijzingstype voor de treffer vertegenwoordigt. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | boolean | Een vlag (1=betaald, 0=niet betaald) die erop wijst of de eerste klap van het bezoek van een betaalde onderzoekshit was. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | string | Numerieke id die het referentietype van de eerste referentie van het bezoek vertegenwoordigt. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | string | Numerieke id van de eerste zoekfunctie van het bezoek. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | integer | Tijdstempel van de eerste hit van het bezoek in UNIX®-tijd. |

+++