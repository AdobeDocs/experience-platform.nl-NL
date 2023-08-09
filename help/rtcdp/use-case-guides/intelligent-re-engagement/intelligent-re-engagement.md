---
title: Intelligente re-engagement
description: Lever boeiende en verbonden ervaringen tijdens de belangrijkste omzettingsmomenten om intelligent onregelmatige klanten opnieuw aan te sluiten.
hide: true
hidefromtoc: true
source-git-commit: 4f0902b874d5e8179c009ad3b603e008b9a22bb4
workflow-type: tm+mt
source-wordcount: '3440'
ht-degree: 2%

---

# Inzet uw klanten op intelligente wijze opnieuw aan om terug te keren

Dankzij intelligente re-engagement kunt u een op maat gemaakte, cross-channel druppelcampagne opzetten om klanten ervan te overtuigen een bepaalde actie uit te voeren. De campagne is bedoeld om gedurende een beperkte periode te werken, waaronder het verzenden van klanten die intent e-mails, sms&#39;en en betaalde advertenties hebben getoond. Zodra de klant de juiste actie heeft ondernomen, wordt de verschuivingscampagne onmiddellijk beëindigd.

![Stap voor stap, intelligent overzicht op hoog niveau van de hernieuwde betrokkenheid.](../intelligent-re-engagement/images/step-by-step.png)

## Vereisten en planning {#prerequisites-and-planning}

Wanneer u de stappen voor het implementeren van het gebruiksscenario uitvoert, maakt u gebruik van de volgende Real-Time CDP-functionaliteit en UI-elementen (vermeld in de volgorde waarin u deze wilt gebruiken). Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Gegevens worden samengevoegd over verschillende gegevensbronnen om de campagne te voeden. Deze gegevens worden vervolgens gebruikt om het campagnepubliek te maken en gepersonaliseerde gegevenselementen aan de oppervlakte te brengen die in de e-mail en de webpromo-tegels worden gebruikt (bijvoorbeeld naam of aan account gerelateerde informatie). CDP wordt ook gebruikt om het publiek over e-mail en het Web (via Adobe Target) te activeren.
   * [Schema&#39;s](/help/xdm/home.md)
   * [Profielen](/help/profile/home.md)
   * [Doelgroepen](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Trigger voor gebeurtenis of publiek](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Soorten publiek/Gebeurtenissen](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Reishandelingen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

Er zijn drie reizen gemaakt om opnieuw aan de slag te gaan.

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

De reis van de re-engagement richt verlaten productdoorbladeren op zowel de website als app. Deze reis wordt geactiveerd wanneer een product is bekeken zonder dat het is aangeschaft of aan de wagen is toegevoegd. De merkbetrokkenheid wordt geactiveerd na drie dagen als er geen lijst is toegevoegd binnen de laatste 24 uur.

![Intelligente reactiereis op hoog niveau van visueel overzicht van de klant.](../intelligent-re-engagement/images/re-engagement-journey.png)

1. Gegevens worden geaggregeerd in Web SDK/Mobile SDK/Edge Network API-opname via Edge Network (voorkeursmethode).
2. Als **klant** maakt u gegevenssets waarvoor [!UICONTROL Profile].
3. Als **klant**, laadt u profielen in Real-Time CDP en bouwt u beleidsregels voor verantwoord gebruik.
4. Als **klant**, maakt u doelgroepen in de lijst met profielen om te controleren of een **user** heeft in de afgelopen drie dagen een merkbetrokkenheid gemaakt.
5. Als **klant**, maakt u een terugvlucht in Adobe Journey Optimizer.
6. Werk zo nodig met de **gegevenspartner** voor activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. Adobe Journey Optimizer controleert op toestemming en stuurt de verschillende geconfigureerde acties door.

>[!TAB Afgekloonde Kart-reis]

Deze verlaten reis van het karretje richt producten die in het karretje zijn geplaatst maar niet op zowel de website als de app gekocht. Gebruikt voor het starten en stoppen van campagnes voor betaalde media

![De klant verliet de reis van het karretje op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png)

1. Gegevens worden geaggregeerd in Web SDK/Mobile SDK/Edge Network API-opname via Edge Network (voorkeursmethode).
2. Als **klant** maakt u gegevenssets waarvoor [!UICONTROL Profile].
3. Als **klant**, laadt u profielen in Real-Time CDP en bouwt u beleidsregels voor verantwoord gebruik.
4. Als **klant**, maakt u doelgroepen in de lijst met profielen om te controleren of een **user** heeft een artikel in hun winkelwagentje geplaatst, maar heeft de aankoop niet voltooid. De **[!UICONTROL Add to cart]** de gebeurtenis tikt van een tijdopnemer die 30 minuten wacht, dan controleert aankoop. Als er geen aankoop is gedaan, wordt de **user** wordt toegevoegd aan de **[!UICONTROL Abandon Cart]** publiek.
5. Als **klant**, maakt u een verlaten wagentje in Adobe Journey Optimizer
6. Werk zo nodig met de **gegevenspartner** voor activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. Adobe Journey Optimizer controleert op toestemming en stuurt de verschillende geconfigureerde acties door.

>[!TAB Reis voor orderbevestiging]

Deze bestelbevestiging is bedoeld voor productaankopen op zowel de website als de app.

![Bevestiging van de reis van de bestelbevestiging van de klant op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png)

1. Gegevens worden geaggregeerd in Web SDK/Mobile SDK/Edge Network API-opname via Edge Network (voorkeursmethode).
2. Als **klant** maakt u gegevenssets waarvoor [!UICONTROL Profile].
3. Als **klant**, laadt u profielen in Real-Time CDP en bouwt u beleidsregels voor verantwoord gebruik.
4. Als **klant**, maakt u doelgroepen in de lijst met profielen om te controleren of een **user** heeft een aankoop gedaan.
5. Als **klant**, maakt u een bevestigingsreis in Adobe Journey Optimizer.
6. Adobe Journey Optimizer stuurt via het voorkeurskanaal een bericht ter bevestiging van de bestelling.

>[!ENDTABS]

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in de bovenstaande overzichten op hoog niveau te voltooien.

### UI-functionaliteit en elementen die u gebruikt {#ui-functionality-and-elements}

Wanneer u de stappen voor het implementeren van het gebruiksscenario uitvoert, maakt u gebruik van de volgende Real-Time CDP-functionaliteit en UI-elementen (vermeld in de volgorde waarin u deze wilt gebruiken). Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [Schema&#39;s](/help/xdm/home.md)
* [Profielen](/help/profile/home.md)
* [Gegevenssets](/help/catalog/datasets/overview.md)
* [Doelgroepen](/help/segmentation/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
* [Doelen](/help/destinations/home.md)

### Een schemaontwerp maken en veldgroepen opgeven

De middelen van het Gegevensmodel van de ervaring (XDM) worden beheerd in [!UICONTROL Schemas] in Adobe Experience Platform. U kunt kernmiddelen bekijken en onderzoeken die door Adobe worden verstrekt, en douanemiddelen en schema&#39;s voor uw organisatie tot stand brengen.

Voer de volgende stappen uit om een schema te maken:

1. Navigeren naar **[!UICONTROL Data Management]** > **[!UICONTROL Schemas]** en selecteert u **[!UICONTROL Create schema]**.
2. Selecteer **[!UICONTROL XDM Individual Profile]/[!UICONTROL XDM ExperienceEvent]**.
3. Navigeren naar **[!UICONTROL Field groups]** en selecteert u **[!UICONTROL Add]**.
4. Gebruik het zoekvak om de veldgroep te zoeken en te selecteren en selecteer vervolgens **[!UICONTROL Add field groups]**.
5. Geef uw schema een naam en naar keuze een beschrijving.
6. Selecteer **[!UICONTROL Save]**.

![Een opname van de stappen om een schema te maken.](../intelligent-re-engagement/images/create-a-schema.gif)

Lees voor meer informatie over het maken van schema&#39;s de [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md)

Er zijn vier schemaontwerpen die voor de heraannemingsreis worden gebruikt.

Voor elk schema moeten specifieke velden worden ingesteld, evenals enkele velden die sterk worden aanbevolen.

#### Veldgroepvereisten voor het schema voor klantkenmerken

Het schema voor klantkenmerken is een [!UICONTROL XDM Individual Profile] schema, dat de volgende veldgroepen bevat:

+++Persoonlijke Contactgegevens (Veldgroep)

[Persoonlijke contactgegevens](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel van Afzonderlijke XDM die de contactinformatie voor een individuele persoon beschrijft.

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| mobilePhone.number | Vereist | Het mobiele telefoonnummer van de persoon, dat wordt gebruikt voor SMS. |
| personalEmail.address | Vereist | Het e-mailadres van de persoon. |

+++

+++Demografische details (veldgroep)

[Demografische details](/help/xdm/field-groups/profile/demographic-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel Individual XDM. De veldgroep biedt een persoonlijk object op hoofdniveau, waarvan de subvelden informatie over een individuele persoon beschrijven.

| Velden | Vereiste |
| --- | --- |
| person.name.firstName | Voorgesteld |
| person.name.lastName | Voorgesteld |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

[Kenmerken externe bronsysteemcontrole](/help/xdm/data-types/external-source-system-audit-attributes.md) is een standaardgegevenstype van de Gegevens van de Ervaring Model (XDM) dat controledetails over een extern bronsysteem vangt.

+++

+++Groepen van het Toegelaten en van het Referentieveld (de Groep van het Gebied)

[De inhoud en voorkeuren](/help/xdm/field-groups//profile/consents.md) veldgroep biedt één objecttype veld, toestemmingen, voor het vastleggen van toestemmings- en voorkeursgegevens.

| Velden | Vereiste |
| --- | --- |
| consents.marketing.email.val | Vereist |
| consents.marketing.preferred | Vereist |
| consents.marketing.push.val | Vereist |
| consents.marketing.sms.val | Vereist |
| consents.personalize.content.val | Vereist |
| consents.share.val | Vereist |

+++

+++Details van de Test van het Profiel (de Groep van het Gebied)

Deze veldgroep wordt gebruikt voor beste praktijken.

+++

![Schema met klantkenmerken waarin de lijst met veldgroepen wordt gemarkeerd.](../intelligent-re-engagement/images/customer-attributes.png)

#### Veldgroepvereisten voor het schema voor digitale transacties van de klant

Het schema voor digitale transacties van de klant is een [!UICONTROL XDM ExperienceEvent] schema, dat de volgende veldgroepen bevat:

+++Adobe Experience Platform Web SDK ExperienceEvent (veldgroep)

| Velden | Vereiste |
| --- | --- |
| device.model | Voorgesteld |
| environment.browserDetails.userAgent | Voorgesteld |

+++

+++Webdetails (Veldgroep)

Webdetails is een standaardschemaveldgroep voor de klasse XDM ExperienceEvent die wordt gebruikt om informatie te beschrijven over webdetailgebeurtenissen zoals interactie, paginadetails en referentie.

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | Voorgesteld | De id voor de webkoppeling of URL die overeenkomt met de interactie. |
| web.webInteraction.linkClicks.value | Voorgesteld | Het aantal klikken voor de webkoppeling of URL die overeenkomt met de interactie. |
| web.webInteraction.name | Voorgesteld | De naam van de webpagina. |
| web.webInteraction.URL | Voorgesteld | De URL voor de webpagina. |
| web.webPageDetails.name | Voorgesteld | De naam van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| web.webPageDetails.URL | Voorgesteld | De URL van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| web.webReferrer.URL | Voorgesteld | Beschrijft de referentie van een Webinteractie, die URL is een bezoeker van onmiddellijk vóór de huidige Webinteractie kwam werd geregistreerd. |

+++

+++Consumer Experience Event (veldgroep)

| Velden | Vereiste |
| --- | --- |
| commerce.cart.cartID | Voorgesteld |
| commerce.cart.cartSource | Voorgesteld |
| commerce.cartAbandons.id | Voorgesteld |
| commerce.cartAbandons.value | Voorgesteld |
| commerce.order.orderType | Voorgesteld |
| commerce.order.payments.paymentAmount | Voorgesteld |
| commerce.order.payments.paymentType | Voorgesteld |
| commerce.order.payments.transactionID | Voorgesteld |
| commerce.order.priceTotal | Voorgesteld |
| commerce.order.purchaseID | Voorgesteld |
| commerce.productListAdds.id | Voorgesteld |
| commerce.productListAdds.value | Voorgesteld |
| commerce.productListOpens.id | Voorgesteld |
| commerce.productListOpens.value | Voorgesteld |
| commerce.productListRemoval.id | Voorgesteld |
| commerce.productListRemoval.value | Voorgesteld |
| commerce.productListViews.id | Voorgesteld |
| commerce.productListViews.value | Voorgesteld |
| commerce.productViews.id | Voorgesteld |
| commerce.productViews.value | Voorgesteld |
| commerce.purchases.id | Voorgesteld |
| commerce.purchases.value | Voorgesteld |
| marketing.campaignGroup | Voorgesteld |
| marketing.campaignName | Voorgesteld |
| marketing.trackingCode | Voorgesteld |
| productListItems.name | Voorgesteld |
| productListItems.priceTotal | Voorgesteld |
| productListItems.product | Voorgesteld |
| productListItems.quantity | Voorgesteld |

+++

+++Details eindgebruiker-id (veldgroep)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| endUserIDs._experience.ease.authenticatedState | Vereist | Status van e-mailadres voor eindgebruiker is geverifieerd. |
| endUserIDs._experience.emailid.id | Vereist | E-mailadres van eindgebruiker. |
| endUserIDs._experience.ease.namespace.code | Vereist | Naamruimte-code van e-mailadres van eindgebruiker. |
| endUserIDs._experience.mcid.authenticatedState | Vereist | Status geverifieerd voor Adobe Marketing Cloud ID (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| endUserIDs._experience.mcid.id | Vereist | Adobe Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| endUserIDs._experience.mcid.namespace.code | Vereist | Adobe Marketing Cloud ID (MCID)-naamruimtecode. |

+++

+++Klasse-waarde (veldgroep)

| Velden | Vereiste |
| --- | --- |
| eventType | Vereist |
| timestamp | Vereist |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

![Schema voor digitale transacties van de klant waarin de lijst met veldgroepen wordt gemarkeerd.](../intelligent-re-engagement/images/customer-digital-transactions.png)

#### Veldgroepvereisten voor het schema voor offlinetransacties van de klant

Het schema voor offline transacties van de klant is een [!UICONTROL XDM ExperienceEvent] schema, dat de volgende veldgroepen bevat:

+++Details van de Handel (de Groep van het Gebied)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| commerce.cart.cartID | Vereist | Een id voor het winkelwagentje. |
| commerce.order.orderType | Vereist | Een object dat het type productvolgorde beschrijft. |
| commerce.order.payments.paymentAmount | Vereist | Een object dat het bedrag van de productbestelling beschrijft. |
| commerce.order.payments.paymentType | Vereist | Een object dat een beschrijving geeft van het type productorderbetaling. |
| commerce.order.payments.transactionID | Vereist | Een transactie-id voor een objectproduct. |
| commerce.order.purchaseID | Vereist | Een aankoop-id voor de objectorder. |
| productListItems.name | Vereist | Een lijst met itemnamen die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| productListItems.priceTotal | Vereist | De totale prijs van de lijst met objecten die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| productListItems.product | Vereist | Het geselecteerde product of de producten. |
| productListItems.quantity | Vereist | De hoeveelheid lijst met objecten die het product of de producten vertegenwoordigt die door een klant is/zijn geselecteerd. |

+++

+++Persoonlijke Contactgegevens (Veldgroep)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| mobilePhone.number | Vereist | Het mobiele telefoonnummer van de persoon, dat wordt gebruikt voor SMS. |
| personalEmail.address | Vereist | Het e-mailadres van de persoon. |

+++

+++Klasse-waarde (veldgroep)

| Velden | Vereiste |
| --- | --- |
| eventType | Vereist |
| timestamp | Vereist |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

![Offline transactieschema van de klant waarin de lijst met veldgroepen wordt gemarkeerd.](../intelligent-re-engagement/images/customer-offline-transactions.png)

#### Veldgroepvereisten voor het schema voor de Adobe-webconnector

Het schema van de Adobe-webconnector is een [!UICONTROL XDM ExperienceEvent] schema, dat de volgende veldgroepen bevat:

De veldgroepen die vereist zijn voor Experience Event-schema voor Adobe Analytics Data Feed zijn:

+++Adobe Analytics ExperienceEvent-sjabloon (veldgroep)

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | Voorgesteld | De id voor de webkoppeling of URL die overeenkomt met de interactie. |
| web.webInteraction.linkClicks.value | Voorgesteld | Het aantal klikken voor de webkoppeling of URL die overeenkomt met de interactie. |
| web.webInteraction.name | Voorgesteld | De naam van de webpagina. |
| web.webInteraction.URL | Voorgesteld | De URL voor de webpagina. |
| web.webPageDetails.name | Voorgesteld | De naam van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| web.webPageDetails.URL | Voorgesteld | De URL van de webpagina waarop de webinteractie heeft plaatsgevonden. |
| web.webReferrer.URL | Voorgesteld | Beschrijft de referentie van een Webinteractie, die URL is een bezoeker van onmiddellijk vóór de huidige Webinteractie kwam werd geregistreerd. |
| commerce.cart.cartID | Voorgesteld | |
| commerce.cart.cartSource | Voorgesteld | |
| commerce.cartAbandons.id | Voorgesteld | |
| commerce.cartAbandons.value | Voorgesteld | |
| commerce.order.orderType | Voorgesteld | |
| commerce.order.payments.paymentAmount | Voorgesteld | |
| commerce.order.payments.paymentType | Voorgesteld | |
| commerce.order.payments.transactionID | Voorgesteld | |
| commerce.order.priceTotal | Voorgesteld | |
| commerce.order.purchaseID | Voorgesteld | |
| commerce.productListAdds.id | Voorgesteld | |
| commerce.productListAdds.value | Voorgesteld | |
| commerce.productListOpens.id | Voorgesteld | |
| commerce.productListOpens.value | Voorgesteld | |
| commerce.productListRemoval.id | Voorgesteld | |
| commerce.productListRemoval.value | Voorgesteld | |
| commerce.productListViews.id | Voorgesteld | |
| commerce.productListViews.value | Voorgesteld | |
| commerce.productViews.id | Voorgesteld | |
| commerce.productViews.value | Voorgesteld | |
| commerce.purchases.id | Voorgesteld | |
| commerce.purchases.value | Voorgesteld | |
| marketing.campaignGroup | Voorgesteld | |
| marketing.campaignName | Voorgesteld | |
| marketing.trackingCode | Voorgesteld | |
| productListItems.name | Voorgesteld | |
| productListItems.priceTotal | Voorgesteld | |
| productListItems.product | Voorgesteld | |
| productListItems.quantity | Voorgesteld | |
| endUserIDs._experience.ease.authenticatedState | Vereist | Status van e-mailadres voor eindgebruiker is geverifieerd. |
| endUserIDs._experience.emailid.id | Vereist | E-mailadres van eindgebruiker. |
| endUserIDs._experience.ease.namespace.code | Vereist | Naamruimte-code van e-mailadres van eindgebruiker. |
| endUserIDs._experience.mcid.authenticatedState | Vereist | Status geverifieerd voor Adobe Marketing Cloud ID (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| endUserIDs._experience.mcid.id | Vereist | Adobe Marketing Cloud-id (MCID). De MCID wordt nu ECID (Experience Cloud-id) genoemd. |
| endUserIDs._experience.mcid.namespace.code | Vereist | Adobe Marketing Cloud ID (MCID)-naamruimtecode. |

+++

+++Klasse-waarde (veldgroep)

| Velden | Vereiste |
| --- | --- |
| eventType | Vereist |
| timestamp | Vereist |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

De externe Attributen van de Controle van het Systeem van de Bron is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

![Het schema van de Webschakelaar van de Adobe die de lijst van gebiedsgroepen benadrukken.](../intelligent-re-engagement/images/adobe-web-connector.png)

>[!ENDTABS]

### Een dataset maken op basis van een schema

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Voor intelligente reizen van de re-engagement, zal elk schema één dataset hebben.

Om een dataset van een schema tot stand te brengen, voltooi de hieronder stappen:

1. Navigeren naar **[!UICONTROL Data Management]** > **[!UICONTROL Datasets]** en selecteert u **[!UICONTROL Create dataset]**.
2. Selecteer **[!UICONTROL Create dataset from schema]**.
3. Selecteer het relevante vernieuwingsschema dat u hebt gemaakt.
4. Geef uw dataset een naam en naar keuze een beschrijving.
5. Selecteer **[!UICONTROL Finish]**.

![Een opname van de stappen om een dataset van een schema tot stand te brengen.](../intelligent-re-engagement/images/dataset-from-schema.gif)

Merk op dat gelijkend op de stap om een schema tot stand te brengen, u de dataset moet toelaten om in het Profiel van de Klant in real time worden omvat. Voor meer informatie over het toelaten van de dataset voor gebruik in het Profiel van de Klant In real time, lees [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Gegevensset inschakelen voor profiel.](../intelligent-re-engagement/images/enable-dataset-for-profile.png)

### Privacy, toestemming en gegevensbeheer

#### Toestemmingsbeleid

>[!IMPORTANT]
>
>Het bieden van klanten de mogelijkheid om zich af te melden van het ontvangen van communicatie van een merk is een wettelijke vereiste, en het verzekeren van deze keuze wordt gerespecteerd. Meer informatie over de toepasselijke wetgeving vindt u in het [Documentatie Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Het volgende beleid van instemming moet in aanmerking worden genomen en worden gebruikt bij het opzetten van een reis met een nieuwe overeenkomst:

* Als toestemmingen.marketing.email.val = &quot;Y&quot; dan kan e-mailen
* Als consents.marketing.sms.val = &quot;Y&quot;dan kan SMS
* Als consents.marketing.push.val = &quot;Y&quot; dan kan Push
* Als consents.share.val = &quot;Y&quot; dan kan Advertise
* Noodzaak gedefinieerd door implementatie door klant

#### DULE label en handhaving

Het persoonlijke e-mailadres wordt gebruikt als rechtstreeks identificeerbare gegevens die kunnen worden gebruikt om een specifieke persoon, in plaats van een apparaat, te identificeren of te contacteren.

* PersonalEmail.address = I1

#### Marketingsbeleid

Er is geen aanvullend marketingbeleid voor de herplaatsingsreizen, maar het volgende moet als gewenst worden beschouwd:

* Overweeg naar wens
* Gevoelige gegevens beperken
* Onsite reclame beperken
* E-maildoelen beperken
* Doelstelling voor meerdere sites beperken
* Het combineren van rechtstreeks identificeerbare gegevens met anonieme gegevens beperken

### Een doelgroep maken

Voer de onderstaande stappen uit om een publiek te maken:

1. Navigeren naar **[!UICONTROL Customer]** > **[!UICONTROL Audiences]** en selecteert u **[!UICONTROL Create audience]**.
2. Selecteren **[!UICONTROL Build rule]** en selecteert u **[!UICONTROL Create]**.
3. Navigeren naar **[!UICONTROL Field]** en selecteert u **[!UICONTROL Events]** tab.
4. Navigeer of gebruik het zoekvak om het gebeurtenistype te zoeken en sleep dit vervolgens naar de builder. Voeg ten slotte gebeurtenisregels toe door gebeurtenistypen te slepen.
5. Geef uw schema een naam en naar keuze een beschrijving.
6. Selecteer **[!UICONTROL Save]**.

![Een opname van de stappen om een publiek te creëren.](../intelligent-re-engagement/images/create-an-audience.gif)

Voor meer informatie over hoe u een publiek kunt maken, leest u de [Handleiding voor de gebruikersinterface van Audience Builder](/help/segmentation/ui/segment-builder.md).

#### Audience creation for brand re-engagement trip

Het publiek voor elke reis in het kader van een nieuwe overeenkomst moet worden opgericht met specifieke evenementen voor segmentkwalificatie. Deze details zijn te vinden op de bijbehorende tabbladen voor elke reis.

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

De volgende gebeurtenissen worden gebruikt voor de reis van de herbetrokkenheid waar de gebruikers producten online bekeken en in de komende 24 uur niet aan het winkelwagentje toegevoegd, gevolgd door geen merkbetrokkenheid in de drie dagen daarna.

Neem een publiek op met ten minste 1 gebeurtenis EventType = ProductViews en ten minste 1 gebeurtenis (EventType is niet gelijk aan commerce.productListAdds) die zich in de afgelopen 24 uur of uren voordoet en na 3 dagen geen gebeurtenis heeft waarbij (EventType = application.launch of web.webpagedetails.pageViews of commerce.purchase) en in de laatste 2 dagen optreedt.

![Een schermafbeelding van het publiek van de hernieuwde betrokkenheid waarin de set regels wordt getoond.](../intelligent-re-engagement/images/re-engagement-audience.png)

>[!TAB Afgekloonde Kart-reis]

De volgende gebeurtenissen worden gebruikt voor profielen die een product aan hun winkelwagentje hebben toegevoegd, maar de aanschaf van het product niet hebben voltooid of het karretje in de afgelopen 24 uur niet hebben gewist.

include EventType = commerce.productListAdds tussen 30 min en 1440 minuten vóór nu.
exclude EventType = commerce.aankopen 30 minuten vóór nu OF EventType = commerce.productListRemovals EN identiteitskaart van de Kar staat de Lijst van het Product toe Adds1 Kart ID (de inclusiegebeurtenis).

![Een schermafbeelding van het publiek van de hernieuwde betrokkenheid waarin de set regels wordt getoond.](../intelligent-re-engagement/images/abandoned-cart-audience.png)

>[!ENDTABS]

Voor meer informatie over het opbouwen van publiek, lees [Handleiding voor de gebruikersinterface van Audience Builder](/help/segmentation/ui/segment-builder.md).

### Reisinstallatie in Adobe Journey Optimizer

>[!NOTE]
>
>Adobe Journey Optimizer omvat niet alles die in de diagrammen bij de bovenkant van deze pagina wordt getoond. Alle betaalde mediaconsters worden gemaakt in [!UICONTROL Destinations].

Specifieke informatie is vereist voor de meervoudige ritten die elk geval van gebruik kan hebben. De specifieke gegevens die voor elke tak van de Reis worden vereist kunnen hieronder op de overeenkomstige lusjes worden gevonden.

>[!BEGINTABS]

>[!TAB Reis voor herbetrokkenheid]

![Overzicht van de door de klant opnieuw uitgevoerde reis in Adobe Journey Optimizer](../intelligent-re-engagement/images/re-engagement-ajo.png)

+++Gebeurtenissen

* Productweergaven
   * Schema: digitale transacties van klanten
   * Velden:
      * EventType
   * Voorwaarde:
      * EventType = commerce.productViews
      * Velden:
         * Commerce.productViews.id
         * Commerce.productViews.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * endUserIDs._experience.ease.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.ease.namespace.code
         * _id

* Toevoegen aan winkelwagentje
   * Schema: digitale transacties van klanten
   * Velden:
      * Type gebeurtenis
   * Voorwaarde:
      * Gebeurtenistype = commerce.productListAdds
      * Velden:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * commerce.cart.cartID
         * endUserIDs._experience.ease.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.ease.namespace.code
         * _id

* Betrokkenheid merk
   * Schema: digitale transacties van klanten
   * Velden:
      * EventType
   * Voorwaarde:
      * EventType in application.launch, commerce.purchase, web.webpagedetails.pageViews
      * Velden:
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.ease.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.ease.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++Key Reis-logica

* Logica voor reizen
   * Weergavegebeurtenis product

* Voorwaarden
   * Controleer of er minstens één online- of offline-aankoopgebeurtenis heeft plaatsgevonden sinds het product voor het laatst is weergegeven.
      * Schema: digitale transacties van klanten
      * eventType = commerce.purchase
      * timestamp > timestamp van het product laatst bekeken

   * Controleren op minstens één offlineaankoop sinds het product voor het laatst is weergegeven:
      * Schema: off-line transacties van de klant v.1
      * eventType = commerce.purchase
      * timestamp > timestamp van het product laatst bekeken

   * Voorwaarden - Selecteer het doelkanaal
      * Email
         * consents.marketing.email.val = y
      * Push
         * consents.marketing.push.val=y
      * Sms
         * consents.marketing.sms.val = y

   * Kanaalpersonalisatie
      * Inhoud van persoonlijke kanalen op basis van de productweergave.

+++

>[!TAB Afgekloonde Kart-reis]

![Door klant verlaten carterreis in Adobe Journey Optimizer overzicht](../intelligent-re-engagement/images/abandoned-cart-ajo.png)

+++Gebeurtenissen

* Toevoegen aan winkelwagentje
   * Schema: digitale transacties van klanten
   * Velden:
      * Type gebeurtenis
   * Voorwaarde:
      * Gebeurtenistype = commerce.productListAdds
      * Velden:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * commerce.cart.cartID
         * endUserIDs._experience.ease.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.ease.namespace.code
         * _id

* Online aankopen
   * Schema: digitale transacties van klanten
   * Velden:
      * Type gebeurtenis
   * Voorwaarde:
      * Gebeurtenistype = commerce.purchase
      * Velden:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * endUserIDs._experience.ease.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.ease.namespace.code
         * _id

* Betrokkenheid merk
   * Schema: digitale transacties van klanten
   * Velden:
      * EventType
   * Voorwaarde:
      * EventType in application.launch, commerce.purchase, web.webpagedetails.pageViews
      * Velden:
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.ease.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.ease.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++Key Journey Logic

* Logica voor reizen
   * Gebeurtenis AddToCart

* AuthenticatedState in authenticated

* Voorwaarde: offlineaankopen sinds de laatste keer dat het winkelwagentje werd verlaten:
   * Schema: off-line transacties van de klant v.1
   * eventType = commerce.purchase
   * timestamp > timestamp of cart was last left

* Voorwaarde: winkelwagentje wordt gewist sinds de laatste keer dat het winkelwagentje werd verlaten:
   * Schema: Digital Transactions van klant v.1
   * eventType = commerce.cartCleared
   * cartID (ID van het winkelwagentje)
   * timestamp > timestamp of cart was last left

* Doelkanaal selecteren (één of meerdere kanalen selecteren voor breder bereik)
   * Email
      * consents.marketing.email.val = y
   * Push
      * consents.marketing.push.val = y
   * Sms
      * consents.marketing.sms.val = y
   * Kanaalpersonalisatie
      * Geef informatie over de details van het winkelwagentje weer en kan meerdere producten in een tabelindeling weergeven.

+++

>[!TAB Reis voor orderbevestiging]

![Bevestigingstraject voor bestelling van klant in Adobe Journey Optimizer-overzicht](../intelligent-re-engagement/images/order-confirmation-ajo.png)

+++Gebeurtenissen

* Online aankopen
   * Schema: digitale transacties van klanten
   * Velden:
      * EventType
   * Voorwaarde:
      * Gebeurtenistype = commerce.purchase
      * Velden:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * timestamp
         * endUserIDs._experience.ease.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.ease.namespace.code
         * _id

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

### Betaalde advertentie voor media instellen in Doelen

Het bestemmingskader wordt gebruikt voor betaalde media advertenties. Zodra de toestemming is gecontroleerd zal het naar de diverse gevormde bestemmingen verzenden. Bijvoorbeeld direct mail, e-mail, enzovoort.

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
