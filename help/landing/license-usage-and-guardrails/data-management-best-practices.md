---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;licentierechten;licenties;aanbevolen procedures
title: Aanbevolen werkwijzen voor gegevensbeheer
description: Meer informatie over de beste praktijken en tools die u kunt gebruiken om uw licentierechten beter te beheren met Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 5da2a6cfc9e9da6bbe6c6560577d22eed32c858c
workflow-type: tm+mt
source-wordcount: '2528'
ht-degree: 0%

---

# Aanbevolen best practices voor licentierechten voor gegevensbeheer

Adobe Experience Platform is een open systeem dat uw gegevens omzet in robuuste klantprofielen die in real time worden bijgewerkt en op AI gebaseerde inzichten gebruiken om u te helpen de juiste ervaringen over elk kanaal te leveren. U kunt gegevens van verschillende typen, volumes en historie invoeren naar het Experience Platform met behulp van bronnen. Vervolgens kunt u die gegevens gebruiken voor gevallen die variëren van segmentatie en personalisatie tot analyse en machinaal leren.

Platform biedt licenties waarmee u kunt bepalen hoeveel profielen u kunt maken en hoeveel gegevens u kunt invoeren. Gezien de capaciteit om om het even welke bron, volume, of geschiedenis van gegevens in te voeren, is het mogelijk om uw vergunningsrechten te overschrijden aangezien uw gegevensvolumes groeien.

In dit document worden aanbevolen procedures beschreven en gereedschappen waarmee u uw licentierechten beter kunt beheren met Adobe Experience Platform.

## Adobe Experience Platform-gegevensopslag

Experience Platform bestaat voornamelijk uit twee gegevensopslagplaatsen: de [!DNL Data Lake] en de profielopslag.

De **[!DNL Data Lake]** hoofdzakelijk de volgende doeleinden dienen:

* fungeert als testgebied voor gegevens aan boord in Experience Platform;
* fungeert als de gegevensopslag op lange termijn voor alle gegevens van het Experience Platform;
* Hiermee worden gebruiksgevallen ingeschakeld, zoals gegevensanalyse en gegevenswetenschap.

De **Profielopslag** is waar klantprofielen worden gecreeerd en hoofdzakelijk de volgende doeleinden dienen:

* treedt op als gegevensopslag voor profielen die worden gebruikt om ervaring in real time te steunen;
* Laat gebruiksgevallen zoals segmentatie, activering, en verpersoonlijking toe.

>[!NOTE]
>
>Uw toegang tot de [!DNL Data Lake] kan afhankelijk zijn van de SKU die u hebt aangeschaft. Neem voor meer informatie over product-SKU&#39;s contact op met uw Adobe-vertegenwoordiger.

## Licentiegebruik {#license-usage}

Wanneer u Experience Platform vergunning geeft, wordt u voorzien van de toestemmingen van het vergunningsgebruik die afhankelijk van SKU variëren:

**[!DNL Addressable Audience]** - het totale aantal klantprofielen dat contractueel in Experience Platform is toegestaan, met inbegrip van zowel bekende als pseudoniem.

**[!DNL Profile Richness]** - de gemiddelde grootte van uw profielgegevens in Experience Platform. U kunt uw [!DNL Profile Richness] aanschaf van een rijkeringspakket.

De [!DNL Profile Richness] De metrische waarde is afhankelijk van de licentie die u hebt aangeschaft. Er zijn twee berekeningen voor [!DNL Profile Richness] beschikbaar:

* De som van alle productiegegevens die in Real-time Customer Data Platform zijn opgeslagen (d.w.z. profielservice en identiteitsdienst) op elk moment, gedeeld door de [!DNL Addressable Audience];
* De som van alle gegevens die in het Platform zijn opgeslagen (inclusief, maar niet beperkt tot [!DNL Data Lake], de Dienst van het Profiel, en de Dienst van de Identiteit) op om het even welk punt in tijd en om het even welke gegevens die u door (in plaats van het opslaan binnen) Platform in de afgelopen 12 maanden stroomt, gedeeld door [!DNL Addressable Audience].

De beschikbaarheid van deze cijfers en de specifieke definitie van elk van deze cijfers variëren afhankelijk van de licenties die uw organisatie heeft aangeschaft.

## Het gebruiksdashboard voor licenties

De gebruikersinterface van Adobe Experience Platform biedt een dashboard waarmee u een momentopname van de licentiegegevens van uw organisatie voor Platform kunt bekijken. De gegevens in het dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de opname is gemaakt. De momentopname is geen benadering of een steekproef van gegevens, en het dashboard werkt niet in real time bij.

Zie de handleiding voor meer informatie over [het gebruiken van het dashboard van het vergunningsgebruik op Platform UI](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Aanbevolen werkwijzen voor gegevensbeheer

In de volgende secties worden aanbevolen procedures beschreven voor een beter gegevensbeheer.

### Gegevens begrijpen

Niet alle gegevens zijn hetzelfde in Adobe Experience Platform. Sommige gegevens kunnen dicht, maar laag in waarde zijn, terwijl andere gering, maar hoog in waarde kunnen zijn. Sommige gegevens kunnen waarde verliezen zodra ze zijn gegenereerd, terwijl andere maanden of jaren waardevol kunnen zijn.

U moet rekening houden met drie dimensies om de waarde van uw gegevens te begrijpen:

| Dimension | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Volume | Geeft de hoeveelheid en het totaal van opgenomen gegevens aan. | Web klikt - hoog in volume en gematigd in trouw. De waarde kan snel afnemen. |
| Timespan | Vertegenwoordigt de tijdsduur dat ingesloten gegevens waardevol blijven. | Offlineaankopen - gematigd in volume en getrouwheid, maar kunnen gedurende lange perioden waardevol zijn. |
| Getrouwheid | Vertegenwoordigt hoe rijk de gegevens met informatie zijn. | Klantenaccounts: laag volume, maar hoog getrouw. Kan waardevol zijn na het leven van een klant. |

### Gereedschappen voor gegevensbeheer {#data-management-tools}

Er zijn twee centrale scenario&#39;s om in overweging te nemen wanneer u ervoor zorgt dat uw gegevensgebruik binnen uw grenzen van de vergunningsbevoegdheid blijft:

### Welke gegevens moeten in Platform worden gebracht?

Gegevens kunnen in een of meer systemen in Platform worden ingevoerd, namelijk de [!DNL Data Lake] en/of de profielopslag. Dit betekent dat er in beide systemen verschillende gegevens kunnen bestaan voor verschillende gebruiksgevallen. U kunt bijvoorbeeld historische gegevens in het dialoogvenster [!DNL Data Lake], maar niet in de profielopslag. U kunt selecteren welke gegevens naar de Opslag van het Profiel moeten verzenden door een dataset voor de opname van het Profiel toe te laten.

>[!NOTE]
>
>Uw toegang tot de [!DNL Data Lake] kan afhankelijk zijn van de SKU die u hebt aangeschaft. Neem voor meer informatie over product-SKU&#39;s contact op met uw Adobe-vertegenwoordiger.

### Welke gegevens moeten worden bewaard?

U kunt zowel gegevensinnamefilters als vervalregels (ook wel &quot;TTL&quot; genoemd) toepassen om gegevens te verwijderen die verouderd zijn geworden voor uw gebruiksgevallen. Gewoonlijk verbruikt gedragsgegevens (zoals analysegegevens) aanzienlijk meer opslag dan recordgegevens (zoals CRM-gegevens). Veel gebruikers in het Platform hebben bijvoorbeeld een toename tot 90% van de profielen die alleen worden gevuld met gedragsgegevens, in vergelijking met recordgegevens. Daarom is het beheren van uw gedragsgegevens essentieel om naleving binnen uw vergunningsrechten te verzekeren.

U kunt een aantal tools gebruiken om binnen uw gebruiksrechten voor licenties te blijven:

* [Inktfilters](#ingestion-filters)
* [Profile Service TTL](#profile-service)

### Inktfilters {#ingestion-filters}

Met insluitingsfilters kunt u alleen de gegevens invoeren die nodig zijn voor uw gebruik en kunt u alle gebeurtenissen die niet vereist zijn, filteren.

| Inslikken, filter | Beschrijving |
| --- | --- |
| Adobe Audience Manager-bronfiltering | Wanneer u een Adobe Audience Manager-bronverbinding maakt, kunt u kiezen welke segmenten en kenmerken u in de [!DNL Data Lake] en de Dienst van het Profiel, eerder dan het opnemen van de gegevens van de Audience Manager in zijn geheel. Zie de handleiding op [een Audience Manager-bronverbinding maken](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) voor meer informatie . |
| Adobe Analytics Data Prep | U kunt [!DNL Data Prep] functionaliteit wanneer het creëren van een bron van de Analyse verbinding om uit gegevens uit te filtreren die niet voor uw gebruiksgevallen wordt vereist. Doorheen [!DNL Data Prep], kunt u definiëren welke kenmerken/kolommen naar Profiel moeten worden gepubliceerd. U kunt ook voorwaardelijke instructies opgeven om het Platform te laten weten of gegevens naar verwachting worden gepubliceerd in het profiel of alleen in het dialoogvenster [!DNL Data Lake]. Zie de handleiding op [een verbinding met een bron voor Analytics maken](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie . |
| Ondersteuning voor het in- en uitschakelen van gegevenssets voor profiel | Om gegevens in de Dienst van het Profiel in te voeren, moet u een dataset voor gebruik in de Opslag van het Profiel toelaten. Hiermee voegt u [!DNL Addressable Audience] en [!DNL Profile Richness] toeslagrechten. Zodra een dataset niet meer voor de gebruiksgevallen van het klantenprofiel wordt vereist, kunt u de integratie van die dataset aan Profiel onbruikbaar maken om ervoor te zorgen dat uw gegevens vergunning volgzaam blijven. Zie de handleiding op [het toelaten van en het onbruikbaar maken van datasets voor Profiel](../../catalog/datasets/enable-for-profile.md) voor meer informatie . |
| Web SDK en Mobile SDK-gegevensuitsluiting | Er zijn twee soorten gegevens die door Web en Mobiele SDK worden verzameld: gegevens die automatisch worden verzameld en gegevens die expliciet door de ontwikkelaar worden verzameld. Om de naleving van de licentie beter te beheren, kunt u automatische gegevensverzameling in de configuratie van de SDK uitschakelen via de context-instelling. Aangepaste gegevens kunnen ook worden verwijderd of niet worden ingesteld door de ontwikkelaar. Zie de handleiding op [basisbeginselen van SDK configureren](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) voor meer informatie . |
| Server-kant die gegevensuitsluiting door:sturen | Als u gegevens naar Platform verzendt gebruikend server-zij door:sturen, kunt u uitsluiten welke gegevens door of de afbeelding in een regelactie te verwijderen worden verzonden om het over alle gebeurtenissen uit te sluiten, of door voorwaarden aan de regel toe te voegen zodat de gegevens slechts voor bepaalde gebeurtenissen in brand steken. Zie de documentatie op [gebeurtenissen en omstandigheden](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

### Profielservice {#profile-service}

Met de TTL-functie (time-to-live) van de profielservice kunt u TTL toepassen op gegevens in de profielopslag. Hierdoor kan het systeem automatisch gegevens verwijderen die na verloop van tijd minder waarde hebben.

De profielopslag bestaat uit de volgende componenten:

| Profielopslagcomponent | Beschrijving |
| --- | --- |
| Profielfragmenten | Elk klantprofiel bestaat uit meerdere **profielfragmenten** die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige **profielfragmenten** verwant met die enige klant die in veelvoudige datasets verschijnt. Wanneer deze fragmenten in Platform worden opgenomen, worden ze aan elkaar gehecht met behulp van de identiteitsgrafiek om één profiel voor die klant te maken. **Profielfragmenten** bestaan uit een naamruimte van de identiteit als de id, met de bijbehorende recordgegevens en/of tijdreeksgegevens. |
| Opnamegegevens (kenmerken) | Een profiel is een weergave van een onderwerp, een organisatie of een individu, dat uit vele **Attributen** (ook bekend als **recordgegevens**). Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. **Gegevens opnemen** is gewoonlijk laag/matig in volume, maar waardevol voor lange periodes. |
| Gegevens uit tijdreeksen (gedrag) | **Gegevens uit tijdreeksen** biedt informatie over een gebruikersgedrag. Vertegenwoordigd door het standaard model van de Gegevens van de Ervaring van het Schema (XDM) [!DNL ExperienceEvent]Gegevens uit tijdreeksen kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. De waarde van gedrag kan in de loop der tijd afnemen. |
| Naamruimte (identiteiten) | Wanneer klantgegevens worden samengevoegd, worden deze samengevoegd tot één profiel door middel van het gebruik van **naamruimten** en de mogelijkheid om deze identiteiten bij elkaar te houden wanneer meer informatie over de gebruiker bekend wordt. Zie de [Overzicht van naamruimten](../../identity-service/namespaces.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

#### Compositierapporten voor profielopslag

Er zijn een aantal rapporten beschikbaar om u te helpen de samenstelling van de Opslag van het Profiel begrijpen. Deze rapporten helpen u geïnformeerde beslissingen te nemen over hoe en waar u uw profiel-TTL&#39;s instelt om uw licentiegebruik beter te optimaliseren:

* **API voor gegevensset-overlap**: Toont de datasets die het meest aan uw Adresseerbare Publiek bijdragen. U kunt dit rapport gebruiken om te bepalen welke [!DNL ExperienceEvent] datasets om TTL voor te plaatsen. Zie de zelfstudie aan [het produceren van de dataset overlappend rapport](../../profile/tutorials/dataset-overlap-report.md) voor meer informatie .
* **API voor overlappen van identiteiten**: Toont de identiteit namespaces die het meest aan uw Adresseerbare Publiek bijdragen. Zie de zelfstudie aan [het genereren van het overlappingsrapport voor de identiteit](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) voor meer informatie .
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous TTL for different time thresholds. You can use this report to identify which pseudonymous TTL threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### [!DNL ExperienceEvent] DataSet TTL {#dataset-ttl}

U kunt TTL op profiel-toegelaten datasets toepassen om gedragsgegevens uit de Opslag van het Profiel te verwijderen die niet meer waardevol voor uw gebruiksgevallen is. Zodra TTL wordt toegepast op een profiel-Toegelaten dataset, verwijdert het Platform automatisch gegevens die niet meer door een tweedelige proces nodig zijn:

* Op alle nieuwe gegevens die naar voren worden verplaatst, wordt de vervalwaarde van TTL toegepast op het tijdstip van opname;
* Voor alle bestaande gegevens wordt de vervalwaarde van TTL toegepast als onderdeel van een eenmalige back-upsysteemtaak.

U kunt verwachten dat de TTL-waarde voor elke gebeurtenis van de tijdstempel van de gebeurtenis afkomstig is. Alle gebeurtenissen ouder dan de vervalwaarde van TTL worden onmiddellijk gelaten vallen aangezien de systeembaan loopt. Alle andere gebeurtenissen worden weggelaten aangezien zij de waarde naderen die van TTL in gebeurtenistimestamp wordt aangewezen.

Zie het volgende voorbeeld voor meer informatie over [!DNL ExperienceEvent] Dataset TTL.

Als u op 15 mei een TTL-waarde van 30 dagen toepast, dan:

* Voor alle nieuwe gebeurtenissen wordt een GVTO van 30 dagen toegepast zodra ze binnenkomen;
* Alle bestaande gebeurtenissen met een tijdstempel die ouder is dan 15 april, worden onmiddellijk verwijderd door een systeemtaak.;
* Gebeurtenissen die een tijdstempel hebben na 15 april, verlopen hun tijdstempel voor de gebeurtenis + TTL-dagen. Dus een evenement met een tijdstempel van 18 april zal drie dagen na 15 mei aflopen.

>[!IMPORTANT]
>
>Zodra een TTL wordt toegepast, zullen om het even welke gegevens die ouder zijn dan het geselecteerde TTL aantal dagen zijn **permanent** verwijderd en kan niet worden hersteld.

Alvorens TTL toe te passen, moet u ervoor zorgen om een raadplegingsvenster van om het even welke segmenten binnen de grens van TTL te houden. Anders, kunnen de segmentresultaten onjuist worden nadat TTL wordt toegepast. Als u bijvoorbeeld een TTL van 30 dagen hebt toegepast voor Adobe Analytics-gegevens en een TTL van 365 dagen voor In-Store Transactiegegevens, leidt het volgende segment tot onjuiste resultaten:

* Bekeken productpagina in de laatste 60 dagen, gevolgd door een aankoop in de winkel;
* Toevoegen aan winkelwagentje, gevolgd door geen aankoop in de laatste 60 dagen.

Omgekeerd, zal het volgende nog correcte resultaten creëren:

* Bekeken productpagina in de laatste 14 dagen, gevolgd door een aankoop in de winkel;
* heeft de afgelopen 30 dagen een specifieke Help-pagina online bekeken;
* in de laatste 120 dagen een product offline heeft gekocht;
* Toegevoegd aan winkelwagentje, gevolgd door aankoop in de laatste 14 dagen.

>[!TIP]
>
>Voor gemak, kunt u zelfde TTL voor alle datasets houden, zodat u zich niet over het effect van TTL over datasets in segmentatielogica moet ongerust maken.

Raadpleeg de documentatie over voor meer informatie over het toepassen van TTL op profielgegevens [Profile Service TTL](../../profile/apply-ttl.md).

## Overzicht van best practices voor compatibiliteit met het gebruik van licenties {#best-practices}

Hieronder volgt een lijst met aanbevolen tips die u kunt volgen om ervoor te zorgen dat u zich beter houdt aan uw gebruiksrechten voor licenties:

* Gebruik de [licentiegebruiksdashboard](../../dashboards/guides/license-usage.md) om de trends van het klantengebruik te volgen en te controleren. Hierdoor kunt u eventuele overschrijdingen die zich kunnen voordoen, overtreffen.
* Configureren [innamefilters](#ingestion-filters) door de gebeurtenissen te identificeren die voor uw segmentatie en verpersoonlijkingsgebruiksgevallen worden vereist. Op deze manier kunt u alleen belangrijke gebeurtenissen verzenden die vereist zijn voor uw gebruiksgevallen.
* Zorg ervoor dat u alleen [ingeschakelde gegevenssets voor profiel](#ingestion-filters) die voor uw segmentatie en verpersoonlijkingsgebruiksgevallen worden vereist.
* Een [[!DNL ExperienceEvent] DataSet TTL](#dataset-ttl) voor gegevens met hoge frequentie, zoals webgegevens.
* Controleer de [Profielsamenstellingsrapporten](#profile-store-composition-reports) om inzicht te krijgen in de samenstelling van je profielwinkel. Op deze manier kunt u de gegevensbronnen begrijpen die het meest bijdragen aan het gebruik van uw licentie.

## Overzicht en beschikbaarheid van functies {#feature-summary}

De beste praktijken en hulpmiddelen die in dit document worden geschetst zullen u helpen uw gebruik van de vergunning van het machtigingsgebruik binnen Adobe Experience Platform beter beheren. Dit document wordt bijgewerkt wanneer extra functies worden vrijgegeven om alle klanten van het Experience Platform zichtbaar en bestuurbaar te maken.

In de volgende tabel wordt de lijst met momenteel beschikbare functies weergegeven, zodat u uw gebruiksrechten voor licenties beter kunt beheren.

| Functie | Beschrijving |
| --- | --- |
| [Datasets voor profiel in-/uitschakelen](../../catalog/datasets/user-guide.md) | Gegevenssetopname in de profielservice in- of uitschakelen |
| [!DNL ExperienceEvent] DataSet TTL | Pas een vervaldatum van TTL voor gedragsdatasets in de Winkel van het Profiel toe. Neem contact op met uw Adobe Support-vertegenwoordiger. |
| [Adobe Analytics Data Prep-filters](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Toepassen [!DNL Kafka] filters om onnodige gegevens uit te sluiten van inname |
| [Adobe Audience Manager-bronverbindingsfilters](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Bronverbindingsfilters van Audience Manager toepassen om onnodige gegevens uit te sluiten van inname |
| [SDK-gegevensfilters toestaan](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | Alloy-filters toepassen om onnodige gegevens uit te sluiten van inname |
| [Gegevensfilters voor doorsturen van gebeurtenissen](../../tags/ui/event-forwarding/overview.md) | Server-kant toepassen [!DNL Kafka] filters om onnodige gegevens uit te sluiten van inname.  Zie de documentatie op [tagregels](../../tags/ui/managing-resources/rules.md) voor aanvullende informatie. |
| [Gebruikersinterface van dashboard voor licentiegebruik](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Bekijk een momentopname van de licentiegerelateerde gegevens van uw organisatie voor Experience Platform |
| [API voor gegevensset-overlap](../../profile/tutorials/dataset-overlap-report.md) | Output de datasets die het meest aan uw Adresseerbare Publiek bijdraagt |
| [API voor overlappen van identiteiten](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Output de identiteitsnaamruimten die het meest aan uw Adresseerbare Publiek bijdragen |

{style=&quot;table-layout:auto&quot;}
