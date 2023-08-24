---
title: Aanvullende informatie over Adobe Experience Platform
description: De release van augustus 2023 bevat opmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 5c1566bac20f7fb83a0ce48c4fe7a22e15dbeb37
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 23 augustus 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Real-Time Customer Data Platform](#rtcdp)
- [Toegangsbeheer op basis van kenmerken](#abac)
- [Dashboards](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Gegevensopname](#data-ingestion)
- [Gegevensvoorbereiding](#data-prep)
- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Gebouwd op Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen met intelligente besluitvorming door de klantenreis te activeren.

[!DNL Real-Time CDP] combineert veelvoudige bronnen van ondernemingsgegevens om klantenprofielen in real time tot stand te brengen. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Intelligente handleiding voor hergebruik | De [Intelligente re-engagement](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) de handleiding van het gebruiksgeval verstrekt details over hoe te om klant opnieuw in dienst te nemen die een omzetting alvorens het op een intelligente en verantwoordelijke manier hebben verlaten te voltooien. Deze gids gebruikt de volgende voorbeeldreizen om klanten opnieuw in dienst te nemen: <ul><li>Reizigersreis: gericht op klanten die het bladeren van producten hebben verlaten.</li><li>Verlaten winkelwagentje - Klanten die producten in het winkelwagentje hebben geplaatst maar de aankoop nog niet hebben voltooid.</li><li>Reis voor bevestiging van bestelling - Gericht op aankopen van producten</li></ul> Gebruik de link Gedetailleerde feedbackopties onder aan het dialoogvenster [Intelligente handleiding voor hergebruik](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) om feedback te geven. |
| Ondersteuning van partnergegevens | Voer upper-funnel marketing in Real-Time CDP, met partner-gesourceerde perspectiefprofielen en partner IDs uit om nieuwe klanten te bereiken en uw eerste-partijgegevens te verrijken: <ul><li>Aanschaf en adresseerbaarheid van de klant: gebruik van cokieless identifiers en hashed PII van gegevenspartners van keuze om nieuwe klanten te bereiken en de afhankelijkheid van cookies van derden te verminderen.</li><li>Volledige kanaalmarketing in één enkel systeem: Zelf-serversegmentatie, publiekscorrectie, en inheemse activering voor toekomstige en bekende klanten in één enkel systeem.</li><li>Stichting van vertrouwen: De gegevens en de profielen van de partner van de regering met geoctrooieerd gegevensgebruik, etikettering, toegangscontroles, en meer aan markt verantwoordelijk. Lees de volgende handleidingen voor het gebruik van hoofdletters en kleine letters voor meer informatie: De handleidingen voor het gebruik van hoofdletters en kleine letters zijn nu beschikbaar. Lees de het prospecteren handleidingen van de gebruiksgeval om te leren hoe te om nieuwe klanten door het prospecteren gebruiksgevallen in dienst te nemen en te verwerven:<ul><li>[Perspectief](../../rtcdp/partner-data/prospecting.md)</li><li>[Onsite personalisatie](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Eerst-partijprofielen aanvullen](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Perspectiefpubliek activeren](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Lees voor meer informatie de [Real-Time CDP-overzicht](../../rtcdp/overview.md).

## Toegangsbeheer op basis van kenmerken {#abac}

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform die privacybewuste merken meer flexibiliteit biedt om gebruikerstoegang te beheren. Afzonderlijke objecten zoals schemavelden en segmenten kunnen worden toegewezen aan gebruikersrollen. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot, gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en ander aangepast type van gegevens over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Configuratie van beleidssandbox voor machtigingen | De nieuwe [configuratie van sandbox met machtigingsbeleid](../../access-control/abac/ui/policies.md) Met deze functie kunt u afhankelijk van uw behoeften en vereisten een op kenmerken gebaseerd toegangsbeheerbeleid toepassen op alle sandboxen of een geselecteerd aantal sandboxen. |

{style="table-layout:auto"}

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie [op attributen-gebaseerd toegangsbeheeroverzicht](../../access-control/abac/overview.md). Voor een uitvoerige gids over het op attributen-gebaseerde toegangsbeheerwerkschema, lees [attribuut-based toegangsbeheergids van begin tot eind](../../access-control/abac/end-to-end-guide.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gebruiksscenario voor analyse en bijhouden van toestemming | Leer hoe u met de [document voor de analyse en het bijhouden van de toestemming](../../dashboards/insights-use-cases/consent-analysis.md). Het bepaalt hoe te om een publiek met de aangewezen attributen voor uw bedrijfsbehoeften te creëren, en dan de inzichten te verbruiken door het gebruik van pre-gevormde widgets in Adobe Experience Platform UI. Het biedt ook instructies voor het bouwen van uw eigen aangepaste widget met de door de gebruiker gedefinieerde dashboardfunctie. Het document heeft betrekking op gevallen waarin toestemming wordt verleend en gevallen waarin toestemming wordt gegeven, overlappen. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden, waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Tags en doorsturen van gebeurtenissen | [Experience Platform-tags (China)](/help/tags/ui/publishing/premium-cdn.md) | De nieuwe functie Tags voor Experience Platforms (China) verbetert de betrouwbaarheid en latentie van websites, waardoor klanten die tags implementeren op websites in China sneller kunnen reageren. Klanten kunnen nu de JavaScript-code in de tagbibliotheek gebruiken wanneer ze websites in China implementeren. Deze eigenschap is ook toegevoegd aan het Verenigde Protocol van de Levering (UPP), toestaand productplaatsing om na aankoop worden geautomatiseerd. |

{style="table-layout:auto"}

Lees voor meer informatie de [overzicht van gegevensverzamelingen](../../tags/home.md).

## Gegevensopname {#data-ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. U kunt opnemen met de API&#39;s Batch of Streaming via Adobe, partners voor gegevensintegratie of de interface van Adobe Experience Platform.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijzigingen in workflows voor gegevensinvoer | Rijen gegevens met waarden die groter zijn dan het opgegeven gegevenstype (bijvoorbeeld lange gegevens die als gegevenstype voor gehele getallen worden doorgegeven) worden nu afgewezen en foutberichten worden gerapporteerd. Eerder werden deze rijen zonder waarschuwing verworpen. |

Lees voor meer informatie de [gegevensinvoer - overzicht](../../ingestion/home.md).

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het filteren van secundaire identiteiten | U kunt de Prep van Gegevens nu gebruiken om uit identiteiten uit Adobe Analytics, zoals STEUN en AACUSTOMID te filteren. Als deze identiteiten worden uitgefilterd, worden ze niet opgenomen in het Real-Time Klantprofiel. Ongefilterde gegevens blijven in het datumpeer worden opgenomen. |
| Ondersteuning voor nieuwe `correlationID` veld voor Adobe Analytics | De `_experience.decisioning.propositions.scopeDetails.correlationID` Het veld is nu beschikbaar in het Adobe Analytics-bronverbindingsschema. Dit veld wordt gebruikt ter ondersteuning van A4T-classificaties en wordt vanaf september 2023 ingevuld. |

{style="table-layout:auto"}

Lees voor meer informatie de [Overzicht van Data Prep](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Gebruik deze klasse om perspectiefprofielen in te brengen die van de top-of-the-funnel van gegevensverkopers van het gebruiksgeval van de klantenverwerving worden afkomstig. |

{style="table-layout:auto"}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Extensie ([!UICONTROL Adobe Analytics ExperienceEvent Full Extension]) | [[!UICONTROL Context Data]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL Context Data] toewijzingsobject toegevoegd aan [!UICONTROL Adobe Analytics ExperienceEvent Full Extension] om contextgegevens voor Adobe Analytics te verstrekken. |
| Veldgroep | Meerdere | Meerdere velden toegevoegd aan [[!UICONTROL Enriched Event Segment Details]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

Lees voor meer informatie de [XDM System, overzicht](../../xdm/home.md).

## Identiteitsservice {#identity-service}

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijzigingen in limieten van identiteitsgrafieken | Eind september zal de identiteitsgrafiek veranderen in 50 identiteiten per grafiek, en de recentste identiteit zal worden opgenomen. Als gevolg hiervan wordt de oudste identiteit verwijderd op basis van de tijdstempel en het type identiteit van de inname, waarbij de identiteitstypen van cookies eerst worden verwijderd. Tegenwoordig geldt voor identiteitsgrafieken een limiet van 150 identiteiten per grafiek. Zodra deze limiet is bereikt, worden grafieken niet meer bijgewerkt. Neem contact op met uw accountvertegenwoordiger om een wijziging in het type identiteit aan te vragen als uw productiessandbox het volgende bevat: <ul><li>een aangepaste naamruimte waarin de personen-id&#39;s (zoals CRM-id&#39;s) zijn geconfigureerd als cookie-/apparaatidentiteitstype.</li><li>een aangepaste naamruimte waarin cookie-/apparaat-id&#39;s zijn geconfigureerd als identiteitstype voor verschillende apparaten.</li></ul> Deze aanvragen worden handmatig verwerkt door Adobe-engineering. Lees voor meer informatie de [handleidingen voor identiteitsservicegegevens](../../identity-service/guardrails.md). |

Lees voor meer informatie de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Zichtbare soorten publiek (beperkte beschikbaarheid) | Het publiek van look-alike verstrekt intelligente inzichten op elk van uw publiek, leveraging machine-leert-gebaseerde inzichten om high-value klanten met uw marketing campagnes te identificeren en te richten. Met look-alike soorten publiek, kunt u uitgebreide soorten publiek tot stand brengen die klanten gelijkend op uw hoog presterende publiek of doelklanten gelijkend op eerder omgezette publiek richten. Lees voor meer informatie over look-alike-soorten publiek de [Overzicht van alle soorten publiek](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

Lees voor meer informatie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van [!DNL SugarCRM] | [!DNL SugarCRM] bronnen zijn nu beschikbaar . Gebruik de [!DNL SugarCRM Accounts & Contacts] en de [!DNL SugarCRM Events] bronnen om gegevens van uw [!DNL SugarCRM] aan Experience Platform. Lees voor meer informatie de [[!DNL SugarCRM] overzicht](../../sources/connectors/crm/sugarcrm.md). |
| Ondersteuning voor inname op aanvraag voor gegevensstromen van bronnen in de gebruikersinterface | U kunt stroomlooppas nu op bestelling voor een bestaande brondataflow in UI tot stand brengen. Lees voor meer informatie de handleiding op [het creëren van een stroomlooppas op bestelling voor bronnen die UI gebruiken](../../sources/tutorials/ui/on-demand-ingestion.md). |

{style="table-layout:auto"}

Lees voor meer informatie de [overzicht van bronnen](../../sources/home.md).
