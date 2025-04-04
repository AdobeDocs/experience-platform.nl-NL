---
title: Aanvullende informatie voor Adobe Experience Platform van februari 2023
description: Aanvullende informatie voor Adobe Experience Platform van februari 2023.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 29%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 22 februari 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Dataverzameling](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Query-service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Bronnen](#sources)

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

### Assurance {#assurance}

Met Adobe Assurance kunt u controleren, testen, simuleren en valideren hoe u gegevens verzamelt of ervaringen opdoet in uw mobiele app.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Openbare API&#39;s | De Adobe Assurance API&#39;s zijn nu beschikbaar. De Assurance API&#39;s zijn een verzameling API&#39;s die gebruikers de mogelijkheid bieden om hun eigen web- en mobiele apps te testen en er fouten in op te sporen, wanneer deze zijn uitgerust met de Adobe Assurance-extensie met Mobile SDK. Om meer over Assurance APIs te leren, te lezen gelieve het [ overzicht van Assurance API ](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Voor meer informatie over Assurance, te lezen gelieve de [ documentatie van Assurance ](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte eigenschappen** {#destinations-new-updated-features}

| Functie | Beschrijving |
| ----------- | ----------- |
| [ Verbetering van het Beleid van de Toestemming ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) voor integratie met [ op dossier-gebaseerde (partij) bestemmingen ](/help/destinations/destination-types.md#file-based) | <p> Wanneer profielen niet meer in aanmerking komen voor een beleid voor toestemming, geeft Experience Platform nu proactief aan dat het beleid is afgesloten naar bestandsbestemmingen. Dit volgt de [ versie in Februari 2023 ](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) van de zelfde functionaliteit voor het stromen bestemmingen. </p> <p> <b> Nota </b>: Deze functionaliteit is beschikbaar slechts aan klanten van **[!UICONTROL Privacy and Security Shield]**, en die van **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie** {#destinations-new-updated-documentation}

| Documentatie | Beschrijving |
| ----------- | ----------- |
| Hoe werken de bestemmingen documentatie | <p>We hebben drie nieuwe artikelen gepubliceerd waarin wordt uitgelegd hoe bestemmingen werken, op basis van gemeenschappelijke vragen van gebruikers:</p> <p><ul><li>[ configureerbare en gemeenschappelijke uitvoermontages in bestemmingen ](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[ de uitvoergedrag van het Profiel voor verschillende bestemmingstypes ](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[ Identiteitsafhandeling in het werkschema van de bestemmingsactivering ](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte functies**

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

Voor meer informatie over XDM in Experience Platform, lees het [ XDM overzicht van het Systeem ](../../xdm/home.md). &#x200B;

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake]. U kunt alle datasets uit Data Lake samenvoegen en de queryresultaten vastleggen als een nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gegevenssets inschakelen voor profiel met SQL | [ ETIKETTERSs van het Gebruik in CTAS vragen om een dataset &quot;toegelaten profiel&quot;te maken ](../../query-service/sql/syntax.md#create-table-as-select), of gebruik ALTER om bestaande datasets bij te werken om voor profiel worden toegelaten. U kunt dit uitgebreide SQL concept gebruiken om naadloze steun voor afgeleide datasets voor uw zaken van het bedrijfsgebruik van het Profiel van de Klant in real time te verlenen. Zie de [ naadloze SQL stroom voor afgeleid datasetdocument ](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md) voor meer details. |
| Geplande query&#39;s controleren | Gebruik het [ Geplande lusje van Vragen ](../../query-service/ui/monitor-queries.md) om belangrijke informatie over uw vraaglooppas te vinden en aan alarm in te tekenen. De vragen van de monitor voor planningsdetails, status, en foutenmeldingen/codes zouden moeten ontbreken. |
| Functie voor automatisch aanvullen in-/uitschakelen | Elimineer bepaalde meta-gegevensbevelen en verbeter verwerkingstijden door [ van een knevel te voorzien van de Redacteur van de Vraag auto-volledige eigenschap ](../../query-service/ui/user-guide.md#auto-complete). Deze functie stelt automatisch potentiële SQL sleutelwoorden en lijstdetails voor de vraag voor aangezien u het schrijft. |
| Gegevenssetvoorbeelden | Specificeer een steekproeftarief in uw vraag en [ de steekproeven van de gebruiksdataset om een eenvormige willekeurige steekproef ](../../query-service/key-concepts/dataset-samples.md) tot stand te brengen, of voorwaardelijke steekproeven tot stand te brengen die op specifieke criteria worden gebaseerd. |

{style="table-layout:auto"}

Voor meer informatie over Query-services raadpleegt u het [overzicht van Query-services](../../query-service/home.md).


## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B edition is gebaseerd op Real-Time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gerelateerde accountservice inschakelen | Met de nieuwe schakelfunctie kunt u de verwante accountservice op uw account inschakelen. Voor meer informatie, lees de gids op [ toelatend de verwante rekeningendienst ](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Meer over Real-Time CDP B2B edition leren, lees het [ overzicht van B2B edition van Real-Time CDP ](../../rtcdp/overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Toegang op abonnementsniveau toewijzen met [!DNL Google PubSub] | U kunt toegang tot een specifiek onderwerpabonnement nu bepalen wanneer het gebruiken van de [!DNL Google PubSub] bron door abonnements identiteitskaart te verstrekken wanneer het voor authentiek verklaren. Voor meer informatie, lees het [!DNL Google PubSub] authentificatieleerprogramma [ gebruikend de Dienst API van de Stroom ](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) of [ Experience Platform UI ](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Aangepaste activiteitsgegevens verzamelen vanuit [!DNL Marketo] | U kunt nu aangepaste activiteitsgegevens van uw [!DNL Marketo] -instantie overbrengen naar Experience Platform. Om de gegevens van de douaneactiviteit in te voeren, moet u de groepen van het gebied van douaneactiviteiten in het B2B schema van Activiteiten opzetten en een dataflow creëren gebruikend de activiteitendataset. Zodra de gegevensstroom volledig is, zal de ingebedde dataset zowel standaard als douaneactiviteiten van uw [!DNL Marketo] instantie bevatten. U kunt [ Dienst van de Vraag ](../../query-service/home.md) dan gebruiken om tot uw verslagen van de douaneactiviteit op Experience Platform toegang te hebben. Voor meer informatie, lees de gids op [ creërend een dataflow voor de gegevens van de douaneactiviteit ](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Niet-geclaimde accounts uitsluiten van [!DNL Marketo] | U kunt nu configureren of u niet-geclaimde accounts wilt uitsluiten of opnemen in de opname wanneer u een gegevensstroom voor bedrijfsgegevens maakt. Voor meer informatie, lees de gids bij [ het creëren van een bronverbinding en een dataflow voor  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u het [overzicht van bronnen](../../sources/home.md).
