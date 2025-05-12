---
title: Aanvullende informatie van april 2025 voor Adobe Experience Platform
description: Aanvullende informatie van april 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6558046e9708267cd0ceda36e7c0bdba6b2f758a
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 93%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/nl/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 29 april 2025**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [Experience League](#experience-league)
- [Dataverzameling](#data-collection)
- [Bestemmingen](#destinations)
- [Experience-datamodel](#xdm)
- [Identiteitsservice](#identity)
- [Query-service](#query-service)
- [Realtime-klantenprofiel](#profile)
- [Sandboxes](#sandboxes)
- [Bronnen](#sources)
- [Playbooks voor gebruiksscenario&#39;s](#use-case-playbooks)

## Experience League {#experience-league}

Experience League is een uitgebreid leerplatform dat is ontworpen om uw vaardigheden met Adobe-producten te verbeteren. Het biedt een verscheidenheid aan middelen, zoals cursussen, documentatie, communitypagina&#39;s, events en toegang tot certificeringen.

| Functie | Beschrijving |
| --- | --- |
| Gepersonaliseerde startpagina | De toegang en past uw gepersonaliseerde homepage op [ Experience League ](https://experienceleague.adobe.com/nl/home#) aan. Meld u aan met uw Adobe-referenties en selecteer vervolgens **[!UICONTROL Experience League]** in het bovenste menu om uw leerervaring te optimaliseren: <ul><li>**Bladwijzers**: gebruik de functie [!UICONTROL Bookmarks] om uw favoriete bronnen op één plek op te slaan en te verzamelen. U kunt verschillende inhoud opslaan, zoals afspeellijsten, artikelen en tutorials.</li><li>**Pas uw leerervaring aan**: verbeter uw leerervaring door uw Experience League-profiel bij te werken met de rollen, branches, producten en het ervaringsniveau die het beste bij uw behoeften passen.</li><li>**Aanbevelingen**: bekijk leerinhoud die wordt aanbevolen op basis van uw recente activiteit.</li><li>**Recent bekeken**: gebruik de sectie [!UICONTROL Recently viewed] om snel terug te gaan naar recent bekeken inhoud, zoals documentatie en video&#39;s.</li><li>**Learning-bronnen**: gebruik het deelvenster [!UICONTROL All learning resources] om naar tutorials, documentatie, community, evenementen en certificeringen te gaan.</li><li>**Nieuw**: bekijk de sectie [!UICONTROL What's new] voor een overzicht van de recentste inhoud op Experience League.</li><li>**Bekijk eerdere evenementen op vraag**: bekijk eerder opgenomen livestreams over productpresentaties, use cases en tutorials met de sectie [!UICONTROL Watch past events on-demand].</li></ul><br> ![Gepersonaliseerde startpagina op Experience League.](../2025/assets/april/personalized-home-page.png "Gepersonaliseerde startpagina op Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Adform] extension | Met de serverextensie [!DNL Adform] kunnen merken het publiek gemakkelijk offline richten met behulp van ECID&#39;s. Deze server-side extensie is niet afhankelijk van cookies van derden of cookie-alternatieve id&#39;s. Bovendien, omdat dit volledig server-kant wordt gedaan, zijn geen extra pixel of andere cliënt-zijveranderingen nodig. Voor meer informatie, zie het [ Adform uitbreidingsoverzicht ](/help/tags/extensions/server/adform/overview.md). |
| [!DNL Amazon] API-extensie voor webgebeurtenissen | Met de API-extensie [!DNL Amazon] Conversies kunnen adverteerders website-interacties rechtstreeks delen met [!DNL Amazon] , waardoor de toewijzing, betrouwbaarheid van gegevens en de optimalisatie van de campagne zijn verbeterd. Deze extensie ondersteunt het doorsturen van gebeurtenissen, zodat u conversiegebeurtenissen zoals aankopen, winkelwagentaanvullingen en meer kunt verzenden en er tegelijkertijd voor zorgt dat de deduplicatie correct wordt uitgevoerd voor een juiste rapportage. Voor meer informatie, zie het [ de uitbreidingsoverzicht van Amazon ](/help/tags/extensions/server/amazon/overview.md). |

{style="table-layout:auto"}

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe heeft het doel [!DNL Marketo Engage Person Sync] bijgewerkt om een probleem op te lossen dat klanten ondervonden wanneer er meerdere e-mails in de identiteitsafbeelding waren. |
| [(V2) Pega CDH Realtime Audience-verbinding](/help/destinations/catalog/personalization/pega-v2.md) | Gebruik het doel [!DNL (V2) Pega Customer Decision Hub Realtime Audience] in Adobe Experience Platform om profielkenmerken en gegevens over doelgroeplidmaatschap naar Pega Customer Decision Hub te sturen voor het nemen van de best mogelijke vervolgbeslissing, wanneer u meerdere Pega Customer Decision Hub-toepassingen hebt geconfigureerd in uw Pega-account. |

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| **Wekelijkse** en **maandelijkse** planningsopties voor volledige bestandsexporten | U kunt nu volledige bestandsexporten voor personen en potentiële doelgroepen plannen op een wekelijkse of maandelijkse basis wanneer u activeert naar op bestanden gebaseerde bestemmingen in de cloudopslag. [Lees meer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) over planningsopties. |

{style="table-layout:auto"}

**Oplossingen, verbeteringen en andere meldingen** {#destinations-fixes-and-enhancements}

- **De opgelegde einddatum voor het exporteren van datasets is verschoven naar 1 september 2025**\
  Als onderdeel van de [release van september 2024](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality) heeft Adobe een standaardeinddatum van 1 mei 2025 ingesteld voor alle dataset-exportgegevensstromen die *vóór die release* zijn gemaakt. Adobe heeft deze opgelegde einddatum nu verschoven naar **1 september 2025** zodat klanten extra tijd hebben om hun planningen bij te werken. Raadpleeg de planningssectie van de [tutorial over het exporteren van datasets](../../destinations/ui/export-datasets.md#schedule-dataset-export) voor informatie over hoe u de einddatum van een dataset-exportgegevensstroom bewerkt.

- **Verbeterde afhandeling van mislukte SFTP-overdrachten voor LiveRamp Onboarding**\
  Adobe heeft een probleem met de bestandsuitvoer naar de [LiveRamp Onboarding](/help/destinations/catalog/advertising/liveramp-onboarding.md)-bestemming via SFTP opgelost. Zo nu en dan mislukten bestandsoverdrachten als gevolg van kortstondige problemen aan de serverkant en bleven er tijdelijke bestanden van mislukte pogingen op de server achter. Deze niet-verwijderbare bestanden blokkeerden daaropvolgende pogingen, omdat Adobe geen toestemming had om ze te overschrijven.\
  Als het tijdelijke bestand niet kan worden verwijderd bij een nieuwe poging, genereert Adobe dankzij de oplossing een nieuw bestand met het achtervoegsel `attempt2` zodat de nieuwe poging wordt voltooid.

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte XDM-onderdelen**

| Functie | Beschrijving |
| --- | --- |
| Tekenreeksvelden ontvangen een minimumwaarde van één | Nieuwe tekenreeksvelden krijgen standaard een minimale lengte van één. Null-waarden voor niet-vereiste velden zijn nog steeds acceptabel. Raadpleeg de gids over [beste praktijken voor datamodeling](../../xdm/schema/best-practices.md#data-integrity-tips) voor meer informatie over beste praktijken. |

{style="table-layout:auto"}

Raadpleeg het [XDM-systeemoverzicht](../../xdm/home.md) voor meer informatie over XDM in Experience Platform.

## Identiteitsservice {#identity}

Met Identity Service van Adobe Experience Platform krijgt u een uitgebreid beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen, zodat u in real-time een impactvolle, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| &rbrack;{type=Informative} [!DNL Identity Graph Linking Rules] De Beperkte Regels van de Grafiek van de Identiteit van de Beschikbaarheid kunnen nu door alle klanten in ontwikkelingszandbakken worden betreden. <ul><li>**Activeringsvereisten**: de functie blijft inactief totdat u de [!DNL Identity Settings] configureert en opslaat. Zonder deze configuratie blijft het systeem normaal werken, zonder veranderingen in gedrag.</li><li>**Belangrijke opmerkingen**: tijdens de fase Beperkte beschikbaarheid kunt u bij Edge-segmentatie onverwachte resultaten van segmentlidmaatschappen ervaren. De segmentatie van streaming en batches functioneert echter zoals gewoonlijk.</li><li>**Volgende stappen**: neem contact op met uw Adobe-accountteam voor informatie over hoe u deze functie in productiesandboxes inschakelt.</li></ul> |

{style="table-layout:auto"}

Raadpleeg de [[!DNL Identity Graph Linking Rules] documentatie](../../identity-service/identity-graph-linking-rules/overview.md) voor meer informatie.

## Query-service {#query-service}

Voer query&#39;s uit op gegevens in het Adobe Experience Platform-data lake met behulp van standaard SQL met Query Service. Combineer naadloos datasets en genereer nieuwe op basis van de queryresultaten om rapportage, datawetenschapworkflows of opname in het realtimeklantprofiel mogelijk te maken. U kunt bijvoorbeeld de gegevens van de klantentransactie samenvoegen met de gedragsgegevens om hoogwaardige doelgroepen te identificeren voor gerichte marketingcampagnes.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| SQL-doelgroepen overschrijven | Vernieuw het doelgroepslidmaatschap door bestaande profielen met de resultaten van een nieuwe SQL-query te overschrijven. Door in één bewerking verouderde records te verwijderen en bijgewerkte records in te voegen, kunt u dynamische doelgroepen efficiënter beheren. Zie de [gids over SQL-doelgroepextensies](../../query-service/data-distiller-audiences/overview.md#replace-audience) voor meer informatie. |
| Queryresultaten downloaden en kopiëren | [Download queryresultaten direct vanuit de Query-editor](../../query-service/ui/overview.md#download-query-results) als CSV-, XLSX- of JSON-bestanden, of [kopieer resultaten naar het klembord](../../query-service/ui/overview.md#copy-results) als komma-gescheiden waarden (CSV) om ze snel in spreadsheettoepassingen zoals Excel te gebruiken. Deze verbeteringen stroomlijnen de workflows voor offline analyse, rapportage en gegevensvalidatie. |
| Queryresultaten op volledig scherm weergeven | [Bekijk een voorvertoning van de queryresultaten in een dialoogvenster dat het volledige scherm inneemt](../../query-service/ui/overview.md#view-results) om de leesbaarheid te verbeteren, gemakkelijk grote datasets te scannen, en rijen te selecteren die u wilt kopiëren. De weergave Volledig scherm biedt een aanpasbare rasterlay-out waarmee u brede tabellen en gedetailleerde output efficiënter kunt bekijken. |
| Verbeterde kolomselectie in modelvoorspelling | Selecteer specifieke kolommen en pas aliassen toe met behulp van de uitgebreide `model_predict`-syntaxis. Haal tussentijdse voorspellingsresultaten op, zoals functievectoren en kansscores. Voor de verbeterde selectie is activering van een functiemarkering vereist. Zie [documentatie van de modellevenscyclus](../../query-service/advanced-statistics/models.md#select-specific-output-fields) voor syntaxisvoorbeelden en informatie over de functiemarkering. |
| Outputs van modelvoorspellingen opslaan met CREATE TABLE en INSERT INTO | [Sla geselecteerde outputs van voorspellingen op in nieuwe tabellen met behulp van CREATE TABLE AS SELECT of voeg ze in bestaande tabellen in met behulp van INSERT INTO SELECT](../../query-service/advanced-statistics/models.md#predict). Als u verbeterde kolomselectie hebt ingeschakeld, kunnen tussentijdse resultaten zoals functievectoren en kansscores ook naast definitieve voorspellingen worden weergegeven. Raadpleeg de [SQL-syntaxisdocumentatie](../../query-service/sql/syntax.md#create-table-as-select) voor gebruiksvoorbeelden. |

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../../query-service/home.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

| Functie | Beschrijving |
| ------- | ----------- |
| Vervaldatum voor gegevens van pseudonieme profielen | Beheer de vervaldatum voor gegevens van pseudonieme profielen in het profieldashboard. Raadpleeg de [gids over de vervaldatum voor gegevens van pseudonieme profielen](../../profile/pseudonymous-profiles.md) om meer te weten te komen over deze functie en pseudonieme profielen. |

{style="table-layout:auto"}

Voor meer informatie over Real-Time Customer Profile, raadpleegt u het [overzicht van profielen](../../profile/home.md)

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen biedt Experience Platform sandboxes die één Experience Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verbeterd.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning van plug-in voor sandbox-tools uitgebreid | U kunt nu aangepaste handelingen als afhankelijke objecten kopiëren wanneer u Journey-objecten in sandbox-tools dupliceert. Daarnaast kunt u bestaande handelingen selecteren die u in de doelsandbox opnieuw wilt gebruiken. U kunt ze ook afzonderlijk aan een pakket toevoegen. Raadpleeg de gids over [sandbox-tools](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects) voor volledige informatie over de ondersteunde Adobe Journey Optimizer-objecten. |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, raadpleegt u het [ overzicht van sandboxes](../../sandboxes/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Nieuwe bronnen**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | De [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md)-bron is nu beschikbaar. Gebruik deze bron om de affiniteitsgegevens van uw [!DNL Algolia]-gebruikersprofielen naar Experience Platform te brengen. U kunt deze gegevens vervolgens gebruiken om de betrokkenheid van gebruikers, conversiepercentages en de algehele klantervaring te verbeteren door hoogwaardige zoekoplossingen te bieden voor websites, e-commerceplatforms en toepassingen. Voor meer informatie kunt u de gids over het [opnemen [!DNL Algolia User Profiles] van gegevens in Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md) raadplegen. |
| [!BADGE Beta]{type=Informative} API-ondersteuning voor [!DNL Azure Databricks] | De [!DNL Azure Databricks]-bron is nu beschikbaar in de API. Gebruik de [!DNL Flow Service]-API om uw [!DNL Databricks] account te koppelen en uw [!DNL Databricks] gegevens over te brengen naar Experience Platform. Raadpleeg de documentatie over [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md) voor meer informatie. |

{style="table-layout:auto"}

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte XDM-velden voor het toevoegen van Streaming Media-gegevens op het Experience Platform. | De nieuwe XDM-veldgroep, `mediaReporting`, is nu beschikbaar voor het toevoegen van Streaming Media-gegevens via de Adobe Analytics-bron op het Experience Platform. Dit veld vervangt het veld `media.mediaTimed`.</br> <br>Gedurende een overgangsperiode van drie maanden blijft data-opname voor `media.mediaTimed`-velden doorgaan. Eind juli 2025 zijn de `media.mediaTimed`-velden echter volledig verouderd en niet meer zichtbaar in de gebruikersinterface van het Experience Platform-schema. Gegevens worden alleen verzonden met behulp van de `mediaReporting`-velden.</br><br>Als u de Analytics-bron hebt geïmplementeerd om Streaming Media-gegevens vóór 22 april 2025 op het Platform te verzamelen, dan moet u de bestaande configuraties migreren om gegevens te verzenden met behulp van de nieuwe veldgroep. Deze migratie moet eind juli 2025 zijn voltooid. Neem contact op met uw Adobe-accountteam voor ondersteuning bij migratie. |
| Nieuwe authenticatietypen voor [!DNL MariaDB] en [!DNL PostgreSQL] | U kunt nu basisauthenticatie gebruiken om uw [!DNL MariaDB]- en [!DNL PostgreSQL]-bronnen op het Experience Platform te authenticeren. Raadpleeg de volgende documentatie voor meer informatie: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Ondersteuning van filteren op rijniveau voor [!DNL Amazon Redshift] | U kunt filtermogelijkheden op rijniveau gebruiken voor uw [!DNL Amazon Redshift]-gegevens op het Experience Platform. Raadpleeg de gids over [het filtreren van gegevens op rijniveau voor bronnen in de API](../../sources/tutorials/api/filter.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).

## Playbooks voor gebruiksscenario&#39;s {#use-case-playbooks}

Playbooks voor gebruiksscenario&#39;s zijn oorspronkelijk ontworpen om u te helpen bij het overwinnen van uitdagingen bij het aan de slag gaan met Real-Time Customer Data Platform of Adobe Journey Optimizer. Ze worden steeds verder ontwikkeld en geven u nu de mogelijkheid om belangrijke gebruiksscenario&#39;s voor marketing een boost te geven. Daarnaast voorzien ze u van inspiratie en standaardassets om te testen en in gebruik te nemen.

Playbooks voor gebruiksscenario&#39;s zijn van een ontdekkingstool veranderd in een samenwerkingskader. Met deze playbooks kunt u nu uw eigen playbooks samenstellen, beheren en met verschillende organisaties delen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} Maak en deel uw eigen playbooks | Met een nieuw kader voor het creëren van playbooks kunt u uw eigen playbooks voor gebruiksscenario&#39;s maken, beheren en delen. Dit omvat ondersteuning voor het vastleggen van belangrijke metadata, het bewerken van trajectkaarten en het koppelen van relevante technische assets. U kunt playbooks binnen een organisatie delen om marketingbenaderingen te standaardiseren en consistentie te handhaven. |

{style="table-layout:auto"}

Als u wilt weten hoe u uw eigen playbooks kunt schrijven en delen, raadpleegt u het document [Uw eigen playbooks schrijven en delen](/help/use-case-playbooks/playbooks/author.md).

Raadoleeg het [overzicht van playbooks voor gebruiksscenario&#39;s](/help/use-case-playbooks/playbooks/overview.md) voor meer informatie. Dit is een overzicht van de functionaliteit van playbooks, hun doel en een demonstratie van begin tot eind, met inbegrip van hoe u instanties kunt maken en gegenereerde assets in andere sandboxomgevingen kunt invoeren.
