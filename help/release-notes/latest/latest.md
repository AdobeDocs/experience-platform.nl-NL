---
title: Aanvullende informatie over Adobe Experience Platform
description: Aanvullende informatie van januari 2024 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 21 februari 2024**

Updates voor bestaande functies in Experience Platform:

- [Waarschuwingen](#alerts)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Sandboxes](#sandboxes)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op gebeurtenisgebaseerde waarschuwingen voor verschillende platformactiviteiten. U kunt zich abonneren op verschillende waarschuwingsregels via de [!UICONTROL Alerts] in de gebruikersinterface van het Platform en kan ervoor kiezen waarschuwingsberichten te ontvangen binnen de gebruikersinterface zelf of via e-mailmeldingen.
**Nieuwe of bijgewerkte functies**
| Functie | Beschrijving | | — | — | | Tabblad Waarschuwingsgeschiedenis | Als beheerder van een Experience Platform kunt u met de functie Waarschuwingsabonnees beheren een waarschuwing toewijzen aan een gebruikers-id voor een Adobe, een extern e-mailadres of een lijst met e-mailgroepen. Zie de klasse [UI-documentatie met waarschuwingen](../../observability/alerts/ui.md) voor meer informatie over het geschiedenislusje. |



Voor meer informatie over waarschuwingen leest u de [[!DNL Observability Insights] overzicht](../../observability/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden, waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [Web In-App Overseinen steun in Web SDK](../../edge/personalization/web-in-app-messaging.md) | De Adobe Experience Platform Web SDK biedt nu ondersteuning voor Web In-App Messaging-configuratie voor Adobe Journey Optimizer-campagnes. |

{style="table-layout:auto"}

Voor meer informatie over gegevensverzamelingen leest u de [overzicht van gegevensverzamelingen](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [PX-verbinding ophalen](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX is een product ervaringsplatform dat productteams in staat stelt te begrijpen hoe gebruikers hun producten gebruiken, feedback te verzamelen en in-app contracten zoals productanalyses te maken om gebruikers aan boord te krijgen en producten te adopteren. |
| [Mailchimp-tagverbinding](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp is een populair platform voor marketingautomatisering en e-mailmarketingservice. U kunt de schakelaar van de Markeringen van Mailchimp gebruiken aan structuur, etiket, of categoriseer uw contacten. |
| [SAP Commerce-verbinding](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce is een op de cloud gebaseerde e-commerceoplossing voor B2B- en B2C-ondernemingen die beschikbaar is als onderdeel van het SAP Customer Experience-portfolio. U kunt deze bestemming gebruiken om uw klantendetails binnen de Handel van SAP van een bestaand publiek van de Experience Platform bij te werken. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Accountsoorten activeren, algemeen beschikbaar | De functionaliteit om het publiek van de rekening aan bepaalde bestemmingen te activeren is nu over het algemeen beschikbaar voor bedrijven die [Zakelijk-naar-zakelijk](/help/rtcdp/overview.md#rtcdp-b2b) en [Van bedrijf tot persoon](/help/rtcdp/overview.md#rtcdp-b2p) edities van Real-time Customer Data Platform. Lees de zelfstudie aan [activeren van accountpubliek](/help/destinations/ui/activate-account-audiences.md) om volledige informatie, met inbegrip van gesteunde bestemmingen te krijgen. |
| Digital Markets Act-instrumenten voor toestemmingshandhaving voor Google-bestemmingen | Google brengt wijzigingen in de [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Klantenovereenkomst](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)en de [Display &amp; Video 360-API](https://developers.google.com/display-video/api/guides/getting-started/overview) ter ondersteuning van de in het kader van de [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in de Europese Unie[Beleid voor EU-gebruikerstoestemming](https://www.google.com/about/company/user-consent-policy/)). Verwacht wordt dat de handhaving van deze wijzigingen in de toestemmingsvereisten met ingang van 6 maart 2024 in werking zal treden. <br/><br/> Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven bij het uploaden van publieksgegevens. Als Google-partner beschikt Adobe over de benodigde instrumenten om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.<br/><br/>Klanten die een privacyschild voor Adobe hebben aangeschaft en een [toestemmingsbeleid](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) om profielen zonder toestemming uit te filteren, hoeft u geen actie te ondernemen.<br/><br/>Klanten die geen privacyschild voor Adobe hebben aangeschaft, moeten de [segmentdefinitie](../../segmentation/home.md#segment-definitions) mogelijkheden binnen [Segment Builder](../../segmentation/ui/segment-builder.md) om profielen zonder toestemming uit te filteren, zodat de bestaande Real-Time CDP Google-bestemmingen zonder onderbreking kunnen worden gebruikt. |
| [!BADGE Beta]{type=Informative} toewijzingsvelden opnieuw ordenen voor batchdoelen | U kunt nu de volgorde van de kolommen in uw CSV-export wijzigen door de toewijzingsvelden in het dialoogvenster [toewijzing](../../destinations/ui/activate-batch-profile-destinations.md#mapping) stap. De volgorde van de toegewezen velden in de gebruikersinterface is afhankelijk van de volgorde van de kolommen in het geëxporteerde CSV-bestand, van boven naar beneden, waarbij de bovenste rij de meest linkse kolom in het CSV-bestand is. <br/><br/> Deze functie is in bètaversie beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |
| [!BADGE Beta]{type=Informative} Vooraf ingestelde standaard exportschema&#39;s voor batchbestemmingen | Experience Platform stelt nu automatisch een standaardschema in voor elke bestandsuitvoer. Zie de documentatie op [exporteren van publiek plannen](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) leren hoe te om het standaardprogramma te wijzigen. <br/><br/> Deze functie is in bètaversie beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |
| [!BADGE Beta]{type=Informative} Bulk geeft publiekactiveringsschema&#39;s voor batchbestemmingen uit | U kunt het activeringsschema voor meerdere soorten publiek nu bulksgewijs bewerken vanuit de categorie [Activeringsgegevens](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) pagina. <br/><br/> Deze functie is in bètaversie beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |
| [!BADGE Beta]{type=Informative} Bulkexportbestanden op aanvraag exporteren naar batchbestemmingen | U kunt publiek in bulk naar partijbestemmingen nu uitvoeren, door [bestanden op aanvraag exporteren](../../destinations/ui/export-file-now.md) functionaliteit. <br/><br/> Deze functie is in bètaversie beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gereedschap Sandbox | Naast nu ondersteunende objecttypen voor toestemmings- en governanceregels, gebruikt u sandboxgereedschappen om schema&#39;s te importeren zonder dat verenigde profielen zijn ingeschakeld, controleert u op ontbrekende kenmerken in de doelsandbox tijdens het importeren van een segment en gebruikt u standaard het bestaande samenvoegingsbeleid. Raadpleeg voor meer informatie over deze functies de [UI-hulplijn voor gereedschap sandbox](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Voor meer informatie over sandboxen leest u de [sandboxen, overzicht](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Nieuwe functie**

| Functie | Beschrijving |
| ------- | ----------- |
| Accountpubliek | Accountpubliek is nu over het algemeen beschikbaar! U kunt nu de segmentatie van uw account gebruiken om de volledige versnelling en verfijning van de ervaring van de segmentatie van de marketing te brengen van op mensen gebaseerd publiek naar op account gebaseerd publiek in zowel de B2B- als de B2P-edities van het Real-Time Klantplatform. Met deze release kunt u op mensen gebaseerde doelgroepen gebruiken als voorspelling voor op account gebaseerde doelgroepen, zoekmogelijkheden toevoegen, het gebruik van aangepaste entiteiten ondersteunen en zijn compatibel met gegevensbeheer. Lees voor meer informatie over deze functie de [overzicht van publiek publiek van account](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] bron | Gebruik de [[!DNL Acxiom Prospecting Data Import] bron](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) om gegevens van terug te winnen en in kaart te brengen [!DNL Acxiom] de dienst van het vooruitzicht aan Experience Platform. |

{style="table-layout:auto"}

Lees voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
