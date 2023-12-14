---
title: Gegevenstype Gegevens sessie
description: Meer informatie over het gegevenstype Sessiedetails Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# [!UICONTROL Session Details Information] gegevenstype

[!UICONTROL Session Details Information] is een standaard XDM-gegevenstype (Experience Data Model) dat gegevens bijhoudt die betrekking hebben op mediaflaysessies. Het schema omvat een breed scala aan eigenschappen die inzicht verschaffen in de manier waarop media-inhoud wordt verbruikt. Gebruik de [!UICONTROL Session Details Information] gegevenstype om de betrokkenheid van de gebruiker vast te leggen door afspeelgebeurtenissen, interacties, voortgangsmarkeringen, pauzes en andere metriek te registreren. Dit biedt waardevolle inzichten in het gedrag van gebruikers en het consumptiepatroon van inhoud.

+++Select om een diagram van het gegevenstype van de Informatie van de Details van de Zitting te tonen.
![Een diagram van het gegevenstype Sessiedetails.](../images/data-types/session-details-information.png)
+++

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Media Session ID] | `ID` | string | De [!UICONTROL Media Session ID] identificeert een instantie van een inhoudsstroom uniek aan een individuele playback. |
| [!UICONTROL Content ID] | `name` | string | **Vereist** De [!UICONTROL Content ID] is een unieke id van de inhoud. Het kan worden gebruikt om terug naar andere industrie of CMS IDs te verbinden. |
| [!UICONTROL Content Name] | `friendlyName` | String | De [!UICONTROL Content Name] is de &quot;vriendelijke&quot; (leesbare) naam van de inhoud. |
| [!UICONTROL Media Content Length] | `length` | Geheel | **Vereist** De [!UICONTROL Media Content Length] Bevat de lengte van de clip/runtime. Dit is de maximale lengte (of duur) van de inhoud die wordt gebruikt (in seconden). |
| [!UICONTROL Broadcast Content Type] | `contentType` | String | **Vereist** De [!UICONTROL Broadcast Content Type] van de levering van de stream. Beschikbare waarden per [!UICONTROL Stream Type] omvatten:<br>Audio: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; en &quot;radio&quot;;<br>Video: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; en &quot;DVoD&quot;.<br>Klanten kunnen aangepaste waarden voor deze parameter opgeven. |
| [!UICONTROL Content Player Name] | `playerName` | String | **Vereist** De naam van de inhoudsspeler. |
| [!UICONTROL Content Channel] | `channel` | String | **Vereist** De [!UICONTROL Content Channel] Dit is het distributiekanaal van waaruit de inhoud is afgespeeld. |
| [!UICONTROL Version] | `appVersion` | String | De SDK-versie die door de speler wordt gebruikt. Dit kan elke aangepaste waarde hebben die voor uw speler zinnig is. |
| [!UICONTROL Series Name] | `show` | String | The Program/Series Name. De Naam van het Programma wordt vereist slechts als de show deel van een reeks uitmaakt. |
| [!UICONTROL Season Number] | `season` | String | De [!UICONTROL Season Number] dat de show tot behoort. Reeks seizoen is alleen vereist als de presentatie deel uitmaakt van een reeks. |
| [!UICONTROL Episode Number] | `episode` | String | The number of the episode. |
| [!UICONTROL Asset ID] | `assetID` | String | De [!UICONTROL Asset ID] is de unieke id voor de inhoud van het media-element, zoals de aflevering-id van de tv-reeks, de id van het filmelement of de livegebeurtenis. Deze id&#39;s zijn doorgaans afgeleid van metagegevensautoriteiten zoals EIDR, TMS/Gracenote of Rovi. Deze id&#39;s kunnen ook afkomstig zijn van andere bedrijfseigen of interne systemen. |
| [!UICONTROL Genre] | `genre` | String | Het type of de groep inhoud zoals gedefinieerd door de inhoudsproducent. Waarden moeten door komma&#39;s worden gescheiden in een variabele implementatie. |
| [!UICONTROL First Air Date] | `firstAirDate` | String | De datum waarop de inhoud voor het eerst op de televisie is uitgezonden. Elke datumnotatie is acceptabel, maar de Adobe beveelt aan: JJJJ-MM-DD. |
| [!UICONTROL First Digital Date] | `firstDigitalDate` | String | De datum waarop de inhoud voor het eerst via een digitaal kanaal of platform is verzonden. Elke datumnotatie is acceptabel, maar de Adobe raadt aan: JJJ-MM-DD. |
| [!UICONTROL Rating Value] | `rating` | String | De rating zoals gedefinieerd in de TV Parental Guidelines. |
| [!UICONTROL  Creator Name] | `originator` | String | De naam van de maker van de inhoud. |
| [!UICONTROL Broadcast Network] | `network` | String | De netwerk-/kanaalnaam. |
| [!UICONTROL Show Type] | `showType` | String | Het type inhoud, bijvoorbeeld trailer of volledige aflevering. |
| [!UICONTROL Ad Load Type] | `adLoad` | String | Het type advertentie dat wordt geladen zoals gedefinieerd door de interne representatie van elke klant. |
| [!UICONTROL MVPD Identifier] | `mvpd` | String | De [!UICONTROL MVPD Identifier] die via verificatie van de Adobe is verstrekt. |
| [!UICONTROL Media Authorized] | `authorized` | String | Bevestigt of de gebruiker via de authentificatie van de Adobe is toegelaten. |
| [!UICONTROL Day Part] | `dayPart` | String | A property that define the time of the day when the content was broadcast or play. Dit zou om het even welke waarde kunnen hebben die zonodig door klanten wordt geplaatst |
| [!UICONTROL Feed Type] | `feed` | String | Het type feed, dat ofwel werkelijke feed-gerelateerde gegevens zoals EAST HD of SD kan vertegenwoordigen, ofwel de bron van de feed zoals een URL. |
| [!UICONTROL Stream Format] | `streamFormat` | String | De indeling van de stream (HD, SD). |
| [!UICONTROL Resume] | `hasResume` | Boolean | Markeert elke playback die na meer dan 30 minuten van buffer, pauze, of stallatieperiode werd hervat. |
| [!UICONTROL Stream Type] | `streamType` | String | Het type van de mediastream. |
| [!UICONTROL Artist] | `artist` | String | De naam van de albumartiest of groep die de muziekopname of video uitvoert. |
| [!UICONTROL Album] | `album` | String | De naam van het album waartoe de muziekopname of video behoort. |
| [!UICONTROL Record Label] | `label` | String | De naam van het recordlabel. |
| [!UICONTROL Author] | `author` | String | De naam van de auteur van de media. |
| [!UICONTROL Radio Station] | `station` | String | De naam van het radiostation waarop de audio wordt afgespeeld. |
| [!UICONTROL Publisher] | `publisher` | String | De naam van de uitgever van de audio-inhoud. |
| [!UICONTROL Video Segment] | `segment` | String | Het interval dat het gedeelte van de inhoud beschrijft dat in minuten is bekeken. |
| [!UICONTROL Media Downloaded Flag] | `isDownloaded` | Boolean | De stream werd lokaal op het apparaat afgespeeld nadat deze was gedownload. |
| [!UICONTROL Federated Data] | `isFederated` | Boolean | [!UICONTROL Federated Data] wordt geplaatst aan waar wanneer de slag wordt gefederaliseerd (namelijk ontvangen door de klant als deel van een gefedereerd gegevensaandeel, eerder dan hun eigen implementatie). |
| [!UICONTROL Media Starts] | `isViewed` | Boolean | De gebeurtenis load voor de media. Dit gebeurt wanneer de viewer de afspeelknop selecteert. Dit telt zelfs als er pre-roladvertenties, het bufferen, fouten, etc. zijn. |
| [!UICONTROL Content Starts] | `isPlayed` | Boolean | [!UICONTROL Content Starts] wordt waar wanneer het eerste frame van media wordt verbruikt. Als de gebruiker tijdens een advertentie valt, buffert, enzovoort, is er geen [!UICONTROL Content Starts] gebeurtenis. |
| [!UICONTROL Content Completes] | `isCompleted` | Boolean | [!UICONTROL Content Completes] Hiermee wordt aangegeven of een getimede media-element is gecontroleerd op voltooiing. Deze gebeurtenis betekent niet noodzakelijkerwijs dat de viewer de hele video heeft bekeken. De viewer heeft mogelijk een voorsprong overgeslagen. |
| [!UICONTROL Content Time Spent] | `timePlayed` | Geheel | [!UICONTROL Content Time Spent] Hiermee wordt de gebeurtenisduur (in seconden) voor alle gebeurtenissen van het type PLAY op de hoofdinhoud samengevat. |
| [!UICONTROL Media Time Spent] | `totalTimePlayed` | Geheel | Beschrijft de totale hoeveelheid tijd die door een gebruiker aan een specifiek getimed media middel wordt doorgebracht, dat besteedde tijd het letten op advertenties omvat. |
| [!UICONTROL Unique Time Played] | `uniqueTimePlayed` | Geheel | Beschrijft de som unieke intervallen die door een gebruiker op een getimed media element worden gezien - namelijk de intervallen van de lengteplayback die veelvoudige tijden worden bekeken slechts eenmaal worden geteld. |
| [!UICONTROL Average Minute Audience] | `averageMinuteAudience` | Getal | Beschrijft de gemiddelde inhoudstijd die voor een specifiek media punt wordt doorgebracht - namelijk de totale inhoudstijd die door de lengte van alle playbackzittingen wordt verdeeld. |
| [!UICONTROL Ad Count] | `adCount` | Geheel | Het aantal advertenties dat tijdens het afspelen is gestart. |
| [!UICONTROL Chapter Count] | `chapterCount` | Geheel | Het aantal hoofdstukken dat tijdens het afspelen is gestart. |
| [!UICONTROL 10% Progress Marker] | `hasProgress10` | Boolean | Geeft aan dat de afspeelkop de 10% markering van het medium heeft doorgegeven op basis van de lengte van de stream. De markering wordt slechts eenmaal geteld, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| [!UICONTROL 25% Progress Marker] | `hasProgress25` | Boolean | Geeft aan dat de afspeelkop de 25% markering van media heeft doorgegeven op basis van de streamlengte. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| [!UICONTROL 50% Progress Marker] | `hasProgress50` | Boolean | Geeft aan dat de afspeelkop de 50% markering van media heeft doorgegeven op basis van de streamlengte. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| [!UICONTROL 75% Progress Marker] | `hasProgress75` | Boolean | Geeft aan dat de afspeelkop de 75%-markering voor media heeft doorgegeven op basis van de lengte van de stream. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| [!UICONTROL 95% Progress Marker] | `hasProgress95` | Boolean | Geeft aan dat de afspeelkop de 95%-markering van media heeft doorgegeven op basis van de streamlengte. Markering telde maar één keer, zelfs als u achterwaarts zoekt. Als u voorwaarts zoekt, worden markeringen die worden overgeslagen, niet geteld. |
| [!UICONTROL Estimated Streams] | `estimatedStreams` | Getal | Het geschatte aantal video- of audiostreams voor elk stuk inhoud. |
| [!UICONTROL Pause Impacted Streams] | `hasPauseImpactedStreams` | Boolean | Geeft aan of een of meer pauzes zijn opgetreden tijdens het afspelen van één media-item. |
| [!UICONTROL Pause Events] | `pauseCount` | Geheel | [!UICONTROL Pause Events] Hiermee wordt het aantal pauzeperioden geteld dat tijdens het afspelen is opgetreden. |
| [!UICONTROL Total Pause Duration] | `pauseTime` | Geheel | [!UICONTROL Total Pause Duration] beschrijft de duur in seconden waarin het afspelen door de gebruiker is gepauzeerd. |
| [!UICONTROL Media Segment Views] | `hasSegmentView` | Boolean | [!UICONTROL Media Segment Views] Hiermee wordt aangegeven dat ten minste één frame, niet noodzakelijkerwijs het eerste frame, is weergegeven. |
| [!UICONTROL Media Session Server Timeout] | `secondsSinceLastCall` | Getal | De [!UICONTROL Media Session Server Timeout] Hiermee wordt de hoeveelheid tijd in seconden aangegeven die is verstreken tussen de laatst bekende interactie van de gebruiker en het moment waarop de sessie werd gesloten. |
| [!UICONTROL Content Delivery Network] | `cdn` | String | De [!UICONTROL Content Delivery Network] van de afgespeelde inhoud. |
| [!UICONTROL Pev3] | `pev3` | String | [!UICONTROL Pev3] Dit is het type mediastream dat wordt gebruikt voor rapportage. |
| [!UICONTROL Pccr] | `pccr` | Boolean | [!UICONTROL Pccr] geeft aan dat er een omleiding heeft plaatsgevonden. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
