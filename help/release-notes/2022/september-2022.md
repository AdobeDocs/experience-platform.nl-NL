---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2022
description: In de release van september 2022 staat een opmerking voor Adobe Experience Platform.
source-git-commit: 5335c77b4636d10064e8786525c9f8f893371b9b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 28 september 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Bronnen](#sources)

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| UI-ondersteuning voor opsommingen en voorgestelde waarden | Naast opsommingen die gegevensvalidatie mogelijk maken, kunt u nu [voorgestelde waarden toevoegen of verwijderen](../../xdm/ui/fields/enum.md) voor standaard of aangepaste tekenreeksvelden, zodat gebruikers van het Platform een lijst met waarden kunnen selecteren bij het maken van segmenten. |

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Eigenschappen van een specifiek element waarmee interactie heeft plaatsgevonden die ertoe heeft geleid dat de proposition-gebeurtenis werd geactiveerd. |
| Veldgroep | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Mediainteracties worden in de loop der tijd bijgehouden. |
| Veldgroep | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Hier vindt u informatie over mediagegevens. |
| Veldgroep | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beschrijft oppervlakken voor Experience Events in Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gedraging | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Toegevoegde waarden voor `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Verwijderde waarden voor `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Veldgroep | (Meerdere) | [Verschillende veldbeschrijvingen zijn bijgewerkt](https://github.com/adobe/xdm/pull/1628/files) over Journey Orchestration-componenten. |
| Veldgroep | (Meerdere) | [De titels voor verschillende Adobe Workfront-componenten zijn bijgewerkt](https://github.com/adobe/xdm/pull/1634/files) ter wille van de consistentie. |
| Veldgroep | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | De naamruimten van verschillende velden zijn bijgewerkt naar `xdm`. |
| Veldgroep | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Een nieuw veld toegevoegd, `isReadSegmentTriggerStartEvent`. |
| Veldgroep | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | De `xdm:uvIndex` veld aan een type geheel getal en de waarde `xdm` naamruimte maken voor verschillende velden waarin naamruimte ontbreekt. |
| Veldgroep | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` en `xdm:implementationDetails` zijn verwijderd uit de veldgroep. |
| Gegevenstype | (Meerdere) | [Verschillende namen van media-eigenschappen zijn bijgewerkt](https://github.com/adobe/xdm/pull/1626/files) voor diverse gegevenstypen, voor consistentie. |
| Gegevenstype | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Toegevoegde bekende namen voor flutter. |
| Gegevenstype | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Het gegevenstype kan nu een lijst met sleutelwaardeparen voor metagegevens accepteren die zijn gekoppeld aan het betreffende punt. |
| Gegevenstype | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] is hernoemd naar [!UICONTROL Proposition Action]. |
| Gegevenstype | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] is hernoemd naar [!UICONTROL Proposition Action]. |
| (Meerdere) | (Meerdere) | Experimentele eigenschappen zijn [gestabiliseerd over alle B2B-componenten](https://github.com/adobe/xdm/pull/1617/files). |
| (Meerdere) | (Meerdere) | Adobe Journey Optimizer-entiteiten zijn [gestabiliseerd](https://github.com/adobe/xdm/pull/1625/files). |
| (Meerdere) | (Meerdere) | De naamruimten van bepaalde velden in verschillende experimentele componenten zijn: [bijgewerkt voor consistentie](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Identiteitsservice {#identity-service}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen gefragmenteerd zijn, die elke klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het verwijderen van gegevenssets | De Dienst van de identiteit steunt nu dataset schrapping wanneer het verzoeken door [Catalogusservice-API](https://developer.adobe.com/experience-platform-apis/references/catalog/), UI of Data Hygiene. Lees de handleiding op [het schrappen van datasets in UI](../../catalog/datasets/user-guide.md#delete-a-dataset) voor meer informatie . |

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Audience Manager segmentpopulatie impact op Real-time klantprofiel | De inname van grote populaties in het Audience Manager segment heeft een directe invloed op uw totale aantal profielen wanneer u eerst een segment van de Audience Manager naar het Platform verzendt gebruikend de bron van de Audience Manager. Dit betekent dat het selecteren van alle segmenten kan leiden tot een aantal profielen dat groter is dan uw gebruiksrechten voor licenties. Lees voor meer informatie de [Overzicht van bron Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Voor informatie over uw licentiegebruik leest u de documentatie op [het gebruiken van het dashboard van het vergunningsgebruik](../../dashboards/guides/license-usage.md). |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).