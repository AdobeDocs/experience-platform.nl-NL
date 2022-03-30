---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ae54c1f3f06c8daaf7c0d36beb4d5884bc258eb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 30 maart 2022**

Nieuwe functies in Adobe Experience Platform:

- [Controlelogboeken](#audit-logs)

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Query Service]](#query-service)
- [Bronnen](#sources)
<!-- - [Experience Data Model (XDM)](#xdm) -->

## Controlelogboeken {#audit-logs}

Experience Platform staat u toe om gebruikersactiviteit voor diverse diensten en mogelijkheden te controleren. De auditlogboeken bevatten informatie over wie wat heeft gedaan en wanneer.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Auditlogboeken voor Dataset, Schema, Klasse, Veldgroep, Gegevenstype, Sandbox, Doel, Segment, Samenvoegen, Beleid, Berekende kenmerken, Productprofiel en Account (Adobe) | Dit zijn de middelen die door auditlogboeken worden geregistreerd. Als de eigenschap wordt toegelaten, zullen de controlelogboeken automatisch worden verzameld aangezien de activiteit voorkomt. U te hoeven niet om logboekinzameling manueel toe te laten. |
| Controleverslagen exporteren | De controlelogboeken kunnen als `CSV` of `JSON` bestand. De gegenereerde bestanden worden rechtstreeks op uw computer opgeslagen. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg voor meer informatie over auditlogs in Platform de [overzicht van auditlogboeken](../../landing/governance-privacy-security/audit-logs/overview.md).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op waarschuwingen op basis van gebeurtenissen voor verschillende activiteiten van Platforms. U kunt zich abonneren op verschillende waarschuwingsregels via de [!UICONTROL Alerts] in de gebruikersinterface van het Platform en kan ervoor kiezen waarschuwingsberichten te ontvangen binnen de gebruikersinterface zelf of via e-mailberichten.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe waarschuwingsregels | Er zijn nu twee nieuwe waarschuwingsregels beschikbaar voor bronnen die te maken hebben met gegevensinvoer. Zie het overzicht op [waarschuwingsregels](../../observability/alerts/rules.md) voor de bijgewerkte lijst met waarschuwingstypen. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg voor meer informatie over waarschuwingen in Platform de [waarschuwingsoverzicht](../../observability/alerts/overview.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere [!DNL dashboards] waardoor u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen wordt gevangen.

### Profieldashboards

Op het dashboard Profielen wordt een momentopname weergegeven van de kenmerkgegevens (record) die uw organisatie heeft in de profielopslag in Experience Platform.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Widget niet-gesegmenteerde profielen | De widget geeft het totale aantal profielen weer dat niet aan een segment is gekoppeld. Het gegenereerde nummer is nauwkeurig vanaf de laatste momentopname en biedt de mogelijkheid om het profiel in uw organisatie te activeren. Zie de [profielen, standaard widget-documentatie](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie . |
| Trend-widget voor niet-gesegmenteerde profielen | Deze widget verschaft een lijngrafiekillustratie voor het aantal profielen dat gedurende een bepaalde tijdsperiode niet aan een segment is gekoppeld. De trend kan worden weergegeven over perioden van 30 dagen, 90 dagen en 12 maanden. Zie de [profielen, standaard widget-documentatie](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie . |
| Gesegmenteerde profielen opheffen op identiteitswidget | Deze widget categoriseert het totale aantal niet-gesegmenteerde profielen op basis van hun unieke id. De gegevens worden weergegeven in een staafdiagram. Zie de [profielen, standaard widget-documentatie](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie . |
| Widget enkele identiteitsprofielen | Deze widget bevat een telling van de profielen van uw organisatie die slechts één type id hebben dat tot hun identiteit leidt, of een e-mail of ECID. Zie de [profielen, standaard widget-documentatie](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Raadpleeg voor meer informatie over profielen de [Overzicht van profieldashboards](../../dashboards/guides/profiles.md).

### Doeldashboards

Het dashboard van Doelen toont een momentopname van de bestemmingen die uw organisatie binnen Experience Platform heeft toegelaten.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Widget aantal doelen | De widget geeft het totale aantal beschikbare eindpunten weer waarop een publiek kan worden geactiveerd en geleverd binnen het systeem. Dit aantal omvat zowel actieve als inactieve bestemmingen. Zie de [standaardwidgetdocumentatie voor doelen](../../dashboards/guides/destinations.md#standard-widgets) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de dashboards van Doelen in Platform, verwijs naar [Overzicht van doeldashboards](../../dashboards/guides/destinations.md).

<!-- ## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

| Feature | Description |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>You can now also define ad-hoc custom fields directly within the schema structure and assign them to a new or existing custom field group without needing to create or edit the field group beforehand.<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md). -->

## Query-service {#query-service}

[!DNL Query Service] staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| `table_exists` | De nieuwe eigenschapbevel wordt gebruikt om te bevestigen of een lijst momenteel in het systeem bestaat of niet. De opdracht retourneert een Booleaanse waarde: `true` if de tabel **doet** bestaan, en `false` als de tabel dat doet **niet** bestaan. Zie de [SQL-syntaxisdocumentatie](../../query-service/sql/syntax.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Raadpleeg voor meer informatie over de beschikbare functies de [Overzicht van Query Service](../../query-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor inname looppas te plaatsen, en gegevensopname door te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe bronnen nu beschikbaar voor B2B-gebruik | U kunt nu alle beschikbare bronnen op het Platform voor B2B-gebruiksgevallen gebruiken. Zie de [broncatalogus](../../sources/home.md) voor een volledige lijst van beschikbare bronnen. |
| Algemene beschikbaarheid van nieuwe [!DNL Oracle Eloqua] bron | U kunt nu de opdracht [!DNL Oracle Eloqua] bron voor naadloze invoer van gegevens uit uw [!DNL Oracle Eloqua] -instantie (account, campagne, contactpersonen) aan Platform. Zie de documentatie op [een [!DNL Oracle Eloqua] bronverbinding](../../sources/connectors/marketing-automation/oracle-eloqua.md) voor meer informatie . |
| API-verbeteringen voor [!DNL Data Landing Zone] | De [!DNL Data Landing Zone] bron ondersteunt nu automatische detectie van bestandseigenschappen bij gebruik van de [!DNL Flow Service] API. Zie de documentatie op [een [!DNL Data Landing Zone] bronverbinding](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
