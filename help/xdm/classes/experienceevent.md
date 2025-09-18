---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Schemaontwerp;Kaart;Kaart;Gebeurtenismodellering;Gebeurtenismodellering;beste praktijken;gebeurtenis;gebeurtenissen;
solution: Experience Platform
title: XDM ExperienceEvent-klasse
description: Leer meer over de klasse XDM ExperienceEvent en best practices voor het modelleren van gebeurtenisgegevens.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: f00b195567c22f69c05909e76906c8770da4b9d0
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] -klasse

[!DNL XDM ExperienceEvent] is een standaard XDM-klasse (Experience Data Model). Gebruik deze klasse om een momentopname met tijdstempels van het systeem te maken wanneer een specifieke gebeurtenis voorkomt of een bepaalde reeks voorwaarden is bereikt.

Een ervaringsgebeurtenis is een feitenverslag van wat voorkwam, met inbegrip van het tijdstip en de identiteit van de betrokken persoon. Gebeurtenissen kunnen expliciet (direct waarneembare menselijke acties) of impliciet (zonder directe menselijke actie) zijn en worden geregistreerd zonder aggregatie of interpretatie. Voor meer informatie op hoog niveau over het gebruik van deze klasse in het ecosysteem van Experience Platform, verwijs naar het [ XDM overzicht ](../home.md#data-behaviors).

De [!DNL XDM ExperienceEvent] -klasse zelf biedt verschillende aan tijdreeksen gerelateerde velden voor een schema. Twee van deze gebieden (`_id` en `timestamp`) worden vereist **** voor alle schema&#39;s die op deze klasse worden gebaseerd, terwijl de rest facultatief is. De waarden van sommige velden worden automatisch ingevuld wanneer gegevens worden ingevoerd.

![ de structuur van XDM ExperienceEvent aangezien het in Experience Platform UI verschijnt.](../images/classes/experienceevent/structure.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_id`<br>**(Required)** | In het veld Experience Event Class `_id` worden afzonderlijke gebeurtenissen geïdentificeerd die in Adobe Experience Platform worden opgenomen. Dit veld wordt gebruikt om de unieke aard van een individuele gebeurtenis te volgen, om te voorkomen dat gegevens worden herhaald en om die gebeurtenis in downstreamdiensten op te zoeken.<br><br> waar de dubbele gebeurtenissen worden ontdekt, kunnen de toepassingen en de diensten van Experience Platform de verdubbeling verschillend behandelen. Dubbele gebeurtenissen in de profielservice worden bijvoorbeeld verwijderd als de gebeurtenis met dezelfde `_id` al bestaat in de profielopslag. Deze gebeurtenissen zullen echter nog steeds in het dataplak worden geregistreerd.<br><br> in sommige gevallen, `_id` kan a [ Universally Unique Identifier (UUID) ](https://datatracker.ietf.org/doc/html/rfc4122) of [ globally Unieke Identifier (GUID) ](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) zijn.<br><br> als u gegevens van een bronverbinding stroomt of direct van een dossier van het Pakket inneemt, zou u deze waarde moeten produceren door een bepaalde combinatie gebieden aaneengeschakeld die de gebeurtenis uniek maken. Voorbeelden van gebeurtenissen die kunnen worden samengevoegd, zijn primaire id, tijdstempel, gebeurtenistype, enzovoort. De samengevoegde waarde moet een tekenreeks met `uri-reference` opmaak zijn. Dit houdt in dat alle dubbele tekens moeten worden verwijderd. Daarna, zou de samengevoegde waarde moeten worden gehakt gebruikend SHA-256 of een ander algoritme van uw keus.<br><br> het is belangrijk om te onderscheiden dat **dit gebied geen identiteit met betrekking tot een individuele persoon** vertegenwoordigt, maar eerder het verslag van gegevens zelf. Identiteitsgegevens met betrekking tot een persoon zouden aan [ identiteitsgebieden ](../schema/composition.md#identity) moeten worden beperkt die door compatibele gebiedsgroepen in plaats daarvan worden verstrekt. |
| `eventMergeId` | Als het gebruiken van [ SDK van het Web van Adobe Experience Platform ](/help/web-sdk/home.md) om gegevens in te voeren, vertegenwoordigt dit identiteitskaart van de ingebedde partij die het te creëren verslag veroorzaakte. Dit veld wordt automatisch ingevuld door het systeem bij het invoeren van gegevens. Het gebruik van dit gebied buiten de context van een implementatie van SDK van het Web wordt niet gesteund. |
| `eventType` | Een tekenreeks die het type of de categorie voor de gebeurtenis aangeeft. Dit gebied kan worden gebruikt als u verschillende gebeurtenistypen binnen het zelfde schema en de dataset wilt onderscheiden, zoals het onderscheiden van een gebeurtenis van de productmening van toe:voegen-aan-winkelwagentje voor een detailhandelsbedrijf.<br><br> Standaardwaarden voor dit bezit worden verstrekt in de [ appendix sectie ](#eventType), met inbegrip van beschrijvingen van hun voorgenomen gebruiksgeval. Dit veld is een uitbreidbare opsomming. Dit houdt in dat u ook uw eigen tekenreeksen voor gebeurtenistypen kunt gebruiken om de gebeurtenissen die u bijhoudt, te categoriseren.<br><br>`eventType` beperkt u tot het gebruik van slechts één gebeurtenis per treffer voor uw toepassing. Daarom moet u berekende velden gebruiken om het systeem te laten weten welke gebeurtenis het belangrijkst is. Voor meer informatie, zie de sectie over [ beste praktijken voor berekende gebieden ](#calculated). |
| `producedBy` | Een tekenreekswaarde die de producent of oorsprong van de gebeurtenis beschrijft. Dit veld kan worden gebruikt om bepaalde gebeurtenisproducenten uit te filteren als dat voor segmentatiedoeleinden nodig is.<br><br> Sommige voorgestelde waarden voor dit bezit worden verstrekt in de [ appendix sectie ](#producedBy). Dit veld is een uitbreidbare opsomming. Dit houdt in dat u ook uw eigen tekenreeksen kunt gebruiken om verschillende gebeurtenisproducenten te vertegenwoordigen. |
| `identityMap` | Een toewijzingsveld dat een set naamloze identiteiten bevat voor het individu waarop de gebeurtenis van toepassing is. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. Om dit gebied voor [ Real-Time Profiel van de Klant ](../../profile/home.md) behoorlijk te gebruiken, probeer niet manueel om de inhoud van het gebied in uw gegevensverrichtingen bij te werken.<br /><br /> zie de sectie over identiteitskaarten in de [ grondbeginselen van schemacompositie ](../schema/composition.md#identityMap) voor meer informatie over hun gebruiksgeval. |
| `timestamp`<br>**(Required)** | Een tijdstempel van ISO 8601 van toen de gebeurtenis voorkwam, die volgens [ RFC 3339 Sectie 5.6 ](https://datatracker.ietf.org/doc/html/rfc3339) wordt geformatteerd. Dit timestamp **moet** in het verleden voorkomen, maar **moet** van 1970 en daarna plaatsvinden. Zie de sectie hieronder op [ timestamps ](#timestamps) voor beste praktijken op het gebruik van dit gebied. |

{style="table-layout:auto"}

## Aanbevolen procedures voor het modelleren van gebeurtenissen

De volgende secties behandelen beste praktijken voor het ontwerpen van uw op gebeurtenis-gebaseerde schema&#39;s van de Gegevens van de Ervaring (XDM) in Adobe Experience Platform.

### Tijdstempels {#timestamps}

Het wortel `timestamp` gebied van een gebeurtenisschema kan **slechts** de observatie van de gebeurtenis vertegenwoordigen zelf, en moet in het verleden voorkomen. Nochtans, moet de gebeurtenis **** vanaf 1970 plaatsvinden. Als voor uw segmentatiegebruik tijdstempels moeten worden gebruikt die in de toekomst kunnen voorkomen, moeten deze waarden elders in het schema van de Experience-gebeurtenis worden beperkt.

Als een bedrijf in de reis- en gastensector bijvoorbeeld een gebeurtenis voor reservering van vluchten modelleert, geeft het veld op klasseniveau `timestamp` de tijd weer waarop de reserveringsgebeurtenis werd waargenomen. Andere tijdstempels die verband houden met de gebeurtenis, zoals de begindatum van de reisreservering, moeten worden vastgelegd in afzonderlijke velden die worden verschaft door standaard- of aangepaste veldgroepen.

![ het schema van de Gebeurtenis van de steekproefervaring van A met benadrukte Reserve van de Vlucht en Datum van het Begin.](../images/classes/experienceevent/timestamps.png)

Door de klasse-vlakke timestamp gescheiden van andere verwante datetime waarden in uw gebeurtenisschema&#39;s te houden, kunt u de flexibele gevallen van het segmentatiegebruik uitvoeren terwijl het bewaren van een timestamped rekening van klantenreizen in uw ervaringstoepassing.

### Berekende velden gebruiken {#calculated}

Bepaalde interacties in uw ervaringstoepassingen kunnen resulteren in meerdere gerelateerde gebeurtenissen die technisch dezelfde tijdstempel voor de gebeurtenis hebben en daarom kunnen worden weergegeven als één gebeurtenisrecord. Bijvoorbeeld, als een klant een product op uw website bekijkt, kan dit in een gebeurtenisverslag resulteren dat twee potentiële `eventType` waarden heeft: een &quot;product view&quot;gebeurtenis (`commerce.productViews`) of een generische &quot;paginamening&quot;gebeurtenis (`web.webpagedetails.pageViews`). In deze gevallen kunt u berekende velden gebruiken om de belangrijkste kenmerken vast te leggen wanneer meerdere gebeurtenissen in één keer worden vastgelegd.

Het gebruik [ Prep van Gegevens van Adobe Experience Platform ](../../data-prep/home.md) aan kaart, transformatie, en bevestigt gegevens aan en van XDM. Gebruikend de beschikbare [ kaartfuncties ](../../data-prep/functions.md) die door de dienst worden verstrekt kunt u logische exploitanten aanhalen om, gegevens van multi-gebeurtenisverslagen voorrang te geven te transformeren en/of te consolideren wanneer in Experience Platform worden opgenomen. In het bovenstaande voorbeeld kunt u `eventType` aanwijzen als een berekend veld dat voorrang geeft aan een &quot;productweergave&quot; boven een &quot;paginaweergave&quot; wanneer beide voorkomen.

Als u manueel gegevens in Experience Platform via UI opneemt, zie de gids op [ berekende gebieden ](../../data-prep/ui/mapping.md#calculated-fields) voor specifieke stappen op hoe te om berekende gebieden tot stand te brengen.

Als u gegevens naar Experience Platform streamt via een bronverbinding, kunt u de bron zodanig configureren dat berekende velden worden gebruikt. Verwijs naar de [ documentatie voor uw bijzondere bron ](../../sources/home.md) voor instructies op hoe te om berekende gebieden uit te voeren wanneer het vormen van de verbinding.

## Compatibele schemaveldgroepen {#field-groups}

>[!NOTE]
>
>De namen van verschillende veldgroepen zijn gewijzigd. Zie het document op [ de naamupdates van de gebiedsgroep ](../field-groups/name-updates.md) voor meer informatie.

Adobe biedt verschillende standaardveldgroepen voor gebruik met de [!DNL XDM ExperienceEvent] -klasse. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

* [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Balance Transfers]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Campaign Marketing Details]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Card Actions]](../field-groups/event/card-actions.md)
* [[!UICONTROL Channel Details]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce Details]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Deposit Details]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Device Trade-In Details]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Dining Reservation]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL End User ID Details]](../field-groups/event/enduserids.md)
* [[!UICONTROL Environment Details]](../field-groups/event/environment-details.md)
* [[!UICONTROL Flight Reservation]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0 Consent]](../field-groups/event/iab.md)
* [[!UICONTROL Lodging Reservation]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL MediaAnalytics Interaction Details]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Quote Request Details]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Reservation Details]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web Details]](../field-groups/event/web-details.md)

## Bijlage

De volgende sectie bevat aanvullende informatie over de klasse [!UICONTROL XDM ExperienceEvent] .

### Geaccepteerde waarden voor `eventType` {#eventType}

In de volgende tabel worden de toegestane waarden voor `eventType` weergegeven, samen met de bijbehorende definities:

| Waarde | Definitie |
| --- | --- |
| `advertising.clicks` | Deze gebeurtenis wordt bijgehouden wanneer een actie om een advertentie te selecteren plaatsvindt. |
| `advertising.completes` | Deze gebeurtenis volgt wanneer een getimed media-element is gecontroleerd op voltooiing. Dit betekent niet noodzakelijkerwijs dat de viewer de hele video heeft bekeken, omdat de viewer vooruit had kunnen slaan. |
| `advertising.conversions` | Deze gebeurtenis volgt een vooraf bepaalde actie die door een klant wordt uitgevoerd die een gebeurtenis voor prestatiesevaluatie teweegbrengt. |
| `advertising.federated` | Deze gebeurtenis controleert of een Gebeurtenis van de Ervaring door gegevensfederatie (gegevens het delen tussen klanten) werd gecreeerd. |
| `advertising.firstQuartiles` | Deze gebeurtenis houdt bij wanneer een digitale video 25% van de duur bij normale snelheid heeft afgespeeld. |
| `advertising.impressions` | Deze gebeurtenis volgt de indrukken van een advertentie voor een klant die het potentieel heeft om te worden bekeken. |
| `advertising.midpoints` | Deze gebeurtenis houdt bij wanneer een digitale video 50% van de duur bij normale snelheid heeft afgespeeld. |
| `advertising.starts` | Deze gebeurtenis volgt wanneer een digitale video is afgespeeld. |
| `advertising.thirdQuartiles` | Deze gebeurtenis houdt bij wanneer een digitale video 75% van de duur bij normale snelheid heeft afgespeeld. |
| `advertising.timePlayed` | Deze gebeurtenis houdt de hoeveelheid tijd bij die een gebruiker aan een specifiek getimed media middel doorbrengt. |
| `application.close` | Deze gebeurtenis volgt wanneer een toepassing werd gesloten of op de achtergrond werd verzonden. |
| `application.launch` | Deze gebeurtenis wordt bijgehouden wanneer een toepassing werd gestart of op de voorgrond werd geplaatst. |
| `click` | **Vervangen** Gebruik in plaats daarvan `decisioning.propositionInteract`. |
| `commerce.backofficeCreditMemoIssued` | Deze gebeurtenis volgt wanneer een kredietkennisgeving aan een klant is uitgegeven. |
| `commerce.backofficeOrderCancelled` | Deze gebeurtenis volgt wanneer een eerder geïnitieerd aankoopproces vóór voltooiing is geëindigd. |
| `commerce.backofficeOrderItemsShipped` | Deze gebeurtenis volgt wanneer de aangeschafte items fysiek naar de klant zijn verzonden. |
| `commerce.backofficeOrderPlaced` | Deze gebeurtenis volgt de plaatsing van een bestelling. |
| `commerce.backofficeShipmentCompleted` | Deze gebeurtenis houdt de succesvolle voltooiing van het volledige verzendproces bij. |
| `commerce.checkouts` | Deze gebeurtenis wordt bijgehouden wanneer een uitcheckgebeurtenis voor een productlijst is opgetreden. Er kunnen meer dan één uitcheckgebeurtenis zijn als er meerdere stappen in een uitcheckproces zijn. Als er meerdere stappen zijn, worden de tijdstempel en de pagina/ervaring waarnaar wordt verwezen voor elke gebeurtenis gebruikt om elke afzonderlijke gebeurtenis (stap) in volgorde weer te geven. |
| `commerce.productListAdds` | Deze gebeurtenis wordt bijgehouden wanneer een product aan de productlijst of winkelwagentje is toegevoegd. |
| `commerce.productListOpens` | Deze gebeurtenis wordt bijgehouden wanneer een nieuwe productlijst (winkelwagentje) is geïnitialiseerd of gemaakt. |
| `commerce.productListRemovals` | Deze gebeurtenis wordt bijgehouden wanneer een product-item uit een productlijst of winkelwagentje is verwijderd. |
| `commerce.productListReopens` | Deze gebeurtenis volgt wanneer een productlijst (winkelwagentje) die niet meer toegankelijk (verlaten) was opnieuw door een klant, zoals via een hermarketing activiteit is geactiveerd. |
| `commerce.productListViews` | Deze gebeurtenis wordt bijgehouden wanneer een productlijst of winkelwagentje een weergave heeft ontvangen. |
| `commerce.productViews` | Deze gebeurtenis wordt bijgehouden wanneer een product een of meer weergaven heeft ontvangen. |
| `commerce.purchases` | Deze gebeurtenis volgt wanneer een bestelling is geaccepteerd. Dit is de enige vereiste actie in een commerciële omschakeling. Er moet naar een aankoopgebeurtenis worden verwezen in een productlijst. |
| `commerce.saveForLaters` | Deze gebeurtenis wordt bijgehouden wanneer een productlijst voor toekomstig gebruik is opgeslagen, zoals een verlanglijst van het product. |
| `decisioning.propositionDisplay` | Deze gebeurtenis wordt gebruikt wanneer het Web SDK automatisch informatie over verzendt wat op een pagina wordt getoond. U hebt dit gebeurtenistype echter niet nodig als u al op andere manieren weergavegegevens opneemt, zoals bij boven- en onderaan pagina-hits. Onder aan pagina-hits kunt u elk gewenst gebeurtenistype kiezen. |
| `decisioning.propositionDismiss` | Dit gebeurtenistype wordt gebruikt wanneer een Adobe Journey Optimizer-bericht in de toepassing of een inhoudskaart wordt gesloten. |
| `decisioning.propositionFetch` | Wordt gebruikt om aan te geven dat een gebeurtenis voornamelijk bedoeld is om beslissingen op te halen. Adobe Analytics zet deze gebeurtenis automatisch neer. |
| `decisioning.propositionInteract` | Dit gebeurtenistype wordt gebruikt om interacties, zoals kliks, op gepersonaliseerde inhoud te volgen. |
| `decisioning.propositionSend` | Deze gebeurtenis volgt wanneer is besloten om een aanbeveling of een aanbieding onder bezwarende titel naar een potentiële klant te sturen. |
| `decisioning.propositionTrigger` | De gebeurtenissen van dit type worden opgeslagen in lokale opslag door [ SDK van het Web ](../../web-sdk/home.md) maar worden niet verzonden naar Ervaring Edge. Telkens wanneer aan een liniaal wordt voldaan, wordt een gebeurtenis gegenereerd en lokaal opgeslagen (als die instelling is ingeschakeld). |
| `delivery.feedback` | Deze gebeurtenis houdt feedbackgebeurtenissen bij voor een levering, zoals een e-maillevering. |
| `directMarketing.emailBounced` | Deze gebeurtenis wordt bijgehouden wanneer een e-mail naar een persoon wordt teruggestuurd. |
| `directMarketing.emailBouncedSoft` | Deze gebeurtenis wordt bijgehouden wanneer een e-mail naar een persoon met een elektronische vorm wordt verzonden. |
| `directMarketing.emailClicked` | Deze gebeurtenis wordt bijgehouden wanneer iemand op een koppeling in een marketingmail heeft geklikt. |
| `directMarketing.emailDelivered` | Deze gebeurtenis wordt bijgehouden wanneer een e-mailbericht naar de e-mailservice van een persoon is verzonden. |
| `directMarketing.emailOpened` | Deze gebeurtenis wordt bijgehouden wanneer een persoon een marketingbericht heeft geopend. |
| `directMarketing.emailSent` | Deze gebeurtenis wordt bijgehouden wanneer een marketingbericht naar een persoon is verzonden. |
| `directMarketing.emailUnsubscribed` | Deze gebeurtenis wordt bijgehouden wanneer een persoon zich niet meer heeft geabonneerd op een marketingmail. |
| `display` | **Vervangen** Gebruik in plaats daarvan `decisioning.propositionDisplay`. |
| `inappmessageTracking.dismiss` | Deze gebeurtenis wordt bijgehouden wanneer een bericht in de app is gesloten. |
| `inappmessageTracking.display` | Deze gebeurtenis wordt bijgehouden wanneer een bericht in de app werd weergegeven. |
| `inappmessageTracking.interact` | Deze gebeurtenis wordt bijgehouden wanneer er interactie plaatsvindt tussen een bericht in de app. |
| `leadOperation.callWebhook` | Deze gebeurtenis houdt bij wanneer een webhaak wordt aangeroepen als reactie op een lead. |
| `leadOperation.changeCampaignStream` | Deze gebeurtenis betekent een verschuiving in de marketing- of betrokkenheidsstrategie voor een bepaalde lead in het bedrijf. |
| `leadOperation.changeEngagementCampaignCadence` | Deze gebeurtenis volgt wanneer er een wijziging is opgetreden in hoe vaak een lead wordt gebruikt als onderdeel van een campagne. |
| `leadOperation.convertLead` | Deze gebeurtenis volgt wanneer een lead werd geconverteerd. |
| `leadOperation.interestingMoment` | Deze gebeurtenis volgt wanneer een interessant moment voor een persoon werd opgenomen. |
| `leadOperation.mergeLeads` | Deze gebeurtenis volgt wanneer informatie van meerdere leads die naar dezelfde entiteit verwijzen, zijn geconsolideerd. |
| `leadOperation.newLead` | Deze gebeurtenis volgt wanneer een lead is gemaakt. |
| `leadOperation.scoreChanged` | Deze gebeurtenis volgt wanneer de waarde van het score-kenmerk van de lead is gewijzigd. |
| `leadOperation.statusInCampaignProgressionChanged` | Deze gebeurtenis wordt bijgehouden wanneer de status van een lead in een campagne is gewijzigd. |
| `listOperation.addToList` | Deze gebeurtenis volgt wanneer een persoon aan een marketing lijst werd toegevoegd. |
| `listOperation.removeFromList` | Deze gebeurtenis volgt wanneer een persoon uit een marketinglijst werd verwijderd. |
| `media.adBreakComplete` | Deze gebeurtenis geeft aan dat een advertentie-einde is voltooid. |
| `media.adBreakStart` | Deze gebeurtenis geeft het begin van een advertentie-einde aan. |
| `media.adComplete` | Deze gebeurtenis geeft aan dat een advertentie is voltooid. |
| `media.adSkip` | Deze gebeurtenis geeft aan wanneer een advertentie is overgeslagen. |
| `media.adStart` | Deze gebeurtenis geeft het begin van een advertentie aan. |
| `media.bitrateChange` | Deze gebeurtenis geeft aan wanneer de bitsnelheid wordt gewijzigd. |
| `media.bufferStart` | Het gebeurtenistype `media.bufferStart` wordt verzonden wanneer het bufferen begint. Er is geen specifiek gebeurtenistype `bufferResume` . Het bufferen wordt verondersteld te zijn hervat wanneer een `play` -gebeurtenis wordt verzonden na een `bufferStart` -gebeurtenis. |
| `media.chapterComplete` | Deze gebeurtenis geeft de voltooiing van een hoofdstuk aan. |
| `media.chapterSkip` | Deze gebeurtenis wordt geactiveerd wanneer een gebruiker een andere sectie of een ander hoofdstuk naar voren of achteren overslaat. |
| `media.chapterStart` | Deze gebeurtenis geeft het begin van een hoofdstuk aan. |
| `media.downloaded` | Deze gebeurtenis houdt bij wanneer media gedownloade inhoud heeft plaatsgevonden. |
| `media.error` | Deze gebeurtenis geeft aan dat er een fout is opgetreden tijdens het afspelen van media. |
| `media.pauseStart` | Deze gebeurtenis volgt wanneer een `pauseStart` -gebeurtenis heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een gebruiker een pauze instelt in het afspelen van media. Er is geen type hervattingsgebeurtenis. Er wordt een resume gegenereerd wanneer u een afspeelgebeurtenis na een `pauseStart` verzendt. |
| `media.ping` | Het gebeurtenistype `media.ping` wordt gebruikt om de doorlopende afspeelstatus aan te geven. Voor hoofdinhoud moet deze gebeurtenis om de 10 seconden tijdens het afspelen worden verzonden, te beginnen 10 seconden nadat het afspelen is gestart. Voor advertentie-inhoud moet deze elke seconde worden verzonden tijdens het bijhouden van de advertentie. Pingel gebeurtenissen zouden niet de paramentenkaart in het verzoeklichaam moeten omvatten. |
| `media.play` | Het gebeurtenistype `media.play` wordt verzonden wanneer de speler van een andere status naar de status `playing` overschakelt, zoals `buffering,` `paused` (wanneer deze wordt hervat door de gebruiker) of `error` (wanneer deze wordt hersteld), inclusief scenario&#39;s zoals automatisch afspelen. Deze gebeurtenis wordt geactiveerd door de callback van de speler `on('Playing')` . |
| `media.sessionComplete` | Deze gebeurtenis wordt verzonden wanneer het einde van de hoofdinhoud is bereikt. |
| `media.sessionEnd` | Het gebeurtenistype `media.sessionEnd` geeft een melding aan de achtergrond van Media Analytics om een sessie onmiddellijk te sluiten wanneer een gebruiker de weergave beëindigt en deze waarschijnlijk niet zal retourneren. Als deze gebeurtenis niet wordt verzonden, wordt de sessie beëindigd na 10 minuten inactiviteit of 30 minuten zonder beweging van de afspeelkop. Alle volgende mediaquery&#39;s met die sessie-id worden genegeerd. |
| `media.sessionStart` | Het gebeurtenistype `media.sessionStart` wordt verzonden met de vraag van de zittingsopening. Bij het ontvangen van een reactie, wordt identiteitskaart van de Zitting gehaald uit de kopbal van de Plaats en gebruikt voor alle verdere gebeurtenisvraag aan de server van de Inzameling. |
| `media.statesUpdate` | Deze gebeurtenis volgt wanneer een `statesUpdate` -gebeurtenis heeft plaatsgevonden. De mogelijkheden voor het bijhouden van de spelerstatus kunnen worden gekoppeld aan een audio- of videostream. De standaardstatussen zijn: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` en `inFocus` . |
| `opportunityEvent.addToOpportunity` | Deze gebeurtenis volgt wanneer een persoon aan een kans werd toegevoegd. |
| `opportunityEvent.opportunityUpdated` | Deze gebeurtenis wordt bijgehouden wanneer een opportuniteit is bijgewerkt. |
| `opportunityEvent.removeFromOpportunity` | Deze gebeurtenis wordt bijgehouden wanneer een persoon uit een opportuniteit is verwijderd. |
| `personalization.request` | **Vervangen** Gebruik in plaats daarvan `decisioning.propositionFetch`. |
| `pushTracking.applicationOpened` | Deze gebeurtenis wordt bijgehouden wanneer een persoon een toepassing heeft geopend via een pushmelding. |
| `pushTracking.customAction` | Deze gebeurtenis wordt bijgehouden wanneer een persoon een aangepaste actie in een pushmelding heeft geselecteerd. |
| `web.formFilledOut` | Deze gebeurtenis volgt wanneer een persoon een formulier op een webpagina heeft ingevuld. |
| `web.webinteraction.linkClicks` | De gebeurtenissignalen dat een verbindingsklik automatisch door het Web SDK is geregistreerd. |
| `web.webpagedetails.pageViews` | Dit gebeurtenistype is de standaardmethode voor het markeren van de hit als paginaweergave. |
| `location.entry` | Deze gebeurtenis houdt de ingang van een persoon of een apparaat op een specifieke plaats bij. |
| `location.exit` | Deze gebeurtenis houdt het afsluiten van een persoon of apparaat vanaf een specifieke locatie bij. |

{style="table-layout:auto"}

### Voorgestelde waarden voor `producedBy` {#producedBy}

In de volgende tabel worden enkele toegestane waarden voor `producedBy` weergegeven:

| Waarde | Definitie |
| --- | --- |
| `self` | Zelf |
| `system` | Systeem |
| `salesRef` | Verkoopvertegenwoordiger |
| `customerRep` | Vertegenwoordiger van klant |
