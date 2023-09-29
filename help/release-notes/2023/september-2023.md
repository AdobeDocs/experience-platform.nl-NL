---
title: Aanvullende informatie over Adobe Experience Platform
description: In de release van september 2023 staat Adobe Experience Platform vermeld.
source-git-commit: 05136ca1a44fa0ecbf2fd9941d047c3a0899f2d1
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 28 september 2023**

Nieuwe functies in Adobe Experience Platform:

- [Berekende kenmerken](#computed-attributes)

Updates voor bestaande functies in Experience Platform:

- [Waarschuwingen](#alerts)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Identiteitsservice](#identity-service)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Berekende kenmerken {#computed-attributes}

Met behulp van berekende kenmerken kunt u gebeurtenisgegevens eenvoudig samenvatten in profielkenmerken via een intuïtieve gebruikersinterface voor verbeterde op gedrag gebaseerde segmentatie, personalisatie en activering. Met deze functie kunt u berekende kenmerken maken op een manier die zichzelf aanbiedt, deze beheren en ze in segmentatie, Real-Time CDP-doelen of Adobe Journey Optimizer gebruiken. Bovendien vereenvoudigen de berekende kenmerken de segmentatie en de workflows voor reizen, zodat u probleemloos relevante ervaringen kunt opdoen. Voor meer informatie over berekende kenmerken leest u de [overzicht van berekende kenmerken](../../profile/computed-attributes/overview.md).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op gebeurtenisgebaseerde waarschuwingen voor verschillende platformactiviteiten. U kunt zich abonneren op verschillende waarschuwingsregels via de [!UICONTROL Alerts] in de gebruikersinterface van het Platform en kan ervoor kiezen waarschuwingsberichten te ontvangen binnen de gebruikersinterface zelf of via e-mailmeldingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Tabblad Waarschuwingsgeschiedenis | De waarschuwingen [!UICONTROL History] tab bevat nu alle gebeurtenissen zoals vertragingen , het starten , het voltooien en mislukken . Lees de [UI-documentatie met waarschuwingen](../../observability/alerts/ui.md) voor meer informatie over het geschiedenislusje. |

{style="table-layout:auto"}

Lees voor meer informatie over waarschuwingen de [[!DNL Observability Insights] overzicht](../../observability/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden, waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Gegevensstromen | Ondersteuning voor opzoeken van apparaten | Wanneer het vormen van een gegevensstroom, kunt u het niveau van apparaat raadplegingsinformatie nu selecteren die moet worden verzameld. De opzoekinformatie van het apparaat omvat gegevens over het apparaat, de hardware, het besturingssysteem en de browser die worden gebruikt om met uw pagina te communiceren. <br>  Opzoekgegevens van het apparaat kunnen niet samen met de gebruikersagent en de clienthints worden verzameld. Als u ervoor kiest apparaatinformatie te verzamelen, wordt de verzameling van gebruikersagent- en clienthints uitgeschakeld en andersom. Alle gegevens van de apparatenraadpleging worden opgeslagen in `xdm:device` veldgroep. Meer informatie vindt u in de documentatie op [configureren, gegevensstromen](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensies | [!DNL TikTok] API-extensie voor webgebeurtenissen | De [[!DNL TikTok] Web Events API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge Network gebruiken en verzenden naar [!DNL TikTok] in de vorm van server-side-gebeurtenissen die de [!DNL TikTok] Web Events API. |

{style="table-layout:auto"}

Voor meer informatie over gegevensverzameling leest u de [overzicht van gegevensverzameling](../../tags/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte doelen** {#new-updated-destinations}

| Bestemming | Nieuw of Bijgewerkt | Beschrijving |
| ----------- |----------------|----------- |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nieuw | [[!DNL HubSpot]](https://www.hubspot.com) is een platform van CRM met alle software, integratie, en middelen u marketing, verkoop, inhoudsbeheer, en de klantendienst moet verbinden. Het staat u toe om uw gegevens, teams, en klanten op één platform van CRM te verbinden. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Bijgewerkt | Extra ondersteuning voor [!DNL Dynamics 365] aangepaste veldvoorvoegsels voor aangepaste velden die niet zijn gemaakt binnen de standaardoplossing in [!DNL Dynamics 365]. Een nieuw invoerveld, **[!UICONTROL Customization Prefix]**, is toegevoegd aan de [Doelgegevens invullen](#destination-details) stap. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | New | Activate audiences previously onboarded to [!DNL LiveRamp] to premium publishers across mobile, web, display, and connected TV mediums. <br> After onboarding audiences to your [!DNL LiveRamp] account through the [LiveRamp - Onboarding](liveramp-onboarding.md) connection, use the new [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) connection to activate the audiences to downstream destinations.  |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Updated | The Experience Cloud Audiences destination is now generally available. Use this destination to activate audiences from Real-Time CDP to Audience Manager and Adobe Analytics. You need an Audience Manager license to send audiences to Adobe Analytics. |

-->

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Uitvoer van gegevens in Real-Time CDP | De [gegevensset exporteren](../../destinations/ui/export-datasets.md) functionaliteit is nu algemeen beschikbaar. Zie [welke gegevenssets u kunt exporteren op basis van de app Experience Platform](../../destinations/ui/export-datasets.md#datasets-to-export) u hebt aangeschaft en de [instructies voor de uitvoer van gegevenssets](/help/destinations/guardrails.md#dataset-exports). |
| (bèta) Ondersteuning voor het exporteren van arraytype-objecten | Exporteer arrays met primitieve waarden (tekenreeks, int of booleaanse waarden) als platte schemabestanden naar de opslagdoelen van de cloud. Meer informatie over de functionaliteit in het dialoogvenster [documentatie](../../destinations/ui/export-arrays-calculated-fields.md). |
| Dynamische dropdown-kiezers in Destination SDK | Wanneer u een doel maakt met Destination SDK, kunt u nu [dynamische vervolgkeuzekiezers](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) om de velden van een vervolgkeuzekiezer te vullen met waarden die zijn opgehaald uit een API. |

**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

- Gebruik van [transparantie controleren](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) nu beschikbaar voor ondernemingsdoelen ([HTTP-API](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) en [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) op het niveau van de dataflow-run om de activeringscijfers en de status in de [gegevensstroomweergave](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), met aanvullende informatie via foutcodes en berichten voor probleemoplossing.
- Wanneer u de naam van het publiek bijwerkt die aan [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md)en andere bestemmingen [update-sjablonen voor publiek](../../destinations/destination-sdk/metadata-api/update-audience-template.md)Deze naamwijzigingen worden nu verderop in de bestemming weergegeven.

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Identiteitsservice {#identity-service}

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface van Identity Service | Gebruik het verbeterde gereedschap voor het maken van aangepaste naamruimten in de gebruikersinterface van het Experience Platform om uw aangepaste naamruimten en de bijbehorende identiteitstypen beter te beheren. De verbeterde interface van de Identiteitsdienst voorziet u van: <ul><li>Contextuele Ervaring: Visuele aanwijzingen, helderheid, en context aan wat een identiteitsnamespace is en identiteitstypes zijn.</li><li>Nauwkeurigheid: betere foutafhandeling, zonder dubbele identiteitsnamen.</li><li>Detectie: toegang tot documentatie vanuit een productdialoogvenster.</li></ul> Lees voor meer informatie de handleiding op [aangepaste naamruimten maken](../../identity-service/namespaces.md#create-namespaces). |
| Wijzigingen in limieten van identiteitsgrafieken | De limiet voor identiteitsgrafieken is gewijzigd van 150 identiteiten in 50 identiteiten. Wanneer een nieuwe identiteit wordt opgenomen in een volledige grafiek, wordt de oudste identiteit op basis van de tijdstempel en het identiteitstype van de inname verwijderd. Identiteitstypen van cookies krijgen prioriteit voor verwijdering. Neem contact op met het accountteam van de Adobe om een wijziging in het type identiteit aan te vragen als uw productiessandbox het volgende bevat: <ul><li>een aangepaste naamruimte waarin de personen-id&#39;s (zoals CRM-id&#39;s) zijn geconfigureerd als cookie-/apparaatidentiteitstype.</li><li>een aangepaste naamruimte waarin cookie-/apparaat-id&#39;s zijn geconfigureerd als identiteitstype voor verschillende apparaten.</li></ul> Deze aanvragen worden handmatig verwerkt door Adobe-engineering. Lees voor meer informatie de [handleidingen voor identiteitsservicegegevens](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Aanpasbare kolommen | U kunt de lay-out van het Portaal van de Publiek met re-sizable kolommen nu aanpassen. Lees voor meer informatie over deze functie de [segmenteringsUI-hulplijn](../../segmentation/ui/overview.md#customize). |
| Uitsplitsing naar frequentie bijwerken | U kunt nu een verdeling van de updatefrequenties van het publiek in uw organisatie bekijken. Lees voor meer informatie over deze functie de [segmenteringsUI-hulplijn](../../segmentation/ui/overview.md#browse). |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).

Voor meer informatie over Segmentatieservice leest u de [Overzicht van segmentatieservice](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe parameters voor `offset` paginering in Self-Serve Sources (Batch SDK) | U kunt nu een `endConditionName` en `endConditionValue` voor uw bron wanneer u `offset` paginering. Met deze parameters kunt u de voorwaarde aangeven die de pagineringslus in de volgende HTTP-aanvraag beëindigt. Lees voor meer informatie de [pagination guide for Self-Serve Sources (Batch SDK)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).