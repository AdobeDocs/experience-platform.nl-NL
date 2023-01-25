---
title: Opmerkingen bij de release van Adobe Experience Platform Januari 2023
description: In de releaseopmerkingen van januari 2023 voor Adobe Experience Platform.
source-git-commit: 0f2ddad37db87d8818281067e3a30cc1b2fb6418
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 januari 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Betrouwbaarheid](#assurance)
- [Gegevensverzameling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Klantprofiel in realtime](#profile)
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

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Door Platform gegenereerde vervaldatum van segmentlidmaatschap | Om het even welk segmentlidmaatschap dat in is `Exited` staat gedurende meer dan 30 dagen op basis van de `lastQualificationTime` wordt geschrapt. |
| Vervaldatum extern publiekslidmaatschap | Standaard blijven leden van externe doelgroepen 30 dagen behouden. Als u deze nog langer wilt behouden, gebruikt u de `validUntil` veld tijdens de opname van publieksgegevens. |

{style=&quot;table-layout:auto&quot;}

**Binnenkomende veroudering** {#deprecation}

Om overtolligheid in de levenscyclus van het segmentlidmaatschap te verwijderen, `Existing` status wordt vervangen door [segmentlidmaatschapskaart](../../xdm/field-groups/profile/segmentation.md) eind maart 2023. Een vervolgaankondiging zal de exacte vervaldatum bevatten.

Post deprecrection, profielen die in een segment worden gekwalificeerd zullen worden vertegenwoordigd zoals `Realized` en de gediskwalificeerde profielen blijven worden weergegeven als `Exited`. Dit zal pariteit met op dossier-gebaseerde bestemmingen met brengen `Active` en `Expired` segmentstatussen.

Deze wijziging kan van invloed zijn op het gebruik van [ondernemingsbestemmingen](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) en hebben geautomatiseerde downstream processen geïmplementeerd, gebaseerd op de `Existing` status. Gelieve te herzien uw downstreamintegratie als dit voor u het geval is. Als u pas na een bepaalde tijd gekwalificeerde profielen wilt identificeren, kunt u een combinatie van de `Realized` en de `lastQualificationTime` in uw overzicht van het segmentlidmaatschap. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger.

Als u meer wilt weten over het realtime profiel van de klant, inclusief zelfstudies en aanbevolen procedures voor het werken met profielgegevens, leest u eerst de [Overzicht van het realtime klantprofiel](../../profile/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Toegang van gebruikers tot submappen van bronnen voor cloudopslag toestaan | U kunt nu toegang definiëren tot een specifieke submap van de bron voor cloudopslag wanneer u een nieuw account maakt. Zodra gecreeerd, zullen de gebruikers tot gegevens van toegelaten subfolder kunnen slechts toegang hebben. Deze functie is beschikbaar voor de volgende bronnen voor cloudopslag: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), en [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Beta beschikbaarheid van [!DNL SugarCRM] | [!DNL SugarCRM] bronnen zijn nu beschikbaar in bèta . Gebruik de [!DNL SugarCRM Accounts & Contacts] en de [!DNL SugarCRM Events] bronnen om gegevens van uw [!DNL SugarCRM] aan Experience Platform. Lees voor meer informatie de [[!DNL SugarCRM] overzicht](../../sources/connectors/crm/sugarcrm.md). |
