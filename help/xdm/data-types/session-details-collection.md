---
title: Gegevenstype verzameling sessiegegevens
description: Leer over het gegevenstype Sessiedetails Collection Data Model (XDM).
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# [!UICONTROL Session Details] Gegevenstype verzameling

[!UICONTROL Session Details] Verzameling is een standaard XDM-gegevenstype (Experience Data Model) dat gegevens bijhoudt die betrekking hebben op mediaflaysessies. De inzamelingsgebieden van media worden gebruikt om gegevens te vangen die naar andere diensten van Adobe voor verdere verwerking worden verzonden. Dit schema omvat een breed scala aan eigenschappen die kunnen worden gebruikt om inzichten in het gedrag van de gebruiker en de consumptiepatronen van de inhoud te bieden. Gebruik het gegevenstype [!UICONTROL Session Details] Verzameling om de betrokkenheid van de gebruiker vast te leggen door afspeelgebeurtenissen, interacties, voortgangsmarkeringen, pauzes en andere metriek te registreren.

+++Select om een diagram van het gegevenstype van de Inzameling van de Details van de Zitting te tonen.
![ A diagram van het gegevenstype van de Inzameling van de Details van de Zitting.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Elke weergavenaam bevat een koppeling naar meer informatie over de audio- en videoparameters. De gekoppelde pagina&#39;s bevatten gegevens over de video en gegevens die worden verzameld door Adobe, implementatiewaarden, netwerkparameters, rapportage en belangrijke overwegingen.

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Ad Load Type] | `adLoad` | String | Nee | Het type advertentie dat wordt geladen zoals gedefinieerd door de interne representatie van elke klant. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | String | Nee | De naam van het album waartoe de muziekopname of video behoort. |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | String | Nee | De naam van de albumartiest of groep die de muziekopname of video uitvoert. |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | String | Nee | [!UICONTROL Asset ID] is de unieke id voor de inhoud van het media-element, zoals de aflevering-id van de tv-reeks, de id van het filmelement of de livegebeurtenis. Deze id&#39;s zijn doorgaans afgeleid van metagegevensautoriteiten zoals EIDR, TMS/Gracenote of Rovi. Deze id&#39;s kunnen ook afkomstig zijn van andere bedrijfseigen of interne systemen. |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | String | Nee | De naam van de auteur van de media. |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | String | Ja | De [!UICONTROL Broadcast Content Type] van de levering van de stream. Beschikbare waarden per [!UICONTROL Stream Type] omvatten:<br> Audio: &quot;lied&quot;, &quot;podcast&quot;, &quot;audiobook&quot;, en &quot;radio&quot;;<br> Video: &quot;VoD&quot;, &quot;Levend&quot;, &quot;Lineair&quot;, &quot;UGC&quot;, en &quot;DVoD&quot;.<br> Klanten kunnen douanewaarden voor deze parameter verstrekken. |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | String | Nee | De netwerk-/kanaalnaam. |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | String | Ja | De [!UICONTROL Content Channel] is het distributiekanaal van waaruit de inhoud is afgespeeld. |
| [[!UICONTROL Content Completes]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | Boolean | Nee | [!UICONTROL Content Completes] geeft aan of een getimede media-element is gecontroleerd op voltooiing. Deze gebeurtenis betekent niet noodzakelijkerwijs dat de viewer de hele video heeft bekeken. De viewer heeft mogelijk een voorsprong overgeslagen. |
| [!UICONTROL Content Delivery Network] | `cdn` | String | Nee | De [!UICONTROL Content Delivery Network] van de afgespeelde inhoud. |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | string | Ja | [!UICONTROL Content ID] is een unieke id van de inhoud. Het kan worden gebruikt om terug naar andere industrie of CMS IDs te verbinden. |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | String | Nee | De [!UICONTROL Content Name] is de &#39;vriendelijke&#39; (leesbare) naam van de inhoud. |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | String | Ja | De naam van de inhoudsspeler. |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | String | Nee | De naam van de maker van de inhoud. |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | String | Nee | A property that define the time of the day when the content was broadcast or play. Dit zou om het even welke waarde kunnen hebben die zonodig door klanten wordt geplaatst |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | String | Nee | The number of the episode. |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | String | Nee | Het type feed, dat ofwel werkelijke feed-gerelateerde gegevens zoals EAST HD of SD kan vertegenwoordigen, ofwel de bron van de feed zoals een URL. |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | String | Nee | De datum waarop de inhoud voor het eerst op de televisie is uitgezonden. Elke datumnotatie is acceptabel, maar de Adobe beveelt aan: JJJJ-MM-DD. |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | String | Nee | De datum waarop de inhoud voor het eerst via een digitaal kanaal of platform is verzonden. Elke datumnotatie is acceptabel, maar de Adobe raadt aan: JJJ-MM-DD. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | String | Nee | Het type of de groep inhoud zoals gedefinieerd door de inhoudsproducent. Waarden moeten door komma&#39;s worden gescheiden in een variabele implementatie. |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | String | Nee | Bevestigt of de gebruiker via de authentificatie van de Adobe is toegelaten. |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Geheel | Ja | [!UICONTROL Media Content Length] bevat de lengte/runtime van de clip. Dit is de maximale lengte (of duur) van de inhoud die wordt verbruikt (in seconden). |
| [[!UICONTROL Media Starts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | Boolean | Nee | De gebeurtenis load voor de media. Dit gebeurt wanneer de viewer de afspeelknop selecteert. Dit telt zelfs als er pre-roladvertenties, het bufferen, fouten, etc. zijn. |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | String | Nee | De MVPD-id (Multi-channel Video Programming Distributor) die via verificatie van de Adobe is opgegeven. |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | String | Nee | De naam van de uitgever van de audio-inhoud. |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | String | Nee | De naam van het radiostation waarop de audio wordt afgespeeld. |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | String | Nee | De rating zoals gedefinieerd in de TV Parental Guidelines. |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | String | Nee | De naam van het recordlabel. |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Boolean | Nee | Markeert elke playback die na meer dan 30 minuten van buffer, pauze, of stallatieperiode werd hervat. |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | String | Nee | De [!UICONTROL Season Number] waartoe de presentatie behoort. Reeks seizoen is alleen vereist als de presentatie deel uitmaakt van een reeks. |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | String | Nee | The Program/Series Name. De Naam van het Programma wordt vereist slechts als de show deel van een reeks uitmaakt. |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | String | Nee | Het type inhoud. Bijvoorbeeld een aanhangwagen of een volledige aflevering. Het type inhoud wordt uitgedrukt als een geheel getal tussen 0 en 3. Bijvoorbeeld &quot;0&quot; = volledige aflevering; &quot;1&quot; = Voorvertoning/trailer; &quot;2&quot; = Clip; &quot;3&quot; = Overige. |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | String | Nee | De indeling van de stream (HD, SD). |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | String | Nee | Het type van de mediastream. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | String | Nee | De SDK-versie die door de speler wordt gebruikt. Dit kan elke aangepaste waarde hebben die voor uw speler zinnig is. |

{style="table-layout:auto"}

<!-- This is required for sessionStart. 
Q) How do I indicate that?
Q) Do you know where to link for:
Ad Load Type
Content Delivery Network
 -->
