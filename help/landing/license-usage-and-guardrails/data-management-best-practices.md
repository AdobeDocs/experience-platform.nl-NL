---
title: Aanbevolen werkwijzen voor gegevensbeheerlicenties
description: Meer informatie over best practices en tools die u kunt gebruiken om uw licentierechten beter te beheren met Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 1%

---

# Aanbevolen best practices voor licentierechten voor gegevensbeheer

Adobe Experience Platform is een open systeem dat uw gegevens omzet in robuuste klantprofielen die in real time worden bijgewerkt en op AI gebaseerde inzichten gebruiken om u te helpen de juiste ervaringen over elk kanaal te leveren. Met behulp van bronnen kunt u gegevens van verschillende typen, volumes en historie invoeren naar Experience Platform. Vervolgens kunt u die gegevens gebruiken voor gevallen die variëren van segmentatie en personalisatie tot analyse en machinaal leren.

Experience Platform biedt licenties waarmee u kunt bepalen hoeveel profielen u kunt maken en hoeveel gegevens u kunt invoeren. Gezien de capaciteit om om het even welke bron, volume, of geschiedenis van gegevens in te voeren, is het mogelijk om uw vergunningsrechten te overschrijden aangezien uw gegevensvolumes groeien.

In dit document worden aanbevolen procedures beschreven en gereedschappen waarmee u uw licentierechten beter kunt beheren met Adobe Experience Platform.

## Adobe Experience Platform-gegevensopslag

Experience Platform bestaat voornamelijk uit twee gegevensopslagruimten: de [!DNL data lake] - en de Profile Store.

De **[!DNL data lake]** heeft voornamelijk de volgende doelen:

* fungeert als testgebied voor gegevens aan boord in Experience Platform;
* fungeert als de gegevensopslag op lange termijn voor alle Experience Platform-gegevens;
* Hiermee worden gebruiksgevallen ingeschakeld, zoals gegevensanalyse en gegevenswetenschap.

De **opslag van het Profiel** is waar de klantenprofielen worden gecreeerd en hoofdzakelijk de volgende doeleinden dienen:

* treedt op als gegevensopslag voor profielen die worden gebruikt om ervaring in real time te steunen;
* Laat gebruiksgevallen zoals segmentatie, activering, en verpersoonlijking toe.

>[!NOTE]
>
>Uw toegang tot [!DNL data lake] kan afhankelijk zijn van de product-SKU die u hebt aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie over product-SKU&#39;s.

## Licentiegebruik {#license-usage}

Wanneer u Experience Platform een licentie geeft, krijgt u gebruiksrechten voor licenties die afhankelijk zijn van de SKU:

**[!DNL Addressable Audience]** - het totale aantal klantprofielen dat contractueel is toegestaan in Experience Platform, inclusief bekende en pseudoniem-profielen.

**[!DNL Total Data Volume]** - de totale hoeveelheid gegevens die beschikbaar is voor Adobe Experience Platform Profile Service voor gebruik in betrokkenheidsworkflows.

De beschikbaarheid van deze cijfers en de specifieke definitie van elk van deze cijfers variëren afhankelijk van de licenties die uw organisatie heeft aangeschaft.

## Het gebruiksdashboard voor licenties

De gebruikersinterface van Adobe Experience Platform biedt een dashboard waarmee u een momentopname kunt bekijken van de licentiegegevens van uw organisatie voor Experience Platform. De gegevens in het dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de momentopname is gemaakt. De momentopname is geen benadering of een steekproef van gegevens, en het dashboard werkt niet in real time bij.

Voor meer informatie, zie de gids op [ gebruikend het dashboard van het vergunningsgebruik op Experience Platform UI ](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

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

### Welke gegevens moeten in Experience Platform worden ingevoerd?

Gegevens kunnen in een of meerdere systemen in Experience Platform worden ingevoerd, namelijk in de [!DNL data lake] - en/of de Profile Store. Dit betekent dat er in beide systemen verschillende gegevens kunnen bestaan voor verschillende gebruiksgevallen. U kunt bijvoorbeeld historische gegevens in de [!DNL data lake] opslaan, maar niet in de Profile Store. U kunt selecteren welke gegevens naar de opslag van het Profiel moeten verzenden door een dataset voor de opname van het Profiel toe te laten.

>[!NOTE]
>
>Uw toegang tot [!DNL data lake] kan afhankelijk zijn van de product-SKU die u hebt aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie over product-SKU&#39;s.

### Welke gegevens moeten worden bewaard?

U kunt zowel gegevensinnamefilters als vervalregels toepassen om gegevens te verwijderen die verouderd zijn geworden voor uw gebruiksgevallen. Gewoonlijk verbruikt gedragsgegevens (zoals analysegegevens) aanzienlijk meer opslag dan recordgegevens (zoals CRM-gegevens). Veel Experience Platform-gebruikers hebben bijvoorbeeld een toename tot 90% van de profielen die alleen worden gevuld met gedragsgegevens, in vergelijking met recordgegevens. Daarom is het beheren van uw gedragsgegevens essentieel om naleving binnen uw vergunningsrechten te verzekeren.

U kunt een aantal tools gebruiken om binnen uw gebruiksrechten voor licenties te blijven:

* [Inktfilters](#ingestion-filters)
* [Profielenarchief](#profile-service)

### Identiteitsservice en adresseerbaar publiek {#identity-service}

Identiteitsgrafieken tellen niet voor uw totale adresseerbare publieksrecht omdat het adresseerbare publiek naar uw totale aantal klantenprofielen verwijst.

Limieten voor identiteitsgrafieken kunnen echter gevolgen hebben voor het adresseerbare publiek als gevolg van het splitsen van identiteiten. Als bijvoorbeeld de oudste ECID uit de grafiek wordt verwijderd, blijft ECID bestaan in Real-Time klantprofiel als een pseudoniem profiel. U kunt [ Pseudoniem de vervaltijden van profielgegevens ](../../profile/pseudonymous-profiles.md) plaatsen om dit gedrag te ontwijken. Voor meer informatie, lees de [ gidsen voor de gegevens van de Dienst van de Identiteit ](../../identity-service/guardrails.md).

### Inktfilters {#ingestion-filters}

Met insluitingsfilters kunt u alleen de gegevens invoeren die nodig zijn voor uw gebruik en kunt u alle gebeurtenissen die niet vereist zijn, filteren.

| Inslikken, filter | Beschrijving |
| --- | --- |
| Adobe Audience Manager-bronfiltering | Wanneer u een Adobe Audience Manager-bronverbinding maakt, kunt u kiezen welke segmenten en kenmerken u in het [!DNL data lake] en Real-Time Klantprofiel wilt opnemen in plaats van de Audience Manager-gegevens in hun geheel in te voeren. Zie de gids bij [ het creëren van een Audience Manager bronverbinding ](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) voor meer informatie. |
| Adobe Analytics Data Prep | U kunt [!DNL Data Prep] -functies gebruiken wanneer u een verbinding maakt met een bron voor Analytics om gegevens uit te filteren die niet vereist zijn voor uw gebruik. Via [!DNL Data Prep] kunt u definiëren welke kenmerken/kolommen naar Profiel moeten worden gepubliceerd. U kunt ook voorwaardelijke instructies opgeven om Experience Platform te laten weten of gegevens naar verwachting naar Profiel zullen worden gepubliceerd, of alleen naar de [!DNL data lake] . Zie de gids bij [ het creëren van een Analytics bronverbinding ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie. |
| Ondersteuning voor het in- en uitschakelen van gegevenssets voor profiel | Om gegevens in het Profiel van de Klant in real time in te voeren, moet u een dataset voor gebruik in de opslag van het Profiel toelaten. Hiermee voegt u uw rechten [!DNL Addressable Audience] en [!DNL Total Data Volume] toe. Zodra een dataset niet meer voor de gebruiksgevallen van het klantenprofiel wordt vereist, kunt u de integratie van die dataset aan Profiel onbruikbaar maken om ervoor te zorgen dat uw gegevens vergunning volgzaam blijven. Zie de gids op [ toelatend en onbruikbaar makend datasets voor Profiel ](../../catalog/datasets/enable-for-profile.md) voor meer informatie. |
| Web SDK en Mobile SDK gegevensuitsluiting | Er zijn twee soorten gegevens die door Web en Mobiele SDK worden verzameld: gegevens die automatisch en gegevens worden verzameld die uitdrukkelijk door uw ontwikkelaar worden verzameld. Voor een beter beheer van de naleving van de licentie kunt u automatische gegevensverzameling in de configuratie van de SDK uitschakelen via de context-instelling. Aangepaste gegevens kunnen ook worden verwijderd of niet worden ingesteld door de ontwikkelaar. |
| Server-kant die gegevensuitsluiting door:sturen | Als u gegevens naar Experience Platform verzendt gebruikend server-zij door:sturen, kunt u uitsluiten welke gegevens door of de afbeelding in een regelactie te verwijderen worden verzonden om het over alle gebeurtenissen uit te sluiten, of door voorwaarden aan de regel toe te voegen zodat de gegevens slechts voor bepaalde gebeurtenissen in brand steken. Zie de documentatie over [ gebeurtenissen en voorwaarden ](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if) voor meer informatie. |
| Gegevens filteren op bronniveau | U kunt logische operatoren en vergelijkingsoperatoren gebruiken om gegevens op rijniveau uit uw bronnen te filteren voordat u een verbinding maakt en gegevens aan Experience Platform toevoegt. Voor meer informatie, lees de gids over [ het filtreren rij-vlakke gegevens voor een bron gebruikend  [!DNL Flow Service]  API ](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Profielenarchief {#profile-service}

De opslag van het Profiel is samengesteld uit de volgende componenten:

| Profielopslagcomponent | Beschrijving |
| --- | --- |
| Profielfragmenten | Elk klantenprofiel is samengesteld uit veelvoudige **profielfragmenten** die zijn samengevoegd om één enkele mening van die klant te vormen. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige **profielfragmenten** met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Experience Platform worden opgenomen, worden ze aan elkaar gehecht met behulp van de identiteitsgrafiek om één profiel voor die klant te maken. {de fragmenten van het 0} Profiel **bestaan uit een identiteit namespace als herkenningsteken, met bijbehorende verslaggegevens en/of tijd-reeksgegevens.** |
| Opnamegegevens (kenmerken) | Een profiel is een vertegenwoordiging van een onderwerp, een organisatie of een individu, dat uit vele **Attributen** (ook als **wordt bekend verslaggegevens** wordt samengesteld). Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. **gegevens van het Verslag** is gewoonlijk laag/gematigd in volume, maar waardevol voor lange periodes. |
| Gegevens uit tijdreeksen (gedrag) | **tijd-reeksen gegevens** verstrekt informatie over een gebruikersgedrag. De gegevens uit tijdreeksen die worden vertegenwoordigd door het standaard XDM (Experience Data Model) van de schemaklasse [!DNL ExperienceEvent] kunnen gebeurtenissen beschrijven zoals items die worden toegevoegd aan een winkelwagentje, koppelingen waarop wordt geklikt en weergegeven video&#39;s. De waarde van gedrag kan in de loop der tijd afnemen. |
| Naamruimte (identiteiten) | Aangezien de klantengegevens samenkomen, wordt het samengevoegd in één enkel profiel door het gebruik van **identiteit namespaces**, en de capaciteit om deze identiteiten samen te kleven aangezien meer informatie over de gebruiker gekend wordt. Zie het [ overzicht van identiteitsnaamruimten ](../../identity-service/features/namespaces.md) voor meer informatie. |

{style="table-layout:auto"}

#### Compositierapporten opslaan van profiel

Er zijn een aantal rapporten beschikbaar om u te helpen de samenstelling van de opslag van het Profiel begrijpen. Met deze rapporten kunt u geïnformeerde beslissingen nemen over hoe en waar u de vervaldatum van de Experience Event moet instellen om uw licentiegebruik beter te optimaliseren:

* **Dataset overlapt Rapport API**: stelt de datasets bloot die het meest aan uw Adresseerbare Publiek bijdragen. U kunt dit rapport gebruiken om aan te geven voor welke [!DNL ExperienceEvent] -gegevenssets een vervaldatum moet worden ingesteld. Zie het leerprogramma bij [ het produceren van de datasetoverlapping rapport ](../../profile/tutorials/dataset-overlap-report.md) voor meer informatie.
* **Identiteitskaart overlap Rapport API**: Verleent de identiteit namespaces die het meest aan uw Adresseerbare Publiek bijdragen. Zie het leerprogramma op [ producerend het rapport van de identiteitsoverlap ](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) voor meer informatie.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Verlopen van gegevens van pseudoniem profiel {#pseudonymous-profile-expirations}

Met deze functie kunt u automatisch schijnbare profielen uit het profielarchief verwijderen. Voor meer informatie over deze eigenschap, te lezen gelieve het [ Pseudoniem overzicht van de gegevensvervalsing van het Profiel ](../../profile/pseudonymous-profiles.md).

#### Verlopen van gebeurtenissen beleven {#event-expirations}

Dit vermogen staat u toe om gedragsgegevens uit een profiel-toegelaten dataset automatisch te verwijderen die niet meer waardevol voor uw gebruiksgevallen is. Zie het overzicht op [ Verlopen van de Gebeurtenis van de Ervaring ](../../profile/event-expirations.md) voor details over hoe dit proces werkt zodra het voor een dataset wordt toegelaten.

## Overzicht van best practices voor compatibiliteit met het gebruik van licenties {#best-practices}

Hieronder volgt een lijst met aanbevolen tips die u kunt volgen om ervoor te zorgen dat u zich beter houdt aan uw gebruiksrechten voor licenties:

* Gebruik het [ dashboard van het vergunningsgebruik ](../../dashboards/guides/license-usage.md) om trends van het klantengebruik te volgen en te controleren. Hierdoor kunt u eventuele overschrijdingen die zich kunnen voordoen, overtreffen.
* Vorm [ innamefilters ](#ingestion-filters) door de gebeurtenissen te identificeren die voor uw segmentatie en het verpersoonlijkingsgebruik worden vereist gevallen. Op deze manier kunt u alleen belangrijke gebeurtenissen verzenden die vereist zijn voor uw gebruiksgevallen.
* Zorg ervoor dat u slechts [ toegelaten datasets voor profiel ](#ingestion-filters) hebt die voor uw segmentatie en verpersoonlijkingsgebruiksgevallen worden vereist.
* Vorm {de Verlopen van de Gebeurtenis van 0} Ervaring ](#event-expirations) en [ Pseudoniem de gegevensvervalsing van het Profiel ](#pseudonymous-profile-expirations) voor high-frequency gegevens zoals Webgegevens.[
* Controleer periodiek de [ Rapporten van de Samenstelling van het Profiel ](#profile-store-composition-reports) om uw de opslagsamenstelling van het Profiel te begrijpen. Op deze manier kunt u de gegevensbronnen begrijpen die het meest bijdragen aan het gebruik van uw licentie.

## Overzicht en beschikbaarheid van functies {#feature-summary}

De beste praktijken en hulpmiddelen die in dit document worden geschetst zullen u helpen uw gebruik van de vergunningsbevoegdheid binnen Adobe Experience Platform beter beheren. Dit document wordt bijgewerkt wanneer extra functies worden vrijgegeven om alle Experience Platform-klanten zichtbaar en bestuurbaar te maken.

In de volgende tabel wordt de lijst met momenteel beschikbare functies weergegeven, zodat u uw gebruiksrechten voor licenties beter kunt beheren.

| Functie | Beschrijving |
| --- | --- |
| [ laat/maakt Datasets voor Profiel ](../../catalog/datasets/user-guide.md) toe onbruikbaar | Schakel gegevenssetinvoer in of uit in realtime-klantprofiel. |
| [ Verlopen van de Gebeurtenis van de Ervaring ](../../profile/event-expirations.md) | Pas een vervaltijd voor alle gebeurtenissen toe die in een profiel-Toegelaten dataset worden opgenomen. Neem contact op met uw Adobe-accountteam of de klantenservice om deze functie in te schakelen. |
| [ Prep van Gegevens van Adobe Analytics filters ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | [!DNL Kafka] -filters toepassen om onnodige gegevens uit te sluiten van inname |
| [ de bronschakelaarfilters van Adobe Audience Manager ](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Audience Manager-bronverbindingsfilters toepassen om onnodige gegevens uit te sluiten van inname |
| [ Gebeurtenis die gegevensfilters ](../../tags/ui/event-forwarding/overview.md) door:sturen | Pas server-kant [!DNL Kafka] filters toe om onnodige gegevens van opname uit te sluiten.  Zie de documentatie over [ markeringsregels ](../../tags/ui/managing-resources/rules.md) voor extra informatie. |
| [ het Dashboard UI van het Gebruik van de Vergunning ](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Een momentopname weergeven van de licentiegegevens van uw organisatie voor Experience Platform |
| [ Dataset overlap Rapport API ](../../profile/tutorials/dataset-overlap-report.md) | Output de datasets die het meest aan uw Adresseerbare Publiek bijdraagt |
| [ Identiteitsoverlapping Rapport API ](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Hiermee worden de naamruimten uitgevoerd die het meest bijdragen aan uw adresseerbare publiek |

{style="table-layout:auto"}
