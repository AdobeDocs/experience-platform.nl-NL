---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 08ad27303b88826fd7e0fcc0a8b3d498de58c260
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 januari 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Betrouwbaarheid](#assurance)
- [Gegevensverzameling](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Betrouwbaarheid {#assurance}

Met Adobe Assurance kunt u controleren, testen, simuleren en valideren hoe u gegevens verzamelt of ervaringen opdoet in uw mobiele app.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Validatie-editor | Er zijn nieuwe verbeteringen toegevoegd aan de validatie-editor. Deze verbeteringen zijn onder andere validatiekolommen, nieuwe gereedschappen voor het samenstellen van code en verbeterde weergaven. |

{style=&quot;table-layout:auto&quot;}

Lees voor meer informatie over Verzekering de [Betrouwbaarheidsdocumentatie](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuw beginscherm | De homepage voor de UI van de Inzameling van Gegevens is bijgewerkt om nuttige onboarding informatie en verbindingen te omvatten om productiviteit te stroomlijnen. Dit omvat:<ol><li>Documentatie en aanbevolen workflows om aan de slag te gaan</li><li>Recente eigenschappen, regels en gegevenselementen</li><li>Populaire extensies</li><li>Nieuwe extensies worden bijgewerkt met een functie voor snelle installatie</li></ol> |
| Gegevens verzenden naar [!DNL Google Ads] gebruiken, gebeurtenis doorsturen | U kunt nu de opdracht [[!DNL Google Ads Enhanced Conversions] API-extensie](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor gebeurtenis door:sturen, gecombineerd met [Google Oauth 2 geheimen](../../tags/ui/event-forwarding/secrets.md#google-oauth2), om servergegevens veilig te verzenden naar [!DNL Google Ads] in real time. |

{style=&quot;table-layout:auto&quot;}

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [(bèta) Adobe Experience Cloud-verbinding Soorten publiek](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Gebruik de [!UICONTROL (Beta) Adobe Experience Cloud Audiences] verbinding om segmenten van Experience Platform aan diverse oplossingen van het Experience Platform, zoals Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Doel, of Marketo te delen. |
| [Verbinding met Pega-profiel](../../destinations/catalog/personalization/pega-profile.md) | Gebruik de [!DNL Pega Profile Connector] in Adobe Experience Platform om een live uitgaande verbinding met uw [!DNL Amazon] S3-opslag om profielgegevens periodiek naar CSV-bestanden vanuit Adobe Experience Platform naar uw eigen S3-emmers te exporteren. In [!DNL Pega Customer Decision Hub], kunt u gegevenstaken plannen om deze profielgegevens uit S3-opslag te importeren om de [!DNL Pega Customer Decision Hub] profiel. |
| [Beta) EU-verbinding voor de handelsbank CRM](../../destinations/catalog/advertising/tradedesk-emails.md) | Met de release van EUID (European Unified ID) ziet u nu twee [!DNL The Trade Desk - CRM] bestemmingen in de [doelcatalogus](/help/destinations/catalog/overview.md). <ul><li> Als u gegevens in de EU verzamelt, moet u de **[!DNL The Trade Desk - CRM (EU)]** bestemming.</li><li> Als u gegevens in de APAC- of NAMER-gebieden bront, gebruikt u de **[!DNL The Trade Desk - CRM (NAMER & APAC)]** bestemming. </li></ul> |

**Nieuwe of bijgewerkte functionaliteit**

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Nieuwe scheidingstekenopties voor bètaboudopslagdoelconnectors | Drie nieuwe scheidingsopties (dubbelpunt) `:`, Pijp, puntkomma `;`) zijn nu beschikbaar voor de nieuwe bètawolopslagbestemmingen - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Bèta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(bèta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(bèta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Meer informatie over de ondersteunde [opties voor bestandsindeling](/help/destinations/ui/batch-destinations-file-formatting-options.md) voor op bestanden gebaseerde doelen. |
| Nieuwe optionele parameter beschikbaar in [klantgegevensvelden](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) configuraties in [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Gebruik deze parameter wanneer u een gebied van klantengegevens moet creëren de waarvan waarde over alle bestemmingsdataflows opstelling door de organisatie van een gebruiker uniek moet zijn. <br> De **[!UICONTROL Integration alias]** in het [[!UICONTROL Custom Personalization]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) doel moet uniek zijn, wat betekent dat twee afzonderlijke dataflows aan deze bestemming niet de zelfde waarde voor dit gebied kunnen hebben. |

**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Oplossen of verbeteren</b></td>
        <td><b>Beschrijving</b></td>
    </tr>
    <tr>
        <td>Bijgewerkt exportgedrag naar op een bestand gebaseerde doelen (PLAT-123316)</td>
        <td>We hebben een probleem opgelost in het gedrag van <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">verplichte kenmerken</a> bij het exporteren van gegevensbestanden naar batchbestemmingen. <br> Eerder werd gecontroleerd dat elke record in de uitvoerbestanden beide bevatte: <ol><li>Een waarde die niet gelijk is aan null <code>mandatoryField</code> kolom en</li><li>Een waarde groter dan null op ten minste een van de andere niet-verplichte velden.</li></ol> De tweede voorwaarde is verwijderd. Hierdoor ziet u mogelijk meer uitvoerrijen in uw geëxporteerde gegevensbestanden, zoals in het onderstaande voorbeeld wordt getoond:<br> <b> Voorbeeldgedrag vóór release januari 2023 </b> <br> Verplicht veld: <code>emailAddress</code> <br> <b>Te activeren invoergegevens</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Uitvoer van activering</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Voorbeeldgedrag na release januari 2023 </b> <br> <b>Uitvoer van activering</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
</table>

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Voorgestelde waarden voor tekenreeksvelden uitschakelen | U kunt nu [afzonderlijke voorgestelde waarden voor tekenreeksvelden uitschakelen](../../xdm/ui/fields/enum.md) in de [!UICONTROL Schemas] werkruimte, inclusief die van standaardcomponenten. Deze functie is alleen beschikbaar voor velden met voorgestelde waarden en wordt niet ondersteund voor opsommingsbeperkingen. |

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL Conversion]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Een klasse voor het bijhouden van conversiegegevens, zoals valutaomrekeningen. |
| Veldgroep | [[!UICONTROL Currency Conversion Rate Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Een veldgroep voor de [!UICONTROL Conversion] klasse, aanvullende gegevens over valutaomrekening vastleggen. |
| Veldgroep | [[!UICONTROL Consent policies evaluation results map with metadata]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Hiermee legt u details vast voor het evaluatieresultaat van het beleid voor meerdere toestemmingen, waaronder metagegevens over toetreders tot het toestemmingsbeleid en deze bestaan. |

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | De `ID` veld is hernoemd naar `name`en de voorgaande `name` veld is nu `friendlyName`. |
| Gegevenstype | [[!UICONTROL Decision Proposition Details]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Toegevoegde `selectionStrategy` veld waarin de details van een selectiestrategie worden weergegeven. |
| Veldgroep | [[!UICONTROL Experience Event - Proposition Interactions]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | De veldgroep is nu compatibel met de [!UICONTROL Journey Step Event] klasse. |
| Gegevenstype | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | De `ID` veld is hernoemd naar `name`. |
| Gegevenstype | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Een wijziging in het patroon in de eigenschap voor het videosegment is omgekeerd. |
| Gegevenstype | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | De `droppedFrameCount` veld. |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | De naam van de `isAuthorized` veld naar `authorized`en de `type` naar een tekenreeks toen deze eerder een Booleaanse waarde had. |
| Gegevenstype | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Verschillende nieuwe velden toegevoegd: `shipDate`, `trackingNumber`, en `trackingURL`. |
| Veldgroep | [[!UICONTROL AJO Entity Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Verschillende nieuwe velden toegevoegd: `journeyNodeID`, `journeyNodeName`, en `journeyModeType`. |
| Veldgroep | [[!UICONTROL Consumer Experience Event]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | De veldgroep is nu ook compatibel met de [!UICONTROL Summary Metrics] klasse. |
| Veldgroep | [[!UICONTROL Product Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | De `productTriggers` veld is nu genest onder een `weather` object. |
| Veldgroep | [[!UICONTROL Relative Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | De `relativeTriggers` veld is nu genest onder een `weather` object. |
| Veldgroep | [[!UICONTROL Severe Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | De `severeTriggers` veld is nu genest onder een `weather` object. |
| Veldgroep | [[!UICONTROL Weather Triggers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | De `weatherTriggers` veld is nu genest onder een `weather` object. |
| Veldgroep | [[!UICONTROL XDM Related Business Accounts]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | De veldgroep is nu stabiel. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Binnenkomende veroudering** {#deprecation}

Om overtolligheid in de levenscyclus van het segmentlidmaatschap te verwijderen, `Existing` status wordt vervangen door [segmentlidmaatschapskaart](../../xdm/field-groups/profile/segmentation.md) eind maart 2023. Een vervolgaankondiging zal de exacte vervaldatum bevatten.

Post deprecrection, profielen die in een segment worden gekwalificeerd zullen worden vertegenwoordigd zoals `Realized` en de gediskwalificeerde profielen blijven worden weergegeven als `Exited`. Dit zal pariteit met op dossier-gebaseerde bestemmingen met brengen `Active` en `Expired` segmentstatussen.

Deze wijziging kan van invloed zijn op het gebruik van [ondernemingsbestemmingen](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) en hebben geautomatiseerde downstream processen geïmplementeerd, gebaseerd op de `Existing` status. Gelieve te herzien uw downstreamintegratie als dit voor u het geval is. Als u pas na een bepaalde tijd gekwalificeerde profielen wilt identificeren, kunt u een combinatie van de `Realized` en de `lastQualificationTime` in uw overzicht van het segmentlidmaatschap. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger.

Als u meer wilt weten over het realtime profiel van de klant, inclusief zelfstudies en aanbevolen procedures voor het werken met profielgegevens, leest u eerst de [Overzicht van het realtime klantprofiel](../../profile/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Door Platform gegenereerde vervaldatum van segmentlidmaatschap | Om het even welk segmentlidmaatschap dat in is `Exited` staat gedurende meer dan 30 dagen op basis van de `lastQualificationTime` wordt geschrapt. |
| Vervaldatum extern publiekslidmaatschap | Standaard blijven leden van externe doelgroepen 30 dagen behouden. Als u deze nog langer wilt behouden, gebruikt u de `validUntil` veld tijdens de opname van publieksgegevens. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Toegang van gebruikers tot submappen van bronnen voor cloudopslag toestaan | U kunt nu toegang definiëren tot een specifieke submap van de bron voor cloudopslag wanneer u een nieuw account maakt. Zodra gecreeerd, zullen de gebruikers tot gegevens van toegelaten subfolder kunnen slechts toegang hebben. Deze functie is beschikbaar voor de volgende bronnen voor cloudopslag: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), en [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Beta beschikbaarheid van [!DNL SugarCRM] | [!DNL SugarCRM] bronnen zijn nu beschikbaar in bèta . Gebruik de [!DNL SugarCRM Accounts & Contacts] en de [!DNL SugarCRM Events] bronnen om gegevens van uw [!DNL SugarCRM] aan Experience Platform. Lees voor meer informatie de [[!DNL SugarCRM] overzicht](../../sources/connectors/crm/sugarcrm.md). |