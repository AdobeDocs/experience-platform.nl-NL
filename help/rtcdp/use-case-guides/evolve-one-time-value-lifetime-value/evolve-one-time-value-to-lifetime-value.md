---
title: Evolueer eenmalig klantenwaarde aan levenwaarde
description: Leer hoe u persoonlijke campagnes kunt maken om de beste complementaire producten of services te bieden op basis van de kenmerken, het gedrag en eerdere aankopen van een specifieke klant.
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '3154'
ht-degree: 0%

---

# Evolueer eenmalig klantenwaarde aan levenwaarde

>[!IMPORTANT]
> 
>* Deze pagina bevat een voorbeeldimplementatie van Real-Time CDP en Adobe Journey Optimizer om het beschreven gebruiksgeval te bereiken. Gebruik de cijfers, kwalificatiecriteria en andere velden op de pagina als richtlijn, niet als beschrijvende cijfers.
>* Als je deze kwestie wilt voltooien, moet je een licentie krijgen voor Real-Time CDP en Adobe Journey Optimizer. Lees meer in de [ eerste vereisten en planningssectie ](#prerequisites-and-planning) verder hieronder.

Implementeer de eenmalige klantwaarde tot het gebruiksscenario voor levenswaarde om de betrokkenheid van merken en merkloyaliteit te stimuleren. Bouw een verbonden klantenervaring op veelvoudige kanalen of reis door de macht van Experience Platform te gebruiken, die door [ Real-Time CDP ](/help/rtcdp/home.md) en [ Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home) wordt uitgebreid.

De personen waarop u zich richt, zijn de niet vaak voorkomende bezoekers van uw eigendommen die de afgelopen drie maanden een aantal aankopen hebben gedaan.

Overweeg deze klanten die uw eigenschappen bezoeken en sporadisch de producten of de diensten kopen die u aanbiedt. U kunt gepersonaliseerde campagnes willen tot stand brengen om aan deze klanten aan te trekken zodat uw merk hen op langere termijn waarde in plaats van eenmalig waarde kan aanbieden. Leer hoe u:

* Gegevens verzamelen en beheren
* Soorten publiek maken
* Reizen maken om deze doelgroepen in Adobe Journey Optimizer te bereiken en ze in Real-Time CDP te activeren.

![ Stap door stap Evolueer éénmalige waarde aan leven hoog niveau visueel overzicht.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## Vereisten en planning {#prerequisites-and-planning}

Rekening houdend met het feit dat u intern een bedrijfsdoel en een doelstelling hebt bepaald om merkloyaliteit te verhogen. Dit kan in het uitvoeren van een gebruiksgeval vertalen om klantenovereenkomst en loyaliteit te drijven.

Om dit te bereiken, bestaat de vereiste technologie uit twee Experience Platform apps [ Real-Time CDP ](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=nl) en [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=nl). Hieronder ziet u verschillende functionaliteit- en UI-elementen van de twee apps die u gebruikt bij de implementatie van het gebruiksscenario.

>[!TIP]
>
>Zorg ervoor dat u de noodzakelijke [ op attributen-gebaseerde toegangsbeheertoestemmingen ](/help/access-control/abac/end-to-end-guide.md) voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)] ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html): Integreer gegevens over gegevensbronnen om de campagne te voeden. Deze gegevens worden vervolgens gebruikt om het campagnepubliek te maken en gepersonaliseerde gegevenselementen aan de oppervlakte te brengen die worden gebruikt in de e-mail en de webpromo-elementen (bijvoorbeeld naam of aan account gerelateerde informatie). Tot slot wordt Real-Time CDP ook gebruikt om het publiek naar betaalmedia-bestemmingen te activeren.
   * [Schema&#39;s](/help/xdm/home.md)
   * [Profielen](/help/profile/home.md)
   * [Gegevenssets](/help/catalog/datasets/overview.md)
   * [Doelgroepen](/help/segmentation/home.md)
   * [Doelen](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer] ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html): De reizen van het ontwerp, opstellingstrekkers, en creeer het juiste overseinen om uw bezoekers te richten.
   * [ de Trigger van de Gebeurtenis of van het Publiek ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [ Soorten publiek en Gebeurtenissen ](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [ Reizen ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Real-Time CDP- en Journey Optimizer-architectuur

Hieronder volgt een architectuurweergave op hoog niveau van de verschillende componenten van Real-Time CDP en Journey Optimizer. In dit diagram ziet u hoe gegevens door de twee Experience Platform-apps lopen van gegevensverzameling tot het punt waar deze wordt geactiveerd via reizen of campagnes naar bestemmingen, om het gebruiksgeval te bereiken dat op deze pagina wordt beschreven.

![ Architectuur hoog niveau visueel overzicht.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

Hieronder volgt een overzicht op hoog niveau van de workflow, een combinatie van een reisworkflow en een activeringsworkflow.

In de onderstaande voorbeeldworkflow zoekt u naar klanten die aan bepaalde criteria voldoen en wilt u ze toestaan terug te keren naar uw website of app. U wilt ze op een reis plaatsen waar ze op een meer terugkerende manier terugkeren in plaats van een beperkte activiteit op uw eigendom. U probeert ze terug te krijgen naar uw eigendom en als ze weer terug zijn, kunt u ze de reis laten maken om terugkerende aankopen op uw site te doen. De campagne die hier wordt opgezet, is beperkt tot één overeenkomst met klanten per maand.

U begint door uw publiek van hoog-getaxeerde en laag-frequente klanten een bericht te verzenden. Controleer vervolgens of ze dit bericht de afgelopen dertig dagen hebben ontvangen. Als dat niet het geval is, kunt u ze op reis laten gaan over bijvoorbeeld een nieuw abonnementsprogramma. U kunt dan een paar dagen wachten (zeven dagen in dit voorbeeld). Als ze na deze keer het abonnement waarover u een bericht hebt verzonden niet hebben aangeschaft, kunt u betaalde mediaadvertenties leveren via bestemmingen. Als ze het abonnement hebben aangeschaft, kunt u ze een bestelbevestiging laten geven en zo de gebruikskwestie voltooien.

>[!IMPORTANT]
>
>Zoals verder hieronder op deze pagina wordt beschreven, door a [ specifieke groep van het toestemmingsgebied in uw schema ](#customer-attributes-schema) te hebben en door [ het uitvoeren van toestemmingsbeleid ](#privacy-consent), worden alle acties en werkschema&#39;s uitgevoerd op een privacy en toestemming-eerste manier.

>[!BEGINSHADEBOX]

![ Stap door stap Evolueer éénmalige waarde aan leven hoog niveau visueel overzicht.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. U maakt schema&#39;s en gegevenssets en markeert deze vervolgens voor [!UICONTROL Profile] .
2. Gegevens worden verzameld en in Experience Platform geïntegreerd via Web SDK, Mobile Edge SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U laadt profielen in Real-Time CDP en bouwt governancebeleid om verantwoord gebruik te garanderen.
4. U bouwt geconcentreerd publiek van de lijst van profielen om voor hoog-getaxeerde en laag-frequente klanten te controleren.
5. U maakt twee reizen in [!DNL Adobe Journey Optimizer], een om gebruikers te informeren over een nieuw abonnementsprogramma en een ander om hen te laten weten dat ze de aankoop later zullen bevestigen.
6. Desgewenst activeert u het publiek van klanten die uw abonnement niet hebben aangeschaft naar de gewenste bestemmingen voor betaalde media.

>[!ENDSHADEBOX]

## Hoe het gebruiksgeval te bereiken {#achieve-use-case-instruction}

Lees de onderstaande secties door om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien. Deze secties bevatten koppelingen naar meer informatie en meer gedetailleerde instructies.

### UI-functionaliteit en elementen die u gebruikt {#ui-functionality-and-elements}

Wanneer u de stappen voor het implementeren van het use case-object uitvoert, gebruikt u de Real-Time CDP-, Adobe Journey Optimizer-functionaliteit en UI-elementen die aan het begin van dit document worden vermeld. Zorg ervoor dat u de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

### Een schemaontwerp maken en veldgroepen opgeven {#schema-design}

Bronnen van het Experience Data Model (XDM) worden beheerd in de [!UICONTROL Schemas] -werkruimte in [!DNL Adobe Experience Platform] . U kunt de belangrijkste bronnen van [!DNL Adobe] (bijvoorbeeld [!UICONTROL field groups] ) weergeven en verkennen en aangepaste bronnen en schema&#39;s voor uw organisatie maken.

Voor meer informatie over het creëren van [ schema&#39;s ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl), leest [ schema tot leerprogramma.](/help/xdm/tutorials/create-schema-ui.md)

Er zijn verscheidene schemaontwerpen die u in deze steekproefimplementatie voor het gebruiksgeval kunt gebruiken om éénmalige waarde aan levenwaarde te evolueren. Elk schema bevat specifieke vereiste velden die moeten worden ingesteld, en enkele velden die worden voorgesteld.

Gebaseerd op steekproefimplementaties, stelt de Adobe voor dat u de volgende drie schema&#39;s creeert om dit gebruiksgeval te verwezenlijken:

* [ de attributenschema van de Klant ](#customer-attributes-schema) (een profielschema)
* [ schema van de Transacties van de Klant digitale ](#customer-digital-transactions-schema) (een schema van de ervaringsgebeurtenis)
* [ de off-line transactieschema van de Klant ](#customer-offline-transactions-schema) (een schema van de ervaringsgebeurtenis)

#### Klantkenmerkenschema {#customer-attributes-schema}

Gebruik dit schema om de profielgegevens te structureren en van verwijzingen te voorzien die omhoog uw klanteninformatie maken. Deze gegevens worden doorgaans in [!DNL Adobe Experience Platform] ingevoerd via uw CRM-systeem of een vergelijkbaar systeem en zijn nodig om te verwijzen naar klantgegevens die worden gebruikt voor personalisatie, marketingtoestemming en verbeterde segmentatiemogelijkheden.

![ de kenmerkenschema van de Klant met benadrukte gebiedsgroepen ](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

Het schema met klantkenmerken wordt vertegenwoordigd door een [!UICONTROL XDM Individual Profile] -klasse, die de volgende veldgroepen bevat:

+++Demografische details (veldgroep)

[ Demografische Details ](/help/xdm/field-groups/profile/demographic-details.md) is een standaardgroep van het schemagebied voor de individuele klasse van het Profiel XDM. De veldgroep biedt een persoonlijk object op hoofdniveau, waarvan de subvelden informatie over een individuele persoon beschrijven.

+++

+++Persoonlijke Contactgegevens (Veldgroep)

[ Persoonlijke Details van het Contact ](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel XDM Individual, die de contactinformatie voor een individuele persoon beschrijft.

+++

+++Externe gegevens van Source System Audit (veldgroep)

[ de Externe Attributen van de Controle van het Systeem van Source ](/help/xdm/data-types/external-source-system-audit-attributes.md) is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

+++Groepen van het Toegelaten en van het Referentieveld (de Groep van het Gebied)

[ de Inhoud en van de Voorkeur ](/help/xdm/field-groups/profile/consents.md) gebiedsgroep verstrekt één enkel voorwerp-type gebied, toestemmingen, om toestemmings en voorkeurinformatie te vangen.

+++

#### Schema voor digitale transacties van klanten {#customer-digital-transactions-schema}

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website of op andere bijbehorende digitale platforms voorkomt. Dit gegeven wordt typisch opgenomen in [!DNL Adobe Experience Platform] via [ Web SDK ](/help/web-sdk/home.md) en is noodzakelijk om diverse doorbladeren en omzettingsgebeurtenissen van verwijzingen te voorzien die voor het teweegbrengen van reizen, gedetailleerde online klantenanalyse, en verbeterde segmenteringsmogelijkheden worden gebruikt.

![ de digitale transactieschema van de Klant met benadrukte gebiedsgroepen ](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

Het schema voor digitale transacties van de klant wordt vertegenwoordigd door een [!UICONTROL XDM ExperienceEvent] klasse, die de volgende gebiedsgroepen omvat:

+++Adobe Experience Platform Web SDK ExperienceEvent (veldgroep)

| Velden | Vereiste |
| --- | --- |
| `device.model` | Voorgesteld |
| `environment.browserDetails.userAgent` | Voorgesteld |

+++

+++Webdetails (Veldgroep)

[ Details van het Web ](/help/xdm/field-groups/event/web-details.md) is een standaardgroep van het schemagebied voor de klasse XDM ExperienceEvent, die wordt gebruikt om informatie betreffende de gebeurtenissen van Webdetails zoals interactie, paginadetails, en verwijzer te beschrijven.

+++

+++Consumer Experience Event (veldgroep)

Deze veldgroep bevat verschillende informatie over acties die gebruikers op uw webeigenschap hebben uitgevoerd, zoals aankoop- of browsergebeurtenissen.

| Veld | Vereiste |
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

De ](/help/xdm/field-groups/event/enduserids.md) het gebiedsgroep van de Details van de Gebruiker van 0} Eind {omvat diverse informatie over uw gebruikers, zoals of zij op uw plaats wanneer het bezoeken voor authentiek worden verklaard, en informatie over hun identiteit.[

+++

+++Externe gegevens van Source System Audit (veldgroep)

De externe Attributen van de Controle van het Systeem van Source is een standaard het gegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Offline transactieschema van de klant {#customer-offline-transactions-schema}

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op platforms buiten uw website voorkomt. Deze gegevens worden doorgaans in [!DNL Adobe Experience Platform] opgenomen vanuit een besturingssysteem (of een vergelijkbaar systeem) en worden meestal via een API-verbinding gestreamd naar Platform. Lees over [ partij ingestie ](/help/ingestion/batch-ingestion/getting-started.md). Zijn doel is de diverse off-line omzettingsgebeurtenissen van verwijzingen te voorzien die voor het teweegbrengen van reizen, diepe online en off-line klantenanalyse, en verbeterde segmenteringsmogelijkheden worden gebruikt.

![ de off-line transactieschema van de Klant met benadrukte gebiedsgroepen ](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

Het schema voor offlinetransacties van de klant wordt vertegenwoordigd door een [!UICONTROL XDM ExperienceEvent] -klasse, die de volgende veldgroepen bevat:

+++Commerce-details (veldgroep)

[ de Details van Commerce ](/help/xdm/field-groups/event/commerce-details.md) is een standaardgroep van het schemagebied voor de [!DNL XDM ExperienceEvent] klasse, die wordt gebruikt om handelsgegevens zoals productinformatie (SKU, naam, hoeveelheid), en standaardkartverrichtingen (orde, controle, verlaten) te beschrijven.

+++

+++Persoonlijke Contactgegevens (Veldgroep)

[[!UICONTROL Personal Contact Details]](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de [!DNL XDM Individual Profile] klasse, die de contactinformatie voor een individuele persoon beschrijft.

+++

+++Externe gegevens van Source System Audit (veldgroep)

De externe Attributen van de Controle van het Systeem van Source is een standaard het gegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Adobe webverbindingsschema {#adobe-web-connector-schema}

>[!NOTE]
>
>Dit is een optionele implementatie als u [!DNL Adobe Analytics Data Connector] gebruikt.

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website of op andere bijbehorende digitale platforms voorkomt. Dit schema is gelijkaardig aan het schema van de Transacties van de Klant Digitale maar verschilt in die zin dat het kan wanneer het Web SDK geen optie voor gegevensinzameling is. Als zodanig kunt u dit schema gebruiken wanneer u [!DNL Adobe Analytics Data Connector] gebruikt om uw onlinegegevens naar [!DNL Adobe Experience Platform] te verzenden als primaire of secundaire gegevensstroom.

![ Adobe Web verbindingsschema met benadrukte gebiedsgroepen ](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

Het schema van de [!DNL Adobe] webconnector wordt vertegenwoordigd door een [!UICONTROL XDM ExperienceEvent] -klasse, die de volgende veldgroepen bevat:

+++Adobe Analytics ExperienceEvent-sjabloon (veldgroep)

[[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](/help/xdm/field-groups/event/analytics-full-extension.md) is een standaardschemaveldgroep, die gemeenschappelijke metriek vastlegt die door Adobe Analytics worden verzameld.

+++

### Een dataset maken op basis van een schema {#dataset-from-schema}

Een dataset is een opslag en beheersstructuur voor een groep gegevens. Elk schema dat wordt gebruikt om deze steekproefimplementatie te verwezenlijken heeft één enkele dataset.

Voor meer informatie over hoe te om a [ dataset ](/help/catalog/datasets/overview.md) van een schema tot stand te brengen, lees de [ gids UI van Datasets ](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Gelijkaardig aan de stap om een schema tot stand te brengen, moet u toelaten dat de dataset in het Profiel van de Klant in real time wordt omvat. Voor meer informatie over het toelaten van de dataset voor gebruik in het Profiel van de Klant in real time, leest [ schema tot leerprogramma.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Privacy, toestemming en gegevensbeheer {#privacy-consent}

#### Toestemmingsbeleid

>[!IMPORTANT]
>
>Het is een wettelijke vereiste om klanten de mogelijkheid te bieden zich niet langer te abonneren op het ontvangen van communicatie van een merk, en om ervoor te zorgen dat deze keuze wordt nagekomen. Leer meer over de toepasselijke wetgeving in het [ overzicht van de Regels van de Privacy ](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Overweeg het uitvoeren van het volgende [ toestemmingsbeleid ](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) en het vragen van uw bezoekers om toestemming alvorens u uit naar hen reist:

* Als `consents.marketing.email.val = "Y"` dan kan e-mailen
* Indien `consents.marketing.sms.val = "Y"` dan kan SMS
* Als `consents.marketing.push.val = "Y"` dan kan duwen
* Als `consents.share.val = "Y"` dan reclame kan maken

#### Label voor gegevensbeheer en handhaving

Overweeg het toevoegen van en het handhaven van de volgende [ etiketten van het gegevensbeheer ](/help/data-governance/labels/overview.md):

* Persoonlijke e-mailadressen worden gebruikt als rechtstreeks identificeerbare gegevens die worden gebruikt voor het identificeren of aanraken van een specifieke persoon in plaats van een apparaat.
   * `personalEmail.address = I1`

#### Marketingsbeleid

Er zijn geen [ marketing beleid ](/help/data-governance/policies/overview.md) vereist voor de reizen die u als deel van dit gebruiksgeval creeert. U kunt echter de volgende beleidsregels in overweging nemen:

* Gevoelige gegevens beperken
* Onsite Advertising beperken
* E-maildoelen beperken
* Lokale doelen beperken
* Het combineren van rechtstreeks identificeerbare gegevens met anonieme gegevens beperken

### Soorten publiek maken {#create-audiences}

Voor dit gebruiksgeval moet u twee soorten publiek maken om specifieke kenmerken of gedragingen te definiëren die worden gedeeld door een subset van profielen in het archief Profiel om een verhandelbare groep personen te onderscheiden. In Adobe Experience Platform kunnen soorten publiek op meerdere manieren worden gemaakt:

* Voor informatie over hoe te om een publiek tot stand te brengen, lees de [ de dienstgids van het publiek UI ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).
* Voor informatie over hoe te om [ publiek ](/help/segmentation/home.md) samen te stellen, lees de [ gids UI van de Samenstelling van het publiek ](/help/segmentation/ui/audience-composition.md).
* Voor informatie over hoe te om publiek door Platform-afgeleide segmentdefinities te bouwen, lees de [ gids UI van de Bouwer van het publiek van het publiek ](/help/segmentation/ui/segment-builder.md).

Met name moet u twee soorten publiek maken en gebruiken in verschillende stappen van het gebruiksscenario, zoals in de onderstaande afbeelding wordt getoond.

![ benadrukte Soorten publiek.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB  Adobe Journey Optimizer Kwalificerend Publiek ]

Dit publiek met een hoge waarde en een lage frequentie bevat de profielen die u via een reis wilt bereiken, om hen op de hoogte te stellen van een nieuw abonnementsprogramma. De publieksdetails zijn hieronder:

* Omschrijving: profielen die in de afgelopen drie maanden in totaal meer dan $250 hebben uitgegeven
* Velden en voorwaarden vereist in het publiek:
   * Event: `commerce.order.payments.paymentamount`
* Totaal bedrag: >= $250
   * EventType: `commerce.purchases`
* Tijdstempel: minder dan 3 maanden eerder


>[!TAB  Betaald media publiek ]

Dit publiek wordt gemaakt om profielen op te nemen die in de afgelopen drie maanden in totaal meer dan $250 hebben besteed en die in de afgelopen zeven dagen geen aankoop hebben gehad. De publieksdetails zijn hieronder:

* Omschrijving: profielen die in de afgelopen drie maanden in totaal meer dan $250 hebben uitgegeven en in de laatste zeven dagen geen aankoop hebben gehad.
* Velden en voorwaarden vereist:
   * EventType: `journey.feedback`
      * Operand: = true
   * Event: `experience.journeyOrchestration.stepEvents.nodeName`
      * Operand: = JourneyStepEventTracker - Abonnement niet aangeschaft
      * Tijdstempel: in afgelopen 7 dagen
   * EventType is niet: `commerce.purchases`
      * Tijdstempel: &lt;= 7 dagen vóór nu
   * Gebeurtenis: SKU
      * Waarde: = `subscription`

>[!ENDTABS]

### Reisinstallatie in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] omvat niet alles die in de diagrammen wordt getoond. Alle [ betaalde media advertenties ](/help/destinations/catalog/social/overview.md) worden gecreeerd in de [!UICONTROL destinations] [ werkruimte ](/help/destinations/ui/destinations-workspace.md).

[[!DNL Adobe Journey Optimizer] ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) helpt u verbonden, contextafhankelijke, en gepersonaliseerde ervaringen aan uw klanten leveren. De reis van de klant is het volledige proces van interactie van een klant met het merk. Voor elke gebruiksreis is specifieke informatie vereist.

Voor dit gebruiksgeval moet u twee aparte ritten maken:

* De levensreis, die het bericht omvat dat u naar uw hoge waarde, lage frequentieklanten verzendt
* De reis van de de bevestiging van de orde voor de gebruikers die op uw vraag antwoorden en een abonnement kopen.

![ benadrukte Reizen.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

Hieronder worden de precieze gegevens vermeld die voor elke tak van de Reis nodig zijn.

>[!BEGINTABS]

>[!TAB  Reis van het Leven ]

De levenslange reis richt het publiek van high-value en laag-frequente klanten die niet binnen de laatste 30 dagen werden gericht. Er wordt een bericht weergegeven aan deze klanten en als ze na 7 dagen nog steeds geen advertenties aanschaffen, kunt u de niet-kopers opnemen in een publiek waarnaar u betaalde mediaberichten kunt weergeven. Als ze wel een aankoop doen, kunt u de kopers instellen op een bestelbevestigingstraject, dat wordt beschreven in het afzonderlijke tabblad.

![ De reis van het leven high-level visueel overzicht.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png " Eenmalige waarde aan levenstransport high-level visueel overzicht."){zoomable="yes"}

+++Gedetailleerde logica voor reizen

De hierboven getoonde reis volgt de volgende logica.

1. Lees publiek: Gebruik a [ gelezen publieksactiviteit ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=en) voor het eerste publiek dat in de sectie van het publiek hierboven wordt gecreeerd.

2. Voorwaarde - Gewenste Kanaal: Gebruik de activiteit van de a [ voorwaarde ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html) om te bepalen hoe te om uit aan klanten te bereiken, hetzij door e-mail, SMS, of dupberichten. Gebruik drie actieactiviteiten om de drie takken tot stand te brengen.

3. Wacht: Het gebruik a [ wacht activiteit ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html) om te wachten tot u op aankopen luistert.

4. Voorwaarde - Aangeschafte Abonnement in afgelopen 7 dagen?: gebruik een voorwaardenactiviteit om te luisteren naar productaankopen in de afgelopen 7 dagen.

5. JourneyStepEventTracker - Abonnement niet Gekochte: Gebruik a [ douaneactie ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html) voor de bezoekers die uw abonnement nog niet hebben gekocht, ondanks het ontvangen van uw bericht. Als onderdeel van de aangepaste voorwaarde aan het einde van de rit maakt u een `journey.feedback` -gebeurtenis en voegt u deze toe aan een gegevensset die is gebaseerd op het [!UICONTROL Journey Step Event] -schema. U gebruikt deze gebeurtenis om het publiek te segmenteren dat het abonnement niet heeft aangeschaft en dat u kunt richten via betaalde mediadeslagen.

+++

>[!TAB  de Bevestigingsreis van de Orde ]

De reis om uw bestelling te bevestigen richt zich op de vraag of een aankoop via de website of mobiele app is gedaan. Nadat een klant de aankoop van bijvoorbeeld een abonnement bij uw bedrijf heeft voltooid, kunt u deze op een bestelbevestigingstraject instellen.

![ de bevestigingsreis van de orde van de Klant high-level visueel overzicht.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png " de bevestigingsreis van de orde van de Klant high-level visueel overzicht."){zoomable="yes"}

+++Reislogica

Gebruik de voorgestelde gebeurtenissen, gebieden, en acties hieronder in uw bevestigingsreis:

* De reis wordt geactiveerd door een online aankoopgebeurtenis
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
   * Selecteer Doelkanaal (u kunt een of meerdere kanalen selecteren voor een groter bereik).
      * Bevestiging van bestellingen wordt beschouwd als dienstbaar in de natuur, dus controle van de toestemming is meestal niet nodig.
      * Email
      * Push
      * Sms

   * Personalization voor kanaalinhoud
      * Hiermee geeft u informatie over de volgordedetails weer en kunt u een lijst met producten weergeven met een tabelindeling.

+++

>[!ENDTABS]

Voor meer informatie over het creëren van reizen in [!DNL Adobe Journey Optimizer], lees [ begonnen met reizen ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) gids.

### Een bestemming instellen om betaalde mediaciliteiten weer te geven {#paid-media-ads}

Sommige gebruikers hebben uw abonnement mogelijk niet aangeschaft, zelfs niet nadat u hun een bericht over het nieuwe programma hebt gestuurd. Nadat u op een aantal dagen hebt gewacht (zeven in dit voorbeeld gebruiken), kunt u ervoor kiezen om betaalde mediaberichten aan deze gebruikers weer te geven en hen aan te moedigen om uw abonnement aan te schaffen.

Gebruik het bestemmingskader in Real-Time CDP voor betaalde media advertenties. Selecteer één van de vele beschikbare reclamebestemmingen om betaalde media advertenties aan uw klanten te tonen en het Betaalde mediapubliek te activeren dat u [ vroeger ](#create-audiences) aan een bestemming van uw keus creeerde. Zie een overzicht van beschikbare [ reclame ](/help/destinations/catalog/advertising/overview.md) en [ sociale ](/help/destinations/catalog/social/overview.md) bestemmingen.

Leren hoe te om gegevens aan bestemmingen (bijvoorbeeld [ te activeren de Commerciële Desk ](/help/destinations/catalog/advertising/tradedesk.md) of [ Klantovereenkomst van Google ](/help/destinations/catalog/advertising/google-customer-match.md)), lees hieronder de documentatie:

* [Een nieuwe doelverbinding maken](/help/destinations/ui/connect-destination.md)
* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](/help/destinations/ui/activate-segment-streaming-destinations.md)

## Volgende stappen {#next-steps}

Door uw low-frequency en high-value gebruikers op een reis te plaatsen en door betaalde media advertenties aan een ondergroep van hen te tonen, hebt u hopelijk sommige van hen van éénmalige waarde aan levenswaardeklanten veranderd, daardoor verbeterend uw merkloyaliteit en klantenbetrokkenheidsmetriek.

Daarna, kunt u andere die gebruiksgevallen onderzoeken door Real-Time CDP worden gesteund, zoals [ intelligent klanten ](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) of [ herbetreurend gepersonaliseerde inhoud aan niet voor authentiek verklaarde gebruikers ](/help/rtcdp/partner-data/onsite-personalization.md) op uw Webeigenschappen.
