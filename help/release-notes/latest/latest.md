---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 78f9b8434d577909ccb1c62211a802e05c8291e1
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 26 januari 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [Query-service](#query-service)
- [Sandboxen](#sandboxes)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op waarschuwingen op basis van gebeurtenissen voor verschillende activiteiten van Platforms. U kunt zich abonneren op verschillende waarschuwingsregels via de [!UICONTROL Alerts] in de gebruikersinterface van het Platform en kan ervoor kiezen waarschuwingsberichten te ontvangen binnen de gebruikersinterface zelf of via e-mailberichten.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe waarschuwingsregels | Er zijn nu verschillende nieuwe waarschuwingsregels beschikbaar voor workflows die betrekking hebben op gegevensinvoer, identiteiten, profielen, segmentering en activering. Zie het overzicht op [waarschuwingsregels](../../observability/alerts/rules.md) voor de bijgewerkte lijst met waarschuwingstypen. |
| In-context alarm voor bronnen dataflows | U kunt zich nu abonneren op het ontvangen van waarschuwingsberichten over de status van uw gegevensstromen tijdens de inlogworkflow. Zie de handleiding voor meer informatie over [abonneren op berichten voor bronnen in de gebruikersinterface](../../sources/tutorials/ui/alerts.md). |

Raadpleeg voor meer informatie over waarschuwingen in Platform de [waarschuwingsoverzicht](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

| Functie | Beschrijving |
| --- | --- |
| Intelligente bijschriften | Een machine het leren algoritme verstrekt automatisch inzichten op uw profiel en publieksgegevens, en illustreert patronen en tendensen over een 30-90 dag, of periode van 12 maanden. De bijschriften bevatten informatie over <ul><li>Algemene vorm en statistieken</li><li>Trends en abrupte wijzigingen</li><li>Seizoenspatronen</li><li>Onverwachte anomalieën</li></ul> Meer informatie is te vinden op de [profielen, dashboards](../../dashboards/guides/profiles.md#profiles-count-trend) en [segmentdashboards](../../dashboards/guides/segments.md#audience-size-trend) documentatie. |
| Overzicht van dashboards | Open de vooraf geconfigureerde rapporten van profiel-, segmenten- en doeldashboards, inclusief geïnstalleerde integraties zoals PowerBI, op een gecentraliseerde locatie. Zie voor meer informatie de [[!DNL Dashboards] overzicht](../../dashboards/home.md). |
| PowerBI-rapportsjablonen | Met nieuwe PowerBI-diagrammen kunt u metriek van het profiel, de segmenten en de doelrapportgegevensmodellen maken, aanpassen of uitbreiden. Met de geautomatiseerde installatieworkflow kunt u uw marketinginzichten binnen uw organisatie delen vanuit de PowerBI-omgeving. Zie voor meer informatie de [[!DNL Dashboards] overzicht](../../dashboards/home.md). |

Voor meer informatie over [!DNL Dashboards], zie de [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Geconsolideerde toewijzingservaring | De nieuwe toewijzingsinterface in het Platform UI voorziet u van een verenigbare afbeeldingservaring om uit intelligente kaartaanbevelingen voordeel te halen, manueel toewijzingsregels te vormen, en om het even welke fouten te zuiveren die aan uw kaartreeksen voorkomen. Zie voor meer informatie de [[!DNL Data Prep] UI-hulplijn](../../data-prep/ui/mapping.md). |

Voor meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

<!--

## [!DNL Destinations] {#destinations}

[!DNL Destinations] are pre-built integrations with destination platforms that allow for the seamless activation of data from Adobe Experience Platform. You can use destinations to activate your known and unknown data for cross-channel marketing campaigns, email campaigns, targeted advertising, and many other use cases.

| Feature | Description |
| ----------- | ----------- |
| Placeholder for next-hit personalization | Description |
| Placeholder for batch monitoring | Description |
| Placeholder for re-introducing scheduling in the UI | Description |
| Placeholder for Marketo destination update | Description |


**New destinations**

| Destination | Description |
| ----------- | ----------- |
| Placeholder for Target | Description |
| Placeholder for Custom Personalization | Description |

For more general information on destinations, refer to the [destinations overview](../../destinations/home.md).

-->

## Query-service {#query-service}

[!DNL Query Service] staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Anoniem blok | Het anonieme blokSQL bouwt staat u toe om de taken van de grote schaal van de gegevensvoorbereiding in de Dienst van de Vraag in kleinere taken te verdelen, dan hergebruik en hen in opeenvolging voor het stijgende laden van gegevens uit te voeren. Zie voor meer informatie de [Overzicht van Query Service](../../query-service/home.md). |
| Datasetorganisatie | Verstrekt een coherente, logische gegevensstructuur om uw gegevensactiva voor gebruik met de Dienst van de Vraag te organiseren aangezien de hoeveelheid gegevensactiva binnen de zandbak groeit. Zie voor meer informatie de [Overzicht van Query Service](../../query-service/home.md). |

Voor meer informatie over [!DNL Query Service], zie de [[!DNL Query Service] overzicht](../../query-service/home.md).

## Sandboxen {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface van sandboxen | De sandboxindicator is nu geïntegreerd in de header voor alle Platform-UI-toepassingen. De sandboxindicator geeft de naam, het gebied en het type van de sandbox weer en geeft u ook toegang tot een vervolgkeuzemenu om tussen de sandboxen te schakelen. Zie voor meer informatie de [UI-hulplijn sandbox](../../sandboxes/ui/user-guide.md). |

Voor meer informatie over sandboxen raadpleegt u de [sandboxen, overzicht](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Segmentovereenkomst | Segmentovereenkomst is een service voor gegevenssamenwerking waarmee twee of meer gebruikers in het Platform gegevens kunnen uitwisselen op basis van gemeenschappelijke id&#39;s op een veilige, beheerde en privacyvriendelijke manier. Segmentovereenkomst maakt gebruik van privacystandaarden voor Platforms en persoonlijke id&#39;s, zoals gehashte e-mails, gehashte telefoonnummers en apparaat-id&#39;s, zoals IDFA&#39;s en GAID&#39;s. Zie voor meer informatie de [Overzicht van afstemming van segment](../../segmentation/ui/segment-match/overview.md). |

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] bronverbeteringen | De [!DNL Event Hubs] De bron ondersteunt nu SAS-sleuteltype verificatie buiten de hoofdmap om verbinding te maken en bronverbinding te maken. Zie voor meer informatie de [[!DNL Event Hubs] overzicht](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] bronverbeteringen | De [!DNL SFTP] De bron staat u nu toe om een vastgestelde aantal van een maximum gezamenlijke verbindingen te vestigen die een dataflow kan gebruiken om met de server van SFTP te verbinden. Zie voor meer informatie de [[!DNL SFTP] overzicht](../../sources/connectors/cloud-storage/sftp.md). |
