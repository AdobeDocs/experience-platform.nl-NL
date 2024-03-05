---
title: Aanbevolen werkwijzen voor gegevensbeheerlicenties
description: Meer informatie over best practices en tools die u kunt gebruiken om uw licentierechten beter te beheren met Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---

# Aanbevolen best practices voor licentierechten voor gegevensbeheer

Adobe Experience Platform is een open systeem dat uw gegevens omzet in robuuste klantprofielen die in real time worden bijgewerkt en op AI gebaseerde inzichten gebruiken om u te helpen de juiste ervaringen over elk kanaal te leveren. U kunt gegevens van verschillende typen, volumes en historie invoeren naar het Experience Platform met behulp van bronnen. Vervolgens kunt u die gegevens gebruiken voor gevallen die variëren van segmentatie en personalisatie tot analyse en machinaal leren.

Platform biedt licenties waarmee u kunt bepalen hoeveel profielen u kunt maken en hoeveel gegevens u kunt invoeren. Gezien de capaciteit om om het even welke bron, volume, of geschiedenis van gegevens in te voeren, is het mogelijk om uw vergunningsrechten te overschrijden aangezien uw gegevensvolumes groeien.

In dit document worden aanbevolen procedures beschreven en gereedschappen waarmee u uw licentierechten beter kunt beheren met Adobe Experience Platform.

## Adobe Experience Platform-gegevensopslag

Experience Platform bestaat voornamelijk uit twee gegevensopslagplaatsen: de [!DNL data lake] en de profielopslag.

De **[!DNL data lake]** hoofdzakelijk de volgende doeleinden dienen:

* fungeert als testgebied voor gegevens aan boord in Experience Platform;
* fungeert als de gegevensopslag op lange termijn voor alle gegevens van het Experience Platform;
* Hiermee worden gebruiksgevallen ingeschakeld, zoals gegevensanalyse en gegevenswetenschap.

De **Profielenarchief** is waar klantprofielen worden gecreeerd en hoofdzakelijk de volgende doeleinden dienen:

* treedt op als gegevensopslag voor profielen die worden gebruikt om ervaring in real time te steunen;
* Laat gebruiksgevallen zoals segmentatie, activering, en verpersoonlijking toe.

>[!NOTE]
>
>Uw toegang tot de [!DNL data lake] kan afhankelijk zijn van de SKU die u hebt aangeschaft. Neem contact op met uw Adobe voor meer informatie over SKU&#39;s.

## Licentiegebruik {#license-usage}

Wanneer u Experience Platform vergunning geeft, wordt u voorzien van de toestemmingen van het vergunningsgebruik die afhankelijk van SKU variëren:

**[!DNL Addressable Audience]** - het totale aantal klantprofielen dat contractueel in Experience Platform is toegestaan, met inbegrip van zowel bekende als pseudoniem.

**[!DNL Profile Richness]** - de gemiddelde grootte van uw profielgegevens in Experience Platform. U kunt uw [!DNL Profile Richness] aanschaf van een rijkeringspakket.

De [!DNL Profile Richness] De metrische waarde is afhankelijk van de licentie die u hebt aangeschaft. Er zijn twee berekeningen voor [!DNL Profile Richness] beschikbaar:

* De som van alle productiegegevens die op elk moment in Adobe Real-time Customer Data Platform zijn opgeslagen (d.w.z. het realtime profiel en de identiteitsservice van de klant), gedeeld door de [!DNL Addressable Audience];
* De som van alle gegevens die in het platform zijn opgeslagen (met inbegrip van, maar niet beperkt tot, de [!DNL data lake], Real-Time Klantprofiel en Identiteitsservice) op elk gewenst moment en alle gegevens die u in de afgelopen 12 maanden via (in plaats van binnen op te slaan) Platform hebt gestreamd, gedeeld door de [!DNL Addressable Audience].

De beschikbaarheid van deze cijfers en de specifieke definitie van elk van deze cijfers variëren afhankelijk van de licenties die uw organisatie heeft aangeschaft.

## Het gebruiksdashboard voor licenties

De gebruikersinterface van Adobe Experience Platform biedt een dashboard waarmee u een momentopname kunt bekijken van de licentiegegevens van uw organisatie voor Platform. De gegevens in het dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de momentopname is gemaakt. De momentopname is geen benadering of een steekproef van gegevens, en het dashboard werkt niet in real time bij.

Zie de handleiding voor meer informatie over [het gebruiken van het dashboard van het vergunningsgebruik op Platform UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Aanbevolen werkwijzen voor gegevensbeheer

In de volgende secties worden aanbevolen procedures beschreven voor een beter gegevensbeheer.

### Uw gegevens begrijpen

Niet alle gegevens zijn hetzelfde in Adobe Experience Platform. Sommige gegevens kunnen dicht, maar laag in waarde zijn, terwijl andere gering, maar hoog in waarde kunnen zijn. Sommige gegevens kunnen hun waarde verliezen zodra ze zijn gegenereerd, terwijl andere voor maanden, zo niet voor jaren, waardevol kunnen zijn.

U moet rekening houden met drie dimensies om de waarde van uw gegevens te begrijpen:

| Dimension | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Volume | Geeft de hoeveelheid en het totaal van de opgenomen gegevens aan. | Web klikt - hoog in volume en gematigd in trouw. De waarde kan snel afnemen. |
| Timespan | Vertegenwoordigt de tijdsduur dat ingesloten gegevens waardevol blijven. | Offlineaankopen - gematigd in volume en getrouwheid, maar kunnen gedurende lange perioden waardevol zijn. |
| Getrouwheid | Vertegenwoordigt hoe rijk de gegevens met informatie zijn. | Klantenaccounts: laag volume, maar hoog getrouw. Kan waardevol zijn na het leven van een klant. |

### Gereedschappen voor gegevensbeheer {#data-management-tools}

Er zijn twee centrale scenario&#39;s om in overweging te nemen wanneer u ervoor zorgt dat uw gegevensgebruik binnen uw grenzen van de vergunningsbevoegdheid blijft:

### Welke gegevens moeten in Platform worden gebracht?

Gegevens kunnen in één of meerdere systemen in Platform worden ingevoerd, namelijk de [!DNL data lake] en/of het archief met profielen. Dit betekent dat er in beide systemen verschillende gegevens kunnen bestaan voor verschillende gebruiksgevallen. U kunt bijvoorbeeld historische gegevens in het dialoogvenster [!DNL data lake], maar niet in de profielopslag. U kunt selecteren welke gegevens naar de opslag van het Profiel moeten verzenden door een dataset voor de opname van het Profiel toe te laten.

>[!NOTE]
>
>Uw toegang tot de [!DNL data lake] kan afhankelijk zijn van de SKU die u hebt aangeschaft. Neem contact op met uw Adobe voor meer informatie over SKU&#39;s.

### Welke gegevens moeten worden bewaard?

U kunt zowel gegevensinnamefilters als vervalregels toepassen om gegevens te verwijderen die verouderd zijn geworden voor uw gebruiksgevallen. Gewoonlijk verbruikt gedragsgegevens (zoals analysegegevens) aanzienlijk meer opslag dan recordgegevens (zoals CRM-gegevens). Veel platformgebruikers hebben bijvoorbeeld een toename van maximaal 90% van de profielen die alleen worden gevuld met gedragsgegevens, in vergelijking met recordgegevens. Daarom is het beheren van uw gedragsgegevens essentieel om naleving binnen uw vergunningsrechten te verzekeren.

U kunt een aantal tools gebruiken om binnen uw gebruiksrechten voor licenties te blijven:

* [Inktfilters](#ingestion-filters)
* [Profielenarchief](#profile-service)

### Identiteitsservice en adresseerbaar publiek {#identity-service}

Identiteitsgrafieken tellen niet voor uw totale adresseerbare publieksrecht omdat het adresseerbare publiek naar uw totale aantal klantenprofielen verwijst.

Limieten voor identiteitsgrafieken kunnen echter gevolgen hebben voor het adresseerbare publiek als gevolg van het splitsen van identiteiten. Als bijvoorbeeld de oudste ECID uit de grafiek wordt verwijderd, blijft ECID bestaan in Real-Time klantprofiel als een pseudoniem profiel. U kunt instellen [Verlopen van Pseudoniem-profielgegevens](../../profile/pseudonymous-profiles.md) om dit gedrag te omzeilen. Lees voor meer informatie de [handleidingen voor identiteitsservicegegevens](../../identity-service/guardrails.md).

### Inktfilters {#ingestion-filters}

Met insluitingsfilters kunt u alleen de gegevens invoeren die nodig zijn voor uw gebruik en kunt u alle gebeurtenissen die niet vereist zijn, filteren.

| Inslikken, filter | Beschrijving |
| --- | --- |
| Adobe Audience Manager-bronfiltering | Wanneer u een Adobe Audience Manager-bronverbinding maakt, kunt u kiezen welke segmenten en kenmerken u in de [!DNL data lake] en Real-Time Klantprofiel, in plaats van de gegevens van de Audience Manager in zijn geheel in te voeren. Zie de handleiding op [een Audience Manager-bronverbinding maken](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) voor meer informatie . |
| Adobe Analytics Data Prep | U kunt [!DNL Data Prep] functionaliteit wanneer het creëren van een bron van de Analyse verbinding om uit gegevens uit te filtreren die niet voor uw gebruiksgevallen wordt vereist. Doorheen [!DNL Data Prep], kunt u definiëren welke kenmerken/kolommen naar Profiel moeten worden gepubliceerd. U kunt ook voorwaardelijke instructies opgeven om Platform te laten weten of gegevens naar verwachting worden gepubliceerd in het profiel of alleen in het dialoogvenster [!DNL data lake]. Zie de handleiding op [een verbinding met een bron voor Analytics maken](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie . |
| Ondersteuning voor het in- en uitschakelen van gegevenssets voor profiel | Om gegevens in het Profiel van de Klant in real time in te voeren, moet u een dataset voor gebruik in de opslag van het Profiel toelaten. Hiermee voegt u [!DNL Addressable Audience] en [!DNL Profile Richness] toeslagrechten. Zodra een dataset niet meer voor de gebruiksgevallen van het klantenprofiel wordt vereist, kunt u de integratie van die dataset aan Profiel onbruikbaar maken om ervoor te zorgen dat uw gegevens vergunning volgzaam blijven. Zie de handleiding op [het toelaten van en het onbruikbaar maken van datasets voor Profiel](../../catalog/datasets/enable-for-profile.md) voor meer informatie . |
| Web SDK en Mobile SDK-gegevensuitsluiting | Er zijn twee soorten gegevens die door Web en Mobiele SDK worden verzameld: gegevens die automatisch en gegevens worden verzameld die uitdrukkelijk door uw ontwikkelaar worden verzameld. Om de naleving van de licentie beter te beheren, kunt u automatische gegevensverzameling in de configuratie van de SDK uitschakelen via de context-instelling. Aangepaste gegevens kunnen ook worden verwijderd of niet worden ingesteld door de ontwikkelaar. |
| Server-kant die gegevensuitsluiting door:sturen | Als u gegevens naar Platform verzendt gebruikend server-zij door:sturen, kunt u uitsluiten welke gegevens door of de afbeelding in een regelactie te verwijderen worden verzonden om het over alle gebeurtenissen uit te sluiten, of door voorwaarden aan de regel toe te voegen zodat de gegevens slechts voor bepaalde gebeurtenissen in brand steken. Zie de documentatie op [gebeurtenissen en omstandigheden](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if) voor meer informatie . |
| Gegevens filteren op bronniveau | U kunt logische en vergelijkingsexploitanten gebruiken om rij-vlakke gegevens van uw bronnen te filtreren alvorens een verbinding tot stand te brengen en gegevens aan Experience Platform op te nemen. Lees voor meer informatie de handleiding op [het filtreren van rij-vlakke gegevens voor een bron gebruikend [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Profielenarchief {#profile-service}

De opslag van het Profiel is samengesteld uit de volgende componenten:

| Profielopslagcomponent | Beschrijving |
| --- | --- |
| Profielfragmenten | Elk klantprofiel bestaat uit meerdere **profielfragmenten** die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige **profielfragmenten** verwant met die enige klant die in veelvoudige datasets verschijnt. Wanneer deze fragmenten in Platform worden opgenomen, worden ze aan elkaar gehecht met behulp van de identiteitsgrafiek om één profiel voor die klant te maken. **Profielfragmenten** bestaan uit een naamruimte van de identiteit als de id, met de bijbehorende recordgegevens en/of tijdreeksgegevens. |
| Opnamegegevens (kenmerken) | Een profiel is een weergave van een onderwerp, een organisatie of een individu, dat uit vele **Attributen** (ook bekend als **recordgegevens**). Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. **Gegevens opnemen** is gewoonlijk laag/matig in volume, maar waardevol voor lange periodes. |
| Gegevens uit tijdreeksen (gedrag) | **Gegevens uit tijdreeksen** biedt informatie over een gebruikersgedrag. Vertegenwoordigd door het standaard model van de Gegevens van de Ervaring van het Schema (XDM) [!DNL ExperienceEvent]Gegevens uit tijdreeksen kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. De waarde van gedrag kan in de loop der tijd afnemen. |
| Naamruimte (identiteiten) | Wanneer klantgegevens worden samengevoegd, worden deze samengevoegd tot één profiel door middel van het gebruik van **naamruimten** en de mogelijkheid om deze identiteiten bij elkaar te houden wanneer meer informatie over de gebruiker bekend wordt. Zie de [Overzicht van naamruimten](../../identity-service/features/namespaces.md) voor meer informatie . |

{style="table-layout:auto"}

#### Compositierapporten opslaan van profiel

Er zijn een aantal rapporten beschikbaar om u te helpen de samenstelling van de opslag van het Profiel begrijpen. Met deze rapporten kunt u geïnformeerde beslissingen nemen over hoe en waar u de vervaldatum van de Experience Event moet instellen om uw licentiegebruik beter te optimaliseren:

* **API voor gegevensset-overlap**: Toont de datasets bloot die het meest aan uw Adresseerbare Publiek bijdragen. U kunt dit rapport gebruiken om te bepalen welke [!DNL ExperienceEvent] datasets om een vervaldatum in te stellen voor. Zie de zelfstudie aan [het produceren van de dataset overlappend rapport](../../profile/tutorials/dataset-overlap-report.md) voor meer informatie .
* **API voor overlappen van identiteiten**: Hiermee wordt de naamruimte van de identiteit weergegeven die het meest bijdraagt aan het adresseerbare publiek. Zie de zelfstudie aan [het genereren van het overlappingsrapport voor de identiteit](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) voor meer informatie .
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Verlopen van gegevens van pseudoniem profiel {#pseudonymous-profile-expirations}

Op deze manier kunt u automatisch schijnbare profielen uit het profielarchief verwijderen. Lees voor meer informatie over deze functie de [Overzicht van de vervaldatum van Pseudoniem-profielgegevens](../../profile/pseudonymous-profiles.md).

#### Verlopen van gebeurtenissen beleven {#event-expirations}

Dit vermogen staat u toe om gedragsgegevens uit een profiel-toegelaten dataset automatisch te verwijderen die niet meer waardevol voor uw gebruiksgevallen is. Zie het overzicht op [Verlopen van gebeurtenissen beleven](../../profile/event-expirations.md) voor details over hoe dit proces werkt zodra het voor een dataset wordt toegelaten.

## Overzicht van best practices voor compatibiliteit met het gebruik van licenties {#best-practices}

Hieronder volgt een lijst met aanbevolen tips die u kunt volgen om ervoor te zorgen dat u zich beter houdt aan uw gebruiksrechten voor licenties:

* Gebruik de [licentiegebruiksdashboard](../../dashboards/guides/license-usage.md) om de trends van het klantengebruik te volgen en te controleren. Hierdoor kunt u eventuele overschrijdingen die zich kunnen voordoen, overtreffen.
* Configureren [innamefilters](#ingestion-filters) door de gebeurtenissen te identificeren die voor uw segmentatie en verpersoonlijkingsgebruiksgevallen worden vereist. Op deze manier kunt u alleen belangrijke gebeurtenissen verzenden die vereist zijn voor uw gebruiksgevallen.
* Zorg ervoor dat u alleen [ingeschakelde gegevenssets voor profiel](#ingestion-filters) die voor uw segmentatie en verpersoonlijkingsgebruiksgevallen worden vereist.
* Configureren [Verlopen van gebeurtenissen beleven](#event-expirations) en [Verlopen van gegevens van pseudoniem profiel](#pseudonymous-profile-expirations) voor hoogfrequente gegevens zoals webgegevens.
* Controleer regelmatig de [Profielsamenstellingsrapporten](#profile-store-composition-reports) om uw de opslagsamenstelling van het Profiel te begrijpen. Op deze manier kunt u de gegevensbronnen begrijpen die het meest bijdragen aan het gebruik van uw licentie.

## Overzicht en beschikbaarheid van functies {#feature-summary}

De beste praktijken en hulpmiddelen die in dit document worden geschetst zullen u helpen uw gebruik van de vergunningsbevoegdheid binnen Adobe Experience Platform beter beheren. Dit document wordt bijgewerkt wanneer extra functies worden vrijgegeven om alle klanten van het Experience Platform zichtbaar en bestuurbaar te maken.

In de volgende tabel wordt de lijst met momenteel beschikbare functies weergegeven, zodat u uw gebruiksrechten voor licenties beter kunt beheren.

| Functie | Beschrijving |
| --- | --- |
| [Datasets voor profiel in-/uitschakelen](../../catalog/datasets/user-guide.md) | Schakel gegevenssetinvoer in of uit in realtime-klantprofiel. |
| [Verlopen van gebeurtenissen beleven](../../profile/event-expirations.md) | Pas een vervaltijd voor alle gebeurtenissen toe die in een profiel-Toegelaten dataset worden opgenomen. Neem contact op met het accountteam of de klantenservice van de Adobe om deze functie in te schakelen. |
| [Adobe Analytics Data Prep-filters](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Toepassen [!DNL Kafka] filters om onnodige gegevens uit te sluiten van inname |
| [Adobe Audience Manager-bronverbindingsfilters](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Bronverbindingsfilters van Audience Manager toepassen om onnodige gegevens uit te sluiten van inname |
| [Gegevensfilters voor doorsturen van gebeurtenissen](../../tags/ui/event-forwarding/overview.md) | Server-kant toepassen [!DNL Kafka] filters om onnodige gegevens uit te sluiten van inname.  Zie de documentatie op [tagregels](../../tags/ui/managing-resources/rules.md) voor aanvullende informatie. |
| [Gebruikersinterface van dashboard voor licentiegebruik](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Bekijk een momentopname van de licentiegerelateerde gegevens van uw organisatie voor Experience Platform |
| [API voor gegevensset-overlap](../../profile/tutorials/dataset-overlap-report.md) | Output de datasets die het meest aan uw Adresseerbare Publiek bijdraagt |
| [API voor overlappen van identiteiten](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Hiermee worden de naamruimten uitgevoerd die het meest bijdragen aan uw adresseerbare publiek |

{style="table-layout:auto"}
