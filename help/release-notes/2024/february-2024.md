---
title: Aanvullende informatie voor Adobe Experience Platform van februari 2024
description: Aanvullende informatie voor Adobe Experience Platform van februari 2024.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 99%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: 21 februari 2024**

Updates van bestaande functies in Experience Platform:

- [Waarschuwingen](#alerts)
- [Dataverzameling](#data-collection)
- [Bestemmingen](#destinations)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Tabblad Waarschuwingsgeschiedenis | Als beheerder van een Experience Platform kunt u met de functie voor waarschuwingsabonnees beheren een waarschuwing toewijzen aan een gebruikers-ID, een extern e-mailadres of een lijst met e-mailgroepen van Adobe. Voor meer informatie kunt u de [gebruikersinterfacedocumentatie voor waarschuwingen](/help/observability/alerts/ui.md) raadplegen voor meer informatie over het tabblad Geschiedenis. |

{style="table-layout:auto"}

Voor meer informatie over waarschuwing leest u het [[!DNL Observability Insights] overzicht &#x200B;](/help/observability/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Web In-App Overseinen steun in Web SDK | De Adobe Experience Platform Web SDK biedt nu ondersteuning voor Web In-App Messaging-configuratie voor Adobe Journey Optimizer-campagnes. |

{style="table-layout:auto"}

Voor meer informatie over dataverzamelingen leest u het [overzicht van dataverzamelingen](/help/tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](/help/data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](/help/data-prep/home.md). -->

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen** {#new-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [Gainsight PX-verbinding](/help/destinations/catalog/analytics/gainsight-px.md) | Gainsight PX is een productervaringsplatform waarmee productteams inzicht kunnen krijgen de manier waarop gebruikers de producten gebruiken, feedback kunnen verzamelen, en in-app contracten kunnen maken zoals productanalyses om gebruikers aan boord te krijgen en producten te gaan gebruiken. |
| [Mailchimp Tags-verbinding](/help/destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp is een populair platform voor marketingautomatisering en e-mailmarketingservice. Met de Mailchimp Tags-connector kunt u contactpersonen structureren, labelen of categoriseren. |
| [SAP Commerce-verbinding](/help/destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce is een cloudgebaseerde e-commerceoplossing voor B2B- en B2C-bedrijven en is beschikbaar als onderdeel van de SAP Customer Experience-portfolio. U kunt deze bestemming gebruiken om klantgegevens binnen SAP Commerce van een bestaand publiek van de Experience Platform bij te werken. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Accountdoelgroepen die algemeen beschikbaar zijn activeren | De functionaliteit om accountdoelgroepen voor bepaalde bestemmingen te activeren is nu algemeen beschikbaar voor bedrijven die de [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) en [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-edities van Real-Time Customer Data Platform aanschaffen. Lees de tutorial over [het activeren van accountdoelgroepen](/help/destinations/ui/activate-account-audiences.md) voor volledige informatie, inclusief ondersteunde bestemmingen. |
| Tools voor handhaving toestemming van de Digital Markets Act voor Google-bestemmingen | Google brengt wijzigingen door in de [Google Ads-API](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) en de [Display &amp; Video 360-API](https://developers.google.com/display-video/api/guides/getting-started/overview) ter ondersteuning van de nalevings- en toestemmingsvereisten die zijn gedefinieerd in de [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_nl) (DMA) in de Europese Unie ([EU-beleid inzake toestemming van gebruikers](https://www.google.com/about/company/user-consent-policy/)). De verwachting is dat deze wijzigingen in de toestemmingsvereisten vanaf 6 maart 2024 van kracht worden. <br/><br/> Om te voldoen aan het EU-beleid inzake toestemming van gebruikers en om doelgroeplijsten te blijven maken voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat ze toestemming van de eindgebruiker doorgeven bij het uploaden van doelgroepgegevens. Als Google-partner beschikt Adobe over de benodigde tools om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.<br/><br/>Klanten die Adobe Privacy &amp; Security Shield hebben aangeschaft en een [toestemmingsbeleid](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) hebben geconfigureerd om profielen waarvoor geen toestemming is verleend, te filteren, hoeven geen actie te ondernemen.<br/><br/>Klanten die Adobe Privacy &amp; Security Shield niet hebben aangeschaft, moeten de mogelijkheden voor [segmentdefinitie](/help/segmentation/home.md#segment-definitions) in [Segment Builder](/help/segmentation/ui/segment-builder.md) gebruiken om niet-toegestane profielen eruit te filteren, zodat ze de bestaande Real-Time CDP Google-bestemmingen zonder onderbreking kunnen blijven gebruiken. |
| [!BADGE Beta]{type=Informative} Toewijzingsvelden opnieuw ordenen voor batchbestemmingen | U kunt nu de volgorde van de kolommen in uw CSV-exporten wijzigen door de toewijzingsvelden in de stap [toewijzing](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) te slepen en neer te zetten. De volgorde van de toegewezen velden in de gebruikersinterface komt overeen met de volgorde van de kolommen in het geëxporteerde CSV-bestand, van boven naar beneden, waarbij de bovenste rij de meest linkse kolom in het CSV-bestand is. <br/><br/> Deze functie bevindt zich in de bètafase en is alleen beschikbaar voor geselecteerde klanten. Neem contact op met uw Adobe-vertegenwoordiger als u toegang tot deze functie wilt aanvragen. |
| [!BADGE Beta]{type=Informative} Vooraf geselecteerde standaard exportschema&#39;s voor batchbestemmingen | Experience Platform stelt nu automatisch een standaardschema in voor elke bestandsexport. Zie de documentatie over [het plannen van doelgroepexporten](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor meer informatie over het wijzigen van het standaardschema. <br/><br/> Deze functie bevindt zich in de bètafase en is alleen beschikbaar voor geselecteerde klanten. Neem contact op met uw Adobe-vertegenwoordiger als u toegang tot deze functie wilt aanvragen. |
| [!BADGE Beta]{type=Informative} Doelgroepactiveringsschema&#39;s in bulk bewerken voor batchbestemmingen | U kunt het activeringsschema voor meerdere doelgroepen nu in bulk bewerken via de pagina [Activeringsgegevens](/help/destinations/ui/destination-details-page.md#bulk-edit-schedule). <br/><br/> Deze functie bevindt zich in de bètafase en is alleen beschikbaar voor geselecteerde klanten. Neem contact op met uw Adobe-vertegenwoordiger als u toegang tot deze functie wilt aanvragen. |
| [!BADGE Beta]{type=Informative} Bestanden op aanvraag in bulk exporteren naar batchbestemmingen | U kunt doelgroepen nu in bulk naar batchbestemmingen exporteren via de functionaliteit voor [bestanden op aanvraag te exporteren](/help/destinations/ui/export-file-now.md). <br/><br/> Deze functie bevindt zich in de bètafase en is alleen beschikbaar voor geselecteerde klanten. Neem contact op met uw Adobe-vertegenwoordiger als u toegang tot deze functie wilt aanvragen. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](/help/destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen biedt Experience Platform sandboxes die één Experience Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verbeterd.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Sandbox-tools | Naast de ondersteuning van objecttypen voor toestemmings- en governanceregels, kunt u nu ook sandbox-tools gebruiken om schema&#39;s te importeren zonder dat uniforme profielen zijn ingeschakeld, controleren op ontbrekende kenmerken in de doelsandbox bij het importeren van een segment en standaard het bestaande samenvoegingsbeleid gebruiken. Zie de [Handleiding voor de gebruikersinterface voor sandbox-tools](/help/sandboxes/ui/sandbox-tooling.md) voor meer informatie over deze functies. |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, raadpleegt u het [Overzicht van sandboxes](/help/sandboxes/home.md).

## Segmentatieservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, prospects, gebruikers of organisaties) segmenteren in doelgroepen. U kunt doelgroepen maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile]-gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Experience Platform] en zijn eenvoudig toegankelijk via elke Adobe-oplossing.

**Nieuwe functie**

| Functie | Beschrijving |
| ------- | ----------- |
| Accountdoelgroepen | Accountdoelgroepen zijn nu algemeen beschikbaar! U kunt nu accountsegmentatie gebruiken om te profiteren van het volledige gemak en de verfijning van de marketingsegmentatie-ervaring van op mensen gebaseerde doelgroepen in op accounts gebaseerde doelgroepen in zowel de B2B- als de B2P-editie van het Real-Time Customer Experience Platform. Met deze release kunt u op personen gebaseerde doelgroepen gebruiken als basis voor op accounts gebaseerde doelgroepen. Ook worden er zoekmogelijkheden toegevoegd, wordt het gebruik van aangepaste entiteiten ondersteund en voldoet de release aan datagovernance. Voor meer informatie over deze functie, raadpleegt u het [overzicht van accountdoelgroepen](/help/segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom]-bron | Gebruik de [[!DNL Acxiom Prospecting Data Import] bron](/help/sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) om gegevens van [!DNL Acxiom] prospect service op te halen en toe te wijzen aan Experience Platform. |

{style="table-layout:auto"}

Voor meer informatie over bronnen, raadpleegt u het [overzicht van bronnen](/help/sources/home.md).
