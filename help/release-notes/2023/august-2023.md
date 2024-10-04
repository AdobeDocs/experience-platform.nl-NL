---
title: Aanvullende informatie van augustus 2023 voor Adobe Experience Platform
description: Aanvullende informatie van augustus 2023 voor Adobe Experience Platform.
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: d6e306294d0a119108e2de7ba03ebed4f633fba1
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 40%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 23 augustus 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Real-Time Customer Data Platform](#rtcdp)
- [Toegangsbeheer op basis van kenmerken](#abac)
- [Dashboards](#dashboards)
- [Dataverzameling](#data-collection)
- [Gegevensopname](#data-ingestion)
- [Gegevensvoorbereiding](#data-prep)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Real-time Customer Data Platform ([!DNL Real-Time CDP]) is gebaseerd op Experience Platform en helpt bedrijven bekende en onbekende gegevens bijeen te brengen om klantprofielen te activeren door middel van intelligente beslissingen tijdens de reis van de klant.

[!DNL Real-Time CDP] combineert meerdere bedrijfsgegevensbronnen om klantprofielen in real-time te maken. Segmenten die op basis van deze profielen zijn samengesteld, kunnen vervolgens naar downstreambestemmingen worden verzonden om gepersonaliseerde één-op-één klantervaringen te bieden via alle kanalen en apparaten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Intelligente handleiding voor hergebruik | De [ Intelligente re-overeenkomst ](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) gebruikscassegids verstrekt details op hoe te om klant opnieuw in dienst te nemen die een omzetting alvorens het op een intelligente en verantwoordelijke manier hebben verlaten te voltooien. Deze gids gebruikt de volgende voorbeeldreizen om klanten opnieuw in dienst te nemen: <ul><li>Reizigersreis: gericht op klanten die het bladeren van producten hebben verlaten.</li><li>Verlaten winkelwagentje - Klanten die producten in het winkelwagentje hebben geplaatst maar de aankoop nog niet hebben voltooid.</li><li>Reis voor bevestiging van bestelling - Gericht op aankopen van producten</li></ul> Gelieve te gebruiken de gedetailleerde koppel terugkoppelt opties bij de bodem van de [ Intelligente gids van het gebruiksgeval van het Terugkeer ](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) om terugkoppelen te verstrekken. |
| Ondersteuning van partnergegevens | Voer upper-funnel marketing in Real-Time CDP, met partner-gesourceerde perspectiefprofielen en partner IDs uit om nieuwe klanten te bereiken en uw eerste-partijgegevens te verrijken: <ul><li>Aanschaf en adresseerbaarheid van de klant: gebruik van cokieless identifiers en hashed PII van gegevenspartners van keuze om nieuwe klanten te bereiken en de afhankelijkheid van cookies van derden te verminderen.</li><li>Volledige kanaalmarketing in één enkel systeem: Zelf-serversegmentatie, publiekscorrectie, en inheemse activering voor toekomstige en bekende klanten in één enkel systeem.</li><li>Stichting van vertrouwen: De gegevens en de profielen van de partner van de regering met geoctrooieerd gegevensgebruik, etikettering, toegangscontroles, en meer aan markt verantwoordelijk. Lees de volgende handleidingen voor het gebruik van hoofdletters en kleine letters voor meer informatie: De handleidingen voor het gebruik van hoofdletters en kleine letters zijn nu beschikbaar. Lees de het prospecteren handleidingen van de gebruiksgeval om te leren hoe te om nieuwe klanten door het prospecteren gebruiksgevallen in dienst te nemen en te verwerven:<ul><li>[ Vooruitziend ](../../rtcdp/partner-data/prospecting.md)</li><li>[ Onsite verpersoonlijking ](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[ Supplement eerste-partijprofielen ](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[ activeer perspectiefpubliek ](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Voor meer informatie, te lezen gelieve het [ overzicht van Real-Time CDP ](../../rtcdp/overview.md).

## Toegangsbeheer op basis van kenmerken {#abac}

Toegangsbeheer op basis van kenmerken is een functionaliteit van Adobe Experience Platform waarmee merken die aandacht hebben voor privacy, meer flexibiliteit krijgen bij toegangsbeheer voor gebruikers. Individuele objecten, zoals schemavelden en segmenten, kunnen aan gebruikersrollen worden toegewezen. Met deze functie kunt u toegang tot individuele objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Met toegangsbeheer op basis van kenmerken kunnen beheerders van uw organisatie de toegang van gebruikers tot gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en andere aangepaste typen gegevens in alle platformworkflows en -bronnen beheren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die bij die velden horen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Configuratie van beleidssandbox voor machtigingen | De nieuwe ](../../access-control/abac/ui/policies.md) eigenschap van de de zandbakconfiguratie van het 1} toestemmingsbeleid staat u toe om een attribuut gebaseerd toegangsbeheerbeleid op allen of een geselecteerd aantal zandbakken af te dwingen, afhankelijk van uw behoeften en vereisten.[ |

{style="table-layout:auto"}

Zie het [overzicht van toegangsbeheer op basis van kenmerken](../../access-control/abac/overview.md) voor meer informatie over toegangsbeheer op basis van kenmerken. Voor een uitgebreide handleiding over de workflow voor toegangsbeheer op basis van kenmerken raadpleegt u de [end-to-end handleiding voor toegangsbeheer op basis van kenmerken](../../access-control/abac/end-to-end-guide.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten kunt bekijken over de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gebruiksscenario voor analyse en bijhouden van toestemming | Leer hoe te om een toestemmingsdashboard voor diverse marketing gebruiksgevallen voor de gegevens van Real-Time CDP met het [ toestemming-analyse en het volgen document ](../../dashboards/insights-use-cases/consent-analysis.md) te bouwen. Het bepaalt hoe te om een publiek met de aangewezen attributen voor uw bedrijfsbehoeften te creëren, en dan de inzichten te verbruiken door het gebruik van pre-gevormde widgets in Adobe Experience Platform UI. Het biedt ook instructies voor het bouwen van uw eigen aangepaste widget met de door de gebruiker gedefinieerde dashboardfunctie. Het document heeft betrekking op gevallen waarin toestemming wordt verleend en gevallen waarin toestemming wordt gegeven, overlappen. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, inclusief het verlenen van toegangsrechten en het maken van aangepaste widgets, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Tags en gebeurtenis doorsturen | [ de Markeringen van het Experience Platform (China) ](/help/tags/ui/publishing/premium-cdn.md) | De nieuwe functie Tags voor Experience Platforms (China) verbetert de betrouwbaarheid en latentie van websites, waardoor klanten die tags implementeren op websites in China sneller kunnen reageren. Klanten kunnen nu de JavaScript-code in de tagbibliotheek gebruiken wanneer ze websites in China implementeren. Deze eigenschap is ook toegevoegd aan het Verenigde Protocol van de Levering (UPP), toestaand productplaatsing om na aankoop worden geautomatiseerd. |

{style="table-layout:auto"}

Voor meer informatie, te lezen gelieve het [ overzicht van gegevensinzamelingen ](../../tags/home.md).

## Gegevensopname {#data-ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het toevoegen van elk type en elke latentie van gegevens. U kunt gegevens toevoegen via batch- of streaming-API&#39;s, via door Adobe gebouwde bronnen, via gegevensintegratiepartners of via de gebruikersinterface van Adobe Experience Platform.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijzigingen in workflows voor gegevensinvoer | Rijen gegevens met waarden die groter zijn dan het opgegeven gegevenstype (bijvoorbeeld lange gegevens die als gegevenstype voor gehele getallen worden doorgegeven) worden nu afgewezen en foutberichten worden gerapporteerd. Eerder werden deze rijen zonder waarschuwing verworpen. |

Voor meer informatie, te lezen gelieve het [ overzicht van de gegevensopname ](../../ingestion/home.md).

## Gegevensvoorbereiding {#data-prep}

Met gegevensvoorbereiding kunnen gegevenstechnici gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience-datamodel).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het filteren van secundaire identiteiten | U kunt de Prep van Gegevens nu gebruiken om uit identiteiten uit Adobe Analytics, zoals STEUN en AACUSTOMID te filteren. Als deze identiteiten worden uitgefilterd, worden ze niet opgenomen in het Real-Time Klantprofiel. Ongefilterde gegevens blijven in het datumpeer worden opgenomen. |

{style="table-layout:auto"}

Voor meer informatie, te lezen gelieve het [ Prep overzicht van Gegevens ](../../data-prep/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

- U kunt [ perspectiefpubliek ](../../destinations/ui/activate-prospect-audiences.md) aan de bestemmingen van de wolkenopslag nu activeren.
- De algemene [ activeringsgarantie ](../../destinations/guardrails.md#general-activation-guardrails) van maximum 100 bestemmingen per zandbak is bijgewerkt om a _harde grens_ te zijn.

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Gebruik deze klasse om perspectiefprofielen in te brengen die van de top-of-the-funnel van gegevensverkopers van het gebruiksgeval van de klantenverwerving worden afkomstig. Raadpleeg de documentatie van [[!UICONTROL XDM Individual Prospect Profile]](../../xdm/classes/prospect.md) voor voorbeelden en meer informatie. |

{style="table-layout:auto"}

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Extensie ([!UICONTROL Adobe Analytics ExperienceEvent Full Extension]) | [[!UICONTROL Context Data]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL Context Data] toewijzingsobject toegevoegd aan [!UICONTROL Adobe Analytics ExperienceEvent Full Extension] voor het verschaffen van contextgegevens voor Adobe Analytics. |
| Veldgroep | Meerdere | Verschillende velden toegevoegd aan [[!UICONTROL Enriched Event Segment Details] ](https://github.com/adobe/xdm/pull/1760/files) . |

{style="table-layout:auto"}

Voor meer informatie, te lezen gelieve het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Identiteitsservice {#identity-service}

Met Adobe Experience Platform Identity Service krijgt u een compleet beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen. Zo kunt u in real-time impactvolle, persoonlijke digitale ervaringen bieden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijzigingen in limieten van identiteitsgrafieken | Eind september zal de identiteitsgrafiek veranderen in 50 identiteiten per grafiek, en de recentste identiteit zal worden opgenomen. Als gevolg hiervan wordt de oudste identiteit verwijderd op basis van de tijdstempel en het type identiteit van de inname, waarbij de identiteitstypen van cookies eerst worden verwijderd. Tegenwoordig geldt voor identiteitsgrafieken een limiet van 150 identiteiten per grafiek. Zodra deze limiet is bereikt, worden grafieken niet meer bijgewerkt. Neem contact op met uw accountvertegenwoordiger om een wijziging in het type identiteit aan te vragen als uw productiessandbox het volgende bevat: <ul><li>een aangepaste naamruimte waarin de personen-id&#39;s (zoals CRM-id&#39;s) zijn geconfigureerd als cookie-/apparaatidentiteitstype.</li><li>een aangepaste naamruimte waarin cookie-/apparaat-id&#39;s zijn geconfigureerd als identiteitstype voor verschillende apparaten.</li></ul> Deze aanvragen worden handmatig verwerkt door Adobe-engineering. Voor meer informatie, lees de [ gidsen voor de gegevens van de Dienst van de Identiteit ](../../identity-service/guardrails.md). |

Voor meer informatie, te lezen gelieve het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Segmentatieservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, prospects, gebruikers of organisaties) segmenteren in doelgroepen. U kunt doelgroepen maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile]-gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform], en zijn gemakkelijk toegankelijk via elke Adobe-toepassing.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Zichtbare soorten publiek (beperkte beschikbaarheid) | Het publiek van look-alike verstrekt intelligente inzichten op elk van uw publiek, leveraging machine-leert-gebaseerde inzichten om high-value klanten met uw marketing campagnes te identificeren en te richten. Met look-alike soorten publiek, kunt u uitgebreide soorten publiek tot stand brengen die klanten gelijkend op uw hoog presterende publiek of doelklanten gelijkend op eerder omgezette publiek richten. Voor meer informatie over blik-alike publiek, te lezen gelieve [ blik-alike publiek overzicht ](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

Voor meer informatie, te lezen gelieve het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van [!DNL SugarCRM] | [!DNL SugarCRM] -bronnen zijn nu beschikbaar. Gebruik de bronnen [!DNL SugarCRM Accounts & Contacts] en [!DNL SugarCRM Events] om gegevens van uw [!DNL SugarCRM] -account naar het Experience Platform te verzenden. Voor meer informatie, lees het [[!DNL SugarCRM]  overzicht ](../../sources/connectors/crm/sugarcrm.md). |
| Ondersteuning voor inname op aanvraag voor gegevensstromen van bronnen in de gebruikersinterface | U kunt stroomlooppas nu op bestelling voor een bestaande brondataflow in UI tot stand brengen. Voor meer informatie, lees de gids op [ creërend een stroom op bestelling voor bronnen gebruikend UI ](../../sources/tutorials/ui/on-demand-ingestion.md). |
| Ondersteuning voor nieuw veld `correlationID` voor Adobe Analytics | Het veld `_experience.decisioning.propositions.scopeDetails.correlationID` is nu beschikbaar in het Adobe Analytics-bronverbindingsschema. Dit veld wordt gebruikt ter ondersteuning van A4T-classificaties en wordt vanaf september 2023 ingevuld. |

{style="table-layout:auto"}

Voor meer informatie, te lezen gelieve het [ overzicht van bronnen ](../../sources/home.md).
