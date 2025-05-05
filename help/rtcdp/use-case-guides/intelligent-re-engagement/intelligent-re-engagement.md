---
title: Intelligente re-engagement
description: Lever boeiende en verbonden ervaringen tijdens de belangrijkste conversiemomenten om op een intelligente manier opnieuw in contact te komen met onregelmatige klanten.
feature: Use Cases
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3871'
ht-degree: 1%

---

# Intelligent opnieuw contact leggen met uw klanten, zodat ze terugkomen

>[!NOTE]
>
>Dit is een voorbeeldimplementatie en de voorbeelden op deze pagina, zoals segmentsyntaxis, zijn slechts voorbeelden. U moet de voorbeelden als richtlijn gebruiken, omdat de implementatie anders kan zijn.

Neem klanten opnieuw in dienst die een omzetting op een intelligente en verantwoordelijke manier hebben verlaten. Verloren klanten met ervaringen aantrekken om de conversie te verhogen en de waarde van de levensduur van de client te verhogen.

U kunt real-time overwegingen gebruiken, rekening houden met alle kwaliteiten en gedragingen van de consument en snelle herkwalificatie bieden op basis van zowel online als offline gebeurtenissen.

Hieronder volgt een architectuurweergave op hoog niveau van de verschillende componenten van Real-Time CDP en Journey Optimizer. In dit diagram ziet u hoe de gegevens door de twee Experience Platform-apps lopen van gegevensverzameling tot het punt waar deze wordt geactiveerd via reizen of campagnes naar bestemmingen, om het gebruiksgeval te bereiken dat op deze pagina wordt beschreven.

![ Intelligent re-engagement hoog niveau visueel overzicht.](../intelligent-re-engagement/images/step-by-step.png)

## Hoofdlettergebruik {#overview}

U zult schema&#39;s, datasets, en publiek aangezien u door voorbeelden van re-betrokkenheidsscenario&#39;s werkt construeren. U zult ook de functies ontdekken die nodig zijn om de voorbeeldreizen in [!DNL Adobe Journey Optimizer] in te stellen en de functies die nodig zijn om betaalde mediaberichten in bestemmingen te maken. In deze handleiding worden voorbeelden gebruikt van het opnieuw betrekken van klanten bij de hieronder beschreven gebruiksritten:

* **Verlaten product doorbladert scenario** - de klanten van het doel die product hebben verlaten doorbladerend op zowel de website als mobiele app.
* **Verlaten kartscenario** - de klanten van het doel die producten in de kar hebben geplaatst maar nog niet op zowel de website als mobiele app gekocht.
* **de bevestigingsscenario van de Orde** - concentreer zich op productaankopen die door de website en mobiele app worden gemaakt.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer u de stappen voor het implementeren van het hoofdlettergebruik uitvoert, maakt u gebruik van de volgende Real-Time CDP- en Adobe Journey Optimizer-functionaliteit (vermeld in de volgorde waarin u deze gaat gebruiken). Zorg ervoor dat u de noodzakelijke [ op attributen-gebaseerde toegangsbeheertoestemmingen ](/help/access-control/home.md) voor al deze gebieden hebt, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)] ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=nl-NL) - integreert gegevens over gegevensbronnen om de campagne te voeden. Deze gegevens worden vervolgens gebruikt om het campagnepubliek te maken en gepersonaliseerde gegevenselementen aan de oppervlakte te brengen die worden gebruikt in de e-mail en de webpromo-elementen (bijvoorbeeld naam of aan account gerelateerde informatie). CDP wordt ook gebruikt om publiek over e-mail en het Web (via [!DNL Adobe Target]) te activeren.
   * [Schema&#39;s](/help/xdm/home.md)
   * [Profielen](/help/profile/home.md)
   * [Gegevenssets](/help/catalog/datasets/overview.md)
   * [Doelgroepen](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=nl-NL)
   * [Bestemmingen](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer] ](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=nl-NL) - Helpt u verbonden, contextafhankelijke, en gepersonaliseerde ervaringen aan uw klanten te leveren.
   * [ de Trigger van de Gebeurtenis of van het Publiek ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html?lang=nl-NL)
   * [ Soorten publiek/Gebeurtenissen ](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=nl-NL)
   * [ Acties van de Reis ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=nl-NL)

## Hoe het gebruiksgeval te bereiken {#achieve-use-case-instruction}

Hieronder vindt u een overzicht op hoog niveau van de drie voorbeelden van scenario&#39;s voor herbetrokkenheid.

>[!BEGINTABS]

>[!TAB  Verlaten Product doorbladert Scenario ]

Het verlaten productbladerscenario richt verlaten product het doorbladeren op zowel de website als mobiele app. Dit scenario wordt geactiveerd wanneer een product is bekeken maar niet is aangeschaft of aan de winkelwagen is toegevoegd. In dit voorbeeld wordt de betrokkenheid van het merk geactiveerd na drie dagen als er geen toevoegingen aan de lijst zijn binnen de laatste 24 uur.<p>![ de intelligente verlaten product van de Klant doorbladert scenario op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/re-engagement-journey.png " de intelligente verlaten product van de Klant doorbladert scenario op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U maakt schema&#39;s en gegevenssets en schakelt deze vervolgens in voor [!UICONTROL Profile] .
2. U voert gegevens in Experience Platform in via Web SDK, Mobile SDK of API. De Source Connector voor Analytics kan ook worden gebruikt, maar kan leiden tot vertraging van de reis.
3. U voegt extra profielgegevens in, die via identiteitsgrafieken kunnen worden gekoppeld aan de geverifieerde webgebruiker en de mobiele-app-bezoeker.
4. U bouwt geconcentreerd publiek van de lijst van profielen om te controleren als a **klant** een overeenkomst in de laatste drie dagen heeft gemaakt.
5. U maakt een verlaten product door bladeren reis in [!DNL Adobe Journey Optimizer].
6. Indien nodig, werk met de **gegevenspartner** voor de activering van publiek aan gewenste betaalde-media bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert op toestemming en verzendt de verschillende geconfigureerde acties.

>[!TAB  Verlaten Scenario van de Kar ]

Het verlaten kartscenario is van toepassing wanneer de producten in het karretje zijn geplaatst maar nog niet op zowel de website als de mobiele app zijn gekocht. Bovendien worden campagnes voor betaalde media gestart en gestopt met deze methode.<p>![ Klant verliet kaartscenario hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png " Klant verliet het scenario van het wortelscenario op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets, toelaat voor [!UICONTROL Profile].
2. U voert gegevens in Experience Platform in via Web SDK, Mobile SDK of API. De Source Connector voor Analytics kan ook worden gebruikt, maar kan leiden tot vertraging van de reis.
3. U voegt extra profielgegevens in, die via identiteitsgrafieken kunnen worden gekoppeld aan de geverifieerde webgebruiker en de mobiele-app-bezoeker.
4. U bouwt geconcentreerd publiek van de lijst van profielen om te controleren als a **klant** een punt in hun kar heeft geplaatst maar niet de aankoop heeft voltooid. De gebeurtenis **[!UICONTROL Add to cart]** schakelt een timer uit die 30 minuten wacht en controleert vervolgens of deze is aangeschaft. Als geen aankoop is gemaakt, dan wordt de **klant** toegevoegd aan het **[!UICONTROL Abandon Cart]** publiek.
5. U maakt in [!DNL Adobe Journey Optimizer] een verlaten wagentje.
6. Indien nodig, werk met de **gegevenspartner** voor de activering van publiek aan gewenste betaalde-media bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert op toestemming en verzendt de verschillende geconfigureerde acties.

>[!TAB  het Bevestigingsscenario van de Orde ]

Het bevestigingsscenario voor bestellingen is vooral gericht op productaankopen via de website en de mobiele app.<p>![ het scenario van de de ordetectie van de Klant op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png " het scenario van de de ordecbevestiging van de Klant hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U maakt schema&#39;s en gegevenssets en schakelt deze vervolgens in voor [!UICONTROL Profile] .
2. U voert gegevens in Experience Platform in via Web SDK, Mobile SDK of API. De Source Connector voor Analytics kan ook worden gebruikt, maar kan leiden tot vertraging van de reis.
3. U voegt extra profielgegevens in, die via identiteitsgrafieken kunnen worden gekoppeld aan de geverifieerde webgebruiker en de mobiele-app-bezoeker.
4. U maakt een bevestigingsreis in [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] verzendt een bericht van de ordesbevestiging gebruikend het aangewezen kanaal.

>[!ENDTABS]

Lees de onderstaande secties door om alle stappen in de bovenstaande overzichten op hoog niveau te voltooien. Deze bevatten koppelingen naar meer informatie en meer gedetailleerde instructies.

### Schema&#39;s maken en veldgroepen opgeven {#schema-design}

Bronnen van het Experience Data Model (XDM) worden beheerd in de [!UICONTROL Schemas] -werkruimte in [!DNL Adobe Experience Platform] . U kunt de belangrijkste bronnen van [!DNL Adobe] (bijvoorbeeld veldgroepen) weergeven en verkennen en aangepaste bronnen en schema&#39;s voor uw organisatie maken.

Voor meer informatie over het creëren van [ schema&#39;s ](/help/xdm/home.md), zie [ schema tot leerprogramma leiden.](/help/xdm/tutorials/create-schema-ui.md) en [ ModelUw Gegevens van de Ervaring van de Klant met XDM ](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

Er zijn vier schemaontwerpen die voor het re-engagement gebruikscase worden gebruikt. Voor elk schema moeten specifieke velden worden ingesteld. U moet toelaten dat het schema in het Profiel van de Klant in real time wordt omvat. Voor meer informatie over het toelaten van het schema voor gebruik in het Profiel van de Klant in real time, leest [ een schema voor het Profiel van de Klant in real time ](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile) toe.

#### Klantkenmerkenschema

Dit schema wordt gebruikt om de profielgegevens te structureren en van verwijzingen te voorzien die omhoog uw klanteninformatie maken. Deze gegevens worden doorgaans in [!DNL Adobe Experience Platform] opgenomen via uw CRM-systeem of een vergelijkbaar systeem en zijn nodig om te verwijzen naar klantgegevens die worden gebruikt voor personalisatie, marketingtoestemming en verbeterde publieksmogelijkheden.

Het schema met klantkenmerken wordt vertegenwoordigd door een [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md) -klasse, die de volgende veldgroepen bevat:

+++Persoonlijke Contactgegevens (Veldgroep)

[ Persoonlijke Details van het Contact ](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel XDM Individual die de contactinformatie voor een individuele persoon beschrijft.

| Velden | Beschrijving |
| --- | --- |
| `mobilePhone.number` | Het mobiele telefoonnummer van de persoon, dat wordt gebruikt voor SMS. |
| `personalEmail.address` | Het e-mailadres van de persoon. |

+++

+++Externe gegevens van Source System Audit (veldgroep)

[ de Externe Attributen van de Controle van het Systeem van Source ](/help/xdm/data-types/external-source-system-audit-attributes.md) is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

+++Groepen van het Toegelaten en van het Referentieveld (de Groep van het Gebied)

De [ Inhoud en de 1&rbrace; het gebiedsgroep van Voorkeur &lbrace;verstrekt één enkel voorwerp-type gebied, toestemmingen, om toestemming en voorkeurinformatie te vangen.](/help/xdm/field-groups//profile/consents.md)

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

Met deze veldgroep kunt u uw reis testen voordat deze wordt gepubliceerd met testprofielen. Voor meer informatie over het creëren van testprofielen, leest [ tot de leerprogramma&#39;s van testprofielen ](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html?lang=nl-NL) en [ het testen van de reiszelfstudie ](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/testing-the-journey.html?lang=nl-NL).

+++

#### Schema voor digitale transacties van klanten

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website of bijbehorende digitale platforms voorkomt. Dit gegeven wordt typisch opgenomen in [!DNL Adobe Experience Platform] via [ SDK van het Web ](/help/web-sdk/home.md) en is noodzakelijk om diverse doorbladeren en omzettingsgebeurtenissen van verwijzingen te voorzien die voor het teweegbrengen van reizen, gedetailleerde online klantenanalyse, verbeterde publieksmogelijkheden, en gepersonaliseerd overseinen worden gebruikt.

Het schema voor digitale transacties van de klant wordt vertegenwoordigd door een [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) -klasse.

+++XDM ExperienceEvent (Class)

De klasse [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) bevat de volgende veldgroepen:

| Velden | Beschrijving |
| --- | --- |
| `_id` | Hiermee worden afzonderlijke gebeurtenissen die in [!DNL Adobe Experience Platform] worden opgenomen, op unieke wijze geïdentificeerd. |
| `timestamp` | Een tijdstempel volgens ISO 8601 van het tijdstip van de gebeurtenis, opgemaakt volgens RFC 3339, sectie 5.6. Deze tijdstempel moet in het verleden voorkomen. |
| `eventType` | Een tekenreeks die het type categorie voor de gebeurtenis aangeeft. |

+++

+++Details eindgebruiker-id (veldgroep)

De [&#128279;](/help/xdm/field-groups/event/enduserids.md) het gebiedsgroep van de Details van de Gebruiker van het 0&rbrace; Eind &lbrace;wordt gebruikt om de identiteitsinformatie van een individu over verscheidene toepassingen van Adobe te beschrijven.

| Velden | Beschrijving |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Status van e-mailadres voor eindgebruiker is geverifieerd. |
| `endUserIDs._experience.emailid.id` | E-mailadres van eindgebruiker. |
| `endUserIDs._experience.emailid.namespace.code` | Naamruimte-code van e-mailadres van eindgebruiker. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] Status geverifieerd voor Marketing Cloud ID (MCID). De MCID wordt nu de Experience Cloud-id (ECID) genoemd. |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud-id (MCID). De MCID wordt nu de Experience Cloud-id (ECID) genoemd. |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] Marketing Cloud ID (MCID)-naamruimtecode. |

+++

+++Commerce-details (veldgroep)

De [ Commerce Details ](/help/xdm/field-groups/event/commerce-details.md) gebiedsgroep wordt gebruikt om handelsgegevens zoals productinformatie (SKU, naam, hoeveelheid), en standaardkartverrichtingen (orde, controle, verlaten) te beschrijven.

| Velden | Beschrijving |
| --- | --- |
| `commerce.cart.cartID` | Een id voor het winkelwagentje. |
| `commerce.order.orderType` | Een object dat het type productvolgorde beschrijft. |
| `commerce.order.payments.paymentAmount` | Een object dat het bedrag van de productbestelling beschrijft. |
| `commerce.order.payments.paymentType` | Een object dat een beschrijving geeft van het type productorderbetaling. |
| `commerce.order.payments.transactionID` | Een transactie-id voor een objectproduct. |
| `commerce.order.purchaseID` | Een aankoop-id voor de objectorder. |
| `productListItems.name` | Een lijst met itemnamen die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| `productListItems.priceTotal` | De totale prijs van de lijst met objecten die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| `productListItems.product` | Het geselecteerde product of de producten. |
| `productListItems.quantity` | De hoeveelheid lijst met objecten die het product of de producten vertegenwoordigt die door een klant is/zijn geselecteerd. |

+++

+++Externe gegevens van Source System Audit (veldgroep)

De externe Attributen van de Controle van het Systeem van Source is een standaard het gegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Offline transactieschema van de klant

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op platforms buiten uw website voorkomt. Deze gegevens worden doorgaans in [!DNL Adobe Experience Platform] ingevoerd via een besturingssysteem (of vergelijkbaar systeem) en worden meestal via een API-verbinding naar Experience Platform gestreamd. Zijn doel is de diverse off-line omzettingsgebeurtenissen van verwijzingen te voorzien die voor het teweegbrengen van reizen, diepe online en off-line klantenanalyse, verbeterde publieksmogelijkheden en gepersonaliseerd overseinen worden gebruikt.

Het schema voor offlinetransacties van de klant wordt vertegenwoordigd door een [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) -klasse.

+++XDM ExperienceEvent (Class)

De klasse [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) bevat de volgende veldgroepen:

| Velden | Beschrijving |
| --- | --- |
| `_id` | Hiermee worden afzonderlijke gebeurtenissen die in [!DNL Adobe Experience Platform] worden opgenomen, op unieke wijze geïdentificeerd. |
| `timestamp` | Een tijdstempel volgens ISO 8601 van het tijdstip van de gebeurtenis, opgemaakt volgens RFC 3339, sectie 5.6. Deze tijdstempel moet in het verleden voorkomen. |
| `eventType` | Een tekenreeks die het type categorie voor de gebeurtenis aangeeft. |

+++

+++Commerce-details (veldgroep)

De [ Commerce Details ](/help/xdm/field-groups/event/commerce-details.md) gebiedsgroep wordt gebruikt om handelsgegevens zoals productinformatie (SKU, naam, hoeveelheid), en standaardkartverrichtingen (orde, controle, verlaten) te beschrijven.

| Velden | Beschrijving |
| --- | --- |
| `commerce.cart.cartID` | Een id voor het winkelwagentje. |
| `commerce.order.orderType` | Een object dat het type productvolgorde beschrijft. |
| `commerce.order.payments.paymentAmount` | Een object dat het bedrag van de productbestelling beschrijft. |
| `commerce.order.payments.paymentType` | Een object dat een beschrijving geeft van het type productorderbetaling. |
| `commerce.order.payments.transactionID` | Een transactie-id voor een objectproduct. |
| `commerce.order.purchaseID` | Een aankoop-id voor de objectorder. |
| `productListItems.name` | Een lijst met itemnamen die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| `productListItems.priceTotal` | De totale prijs van de lijst met objecten die het product of de producten vertegenwoordigen die door een klant zijn geselecteerd. |
| `productListItems.product` | Het geselecteerde product of de producten. |
| `productListItems.quantity` | De hoeveelheid lijst met objecten die het product of de producten vertegenwoordigt die door een klant is/zijn geselecteerd. |

+++

+++Persoonlijke Contactgegevens (Veldgroep)

[ Persoonlijke Details van het Contact ](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel XDM Individual die de contactinformatie voor een individuele persoon beschrijft.

| Velden | Beschrijving |
| --- | --- |
| `mobilePhone.number` | Het mobiele telefoonnummer van de persoon, dat wordt gebruikt voor SMS. |
| `personalEmail.address` | Het e-mailadres van de persoon. |

+++

+++Externe gegevens van Source System Audit (veldgroep)

De externe Attributen van de Controle van het Systeem van Source is een standaard het gegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

#### Adobe-schema voor webconnector

>[!NOTE]
>
>Dit is een optionele implementatie als u [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md) gebruikt.

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website of bijbehorende digitale platforms voorkomt. Dit schema is gelijkaardig aan het Digitale schema van Transacties van de Klant maar verschilt in die zin dat het bedoeld is om te worden gebruikt wanneer [ SDK van het Web ](/help/web-sdk/home.md) geen optie voor gegevensinzameling is; zo, is dit schema nodig wanneer u [!DNL Adobe Analytics Source Connector] gebruikt om uw online gegevens in [!DNL Adobe Experience Platform] of als primaire of secundaire gegevensstroom te verzenden.

Het schema van de [!DNL Adobe] webconnector wordt vertegenwoordigd door een [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) -klasse.

+++XDM ExperienceEvent (Class)

De klasse [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) bevat de volgende veldgroepen:

| Velden | Beschrijving |
| --- | --- |
| `_id` | Hiermee worden afzonderlijke gebeurtenissen die in [!DNL Adobe Experience Platform] worden opgenomen, op unieke wijze geïdentificeerd. |
| `timestamp` | Een tijdstempel volgens ISO 8601 van het tijdstip van de gebeurtenis, opgemaakt volgens RFC 3339, sectie 5.6. Deze tijdstempel moet in het verleden voorkomen. |
| `eventType` | Een tekenreeks die het type categorie voor de gebeurtenis aangeeft. |

+++

+++Adobe Analytics ExperienceEvent-sjabloon (veldgroep)

De [&#128279;](/help/xdm/field-groups/event/analytics-full-extension.md) het gebiedsgroep van 1&rbrace; van Adobe Analytics ExperienceEvent vangt gemeenschappelijke metriek die door Adobe Analytics worden verzameld.

| Velden | Beschrijving |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Status van e-mailadres voor eindgebruiker is geverifieerd. |
| `endUserIDs._experience.emailid.id` | E-mailadres van eindgebruiker. |
| `endUserIDs._experience.emailid.namespace.code` | Naamruimte-code van e-mailadres van eindgebruiker. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] Status geverifieerd voor Marketing Cloud ID (MCID). De MCID wordt nu de Experience Cloud-id (ECID) genoemd. |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud-id (MCID). De MCID wordt nu de Experience Cloud-id (ECID) genoemd. |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] Marketing Cloud ID (MCID)-naamruimtecode. |

+++

+++Externe gegevens van Source System Audit (veldgroep)

De externe Attributen van de Controle van het Systeem van Source is een standaard het gegevenstype van de Gegevens van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

+++

### Een dataset maken op basis van een schema {#create-datasets}

Een dataset is een opslag en beheersstructuur voor een groep gegevens. Elk schema voor intelligente scenario&#39;s van de re-engagement zou zijn eigen dataset moeten hebben.

Voor meer informatie over hoe te om a [ dataset ](/help/catalog/datasets/overview.md) van een schema tot stand te brengen, lees de [ gids UI van Datasets ](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Gelijkaardig aan de stap om een schema tot stand te brengen, moet u toelaten dat de dataset in het Profiel van de Klant in real time wordt omvat. Voor meer informatie over het toelaten van de dataset voor gebruik in het Profiel van de Klant in real time, zie zelfstudie over [ brengend gegevens in het Profiel van de Klant in real time ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=nl-NL).

### Toestemming en gegevensbeheer {#privacy-consent}

>[!IMPORTANT]
>
>Het is een wettelijke vereiste om klanten de mogelijkheid te bieden zich niet langer te abonneren op het ontvangen van communicatie van een merk, en om ervoor te zorgen dat deze keuze wordt nagekomen. Leer meer over de toepasselijke wetgeving in het [ overzicht van de Regels van de Privacy ](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html?lang=nl-NL).

#### Toestemmingsbeleid

Wanneer het creëren van een re-betrokkenheidspad, denk na toevoegend het volgende [ toestemmingsbeleid ](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html?lang=nl-NL):

* Als `consents.marketing.email.val = "Y"` dan kan e-mailen
* Indien `consents.marketing.sms.val = "Y"` dan kan SMS
* Als `consents.marketing.push.val = "Y"` dan kan duwen
* Als `consents.share.val = "Y"` dan reclame kan maken

#### Etikettering en handhaving van gegevensbeheer

Wanneer het creëren van een re-betrokkenheidspad, denk na toevoegend de volgende [ etiketten van het Beleid van Gegevens ](/help/data-governance/labels/overview.md):

* Persoonlijke e-mailadressen worden gebruikt als direct identificeerbare gegevens die worden gebruikt om een specifieke persoon te identificeren of contact met hem te krijgen in plaats van met een apparaat.
   * `personalEmail.address = I1`

#### Beleid voor gegevensgebruik

Er zijn geen [ beleid van het gegevensgebruik ](/help/data-governance/policies/overview.md) wordt vereist voor het verlaten product doorbladert scenario. U dient echter het volgende in overweging te nemen:

* Gevoelige gegevens beperken
* Onsite Advertising beperken
* E-maildoelen beperken
* Doelstelling voor meerdere sites beperken
* Het combineren van rechtstreeks identificeerbare gegevens met anonieme gegevens beperken

### Soorten publiek maken {#create-audience}

In de scenario&#39;s voor herbetrokkenheid wordt gebruikgemaakt van publiek om specifieke kenmerken of gedragingen te definiëren die worden gedeeld door een subset van profielen in uw profielarchief om een verhandelbare groep personen te onderscheiden van uw klantenbasis. Soorten publiek kan op meerdere manieren worden gemaakt in [!DNL Adobe Experience Platform] .

Voor meer informatie over hoe te om een publiek tot stand te brengen, lees de [ gids UI van de publieksdienst ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=nl-NL#create-audience).

Voor meer informatie over hoe te om [ Soorten publiek ](/help/segmentation/home.md) direct samen te stellen, lees de [ gids UI van de Samenstelling van het publiek ](/help/segmentation/ui/audience-composition.md).

Voor meer informatie over hoe te om publiek door Experience Platform-Afgeleide publieksdefinities te bouwen, lees de [ gids UI van de Bouwer van de Publiek ](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB  Verlaten Product doorbladert Scenario ]

Dit publiek wordt gemaakt als een uitbreiding op het klassieke scenario &#39;Kart Abandenvironment&#39;. Terwijl het verlaten van het winkelwagentje zich doorgaans concentreert op een toevoeging van winkelwagentjes zonder een latere aankoop binnen een bepaalde periode, zoekt dit publiek naar een eerdere betrokkenheid, met name diegenen die mogelijk door een bepaald product hebben gebladerd maar het niet aan hun winkelwagentje hebben toegevoegd en binnen een bepaalde tijd geen vervolgactiviteit op uw site hadden. Dit publiek helpt om uw merk &quot;bovenaan&quot;voor klanten te houden die aan deze inclusiecriteria voldoen en kan ook voor klanten worden gebruikt waarvan digitale eigenschappen van een traditioneel e-commercemodel kunnen verschillen.

+++Afgeknot productweergave zonder betrokkenheid in de afgelopen drie dagen

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers producten online bekeken, en niet (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegden aan kartgebeurtenissen) in de drie dagen na het volgen begonnen.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.productViews`
* En `THEN` (sequentiële gebeurtenis) sluit `eventType: commerce.productListAdds` AND `application.launch` AND `web.webpagedetails.pageViews` AND `commerce.purchases` uit (omvat zowel online als offline)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`

+++

+++Productweergave met betrokkenheid in de laatste drie dagen

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers producten online bekeken, en (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegen aan kartgebeurtenissen) in de drie dagen na het volgen van de verbinding in dienst genomen.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.productViews`
* En `THEN` (sequentiële gebeurtenis) bevat `eventType: commerce.productListAdds` OR `application.launch` OR `web.webpagedetails.pageViews` OR `commerce.purchases` (inclusief online en offline)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`
+++

+++streaming betrokkenheid in de laatste dag

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegen aan kartgebeurtenissen) in de afgelopen 1 dag hebben betrokken.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 1 day` (streaming)

+++

+++Betrokkenheidsbatch in de laatste drie dagen

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegen aan kartgebeurtenissen) in de laatste drie dagen hebben betrokken.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `EventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 3 days` (batch)

+++

>[!TAB  Verlaten Scenario van de Kar ]

Dit publiek wordt gemaakt ter ondersteuning van het klassieke scenario &#39;Kart Abandenvironment&#39;. Het doel is om klanten te vinden die een product aan hun winkelwagentje hebben toegevoegd maar uiteindelijk niet met een aankoop hebben gevolgd. Dit publiek zal niet alleen uw merk &quot;bovenaan&quot;voor uw klanten houden maar ook de producten die zij zonder een verdere aankoop hebben verlaten.

De volgende gebeurtenissen worden gebruikt voor het verlaten kartscenario waar de gebruikers een product aan hun karretje tussen 1 en 4 dagen geleden toevoegden, maar de aankoop niet voltooiden of hun karretje ontruimen.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now AND <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

De beschrijving voor het verlaten kartscenario verschijnt als:

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB  het Bevestigingsscenario van de Orde ]

Voor deze reis is geen publiek nodig.

>[!ENDTABS]

### Reisinstallatie in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] omvat niet alles die in de diagrammen wordt getoond. Alle [ betaalde media advertenties ](/help/destinations/catalog/social/overview.md) worden gecreeerd in [!UICONTROL Destinations].

[[!DNL Adobe Journey Optimizer] ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=nl-NL) helpt u verbonden, contextafhankelijke, en gepersonaliseerde ervaringen aan uw klanten leveren. De reis van de klant is het volledige proces van interactie van een klant met het merk. Voor elke gebruiksreis is specifieke informatie vereist. Hieronder staan de precieze gegevens die nodig zijn voor elke reis.

>[!BEGINTABS]

>[!TAB  Verlaten Product doorbladert Scenario ]

Het verlaten productbladerscenario richt verlaten product het doorbladeren op zowel de website als mobiele app.<p>![ de verlaten productdoorblader van de Klant scenario op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/re-engagement-journey.png " de verlaten productdoorblader van de Klant scenario hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

+++Gebeurtenissen

Gebeurtenissen stellen u in staat om uw reizen tijdelijk te activeren en berichten in real-time te verzenden aan de persoon die de reis maakt. Voor meer informatie over gebeurtenissen, lees de [ algemene gebeurtenisgids ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=nl-NL).

* Gebeurtenis 1: productweergaven
   * Schema: digitale transacties van klanten
   * Velden:
      * `eventType`
   * Voorwaarde:
      * `eventType = commerce.productViews`
      * Velden:
         * `eventType`
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
      * `eventType`
   * Voorwaarde:
      * `eventType = commerce.productListAdds`
      * Velden:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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
      * `eventType`
   * Voorwaarde:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

+++Logische sleutel voor canvas

De belangrijkste logica van het reiscanvas vereist u om specifieke gebeurtenissen te identificeren en acties te vormen om te plaatsvinden nadat de gebeurtenis voorkomt.

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

   * Channel Personalization
      * Inhoud van persoonlijke kanalen op basis van de productweergave.

+++

>[!TAB  Verlaten Scenario van de Kar ]

Het verlaten kartscenario richt producten die in de kar zijn geplaatst maar nog niet op zowel de website als de mobiele app gekocht.<p>![ Klant verliet kaartscenario hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png " Klant verliet het scenario van het wortelscenario op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

+++Gebeurtenissen

Gebeurtenissen stellen u in staat om uw reizen tijdelijk te activeren en berichten in real-time te verzenden aan de persoon die de reis maakt. Voor meer informatie over gebeurtenissen, lees de [ algemene gebeurtenisgids ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=nl-NL).

* Gebeurtenis 2: Toevoegen aan winkelwagentje
   * Schema: digitale transacties van klanten
   * Velden:
      * `eventType`
   * Voorwaarde:
      * `eventType = commerce.productListAdds`
      * Velden:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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
      * `eventType`
   * Voorwaarde:
      * `eventType = commerce.purchases`
      * Velden:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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
      * `eventType`
   * Voorwaarde:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

+++Logische sleutel voor canvas

De belangrijkste logica van het reiscanvas vereist u om specifieke gebeurtenissen te identificeren en acties te vormen om te plaatsvinden nadat de gebeurtenis voorkomt.

* Logica voor reizen
   * `AddToCart` Event

* AuthenticatedState in authenticated

* Voorwaarde: offlineaankopen sinds de laatste keer dat het winkelwagentje werd verlaten:
   * Schema: offline transacties van klanten
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Voorwaarde: winkelwagentje wordt gewist sinds de laatste keer dat het winkelwagentje werd verlaten:
   * Schema: digitale transacties van klanten
   * `eventType = commerce.cartCleared`
   * `cartID` (ID van het winkelwagentje)
   * `timestamp > timestamp of cart was last abandoned`

* Doelkanaal selecteren (één of meerdere kanalen selecteren voor breder bereik)
   * Email
      * `consents.marketing.email.val = y`
   * Push
      * `consents.marketing.push.val = y`
   * Sms
      * `consents.marketing.sms.val = y`
   * Channel Personalization
      * Geef informatie over de details van het winkelwagentje weer en kan meerdere producten in een tabelindeling weergeven.

+++

>[!TAB  het Bevestigingsscenario van de Orde ]

Het bevestigingsscenario voor bestellingen is vooral gericht op productaankopen via de website en de mobiele app.<p>![ het scenario van de de ordetectie van de Klant op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png " het scenario van de de ordecbevestiging van de Klant hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

+++Gebeurtenissen

Gebeurtenissen stellen u in staat om uw reizen tijdelijk te activeren en berichten in real-time te verzenden aan de persoon die de reis maakt. Voor meer informatie over gebeurtenissen, lees de [ algemene gebeurtenisgids ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=nl-NL).

* Gebeurtenis 4: online aankopen
   * Schema: digitale transacties van klanten
   * Velden:
      * `eventType`
   * Voorwaarde:
      * `eventType = commerce.purchases`
      * Velden:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

+++Logische sleutel voor canvas

De belangrijkste logica van het reiscanvas vereist u om specifieke gebeurtenissen te identificeren en acties te vormen om te plaatsvinden nadat de gebeurtenis voorkomt.

* Logica voor reizen
   * Ordergebeurtenis

* Voorwaarden
   * Selecteer Doelkanaal (selecteer een of meerdere kanalen voor een groter bereik).
      * Bevestiging van bestellingen wordt beschouwd als dienstbaar in de natuur, dus controle van de toestemming is meestal niet nodig.
      * Email
      * Push
      * Sms

   * Personalization voor kanaalinhoud
      * Hiermee geeft u informatie over de volgordedetails weer en kunt u een lijst met producten weergeven met een tabelindeling.

+++

>[!ENDTABS]

Voor meer informatie over het creëren van reizen in [!DNL Adobe Journey Optimizer], lees [ begonnen met reisgids ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=nl-NL).

### Betaalde mediadeskundigen instellen in bestemmingen {#paid-media-ads}

Het bestemmingskader wordt gebruikt voor betaalde media advertenties. Zodra de toestemming is gecontroleerd verzendt het naar de diverse gevormde bestemmingen. Voor meer informatie over bestemmingen, lees het [ overzichtsdocument van Doelen ](/help/destinations/home.md).

#### Vereiste gegevens voor bestemmingen

Streaming publiek exportbestemmingen (zoals Facebook, Google Customer Match, Google DV360) ondersteunen verschillende identiteiten uit klantgegevens:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

U kunt verlaten productdoorbladeren activeren en het kartpubliek verlaten aan betaalde media advertenties.

* Stream/activering
   * [ Advertising ](/help/destinations/catalog/advertising/overview.md)/[ Betaalde Media &amp; Sociale ](/help/destinations/catalog/social/overview.md)
   * [Mobiel](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Streaming doel](/help/destinations/catalog/streaming/http-destination.md)
   * [ de bestemming van de Douane die door Destination SDK wordt gecreeerd te gebruiken.](/help/destinations/destination-sdk/overview.md). Als u een klant van Real-Time CDP Ultimate bent, kunt u een privé [ douanebestemming ook creëren gebruikend Destination SDK ](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)

## Volgende stappen {#next-steps}

Door uw klanten opnieuw in dienst te nemen die een omzetting op een intelligente en verantwoordelijke manier verlieten, hebt u hopelijk omzettingen verhoogd en de waarde van het cliëntleven verhoogd.

Daarna, kunt u andere gebruiksgevallen onderzoeken die door Real-Time CDP worden gesteund, zoals [ tonend gepersonaliseerde inhoud aan niet voor authentiek verklaarde gebruikers ](/help/rtcdp/partner-data/onsite-personalization.md) op uw Webeigenschappen.
