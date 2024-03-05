---
keywords: Experience Platform;home;populaire onderwerpen;schema;schema;Schema;XDM;velden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Schemaontwerp;Kaart;Gebeurtenismodellering;Gebeurtenismodellering;beste praktijken;gebeurtenis;gebeurtenissen;
solution: Experience Platform
title: XDM ExperienceEvent-klasse
description: Leer meer over de klasse XDM ExperienceEvent en best practices voor het modelleren van gebeurtenisgegevens.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '2623'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] is een standaard XDM-klasse (Experience Data Model). Gebruik deze klasse om een momentopname met tijdstempels van het systeem te maken wanneer een specifieke gebeurtenis voorkomt of een bepaalde reeks voorwaarden is bereikt.

Een ervaringsgebeurtenis is een feitenverslag van wat voorkwam, met inbegrip van het tijdstip en de identiteit van de betrokken persoon. Gebeurtenissen kunnen expliciet (direct waarneembare menselijke acties) of impliciet (zonder directe menselijke actie) zijn en worden geregistreerd zonder aggregatie of interpretatie. Raadpleeg voor meer informatie op hoog niveau over het gebruik van deze klasse in het ecosysteem van het platform de [XDM-overzicht](../home.md#data-behaviors).

De [!DNL XDM ExperienceEvent] De klasse zelf verstrekt verscheidene op tijd-reeksen betrekking hebbende gebieden aan een schema. Twee van deze velden (`_id` en `timestamp`) zijn **vereist** voor alle schema&#39;s die op deze klasse worden gebaseerd, terwijl de rest facultatief is. De waarden van sommige velden worden automatisch ingevuld wanneer gegevens worden ingevoerd.

![De structuur van XDM ExperienceEvent zoals deze wordt weergegeven in de gebruikersinterface van het platform.](../images/classes/experienceevent/structure.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_id`<br>**(Vereist)** | De klasse Experience Event `_id` in het veld worden afzonderlijke gebeurtenissen die in Adobe Experience Platform worden ingevoerd, afzonderlijk geïdentificeerd. Dit veld wordt gebruikt om de unieke aard van een individuele gebeurtenis te volgen, om te voorkomen dat gegevens worden herhaald en om die gebeurtenis in downstreamdiensten op te zoeken.<br><br>Wanneer dubbele gebeurtenissen worden ontdekt, kunnen de toepassingen en de diensten van het Platform de duplicatie verschillend behandelen. Bijvoorbeeld, dubbele gebeurtenissen in de Dienst van het Profiel worden gelaten vallen als de gebeurtenis met het zelfde `_id` bestaat al in de profielwinkel.<br><br>In sommige gevallen `_id` kan een [Universally Unique Identifier (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) of [Globally Unique Identifier (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Als u gegevens streamt via een bronverbinding of rechtstreeks vanuit een Parquet-bestand opgeeft, moet u deze waarde genereren door een bepaalde combinatie van velden samen te voegen die de gebeurtenis uniek maken. Voorbeelden van gebeurtenissen die kunnen worden samengevoegd, zijn primaire id, tijdstempel, gebeurtenistype, enzovoort. De samengevoegde waarde moet een `uri-reference` geformatteerde tekenreeks: eventuele dubbele tekens moeten worden verwijderd. Daarna, zou de samengevoegde waarde moeten worden gehakt gebruikend SHA-256 of een ander algoritme van uw keus.<br><br>Het is van belang te onderscheiden dat **dit veld vertegenwoordigt geen identiteit die betrekking heeft op een individuele persoon**, maar eerder de gegevensregistratie zelf. Identiteitsgegevens betreffende een persoon moeten worden beperkt tot [identiteitsvelden](../schema/composition.md#identity) in plaats daarvan worden verstrekt door compatibele veldgroepen. |
| `eventMergeId` | Als u de [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) om gegevens in te voeren, vertegenwoordigt dit identiteitskaart van de opgenomen partij die het verslag om veroorzaakte te creëren. Dit veld wordt automatisch ingevuld door het systeem bij het invoeren van gegevens. Het gebruik van dit gebied buiten de context van een implementatie van SDK van het Web wordt niet gesteund. |
| `eventType` | Een tekenreeks die het type of de categorie voor de gebeurtenis aangeeft. Dit gebied kan worden gebruikt als u verschillende gebeurtenistypen binnen het zelfde schema en de dataset wilt onderscheiden, zoals het onderscheiden van een gebeurtenis van de productmening van toe:voegen-aan-winkelwagentje voor een detailhandelsbedrijf.<br><br>Standaardwaarden voor deze eigenschap worden gegeven in het gedeelte [aanhangsel](#eventType), met een beschrijving van het beoogde gebruik. Dit veld is een uitbreidbare opsomming. Dit houdt in dat u ook uw eigen tekenreeksen voor gebeurtenistypen kunt gebruiken om de gebeurtenissen die u bijhoudt, te categoriseren.<br><br>`eventType` beperkt u tot het gebruik van slechts één gebeurtenis per hit op uw toepassing en daarom moet u berekende velden gebruiken om het systeem te laten weten welke gebeurtenis het belangrijkst is. Zie de sectie over [aanbevolen procedures voor berekende velden](#calculated). |
| `producedBy` | Een tekenreekswaarde die de producent of oorsprong van de gebeurtenis beschrijft. Dit veld kan worden gebruikt om bepaalde gebeurtenisproducenten uit te filteren als dat voor segmentatiedoeleinden nodig is.<br><br>Sommige voorgestelde waarden voor deze eigenschap zijn opgenomen in het dialoogvenster [aanhangsel](#producedBy). Dit veld is een uitbreidbare opsomming. Dit houdt in dat u ook uw eigen tekenreeksen kunt gebruiken om verschillende gebeurtenisproducenten te vertegenwoordigen. |
| `identityMap` | Een toewijzingsveld dat een set naamloze identiteiten bevat voor het individu waarop de gebeurtenis van toepassing is. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. U kunt dit veld op de juiste wijze gebruiken voor [Klantprofiel in realtime](../../profile/home.md)Probeer niet handmatig de inhoud van het veld bij te werken in uw gegevensbewerkingen.<br /><br />Zie de sectie over identiteitskaarten in het dialoogvenster [grondbeginselen van de schemacompositie](../schema/composition.md#identityMap) voor meer informatie over het gebruik ervan . |
| `timestamp`<br>**(Vereist)** | Een ISO 8601-tijdstempel van wanneer de gebeurtenis heeft plaatsgevonden, opgemaakt volgens [RFC 3339 — Sectie 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Deze tijdstempel **moet** in het verleden , maar **moet** vanaf 1970. Zie de onderstaande sectie over [tijdstempels](#timestamps) voor beste praktijken op het gebruik van dit gebied. |

{style="table-layout:auto"}

## Aanbevolen procedures voor het modelleren van gebeurtenissen

De volgende secties behandelen beste praktijken voor het ontwerpen van uw op gebeurtenis-gebaseerde schema&#39;s van de Gegevens van de Ervaring (XDM) in Adobe Experience Platform.

### Tijdstempels {#timestamps}

De basis `timestamp` veld van een gebeurtenisschema kan **alleen** de waarneming van het evenement zelf vertegenwoordigen en in het verleden moeten plaatsvinden. De gebeurtenis **moet** vanaf 1970. Als voor uw segmentatiegebruik tijdstempels moeten worden gebruikt die in de toekomst kunnen voorkomen, moeten deze waarden elders in het schema van de Experience-gebeurtenis worden beperkt.

Als een bedrijf in de reis- en gastsector bijvoorbeeld een vluchtreserveringsevenement modelleert, moet de klasse `timestamp` wordt het tijdstip weergegeven waarop de reserveringsgebeurtenis is waargenomen. Andere tijdstempels die verband houden met de gebeurtenis, zoals de begindatum van de reisreservering, moeten worden vastgelegd in afzonderlijke velden die worden verschaft door standaard- of aangepaste veldgroepen.

![Een voorbeeldweergave van het gebeurtenisschema van de ervaring met de vluchtreservering en de begindatum gemarkeerd.](../images/classes/experienceevent/timestamps.png)

Door de klasse-vlakke timestamp gescheiden van andere verwante datetime waarden in uw gebeurtenisschema&#39;s te houden, kunt u de flexibele gevallen van het segmentatiegebruik uitvoeren terwijl het bewaren van een timestamped rekening van klantenreizen in uw ervaringstoepassing.

### Berekende velden gebruiken {#calculated}

Bepaalde interacties in uw ervaringstoepassingen kunnen resulteren in meerdere gerelateerde gebeurtenissen die technisch dezelfde tijdstempel voor de gebeurtenis hebben en daarom kunnen worden weergegeven als één gebeurtenisrecord. Als een klant bijvoorbeeld een product op uw website weergeeft, kan dit resulteren in een gebeurtenisrecord met twee mogelijke `eventType` waarden: een &quot;product view&quot;-gebeurtenis (`commerce.productViews`) of een algemene gebeurtenis &quot;paginaweergave&quot; (`web.webpagedetails.pageViews`). In deze gevallen kunt u berekende velden gebruiken om de belangrijkste kenmerken vast te leggen wanneer meerdere gebeurtenissen in één keer worden vastgelegd.

Gebruiken [Adobe Experience Platform Data Prep](../../data-prep/home.md) om gegevens toe te wijzen, om te zetten en te bevestigen aan en van XDM. De beschikbare [toewijzingsfuncties](../../data-prep/functions.md) Wordt geleverd door de service. U kunt logische operatoren aanroepen om gegevens uit records met meerdere gebeurtenissen bij het opnemen in het Experience Platform prioriteit te geven, te transformeren en/of te consolideren. In het bovenstaande voorbeeld kunt u `eventType` als een berekend veld dat voorrang geeft aan een &quot;productweergave&quot; boven een &quot;paginaweergave&quot; wanneer deze beide voorkomen.

Als u gegevens handmatig via de gebruikersinterface in Platform opneemt, raadpleegt u de handleiding [berekende velden](../../data-prep/ui/mapping.md#calculated-fields) voor specifieke stappen voor het maken van berekende velden.

Als u gegevens aan Platform stroomt gebruikend een bronverbinding, kunt u de bron vormen om berekende gebieden in plaats daarvan te gebruiken. Zie de [documentatie voor uw specifieke bron](../../sources/home.md) voor instructies op hoe te om berekende gebieden uit te voeren wanneer het vormen van de verbinding.

## Compatibele schemaveldgroepen {#field-groups}

>[!NOTE]
>
>De namen van verschillende veldgroepen zijn gewijzigd. Document weergeven op [veldgroepnaapupdates](../field-groups/name-updates.md) voor meer informatie .

Adobe biedt verschillende standaardveldgroepen voor gebruik met de [!DNL XDM ExperienceEvent] klasse. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

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

De volgende sectie bevat aanvullende informatie over de [!UICONTROL XDM ExperienceEvent] klasse.

### Geaccepteerde waarden voor `eventType` {#eventType}

In de volgende tabel worden de toegestane waarden voor `eventType`, alsmede de definities ervan:

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
| `decisioning.propositionDisplay` | Deze gebeurtenis volgt wanneer een beslissingsvoorstel aan een persoon werd getoond. |
| `decisioning.propositionDismiss` | Deze gebeurtenis volgt wanneer is besloten om zich niet aan de voorgestelde aanbieding te houden. |
| `decisioning.propositionInteract` | Deze gebeurtenis volgt wanneer een persoon met een beslissingsvoorstel interactie heeft gehad. |
| `decisioning.propositionSend` | Deze gebeurtenis volgt wanneer is besloten om een aanbeveling of een aanbieding onder bezwarende titel naar een potentiële klant te sturen. |
| `decisioning.propositionTrigger` | Deze gebeurtenis houdt de activering van een propositieproces bij. Er is een bepaalde voorwaarde of handeling opgetreden om de presentatie van een aanbieding te vragen. |
| `delivery.feedback` | Deze gebeurtenis houdt feedbackgebeurtenissen bij voor een levering, zoals een e-maillevering. |
| `directMarketing.emailBounced` | Deze gebeurtenis wordt bijgehouden wanneer een e-mail naar een persoon wordt teruggestuurd. |
| `directMarketing.emailBouncedSoft` | Deze gebeurtenis wordt bijgehouden wanneer een e-mail naar een persoon met een elektronische vorm wordt verzonden. |
| `directMarketing.emailClicked` | Deze gebeurtenis wordt bijgehouden wanneer iemand op een koppeling in een marketingmail heeft geklikt. |
| `directMarketing.emailDelivered` | Deze gebeurtenis wordt bijgehouden wanneer een e-mailbericht naar de e-mailservice van een persoon is verzonden. |
| `directMarketing.emailOpened` | Deze gebeurtenis wordt bijgehouden wanneer een persoon een marketingbericht heeft geopend. |
| `directMarketing.emailSent` | Deze gebeurtenis wordt bijgehouden wanneer een marketingbericht naar een persoon is verzonden. |
| `directMarketing.emailUnsubscribed` | Deze gebeurtenis wordt bijgehouden wanneer een persoon zich niet meer heeft geabonneerd op een marketingmail. |
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
| `media.adBreakComplete` | Deze gebeurtenis volgt wanneer een `adBreakComplete` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd aan het begin van een advertentie-einde. |
| `media.adBreakStart` | Deze gebeurtenis volgt wanneer een `adBreakStart` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd aan het einde van een advertentie-einde. |
| `media.adComplete` | Deze gebeurtenis volgt wanneer een `adComplete` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een advertentie is voltooid. |
| `media.adSkip` | Deze gebeurtenis volgt wanneer een `adSkip` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een advertentie is overgeslagen. |
| `media.adStart` | Deze gebeurtenis volgt wanneer een `adStart` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een advertentie is gestart. |
| `media.bitrateChange` | Deze gebeurtenis volgt wanneer een `bitrateChange` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer de bitsnelheid wordt gewijzigd. |
| `media.bufferStart` | Deze gebeurtenis volgt wanneer een `bufferStart` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer media beginnen te bufferen. |
| `media.chapterComplete` | Deze gebeurtenis volgt wanneer een `chapterComplete` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een hoofdstuk in de media is voltooid. |
| `media.chapterSkip` | Deze gebeurtenis volgt wanneer een `chapterSkip` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een gebruiker een ander gedeelte of hoofdstuk binnen de media-inhoud naar voren of achteren overslaat. |
| `media.chapterStart` | Deze gebeurtenis volgt wanneer een `chapterStart` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd aan het begin van een specifieke sectie of een specifiek hoofdstuk in de media-inhoud. |
| `media.downloaded` | Deze gebeurtenis houdt bij wanneer media gedownloade inhoud heeft plaatsgevonden. |
| `media.error` | Deze gebeurtenis volgt wanneer een `error` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een fout of probleem optreedt tijdens het afspelen van media. |
| `media.pauseStart` | Deze gebeurtenis volgt wanneer een `pauseStart` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer een gebruiker een pauze instelt in het afspelen van media. |
| `media.ping` | Deze gebeurtenis volgt wanneer een `ping` heeft plaatsgevonden. Dit verifieert de beschikbaarheid van een media middel. |
| `media.play` | Deze gebeurtenis volgt wanneer een `play` heeft plaatsgevonden. Deze gebeurtenis wordt geactiveerd wanneer de media-inhoud wordt afgespeeld, wat een actief verbruik door de gebruiker aangeeft. |
| `media.sessionComplete` | Deze gebeurtenis volgt wanneer een `sessionComplete` heeft plaatsgevonden. Deze gebeurtenis markeert het einde van een mediaflaysessie. |
| `media.sessionEnd` | Deze gebeurtenis volgt wanneer een `sessionEnd` heeft plaatsgevonden. Deze gebeurtenis geeft het einde van een mediasessie aan. Deze conclusie kan inhouden dat de mediaspeler wordt gesloten of dat het afspelen wordt gestopt. |
| `media.sessionStart` | Deze gebeurtenis volgt wanneer een `sessionStart` heeft plaatsgevonden. Deze gebeurtenis markeert het begin van een mediaflaysessie. Deze wordt geactiveerd wanneer een gebruiker een mediabestand begint af te spelen. |
| `media.statesUpdate` | Deze gebeurtenis volgt wanneer een `statesUpdate` heeft plaatsgevonden. De mogelijkheden voor het bijhouden van de spelerstatus kunnen worden gekoppeld aan een audio- of videostream. De standaardstatussen zijn: volledig scherm, dempen, closedCaptioning, pictureInPicture, en inFocus. |
| `opportunityEvent.addToOpportunity` | Deze gebeurtenis volgt wanneer een persoon aan een kans werd toegevoegd. |
| `opportunityEvent.opportunityUpdated` | Deze gebeurtenis wordt bijgehouden wanneer een opportuniteit is bijgewerkt. |
| `opportunityEvent.removeFromOpportunity` | Deze gebeurtenis wordt bijgehouden wanneer een persoon uit een opportuniteit is verwijderd. |
| `pushTracking.applicationOpened` | Deze gebeurtenis wordt bijgehouden wanneer een persoon een toepassing heeft geopend via een pushmelding. |
| `pushTracking.customAction` | Deze gebeurtenis wordt bijgehouden wanneer een persoon een aangepaste actie in een pushmelding heeft geselecteerd. |
| `web.formFilledOut` | Deze gebeurtenis volgt wanneer een persoon een formulier op een webpagina heeft ingevuld. |
| `web.webinteraction.linkClicks` | Deze gebeurtenis houdt bij wanneer een koppeling een of meer keren is geselecteerd. |
| `web.webpagedetails.pageViews` | Deze gebeurtenis wordt bijgehouden wanneer een webpagina een of meer weergaven heeft ontvangen. |
| `location.entry` | Deze gebeurtenis houdt de ingang van een persoon of een apparaat op een specifieke plaats bij. |
| `location.exit` | Deze gebeurtenis houdt het afsluiten van een persoon of apparaat vanaf een specifieke locatie bij. |

{style="table-layout:auto"}

### Voorgestelde waarden voor `producedBy` {#producedBy}

In de volgende tabel worden enkele toegestane waarden voor `producedBy`:

| Waarde | Definitie |
| --- | --- |
| `self` | Zelf |
| `system` | Systeem |
| `salesRef` | Verkoopvertegenwoordiger |
| `customerRep` | Vertegenwoordiger van klant |
