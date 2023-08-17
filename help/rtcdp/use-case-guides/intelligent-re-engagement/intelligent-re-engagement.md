---
title: Intelligente re-engagement
description: Lever boeiende en verbonden ervaringen tijdens de belangrijkste omzettingsmomenten om intelligent onregelmatige klanten opnieuw aan te sluiten.
hide: true
hidefromtoc: true
source-git-commit: 43e365e20a2fd91a0e822eb6f66bb7db6fc218f5
workflow-type: tm+mt
source-wordcount: '2915'
ht-degree: 2%

---

# Inzet uw klanten op intelligente wijze opnieuw aan om terug te keren

Neem cliënten opnieuw in dienst die een omzetting hebben verlaten alvorens het op een intelligente en verantwoordelijke manier te voltooien. Verloren klanten door ervaringen eerder dan herinneringen aantrekken om conversie te verbeteren en de groei van de waarde van de cliëntlevensduur te drijven.

U kunt real-time overwegingen gebruiken, rekening houden met alle kwaliteiten en gedragingen van de consument en snelle herkwalificatie bieden op basis van zowel online als offline gebeurtenissen.

![Stap voor stap, intelligent overzicht op hoog niveau van de hernieuwde betrokkenheid.](../intelligent-re-engagement/images/step-by-step.png)

## Hoofdlettergebruik

U zult schema&#39;s, datasets, en publiek aangezien u door voorbeelden van re-engagement reizen werkt. U zult ook de eigenschappen ontdekken nodig om de voorbeeldreizen in te stellen [!DNL Adobe Journey Optimizer] en die welke nodig zijn om betaalde mediaberichten op bestemmingen te maken. In deze handleiding worden voorbeelden gebruikt van het opnieuw betrekken van klanten bij de hieronder beschreven gebruiksritten:

* **Reizigersreis** - richt klanten die het doorbladeren van producten op zowel de website als de mobiele app hebben verlaten.
* **Verlaten karretje** - richt klanten die producten in de kar hebben geplaatst maar nog niet op zowel de website als de mobiele app gekocht.
* **Bevestiging van bestelling** - Gericht op aankopen van producten via de website en de mobiele app.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer u de stappen voor het implementeren van het gebruiksscenario uitvoert, maakt u gebruik van de volgende Real-Time CDP-functionaliteit en UI-elementen (vermeld in de volgorde waarin u deze wilt gebruiken). Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Gegevens worden samengevoegd over verschillende gegevensbronnen om de campagne te voeden. Deze gegevens worden vervolgens gebruikt om het campagnepubliek te maken en gepersonaliseerde gegevenselementen aan de oppervlakte te brengen die worden gebruikt in de e-mail en de webpromo-elementen (bijvoorbeeld naam of aan account gerelateerde informatie). CDP wordt ook gebruikt om publiek over e-mail en het Web (via Adobe Target) te activeren.
   * [Schema&#39;s](/help/xdm/home.md)
   * [Profielen](/help/profile/home.md)
   * [Gegevenssets](/help/catalog/datasets/overview.md)
   * [Doelgroepen](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Doelen](/help/destinations/home.md)
   * [Trigger voor gebeurtenis of publiek](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Soorten publiek/Gebeurtenissen](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Reishandelingen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

Hieronder vindt u een overzicht op hoog niveau van de drie voorbeelden van herplaatsingsreizen.

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

De reis om opnieuw aan de slag te gaan richt verlaten product het doorbladeren op zowel de website als mobiele app. Deze reis wordt geactiveerd wanneer een product is bekeken maar niet is aangeschaft of aan de wagen is toegevoegd. De merkbetrokkenheid wordt geactiveerd na drie dagen als er geen toevoegingen aan de lijst zijn binnen de laatste 24 uur.<p>![Intelligente reactiereis op hoog niveau van visueel overzicht van de klant.](../intelligent-re-engagement/images/re-engagement-journey.png "Intelligente reactiereis op hoog niveau van visueel overzicht van de klant."){width="1920" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets die voor duidelijk zijn [!UICONTROL Profile].
2. Gegevens worden geaggregeerd in Experience Platform via Web SDK, Mobile Edge SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U laadt profielen in Real-Time CDP en bouwt governancebeleid om verantwoord gebruik te garanderen.
4. U maakt doelgroepen in de lijst met profielen om te controleren of een **klant** heeft in de laatste drie dagen een betrokkenheid gemaakt.
5. U maakt een terugkerende reis in [!DNL Adobe Journey Optimizer].
6. Werk zo nodig met de **gegevenspartner** voor de activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert de toestemming en verzendt de diverse gevormde acties.

>[!TAB Afgekloonde Kart-reis]

De niet langer gebruikte reisweg is gericht op producten die in de wagen zijn geplaatst maar nog niet op de website en mobiele app zijn gekocht. Bovendien worden campagnes voor betaalde media gestart en gestopt met deze methode.<p>![De klant verliet de reis van het karretje op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png "De klant verliet de reis van het karretje op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets die voor duidelijk zijn [!UICONTROL Profile].
2. Gegevens worden geaggregeerd in Experience Platform via Web SDK, Mobile Edge SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U laadt profielen in Real-Time CDP en bouwt governancebeleid om verantwoord gebruik te garanderen.
4. U maakt doelgroepen in de lijst met profielen om te controleren of een **klant** heeft een artikel in hun winkelwagentje geplaatst, maar heeft de aankoop niet voltooid. De **[!UICONTROL Add to cart]** de gebeurtenis tikt van een tijdopnemer die 30 minuten wacht, dan controleert aankoop. Als er geen aankoop is gedaan, wordt de **klant** wordt toegevoegd aan de **[!UICONTROL Abandon Cart]** publiek.
5. Je creëert een verlaten carterreis in Adobe Journey Optimizer
6. Werk zo nodig met de **gegevenspartner** voor de activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert de toestemming en verzendt de diverse gevormde acties.

>[!TAB Reis voor orderbevestiging]

De reis voor het bevestigen van bestellingen is vooral gericht op productaankopen via de website en de mobiele app.<p>![Bevestiging van de reis van de bestelbevestiging van de klant op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Bevestiging van de reis van de bestelbevestiging van de klant op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets die voor duidelijk zijn [!UICONTROL Profile].
2. Gegevens worden geaggregeerd in Experience Platform via Web SDK, Mobile Edge SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U laadt profielen in Real-Time CDP en bouwt governancebeleid om verantwoord gebruik te garanderen.
4. U maakt doelgroepen in de lijst met profielen om te controleren of een **klant** heeft een aankoop gedaan.
5. Je maakt een bevestigingsreis in Adobe Journey Optimizer.
6. [!DNL Adobe Journey Optimizer] verzendt een bericht van de ordesbevestiging gebruikend het aangewezen kanaal.

>[!ENDTABS]

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door om alle stappen in de bovenstaande overzichten op hoog niveau te voltooien. Deze bevatten koppelingen naar meer informatie en meer gedetailleerde instructies.

### UI-functionaliteit en elementen die u gebruikt {#ui-functionality-and-elements}

Wanneer u de stappen voor het implementeren van het hoofdlettergebruik uitvoert, maakt u gebruik van de Real-Time CDP-functionaliteit en UI-elementen die aan het begin van dit document worden vermeld. Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

### Een schemaontwerp maken en veldgroepen opgeven

De middelen van het Gegevensmodel van de ervaring (XDM) worden beheerd in [!UICONTROL Schemas] in Adobe Experience Platform. U kunt kernmiddelen bekijken en onderzoeken die door Adobe worden verstrekt en douanemiddelen en schema&#39;s voor uw organisatie tot stand brengen.

Lees voor meer informatie over het maken van schema&#39;s de [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md)

Er zijn vier schemaontwerpen die voor de reis van het re-engagement worden gebruikt. Voor elk schema moeten specifieke velden worden ingesteld en moeten bepaalde velden worden ingesteld die sterk worden aanbevolen.

#### Klantkenmerkenschema

Het schema met klantkenmerken wordt weergegeven door een [!UICONTROL XDM Individual Profile] klasse, die de volgende veldgroepen bevat:

+++Persoonlijke Contactgegevens (Veldgroep)

[Persoonlijke contactgegevens](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel van Afzonderlijke XDM die de contactinformatie voor een individuele persoon beschrijft.

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `mobilePhone.number` | Vereist | Het mobiele telefoonnummer van de persoon, dat wordt gebruikt voor SMS. |
| `personalEmail.address` | Vereist | Het e-mailadres van de persoon. |

+++

+++Demografische details (veldgroep)

[Demografische details](/help/xdm/field-groups/profile/demographic-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel Individual XDM. De veldgroep biedt een persoonlijk object op hoofdniveau, waarvan de subvelden informatie over een individuele persoon beschrijven.

| Velden | Vereiste |
| --- | --- |
| `person.name.firstName` | Voorgesteld |
| `person.name.lastName` | Voorgesteld |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

[Kenmerken externe bronsysteemcontrole](/help/xdm/data-types/external-source-system-audit-attributes.md) is een standaardgegevenstype van de Gegevens van de Ervaring Model (XDM) dat controledetails over een extern bronsysteem vangt.

+++

+++Groepen van het Toegelaten en van het Referentieveld (de Groep van het Gebied)

[De inhoud en voorkeuren](/help/xdm/field-groups//profile/consents.md) veldgroep biedt één objecttype veld, toestemmingen, voor het vastleggen van toestemmings- en voorkeursgegevens.

| Velden | Vereiste |
| --- | --- |
| `consents.marketing.email.val` | Vereist |
| `consents.marketing.preferred` | Vereist |
| `consents.marketing.push.val` | Vereist |
| `consents.marketing.sms.val` | Vereist |
| `consents.personalize.content.val` | Vereist |
| `consents.share.val` | Vereist |

+++

+++Details van de Test van het Profiel (de Groep van het Gebied)

Deze veldgroep wordt gebruikt voor beste praktijken.

+++

#### Schema voor digitale transacties van klanten

Het schema voor digitale transacties van de klant wordt vertegenwoordigd door een [!UICONTROL XDM ExperienceEvent] klasse, die de volgende veldgroepen bevat:

+++Adobe Experience Platform Web SDK ExperienceEvent (veldgroep)

| Velden | Vereiste |
| --- | --- |
| `device.model` | Voorgesteld |
| `environment.browserDetails.userAgent` | Voorgesteld |

+++

+++Webdetails (Veldgroep)

Webdetails is een standaardschemaveldgroep voor de klasse XDM ExperienceEvent die wordt gebruikt om informatie te beschrijven over webdetailgebeurtenissen zoals interactie, paginadetails en referentie.

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Voorgesteld | De id voor de webkoppeling of URL die overeenkomt met de interactie. |
| `web.webInteraction.linkClicks.value` | Voorgesteld | Het aantal klikken voor de webkoppeling of URL die overeenkomt met de interactie. |
| `web.webInteraction.name` | Voorgesteld | De naam van de webpagina. |
| `web.webInteraction.URL` | Voorgesteld | De URL voor de webpagina. |
| `web.webPageDetails.name` | Voorgesteld | De naam van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| `web.webPageDetails.URL` | Voorgesteld | De URL van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| `web.webReferrer.URL` | Voorgesteld | Beschrijft de referentie van een Webinteractie, die URL is een bezoeker van onmiddellijk vóór de huidige Webinteractie kwam werd geregistreerd. |

+++

+++Consumer Experience Event (veldgroep)

| Velden | Vereiste |
| --- | --- |
| `commerce.cart.cartID` | Voorgesteld |
| `commerce.cart.cartSource` | Voorgesteld |
| `commerce.cartAbandons.id` | Voorgesteld |
| `commerce.cartAbandons.value` | Voorgesteld |
| `commerce.order.orderType` | Voorgesteld |
| `commerce.order.payments.paymentAmount` | Voorgesteld |
| `commerce.order.payments.paymentType` | Voorgesteld |
| `commerce.order.payments.transactionID` | Voorgesteld |
| `commerce.order.priceTotal` | Voorgesteld |
| `commerce.order.purchaseID` | Voorgesteld |
| `commerce.productListAdds.id` | Voorgesteld |
| `commerce.productListAdds.value` | Voorgesteld |
| `commerce.productListOpens.id` | Voorgesteld |
| `commerce.productListOpens.value` | Voorgesteld |
| `commerce.productListRemoval.id` | Voorgesteld |
| `commerce.productListRemoval.value` | Voorgesteld |
| `commerce.productListViews.id` | Voorgesteld |
| `commerce.productListViews.value` | Voorgesteld |
| `commerce.productViews.id` | Voorgesteld |
| `commerce.productViews.value` | Voorgesteld |
| `commerce.purchases.id` | Voorgesteld |
| `commerce.purchases.value` | Voorgesteld |
| `marketing.campaignGroup` | Voorgesteld |
| `marketing.campaignName` | Voorgesteld |
| `marketing.trackingCode` | Voorgesteld |
| `productListItems.name` | Voorgesteld |
| `productListItems.priceTotal` | Voorgesteld |
| `productListItems.product` | Voorgesteld |
| `productListItems.quantity` | Voorgesteld |

+++

+++Details eindgebruiker-id (veldgroep)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Vereist | Status van e-mailadres voor eindgebruiker is geverifieerd. |
| `endUserIDs._experience.emailid.id` | Vereist | E-mailadres van eindgebruiker. |
| `endUserIDs._experience.emailid.namespace.code` | Vereist | Naamruimte-code van e-mailadres van eindgebruiker. |
| `endUserIDs._experience.mcid.authenticatedState` | Vereist | Status geverifieerd voor Adobe Marketing Cloud ID (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.id` | Vereist | Adobe Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.namespace.code` | Vereist | Adobe Marketing Cloud ID (MCID)-naamruimtecode. |

+++

+++Klasse-waarde (veldgroep)

| Velden | Vereiste |
| --- | --- |
| `eventType` | Vereist |
| `timestamp` | Vereist |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Offline transactieschema van de klant

Het schema voor offline transacties van de klant wordt vertegenwoordigd door een [!UICONTROL XDM ExperienceEvent] klasse, die de volgende veldgroepen bevat:

+++Details van de Handel (de Groep van het Gebied)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `commerce.cart.cartID` | Vereist | Een id voor het winkelwagentje. |
| `commerce.order.orderType` | Vereist | Een object dat het type productvolgorde beschrijft. |
| `commerce.order.payments.paymentAmount` | Vereist | Een object dat het bedrag van de productbestelling beschrijft. |
| `commerce.order.payments.paymentType` | Vereist | Een object dat een beschrijving geeft van het type productorderbetaling. |
| `commerce.order.payments.transactionID` | Vereist | Een transactie-id voor een objectproduct. |
| `commerce.order.purchaseID` | Vereist | Een aankoop-id voor de objectorder. |
| `productListItems.name` | Vereist | Een lijst met itemnamen die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| `productListItems.priceTotal` | Vereist | De totale prijs van de lijst met objecten die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| `productListItems.product` | Vereist | Het geselecteerde product of de producten. |
| `productListItems.quantity` | Vereist | De hoeveelheid lijst met objecten die het product of de producten vertegenwoordigt die door een klant is/zijn geselecteerd. |

+++

+++Persoonlijke Contactgegevens (Veldgroep)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `mobilePhone.number` | Vereist | Het mobiele telefoonnummer van de persoon, dat wordt gebruikt voor SMS. |
| `personalEmail.address` | Vereist | Het e-mailadres van de persoon. |

+++

+++Klasse-waarde (veldgroep)

| Velden | Vereiste |
| --- | --- |
| `eventType` | Vereist |
| `timestamp` | Vereist |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Adobe webverbindingsschema

Het schema van de Adobe Webschakelaar wordt vertegenwoordigd door [!UICONTROL XDM ExperienceEvent] klasse, die de volgende veldgroepen bevat:

+++Adobe Analytics ExperienceEvent-sjabloon (veldgroep)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Voorgesteld | De id voor de webkoppeling of URL die overeenkomt met de interactie. |
| `web.webInteraction.linkClicks.value` | Voorgesteld | Het aantal klikken voor de webkoppeling of URL die overeenkomt met de interactie. |
| `web.webInteraction.name` | Voorgesteld | De naam van de webpagina. |
| `web.webInteraction.URL` | Voorgesteld | De URL voor de webpagina. |
| `web.webPageDetails.name` | Voorgesteld | De naam van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| `web.webPageDetails.URL` | Voorgesteld | De URL van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| `web.webReferrer.URL` | Voorgesteld | Beschrijft de referentie van een Webinteractie, die URL is een bezoeker van onmiddellijk vóór de huidige Webinteractie kwam werd geregistreerd. |
| `commerce.cart.cartID` | Voorgesteld | |
| `commerce.cart.cartSource` | Voorgesteld | |
| `commerce.cartAbandons.id` | Voorgesteld | |
| `commerce.cartAbandons.value` | Voorgesteld | |
| `commerce.order.orderType` | Voorgesteld | |
| `commerce.order.payments.paymentAmount` | Voorgesteld | |
| `commerce.order.payments.paymentType` | Voorgesteld | |
| `commerce.order.payments.transactionID` | Voorgesteld | |
| `commerce.order.priceTotal` | Voorgesteld | |
| `commerce.order.purchaseID` | Voorgesteld | |
| `commerce.productListAdds.id` | Voorgesteld | |
| `commerce.productListAdds.value` | Voorgesteld | |
| `commerce.productListOpens.id` | Voorgesteld | |
| `commerce.productListOpens.value` | Voorgesteld | |
| `commerce.productListRemoval.id` | Voorgesteld | |
| `commerce.productListRemoval.value` | Voorgesteld | |
| `commerce.productListViews.id` | Voorgesteld | |
| `commerce.productListViews.value` | Voorgesteld | |
| `commerce.productViews.id` | Voorgesteld | |
| `commerce.productViews.value` | Voorgesteld | |
| `commerce.purchases.id` | Voorgesteld | |
| `commerce.purchases.value` | Voorgesteld | |
| `marketing.campaignGroup` | Voorgesteld | |
| `marketing.campaignName` | Voorgesteld | |
| `marketing.trackingCode` | Voorgesteld | |
| `productListItems.name` | Voorgesteld | |
| `productListItems.priceTotal` | Voorgesteld | |
| `productListItems.product` | Voorgesteld | |
| `productListItems.quantity` | Voorgesteld | |
| `endUserIDs._experience.emailid.authenticatedState` | Vereist | Status van e-mailadres voor eindgebruiker is geverifieerd. |
| `endUserIDs._experience.emailid.id` | Vereist | E-mailadres van eindgebruiker. |
| `endUserIDs._experience.emailid.namespace.code` | Vereist | Naamruimte-code van e-mailadres van eindgebruiker. |
| `endUserIDs._experience.mcid.authenticatedState` | Vereist | Status geverifieerd voor Adobe Marketing Cloud ID (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.id` | Vereist | Adobe Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.namespace.code` | Vereist | Adobe Marketing Cloud ID (MCID)-naamruimtecode. |

+++

+++Klasse-waarde (veldgroep)

| Velden | Vereiste |
| --- | --- |
| `eventType` | Vereist |
| `timestamp` | Vereist |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

### Een dataset maken op basis van een schema

Een dataset is een opslag en beheersstructuur voor een groep gegevens, vaak een lijst met gebieden (rijen) en een schema (kolommen). Elk schema voor intelligente reizen voor opnieuw engagement heeft één dataset.

Voor meer informatie over hoe te om een dataset van een schema tot stand te brengen, lees [UI-gids voor gegevensbestanden](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Gelijkaardig aan de stap om een schema tot stand te brengen, moet u toelaten dat de dataset in het Profiel van de Klant in real time wordt omvat. Voor meer informatie over het toelaten van de dataset voor gebruik in het Profiel van de Klant In real time, lees [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Privacy, toestemming en gegevensbeheer

#### Toestemmingsbeleid

>[!IMPORTANT]
>
>Het bieden van klanten de mogelijkheid om zich af te melden van het ontvangen van communicatie van een merk is een wettelijke vereiste, en het verzekeren van deze keuze wordt gerespecteerd. Meer informatie over de toepasselijke wetgeving vindt u in het [Documentatie Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Bij het maken van een pad voor een nieuwe afspraak moet rekening worden gehouden met het volgende beleid voor toestemming en moet dit worden gebruikt:

* Indien `consents.marketing.email.val = "Y"` vervolgens kunt u e-mailen
* Indien `consents.marketing.sms.val = "Y"` Dan kan SMS
* Indien `consents.marketing.push.val = "Y"` vervolgens kan duwen
* Indien `consents.share.val = "Y"` kan vervolgens adverteren
* Noodzaak gedefinieerd door implementatie door klant

#### DULE label en handhaving

Persoonlijke e-mailadressen worden gebruikt als direct identificeerbare gegevens die worden gebruikt om een specifieke persoon te identificeren of contact met hem te krijgen in plaats van met een apparaat.

* `personalEmail.address = I1`

#### Marketingsbeleid

Er is geen aanvullend marketingbeleid vereist voor de herplaatsingsreizen, maar het volgende moet als gewenst worden beschouwd:

* Gevoelige gegevens beperken
* Onsite reclame beperken
* E-maildoelen beperken
* Doelstelling voor meerdere sites beperken
* Het combineren van rechtstreeks identificeerbare gegevens met anonieme gegevens beperken

### Een doelgroep maken

#### Audience creation for brand re-engagement trip

Bij de reactiereizen worden doelgroepen gebruikt om specifieke kenmerken of gedragingen te definiëren die door een subset van profielen uit uw profielarchief worden gedeeld, zodat een verhandelbare groep personen kan worden onderscheiden van uw klantenbasis. Op Adobe Experience Platform kunnen soorten publiek op twee verschillende manieren tot stand worden gebracht: rechtstreeks samengesteld als publiek of door middel van op platform gebaseerde segmentdefinities.

Lees voor meer informatie over hoe u het publiek rechtstreeks kunt samenstellen de [Handleiding voor compositie van publiek](/help/segmentation/ui/audience-composition.md).

Voor meer informatie over hoe te om publiek door Platform-afgeleide segmentdefinities te bouwen, lees [Handleiding voor de gebruikersinterface van Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

De volgende gebeurtenissen worden gebruikt voor de reis van de herbetrokkenheid waar de gebruikers producten online bekeken en in de komende 24 uur niet aan het winkelwagentje toegevoegd, gevolgd door geen merkbetrokkenheid in de drie dagen daarna.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.productListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

De beschrijving voor de reis van de herinrichting ziet er als volgt uit:

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Afgekloonde Kart-reis]

De volgende evenementen worden gebruikt voor de verlaten cartograaf, waar gebruikers een product aan hun karretje hebben toegevoegd, maar de aankoop niet hebben voltooid of hun karretje in de afgelopen 24 uur niet hebben gewist.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 30 minutes before now and <= 1440 minutes before now`
* `EventType: commerce.purchases`
   * `Timestamp: <= 30 minutes before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 30 minutes before now`

De beschrijving van de verlaten wagenreis ziet er als volgt uit:

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!ENDTABS]

### Reisinstallatie in Adobe Journey Optimizer

>[!NOTE]
>
>Adobe Journey Optimizer omvat niet alles die in de diagrammen bij de bovenkant van deze pagina wordt getoond. Alle betaalde mediaconsters worden gemaakt in [!UICONTROL Destinations].

Met Adobe Journey Optimizer kunt u verbonden, contextafhankelijke en persoonlijke ervaringen aan uw klanten aanbieden. De reis van de klant is het volledige proces van interactie van een klant met het merk. Voor elke gebruiksreis is specifieke informatie vereist. Hieronder worden de precieze gegevens vermeld die voor elke tak van de Reis nodig zijn.

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

+++Gebeurtenissen

* Productweergaven
   * Schema: digitale transacties van klanten
   * Velden:
      * `EventType`
   * Voorwaarde:
      * `EventType = commerce.productViews`
      * Velden:
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Toevoegen aan winkelwagentje
   * Schema: digitale transacties van klanten
   * Velden:
      * `EventType`
   * Voorwaarde:
      * `EventType = commerce.productListAdds`
      * Velden:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Betrokkenheid merk
   * Schema: digitale transacties van klanten
   * Velden:
      * `EventType`
   * Voorwaarde:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Velden:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Key Reis-logica

* Logica voor reizen
   * Weergavegebeurtenis product

* Voorwaarden
   * Controleer of er minstens één online- of offline-aankoopgebeurtenis heeft plaatsgevonden sinds het product voor het laatst is weergegeven.
      * Schema: digitale transacties van klanten
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Controleren op minstens één offlineaankoop sinds het product voor het laatst is weergegeven:
      * Schema: off-line transacties van de klant v.1
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Voorwaarden - Selecteer het doelkanaal
      * Email
         * `consents.marketing.email.val = y`
      * Push
         * `consents.marketing.push.val=y`
      * Sms
         * `consents.marketing.sms.val = y`

   * Kanaalpersonalisatie
      * Inhoud van persoonlijke kanalen op basis van de productweergave.

+++

>[!TAB Afgekloonde Kart-reis]

+++Gebeurtenissen

* Toevoegen aan winkelwagentje
   * Schema: digitale transacties van klanten
   * Velden:
      * `EventType`
   * Voorwaarde:
      * `EventType = commerce.productListAdds`
      * Velden:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Online aankopen
   * Schema: digitale transacties van klanten
   * Velden:
      * `EventType`
   * Voorwaarde:
      * `EventType = commerce.purchases`
      * Velden:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Betrokkenheid merk
   * Schema: digitale transacties van klanten
   * Velden:
      * `EventType`
   * Voorwaarde:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Velden:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Key Journey Logic

* Logica voor reizen
   * `AddToCart` Gebeurtenis

* AuthenticatedState in authenticated

* Voorwaarde: offlineaankopen sinds de laatste keer dat het winkelwagentje werd verlaten:
   * Schema: off-line transacties van de klant v.1
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Voorwaarde: winkelwagentje wordt gewist sinds de laatste keer dat het winkelwagentje werd verlaten:
   * Schema: Digital Transactions van klant v.1
   * `eventType = commerce.cartCleared`
   * `cartID` (ID van de kar)
   * `timestamp > timestamp of cart was last abandoned`

* Doelkanaal selecteren (één of meerdere kanalen selecteren voor breder bereik)
   * Email
      * `consents.marketing.email.val = y`
   * Push
      * `consents.marketing.push.val = y`
   * Sms
      * `consents.marketing.sms.val = y`
   * Kanaalpersonalisatie
      * Geef informatie over de details van het winkelwagentje weer en kan meerdere producten in een tabelindeling weergeven.

+++

>[!TAB Reis voor orderbevestiging]

+++Gebeurtenissen

* Online aankopen
   * Schema: digitale transacties van klanten
   * Velden:
      * `EventType`
   * Voorwaarde:
      * `EventType = commerce.purchases`
      * Velden:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++Key Reis-logica

* Logica voor reizen
   * Ordergebeurtenis

* Voorwaarden
   * Selecteer Doelkanaal (selecteer een of meerdere kanalen voor een groter bereik).
      * Bevestiging van bestellingen wordt beschouwd als dienstbaar in de natuur, dus controle van de toestemming is meestal niet nodig.
      * Email
      * Push
      * Sms

   * Aanpassing kanaalinhoud
      * Hiermee geeft u informatie over de volgordedetails weer en kunt u een lijst met producten weergeven met een tabelindeling.

+++

>[!ENDTABS]

Meer informatie over het maken van reizen in [Adobe Journey Optimizer], lees de [Aan de slag met reishandleiding](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Betaalde mediadeskundigen instellen in bestemmingen

Het bestemmingskader wordt gebruikt voor betaalde media advertenties. Zodra de toestemming is gecontroleerd verzendt het naar de diverse gevormde bestemmingen. Bijvoorbeeld direct mail, e-mail, push, en SMS.

#### Vereiste gegevens voor bestemmingen

Streaming segment exportbestemmingen (zoals Facebook, Google Customer Match, Google DV360) ondersteunen verschillende identiteiten van klantgegevens:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Het segment Abandon Cart streamt en kan daarom door het kader van de Bestemming voor dit gebruiksgeval worden gebruikt.

* Stream/activering
   * [Reclame](/help/destinations/catalog/advertising/overview.md)/[Betaalde media en sociale media](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Streaming doel](/help/destinations/catalog/streaming/http-destination.md)
   * [Aangepaste Destination SDK](/help/destinations/destination-sdk/overview.md)

* Bestand/gepland om de drie uur
   * [E-mailmarketing](/help/destinations/catalog/email-marketing/overview.md)
