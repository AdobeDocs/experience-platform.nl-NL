---
title: 'Aanvullende informatie van januari 2022 voor Adobe Experience Platform '
description: Aanvullende informatie van januari 2022 voor Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 25%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 26 januari 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op waarschuwingen die zijn gebaseerd op gebeurtenissen voor verschillende Experience Platform-activiteiten. U kunt zich abonneren op verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de Experience Platform-gebruikersinterface en u kunt ervoor kiezen waarschuwingsberichten te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe waarschuwingsregels | Er zijn nu verschillende nieuwe waarschuwingsregels beschikbaar voor workflows die betrekking hebben op gegevensinvoer, identiteiten, profielen, segmentering en activering. Zie het overzicht op [ waakzame regels ](../../observability/alerts/rules.md) voor de bijgewerkte lijst van waakzame types. |
| In-context alarm voor bronnen dataflows | U kunt zich nu abonneren op het ontvangen van waarschuwingsberichten over de status van uw gegevensstromen tijdens de inlogworkflow. Voor meer informatie, zie de gids op [ het intekenen aan bronalarm in UI ](../../sources/tutorials/ui/alerts.md). |

Voor meer informatie over alarm in Experience Platform, verwijs naar het [ alarm overzicht ](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten kunt bekijken over de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnamen.

| Functie | Beschrijving |
| --- | --- |
| Intelligente bijschriften | Een machine het leren algoritme verstrekt automatisch inzichten op uw profiel en publieksgegevens, en illustreert patronen en tendensen over een 30-90 dag, of periode van 12 maanden. De bijschriften bevatten informatie over <ul><li>Algemene vorm en statistieken</li><li>Trends en abrupte wijzigingen</li><li>Seizoenspatronen</li><li>Onverwachte anomalieën</li></ul> Meer informatie kan op de [ profielen dashboards ](../../dashboards/guides/profiles.md#profiles-count-trend) en [ segmentdashboards ](../../dashboards/guides/audiences.md#audience-size-trend) documentatie worden gevonden. |
| Overzicht van dashboards | Open de vooraf geconfigureerde rapporten van profiel-, segmenten- en doeldashboards, inclusief alle geïnstalleerde integraties zoals PowerBI, op een gecentraliseerde locatie. Voor meer informatie, zie de [[!DNL Dashboards]  inventarisdocumentatie ](../../dashboards/inventory.md). |
| PowerBI-rapportsjablonen | Met nieuwe PowerBI-diagrammen kunt u metriek van het profiel, de segmenten en de gegevensmodellen voor bestemmingsrapportage samenstellen, aanpassen of uitbreiden. Met de geautomatiseerde installatieworkflow kunt u uw marketinginzichten binnen uw organisatie delen vanuit de PowerBI-omgeving. Voor meer informatie, zie de [ documentatie van het het rapportmalplaatje van PowerBI ](../../dashboards/integrations/power-bi.md). |

Voor meer informatie over [!DNL Dashboards] raadpleegt u het [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Geconsolideerde toewijzingservaring | De nieuwe toewijzingsinterface in Experience Platform UI voorziet u van een verenigbare afbeeldingservaring om uit intelligente kaartaanbevelingen voordeel te halen, manueel toewijzingsregels te vormen, en om het even welke fouten te zuiveren die aan uw kaartreeksen voorkomen. Voor meer informatie, zie de [[!DNL Data Prep]  gids UI ](../../data-prep/ui/mapping.md). |

Voor meer informatie over [!DNL Data Prep] raadpleegt u het [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| Zelfde pagina en volgende pagina personalisatie | De [ zelfde-pagina en volgende-pagina verpersoonlijkingseigenschap ](../../destinations/ui/activate-edge-personalization-destinations.md) verstrekt een gedeelde, gerichte mening van gebruikers voor toepassingen op Edge Network, voor consistentie tussen marketing en klantenkanalen. Deze verpersoonlijking is mogelijk door de [ verbinding van Adobe Target ](../../destinations/catalog/personalization/adobe-target-connection.md) en de [ de verpersoonlijkingsverbinding van de Douane ](../../destinations/catalog/personalization/custom-personalization.md). Om uw zelfde-pagina of volgende-pagina verpersoonlijkingscampagnes te vormen, zie het [ specifieke leerprogramma ](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Batchdoelbewaking en segmentcijfers | De functionaliteit van bestemmings controle wordt nu uitgebreid van het stromen bestemmingen om ook partijbestemmingen en segment-vlakke metriek voor uw activeringsgegevens te omvatten. Voor meer informatie, lees [ controlerend het dashboard van bestemmingen ](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [ controle segment baandashboard ](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard), en [ segment-vlakke mening ](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Bewerken in de gebruikersinterface plannen voor bestaande gegevens voor batchactivering | Deze versie introduceert de optie om het schema van uw bestaande activeringsgegevens te bewerken naar batchbestemmingen. Voor meer informatie, lees [ profielgegevens aan de bestemmingen van het partijprofiel ](/help/destinations/ui/activate-batch-profile-destinations.md) activeren. |
| Verbeteringen voor Marketo-bestemming | De klanten van Experience Platform die Marketo Engage gebruiken kunnen hun gegevensbestand van Marketo met de nieuwe capaciteit maximaliseren om net-nieuwe persoonverslagen in Marketo Engage van Experience Platform via de [ de bestemmingsschakelaar van Marketo ](/help/destinations/catalog/adobe/marketo-engage.md) te duwen. <br> Wanneer u publiekssegmenten van Experience Platform naar Marketo Engage verzendt, kunnen er automatisch personen binnen het segment worden toegevoegd die nog niet in uw Marketo Engage-database bestaan. Voor meer informatie, lees [ een Segment van Adobe Experience Platform aan een Statische Lijst van Marketo ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html) (stap 9 in het leerprogramma wijst erop hoe te om net-nieuwe persoonverslagen in Marketo te duwen). |

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [ verbinding van Adobe Target ](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie en experimenteren biedt in alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer. Adobe Target is een personalisatieverbinding in Adobe Experience Platform. |
| [&#128279;](../../destinations/catalog/personalization/custom-personalization.md) de verpersoonlijkingsverbinding van 0&rbrace; Douane | Deze verpersoonlijkingsverbinding verstrekt een manier om segmentinformatie van Adobe Experience Platform aan externe verpersoonlijkingsplatforms, inhoudsbeheersystemen, en servers, en andere toepassingen terug te winnen die op klantenwebsites lopen. |

Voor meer algemene informatie over bestemmingen raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Query-service {#query-service}

Met [!DNL Query Service] kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake] . U kunt willekeurige datasets van [!DNL Data Lake] combineren en de queryresultaten vastleggen als nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Anoniem blok | Het anonieme blokSQL bouwt staat u toe om de taken van de grote schaal van de gegevensvoorbereiding in de Dienst van de Vraag in kleinere taken te verdelen, dan hergebruik en hen in opeenvolging voor het stijgende laden van gegevens uit te voeren. Voor meer informatie, zie de [ steekproefvragen voor anonieme blokdocumentatie ](../../query-service/key-concepts/anonymous-block.md). |
| Datasetorganisatie | Verstrekt een coherente, logische gegevensstructuur om uw gegevensactiva voor gebruik met de Dienst van de Vraag te organiseren aangezien de hoeveelheid gegevensactiva binnen de zandbak groeit. Voor meer informatie, zie [ de documentatie van gegevensactiva organiseren ](../../query-service/best-practices/organize-data-assets.md). |

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Experience Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface van sandboxen | De sandboxindicator is nu geïntegreerd in de header voor alle Experience Platform UI-toepassingen. De sandboxindicator geeft de naam, het gebied en het type van de sandbox weer en geeft u ook toegang tot een vervolgkeuzemenu om tussen de sandboxen te schakelen. Voor meer informatie, zie de [ gids UI van de zandbak ](../../sandboxes/ui/user-guide.md). |

Voor meer informatie over zandbakken, te zien gelieve het [ overzicht van zandbakken ](../../sandboxes/home.md).

## Segmentatieservice {#segmentation}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Segmentovereenkomst | Segment Match is een service voor gegevenssamenwerking waarmee twee of meer Experience Platform-gebruikers gegevens kunnen uitwisselen op basis van gemeenschappelijke id&#39;s op een veilige, beheerde en privacyvriendelijke manier. Segmentovereenkomst maakt gebruik van Experience Platform-privacystandaarden en persoonlijke id&#39;s, zoals gehashte e-mails, gehashte telefoonnummers en apparaat-id&#39;s, zoals IDFA&#39;s en GAID&#39;s. Voor meer informatie, zie het [ overzicht van de Gelijke van het Segment ](../../segmentation/ui/segment-match/overview.md). |

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

| Functie | Beschrijving |
| --- | --- |
| Beta-bronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] bronverbeteringen | De [!DNL Event Hubs] -bron ondersteunt nu niet-root SAS-sleuteltype verificatie voor het maken van verbinding en het maken van bronverbinding. Voor meer informatie, zie het [[!DNL Event Hubs]  overzicht ](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] bronverbeteringen | Met de [!DNL SFTP] -bron kunt u nu een ingesteld aantal maximale gelijktijdige verbindingen instellen die een gegevensstroom kan gebruiken om verbinding te maken met de SFTP-server. Voor meer informatie, zie het [[!DNL SFTP]  overzicht ](../../sources/connectors/cloud-storage/sftp.md). |
