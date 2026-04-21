---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5d1825bad97d3ec4beece416dc3e0fc9f6ca636d
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 20%

---

# Opmerkingen bij de release Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is voorgenomen als a **voorproef** van de versienota&#39;s voor de huidige maand. Release-items kunnen worden gewijzigd en worden toegevoegd of verwijderd in de definitieve versie.

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: april 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Bestemmingen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Queryservice](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [!BADGE &#x200B; Beta &#x200B;]{type=Informative} [&#x200B; Microsoft voegt de Gelijke van de Klant &#x200B;](../destinations/catalog/advertising/microsoft-ads-customer-match.md) toe | Klanten afstemmen op e-mailadres en met hen communiceren over de [!DNL Microsoft Advertising Network] , waaronder advertentie voor zoeken en publiek. Koppel uw [!DNL Microsoft Advertising] -account aan Real-Time CDP om het maken en beheren van lijsten door klanten rechtstreeks vanuit Experience Platform te automatiseren. |
| [!BADGE &#x200B; Beta &#x200B;]{type=Informative} [&#x200B; reddit de Audience van de Douane &#x200B;](../destinations/catalog/advertising/reddit-custom-audience.md) | Verzend het publiek van Experience Platform naar [!DNL Reddit Ads] . Sluit uw [!DNL Reddit] -account aan, wijs identiteiten toe en activeer het publiek om mensen te bereiken die actief hun interesses verkennen op [!DNL Reddit] . |
| [&#x200B; Amazon Ads v2 &#x200B;](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2] is het huidige doel voor alle nieuwe [!DNL Amazon Ads] verbindingen. Als u een bestaande [&#x200B; (Verouderd)  [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) verbinding hebt, blijft het functioneren zonder enige vereiste veranderingen. [!DNL Amazon Ads v2] verbindt met [!DNL Ads Data Manager], die steun voor uitgebreide identiteitstypes, adres-verwante gebieden, en gegeven-delend over [!DNL Amazon Ads] producten verleent, verbeterend het richten en publiek past tarieven in vergelijking met [&#x200B; (Verouderd)  [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) aan. |
| [!DNL Rokt] | Met [!DNL Rokt] kunt u Experience Platform-doelgroepen verbinden met door AI gestuurde realtime beslissingen, waardoor de campagneprestaties worden verbeterd dankzij een nauwkeurigere gerichtheid, onderdrukking en personalisatie. |

{style="table-layout:auto"}

**Bevestigingen en verbeteringen**

| Repareren | Beschrijving |
| --- | --- |
| Aangepaste ondersteuning voor Personalization-bewaking | Het controledashboard voor bestemmingen ondersteunt nu [!DNL Custom Personalization] doelen. De beperkingsopmerking die [!DNL Custom Personalization] van controle heeft uitgesloten, is verwijderd. |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Zichtbaarheid veldgroepsschema | Bekijk welke schema&#39;s een gebiedsgroep van de detailpagina gebruiken en verken hen in een sorteerbare dialoog met schemameta-gegevens. Hierdoor kunt u snel afhankelijkheden en effecten beoordelen zonder weg te navigeren. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; XDM overzicht van het Systeem &#x200B;](../xdm/home.md).

## Queryservice {#query-service}

Gebruik Query Service om query&#39;s uit te voeren in Adobe Experience Platform [!DNL Data Lake] met standaard SQL. Sluit aan om het even welke datasets van [!DNL Data Lake] aan en vang vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Wetenschap van Gegevens Workspace, of opname in het Profiel van de Klant in real time.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Data Distiller Accelerators | De looppas en plant Adobe-geleide, geparameterized SQL malplaatjes in de Dienst UI van de Vraag om gemeenschappelijke analyses uit te voeren zonder SQL te schrijven. Dit helpt u analytische werkschema&#39;s te standaardiseren en vertrouwde op vraaglogica over uw organisatie opnieuw te gebruiken. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; overzicht van de Dienst van de Vraag &#x200B;](../query-service/home.md).

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP] biedt uniforme, activeerbare klantprofielen door gegevens via meerdere kanalen in real-time in te voeren, te verwerken en te activeren. Met Real-Time CDP kunnen organisaties bestaande gegevensbronnen verbinden, een rijk publiek maken en activeren en zorgen voor activering die voldoet aan de privacy op alle bestemmingen, allemaal vanuit Experience Platform. Dit stelt marketers, analisten en IT-teams in staat om hun klanten via naadloze, kanaaloverschrijdende marketingcampagnes zeer persoonlijke, actuele ervaringen te bieden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Real-Time CDP MCP (Beta) | Gebruik Real-Time CDP MCP om Real-Time CDP in AI agenten en MCP-compatibele cliënten te brengen, toelatend u om met de hulpmiddelen van Real-Time CDP direct door uw inheemse ervaring van LLM in wisselwerking te staan. Door een MCP-compatibele cliënt (zoals Claude, ChatGPT, Claude Code, Codex, Cursor, of de Code van VS) aan `https://rtcdp-mcp.adobe.io/mcp` aan te sluiten, kunt u natuurlijke taal gebruiken om publiek, bestemmingsconfiguratie, en activeringsloopgeschiedenis te inspecteren, zonder Experience Platform REST API vraag te schrijven of veelvoudige werkschema&#39;s te navigeren UI. Nadat u een Adobe-aanmelding in een browser hebt voltooid, hebt u alleen-lezen toegang tot gereedschappen, zoals: <ul><li>Bestaande soorten publiek zoeken</li><li>Bekijk het lidmaatschap van een publiek</li><li>Bestemmingstypen weergeven</li><li>Gevormde accounts weergeven</li><li>Gevormde doelen weergeven</li><li>Source-verbindingen weergeven</li><li>Doelverbindingen weergeven</li><li>Activeringscycli controleren</li></ul>. Voor elke aanvraag zijn `imsOrgId` - en `sandboxName` -parameters vereist om ervoor te zorgen dat acties binnen het bereik van uw organisatie en sandbox vallen. Schrijfbewerkingen worden niet ondersteund in deze Beta-versie. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; overzicht van Real-Time CDP &#x200B;](../rtcdp/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Expressie | Het Uitdrukkelijke Exemplaar van het gebruik om voorwerpen aan een doelzandbak in één enkele actie van [&#x200B; te kopiëren Sandbox het Tooling UI &#x200B;](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Afhankelijke objecten worden automatisch gedetecteerd en worden gemaakt in de doelsandbox of worden opnieuw gebruikt wanneer ze al bestaan. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; zandbakenoverzicht &#x200B;](../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

Gebruik Segmentatieservice om publiek te maken van uw klantgegevens en hun volledige levenscyclus in Experience Platform te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bewaking van streaming segmentering | Monitor die segmentatie met zicht in real time in evaluatiesnelheid, innamelatentie, en de metriek van de gegevenskwaliteit op zandbak, dataset, en segmentniveau stroomt. De metriek van de mening met inbegrip van evaluatiesnelheid, P95 ingesliplatentie, ontvangen verslagen, geëvalueerde verslagen, ontbroken verslagen, en overgeslagen verslagen. Bekijk ook netto nieuwe profielen die per segment zijn gekwalificeerd en gediskwalificeerd. Gebruik deze inzichten om capaciteitsschendingen en inname kwesties te identificeren alvorens zij uw gegevens beïnvloeden. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; overzicht van het publiek &#x200B;](../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| Automatische gegevensstroomuitschakeling | Bronnen die gegevens opnemen die gedurende 30 dagen ononderbroken mislukken, worden automatisch uitgeschakeld, zodat ongezonde gegevensstromen kunnen worden opgevangen en herhalende mislukte run kan worden beperkt. |
| [!DNL Delta Sharing] | U kunt de [!DNL Delta Sharing] -bron gebruiken om Delta-tabellen naar Experience Platform te brengen via een beveiligd, open protocol voor het delen van gegevens. Nadat u een [!DNL Delta Sharing] verbinding vormt en de aandelen en lijsten selecteert u wilt opnemen, brengt Platform automatisch die gegevens in uw datasets zodat u het voor analyse, segmentatie, en activering kunt gebruiken. |
| [!DNL Meta Ads] (Beta) | U kunt de [!DNL Meta Ads] bronschakelaar (Beta) in de werkruimte van Bronnen gebruiken om aan [!DNL Meta] voor authentiek te verklaren, uw advertentieverslagen te selecteren, en opname van [!DNL Meta Ads] campagne en prestatiesgegevens in de datasets van Experience Platform te plannen. |
| [!DNL Talon.One] | U kunt nu Experience Platform verbinden met [!DNL Talon.One] door de nieuwe batch- en streaming bronnen van [!DNL Talon.One] te gebruiken. Gebruik de nieuwe bronnen om loyaliteitsprofielgegevens evenals transactie en loyaliteitsactiviteitengebeurtenissen aan Experience Platform in te voeren. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).
