---
title: Opmerkingen bij de release van Adobe Experience Platform, april 2022
description: In de release van april 2022 staat een opmerking voor Adobe Experience Platform.
source-git-commit: 4bbf7642a456f36ea0fe7fc1c8d68ad37351ff4c
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 april 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Experience Data Model (XDM)](#xdm)

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
