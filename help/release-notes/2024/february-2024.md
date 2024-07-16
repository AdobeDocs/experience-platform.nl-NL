---
title: Opmerkingen bij de release van Adobe Experience Platform, februari 2024
description: In de release van februari 2024 staat een opmerking voor Adobe Experience Platform.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: aa33f7006b1a3abf7d19ffe3e0d5e5ee39fe9a5d
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 2%

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

Met Experience Platform kunt u zich abonneren op gebeurtenisgebaseerde waarschuwingen voor verschillende platformactiviteiten. U kunt zich abonneren op verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van het platform en u kunt ervoor kiezen waarschuwingsberichten te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Tabblad Waarschuwingsgeschiedenis | Als beheerder van een Experience Platform kunt u met de functie Waarschuwingsabonnees beheren een waarschuwing toewijzen aan een gebruikers-id voor een Adobe, een extern e-mailadres of een lijst met e-mailgroepen. Voor meer informatie, zie het [ alarm UI documentatie ](../../observability/alerts/ui.md) voor meer informatie over het geschiedenislusje. |

{style="table-layout:auto"}

Meer over alarm leren, lees het [[!DNL Observability Insights]  overzicht ](../../observability/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| [ de steun van het Overseinen van het Web in-App in Web SDK ](../../web-sdk/personalization/web-in-app-messaging.md) | De Adobe Experience Platform Web SDK biedt nu ondersteuning voor Web In-App Messaging-configuratie voor Adobe Journey Optimizer-campagnes. |

{style="table-layout:auto"}

Meer over gegevensinzamelingen leren, lees het [ overzicht van gegevensinzamelingen ](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [ verzamelen PX verbinding ](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX is een product ervaringsplatform dat productteams in staat stelt te begrijpen hoe gebruikers hun producten gebruiken, feedback te verzamelen en in-app contracten zoals productanalyses te maken om gebruikers aan boord te krijgen en producten te adopteren. |
| [ de verbinding van de Markeringen van Mailchimp ](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp is een populair platform voor marketingautomatisering en e-mailmarketingservice. U kunt de schakelaar van de Markeringen van Mailchimp gebruiken aan structuur, etiket, of categoriseer uw contacten. |
| [ de verbinding van SAP Commerce ](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce is een op de cloud gebaseerde e-commerceoplossing voor B2B- en B2C-bedrijven en is beschikbaar als onderdeel van de SAP Customer Experience-portfolio. U kunt deze bestemming gebruiken om uw klantendetails binnen SAP Commerce van een bestaand publiek van de Experience Platform bij te werken. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Accountsoorten activeren, algemeen beschikbaar | De functionaliteit om rekeningspubliek aan bepaalde bestemmingen te activeren is nu algemeen beschikbaar voor bedrijven die [ zaken-aan-Zaken ](/help/rtcdp/overview.md#rtcdp-b2b) en [ zaken-aan-Persoonlijke ](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-time Customer Data Platform kopen. Lees het leerprogramma op [ activerend rekeningspubliek ](/help/destinations/ui/activate-account-audiences.md) om volledige informatie, met inbegrip van gesteunde bestemmingen te krijgen. |
| Digital Markets Act-instrumenten voor toestemmingshandhaving voor Google-bestemmingen | Google geeft veranderingen in de [ Adds API van Google ](https://developers.google.com/google-ads/api/docs/start), [ Overeenkomst van de Klant ](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) vrij, en [ Vertoning &amp; Video 360 API ](https://developers.google.com/display-video/api/guides/getting-started/overview) om de naleving en toestemmings-gerelateerde vereisten te steunen die onder de [ Wet van de Markten ](https://digital-markets-act.ec.europa.eu/index_en) (DMA) worden bepaald in de Europese Unie ([ EU het Beleid van de Toestemming van de Gebruiker ](https://www.google.com/about/company/user-consent-policy/)). Verwacht wordt dat de handhaving van deze wijzigingen in de toestemmingsvereisten met ingang van 6 maart 2024 in werking zal treden. <br/><br/> Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven wanneer zij publieksgegevens uploaden. Als Google-partner beschikt Adobe over de benodigde instrumenten om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.<br/><br/> Klanten die de Privacy van de Adobe &amp; het Schild van de Veiligheid hebben gekocht en het beleid van de a [ toestemming ](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) hebben gevormd om niet-goedgekeurde profielen uit te filteren hoeven geen actie te ondernemen.<br/><br/> Klanten die geen Adobe Privacy &amp; het Schild van de Veiligheid hebben gekocht moeten de [ segmentdefinitie ](../../segmentation/home.md#segment-definitions) mogelijkheden binnen [ Bouwer van het Segment ](../../segmentation/ui/segment-builder.md) gebruiken om uit niet-goedgekeurde profielen te filtreren, om de bestaande bestemmingen van Real-Time CDP Google zonder onderbreking te blijven gebruiken. |
| [!BADGE  Beta ] {type=Informative} de kaartgebieden van de herschikking voor partijbestemmingen | U kunt de orde van de kolommen in uw uitvoer CSV nu veranderen door de kaartgebieden in de [ in kaart brengende ](../../destinations/ui/activate-batch-profile-destinations.md#mapping) stap te slepen en te laten vallen. De volgorde van de toegewezen velden in de gebruikersinterface is afhankelijk van de volgorde van de kolommen in het geëxporteerde CSV-bestand, van boven naar beneden, waarbij de bovenste rij de meest linkse kolom in het CSV-bestand is. <br/><br/> Deze functie is in bèta beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |
| [!BADGE  Beta ] {type=Informative} Vooraf ingestelde standaard uitvoerprogramma&#39;s voor partijbestemmingen | Experience Platform stelt nu automatisch een standaardschema in voor elke bestandsuitvoer. Zie de documentatie bij [ het plannen publieksuitvoer ](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) leren hoe te om het standaardprogramma te wijzigen. <br/><br/> Deze functie is in bèta beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |
| [!BADGE  Beta ] {type=Informative} Bulk geeft publieksactiveringsprogramma&#39;s voor partijbestemmingen uit | U kunt het activeringsprogramma voor veelvoudige publiek in bulk, van de [ gegevens van de Activering ](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) pagina nu uitgeven. <br/><br/> Deze functie is in bèta beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |
| [!BADGE  Beta ] {type=Informative} Bulk de uitvoerdossiers op bestelling aan partijbestemmingen | U kunt publiek in bulk aan partijbestemmingen, door de [ uitvoerdossiers op bestelling ](../../destinations/ui/export-file-now.md) functionaliteit nu uitvoeren. <br/><br/> Deze functie is in bèta beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Gereedschap Sandbox | Naast nu ondersteunende objecttypen voor toestemmings- en governanceregels, gebruikt u sandboxgereedschappen om schema&#39;s te importeren zonder dat verenigde profielen zijn ingeschakeld, controleert u op ontbrekende kenmerken in de doelsandbox tijdens het importeren van een segment en gebruikt u standaard het bestaande samenvoegingsbeleid. Voor meer informatie over deze eigenschappen, zie de [ zandbak tooling UI gids ](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Voor meer informatie over zandbakken, lees het [ overzicht van zandbakken ](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) segmenteren naar het publiek. U kunt een publiek maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze soorten publiek worden centraal geconfigureerd en onderhouden op [!DNL Platform] en zijn gemakkelijk toegankelijk voor elke Adobe.

**Nieuwe eigenschap**

| Functie | Beschrijving |
| ------- | ----------- |
| Accountpubliek | Accountpubliek is nu over het algemeen beschikbaar! U kunt nu de segmentatie van uw account gebruiken om de volledige versnelling en verfijning van de ervaring van de segmentatie van de marketing te brengen van op mensen gebaseerd publiek naar op account gebaseerd publiek in zowel de B2B- als de B2P-edities van het Real-Time Klantplatform. Met deze release kunt u op mensen gebaseerde doelgroepen gebruiken als voorspelling voor op account gebaseerde doelgroepen, zoekmogelijkheden toevoegen, het gebruik van aangepaste entiteiten ondersteunen en zijn compatibel met gegevensbeheer. Voor meer informatie over deze eigenschap, te lezen gelieve het [ overzicht van het rekeningspubliek ](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE  Beta ] {type=Informative} [!DNL Acxiom] bron | Gebruik de [[!DNL Acxiom Prospecting Data Import]  bron ](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) om gegevens van [!DNL Acxiom] perspectiefdienst aan Experience Platform terug te winnen en in kaart te brengen. |

{style="table-layout:auto"}

Voor meer informatie over bronnen, lees het [ overzicht van bronnen ](../../sources/home.md).
