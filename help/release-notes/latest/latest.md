---
title: Aanvullende informatie van juli 2025 voor Adobe Experience Platform
description: Aanvullende informatie van juli 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 2a8d5576ea937cdda70f10218b5eec35613fd264
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 24%

---


# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 29 juli 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Capaciteit](#capacity)
- [Bestemmingen](#destinations)
- [Gegevensopname](#data-ingestion)
- [ Dienst van de Vraag ] (#query-dienst
- [Real-Time CDP B2B Edition](#b2b)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Capaciteit {#capacity}

>[!AVAILABILITY]
>
>Deze functie is afhankelijk van uw regio beschikbaar voor gebruik. Voor gebruikers in Amerika, zal dit vanaf 11 augustus beschikbaar zijn. Voor gebruikers in Europa zal dit vanaf 25 augustus beschikbaar zijn. Voor gebruikers in Azië is deze vanaf 8 september beschikbaar.

De capaciteit verstrekt een uitvoerige mening van 0&rbrace; begeleidingen van uw organisatie [ en geeft aanbevelingen op hoe te om potentiële capaciteitsschendingen op te lossen door uw capaciteiten op een zandbakniveau toe te wijzen. ](../../rtcdp/guardrails/overview.md) Met deze release kunt u uw capaciteit voor zowel streaming opname als streaming segmentatie bekijken.

Voor meer informatie, te lezen gelieve het [ overzicht van de Capaciteit ](../../landing/license-usage-and-guardrails/capacity.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Beperkte beschikbaarheid van de [ Klantovereenkomst van Google + Vertoning &amp; Video 360 ](/help/destinations/catalog/advertising/google-customer-match-dv360.md) verbinding | Nadat Adobe in juni kort beschikbaar was voor alle klanten, heeft het deze integratie teruggegeven aan beperkte beschikbaarheid. Momenteel is de toegang tot deze bestemming beperkt tot klanten die al zijn ingeschakeld, terwijl Adobe en Google werken aan het oplossen van implementatieproblemen. Als u geïnteresseerd bent in deze integratie wanneer de bredere rollout wordt hervat, neemt u contact op met uw Adobe-vertegenwoordiger om uw intentie uit te drukken. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Accountnamen en beschrijvingen voor doelverbindingen | U kunt [ rekeningsnamen en beschrijvingen ](/help/destinations/ui/connect-destination.md) nu toevoegen wanneer het verbinden met bestemmingen, toelatend beter beheer van bestemmingen met veelvoudige rekeningen. |
| Verbeterde gegevensstroominformatie voor Edge-doelen | De recht-spoorinformatie voor [ Adobe Target ](/help/destinations/catalog/personalization/adobe-target-v2.md) en [ de bestemmingen van de Douane Personalization ](/help/destinations/catalog/personalization/custom-personalization.md) is verbeterd om de gegevensstroomnaam te tonen, die duidelijkere zichtbaarheid in bijbehorende configuraties aanbieden datastream en die verwarring helpen verminderen wanneer het herzien van bestaande dataflows. De **[!UICONTROL Datastream ID]** -kiezer in het doelconfiguratiescherm is bijgewerkt naar **[!UICONTROL Datastream]** voor meer duidelijkheid in de gebruikersinterface. |
| Zichtbaarheid van marketingacties in doelselectie | Marketingacties worden nu weergegeven in de rechtertrack van het tabblad **[[!UICONTROL Browse]](/help/destinations/ui/destinations-workspace.md#browse)** in de werkruimte Doelen en op de pagina **[[!UICONTROL Dataflow runs]](/help/dataflows/ui/monitor-destinations.md)** , zodat wijzigingen in marketingacties direct zichtbaar zijn zonder dat u naar de weergavepagina hoeft te navigeren. Deze verbetering verbetert de gebruikerservaring door het gemakkelijker te maken om marketing actieconfiguraties tijdens bestemmingsopstelling te verifiëren. |
| [!BADGE &#x200B; Beperkte bèta &#x200B;]{type=Informative} geeft marketing acties voor bestemmingen uit | U kunt [ marketing acties ](/help/destinations/ui/edit-activation.md#edit-marketing-actions) voor bestaande bestemmingen nu uitgeven. Deze functie is momenteel in beperkte bèta. Neem contact op met uw Adobe-vertegenwoordiger om toegang aan te vragen. |
| [!BADGE &#x200B; Beperkte bèta &#x200B;]{type=Informative} geeft bestemmingen uit | U kunt [ uw bestemmingsconfiguratie ](/help/destinations/ui/edit-destination.md) nu uitgeven nadat het is gecreeerd. Deze functie is momenteel in beperkte bèta. Neem contact op met uw Adobe-vertegenwoordiger om toegang aan te vragen. |

**Oplossingen**

| Probleem | Beschrijving |
| --- | --- |
| Functionaliteit voor schuiven in categorieën | Probleem verholpen waarbij het categorieszijmenu in de catalogus met doelen en bronnen niet goed door de muis werd geschoven, wat de navigatiebruikbaarheid voor gebruikers die door doelcategorieën bladeren, verbeterde. |

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Gegevensopname {#ingestion}

Experience Platform biedt een uitgebreid raamwerk voor gegevensinvoer dat zowel batch- als streaming gegevensinvoer uit verschillende bronnen ondersteunt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor het controleren van het opnemen van streaming-profielen | Controle in real time voor het stromen van profielopname is nu beschikbaar, die transparantie in productie, latentie, en de metriek van de gegevenskwaliteit verstrekt. Dit steunt pro-actieve alarmering en actionable inzichten om gegevensingenieurs te helpen capaciteitsschendingen en inspraakkwesties identificeren. Lees de gids bij [ controle het stromen profielopname ](../../dataflows/ui/monitor-streaming-profile.md) voor meer informatie. |

Voor meer informatie, lees het [ overzicht van de gegevensopname ](../../ingestion/home.md).

## Query-service {#query-service}

Voer query&#39;s uit op gegevens in het Adobe Experience Platform-data lake met behulp van standaard SQL met Query Service. Combineer naadloos datasets en genereer nieuwe op basis van de queryresultaten om rapportage, datawetenschapworkflows of opname in het realtimeklantprofiel mogelijk te maken. U kunt bijvoorbeeld de gegevens van de klantentransactie samenvoegen met de gedragsgegevens om hoogwaardige doelgroepen te identificeren voor gerichte marketingcampagnes.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
|--------|-------------|
| Ondersteuning voor niet-verlopen tekenbeperkingen voor het wachtwoord voor referenties. | Distiller van gegevens steunt nu [ niet-vervallende geloofsbrieven met specifieke karakterbeperkingen ](../../query-service/ui/credentials.md#non-expiring-credentials). Wachtwoorden vereisen minstens één getal, één kleine letter, één hoofdletter en één speciaal teken, maar het dollarteken ($) wordt niet ondersteund. Aanbevolen speciale tekens zijn onder andere `!, @, #, ^, or &` . |
| Verbeterde prestatiesconsistentie over milieu&#39;s | De prestaties van Distiller van gegevens [ zijn nu verenigbaar tussen ontwikkeling en productiestanddozen ](../../query-service/troubleshooting-guide.md#data-distiller), met gelijkaardige achterste middelen beschikbaar in beide milieu&#39;s. De verbruikte computeruren kunnen variëren op basis van het gegevensvolume en de beschikbare back-end computerbronnen op het moment van verwerking. |

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../../query-service/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B edition biedt uitgebreide B2B-mogelijkheden voor klantgegevensbeheer, waardoor organisaties uniforme klantprofielen kunnen maken, een geavanceerd B2B-publiek kunnen maken en gegevens op verschillende marketingkanalen kunnen activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| B2B-architectuurupgrade | Experience Platform werkt aan een upgrade naar een nieuwe B2B-architectuur die aanzienlijke verbeteringen doorvoert voor het publiek met meerdere entiteiten met B2B-kenmerken. Deze upgrade consolideert de ondersteuning voor samenvoegbeleid, verbetert de nauwkeurigheid van het aantal gebruikers en verbetert de mogelijkheden voor het oplossen van entiteiten. Lees het [ overzicht van de de architectuurverbetering van Real-Time CDP B2B edition ](../../rtcdp/b2b-architecture-upgrade.md) voor een uitvoerige uitsplitsing van de veranderingen. |
| Beleidsconsolidatie samenvoegen voor het publiek met meerdere entiteiten | Het publiek met meerdere entiteiten met B2B-kenmerken ondersteunt nu slechts één enkel samenvoegingsbeleid — het standaardsamenvoegbeleid — in plaats van het ondersteunen van meerdere samenvoegingsbeleidsregels. Deze verandering verzekert verenigbare publiekssamenstelling en vereenvoudigt het beheer van de fusielogica. Voor meer informatie, lees het [ overzicht van het samenvoegingsbeleid ](../../profile/merge-policies/overview.md). |
| Verbeterde publiekscijfers voor B2B-entiteiten | De schattingen van de omvang van het publiek voor soorten publiek met B2B-entiteiten zoals Accounts en Opportunity zijn nu precies, gebaseerd op de resultaten van realtime segmentatie. Deze verbetering levert nauwkeurigere en betrouwbaardere schattingen op voor het publiek dat complexe B2B-relaties omvat. |
| Momentopnamen van account voor publieksleden | De details van het publiek van het lidmaatschap van de Publiek zijn nu inbegrepen voor de entiteiten van de Rekening in momentopname uitvoer, toelatend toegang tot account-vlakke publieksstatus, timestamps, en lidmaatschapsindicatoren. Dit brengt eigenschappariteit tussen Profiel (Persoon) en de segmentatiemodellen van de Rekening. |
| Wijzigingen in het gereedschap Sandbox voor gebruikers met meerdere entiteiten | Het importeren van publiek met meerdere entiteiten met B2B-entiteiten en Experience Events die vóór de migratie zijn geëxporteerd, wordt niet meer ondersteund. Deze doelgroepen kunnen niet automatisch worden geconverteerd naar de nieuwe architectuur en kunnen niet worden gevalideerd bij het importeren. Soorten publiek moet na migratie opnieuw worden geëxporteerd voordat het kan worden geïmporteerd in doelsandboxen. Voor meer informatie, leest de [ gids over voorwerpen die voor zandbak tooling ](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) worden gesteund. |
| B2B-entiteit API-afwaarderingen | [!DNL Profile Access] API opzoekbewerkingen voor B2B-entiteiten (Account-Person Relation, Opportunity Person-Relation, Campaign, Campaign Member, Marketing List en Marketing List Member) zijn nu afgekeurd. Daarnaast zijn API-verwijderingsbewerkingen voor B2B-entiteiten (Account, Account-Person Relatie, Opportunity, Opportunity Person-Relation, Campagne, Campagne Member, Marketing List en Marketing List members) ook afgekeurd. [!DNL Profile Access] Voor meer informatie, lees de [ gids van het entiteiteneindpunt API ](../../profile/api/entities.md). |
| Updates van naamruimte voor entiteit oplossen | Account en Opportunity-entiteiten gebruiken nu op tijd gebaseerde samenvoeging met specifieke naamruimten (`b2b_account` voor account, `b2b_opportunity` voor opportunity). Alle andere entiteiten zijn verenigd met primaire identiteitsoverlappingen die worden samengevoegd met samenvoeging op basis van tijdprioriteit. Voor meer informatie over entiteitresolutie, lees de [ gids van het entiteitseindpunt API ](../../profile/api/entities.md). |

Voor meer informatie, lees het [ overzicht van B2B edition van Real-Time CDP ](../../rtcdp/b2b-overview.md).

## Sandboxes {#sandboxes}

Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijzigingen in de import van meerdere personen | Sandbox tooling is bijgewerkt om de nieuwe B2B architectuurverbetering te steunen. Meerdere entiteiten die B2B-entiteiten en Experience Events bevatten, moeten na de architectuurupgrade opnieuw worden geëxporteerd voordat ze via sandboxgereedschappen naar doelsandboxen kunnen worden geïmporteerd. Het importeren van pre-upgradeversies zal mislukken. Voor meer informatie, leest de [ gids over voorwerpen die voor zandbak tooling ](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) worden gesteund. |

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| API voor extern publiek | Met de API voor extern publiek kunt u extern gegenereerde soorten publiek programmatisch importeren in Adobe Experience Platform. Voor meer informatie, te lezen gelieve de [ externe gids van het publiekseindpunt ](../../segmentation/api/external-audiences.md). |

Voor meer informatie over segmentatie, lees het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md)

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe bronnen**

| Source | Beschrijving |
| --- | --- |
| Ondersteuning voor [!DNL Didomi] (Streaming SDK) | Gebruik de [!DNL Didomi] -bron om gegevens van toestemmings- en voorkeursbeheer van [!DNL Didomi] in te voeren, die de naleving van privacyregels en op toestemming gebaseerde marketingstrategieën ondersteunen. Lees het [[!DNL Didomi]  bronoverzicht ](../../sources/connectors/consent-and-preferences/didomi.md) voor informatie over hoe te om opstelling te krijgen. Voor stappen bij het creëren van een bronverbinding, lees de [[!DNL Didomi]  gids van de bronverbinding ](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md). |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het vastleggen van wijzigingsgegevens in bepaalde bronnen met de API van [!DNL Flow Service] | U kunt nu gegevensstromen tot stand brengen die veranderingsgegevens toelaten vangen voor stijgende opname gebruikend bronschakelaars. Met deze functie kunnen klanten het gegevenstype wijzigen voor incrementele inname, waardoor de gegevensversheid toeneemt en de verwerkingsoverhead afneemt. Voor meer informatie, lees de documentatie over [ gebruikend veranderingsgegevens vangen voor bronnen ](../../sources/tutorials/api/change-data-capture.md) |
| Ondersteuning voor zachte verwijdering van records in [!DNL Salesforce] | De [!DNL Salesforce] -bron ondersteunt nu het opnemen van schermverwijderde records via een optionele `includeDeletedObjects` -parameter. Wanneer deze waarde is ingesteld op true, kunnen klanten geneste verwijderde records opnemen in hun [!DNL Salesforce] query&#39;s en deze records naar Experience Platform overbrengen. Lees de [[!DNL Salesforce]  brondocumentatie ](../../sources/connectors/crm/salesforce.md) voor meer informatie. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).