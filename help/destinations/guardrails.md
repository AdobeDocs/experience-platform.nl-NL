---
keywords: Experience Platform;activering;problemen oplossen;instructies;richtlijnen;beperken
title: Standaardinstructies voor activeringsgegevens
solution: Experience Platform
product: experience platform
type: Documentation
description: Meer informatie over het standaardgebruik en de tarieflimieten van gegevensactivering.
source-git-commit: 69496d2e00ce866413786160d4524cabd03ae350
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 1%

---

# Grails voor activeringsgegevens

Deze pagina bevat standaardgebruiks- en tarieflimieten voor activeringsgedrag. Bij het bekijken van de volgende instructies wordt aangenomen dat u de juiste instructies hebt [verbonden met bestemmingen](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* De meeste klanten overschrijden deze standaardgrenzen niet. Neem contact op met uw medewerker van de klantenservice als u meer wilt weten over aangepaste limieten.
>* De limieten die in dit document worden uiteengezet, worden voortdurend verbeterd. Kom regelmatig terug voor updates.
>* Afhankelijk van individuele downstreambeperkingen, kunnen sommige doelen strengere instructies hebben dan de doelen die op deze pagina worden beschreven. Controleer ook of [catalogus](/help/destinations/catalog/overview.md) pagina van het doel waarmee u verbinding maakt en gegevens activeert.


## Limiettypen {#limit-types}

Dit document bevat twee typen standaardlimieten:

* **Zachte limiet:** Het is mogelijk om verder te gaan dan een zachte limiet, maar zachte limieten bieden een aanbevolen richtlijn voor systeemprestaties.
* **Harde limiet:** Een harde grens verstrekt een absoluut maximum. De interface van het Experience Platform of API staat u niet toe om voorbij deze grens te gaan, of een fout is teruggekeerd als u voorbij deze grens gaat.


## Activeringslimieten {#activation-limits}

De volgende instructies bieden aanbevolen limieten bij het activeren van gegevens in realtime-klantprofiel voor bestemmingen.

### Algemene activeringsinstructies {#general-activation-guardrails}

De onderstaande instructies zijn over het algemeen van toepassing op activering via [alle doeltypen](/help/destinations/destination-types.md#destination-types).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximum aantal segmenten aan één enkele bestemming | 250 | Zacht | De aanbeveling moet een maximum van 250 segmenten aan één enkele bestemming in een dataflow in kaart brengen. <br><br> Als u meer dan 250 segmenten aan een bestemming moet activeren, kunt u of: <ul><li> Ontkaart segmenten die u niet meer wilt activeren, of</li><li>Creeer een nieuwe dataflow aan de gewenste bestemming en kaartsegmenten aan deze nieuwe dataflow.</li></ul> <br> Merk op dat in het geval van sommige bestemmingen, u tot minder dan 250 segmenten kan worden beperkt die aan de bestemming worden in kaart gebracht. Deze bestemmingen worden hieronder op de pagina in hun respectieve secties vermeld. |
| Maximum aantal bestemmingen | 100 | Zacht | De aanbeveling moet een maximum van 100 bestemmingen tot stand brengen die u gegevens kunt verbinden en activeren om *per sandbox*. [Aanpasbare Edge-doelen (Aangepaste verpersoonlijking)](#edge-destinations-activation) maximaal 10 van de 100 aanbevolen bestemmingen. |
| Maximumaantal kenmerken dat aan een doel is toegewezen | 50 | Zacht | In het geval van verschillende doelen en doeltypen kunt u profielkenmerken en identiteiten selecteren die u wilt toewijzen voor export. Voor optimale prestaties, zou een maximum van 50 attributen in een dataflow aan een bestemming moeten worden in kaart gebracht. |
| Type gegevens die op bestemmingen worden geactiveerd | Profielgegevens, inclusief identiteiten en identiteitskaarten | Hard | Momenteel is het alleen mogelijk om te exporteren *profielrecordkenmerken* naar bestemmingen. XDM-kenmerken die gebeurtenisgegevens beschrijven, worden momenteel niet ondersteund voor exporteren. |
| Type gegevens geactiveerd voor doelen - ondersteuning voor array- en kaartkenmerken | Niet beschikbaar | Hard | Op dit moment is het **niet** kunnen worden geëxporteerd *array- of toewijzingskenmerken* naar bestemmingen. De uitzondering op deze regel is de [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md), die wordt geëxporteerd in zowel streaming als bestandgebaseerde activering. |

{style=&quot;table-layout:auto&quot;}

### Streaming activering {#streaming-activation}

De onderstaande instructies zijn van toepassing op activering via [streaming doelen](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Aantal activeringen (HTTP-berichten met profielexport) per seconde | N.v.t. | - | Er is momenteel geen grens aan het aantal berichten per seconde die van Experience Platform naar API eindpunten van partnerbestemmingen worden verzonden. <br> Om het even welke grenzen of latentie worden gedicteerd door het eindpunt waar het Experience Platform gegevens verzendt. Controleer ook of [catalogus](/help/destinations/catalog/overview.md) pagina van het doel waarmee u verbinding maakt en gegevens activeert. |

{style=&quot;table-layout:auto&quot;}

### Batch (op bestand gebaseerd) activeren {#batch-file-based-activation}

De onderstaande instructies zijn van toepassing op activering via [batchbestemmingen (op basis van bestanden)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Activeringsfrequentie | Eén dagelijkse volledige export of frequentere incrementele export om de 3, 6, 8 of 12 uur. | Hard | Lees de [volledige bestanden exporteren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) en [incrementele bestanden exporteren](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) Documentatiegedeelten voor meer informatie over de frequentieverhogingen voor batchexport. |
| Maximumaantal segmenten dat in een bepaald uur kan worden geëxporteerd | 100 | Zacht | De aanbeveling moet een maximum van 100 segmenten aan partijbestemmingsdataflows toevoegen. |
| Maximumaantal rijen (records) per bestand dat moet worden geactiveerd | 5 miljoen | Hard | Adobe Experience Platform splitst de geëxporteerde bestanden automatisch op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel. Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking, als zodanig: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Lees voor meer informatie de [sectie plannen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) van de activerende batchdoelzelfstudie. |

{style=&quot;table-layout:auto&quot;}

### Ad-hocactivering {#ad-hoc-activation}

De onderstaande instructies zijn van toepassing op de [ad-hocactivering](/help/destinations/api/ad-hoc-activation-api.md) methode.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Segmenten geactiveerd per ad-hocactiveringstaak | 80 | Hard | Momenteel kan elke ad-hocactiveringstaak maximaal 80 segmenten activeren. Als u probeert meer dan 80 segmenten per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd. |
| Gelijktijdige ad-hocactiveringstaken per segment | 1 | Hard | Voer niet meer dan één gelijktijdige ad-hocactiveringstaak per segment uit. |

{style=&quot;table-layout:auto&quot;}

### Activering van Edge-verpersoonlijkingsdoelen {#edge-destinations-activation}

De onderstaande instructies zijn van toepassing op activering via [Edge-verpersoonlijkingsdoelen](/help/destinations/destination-types.md#streaming-profile-export).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximum aantal [Aangepaste personalisatie](/help/destinations/catalog/personalization/custom-personalization.md) bestemmingen | 10 | Zacht | U kunt gegevensstromen aan 10 Aangepaste verpersoonlijkingsbestemmingen per zandbak plaatsen. |
| Maximumaantal kenmerken dat per sandbox aan een verpersoonlijkingsdoel is toegewezen | 20 | Hard | Een maximum van 20 attributen kan in een dataflow aan een verpersoonlijkingsbestemming, per zandbak worden in kaart gebracht. |
| Maximumaantal segmenten toegewezen aan één [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) doel | 50 | Zacht | U kunt maximaal 50 segmenten in een activeringsstroom activeren naar één Adobe Target-bestemming. |

{style=&quot;table-layout:auto&quot;}

### Destination SDK guardrails {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) is een reeks van configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De onderstaande instructies zijn van toepassing op de doelen die u configureert met behulp van Destination SDK.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximum aantal [persoonlijke aangepaste bestemmingen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Zacht | U kunt maximaal vijf aangepaste streaming privédoelen of batchdoelen maken met behulp van Destination SDK. Neem contact op met een aangepaste zorgvertegenwoordiger als u meer dan vijf van dergelijke doelen moet maken. |
| Profielexportbeleid voor Destination SDK | <ul><li>`maxBatchAgeInSecs` (minimaal 1 800 en maximaal 3 600)</li><li>`maxNumEventsInBatch` (minimaal 1 000, maximaal 10 000)</li></ul> | Hard | Wanneer u de [configureerbare samenvoeging](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) Houd rekening met de minimum- en maximumwaarden die bepalen hoe vaak HTTP-berichten naar de op API gebaseerde bestemming worden verzonden en hoeveel profielen de berichten moeten bevatten. |

{style=&quot;table-layout:auto&quot;}

### Beleidswijziging en opnieuw proberen van bestemming {#destination-throttling-and-retry-policy}

Gegevens over drempelwaarden of beperkingen voor bepaalde bestemmingen. Deze sectie verstrekt ook informatie betreffende het hertestbeleid voor bestemmingen.

| Type bestemming | Beschrijving |
| --- | --- |
| Enterprise-bestemmingen (HTTP-API, Amazon Kinesis, Azure EventHubs) | In 95 percent van de tijd, probeert het Experience Platform om een productietolerantie van minder dan 10 minuten voor met succes verzonden berichten met een tarief van minder dan 10.000 verzoeken per seconde voor elke dataflow aan een ondernemingsbestemming aan te bieden. <br> In het geval van ontbroken verzoeken aan uw ondernemingsbestemming, slaat het Experience Platform de ontbroken verzoeken op en probeert tweemaal om de verzoeken naar uw eindpunt te verzenden. |

{style=&quot;table-layout:auto&quot;}

## Guardrails voor ander Experience Platform {#guardrails-other-services}

Informatie over hulplijnen weergeven voor andere services van Experience Platforms:

* Guardrails voor [gegevensinvoer](/help/ingestion/guardrails.md)
* Guardrails voor [[!DNL Identity Service] data](/help/identity-service/guardrails.md)
* Guardrails voor [[!DNL Real-time Customer Profile] data](/help/profile/guardrails.md)
* Guardrails voor [[!DNL Query Service] data](/help/query-service/guardrails.md)