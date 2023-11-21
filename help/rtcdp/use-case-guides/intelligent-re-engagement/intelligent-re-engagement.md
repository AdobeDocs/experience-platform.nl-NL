---
title: Intelligente re-engagement
description: Lever boeiende en verbonden ervaringen tijdens de belangrijkste conversiemomenten om op een intelligente manier opnieuw in contact te komen met onregelmatige klanten.
feature: Use Cases
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: 3353866aa2d52c784663f355183e940e727b2af7
workflow-type: tm+mt
source-wordcount: '3569'
ht-degree: 2%

---

# Intelligent opnieuw contact leggen met uw klanten, zodat ze terugkomen

>[!NOTE]
>
>Dit is een voorbeeldimplementatie en de voorbeelden op deze pagina, zoals segmentsyntaxis, zijn slechts voorbeelden. U moet de voorbeelden als richtlijn gebruiken, omdat de implementatie anders kan zijn.

Neem klanten opnieuw in dienst die een omzetting op een intelligente en verantwoordelijke manier hebben verlaten. Verloren klanten met ervaringen aantrekken om de conversie te verhogen en de waarde van de levensduur van de client te verhogen.

U kunt real-time overwegingen gebruiken, rekening houden met alle kwaliteiten en gedragingen van de consument en snelle herkwalificatie bieden op basis van zowel online als offline gebeurtenissen.

![Intelligent vernieuwend visueel overzicht op hoog niveau.](../intelligent-re-engagement/images/step-by-step.png)

## Hoofdlettergebruik {#overview}

U zult schema&#39;s, datasets, en publiek aangezien u door voorbeelden van re-betrokkenheidsscenario&#39;s werkt construeren. U zult ook de eigenschappen ontdekken nodig om de voorbeeldreizen in te stellen [!DNL Adobe Journey Optimizer] en die welke nodig zijn om betaalde mediaberichten op bestemmingen te maken. In deze handleiding worden voorbeelden gebruikt van het opnieuw betrekken van klanten bij de hieronder beschreven gebruiksritten:

* **Verlaten productbladerscenario** - Doelklanten die het bladeren door producten op zowel de website als de mobiele app hebben verlaten.
* **Verlaten kartonscenario** - Doelklanten die producten in het winkelwagentje hebben geplaatst maar nog niet op de website en de mobiele app zijn aangeschaft.
* **Orderbevestiging** - Focus op aankopen van producten via de website en de mobiele app.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer u de stappen voor het implementeren van het hoofdlettergebruik uitvoert, maakt u gebruik van de volgende Real-Time CDP- en Adobe Journey Optimizer-functionaliteit (vermeld in de volgorde waarin u deze gaat gebruiken). Zorg ervoor dat u de benodigde [attribuut-gebaseerde toegangsbeheertoestemmingen](/help/access-control/home.md) voor al deze gebieden, of vraag uw systeembeheerder om u de noodzakelijke toestemmingen te verlenen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - integreert gegevens in verschillende gegevensbronnen om de campagne te voeden. Deze gegevens worden vervolgens gebruikt om het campagnepubliek te maken en gepersonaliseerde gegevenselementen aan de oppervlakte te brengen die worden gebruikt in de e-mail en de webpromo-elementen (bijvoorbeeld naam of aan account gerelateerde informatie). CDP wordt ook gebruikt om publiek over e-mail en het Web (via [!DNL Adobe Target]).
   * [Schema&#39;s](/help/xdm/home.md)
   * [Profielen](/help/profile/home.md)
   * [Gegevenssets](/help/catalog/datasets/overview.md)
   * [Doelgroepen](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Doelen](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html) - Helpt u verbonden, contextafhankelijke en persoonlijke ervaringen aan uw klanten te leveren.
   * [Trigger voor gebeurtenis of publiek](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Soorten publiek/Gebeurtenissen](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Reishandelingen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Hoe het gebruiksgeval te bereiken {#achieve-use-case-instruction}

Hieronder vindt u een overzicht op hoog niveau van de drie voorbeelden van scenario&#39;s voor herbetrokkenheid.

>[!BEGINTABS]

>[!TAB Verlaten door product Bladeren Scenario]

Het verlaten productbladerscenario richt verlaten product het doorbladeren op zowel de website als mobiele app. Dit scenario wordt geactiveerd wanneer een product is bekeken maar niet is aangeschaft of aan de winkelwagen is toegevoegd. In dit voorbeeld wordt de betrokkenheid van het merk geactiveerd na drie dagen als er geen toevoegingen aan de lijst zijn binnen de laatste 24 uur.<p>![Het intelligente verlaten product van de klant doorbladert scenario op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/re-engagement-journey.png "Het intelligente verlaten product van de klant doorbladert scenario op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets, dan laat voor toe [!UICONTROL Profile].
2. U voert gegevens in Experience Platform in via Web SDK, Mobile SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U voegt extra profielgegevens in, die via identiteitsgrafieken kunnen worden gekoppeld aan de geverifieerde webbezoeker en/of de mobiele gebruiker van de app.
4. U maakt doelgroepen in de lijst met profielen om te controleren of een **klant** heeft in de laatste drie dagen een betrokkenheid gemaakt.
5. U creeert een verlaten product doorbladert reis binnen [!DNL Adobe Journey Optimizer].
6. Werk zo nodig met de **gegevenspartner** voor de activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert de toestemming en verzendt de diverse gevormde acties.

>[!TAB Abandoned Cart Scenario]

Het verlaten kartscenario is van toepassing wanneer de producten in het karretje zijn geplaatst maar nog niet op zowel de website als de mobiele app zijn gekocht. Bovendien worden campagnes voor betaalde media gestart en gestopt met deze methode.<p>![Door de klant verlaten kaartscenario op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Door de klant verlaten kaartscenario op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets, toelaat voor [!UICONTROL Profile].
2. U voert gegevens in Experience Platform in via Web SDK, Mobile SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U voegt extra profielgegevens in, die via identiteitsgrafieken kunnen worden gekoppeld aan de geverifieerde webbezoeker en/of de mobiele gebruiker van de app.
4. U maakt doelgroepen in de lijst met profielen om te controleren of een **klant** heeft een artikel in hun winkelwagentje geplaatst, maar heeft de aankoop niet voltooid. De **[!UICONTROL Add to cart]** de gebeurtenis tikt van een tijdopnemer die 30 minuten wacht, dan controleert aankoop. Als er geen aankoop is gedaan, wordt de **klant** wordt toegevoegd aan de **[!UICONTROL Abandon Cart]** publiek.
5. Je maakt een verlaten cartooptocht in [!DNL Adobe Journey Optimizer].
6. Werk zo nodig met de **gegevenspartner** voor de activering van het publiek naar de gewenste betaalmedia-bestemmingen.
7. [!DNL Adobe Journey Optimizer] controleert de toestemming en verzendt de diverse gevormde acties.

>[!TAB Scenario voor orderbevestiging]

Het bevestigingsscenario voor bestellingen is vooral gericht op productaankopen via de website en de mobiele app.<p>![Bevestigingsscenario op hoog niveau voor bestellingen van klanten: visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Bevestigingsscenario op hoog niveau voor bestellingen van klanten: visueel overzicht."){width="1920" zoomable="yes"}</p>

1. U creeert schema&#39;s en datasets, dan laat voor toe [!UICONTROL Profile].
2. U voert gegevens in Experience Platform in via Web SDK, Mobile SDK of API. Ook kan de gegevensverbinding van Analytics worden gebruikt, maar kan in reisvertraging resulteren.
3. U voegt extra profielgegevens in, die via identiteitsgrafieken kunnen worden gekoppeld aan de geverifieerde webbezoeker en/of de mobiele gebruiker van de app.
4. U maakt een bevestigingstraject in [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] verzendt een bericht van de ordesbevestiging gebruikend het aangewezen kanaal.

>[!ENDTABS]

Lees de onderstaande secties door om alle stappen in de bovenstaande overzichten op hoog niveau te voltooien. Deze bevatten koppelingen naar meer informatie en meer gedetailleerde instructies.

### Schema&#39;s maken en veldgroepen opgeven {#schema-design}

De middelen van het Gegevensmodel van de ervaring (XDM) worden beheerd in [!UICONTROL Schemas] werkruimte in [!DNL Adobe Experience Platform]. U kunt de belangrijkste bronnen bekijken en verkennen die door [!DNL Adobe] (bijvoorbeeld veldgroepen) en maak aangepaste bronnen en schema&#39;s voor uw organisatie.

Meer informatie over het maken van [schema&#39;s](/help/xdm/home.md), zie de [Schema-zelfstudie maken.](/help/xdm/tutorials/create-schema-ui.md) en [Uw klantgegevens modelleren met XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

Er zijn vier schemaontwerpen die voor het re-engagement gebruikscase worden gebruikt. Voor elk schema moeten specifieke velden worden ingesteld. U moet toelaten dat het schema in het Profiel van de Klant in real time wordt omvat. Voor meer informatie over het toelaten van het schema voor gebruik in het Profiel van de Klant In real time, lees [laat een schema voor het Profiel van de Klant in real time toe](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### Klantkenmerkenschema

Dit schema wordt gebruikt om de profielgegevens te structureren en van verwijzingen te voorzien die omhoog uw klanteninformatie maken. Deze gegevens worden doorgaans opgenomen in [!DNL Adobe Experience Platform] via uw CRM of vergelijkbare systeem en is noodzakelijk om te verwijzen naar klantgegevens die worden gebruikt voor personalisatie, marketingtoestemming en verbeterde publiekscapaciteiten.

Het schema met klantkenmerken wordt weergegeven door een [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md) klasse, die de volgende veldgroepen bevat:

+++Persoonlijke Contactgegevens (Veldgroep)

[Persoonlijke contactgegevens](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel van Afzonderlijke XDM die de contactinformatie voor een individuele persoon beschrijft.

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `mobilePhone.number` | Vereist | Het mobiele telefoonnummer van de persoon, dat wordt gebruikt voor SMS. |
| `personalEmail.address` | Vereist | Het e-mailadres van de persoon. |

+++

+++Externe gegevens van de Controle van het Bronsysteem (de Groep van het Gebied)

[Kenmerken externe bronsysteemcontrole](/help/xdm/data-types/external-source-system-audit-attributes.md) is een standaardgegevenstype van de Gegevens van de Ervaring Model (XDM) dat controledetails over een extern bronsysteem vangt.

+++

+++Groepen van het Toegelaten en van het Referentieveld (de Groep van het Gebied)

De [Inhoud en voorkeuren](/help/xdm/field-groups//profile/consents.md) veldgroep biedt één objecttype veld, toestemmingen, voor het vastleggen van toestemmings- en voorkeursgegevens.

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

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website en/of bijbehorende digitale platforms voorkomt. Deze gegevens worden doorgaans opgenomen in [!DNL Adobe Experience Platform] via [Web SDK](/help/edge/home.md) en is noodzakelijk om de diverse doorbladeren en omzettingsgebeurtenissen te verwijzen die voor het teweegbrengen van reizen, gedetailleerde online klantenanalyse, en verbeterde publieksmogelijkheden worden gebruikt.

Het schema voor digitale transacties van de klant wordt vertegenwoordigd door een [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) klasse.

+++XDM ExperienceEvent (Class)

De [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) klasse bevat de volgende veldgroepen:

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `_id` | Vereist | Identificeert uniek individuele gebeurtenissen die in worden opgenomen [!DNL Adobe Experience Platform]. |
| `timestamp` | Vereist | Een tijdstempel volgens ISO 8601 van het tijdstip van de gebeurtenis, opgemaakt volgens RFC 3339, sectie 5.6. Deze tijdstempel moet in het verleden voorkomen. |
| `eventType` | Vereist | Een tekenreeks die het type categorie voor de gebeurtenis aangeeft. |

+++

+++Details eindgebruiker-id (veldgroep)

De [Gegevens van eindgebruiker](/help/xdm/field-groups/event/enduserids.md) de veldgroep wordt gebruikt om de identiteitsinformatie van een individu over verscheidene toepassingen van de Adobe te beschrijven.

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

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op platforms buiten uw website voorkomt. Deze gegevens worden doorgaans opgenomen in [!DNL Adobe Experience Platform] van een POS (of vergelijkbaar systeem) en meestal gestreamd naar Platform via een API-verbinding. Zijn doel is de diverse off-line omzettingsgebeurtenissen van verwijzingen te voorzien die voor het teweegbrengen van reizen, diepe online en off-line klantenanalyse, en verbeterde publieksmogelijkheden worden gebruikt.

Het schema voor offline transacties van de klant wordt vertegenwoordigd door een [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) klasse.

+++XDM ExperienceEvent (Class)

De [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) klasse bevat de volgende veldgroepen:

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `_id` | Vereist | Identificeert uniek individuele gebeurtenissen die in worden opgenomen [!DNL Adobe Experience Platform]. |
| `timestamp` | Vereist | Een tijdstempel volgens ISO 8601 van het tijdstip van de gebeurtenis, opgemaakt volgens RFC 3339, sectie 5.6. Deze tijdstempel moet in het verleden voorkomen. |
| `eventType` | Vereist | Een tekenreeks die het type categorie voor de gebeurtenis aangeeft. |

+++

+++Details van de Handel (de Groep van het Gebied)

De [Handelsgegevens](/help/xdm/field-groups/event/commerce-details.md) de veldgroep wordt gebruikt om handelsgegevens zoals productinformatie (SKU, naam, hoeveelheid), en standaardkartverrichtingen (orde, checkout, verlaten) te beschrijven.

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

[Persoonlijke contactgegevens](/help/xdm/field-groups/profile/personal-contact-details.md) is een standaardschemagebiedgroep voor de klasse van het Profiel van Afzonderlijke XDM die de contactinformatie voor een individuele persoon beschrijft.

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
>Dit is een optionele implementatie als u de [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md).

Dit schema wordt gebruikt om de gebeurtenisgegevens te structureren en te verwijzen die uw klantenactiviteit vormen die op uw website en/of bijbehorende digitale platforms voorkomt. Dit schema is gelijkaardig aan het schema van de Transacties van de Klant Digitale maar verschilt in die zin dat het bedoeld is om te worden gebruikt wanneer [Web SDK](/help/edge/home.md) is geen optie voor gegevensverzameling; daarom is dit schema nodig wanneer u het [!DNL Adobe Analytics Source Connector] om uw online gegevens te verzenden naar [!DNL Adobe Experience Platform] hetzij als primaire of secundaire gegevensstroom.

De [!DNL Adobe] het schema van de Webschakelaar wordt vertegenwoordigd door een [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) klasse.

+++XDM ExperienceEvent (Class)

De [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) klasse bevat de volgende veldgroepen:

| Velden | Vereiste | Beschrijving |
| --- | --- | --- |
| `_id` | Vereist | Identificeert uniek individuele gebeurtenissen die in worden opgenomen [!DNL Adobe Experience Platform]. |
| `timestamp` | Vereist | Een tijdstempel volgens ISO 8601 van het tijdstip van de gebeurtenis, opgemaakt volgens RFC 3339, sectie 5.6. Deze tijdstempel moet in het verleden voorkomen. |
| `eventType` | Vereist | Een tekenreeks die het type categorie voor de gebeurtenis aangeeft. |

+++

+++Adobe Analytics ExperienceEvent-sjabloon (veldgroep)

De [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) veldgroep legt algemene meetgegevens vast die door Adobe Analytics worden verzameld.

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

### Een dataset maken op basis van een schema {#create-datasets}

Een dataset is een opslag en beheersstructuur voor een groep gegevens. Elk schema voor intelligente scenario&#39;s van de re-engagement zou zijn eigen dataset moeten hebben.

Voor meer informatie over het maken van een [gegevensset](/help/catalog/datasets/overview.md) in een schema, lees de [UI-gids voor gegevensbestanden](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Gelijkaardig aan de stap om een schema tot stand te brengen, moet u toelaten dat de dataset in het Profiel van de Klant in real time wordt omvat. Voor meer informatie over het toelaten van de dataset voor gebruik in het Profiel van de Klant in real time, zie zelfstudie over [gegevens in realtime-klantprofiel plaatsen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).

### Toestemming en gegevensbeheer {#privacy-consent}

>[!IMPORTANT]
>
>Het is een wettelijke vereiste om klanten de mogelijkheid te bieden zich niet langer te abonneren op het ontvangen van communicatie van een merk, en om ervoor te zorgen dat deze keuze wordt nagekomen. Meer informatie over de toepasselijke wetgeving vindt u in het [Overzicht van privacyregels](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

#### Toestemmingsbeleid

Als u een pad voor opnieuw toewijzen maakt, kunt u het volgende toevoegen [toestemmingsbeleid](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html):

* Indien `consents.marketing.email.val = "Y"` vervolgens kunt u e-mailen
* Indien `consents.marketing.sms.val = "Y"` Dan kan SMS
* Indien `consents.marketing.push.val = "Y"` vervolgens kan duwen
* Indien `consents.share.val = "Y"` kan vervolgens adverteren

#### Etikettering en handhaving van gegevensbeheer

Als u een pad voor opnieuw toewijzen maakt, kunt u het volgende toevoegen [Labels voor gegevensbeheer](/help/data-governance/labels/overview.md):

* Persoonlijke e-mailadressen worden gebruikt als direct identificeerbare gegevens die worden gebruikt om een specifieke persoon te identificeren of contact met hem te krijgen in plaats van met een apparaat.
   * `personalEmail.address = I1`

#### Beleid voor gegevensgebruik

Er zijn geen [beleid voor gegevensgebruik](/help/data-governance/policies/overview.md) vereist voor het verlaten product doorbladert scenario. U dient echter het volgende in overweging te nemen:

* Gevoelige gegevens beperken
* Onsite reclame beperken
* E-maildoelen beperken
* Doelstelling voor meerdere sites beperken
* Het combineren van rechtstreeks identificeerbare gegevens met anonieme gegevens beperken

### Soorten publiek maken {#create-audience}

In de scenario&#39;s voor herbetrokkenheid wordt gebruikgemaakt van publiek om specifieke kenmerken of gedragingen te definiëren die worden gedeeld door een subset van profielen in uw profielarchief om een verhandelbare groep personen van uw klantenbasis te onderscheiden. Soorten publiek kan op meerdere manieren worden gemaakt [!DNL Adobe Experience Platform].

Voor meer informatie over het maken van een publiek leest u de [gebruikersinterface-handleiding voor publieksservices](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Voor meer informatie over hoe u direct samenstelt [Soorten publiek](/help/segmentation/home.md), lees de [Handleiding voor compositie van publiek](/help/segmentation/ui/audience-composition.md).

Voor meer informatie over hoe te om publiek door Platform-afgeleide publieksdefinities te bouwen, lees [Handleiding voor de gebruikersinterface van Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Verlaten door product Bladeren Scenario]

Dit publiek wordt gemaakt als een uitbreiding op het klassieke scenario &#39;Kart Abandenvironment&#39;. Terwijl het verlaten van het winkelwagentje zich doorgaans concentreert op een toevoeging van winkelwagentjes zonder een latere aankoop binnen een bepaalde periode, zoekt dit publiek naar een eerdere betrokkenheid, met name diegenen die mogelijk door een bepaald product hebben gebladerd maar het niet aan hun winkelwagentje hebben toegevoegd en binnen een bepaalde tijd geen vervolgactiviteit op uw site hadden. Dit publiek helpt om uw merk &quot;bovenaan&quot;voor klanten te houden die aan deze inclusiecriteria voldoen en kan ook voor klanten worden gebruikt waarvan digitale eigenschappen van een traditioneel e-commercemodel kunnen verschillen.

+++Afgeknot productweergave zonder betrokkenheid in de afgelopen drie dagen

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers producten online bekeken, en niet (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegden aan kartgebeurtenissen) in de drie dagen na het volgen begonnen.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.productViews`
* en `THEN` (opeenvolgende gebeurtenis) exclude `eventType: commerce.procuctListAdds` of `application.launch` of `web.webpagedetails.pageViews` of `commerce.purchases` (inclusief online en offline)
   * `Timestamp: > 3 days after productView`

+++

+++Productweergave met betrokkenheid in de laatste drie dagen

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers producten online bekeken, en (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegen aan kartgebeurtenissen) in de drie dagen na het volgen van de verbinding in dienst genomen.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.productViews`
* en `THEN` (sequentiële gebeurtenis) include `eventType: commerce.procuctListAdds` of `application.launch` of `web.webpagedetails.pageViews` of `commerce.purchases` (inclusief online en offline)
   * `Timestamp: > 3 days after productView`

+++streaming betrokkenheid in de laatste dag

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegen aan kartgebeurtenissen) in de afgelopen 1 dag hebben betrokken.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 1 day` (Streaming)

+++

+++Betrokkenheidsbatch in de laatste drie dagen

De volgende gebeurtenis wordt gebruikt voor het verlaten productbladerscenario waar de gebruikers (plaatsbezoeken, toepassingsbezoeken, online aankoop, off-line aankoop, en toevoegen aan kartgebeurtenissen) in de laatste drie dagen hebben betrokken.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `EventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 3 days` (Batch)

+++

>[!TAB Abandoned Cart Scenario]

Dit publiek wordt gemaakt ter ondersteuning van het klassieke scenario &#39;Kart Abandenvironment&#39;. Het doel is om klanten te vinden die een product aan hun winkelwagentje hebben toegevoegd maar uiteindelijk niet met een aankoop hebben gevolgd. Dit publiek zal niet alleen uw merk &quot;bovenaan&quot;voor uw klanten houden maar ook de producten die zij zonder een verdere aankoop hebben verlaten.

De volgende gebeurtenissen worden gebruikt voor het verlaten kartscenario waar de gebruikers een product aan hun karretje tussen 1 en 4 dagen geleden toevoegden, maar de aankoop niet voltooiden of hun karretje ontruimen.

Voor het instellen van dit publiek zijn de volgende velden en voorwaarden vereist:

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

De beschrijving voor het verlaten kartscenario verschijnt als:

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Scenario voor orderbevestiging]

Voor deze reis is geen publiek nodig.

>[!ENDTABS]

### Reisinstallatie in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] omvat niet alles die in de diagrammen wordt getoond. Alles [betaalde mediasleutels](/help/destinations/catalog/social/overview.md) worden gemaakt in [!UICONTROL Destinations].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) helpt u verbonden, contextafhankelijke en persoonlijke ervaringen aan uw klanten te leveren. De reis van de klant is het volledige proces van interactie van een klant met het merk. Voor elke gebruiksreis is specifieke informatie vereist. Hieronder staan de precieze gegevens die nodig zijn voor elke reis.

>[!BEGINTABS]

>[!TAB Verlaten door product Bladeren Scenario]

Het verlaten productbladerscenario richt verlaten product het doorbladeren op zowel de website als mobiele app.<p>![Door de klant verlaten product bladeren scenario&#39;s op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/re-engagement-journey.png "Door de klant verlaten product bladeren scenario&#39;s op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

+++Gebeurtenissen

* Gebeurtenis 1: productweergaven
   * Schema: digitale transacties van klanten
   * Velden:
      * `eventType`
   * Voorwaarde:
      * `eventType = commerce.productViews`
      * Velden:
         * `commerce.productViews.id`
         * `commerce.productViews.value`
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

>[!TAB Abandoned Cart Scenario]

Het verlaten kartscenario richt producten die in de kar zijn geplaatst maar nog niet op zowel de website als de mobiele app gekocht.<p>![Door de klant verlaten kaartscenario op hoog niveau visueel overzicht.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Door de klant verlaten kaartscenario op hoog niveau visueel overzicht."){width="1920" zoomable="yes"}</p>

+++Gebeurtenissen

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

>[!TAB Scenario voor orderbevestiging]

Het bevestigingsscenario voor bestellingen is vooral gericht op productaankopen via de website en de mobiele app.<p>![Bevestigingsscenario op hoog niveau voor bestellingen van klanten: visueel overzicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Bevestigingsscenario op hoog niveau voor bestellingen van klanten: visueel overzicht."){width="1920" zoomable="yes"}</p>

+++Gebeurtenissen

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

Streaming publiek exportbestemmingen (zoals Facebook, Google Customer Match, Google DV360) ondersteunen verschillende identiteiten van klantgegevens:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

het publiek van de verlaten winkelwagentje wordt beoordeeld als een streaming publiek en kan daarom door het bestemmingskader voor dit gebruiksgeval worden gebruikt .

* Stream/activering
   * [Reclame](/help/destinations/catalog/advertising/overview.md)/[Betaalde media en sociale media](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Streaming doel](/help/destinations/catalog/streaming/http-destination.md)
   * [Aangepast doel gemaakt met Destination SDK.](/help/destinations/destination-sdk/overview.md). Als u een Real-Time CDP Ultimate-klant bent, kunt u ook een persoonlijke [aangepast doel met Destination SDK](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)
