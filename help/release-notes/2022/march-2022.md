---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: 9117fffc58786f05e8741d9695ddb551344b6cc7
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 30 maart 2022**

Nieuwe functies in Adobe Experience Platform:

- [Controlelogboeken](#audit-logs)

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Experience Data Model (XDM)](#xdm)
- [Bronnen](#sources)

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

## Experience Data Model (XDM) {#xdm}

Het Model van Gegevens van de ervaring (XDM) is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Afzonderlijke standaardvelden voor een schema toevoegen of verwijderen | De Redacteur UI van het Schema staat u nu toe om gedeelten standaardgebiedsgroepen aan uw schema&#39;s toe te voegen, die meer flexibiliteit voor de gebieden verstrekken u verkiest te omvatten zonder het moeten douanemiddelen van kras bouwen.<br><br>U kunt aangepaste ad-hocvelden nu ook rechtstreeks definiëren in de schemastructuur en deze toewijzen aan een nieuwe of bestaande aangepaste veldgroep zonder dat u de veldgroep vooraf hoeft te maken of te bewerken.<br><br>Zie de handleiding op [schema&#39;s maken en bewerken in de gebruikersinterface](../../xdm/ui/resources/schemas.md) voor meer informatie over deze nieuwe workflows. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe bronnen nu beschikbaar voor B2B-gebruik | U kunt nu alle beschikbare bronnen op het Platform voor B2B-gebruiksgevallen gebruiken. Zie de [broncatalogus](../../sources/home.md) voor een volledige lijst van beschikbare bronnen. |
| Algemene beschikbaarheid van nieuwe [!DNL Oracle Eloqua] bron | U kunt nu de opdracht [!DNL Oracle Eloqua] bron voor naadloze invoer van gegevens uit uw [!DNL Oracle Eloqua] -instantie (account, campagne, contactpersonen) aan Platform. Zie de documentatie op [een [!DNL Oracle Eloqua] bronverbinding](../../sources/connectors/oracle-eloqua.md) voor meer informatie . |
| API-verbeteringen voor [!DNL Data Landing Zone] | De [!DNL Data Landing Zone] bron ondersteunt nu automatische detectie van bestandseigenschappen bij gebruik van de [!DNL Flow Service] API. Zie de documentatie op [een [!DNL Data Landing Zone] bronverbinding](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
