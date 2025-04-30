---
title: Aanvullende informatie van april 2025 voor Adobe Experience Platform
description: Aanvullende informatie van april 2025 voor Adobe Experience Platform.
source-git-commit: d2ee1adb031af83569f7b226a8881297423fc257
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 28%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor opmerkingen bij andere Adobe Experience Platform-toepassingen:
>
>- [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [ Adobe Journey Optimizer B2B ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [ Real-Time CDP Collaboration ](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 29 april 2025**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [Experience League](#experience-league)
- [Bestemmingen](#destinations)
- [Experience Data Model](#xdm)
- [Identiteitsservice](#identity)
- [Query-service](#query-service)
- [Realtime-klantenprofiel](#profile)
- [Bronnen](#sources)

## Experience League {#experience-league}

Experience League is een uitgebreid trainingsplatform dat u helpt uw vaardigheden met Adobe-producten te verbeteren. Het biedt een verscheidenheid van middelen, met inbegrip van cursussen, documentatie, communautaire pagina&#39;s, gebeurtenissen, en toegang tot certificatie aan.

| Functie | Beschrijving |
| --- | --- |
| Persoonlijke homepage | De toegang en past uw gepersonaliseerde homepage op [ Experience League ](https://experienceleague.adobe.com/en/home#) aan. Meld u aan met uw Adobe-gebruikersgegevens en selecteer vervolgens **[!UICONTROL Experience League]** in het bovenste menu om uw leerervaring te optimaliseren: <ul><li>**Bladwijzers**: Gebruik de [!UICONTROL Bookmarks] eigenschap om uw favoriete middelen op één plaats te bewaren en te verzamelen. U kunt diverse inhoud opslaan, zoals afspeellijsten, artikelen en zelfstudies.</li><li>**pas uw het leren** aan: Verbeter uw het leren ervaring door uw profiel van Experience League met de rollen, de industrieën, de producten, en het ervaringsniveau bij te werken dat het beste uw behoeften aanpast.</li><li>**Aanbevelingen**: De het leren van mening adviseerde inhoud die op uw recente activiteit wordt gebaseerd.</li><li>**onlangs bekeken**: Gebruik de [!UICONTROL Recently viewed] sectie om snel terug naar onlangs bekeken inhoud zoals documentatie en video&#39;s te navigeren.</li><li>**Lerende middelen**: Gebruik het [!UICONTROL All learning resources] paneel om aan leerprogramma&#39;s, documentatie, gemeenschap, gebeurtenissen, en certificatie te navigeren.</li><li>**wat** nieuw is: Bekijk de [!UICONTROL What's new] sectie voor een stroom van de recentste inhoud op Experience League.</li><li>**Controle voorbij gebeurtenissen op bestelling**: Bekijk eerder geregistreerde levende stromen op productspots, gebruiksgevallen, en leerprogramma&#39;s met de [!UICONTROL Watch past events on-demand] sectie.</li></ul><br> ![ Persoonlijke homepage op Experience League.](../2025/assets/april/personalized-home-page.png " Persoonlijke homepage op Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [ Marketo Engage Person Sync ](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe heeft het doel van [!DNL Marketo Engage Person Sync] bijgewerkt om een probleem op te lossen dat van invloed was op klanten wanneer er meerdere e-mails in de identiteitskaart stonden. |

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| **wekelijks** en **Maandelijks** het plannen opties voor volledige dossieruitvoer | U kunt de volledige dossieruitvoer voor mensen en het potentiële publiek nu plannen op een wekelijkse of maandelijkse basis wanneer het activeren aan op dossier-gebaseerde bestemmingen van de cloudopslag. [ las meer ](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) over het plannen van opties. |

{style="table-layout:auto"}

**Bevestigingen, verhogingen, en andere aankondigingen** {#destinations-fixes-and-enhancements}

- **Handhaving van gegevensset de einddata van de uitvoer vertraagde aan 1 September, 2025**\
  Als deel van de [ Versie van september 2024 ](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality), plaatste Adobe een standaardeinddatum van 1 Mei, 2025, voor om het even welke gegevensset uitgevoerde dataflows die *vóór die versie* worden gecreeerd. Adobe breidt nu deze handhavingsdeadline tot **1 September, 2025** uit om klanten van extra tijd te voorzien om hun programma&#39;s bij te werken. Verwijs naar de het plannen sectie van het [ de leerprogramma&#39;s van de uitvoerdatasets ](../../destinations/ui/export-datasets.md#schedule-dataset-export) voor informatie over hoe te om de einddatum van een datasetuitvoer dataflow uit te geven.

- **Verbeterde behandeling van ontbroken overdrachten SFTP voor LiveRamp onboarding**\
  Adobe heeft een moeilijke situatie voor een kwestie uitgevoerd die dossieruitvoer aan [ LiveRamp Onboarding ](/help/destinations/catalog/advertising/liveramp-onboarding.md) bestemming via SFTP beïnvloedt. Soms zijn bestandsoverdrachten mislukt als gevolg van voorbijgaande serverproblemen en zijn tijdelijke bestanden van mislukte pogingen op de server gebleven. Deze onbewerkbare bestanden blokkeerden volgende pogingen, omdat Adobe geen toestemming had om deze te overschrijven.\
  Als het tijdelijke bestand niet kan worden verwijderd bij een nieuwe poging, genereert Adobe met de fix een nieuw bestand met het achtervoegsel `attempt2` , om ervoor te zorgen dat het nieuwe bestand correct wordt voltooid.

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte componenten XDM**

| Functie | Beschrijving |
| --- | --- |
| Tekenreeksvelden ontvangen een minimumwaarde van één | Nieuwe tekenreeksvelden krijgen standaard een minimale lengte van één. Null-waarden voor niet-vereiste velden zijn nog steeds acceptabel. Voor meer informatie over beste praktijken, lees de gids over [ beste praktijken voor gegevens modelleren ](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Raadpleeg het [XDM-systeemoverzicht](../../xdm/home.md) voor meer informatie over XDM in Experience Platform.

## Identiteitsservice {#identity}

Met Identity Service van Adobe Experience Platform krijgt u een uitgebreid beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen, zodat u in real-time een impactvolle, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE  Beperkte Beschikbaarheid ]{type=Informative} [!DNL Identity Graph Linking Rules] | De Regels van de Vereniging van de Grafiek van de identiteit zijn nu in Beperkte Beschikbaarheid, en kunnen door alle klanten in ontwikkelingszandbakken worden betreden. <ul><li>**de vereisten van de Activering**: De eigenschap zal inactief blijven tot u vormt en uw [!DNL Identity Settings] bewaart. Zonder deze configuratie, zal het systeem normaal, zonder veranderingen in gedrag blijven werken.</li><li>**Belangrijke nota&#39;s**: Tijdens deze Beperkte fase van de Beschikbaarheid, kan de segmentatie van Edge onverwachte resultaten van het segmentlidmaatschap veroorzaken. Streaming en batchsegmentatie functioneren echter naar behoren.</li><li>**Volgende stappen**: Voor informatie over hoe te om deze eigenschap in productiestanddozen toe te laten, gelieve uw Adobe accountteam te contacteren.</li></ul> |

{style="table-layout:auto"}

Voor meer informatie, lees de [[!DNL Identity Graph Linking Rules]  documentatie ](../../identity-service/identity-graph-linking-rules/overview.md).

## Query-service {#query-service}

Voer query&#39;s uit op gegevens in het Adobe Experience Platform-data lake met behulp van standaard SQL met Query Service. Combineer naadloos datasets en genereer nieuwe op basis van de queryresultaten om rapportage, datawetenschapworkflows of opname in het realtimeklantprofiel mogelijk te maken. U kunt bijvoorbeeld de gegevens van de klantentransactie samenvoegen met de gedragsgegevens om hoogwaardige doelgroepen te identificeren voor gerichte marketingcampagnes.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| SQL-publiek overschrijven | Vernieuw het publiekslidmaatschap door bestaande profielen met de resultaten van een nieuwe SQL vraag te beschrijven. Hierdoor kunt u het dynamische publiek efficiënter beheren door verouderde records te verwijderen en bijgewerkte records in één bewerking in te voegen. Voor meer informatie, zie de [ SQL gids van de publieksuitbreiding ](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Zoekresultaten downloaden en kopiëren | [ de vraagresultaten van de Download direct van de Redacteur van de Vraag ](../../query-service/ui/overview.md#download-query-results) als CSV, XLSX, of JSON- dossiers, of [ exemplaarresultaten aan uw klembord ](../../query-service/ui/overview.md#copy-results) als komma-gescheiden waarden (CSV) voor snel gebruik in spreadsheettoepassingen zoals Excel. Deze verbeteringen stroomlijnen de workflows voor offline analyse, rapportage en gegevensvalidatie. |
| Zoekresultaten op volledig scherm weergeven | [ de vraagresultaten van de Voorproef in een volledig-schermdialoog ](../../query-service/ui/overview.md#view-results) om leesbaarheid te verbeteren, gemakkelijk grote datasets af te tasten, en rijen voor het kopiëren te selecteren. De weergave Volledig scherm biedt een aanpasbare rasterlay-out waarmee u brede tabellen en gedetailleerde uitvoer efficiënter kunt bekijken. |
| Verbeterde kolomselectie in modelvoorspelling | Selecteer specifieke kolommen en pas aliassen toe gebruikend de uitgebreide `model_predict` syntaxis. Hiermee haalt u tussentijdse voorspellingsresultaten op, zoals eigenschapvectoren en kansscores. Voor de verbeterde selectie is activering van een functiemarkering vereist. Zie [ documentatie van de modellevenscyclus ](../../query-service/advanced-statistics/models.md#select-specific-output-fields) voor syntaxisvoorbeelden en details van de eigenschapvlag. |
| Modelvoorspellingsuitvoer opslaan met CREATE TABLE en INVOEGEN IN | [ sparen geselecteerde voorspelling output in nieuwe lijsten gebruikend CREEER LIJST ALS UITGEZOCHT of neem in bestaande lijsten op gebruikend TUSSENVOEGSEL IN UITGEZOCHT ](../../query-service/advanced-statistics/models.md#predict). Als de verbeterde kolomselectie wordt toegelaten, kunnen de middenresultaten zoals eigenschapvectoren en de waarschijnlijkheid ook naast definitieve voorspellingen worden voortgeduurd. Voor gebruiksvoorbeelden, verwijs naar de [ SQL syntaxisdocumentatie ](../../query-service/sql/syntax.md#create-table-as-select). |

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../../query-service/home.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

| Functie | Beschrijving |
| ------- | ----------- |
| Vervaldatum van pseudoniem profielgegevens | Het verlopen van uw Pseudoniem-profielgegevens beheren in het dashboard Profiel. Om meer over deze eigenschap en Pseudoniem Profielen te leren, te lezen gelieve de [ Pseudoniem gids van de gegevensvervalsing van het Profiel ](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

Voor meer informatie over Real-Time Customer Profile, raadpleegt u het [overzicht van profielen](../../profile/home.md)

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Nieuwe bronnen**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | De [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) -bron is nu beschikbaar. Gebruik deze bron om gegevens over gebruikersprofielen van [!DNL Algolia] naar Experience Platform te brengen. U kunt deze gegevens dan gebruiken om de betrokkenheid van gebruikers, conversietarieven, en algemene klantenervaring te verbeteren door krachtige onderzoeksoplossingen voor websites, e-commerceplatforms, en toepassingen te verstrekken. Voor meer informatie, leest de gids op hoe te [  [!DNL Algolia User Profiles]  gegevens aan Experience Platform ](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md) innemen. |
| [!BADGE  Beta ]{type=Informative} API steun voor [!DNL Azure Databricks] | De [!DNL Azure Databricks] -bron is nu beschikbaar in de API. Gebruik de [!DNL Flow Service] API om uw [!DNL Databricks] -account te verbinden en uw [!DNL Databricks] -gegevens naar Experience Platform te brengen. Lees de documentatie bij [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md) voor meer informatie. |

{style="table-layout:auto"}

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte XDM-velden voor het opnemen van Streaming Media-gegevens in Experience Platform. | De nieuwe XDM-veldgroep, `mediaReporting` , is nu beschikbaar voor het opnemen van Streaming Media-gegevens via de Adobe Analytics-bron in Experience Platform. Dit veld vervangt het veld `media.mediaTimed` .</br> <br> Gedurende een overgangsperiode van drie maanden, zal gegevensinvoer op `media.mediaTimed` gebieden verdergaan. Eind juli 2025 zijn de velden `media.mediaTimed` echter volledig verouderd en niet meer zichtbaar in de gebruikersinterface van het Experience Platform-schema. Gegevens worden alleen verzonden met behulp van de velden `mediaReporting` .</br><br> als u de bron van Analytics hebt uitgevoerd om het stromen gegevens van Media in Platform vóór 22 April, 2025 te verzamelen, dan moet u uw bestaande configuraties migreren om gegevens te verzenden gebruikend de nieuwe gebiedsgroep. Deze migratie moet eind juli 2025 zijn voltooid. Neem contact op met uw Adobe-accountteam voor ondersteuning van migratie. |
| Nieuwe verificatietypen voor [!DNL MariaDB] en [!DNL PostgreSQL] | U kunt nu basisverificatie gebruiken om uw [!DNL MariaDB] - en [!DNL PostgreSQL] -bronnen op Experience Platform te verifiëren. Lees de volgende documentatie voor meer informatie: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Ondersteuning voor filteren op rijniveau voor [!DNL Amazon Redshift] | U kunt filtermogelijkheden op rijniveau gebruiken voor uw [!DNL Amazon Redshift] -gegevens op Experience Platform. Voor meer informatie, lees de gids over [ het filtreren rij-vlakke gegevens voor bronnen in API ](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).
