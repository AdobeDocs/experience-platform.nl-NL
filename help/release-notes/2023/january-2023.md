---
title: Opmerkingen bij de release van Adobe Experience Platform Januari 2023
description: Aanvullende informatie van januari 2023 voor Adobe Experience Platform.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: d23f1cc9dd0155aceae78bf938d35463e9c38181
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 25 januari 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Betrouwbaarheid](#assurance)
- [Gegevensverzameling](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Kunstmatige inlichtingendiensten/leerdiensten voor machines {#ai-ml}

Artificial Intelligence and Machine Learning services stellen marketinganalisten en artsen in staat om de kracht van AI/ML te benutten in gevallen waarin de klant gebruikmaakt van ervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten, zonder de behoefte aan de deskundigheid van de gegevenswetenschap, specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties.

### Attribution AI

Attribution AI wordt gebruikt om credits toe te wijzen aan aanraakpunten die tot conversiegebeurtenissen leiden. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Gereedheid van HIPAA | Klanten met een gezondheidszorgschild kunnen nu beschermde gezondheidsinformatie ontvangen, gebruiken, onderhouden of doorgeven in Attribution AI en bepaalde andere op Experience Platform gebaseerde toepassingen. Gezondheidsschild is voor klanten in de gezondheidszorg die ofwel een onder de HIPAA vallende entiteit zijn, ofwel een zakelijke vennoot. Voor meer informatie, lees de documentatie over [ HIPAA en de Producten en de Diensten van de Adobe ](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Kolommen met aanvullende scoregegevens bewerken | U kunt extra kolommen van de scoredataset (het melden van kolommen) nu toevoegen of verwijderen wanneer u bestaande modellen uitgeeft. Hierdoor wordt de flexibiliteit van de toewijzingsscores uitgebreid om u inzichten aan extra dimensies te verstrekken nadat een model reeds is gecreeerd. Zie de [ gids UI van de Attributie ](../../intelligent-services/attribution-ai/user-guide.md) om meer te leren. |

{style="table-layout:auto"}

Gelieve te zien het [ AI/ML de diensten ](../../intelligent-services/attribution-ai/overview.md) overzicht voor meer informatie.

### Customer AI

De AI van de Klant voor Real-time Customer Data Platform, wordt gebruikt om douanescore zoals kurn en omzetting voor individuele profielen op schaal te produceren. Dit wordt bereikt zonder de bedrijfsbehoeften te hoeven omzetten in een machine learning-probleem, een algoritme te kiezen, te trainen of te implementeren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Gereedheid van HIPAA | Klanten met een gezondheidszorgschild kunnen nu beschermde gezondheidsinformatie ontvangen, gebruiken, onderhouden of doorgeven in Customer AI voor Real-time Customer Data Platform en bepaalde andere toepassingen op basis van Experience Platforms. Gezondheidsschild is voor klanten in de gezondheidszorg die ofwel een onder de HIPAA vallende entiteit zijn, ofwel een zakelijke vennoot. Voor meer informatie, zie de documentatie over [ HIPAA en de Producten en de Diensten van de Adobe ](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Gelieve te zien het [ AI/ML de diensten ](../../intelligent-services/customer-ai/overview.md) overzicht voor meer informatie.

## Betrouwbaarheid {#assurance}

Met Adobe Assurance kunt u controleren, testen, simuleren en valideren hoe u gegevens verzamelt of ervaringen opdoet in uw mobiele app.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Validatie-editor | Er zijn nieuwe verbeteringen toegevoegd aan de validatie-editor. Deze verbeteringen zijn onder andere validatiekolommen, nieuwe gereedschappen voor het samenstellen van code en verbeterde weergaven. |

{style="table-layout:auto"}

Voor meer informatie over Verzekering, te lezen gelieve de [ documentatie van de Verzekering ](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuw beginscherm | De homepage voor de UI van de Inzameling van Gegevens is bijgewerkt om nuttige onboarding informatie en verbindingen te omvatten om productiviteit te stroomlijnen. Dit omvat:<ol><li>Documentatie en aanbevolen workflows om aan de slag te gaan</li><li>Recente eigenschappen, regels en gegevenselementen</li><li>Populaire extensies</li><li>Nieuwe extensies worden bijgewerkt met een functie voor snelle installatie</li></ol> |
| Gegevens naar [!DNL Google Ads] verzenden met behulp van gebeurtenissen doorsturen | U kunt de [[!DNL Google Ads Enhanced Conversions]  API uitbreiding ](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor gebeurtenis nu gebruiken door:sturen, gecombineerd met [ Google Oauth 2 geheimen ](../../tags/ui/event-forwarding/secrets.md#google-oauth2), om server-zijgegevens aan [!DNL Google Ads] in real time veilig te verzenden. |

{style="table-layout:auto"}

## Doelen (bijgewerkt op 2 februari) {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen**

| Doel | Beschrijving |
| ----------- | ----------- |
| [ (Beta) Adobe Experience Cloud Poortverbinding ](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Gebruik de [!UICONTROL (Beta) Adobe Experience Cloud Audiences] verbinding om segmenten van Experience Platform aan diverse oplossingen van het Experience Platform, zoals Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Doel, of Marketo te delen. |
| [ verbinding van het Profiel van Pega ](../../destinations/catalog/personalization/pega-profile.md) | Gebruik [!DNL Pega Profile Connector] in Adobe Experience Platform om een live uitgaande verbinding met uw [!DNL Amazon] S3-opslag te maken en profielgegevens periodiek naar CSV-bestanden vanuit Adobe Experience Platform naar uw eigen S3-emmers te exporteren. In [!DNL Pega Customer Decision Hub] kunt u gegevenstaken plannen om deze profielgegevens te importeren uit S3-opslag om het [!DNL Pega Customer Decision Hub] -profiel bij te werken. |
| [ (Beta) The Trade Desk CRM EU connection ](../../destinations/catalog/advertising/tradedesk-emails.md) | Met de versie van EUID (Europese Verenigde identiteitskaart), ziet u nu twee [!DNL The Trade Desk - CRM] bestemmingen in de [ bestemmingscatalogus ](/help/destinations/catalog/overview.md). <ul><li> Gebruik de **[!DNL The Trade Desk - CRM (EU)]** -bestemming als u gegevens in de EU levert.</li><li> Gebruik het doel **[!DNL The Trade Desk - CRM (NAMER & APAC)]** als u gegevens in de APAC- of NAMER-gebieden bront. </li></ul> |

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Verbetering van het beleid voor betaalde mediaconcept voor integratie met streaming doelen | Een [ verhoging om beleidshandhaving ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) op [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations) voor betaalde media activering gebruik-gevallen goed te keuren. Wanneer profielen niet meer voor een toestemmingsbeleid in aanmerking komen, deelt Experience Platform nu proactief hun beleidsuitgang aan het stromen bestemmingen mee. <br> <b> Nota </b>: Deze functionaliteit is beschikbaar slechts aan klanten van **[!UICONTROL Privacy and Security Shield]**, en die van **[!UICONTROL Healthcare Shield]**. |
| Nieuwe scheidingstekenopties voor bètaboudopslagdoelconnectors | Drie nieuwe scheidingsopties (Colon `:`, Pipe, Semicolon `;`) zijn nu beschikbaar voor de nieuwe bètawolopslagbestemmingen - [ (Beta) Amazon S3 ](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ (Beta) Azure Blob ](/help/destinations/catalog/cloud-storage/azure-blob.md), [ (Beta) Azure Data Lake Storage Gen2 ](/help/destinations/catalog/cloud-storage/adls-gen2.md), [ (Beta) Data Landing Zone ](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [ (Beta Google) Cloudopslag ](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [ (Beta) SFTP ](/help/destinations/catalog/cloud-storage/sftp.md). <br> las over de gesteunde [ dossier het formatteren opties ](/help/destinations/ui/batch-destinations-file-formatting-options.md) voor op dossier-gebaseerde bestemmingen. |
| Nieuwe facultatieve parameter beschikbaar in [ gebieden van klantengegevens ](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) configuraties in [ Destination SDK ](/help/destinations/destination-sdk/overview.md) | `unique`: Gebruik deze parameter wanneer u een gegevensveld voor klanten moet maken waarvan de waarde uniek moet zijn voor alle doelgegevensstromen die door de organisatie van een gebruiker zijn ingesteld. <br> Het **[!UICONTROL Integration alias]** -veld in het [[!UICONTROL Custom Personalization]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) -doel moet bijvoorbeeld uniek zijn, wat betekent dat twee afzonderlijke gegevensstromen naar dit doel niet dezelfde waarde voor dit veld kunnen hebben. |

**Correcties en verhogingen** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Oplossen of verbeteren</b></td>
        <td><b>Beschrijving</b></td>
    </tr>
    <tr>
        <td>Bijgewerkt exportgedrag naar op een bestand gebaseerde doelen (PLAT-123316)</td>
        <td>Wij bevestigden een kwestie in het gedrag van <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes"> verplichte attributen </a> wanneer het uitvoeren van gegevensdossiers aan partijbestemmingen. <br> Eerder werd gecontroleerd of elke record in de uitvoerbestanden beide bevatte: <ol><li>Een waarde die niet gelijk is aan null van de kolom <code>mandatoryField</code> en</li><li>Een waarde groter dan null op ten minste een van de andere niet-verplichte velden.</li></ol> De tweede voorwaarde is verwijderd. Dientengevolge, zou u meer outputrijen in uw uitgevoerde gegevensdossiers kunnen zien, zoals aangetoond in het voorbeeld hieronder:<br> <b> gedrag van de steekproef vóór de versie van Januari 2023 </b> <br> Verplicht gebied: <code>emailAddress</code> <br> <b> de gegevens van de Input om </b> <br> te activeren<table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b> output van de Activering </b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Het gedrag van de steekproef na de versie van Januari 2023 </b> <br> <b> output van de Activering </b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>UI- en API-validatie voor vereiste toewijzingen en dubbele toewijzingen (PLAT-123316)</td>
        <td>De bevestiging wordt nu afgedwongen als volgt in UI en API wanneer <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping"> kaartingsgebieden </a> in het activerende bestemmingswerkschema:<ul><li><b> Vereiste afbeeldingen </b>: Als de bestemming opstelling door de bestemmingsontwikkelaar met vereiste afbeeldingen (bijvoorbeeld, <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html"> Google Ad Manager 360 </a> bestemming) is geweest, dan moeten deze vereiste afbeeldingen door de gebruiker worden toegevoegd wanneer het activeren van gegevens aan de bestemming. </li><li><b> Dubbele afbeeldingen </b>: In de afbeeldingsstap van het activeringswerkschema, kunt u dubbele waarden op de brongebieden, maar niet op de doelgebieden toevoegen. Zie de onderstaande tabel voor een voorbeeld van toegestane en verboden combinaties van toewijzingen. <br><table><thead><tr><th>Toegestaan/verboden</th><th>Source-veld</th><th>Doelveld</th></tr></thead><tbody><tr><td>Toegestaan</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>email   alias2</li></ul></td></tr><tr><td>Verboden</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in weergavenamen van boomstructuur | Eerder werden veldnamen weergegeven in de gebruikersinterface, maar nu zijn de weergavenamen voor schemavelden op het schemacanvas mensvriendelijker voor lezen. |

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL Conversion]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Een klasse voor het bijhouden van conversiegegevens, zoals valutaomrekeningen. |
| Veldgroep | [[!UICONTROL Currency Conversion Rate Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Een veldgroep voor de [!UICONTROL Conversion] -klasse, waarin aanvullende details zijn opgenomen die betrekking hebben op valutaconversie. |
| Veldgroep | [[!UICONTROL Consent policies evaluation results map with metadata]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.json) | Hiermee legt u details vast voor het evaluatieresultaat van het beleid voor meerdere toestemmingen, waaronder metagegevens over toetreders tot het toestemmingsbeleid en deze bestaan. |

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | De naam van het veld `ID` is gewijzigd in `name` en het vorige veld `name` is nu `friendlyName` . |
| Gegevenstype | [[!UICONTROL Decision Proposition Details]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Er is een veld `selectionStrategy` toegevoegd waarin de details van een selectiestrategie worden vastgelegd. |
| Veldgroep | [[!UICONTROL Experience Event - Proposition Interactions]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | De veldgroep is nu compatibel met de klasse [!UICONTROL Journey Step Event] . |
| Gegevenstype | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | De naam van het veld `ID` is gewijzigd in `name` . |
| Gegevenstype | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/media.schema.json) | Een wijziging in het patroon in de eigenschap voor het videosegment is omgekeerd. |
| Gegevenstype | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Het veld `droppedFrameCount` is verwijderd. |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | De naam van het veld `isAuthorized` is gewijzigd in `authorized` en de naam `type` is bijgewerkt naar een tekenreeks die eerder een Booleaanse waarde had. |
| Gegevenstype | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Er zijn verschillende nieuwe velden toegevoegd: `shipDate` , `trackingNumber` en `trackingURL` . |
| Veldgroep | [[!UICONTROL AJO Entity Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Er zijn verschillende nieuwe velden toegevoegd: `journeyNodeID` , `journeyNodeName` en `journeyModeType` . |
| Veldgroep | [[!UICONTROL Consumer Experience Event]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | De veldgroep is nu ook compatibel met de klasse [!UICONTROL Summary Metrics] . |
| Veldgroep | [[!UICONTROL Product Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Het veld `productTriggers` is nu genest onder een object `weather` . |
| Veldgroep | [[!UICONTROL Relative Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Het veld `relativeTriggers` is nu genest onder een object `weather` . |
| Veldgroep | [[!UICONTROL Severe Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Het veld `severeTriggers` is nu genest onder een object `weather` . |
| Veldgroep | [[!UICONTROL Weather Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Het veld `weatherTriggers` is nu genest onder een object `weather` . |
| Veldgroep | [[!UICONTROL XDM Related Business Accounts]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | De veldgroep is nu stabiel. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Komende veroudering** {#deprecation}

Om overtolligheid in de levenscyclus van het segmentlidmaatschap te verwijderen, zal de `Existing` status van de [ kaart van het segmentlidmaatschap ](../../xdm/field-groups/profile/segmentation.md) aan het eind van Maart 2023 worden afgekeurd. Een vervolgaankondiging zal de exacte vervaldatum bevatten.

Post-afgekeurde profielen, profielen die in een segment zijn gekwalificeerd, worden weergegeven als `Realized` en profielen die zijn gediskwalificeerd, worden wel weergegeven als `Exited` . Dit zorgt voor pariteit met op bestanden gebaseerde doelen met `Active` - en `Expired` -segmentstatussen.

Deze verandering zou u kunnen beïnvloeden als u [ ondernemingsbestemmingen ](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) gebruikt en stroomafwaartse processen op zijn plaats, gebaseerd op de `Existing` status geautomatiseerd hebt. Gelieve te herzien uw downstreamintegratie als dit voor u het geval is. Als u pas gekwalificeerde profielen wilt identificeren na een bepaalde tijd, kunt u overwegen een combinatie van de status `Realized` en de status `lastQualificationTime` in uw overzicht van segmentlidmaatschap te gebruiken. Neem voor meer informatie contact op met uw Adobe.

Meer over het Profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met profielgegevens leren, gelieve te beginnen door het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md) te lezen.

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Bulkwaarde importeren in Segment Builder | De Bouwer van het segment steunt nu het invoeren veelvoudige waarden, of door een CSV of TSV dossier te uploaden of door komma&#39;s gescheiden waarden manueel op te nemen. Meer informatie kan binnen de [ gids van de Bouwer van het Segment ](../../segmentation/ui/segment-builder.md#rule-builder-canvas) worden gevonden. |
| Vervaldatum extern publiekslidmaatschap | Standaard blijven leden van externe doelgroepen 30 dagen behouden. Gebruik het veld `validUntil` tijdens het invoeren van publieksgegevens om deze gegevens langer te behouden. |
| Door het platform gegenereerde vervaldatum van segmentlidmaatschap | Elk segmentlidmaatschap dat langer dan 30 dagen in de status `Exited` staat, op basis van het veld `lastQualificationTime` , wordt verwijderd. |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en stelt u in staat die gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Toegang van gebruikers tot submappen van bronnen voor cloudopslag toestaan | U kunt nu toegang definiëren tot een specifieke submap van de bron voor cloudopslag wanneer u een nieuw account maakt. Zodra gecreeerd, zullen de gebruikers tot gegevens van toegelaten subfolder kunnen slechts toegang hebben. Deze eigenschap is beschikbaar aan de volgende bronnen van de wolkenopslag: [ Azure BlobOpslag ](../../sources/connectors/cloud-storage/blob.md), [ de Opslag van de Wolk van Google ](../../sources/connectors/cloud-storage/google-cloud-storage.md), [ Google PubSub ](../../sources/connectors/cloud-storage/google-pubsub.md), en [ SFTP ](../../sources/connectors/cloud-storage/sftp.md). |
| Beta-beschikbaarheid van [!DNL SugarCRM] | [!DNL SugarCRM] -bronnen zijn nu beschikbaar in bèta. Gebruik de bronnen [!DNL SugarCRM Accounts & Contacts] en [!DNL SugarCRM Events] om gegevens van uw [!DNL SugarCRM] -account naar het Experience Platform te verzenden. Voor meer informatie, lees het [[!DNL SugarCRM]  overzicht ](../../sources/connectors/crm/sugarcrm.md). |
