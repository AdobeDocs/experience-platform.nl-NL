---
title: Opmerkingen bij de release van Adobe Experience Platform, februari 2023
description: In de release van februari 2023 staat Adobe Experience Platform vermeld.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 5bf54374773fd95ae1c40dd00b5dbe633031b70e
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 22 februari 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query-service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Bronnen](#sources)

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

### Betrouwbaarheid {#assurance}

Met Adobe Assurance kunt u controleren, testen, simuleren en valideren hoe u gegevens verzamelt of ervaringen opdoet in uw mobiele app.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Openbare API&#39;s | De Adobe Assurance API&#39;s zijn nu beschikbaar. De API&#39;s voor Betrouwbaarheid zijn een verzameling API&#39;s die gebruikers de mogelijkheid bieden om hun eigen web- en mobiele toepassingen te testen en er fouten in op te sporen, wanneer deze zijn uitgerust met de Adobe Assurance-extensie met Mobile SDK. Om meer over de Verzekering APIs te leren, te lezen gelieve het [ overzicht van de Verzekering API ](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Voor meer informatie over Verzekering, te lezen gelieve de [ documentatie van de Verzekering ](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte eigenschappen** {#destinations-new-updated-features}

| Functie | Beschrijving |
| ----------- | ----------- |
| [ Verbetering van het Beleid van de Toestemming ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) voor integratie met [ op dossier-gebaseerde (partij) bestemmingen ](/help/destinations/destination-types.md#file-based) | <p> Wanneer de profielen niet meer voor een toestemmingsbeleid gekwalificeerd zijn, deelt Experience Platform nu proactief hun beleidsuitgang aan op dossier-gebaseerde bestemmingen mee. Dit volgt de [ versie in Februari 2023 ](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) van de zelfde functionaliteit voor het stromen bestemmingen. </p> <p> <b> Nota </b>: Deze functionaliteit is beschikbaar slechts aan klanten van **[!UICONTROL Privacy and Security Shield]**, en die van **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie** {#destinations-new-updated-documentation}

| Documentatie | Beschrijving |
| ----------- | ----------- |
| Hoe werken de bestemmingen documentatie | <p>We hebben drie nieuwe artikelen gepubliceerd waarin wordt uitgelegd hoe bestemmingen werken, op basis van gemeenschappelijke vragen van gebruikers:</p> <p><ul><li>[ configureerbare en gemeenschappelijke uitvoermontages in bestemmingen ](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[ de uitvoergedrag van het Profiel voor verschillende bestemmingstypes ](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[ Identiteitsafhandeling in het werkschema van de bestemmingsactivering ](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Veldveroudering via de gebruikersinterface | U kunt [ gebieden van uw schema&#39;s nu verwerpen nadat het gegeven ](../../xdm/tutorials/field-deprecation-ui.md) is opgenomen. Met XDM-veldafleiding kunt u velden verwijderen uit de UI-weergave en deze voor gebruik behouden. Indien nodig kunt u afgekeurde velden opnieuw weergeven en worden alle segmenten, query&#39;s of downstreamoplossingen die verwijzen naar de velden, op de gebruikelijke wijze uitgevoerd. |

{style="table-layout:auto"}

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1669/files) | De klasse van het Profiel van het Individuele Vooruitzicht XDM brengt in partner-Geleverde IDs. |

{style="table-layout:auto"}

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [!UICONTROL Frequency Capping Constraints] | De [!UICONTROL Frequency Capping Constraints] gebiedsgroep is [ bijgewerkt om herhalings en douanegebeurtenissen ](https://github.com/adobe/xdm/pull/1641/files) te steunen. |
| Gegevenstype | [!UICONTROL Web referrer] | De verwijzingseigenschappen van het Web zijn [ bijgewerkt om `xdm:linkName` en `xdm:linkRegion` ](https://github.com/adobe/xdm/pull/1666/files) te omvatten. Dit zijn respectievelijk de naam en het gebied van het HTML-element dat op de vorige pagina is geselecteerd. |
| Veldgroep | [!UICONTROL Adobe CJM ExperienceEvent - Message interaction details] | [ het [!UICONTROL Tracker URL] gebied werd toegevoegd ](https://github.com/adobe/xdm/pull/1665/files) aan [!UICONTROL Adobe CJM ExperienceEvent]. Deze tracker bevat de URL die door de gebruiker is geselecteerd. |
| Veldgroep | [!UICONTROL Adobe CJM ExperienceEvent - Message interaction detail] | [ het lege `meta:enum` bezit werd verwijderd ](https://github.com/adobe/xdm/pull/1668/files) van het URL [!UICONTROL Tracking Type] gebied. |
| Gegevenstype | [!UICONTROL Media information] | [ het regex patroon van het `videoSegment` bezit in [!UICONTROL Media information] datatype werd verwijderd ](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, lees het [ XDM overzicht van het Systeem ](../../xdm/home.md). &#x200B;

## Query-service {#query-service}

Met Query Service kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake] . U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Wetenschap van Gegevens Workspace, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Gegevenssets inschakelen voor profiel met SQL | [ ETIKETTERSs van het Gebruik in CTAS vragen om een dataset &quot;toegelaten profiel&quot;te maken ](../../query-service/sql/syntax.md#create-table-as-select), of gebruik ALTER om bestaande datasets bij te werken om voor profiel worden toegelaten. U kunt dit uitgebreide SQL concept gebruiken om naadloze steun voor afgeleide datasets voor uw zaken van het bedrijfsgebruik van het Profiel van de Klant in real time te verlenen. Zie de [ naadloze SQL stroom voor afgeleid datasetdocument ](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md) voor meer details. |
| Geplande query&#39;s controleren | Gebruik het [ Geplande lusje van Vragen ](../../query-service/ui/monitor-queries.md) om belangrijke informatie over uw vraaglooppas te vinden en aan alarm in te tekenen. De vragen van de monitor voor planningsdetails, status, en foutenmeldingen/codes zouden moeten ontbreken. |
| Functie voor automatisch aanvullen in-/uitschakelen | Elimineer bepaalde meta-gegevensbevelen en verbeter verwerkingstijden door [ van een knevel te voorzien van de Redacteur van de Vraag auto-volledige eigenschap ](../../query-service/ui/user-guide.md#auto-complete). Deze functie stelt automatisch potentiële SQL sleutelwoorden en lijstdetails voor de vraag voor aangezien u het schrijft. |
| Gegevenssetvoorbeelden | Specificeer een steekproeftarief in uw vraag en [ de steekproeven van de gebruiksdataset om een eenvormige willekeurige steekproef ](../../query-service/key-concepts/dataset-samples.md) tot stand te brengen, of voorwaardelijke steekproeven tot stand te brengen die op specifieke criteria worden gebaseerd. |

{style="table-layout:auto"}

Voor meer informatie over de Diensten van de Vraag, verwijs naar het [ overzicht van de Dienst van de Vraag ](../../query-service/home.md).


## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B Edition is gebaseerd op Real-time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Gerelateerde accountservice inschakelen | Met de nieuwe schakelfunctie kunt u de verwante accountservice op uw account inschakelen. Voor meer informatie, lees de gids op [ toelatend de verwante rekeningendienst ](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Meer over de Uitgave van Real-Time CDP B2B leren, lees het [ overzicht van de Uitgave van Real-Time CDP B2B ](../../rtcdp/overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en stelt u in staat die gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Toegang op abonnementsniveau toewijzen met [!DNL Google PubSub] | U kunt toegang tot een specifiek onderwerpabonnement nu bepalen wanneer het gebruiken van de [!DNL Google PubSub] bron door abonnements identiteitskaart te verstrekken wanneer het voor authentiek verklaren. Voor meer informatie, lees het [!DNL Google PubSub] authentificatieleerprogramma [ gebruikend de Dienst API van de Stroom ](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) of [ Platform UI ](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Aangepaste activiteitsgegevens verzamelen vanuit [!DNL Marketo] | U kunt nu aangepaste activiteitsgegevens van uw [!DNL Marketo] -instantie overbrengen naar het Experience Platform. Om de gegevens van de douaneactiviteit in te voeren, moet u de groepen van het gebied van douaneactiviteiten in het B2B schema van Activiteiten opzetten en een dataflow creëren gebruikend de activiteitendataset. Zodra de gegevensstroom volledig is, zal de ingebedde dataset zowel standaard als douaneactiviteiten van uw [!DNL Marketo] instantie bevatten. U kunt [ Dienst van de Vraag ](../../query-service/home.md) dan gebruiken om tot uw verslagen van de douaneactiviteit op Platform toegang te hebben. Voor meer informatie, lees de gids op [ creërend een dataflow voor de gegevens van de douaneactiviteit ](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Niet-geclaimde accounts uitsluiten van [!DNL Marketo] | U kunt nu configureren of u niet-geclaimde accounts wilt uitsluiten of opnemen in de opname wanneer u een gegevensstroom voor bedrijfsgegevens maakt. Voor meer informatie, lees de gids bij [ het creëren van een bronverbinding en een dataflow voor  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Meer over bronnen leren, lees het [ overzicht van bronnen ](../../sources/home.md).
