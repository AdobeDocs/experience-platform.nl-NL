---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd;profiel;rtcp;XDM-grafieken
title: Overzicht van realtime-klantprofiel
topic: hulplijn
description: Klantprofiel in realtime is een algemene opzoekeenheid die gegevens uit verschillende bedrijfsgegevenselementen samenvoegt en vervolgens toegang tot die gegevens biedt in de vorm van individuele klantprofielen en gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden.
translation-type: tm+mt
source-git-commit: 08eff53f107549fab0f167a6c206b632f3c8c183
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] - overzicht

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-time Customer Profile] kunt u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. [!DNL Profile] staat u toe om uw klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt. Dit overzicht zal u helpen de rol en het gebruik van [!DNL Real-time Customer Profile] in [!DNL Experience Platform] begrijpen.

## [!DNL Profile] in Experience Platform

De verhouding tussen het Profiel van de Klant in real time en andere diensten binnen Experience Platform wordt benadrukt in het volgende diagram:

![](images/profile-overview/profile-in-platform.png)

## Werken met profielen

[!DNL Real-time Customer Profile] voegt gegevens van verschillende bedrijfssystemen samen en verleent dan toegang tot die gegevens in de vorm van klantenprofielen met verwante gebeurtenissen van de tijdreeksen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden. In de volgende secties worden enkele kernconcepten beschreven die u moet begrijpen om profielen op effectieve wijze te kunnen maken en onderhouden binnen het Platform.

### Profielgegevensopslag

Hoewel [!DNL Real-time Customer Profile] ingeslikte gegevens verwerkt en Adobe Experience Platform [!DNL Identity Service] gebruikt om verwante gegevens samen te voegen via identiteitstoewijzing, behoudt het zijn eigen gegevens in de [!DNL Profile] gegevensopslag. De opslag [!DNL Profile] is gescheiden van catalogusgegevens in het gegevenspeer en [!DNL Identity Service] gegevens in de identiteitsgrafiek.

De profielopslag gebruikt een Microsoft Azure Cosmos DB-infrastructuur en het Platform Data Lake gebruikt de opslag van Microsoft Azure Data Lake.

### Profielhulplijnen

Experience Platform biedt een reeks instructies om u te helpen voorkomen dat u [XDM-schema&#39;s (Experience Data Model) maakt](../xdm/home.md) die niet kunnen worden ondersteund door het realtime profiel van de klant. Dit omvat zachte grenzen die in prestatiesdegradatie zullen resulteren, evenals harde grenzen die in fouten en systeembreuken zullen resulteren. Lees de [Profielhulplijnen](guardrails.md) documentatie voor meer informatie, zoals een lijst met richtlijnen en voorbeelden van gebruiksgevallen.

### (Beta) Profieldashboard {#profile-dashboard}

>[!IMPORTANT]
>
>De dashboardfunctionaliteit bevindt zich momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De interface van het Experience Platform biedt een dashboard waarmee u belangrijke informatie over uw gegevens van het Profiel van de Klant in real time kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Raadpleeg de [Handleiding voor het dashboard van het profiel](ui/profile-dashboard.md) voor meer informatie over de toegang tot en het werken met het dashboard [!DNL Profile] in de gebruikersinterface en voor gedetailleerde informatie over de metriek die in het dashboard wordt weergegeven.

### Profielfragmenten versus samengevoegde profielen {#profile-fragments-vs-merged-profiles}

Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Wanneer de gegevens uit meerdere bronnen conflicteren (bijvoorbeeld één fragment vermeldt de klant als &#39;single&#39;, terwijl de andere de klant als &#39;getrouwd&#39; vermeldt), bepaalt het [samenvoegbeleid](#merge-policies) welke informatie voorrang moet krijgen en in het profiel voor de persoon moet worden opgenomen. Daarom is het totale aantal profielfragmenten in Platform waarschijnlijk altijd hoger dan het totale aantal samengevoegde profielen, aangezien elk profiel uit meerdere fragmenten bestaat.

### Gegevens opnemen

Een profiel is een weergave van een onderwerp, een organisatie of een individu, dat uit vele kenmerken bestaat (ook wel recordgegevens genoemd). Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. Met [!DNL Experience Platform] kunt u profielen aanpassen om specifieke gegevens te gebruiken die relevant zijn voor uw bedrijf. De standaard [!DNL Experience Data Model] (XDM) klasse, [!DNL XDM Individual Profile], is de aangewezen klasse waarop om een schema te bouwen wanneer het beschrijven van de gegevens van het klantenverslag, en levert de gegevensintegraal aan vele interactie tussen de diensten van het Platform. Voor meer informatie bij het werken met schema&#39;s in [!DNL Experience Platform], gelieve te beginnen door [XDM systeemoverzicht](../xdm/home.md) te lezen.

### Gebeurtenissen van tijdreeksen

De gegevens van de tijdreeksen verstrekken een momentopname van het systeem op het tijdstip dat een actie of direct of indirect door een onderwerp werd genomen, evenals gegevens detailleert de gebeurtenis zelf. Deze tijdreeksgegevens worden vertegenwoordigd door de XDM ExperienceEvent-standaardschemaklasse en kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. Gegevens uit tijdreeksen kunnen worden gebruikt om segmentatieregels te baseren op, en gebeurtenissen kunnen individueel worden benaderd in de context van een profiel.

### Identiteiten

Elk bedrijf wil met zijn klanten op een manier communiceren die zich persoonlijk voelt. Een van de uitdagingen bij het aanbieden van relevante digitale ervaringen aan klanten is echter het begrijpen van hoe ze hun losgekoppelde gegevens aan elkaar kunnen koppelen. Deze gegevens worden vaak verspreid over verschillende digitale kanalen, zoals tablets, mobiele telefoons en laptops. [!DNL Identity Service] kunt u het volledige beeld van uw klant samenvoegen door identiteiten van veelvoudige kanalen te verbinden en een identiteitsgrafiek voor elke klant te creëren. Ga naar [Overzicht van de Identiteitsdienst](../identity-service/home.md) voor meer informatie.

### Beleid samenvoegen

Wanneer het brengen van gegevensfragmenten uit veelvoudige bronnen en het combineren van hen om een volledige mening van elk van uw individuele klanten te zien, zijn het fusiebeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens zullen worden geprioriteerd en welke gegevens zullen worden gebruikt om het klantenprofiel tot stand te brengen. Wanneer er conflicterende gegevens van veelvoudige datasets zijn, zal het fusiebeleid bepalen hoe die gegevens moeten worden behandeld en welke waarde zou moeten worden gebruikt. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen.

Voor meer informatie bij het werken met fusiebeleid gebruikend [!DNL Real-time Customer Profile] API, zie [de gids ](api/merge-policies.md)van het eindpunt van samenvoegingsbeleid. Om met samenvoegbeleid te werken gebruikend [!DNL Experience Platform] UI, verwijs naar [de gids UI van het samenvoegingsbeleid](ui/merge-policies.md).

### Unieschema&#39;s {#profile-fragments-and-union-schemas}

Een van de belangrijkste functies van [!DNL Real-time Customer Profile] is de mogelijkheid om multikanaalgegevens te verenigen. Wanneer [!DNL Real-time Customer Profile] wordt gebruikt om tot een entiteit toegang te hebben, kan het u van een samengevoegde mening van alle profielfragmenten voor die entiteit over datasets voorzien, die als &quot;verenigingsmening&quot;wordt bedoeld en door wat als verenigingsschema wordt bekend gemaakt mogelijk gemaakt.

Meer over verenigingsschema&#39;s, met inbegrip van hoe te om tot verenigingsschema&#39;s in UI toegang te hebben, bezoek [verenigingsschema UI guide](ui/union-schema.md).

### (Alpha) Berekende kenmerken

>[!IMPORTANT]
>
>De berekende kenmerkfunctionaliteit staat in alpha. De documentatie en functionaliteit kunnen worden gewijzigd.

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Voor meer informatie over berekende kenmerken, waaronder het begrip van de rol die berekende kenmerken spelen in Adobe Experience Platform, moet u eerst het [overzicht van berekende kenmerken](computed-attributes/overview.md) lezen.

## Profielen en segmenten

Adobe Experience Platform [!DNL Segmentation Service] levert het publiek dat nodig is om uw individuele klanten van energie te voorzien. Wanneer een publiekssegment wordt gecreeerd, wordt identiteitskaart van dat segment toegevoegd aan de lijst van segmentlidmaatschap voor alle kwalificerende profielen. De regels van het segment worden gebouwd en toegepast op [!DNL Real-time Customer Profile] gegevens gebruikend RESTful APIs en het gebruikersinterface van de Bouwer van het Segment. Om meer over segmentatie te leren, te beginnen door [Overzicht van de Dienst van de Segmentatie](../segmentation/home.md) te lezen.

### Streaming opname en streamingsegmentatie

Invoer in realtime wordt mogelijk gemaakt via een proces dat streaming opname wordt genoemd. Aangezien profiel en tijdreeksgegevens worden opgenomen, [!DNL Real-time Customer Profile] automatisch besluit om die gegevens van segmenten door een aan de gang zijnde proces te omvatten of uit te sluiten die het stromen segmentatie wordt genoemd, alvorens het met bestaande gegevens samen te voegen en de verenigingsmening bij te werken. Dientengevolge, kunt u onmiddellijk berekeningen uitvoeren en besluiten nemen om verbeterde, geïndividualiseerde ervaringen aan klanten te leveren aangezien zij met uw merk in wisselwerking staan. Terwijl het worden opgenomen, ondergaat de gegevens ook bevestiging om ervoor te zorgen het behoorlijk wordt opgenomen en conform het schema is waarop de dataset gebaseerd is. Voor meer informatie over welke bevestiging tijdens opname wordt gedaan, gelieve te beginnen door [kwaliteitsoverzicht van gegevensopname te lezen](../ingestion/quality/overview.md).

## Edge-prognoses

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Adobe Experience Platform biedt realtime toegang tot gegevens via het gebruik van zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. Bijvoorbeeld, gebruiken de toepassingen van de Adobe zoals Adobe Target en Adobe Campaign randen om gepersonaliseerde klantenervaringen in real time te verstrekken. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Als u meer wilt weten en wilt gaan werken met projecties met de [!DNL Real-time Customer Profile]-API, raadpleegt u de [handleiding voor randprojectie-eindpunten](api/edge-projections.md).

## Gegevens invoegen in [!DNL Profile]

[!DNL Platform] kan worden gevormd om verslag en tijdreeksgegevens naar te verzenden  [!DNL Profile], ondersteunend het stromen in real time en partijingestie. Voor meer informatie, zie de zelfstudie die schetst hoe te om [gegevens aan het Profiel van de Klant in real time ](tutorials/add-profile-data.md) toe te voegen.

>[!NOTE]
>
>Gegevens die zijn verzameld via Adobe-oplossingen, zoals [!DNL Analytics Cloud], [!DNL Marketing Cloud] en [!DNL Advertising Cloud], stromen naar [!DNL Experience Platform] en worden opgenomen in [!DNL Profile].

### Metrische gegevens voor het opnemen van profielen

Met observability Insights kunt u belangrijke metriek in Adobe Experience Platform onthullen. Naast [!DNL Experience Platform] gebruiksstatistieken en prestatie-indicatoren voor diverse functies [!DNL Platform], zijn er specifieke op profiel betrekking hebbende metriek die u toestaan om inzicht in inkomende verzoektarieven, succesvolle innametarieven, ingebedde verslaggrootte, en meer te krijgen. Voor meer informatie, begin door [Observability Insights API overzicht](../observability/api/overview.md) te lezen, en voor een volledige lijst van de metriek van het Profiel van de Klant in real time, zie de documentatie over [beschikbare metriek](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] en [!DNL Privacy]

[!DNL Data governance] is een reeks strategieën en technologieën die worden gebruikt om klantengegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren van toepassing op gegevensgebruik.

Met betrekking tot de toegang tot gegevens speelt gegevensbeheer een sleutelrol binnen [!DNL Experience Platform] op diverse niveaus:
* Labels voor gegevensgebruik
* Beleid voor gegevenstoegang
* Toegangscontrole van gegevens voor marketingacties

[!DNL Data governance] wordt op verschillende punten beheerd. Deze omvatten het bepalen van welke gegevens in [!DNL Platform] worden opgenomen en welke gegevens toegankelijk zijn na inname voor een bepaalde marketingactie. Voor meer informatie, begin door [gegeven goed te lezen overzicht](../data-governance/home.md).

### Verzoeken om opt-out en privacy van gegevens verwerken

[!DNL Experience Platform] biedt uw klanten de mogelijkheid om weigeren-aanvragen te verzenden met betrekking tot het gebruik en de opslag van hun gegevens binnen  [!DNL Real-time Customer Profile]. Raadpleeg de documentatie over [het afhandelen van aanvragen voor opt-out](../segmentation/honoring-opt-outs.md) voor meer informatie over de manier waarop aanvragen voor opt-out worden afgehandeld.

## Volgende stappen en extra bronnen

Als u meer wilt weten over het werken met [!DNL Real-time Customer Profile]-gegevens met de interface van het Experience Platform of de API voor profiel, leest u eerst de [Handleiding voor profiel-gebruikersinterface](ui/user-guide.md) of [API-ontwikkelaarshandleiding](api/overview.md).