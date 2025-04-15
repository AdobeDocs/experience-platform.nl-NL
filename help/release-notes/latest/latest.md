---
title: Aanvullende informatie van maart 2025 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f0879683629ba10ed1b799e52f0adf332f079daf
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 100%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:26 maart 2025**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [Aanvullende informatie voor Adobe Experience Platform](#adobe-experience-platform-release-notes)

   - [Dashboards](#dashboards)
   - [Bestemmingen](#destinations)
   - [Samenstelling van Federated-doelgroep](#federated-audience-composition)
   - [Segmentatieservice](#segmentation-service)
   - [Bronnen](#sources)

## Dashboards {#dashboards}

Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten krijgt in de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnames.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Dashboard voor licentiegebruik op basis van metrics | Het dashboard voor licentiegebruik bevat nu een gestroomlijnde gebruikersinterface met twee tabbladen: **Metrics** en **Producten**. Het nieuwe tabblad **Metrics** biedt een geconsolideerd overzicht van alle traceerbare licentiegegevens voor uw gekochte producten. Elke indicator bevat een inline-infopictogram met beschrijvingen en bijbehorende producten. Gebruikers kunnen productie- of ontwikkelingssandboxes selecteren, historische gebruikstrends bekijken in interactieve grafieken en sandboxspecifieke gegevens exporteren als CSV-bestanden. Deze updates stroomlijnen het bijhouden van licenties en bieden duidelijker inzicht. Meer informatie vindt u in de [handleiding van het dashboard voor licentiegebruik](../../dashboards/guides/license-usage.md). |
| Bijgewerkte voorspellingsfrequentie | Het dashboard voor licentiegebruik biedt nu nauwkeuriger inzicht in het verwachte verbruik door de gebruiksvoorspellingen **wekelijks** bij te werken in plaats van maandelijks. Deze voorspellingen tonen het geschatte gebruik voor de komende zes weken op basis van recente trends. Deze wijziging zorgt voor snellere besluitvorming, eerder ingrijpen en betere licentieplanning. Zie de [handleiding van het dashboard voor licentiegebruik](../../dashboards/guides/license-usage.md#predicted-usage) voor meer informatie. |
| Bijgewerkte beschrijvingen van metrics in de gebruikersinterface | De definities van metrics in het dashboard voor licentiegebruik zijn herzien voor duidelijkheid en consistentie. U kunt nu bijgewerkte beschrijvingen rechtstreeks in het dashboard bekijken met behulp van inline-infopictogrammen naast elke indicator op het tabblad **Metrics**. Dankzij deze updates wordt het begrijpelijker hoe metrics worden bijgehouden en voor welke producten ze gelden. Zie de [handleiding van het dashboard voor licentiegebruik](../../dashboards/guides/license-usage.md#available-metrics) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [Demandbase People-verbinding](/help/destinations/catalog/advertising/demandbase-people.md) | Gebruik de [!DNL Demandbase People]-verbinding om profielen voor uw Demandbase-campagnes te activeren voor doelgroeptargeting, personalisatie en onderdrukking. |
| [Bombora-accountverbinding](/help/destinations/catalog/advertising/bombora.md) | Gebruik de [!DNL Bombora]-verbinding om profielen voor uw Bombora-campagnes te activeren voor doelgroeptargeting, personalisatie en onderdrukking, op basis van [accountdoelgroepen](/help/segmentation/types/account-audiences.md). |
| [Airship Attributes](/help/destinations/catalog/mobile-engagement/airship-attributes.md)-upgrade | Vanaf 25 maart 2025 kunt u twee **[!UICONTROL Airship Attributes]**-kaarten naast elkaar zien in de bestemmingencatalogus. Dit komt door een interne upgrade van de bestemmingsservice. De naam van de bestaande bestemmingsconnector **[!UICONTROL Airship Attributes]** is gewijzigd in **[!UICONTROL (Deprecated) Airship Attributes]** en er is nu een nieuwe kaart met de naam **[!UICONTROL Airship Attributes]** voor u beschikbaar. <br> Gebruik de **[!UICONTROL Airship Attributes]**-verbinding in de catalogus voor nieuwe activeringsgegevensstromen. Als u actieve gegevensstromen naar de bestemming [!DNL (Deprecated) Airship Attributes] hebt, worden deze automatisch bijgewerkt. U hoeft dus niets te doen. <br> Als u gegevensstromen maakt via de [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] bijwerken naar de volgende waarden: <ul><li> Stroomspecificatie-ID: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> Verbindingsspecificatie-ID: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| [Verbeterde rapportagenauwkeurigheid voor streamingbestemmingen](../../dataflows/ui/monitor-destinations.md) | Vanaf maart 2025 brengt Adobe een update uit om de rapportagenauwkeurigheid voor streamingbestemmingen te verbeteren. Deze verbetering zorgt voor een betere afstemming tussen het Experience Platform en de rapportage van de bestemmingsplatforms. <br> Vóór deze update werden alle activeringspogingen in **[!UICONTROL Identities failed]** opgenomen. Na deze update wordt alleen de laatste activeringspoging opgenomen in het totale aantal. <br> Deze verbetering geldt voor alle streamingbestemmingen. <br> Na deze verbetering kunnen gebruikers van streamingbestemmingen een daling in hun **[!UICONTROL Identities failed]**-aantal verwachten. |
| [Ondersteuning voor het exporteren van kaartvelden voor ondernemings- en Edge-bestemmingen](/help/destinations/ui/export-arrays-maps-objects.md) | Bij het exporteren van gegevens naar de bestemmingen [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) en [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) kunt u nu kaartvelden selecteren voor export in de toewijzingsstap van de activeringsworkflow. <br> ![Exporteer een kaartveld naar de ondernemingsbestemming.](../2025/assets/march/export-map.png "Exporteer kaartveld naar ondernemingsbestemming."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Samenstelling van Federated-doelgroep {#federated-audience-composition}

Voor informatie over de recentste updates voor Samenstelling van Federated-doelgroepen, raadpleegt u hier de [ specifieke aanvullende informatie](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen in Account Audience Builder | In Audience Builder kunt u nu filteren op kenmerken, zodat alleen de ingevulde kenmerken worden weergegeven. Ook kunt u samenvattingsgegevens voor deze ingevulde kenmerken bekijken. Meer informatie over deze verbeteringen vindt u in de documentatie van [Audience Builder](../../rtcdp/segmentation/audience-builder.md). |
| Flexibele publieksevaluatie algemene beschikbaarheid | De flexibele publieksevaluatie is nu algemeen beschikbaar. Met flexibele doelgroepevaluatie kunt u op aanvraag nieuwe doelgroepen creëren voor tijdgevoelige communicatie. Meer informatie over flexibele publieksevaluatie vindt u in het [overzicht flexibele publieksevaluatie](../../segmentation/methods/flexible-audience-evaluation.md). |

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Nieuwe bronnen**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Bombora Intent] | De bron [!DNL Bombora Intent] is nu beschikbaar in de bronnencatalogus. Gebruik deze bron voor het volgende: <ul><li>Bombora Company Surge Intent-gegevens integreren om accounts te identificeren die actief onderzoek doen naar uw producten of diensten.</li><li>Prioriteit geven aan accounts binnen de markt, zodat u nauwkeurige segmenten kunt maken en zeer gerichte ABM-campagnes kunt uitvoeren. Zo zorgt u ervoor dat uw marketingactiviteiten zich richten op de accounts die de grootste kans op conversie bieden.</li><li>Inzet van intentiegedreven strategieën om advertentie-uitgaven te optimaliseren, betrokkenheid te vergroten en ROI te maximaliseren.</li></ul> Voor meer informatie kunt u de handleiding lezen over het [koppelen van uw  [!DNL Bombora] account aan Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | De bron [!DNL Demandbase Intent] is nu beschikbaar in de bronnencatalogus. Gebruik deze bron voor het volgende: <ul><li>Integreer de Account Intent-gegevens van Demandbase om accounts met hoge interesse te identificeren op basis van realtimebetrokkenheid.</li><li>Door prioriteit te geven aan de sterkste intentiesignalen kunt u nauwkeurige segmenten maken en zeer gerichte campagnes uitvoeren. Zo weet u zeker dat uw marketingactiviteiten zich richten op accounts die de grootste kans op conversie bieden.</li><li>Intentiegestuurde strategieën activeren om advertentie-uitgaven te optimaliseren, de betrokkenheid te vergroten en het rendement op uw investering te verhogen.</li></ul> Voor meer informatie kunt u de handleiding lezen over het [koppelen van uw  [!DNL Demandbase] account aan Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen aan de bron [!DNL Google Ads] | U kunt nu de [[!DNL Google Ads] bron](../../sources/connectors/advertising/ads.md) gebruiken om geaggregeerde gegevens op te nemen. U kunt [!DNL Google Ads Query Builder] gebruiken om de kenmerken, segmenten en bronnen op te geven die u wilt opnemen in Experience Platform. Voor meer informatie kunt u de handleiding lezen over het [koppelen van uw  [!DNL Google Ads] account aan Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md). |
| Verbeteringen aan de [!DNL Microsoft Dynamics]-bron | U kunt nu de primaire sleutel van een bepaalde [!DNL Microsoft Dynamics]-tabel opgeven wanneer u de inhoud en structuur van uw gegevens verkent. Gebruik deze functie om uw zoekopdrachten met de [!DNL Microsoft Dynamics]-bron te optimaliseren. Voor meer informatie kunt u de handleiding over het [koppelen van uw [!DNL Microsoft Dynamics] bron met Experience Platform via de API](../../sources/tutorials/api/create/crm/ms-dynamics.md) raadplegen. |
| Ondersteuning voor API-sleutelauthenticatie in Self-Serve Sources (Batch SDK) | U kunt nu API-sleutelauthenticatie gebruiken als verificatietype bij het integreren van een nieuwe bron met Self-Serve Sources (Batch SDK). Voor meer informatie kunt u de handleiding [over het configureren van uw verificatiespecificatie in Batch SDK](../../sources/sources-sdk/config/authspec.md) raadplegen. |
| Ondersteuning voor op kenmerken gebaseerde toegangscontrole in bronnen | U kunt nu op kenmerken gebaseerde toegangscontrolefuncties gebruiken voor uw brongegevensstromen. Raadpleeg de volgende handleidingen voor meer informatie: <ul><li>[Labels toepassen op uw brongegevensstromen met behulp van de API](../../sources/tutorials/api/labels.md)</li><li>[Pas labels toe op uw brongegevensstromen met behulp van de gebruikersinterface](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).
