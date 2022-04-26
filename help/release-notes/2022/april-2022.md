---
title: Opmerkingen bij de release van Adobe Experience Platform, april 2022
description: In de release van april 2022 staat een opmerking voor Adobe Experience Platform.
source-git-commit: d09eb2e71a5ebce31aeaf8560c20f0c8595f5d19
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 april 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensstromen](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Experience Data Model (XDM)](#xdm)
- [Real-time Customer Data Platform B2B Edition](#B2B)
- [Bronnen](#sources)

## Gegevensstromen {#dataflows}

In Platform, worden de gegevens opgenomen van vele verschillende bronnen, binnen het systeem geanalyseerd, en geactiveerd aan een brede verscheidenheid van bestemmingen. Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Gegevensstromen zijn een weergave van taken die gegevens over het Platform verplaatsen. Deze gegevensstromen worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door de Dienst van de Identiteit en het Profiel van de Klant in real time alvorens uiteindelijk aan bestemmingen wordt geactiveerd wordt gebruikt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Segmentdashboard | U kunt het controledashboard nu gebruiken om de gegevensstromen voor segmenten te controleren. Lees de handleiding voor meer informatie op [het controleren van segmenten in UI](../../dataflows/ui/monitor-segments.md) |

Voor meer algemene informatie over gegevensstromen raadpleegt u de [gegevensstroomoverzicht](../../dataflows/home.md). Als u meer wilt weten over segmentatie, raadpleegt u de [segmentatieoverzicht](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor Adobe Analytics-bron | De Adobe Analytics-bron biedt nu ondersteuning voor functies voor het voorvertonen van gegevens, zodat u uw gegevens uit de Analytics-rapportenreeks kunt toewijzen aan een doel-XDM-schema wanneer u een gegevensstroom maakt. Zie de zelfstudie aan [een verbinding met een bron voor Analytics maken](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie . |
| Ondersteuning voor het importeren van bestaande toewijzingsregels | U kunt nu toewijzingsregels importeren uit een bestaande gegevensstroom om uw databaseconfiguraties te versnellen en fouten te beperken. Zie de zelfstudie aan [bestaande toewijzingsregels importeren](../../data-prep/ui/mapping.md) voor meer informatie . |

Voor meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Afzonderlijke standaardvelden voor een schema toevoegen of verwijderen | De Redacteur UI van het Schema staat u nu toe om gedeelten standaardgebiedsgroepen aan uw schema&#39;s toe te voegen, die meer flexibiliteit voor de gebieden verstrekken u verkiest te omvatten zonder het moeten douanemiddelen van kras bouwen.<br><br>U kunt aangepaste ad-hocvelden nu ook rechtstreeks definiëren in de schemastructuur en deze toewijzen aan een nieuwe of bestaande aangepaste veldgroep zonder dat u de veldgroep vooraf hoeft te maken of te bewerken.<br><br>Zie de handleiding op [schema&#39;s maken en bewerken in de gebruikersinterface](../../xdm/ui/resources/schemas.md) voor meer informatie over deze nieuwe workflows. |

{style=&quot;table-layout:auto&quot;}

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Algemeen schema | [[!UICONTROL Data Hygiene Operation Request]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Hiermee legt u de details vast van een verzoek om gegevens te wissen om records in een opgegeven gegevensset of sandbox te verwijderen of te wijzigen. |
| Descriptor | [[!UICONTROL Time-series Granularity Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Geeft de granulariteit van tijdreeksen en samenvattingsgegevens aan. Wanneer toegepast op een schema, de schema&#39;s `timestamp` field is de eerste tijdstempel in een periode van deze granulariteit. |
| Klasse | [[!UICONTROL XDM Summary Metrics]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Verstrekt vooraf samengevatte metriek met groeperingsdimensies, zoals de resultaten van SQL UITGEZOCHT met GROUP DOOR. |
| Veldgroep | [[!UICONTROL Consent policies evaluation results map]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Vangt het resultaat van de beoordeling van het toestemmingsbeleid voor een individu. |
| Veldgroep | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Vangt plaats-onderzoek verwante informatie zoals onderzoeksvraag, het filtreren, en het opdracht geven tot. |
| Veldgroep | [[!UICONTROL Merge Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Hiermee legt u de details vast van een gebeurtenis waarbij twee of meer leads worden samengevoegd. |
| Veldgroep | [[!UICONTROL Email Sent]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Hiermee legt u de details vast van een gebeurtenis waarbij een e-mailbericht naar een ontvanger wordt verzonden. |
| Veldgroep | [[!UICONTROL Stitching Fields]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Hiermee legt u waarden vast die zijn berekend via het identiteitsstitching-proces voor een gebeurtenis. |
| Veldgroep | [[!UICONTROL Secondary Recipient Detail For Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Een Adobe Journey Optimizer gebiedsgroep die een secundair ontvangend detail voor een controle vangt. |
| Veldgroep | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hiermee worden gegevens vastgelegd die betrekking hebben op een relatie tussen een rekeningpersoon. |
| Veldgroep | [[!UICONTROL Account Person Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hiermee worden gegevens vastgelegd die betrekking hebben op een relatie tussen een rekeningpersoon. |
| Gegevenstype | [[!UICONTROL Cart]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Leg informatie vast over een winkelwagentje voor e-handel. |
| Gegevenstype | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Vangt verzendgegevens voor een of meer producten. |
| Gegevenstype | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Hiermee legt u gegevens vast over zoekactiviteiten ter plaatse. |
| Extensie (Workfront) | [[!UICONTROL Operational Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Hiermee legt u gegevens vast over een operationele taak. |
| Extensie (Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Hiermee legt u gegevens vast die betrekking hebben op een werkportfolio. |
| Extensie (Workfront) | [[!UICONTROL Work Program Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Hiermee legt u de details van een werkprogramma vast. |
| Extensie (Workfront) | [[!UICONTROL Work Project Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Hiermee legt u de details van een werkproject vast. |

{style=&quot;table-layout:auto&quot;}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Algemeen schema | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nieuwe opsommingswaarden voor `destinationCategory`. |
| Descriptor | [[!UICONTROL Friendly Name Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Extra ondersteuning voor het verwijderen van voorgestelde waarden (`meta:enum`) die niet nodig zijn vanuit standaardvelden. |
| Veldgroep | [[!UICONTROL User Login Process]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` toegevoegd. |
| Gegevenstype | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Er zijn verschillende tekstvelden toegevoegd die betrekking hebben op winkelwagentjes. |
| Gegevenstype | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nieuwe velden toegevoegd voor geselecteerde opties en kortingsbedrag. |
| Extensie (intelligente diensten) | [[!UICONTROL Intelligent Services JourneyAI Send Time Optimization]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimaliseer opslagindeling voor scores tijdens het verzenden. |
| Extensie (Workfront) | [[!UICONTROL Workfront Change Event]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Verschillende velden vervangen door een `workfront:customData` veld voor aangepaste formuliervelden. |
| Extensie (Workfront) | [[!UICONTROL Work Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Verschillende velden toegevoegd. |
| Extensie (Workfront) | [[!UICONTROL Work Object]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nieuwe velden voor het type bovenliggend object en aangepaste formuliervelden. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

### Real-time Customer Data Platform B2B Edition {#B2B}

Gebaseerd op Real-time Customer Data Platform (Real-Time CDP), is de Echte - tijdCDP B2B Uitgave speciaal-gebouwd voor marketers die in een zaken-aan-zaken de dienstmodel werken. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen te betrekken.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor `isDeleted` functionaliteit | Alles [!DNL Marketo] gegevenssets, behalve `Activities` nu de `isDeleted` toewijzing. De nieuwe toewijzing wordt automatisch toegevoegd aan uw bestaande B2B dataflows. U kunt de `isDeleted` toewijzen aan filtergegevens die zijn verwijderd, zodat de gegevens in de [!DNL Data Lake] is consistent met uw brongegevens. Zie de [[!DNL Marketo] hulplijn met toewijzingsvelden](../../sources/connectors/adobe-applications/mapping/marketo.md) voor meer informatie over `isDeleted`. |

Als u meer wilt weten over de Real-time Customer Data Platform B2B Edition, raadpleegt u de [B2B-overzicht](../../rtcdp/b2b-overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor [!DNL OneTrust Integration] | U kunt nu de opdracht [!DNL OneTrust Integration] bron voor het toevoegen van toestemmings- en voorkeursgegevens uit uw [!DNL OneTrust] aan Platform. Zie de documentatie op [een [!DNL OneTrust Integration] bronverbinding](../../sources/connectors/consent-and-preferences/onetrust.md) voor meer informatie . |
| Ondersteuning voor [!DNL Square] | U kunt nu de opdracht [!DNL Square] bron om betalingsgegevens van uw [!DNL Square] aan Platform. |
| Ondersteuning voor het verwijderen van klantkenmerkgegevensstromen | U kunt nu dataflows verwijderen die zijn gemaakt met de bronconnector Klantkenmerken. |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
