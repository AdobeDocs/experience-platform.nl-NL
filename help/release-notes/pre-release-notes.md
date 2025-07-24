---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 7e91181f71b84fdaf04a39e003cbbd415827e282
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 22%

---

# Opmerkingen bij de release Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is voorgenomen als a **voorproef** van de versienota&#39;s voor de huidige maand. Release-items kunnen worden gewijzigd en worden toegevoegd of verwijderd in de definitieve versie.

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/nl/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 29 juli 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Bestemmingen](#destinations)
- [Gegevensopname](#ingestion)
- [Query-service](#query-service)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Consolidatie van Marketo-doelkaarten | Marketo V2 en Marketo Engage Person Sync bestemmingskaarten zijn geconsolideerd in één, verenigde doelkaart. Deze consolidatie vereenvoudigt het proces van de bestemmingsselectie en verstrekt een meer gestroomlijnde ervaring voor de integratie van Marketo. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde gegevensstroominformatie voor Edge-doelen | De verbeterde juiste spoorinformatie voor bestemmingen Adobe Target en van de Douane Personalization toont nu de gegevensstroomnaam, die duidelijkere zichtbaarheid in bijbehorende configuraties van de gegevensstroom verstrekt en verwarring vermindert wanneer het herzien van bestaande gegevensstromen. De **[!UICONTROL Datastream ID]** -kiezer in het doelconfiguratiescherm is bijgewerkt naar **[!UICONTROL Datastream]** voor meer duidelijkheid in de gebruikersinterface. |
| Zichtbaarheid van marketingacties in doelselectie | Marketingacties worden nu weergegeven in de rechtertrack van het doeltabblad **[!UICONTROL Browse]** en op de pagina **[!UICONTROL Dataflow runs]** , zodat wijzigingen in marketingacties direct zichtbaar zijn zonder dat navigatie naar de weergavepagina is vereist. Deze verbetering verbetert de gebruikerservaring door het gemakkelijker te maken om marketing actieconfiguraties tijdens bestemmingsopstelling te verifiëren. |
| (Beperkte bètaversie) Marketing-acties voor doelen bewerken | U kunt nu marketingacties voor bestaande doelen bewerken. Deze functionaliteit is in beperkte bèta. Neem contact op met uw Adobe-vertegenwoordiger als u toegang tot de site wilt aanvragen. |
| (Beperkte bètaversie) Doelen bewerken | U kunt de doelconfiguratie nu bewerken nadat u deze hebt gemaakt. Deze functionaliteit is in beperkte bèta. Neem contact op met uw Adobe-vertegenwoordiger als u toegang tot de site wilt aanvragen. |
| Accountnamen en beschrijvingen voor doelverbindingen | U kunt nu accountnamen en beschrijvingen toevoegen wanneer u verbinding maakt met doelen, waardoor u beter beheer van doelen met meerdere accounts kunt maken. |

**Oplossingen**

| Probleem | Beschrijving |
| --- | --- |
| Functionaliteit voor schuiven in categorieën | Probleem verholpen waarbij het categorieszijmenu in de catalogus met doelen en bronnen niet goed door de muis werd geschoven, wat de navigatiebruikbaarheid voor gebruikers die door doelcategorieën bladeren, verbeterde. |

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Gegevensopname {#ingestion}

Experience Platform biedt een uitgebreid raamwerk voor gegevensinvoer dat zowel batch- als streaming gegevensinvoer uit verschillende bronnen ondersteunt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor het controleren van het opnemen van streaming-profielen | Controle in real time voor het stromen van profielopname is nu beschikbaar, die transparantie in productie, latentie, en de metriek van de gegevenskwaliteit verstrekt. Dit steunt pro-actieve alarmering en actionable inzichten om gegevensingenieurs te helpen capaciteitsschendingen en inspraakkwesties identificeren. |

Voor meer informatie, lees het [ overzicht van de gegevensopname ](../ingestion/home.md).

## Query-service {#query-service}

Adobe Experience Platform Query Service biedt een robuuste SQL-interface voor gegevensanalyse en -exploratie op het hele platform.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterd sessiebeheer | Data Distiller bevat nu verbeterde mogelijkheden voor sessiebeheer, die betere controle bieden over gebruikerssessies en verbeterde prestatietoezicht in ontwikkelings- en productieomgevingen. |
| Ondersteuning voor niet-verlopen tekenbeperkingen voor het wachtwoord voor referenties. | Data Distiller biedt nu ondersteuning voor niet-verlopen referenties met specifieke tekenbeperkingen. Wachtwoorden vereisen minstens één getal, één kleine letter, één hoofdletter en één speciaal teken, maar het dollarteken ($) wordt niet ondersteund. Aanbevolen speciale tekens zijn onder andere `!, @, #, ^, or &` . |
| Verbeterde prestatiesconsistentie over milieu&#39;s | Distiller-prestaties van gegevens zijn nu consistent tussen ontwikkelings- en productiesandboxen, met vergelijkbare back-endbronnen in beide omgevingen. De verbruikte computeruren kunnen variëren op basis van het gegevensvolume en de beschikbare back-end computerbronnen tijdens de verwerking. |

Voor meer informatie, lees het [ overzicht van de Dienst van de Vraag ](../query-service/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B edition biedt uitgebreide B2B-mogelijkheden voor klantgegevensbeheer, waardoor organisaties uniforme klantprofielen kunnen maken, een geavanceerd B2B-publiek kunnen maken en gegevens op verschillende marketingkanalen kunnen activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| B2B-architectuurupgrade | Experience Platform werkt aan een upgrade naar een nieuwe B2B-architectuur die aanzienlijke verbeteringen doorvoert voor het publiek met meerdere entiteiten met B2B-kenmerken. Deze upgrade consolideert de ondersteuning voor samenvoegbeleid, verbetert de nauwkeurigheid van het aantal gebruikers en verbetert de mogelijkheden voor het oplossen van entiteiten. |
| Consolidatie van het beleid voor meerdere soorten publiek samenvoegen | Het publiek met meerdere entiteiten met B2B-kenmerken ondersteunt nu slechts één enkel samenvoegingsbeleid — het standaardsamenvoegbeleid — in plaats van het ondersteunen van meerdere samenvoegingsbeleidsregels. Deze verandering verzekert verenigbare publiekssamenstelling en vereenvoudigt het beheer van de fusielogica. |
| Updates voor beperkingen voor het accountpubliek | Accountgebruikers hebben niet langer de vorige beperkingen van een terugzoekvenster van 30 dagen voor Experience Events, beperkingen van aangepaste entiteiten of beperkingen bij het gebruik van `inSegment` -gebeurtenissen. Deze updates bieden meer flexibiliteit bij het maken van complexe B2B-publieksdefinities. |
| Verbeterde publiekscijfers voor B2B-entiteiten | De schattingen van de omvang van het publiek voor soorten publiek met B2B-entiteiten zoals Accounts en Opportunity zijn nu precies, gebaseerd op de resultaten van realtime segmentatie. Deze verbetering levert nauwkeurigere en betrouwbaardere schattingen op voor het publiek dat complexe B2B-relaties omvat. |
| Momentopnamen van account voor publieksleden | De details van het publiek van het lidmaatschap van de Publiek zijn nu inbegrepen voor de entiteiten van de Rekening in momentopname uitvoer, toelatend toegang tot account-vlakke publieksstatus, timestamps, en lidmaatschapsindicatoren. Dit brengt eigenschappariteit tussen Profiel (Persoon) en de segmentatiemodellen van de Rekening. |
| Wijzigingen in het gereedschap Sandbox voor gebruikers met meerdere entiteiten | Het importeren van publiek met meerdere entiteiten met B2B-entiteiten en Experience Events die vóór de migratie zijn geëxporteerd, wordt niet meer ondersteund. Deze doelgroepen kunnen niet automatisch worden geconverteerd naar de nieuwe architectuur en kunnen niet worden gevalideerd bij het importeren. Soorten publiek moet na migratie opnieuw worden geëxporteerd voordat het kan worden geïmporteerd in doelsandboxen. |
| B2B Entiteit API-afschriften | Het publiek wordt nu afgekeurd via API voor B2B-entiteiten (Account, Opportunity, Account-Person Relation, Opportunity-Person Relation, Campaign, Campaign Member, Marketing List en Marketing List Member). Bovendien zijn de opzoekings- en verwijderingsbewerkingen van de API voor profieltoegang voor deze B2B-entiteiten ook afgekeurd. |
| Updates van naamruimte voor entiteit oplossen | Account en Opportunity-entiteiten gebruiken nu op tijd gebaseerde samenvoeging met specifieke naamruimten (`b2b_account` voor account, `b2b_opportunity` voor opportunity). Alle andere entiteiten zijn verenigd met primaire identiteitsoverlappingen die worden samengevoegd met samenvoeging op basis van tijdprioriteit. |

Voor meer informatie, lees het [ overzicht van B2B edition van Real-Time CDP ](../rtcdp/b2b-overview.md).

## Sandboxes {#sandboxes}

Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijzigingen in de import van meerdere personen | Sandbox tooling is bijgewerkt om de nieuwe B2B architectuurverbetering te steunen. Meerdere entiteiten die B2B-entiteiten en Experience Events bevatten, moeten na de architectuurupgrade opnieuw worden geëxporteerd voordat ze via sandboxgereedschappen naar doelsandboxen kunnen worden geïmporteerd. Het importeren van pre-upgradeversies zal mislukken. |

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| API voor extern publiek | Met de API voor extern publiek kunt u extern gegenereerde soorten publiek programmatisch importeren in Adobe Experience Platform. |

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe bronnen**

| Source | Beschrijving |
| --- | --- |
| Ondersteuning voor [!DNL Didomi] (Streaming SDK) | Met de [!DNL Didomi] -bronaansluiting kunt u gegevens voor het beheer van toestemmingen invoeren vanaf het platform van [!DNL Didomi] , zodat u de privacyregels en op toestemming gebaseerde marketingstrategieën kunt naleven. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het vastleggen van wijzigingsgegevens in bepaalde bronnen | U kunt nu gegevensstromen tot stand brengen die veranderingsgegevens toelaten vangen voor stijgende opname gebruikend bronschakelaars. Met deze functie kunnen klanten het gegevenstype wijzigen voor incrementele inname, waardoor de gegevensversheid toeneemt en de verwerkingsoverhead afneemt. |
| Ondersteuning voor zachte verwijdering van records in [!DNL Salesforce] | De [!DNL Salesforce] -bron ondersteunt nu het opnemen van schermverwijderde records via een optionele `includeDeletedObjects` -parameter. Wanneer deze waarde is ingesteld op true, kunnen klanten geneste verwijderde records opnemen in hun [!DNL Salesforce] query&#39;s en deze records naar Experience Platform overbrengen. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).
