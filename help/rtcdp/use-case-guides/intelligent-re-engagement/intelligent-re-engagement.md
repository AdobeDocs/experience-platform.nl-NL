---
title: Intelligente re-engagement
description: Lever boeiende en verbonden ervaringen tijdens de belangrijkste omzettingsmomenten om intelligent onregelmatige klanten opnieuw aan te sluiten.
source-git-commit: 79ba0e350d64f43558af9bc3c2ecd4ac13d11499
workflow-type: tm+mt
source-wordcount: '3403'
ht-degree: 2%

---

# Inzet uw klanten op intelligente wijze opnieuw aan om terug te keren

Neem klanten opnieuw in dienst die een omzetting hebben verlaten alvorens het op een intelligente en verantwoordelijke manier te voltooien. Verloren klanten door ervaringen eerder dan herinneringen aantrekken om conversie te verbeteren en de groei van de waarde van de cliëntlevensduur te drijven.

U kunt real-time overwegingen gebruiken, rekening houden met alle kwaliteiten en gedragingen van de consument en snelle herkwalificatie bieden op basis van zowel online als offline gebeurtenissen.

![Stap voor stap, intelligent overzicht op hoog niveau van de hernieuwde betrokkenheid.](../intelligent-re-engagement/images/step-by-step.png)

## Hoofdlettergebruik

U zult schema&#39;s, datasets, en publiek aangezien u door voorbeelden van re-engagement reizen werkt. U zult ook de eigenschappen ontdekken nodig om de voorbeeldreizen in te stellen [!DNL Adobe Journey Optimizer] en die welke nodig zijn om betaalde mediaberichten op bestemmingen te maken. In deze handleiding worden voorbeelden gebruikt van het opnieuw betrekken van klanten bij de hieronder beschreven gebruiksritten:

* **Reizigersreis** - richt klanten die het doorbladeren van producten op zowel de website als de mobiele app hebben verlaten.
* **Verlaten karretje** - richt klanten die producten in de kar hebben geplaatst maar nog niet op zowel de website als de mobiele app gekocht.
* **Bevestiging van bestelling** - Gericht op aankopen van producten via de website en de mobiele app.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer u de stappen voor het implementeren van het gebruiksscenario uitvoert, maakt u gebruik van de volgende Real-Time CDP-functionaliteit en UI-elementen (vermeld in de volgorde waarin u deze wilt gebruiken). Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - integreert gegevens in verschillende gegevensbronnen om de campagne te voeden. Deze gegevens worden vervolgens gebruikt om het campagnepubliek te maken en gepersonaliseerde gegevenselementen aan de oppervlakte te brengen die worden gebruikt in de e-mail en de webpromo-elementen (bijvoorbeeld naam of aan account gerelateerde informatie). CDP wordt ook gebruikt om publiek over e-mail en het Web (via [!DNL Adobe Target]).
   * [Schema&#39;s](/help/xdm/home.md)
   * [Profielen](/help/profile/home.md)
   * [Gegevenssets](/help/catalog/datasets/overview.md)
   * [Doelgroepen](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Doelen](/help/destinations/home.md)
   * [Trigger voor gebeurtenis of publiek](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Soorten publiek/Gebeurtenissen](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Reishandelingen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

Hieronder vindt u een overzicht op hoog niveau van de drie voorbeelden van herplaatsingsreizen.

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

De reis om opnieuw aan de slag te gaan richt verlaten product het doorbladeren op zowel de website als mobiele app. Deze reis wordt geactiveerd wanneer een product is bekeken maar niet is aangeschaft of aan de wagen is toegevoegd. De merkbetrokkenheid wordt geactiveerd na drie dagen als er geen toevoegingen aan de lijst zijn binnen de laatste 24 uur.<p>![Intelligente reactiereis op hoog niveau van visueel overzicht van de klant.](../intelligent-re-engagement/images/re-engagement-journey.png "Intelligente reactiereis op hoog niveau van visueel overzicht van de klant."){width="2560" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets, dan merk voor [!UICONTROL Profile].
2. Gegevens zijn geïntegreerd in Experience Platform via Web SDK, Mobile Edge SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U laadt profielen in Real-Time CDP en bouwt governancebeleid om verantwoord gebruik te garanderen.
4. U maakt doelgroepen in de lijst met profielen om te controleren of een **klant** heeft in de laatste drie dagen een betrokkenheid gemaakt.
5. U maakt een terugkerende reis in [!DNL Adobe Journey Optimizer].
6. Werk zo nodig met de **gegevenspartner** voor de activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert de toestemming en verzendt de diverse gevormde acties.

>[!TAB Afgekloonde Kart-reis]

De niet langer gebruikte reisweg is gericht op producten die in de wagen zijn geplaatst maar nog niet op de website en mobiele app zijn gekocht. Bovendien worden campagnes voor betaalde media gestart en gestopt met deze methode.<p>![De klant verliet de reis van het karretje op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png "De klant verliet de reis van het karretje op hoog niveau visueel overzicht."){width="2560" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets, het merk voor [!UICONTROL Profile].
2. Gegevens zijn geïntegreerd in Experience Platform via Web SDK, Mobile Edge SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U laadt profielen in Real-Time CDP en bouwt governancebeleid om verantwoord gebruik te garanderen.
4. U maakt doelgroepen in de lijst met profielen om te controleren of een **klant** heeft een artikel in hun winkelwagentje geplaatst, maar heeft de aankoop niet voltooid. De **[!UICONTROL Add to cart]** de gebeurtenis tikt van een tijdopnemer die 30 minuten wacht, dan controleert aankoop. Als er geen aankoop is gedaan, wordt de **klant** wordt toegevoegd aan de **[!UICONTROL Abandon Cart]** publiek.
5. Je maakt een verlaten cartooptocht in [!DNL Adobe Journey Optimizer].
6. Werk zo nodig met de **gegevenspartner** voor de activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert de toestemming en verzendt de diverse gevormde acties.

>[!TAB Reis voor orderbevestiging]

De reis voor het bevestigen van bestellingen is vooral gericht op productaankopen via de website en de mobiele app.<p>![Bevestiging van de reis van de bestelbevestiging van de klant op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Bevestiging van de reis van de bestelbevestiging van de klant op hoog niveau visueel overzicht."){width="2560" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets, dan merk voor [!UICONTROL Profile].
2. Gegevens zijn geïntegreerd in Experience Platform via Web SDK, Mobile Edge SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U laadt profielen in Real-Time CDP en bouwt governancebeleid om verantwoord gebruik te garanderen.
4. U maakt een bevestigingstraject in [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] verzendt een bericht van de ordesbevestiging gebruikend het aangewezen kanaal.

>[!ENDTABS]

## Hoe het gebruiksgeval te bereiken {#achieve-use-case-instruction}

Lees de onderstaande secties door om alle stappen in de bovenstaande overzichten op hoog niveau te voltooien. Deze bevatten koppelingen naar meer informatie en meer gedetailleerde instructies.

### UI-functionaliteit en elementen die u gebruikt {#ui-functionality-and-elements}

Wanneer u de stappen voor het implementeren van het hoofdlettergebruik uitvoert, maakt u gebruik van de Real-Time CDP-functionaliteit en UI-elementen die aan het begin van dit document worden vermeld. Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

### Een schemaontwerp maken en veldgroepen opgeven {#schema-design}

De middelen van het Gegevensmodel van de ervaring (XDM) worden beheerd in [!UICONTROL Schemas] werkruimte in [!DNL Adobe Experience Platform]. U kunt de belangrijkste bronnen bekijken en verkennen die door [!DNL Adobe] (bijvoorbeeld [!UICONTROL Field Groups]) en maak aangepaste bronnen en schema&#39;s voor uw organisatie.

Meer informatie over het maken van [schema&#39;s](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl), lees de [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md)

Er zijn vier schemaontwerpen die voor het re-engagement gebruikscase worden gebruikt. Voor elk schema moeten specifieke velden worden ingesteld en moeten bepaalde velden worden ingesteld die sterk worden aanbevolen.

#### Klantkenmerkenschema

Dit schema wordt gebruikt om de profielgegevens te structureren en van verwijzingen te voorzien die omhoog uw klanteninformatie maken. Deze gegevens worden doorgaans opgenomen in [!DNL Adobe Experience Platform] via uw CRM of vergelijkbaar systeem en is noodzakelijk om klantgegevens te raadplegen die worden gebruikt voor personalisatie, marketingtoestemming en verbeterde segmenteringsmogelijkheden.

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

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website en/of bijbehorende digitale platforms voorkomt. Deze gegevens worden doorgaans opgenomen in [!DNL Adobe Experience Platform] via Web SDK en is noodzakelijk om de verschillende doorblader en omzettingsgebeurtenissen van verwijzingen te voorzien die voor het teweegbrengen van reizen, gedetailleerde online klantenanalyse, en verbeterde segmenteringsmogelijkheden worden gebruikt.

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
| `endUserIDs._experience.mcid.authenticatedState` | Vereist | [!DNL Adobe] Status geverifieerd voor Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.id` | Vereist | [!DNL Adobe] Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.namespace.code` | Vereist | [!DNL Adobe] Marketing Cloud-id (MCID) naamruimtecode. |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Offline transactieschema van de klant

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op platforms buiten uw website voorkomt. Deze gegevens worden doorgaans opgenomen in [!DNL Adobe Experience Platform] van een POS (of vergelijkbaar systeem) en meestal gestreamd naar Platform via een API-verbinding. Zijn doel is de diverse off-line omzettingsgebeurtenissen van verwijzingen te voorzien die voor het teweegbrengen van reizen, diepe online en off-line klantenanalyse, en verbeterde segmenteringsmogelijkheden worden gebruikt.

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

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Adobe webverbindingsschema

>[!NOTE]
>
>Dit is een optionele implementatie als u de [!DNL Adobe Analytics Data Connector].

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website en/of bijbehorende digitale platforms voorkomt. Dit schema is gelijkaardig aan het schema van de Transacties van de Klant Digitale maar verschilt in die zin dat het bedoeld is om te worden gebruikt wanneer het Web SDK geen optie voor gegevensinzameling is; zo, is dit schema nodig wanneer u het gebruikt [!DNL Adobe Analytics Data Connector] om uw online gegevens te verzenden naar [!DNL Adobe Experience Platform] hetzij als primaire of secundaire gegevensstroom.

De [!DNL Adobe] webconnectorschema wordt voorgesteld door een [!UICONTROL XDM ExperienceEvent] klasse, die de volgende veldgroepen bevat:

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
| `endUserIDs._experience.mcid.authenticatedState` | Vereist | [!DNL Adobe] Status geverifieerd voor Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.id` | Vereist | [!DNL Adobe] Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| `endUserIDs._experience.mcid.namespace.code` | Vereist | [!DNL Adobe] Marketing Cloud-id (MCID) naamruimtecode. |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

### Een dataset maken op basis van een schema {#dataset-from-schema}

Een dataset is een opslag en beheersstructuur voor een groep gegevens. Elk schema voor intelligente reizen voor opnieuw engagement heeft één dataset.

Voor meer informatie over het maken van een [gegevensset](/help/catalog/datasets/overview.md) in een schema, lees de [UI-gids voor gegevensbestanden](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Gelijkaardig aan de stap om een schema tot stand te brengen, moet u toelaten dat de dataset in het Profiel van de Klant in real time wordt omvat. Voor meer informatie over het toelaten van de dataset voor gebruik in het Profiel van de Klant In real time, lees [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Privacy, toestemming en gegevensbeheer {#privacy-consent}

#### Toestemmingsbeleid

>[!IMPORTANT]
>
>Het bieden van klanten de mogelijkheid om zich af te melden van het ontvangen van communicatie van een merk is een wettelijke vereiste, en het verzekeren van deze keuze wordt gerespecteerd. Meer informatie over de toepasselijke wetgeving vindt u in het [Overzicht van privacyregels](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Bij het maken van een pad voor opnieuw toewijzen, geldt het volgende [toestemmingsbeleid](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) dient te worden overwogen:

* Indien `consents.marketing.email.val = "Y"` vervolgens kunt u e-mailen
* Indien `consents.marketing.sms.val = "Y"` Dan kan SMS
* Indien `consents.marketing.push.val = "Y"` vervolgens kan duwen
* Indien `consents.share.val = "Y"` kan vervolgens adverteren

#### Label voor gegevensbeheer en handhaving

Bij het maken van een pad voor opnieuw toewijzen, geldt het volgende [Labels voor gegevensbeheer](/help/data-governance/labels/overview.md) dient te worden overwogen:

* Persoonlijke e-mailadressen worden gebruikt als direct identificeerbare gegevens die worden gebruikt om een specifieke persoon te identificeren of contact met hem te krijgen in plaats van met een apparaat.
   * `personalEmail.address = I1`

#### Marketingsbeleid

Er zijn geen [marketingbeleid](/help/data-governance/policies/overview.md) die nodig zijn voor het opnieuw in dienst nemen van een dienstverband, moeten echter de volgende punten als gewenst worden beschouwd:

* Gevoelige gegevens beperken
* Onsite reclame beperken
* E-maildoelen beperken
* Doelstelling voor meerdere sites beperken
* Het combineren van rechtstreeks identificeerbare gegevens met anonieme gegevens beperken

### Een doelgroep maken {#create-audience}

#### Audience creation for brand re-engagement trip

Bij de reactiereizen worden doelgroepen gebruikt om specifieke kenmerken of gedragingen te definiëren die door een subset van profielen uit uw profielarchief worden gedeeld, zodat een verhandelbare groep personen kan worden onderscheiden van uw klantenbasis. Soorten publiek kan op meerdere manieren worden gemaakt [!DNL Adobe Experience Platform].

Voor meer informatie over het maken van een publiek leest u de [UI-gids voor de service Publiek](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Voor meer informatie over hoe u direct samenstelt [Soorten publiek](/help/segmentation/home.md), lees de [Handleiding voor compositie van publiek](/help/segmentation/ui/audience-composition.md).

Voor meer informatie over hoe te om publiek door Platform-afgeleide segmentdefinities te bouwen, lees [Handleiding voor de gebruikersinterface van Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

Dit publiek wordt gemaakt als een uitbreiding op het klassieke scenario &#39;Kart Abandenvironment&#39;. Terwijl het verlaten van het winkelwagentje zich doorgaans concentreert op een toevoeging van winkelwagentjes zonder een latere aankoop binnen een bepaalde periode, zoekt dit publiek naar een eerdere betrokkenheid, met name diegenen die mogelijk door een bepaald product hebben gebladerd maar het niet aan hun winkelwagentje hebben toegevoegd en binnen een bepaalde tijd geen vervolgactiviteit op uw site hadden. Dit publiek helpt om uw merk &quot;bovenaan&quot;voor klanten te houden die aan deze inclusiecriteria voldoen en kan ook voor klanten worden gebruikt waarvan digitale eigenschappen van een traditioneel e-commercemodel kunnen verschillen.

De volgende gebeurtenissen worden gebruikt voor de reis van de herbetrokkenheid waar de gebruikers producten online bekeken en in de komende 24 uur niet aan het winkelwagentje toegevoegd, gevolgd door geen merkbetrokkenheid in de drie dagen daarna.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

De beschrijving voor de reis van de herinrichting ziet er als volgt uit:

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Afgekloonde Kart-reis]

Dit publiek wordt gemaakt ter ondersteuning van het klassieke scenario &#39;Kart Abandenvironment&#39;. Het doel is om klanten te vinden die een product aan hun winkelwagentje hebben toegevoegd maar uiteindelijk niet met een aankoop hebben gevolgd. Dit publiek zal niet alleen uw merk &quot;bovenaan&quot;voor uw klanten houden maar ook de producten die zij zonder een verdere aankoop hebben verlaten.

De volgende evenementen worden gebruikt voor de verlaten cartograaf, waar gebruikers een product aan hun karretje hebben toegevoegd, maar de aankoop niet hebben voltooid of hun karretje in de afgelopen 24 uur niet hebben gewist.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `EventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

De beschrijving van de verlaten wagenreis ziet er als volgt uit:

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Reis voor orderbevestiging]

Voor deze reis is geen publiek nodig.

>[!ENDTABS]

### Reisinstallatie in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] omvat niet alles die in de diagrammen wordt getoond. Alles [betaalde mediasleutels](/help/destinations/catalog/social/overview.md) worden gemaakt in [!UICONTROL Destinations].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) helpt u verbonden, contextafhankelijke en persoonlijke ervaringen aan uw klanten te leveren. De reis van de klant is het volledige proces van interactie van een klant met het merk. Voor elke gebruiksreis is specifieke informatie vereist. Hieronder worden de precieze gegevens vermeld die voor elke tak van de Reis nodig zijn.

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

De reis om opnieuw aan de slag te gaan richt verlaten product het doorbladeren op zowel de website als mobiele app.<p>![Intelligente reactiereis op hoog niveau van visueel overzicht van de klant.](../intelligent-re-engagement/images/re-engagement-journey.png "Intelligente reactiereis op hoog niveau van visueel overzicht van de klant."){width="2560" zoomable="yes"}</p>

+++Gebeurtenissen

* Gebeurtenis 1: productweergaven
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

* Gebeurtenis 2: Toevoegen aan winkelwagentje
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

* Gebeurtenis 3: Betrokkenheid merk
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
      * Schema: offline transacties van klanten
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

De niet langer gebruikte reisweg is gericht op producten die in de wagen zijn geplaatst maar nog niet op de website en mobiele app zijn gekocht.<p>![De klant verliet de reis van het karretje op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png "De klant verliet de reis van het karretje op hoog niveau visueel overzicht."){width="2560" zoomable="yes"}</p>

+++Gebeurtenissen

* Gebeurtenis 2: Toevoegen aan winkelwagentje
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

* Gebeurtenis 4: online aankopen
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

* Gebeurtenis 3: Betrokkenheid merk
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
   * Schema: offline transacties van klanten
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Voorwaarde: winkelwagentje wordt gewist sinds de laatste keer dat het winkelwagentje werd verlaten:
   * Schema: digitale transacties van klanten
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

De reis voor het bevestigen van bestellingen is vooral gericht op productaankopen via de website en de mobiele app.<p>![Bevestiging van de reis van de bestelbevestiging van de klant op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Bevestiging van de reis van de bestelbevestiging van de klant op hoog niveau visueel overzicht."){width="2560" zoomable="yes"}</p>

+++Gebeurtenissen

* Gebeurtenis 4: online aankopen
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

Meer informatie over het maken van reizen in [!DNL Adobe Journey Optimizer], lees de [Aan de slag met reishandleiding](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Betaalde mediadeskundigen instellen in bestemmingen {#paid-media-ads}

Het bestemmingskader wordt gebruikt voor betaalde media advertenties. Zodra de toestemming is gecontroleerd verzendt het naar de diverse gevormde bestemmingen. Voor meer informatie over bestemmingen, lees [Overzicht van doelen](/help/destinations/home.md) document.

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
