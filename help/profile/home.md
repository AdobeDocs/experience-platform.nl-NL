---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Overzicht van het realtime klantprofiel
topic: guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 0%

---


# Overzicht van het realtime klantprofiel

Met Adobe Experience Platform kunt u uw klanten een gecoördineerde, consistente en relevante ervaring bieden, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt. Dit overzicht zal u helpen de rol en het gebruik van het Profiel van de Klant in real time in Experience Platform begrijpen.

## Klantprofiel in realtime

Klantprofiel in real-time is een algemene opzoekeenheid die gegevens uit verschillende bedrijfsgegevenselementen samenvoegt en vervolgens toegang tot die gegevens biedt in de vorm van individuele klantprofielen en gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen gecoördineerde, consistente en relevante ervaringen opdoen met hun publiek.

### Profielgegevensopslag

Hoewel het Profiel van de Klant in real time ingebedde gegevens verwerkt en de Dienst van de Identiteit van het Adobe Experience Platform gebruikt om verwante gegevens door identiteitstoewijzing samen te voegen, handhaaft het zijn eigen gegevens in de opslag van het Profiel. Met andere woorden, de opslag van het Profiel is gescheiden van de gegevens van de Catalogus (Gegevens meer) en van de Dienst van de Identiteit (identiteitsgrafiek).

### Profiel en Platform

De verhouding tussen het Profiel van de Klant in real time en andere diensten binnen Experience Platform wordt benadrukt in het volgende diagram:

![De relatie tussen Profiel en andere diensten van het Experience Platform.](images/profile-overview/profile-in-platform.png)

### Profielen en gegevens opnemen

Een profiel is een weergave van een onderwerp, een organisatie of een individu, ook wel recordgegevens genoemd. Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. Met Experience Platform kunt u profielen aanpassen om gegevenstypen te gebruiken die relevant zijn voor uw bedrijf. De standaard klasse van het Profiel van de Gegevens van de Ervaring Model (XDM) Individuele is de aangewezen klasse waarop om een schema te bouwen wanneer het beschrijven van gegevens van het klantenverslag, en de gegevensintegraal aan vele interactie tussen de diensten van het Platform verstrekt. Voor meer informatie over het werken met schema&#39;s in Experience Platform, gelieve te beginnen door het [XDM systeemoverzicht](../xdm/home.md)te lezen.

### Gebeurtenissen van tijdreeksen

De gegevens van de tijdreeksen verstrekken een momentopname van het systeem op het tijdstip dat een actie of direct of indirect door een onderwerp werd genomen, evenals gegevens detailleert de gebeurtenis zelf. Deze tijdreeksgegevens worden vertegenwoordigd door de XDM ExperienceEvent-standaardschemaklasse en kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. Gegevens uit tijdreeksen kunnen worden gebruikt om segmentatieregels te baseren op, en gebeurtenissen kunnen individueel worden benaderd in de context van een profiel.

### Identiteiten

Elk bedrijf wil met zijn klanten op een manier communiceren die zich persoonlijk voelt. Een van de uitdagingen bij het aanbieden van relevante digitale ervaringen aan klanten is echter het begrijpen van hoe ze hun losgekoppelde gegevens aan elkaar kunnen koppelen. Deze gegevens worden vaak verspreid over verschillende digitale kanalen, zoals tablets, mobiele telefoons en laptops. Met de identiteitsservice kunt u het volledige beeld van uw klant samenvoegen door identiteiten van meerdere kanalen te koppelen, een identiteitsgrafiek voor elke klant te maken, zodat u deze beter kunt begrijpen. Ga naar het overzicht [van de](../identity-service/home.md) identiteitsservice voor meer informatie.

### Segmentatie

De Dienst van de Segmentatie van het Adobe Experience Platform produceert de publiek nodig om ervaringen voor uw individuele klanten te aandrijven. Wanneer een publiekssegment wordt gecreeerd, wordt identiteitskaart van dat segment toegevoegd aan de lijst van segmentlidmaatschap voor alle kwalificerende profielen. De regels van het segment worden gebouwd en toegepast op de gegevens van het Profiel van de Klant in real time gebruikend RESTful APIs en de gebruikersinterface van de Bouwer van het Segment. Om meer over segmentatie te leren, gelieve te beginnen door het overzicht [van de Dienst van de](../segmentation/home.md)Segmentatie te lezen.

### Profielfragmenten en samenvoegingsschema&#39;s {#profile-fragments-and-union-schemas}

Een van de belangrijkste kenmerken van Real-Time Customer Profile is de mogelijkheid om gegevens met meerdere kanalen te verenigen. Wanneer het Profiel van de Klant in real time wordt gebruikt om tot een entiteit toegang te hebben, kan het u van een samengevoegde mening van alle profielfragmenten voor die entiteit over datasets voorzien, die als verenigingsmening wordt bedoeld en die door wat als verenigingsschema wordt genoemd mogelijk gemaakt. In real time gegevens van het Profiel van de Klant worden samengevoegd over bronnen wanneer een entiteit of een profiel door zijn identiteitskaart wordt betreden of als segment wordt uitgevoerd. Voor meer informatie over de toegang tot van profielen en verenigingsmeningen die in real time API van het Profiel van de Klant gebruiken, bezoek de gids [van het](api/entities.md)entiteitseindpunt.

### Beleid samenvoegen

Wanneer het samenbrengen van gegevens uit veelvoudige bronnen en het combineren om een volledige mening van elk van uw individuele klanten te zien, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Voor meer informatie bij het werken met samenvoegbeleid die in real time API van het Profiel van de Klant gebruiken, gelieve de gids [van het eindpunt van het](api/merge-policies.md)fusiebeleid te zien. Als u met samenvoegbeleid wilt werken met de gebruikersinterface van het Experience Platform, raadpleegt u de gebruikershandleiding [van het](ui/merge-policies.md)samenvoegbeleid.

### (Alfa) Berekende kenmerken configureren

>[!IMPORTANT]
>De berekende kenmerkfunctionaliteit die in dit document wordt beschreven is in alpha. De documentatie en de functionaliteit kunnen worden gewijzigd.

Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op het profielniveau, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen. Elk berekend kenmerk bevat een expressie, ofwel &quot;rule&quot;, die binnenkomende gegevens evalueert en de resulterende waarde opslaat in een profielkenmerk of in een gebeurtenis. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Voor meer informatie over gegevens verwerkte attributen, en geleidelijke instructies voor het werken met hen die in real time API van het Profiel van de Klant gebruiken, te zien gelieve de [gegevens verwerkte gids](api/computed-attributes.md)van het attributeneindpunt. Deze gids zal u helpen beter begrijpen de rol gegevens verwerkte attributen binnen Adobe Experience Platform spelen, en het omvat steekproefAPI vraag voor het uitvoeren van basisCRUD verrichtingen.

## Realtime componenten

Deze sectie introduceert de componenten die het Profiel van de Klant in real time toestaan om verslag en tijdreeksgegevens in real time bij te werken en te controleren.

### Streaming opname en streamingsegmentatie

Invoer in realtime wordt mogelijk gemaakt via een proces dat streaming opname wordt genoemd. Aangezien profiel en tijdreeksgegevens worden opgenomen, beslist het Profiel van de Klant in real time automatisch om die gegevens van segmenten door een aan de gang zijnde proces te omvatten of uit te sluiten die het stromen segmentatie wordt genoemd, alvorens het met bestaande gegevens samen te voegen en de verenigingsmening bij te werken. Dientengevolge, kunt u onmiddellijk berekeningen uitvoeren en besluiten nemen om verbeterde, geïndividualiseerde ervaringen aan klanten te leveren aangezien zij met uw merk in wisselwerking staan. Terwijl het worden opgenomen, ondergaat de gegevens ook bevestiging om ervoor te zorgen het behoorlijk wordt opgenomen en conform het schema is waarop de dataset gebaseerd is. Voor meer informatie over welke bevestiging tijdens opname wordt gedaan, gelieve te beginnen door het kwaliteitsoverzicht [van](../ingestion/quality/overview.md)gegevensinvoer te lezen.

### Edge-projectieconfiguraties en -doelen

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Adobe Experience Platform maakt deze realtime toegang tot gegevens mogelijk via het gebruik van zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. Adobe-toepassingen zoals Adobe Target en Adobe Campaign gebruiken bijvoorbeeld randen voor persoonlijke ervaringen van klanten in real-time. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Raadpleeg de handleiding voor [Edge-projectieeindpunten voor](api/edge-projections.md)Edge-projecties voor meer informatie en om te beginnen met het gebruik van de Real-time Customer Profile API.

## Gegevens toevoegen aan realtime klantprofiel

Platform kan worden gevormd om uw verslag en tijdreeksgegevens naar Profiel te verzenden, ondersteunend het stromen in real time en partij ingestie. Voor meer informatie, zie de zelfstudie die schetst hoe te om gegevens aan het Profiel [van de Klant in real time](tutorials/add-profile-data.md)toe te voegen.

>[!Nofferte]
>De gegevens die via Adobe-oplossingen zijn verzameld, waaronder Analytics Cloud, Marketing Cloud en Advertising Cloud, stromen naar Experience Platform en worden opgenomen in Profile.

### Metrische gegevens voor het opnemen van profielen

Met waarnemingsinformatie kunt u belangrijke meetgegevens in Adobe Experience Platform blootstellen. Naast gebruiksstatistieken van het Platform en prestatiesindicatoren voor diverse functies van het Platform, zijn er specifieke op profiel betrekking hebbende metriek die u toestaan om inzicht in inkomende verzoektarieven, succesvolle innamepercentages, ingebedde verslaggrootte, en meer te krijgen. Meer leren, begin door het overzicht [van de Inzichten van de](../observability/home.md)Waarnemelijkheid te lezen, en voor een volledige lijst van de metriek van het Profiel, zie de documentatie over [beschikbare metriek](../observability/metrics.md).

## Beheer van gegevens en privacy

Het beheer van gegevens is een reeks strategieën en technologieën die worden gebruikt om klantengegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren van toepassing op gegevensgebruik.

Wat de toegang tot gegevens betreft, speelt het beheer van gegevens een sleutelrol binnen het Experience Platform op verschillende niveaus:
* Labels voor gegevensgebruik
* Beleid voor gegevenstoegang
* Toegangscontrole van gegevens voor marketingacties

Het gegevensbeheer wordt op verschillende punten beheerd. Deze omvatten het bepalen van welke gegevens in het Platform worden opgenomen en welke gegevens na inname voor een bepaalde marketingactie toegankelijk zijn. Voor meer informatie, begin door het overzicht [van het](../data-governance/home.md)gegevensbeheer te lezen.

### Verzoeken om opt-out en privacy van gegevens verwerken

Met Experience Platform kunnen uw klanten weigeren-aanvragen met betrekking tot het gebruik en de opslag van hun gegevens verzenden naar het realtime profiel van de klant. Raadpleeg de documentatie over het [naleven van opt-out-verzoeken](../segmentation/honoring-opt-outs.md)voor meer informatie over de manier waarop aanvragen vooropt-out worden afgehandeld.

## Richtlijnen voor profielen

Experience Platform heeft een aantal richtlijnen om profiel effectief te gebruiken.

| Sectie | Grens |
| ------- | -------- |
| Samenvoegingsschema van profiel | Een maximum van **20** datasets kan tot het de unieschema van het Profiel bijdragen. |
| Relaties met meerdere entiteiten | Er kunnen maximaal **5** relaties met meerdere entiteiten worden gemaakt. |
| JSON-diepte voor associatie met meerdere entiteiten | De maximale JSON-diepte is **4**. |
| Gegevens uit tijdreeksen | Gegevens uit tijdreeksen zijn **niet** toegestaan in Profiel voor entiteiten van derden. |
| Schema-relaties van derden | Schema-relaties van derden zijn **niet** toegestaan. |
| Profielfragment | De aanbevolen maximale grootte van een profielfragment is **10kB**.<br><br> De absolute maximumgrootte van een profielfragment is **1 MB**. |
| Niet-persoonlijke entiteit | De maximale totale grootte voor één niet-persoonlijke entiteit is **200 MB**. |
| Gegevensbestanden per niet-persoonlijke entiteit | Een maximum van **1** dataset kan aan een niet-persoonentiteit worden geassocieerd. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>Een niet-persoonlijke entiteit verwijst naar elke XDM-klasse die **geen** deel uitmaakt van Profiel.

## Volgende stappen en extra bronnen

Als u meer wilt weten over Real-time klantprofiel, blijft u de documentatie lezen en kunt u uw kennis aanvullen door de onderstaande video te bekijken of andere videozelfstudies voor [Experience Platforms te bekijken](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html).

>[!WARNING]
>De interface van het Platform die in de volgende video wordt weergegeven, is verouderd. Raadpleeg de gebruikershandleiding [van het profiel van de](ui/user-guide.md) real-time klant voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)