---
title: Opmerkingen bij de release van Adobe Experience Platform Januari 2022
description: Aanvullende informatie van januari 2022 voor Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 1e9d6b0c43461902c5b966aa1d0576103e872e0c
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 26 januari 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op gebeurtenisgebaseerde waarschuwingen voor verschillende platformactiviteiten. U kunt zich abonneren op verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van het platform en u kunt ervoor kiezen waarschuwingsberichten te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe waarschuwingsregels | Er zijn nu verschillende nieuwe waarschuwingsregels beschikbaar voor workflows die betrekking hebben op gegevensinvoer, identiteiten, profielen, segmentering en activering. Zie het overzicht op [ waakzame regels ](../../observability/alerts/rules.md) voor de bijgewerkte lijst van waakzame types. |
| In-context alarm voor bronnen dataflows | U kunt zich nu abonneren op het ontvangen van waarschuwingsberichten over de status van uw gegevensstromen tijdens de inlogworkflow. Voor meer informatie, zie de gids op [ het intekenen aan bronalarm in UI ](../../sources/tutorials/ui/alerts.md). |

Voor meer informatie over alarm in Platform, verwijs naar het [ alarm overzicht ](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

| Functie | Beschrijving |
| --- | --- |
| Intelligente bijschriften | Een machine het leren algoritme verstrekt automatisch inzichten op uw profiel en publieksgegevens, en illustreert patronen en tendensen over een 30-90 dag, of periode van 12 maanden. De bijschriften bevatten informatie over <ul><li>Algemene vorm en statistieken</li><li>Trends en abrupte wijzigingen</li><li>Seizoenspatronen</li><li>Onverwachte anomalieën</li></ul> Meer informatie kan op de [ profielen dashboards ](../../dashboards/guides/profiles.md#profiles-count-trend) en [ segmentdashboards ](../../dashboards/guides/audiences.md#audience-size-trend) documentatie worden gevonden. |
| Overzicht van dashboards | Open de vooraf geconfigureerde rapporten van profiel-, segmenten- en doeldashboards, inclusief alle geïnstalleerde integraties zoals PowerBI, op een gecentraliseerde locatie. Voor meer informatie, zie de [[!DNL Dashboards]  inventarisdocumentatie ](../../dashboards/inventory.md). |
| PowerBI-rapportsjablonen | Met nieuwe PowerBI-diagrammen kunt u metriek van het profiel, de segmenten en de gegevensmodellen voor bestemmingsrapportage samenstellen, aanpassen of uitbreiden. Met de geautomatiseerde installatieworkflow kunt u uw marketinginzichten binnen uw organisatie delen vanuit de PowerBI-omgeving. Voor meer informatie, zie de [ documentatie van het het rapportmalplaatje van PowerBI ](../../dashboards/integrations/power-bi.md). |

Voor meer informatie over [!DNL Dashboards], gelieve te zien het [[!DNL Dashboards]  overzicht ](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Geconsolideerde toewijzingservaring | De nieuwe toewijzingsinterface in Platform UI voorziet u van een verenigbare afbeeldingservaring om uit intelligente kaartaanbevelingen voordeel te halen, manueel toewijzingsregels te vormen, en om het even welke fouten te zuiveren die aan uw kaartreeksen voorkomen. Voor meer informatie, zie de [[!DNL Data Prep]  gids UI ](../../data-prep/ui/mapping.md). |

Voor meer informatie over [!DNL Data Prep], gelieve te zien het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ----------- | ----------- |
| Zelfde pagina en volgende pagina personalisatie | De [ zelfde-pagina en volgende-pagina verpersoonlijkingseigenschap ](../../destinations/ui/activate-edge-personalization-destinations.md) verstrekt een gedeelde, gerichte mening van gebruikers voor toepassingen op de Edge Network, voor consistentie tussen marketing en klantenkanalen. Deze verpersoonlijking is mogelijk door de [ verbinding van Adobe Target ](../../destinations/catalog/personalization/adobe-target-connection.md) en de [ de verpersoonlijkingsverbinding van de Douane ](../../destinations/catalog/personalization/custom-personalization.md). Om uw zelfde-pagina of volgende-pagina verpersoonlijkingscampagnes te vormen, zie het [ specifieke leerprogramma ](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Batchdoelbewaking en segmentcijfers | De functionaliteit van bestemmings controle wordt nu uitgebreid van het stromen bestemmingen om ook partijbestemmingen en segment-vlakke metriek voor uw activeringsgegevens te omvatten. Voor meer informatie, lees [ controlerend het dashboard van bestemmingen ](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [ controle segment baandashboard ](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard), en [ segment-vlakke mening ](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Bewerken in de gebruikersinterface plannen voor bestaande gegevens voor batchactivering | Deze versie introduceert de optie om het schema van uw bestaande activeringsgegevens te bewerken naar batchbestemmingen. Voor meer informatie, lees [ profielgegevens aan de bestemmingen van het partijprofiel ](/help/destinations/ui/activate-batch-profile-destinations.md) activeren. |
| Verbeteringen voor Marketo-bestemming | De klanten van het Experience Platform die Marketo Engage gebruiken kunnen hun gegevensbestand van Marketo met de nieuwe capaciteit maximaliseren om net-nieuwe persoonverslagen in Marketo Engage van Experience Platform via de [ de bestemmingsschakelaar van Marketo ](/help/destinations/catalog/adobe/marketo-engage.md) te duwen. <br> Wanneer het verzenden van publiekssegmenten van Experience Platform naar Marketo Engage, kunnen de mensen binnen het segment die niet reeds in uw gegevensbestand van het Marketo Engage bestaan automatisch aan het worden toegevoegd. Voor meer informatie, lees [ een Segment van Adobe Experience Platform aan een Statische Lijst van Marketo ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html) (stap 9 in het leerprogramma wijst erop hoe te om net-nieuwe persoonverslagen in Marketo te duwen). |

**Nieuwe bestemmingen**

| Doel | Beschrijving |
| ----------- | ----------- |
| [ verbinding van Adobe Target ](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie en experimenteren biedt in alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer. Adobe Target is een personalisatieverbinding in Adobe Experience Platform. |
| ](../../destinations/catalog/personalization/custom-personalization.md) de verpersoonlijkingsverbinding van 0} Douane[ | Deze verpersoonlijkingsverbinding verstrekt een manier om segmentinformatie van Adobe Experience Platform aan externe verpersoonlijkingsplatforms, inhoudsbeheersystemen, en servers, en andere toepassingen terug te winnen die op klantenwebsites lopen. |

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Query-service {#query-service}

Met [!DNL Query Service] kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake] . U kunt zich bij om het even welke datasets van [!DNL Data Lake] aansluiten en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Wetenschap van Gegevens Workspace, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Anoniem blok | Het anonieme blokSQL bouwt staat u toe om de taken van de grote schaal van de gegevensvoorbereiding in de Dienst van de Vraag in kleinere taken te verdelen, dan hergebruik en hen in opeenvolging voor het stijgende laden van gegevens uit te voeren. Voor meer informatie, zie de [ steekproefvragen voor anonieme blokdocumentatie ](../../query-service/key-concepts/anonymous-block.md). |
| Datasetorganisatie | Verstrekt een coherente, logische gegevensstructuur om uw gegevensactiva voor gebruik met de Dienst van de Vraag te organiseren aangezien de hoeveelheid gegevensactiva binnen de zandbak groeit. Voor meer informatie, zie [ de documentatie van gegevensactiva organiseren ](../../query-service/best-practices/organize-data-assets.md). |

Voor meer informatie over [!DNL Query Service], gelieve te zien het [[!DNL Query Service]  overzicht ](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface van sandboxen | De sandboxindicator is nu geïntegreerd in de header voor alle Platform UI-toepassingen. De sandboxindicator geeft de naam, het gebied en het type van de sandbox weer en geeft u ook toegang tot een vervolgkeuzemenu om tussen de sandboxen te schakelen. Voor meer informatie, zie de [ gids UI van de zandbak ](../../sandboxes/ui/user-guide.md). |

Voor meer informatie over zandbakken, te zien gelieve het [ overzicht van zandbakken ](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Segmentovereenkomst | Segmentovereenkomst is een service voor gegevenssamenwerking waarmee twee of meer platformgebruikers gegevens kunnen uitwisselen op basis van gemeenschappelijke id&#39;s op een veilige, beheerde en privacyvriendelijke manier. Segmentovereenkomst maakt gebruik van privacystandaarden van het platform en persoonlijke id&#39;s, zoals gehashte e-mails, gehashte telefoonnummers en apparaat-id&#39;s, zoals IDFA&#39;s en GAID&#39;s. Voor meer informatie, zie het [ overzicht van de Gelijke van het Segment ](../../segmentation/ui/segment-match/overview.md). |

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Beta-bronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] bronverbeteringen | De [!DNL Event Hubs] -bron ondersteunt nu niet-root SAS-sleuteltype verificatie voor het maken van verbinding en het maken van bronverbinding. Voor meer informatie, zie het [[!DNL Event Hubs]  overzicht ](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] bronverbeteringen | Met de [!DNL SFTP] -bron kunt u nu een ingesteld aantal maximale gelijktijdige verbindingen instellen die een gegevensstroom kan gebruiken om verbinding te maken met de SFTP-server. Voor meer informatie, zie het [[!DNL SFTP]  overzicht ](../../sources/connectors/cloud-storage/sftp.md). |
