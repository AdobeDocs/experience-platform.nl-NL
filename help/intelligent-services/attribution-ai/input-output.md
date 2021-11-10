---
keywords: Experience Platform;aan de slag;Attribution ai;populaire onderwerpen;Attribution ai input;Attribution ai output;
feature: Attribution AI
title: Invoer en Uitvoer in Attribution AI
topic-legacy: Input and Output data for Attribution AI
description: In het volgende document worden de verschillende invoer- en uitvoerbestanden beschreven die in Attribution AI worden gebruikt.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: 9023019ed8a781f9ae3965adab875cf2244f55a9
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 0%

---

# Invoer en uitvoer in [!DNL Attribution AI]

In het volgende document worden de verschillende invoer- en uitvoerbestanden beschreven die worden gebruikt in [!DNL Attribution AI].

## [!DNL Attribution AI] invoergegevens

Attribution AI werkt door de volgende datasets te analyseren om algoritmische scores te berekenen:

- Adobe Analytics-gegevenssets die gebruikmaken van de [Bronconnector voor analyse](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Gegevensset Experience Event (EE)
- Gegevensset met consumentenervaringen (CEE)

U kunt veelvoudige datasets van verschillende bronnen toevoegen als elk van de datasets het zelfde identiteitstype (namespace) zoals ECID deelt. Ga voor meer informatie over het toevoegen van meerdere datasets naar de [Gebruikershandleiding voor Attribution AI](./user-guide.md#identity).

>[!IMPORTANT]
>
>De Adobe Analytics-bronaansluiting kan maximaal vier weken duren om back-ups van gegevens te maken. Als u onlangs opstelling een schakelaar, zou u moeten verifiëren dat de dataset de minimumlengte van gegevens heeft die voor Attribution AI wordt vereist. Controleer de [historische gegevens](#data-requirements) om te controleren of u voldoende gegevens hebt om nauwkeurige algoritmische scores te berekenen.

Voor meer informatie over het instellen van de [!DNL Consumer Experience Event] (CEE) schema, gelieve te verwijzen naar [Intelligente services voor het verzamelen van gegevens](../data-preparation.md) hulplijn. Ga voor meer informatie over het toewijzen van Adobe Analytics-gegevens naar de [Toewijzingen van analytische velden](../../sources/connectors/adobe-applications/analytics.md) documentatie.

Niet alle kolommen in de [!DNL Consumer Experience Event] (CEE) schema is verplicht voor Attribution AI.

>[!NOTE]
>
> De volgende 9 kolommen zijn verplicht. Aanvullende kolommen zijn optioneel, maar aanbevolen/noodzakelijk als u dezelfde gegevens wilt gebruiken voor andere Adobe-oplossingen, zoals [!DNL Customer AI] en [!DNL Journey AI].

| Verplichte kolommen | Vereist voor |
| --- | --- |
| Primair identiteitsveld | Aanraakpunt/Omzetting |
| Tijdstempel | Aanraakpunt/Omzetting |
| Kanaal._type | Aanraakpunt |
| Channel.mediaAction | Aanraakpunt |
| Channel.mediaType | Aanraakpunt |
| Marketing.trackingCode | Aanraakpunt |
| Marketing.campaignname | Aanraakpunt |
| Marketing.campaigngroup | Aanraakpunt |
| Commerce | Conversie |

Over het algemeen wordt de toewijzing uitgevoerd bij conversiekolommen zoals bestelling, aankopen en kassa&#39;s onder &quot;handel&quot;. De kolommen voor &quot;channel&quot; en &quot;marketing&quot; worden gebruikt om aanraakpunten voor Attribution AI te definiëren (bijvoorbeeld `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Voor optimale resultaten en inzichten verdient het aanbeveling zoveel mogelijk conversie- en aanraakpuntkolommen op te nemen. Bovendien hoeft u niet alleen de bovenstaande kolommen te gebruiken. U kunt andere aanbevolen of aangepaste kolommen opnemen als een conversie- of aanraakpuntdefinitie.

>[!TIP]
>
>Als u Adobe Analytics-gegevens gebruikt in uw CEE-schema, worden de aanraakpuntgegevens voor Analytics meestal opgeslagen in `channel.typeAtSource` (bijvoorbeeld `channel.typeAtSource = 'email'`).

De kolommen hieronder zijn niet vereist maar het wordt geadviseerd dat u hen in uw CEE schema opneemt als u de beschikbare informatie hebt.

**Aanvullende aanbevolen kolommen:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

## Historische gegevens {#data-requirements}

>[!IMPORTANT]
>
> De minimale hoeveelheid gegevens die nodig is om Attribution AI te laten functioneren is als volgt:
> - U moet minstens 3 maanden (90 dagen) gegevens verstrekken om een goed model in werking te stellen.
> - U hebt minstens 1000 conversies nodig.


Attribution AI vereist historische gegevens als input voor modeltraining. De vereiste gegevensduur wordt hoofdzakelijk bepaald door twee sleutelfactoren: trainingsvenster en terugkijkvenster. De input met kortere opleidingsvensters is gevoeliger voor recente tendensen, terwijl de langere trainingsvensters helpen stabielere en nauwkeurigere modellen produceren. Het is belangrijk om het doel met historische gegevens te modelleren die uw bedrijfsdoelstellingen het best vertegenwoordigen.

De [configuratie van trainingsvensters](./user-guide.md#training-window) filterconversiegebeurtenissen die moeten worden opgenomen voor modeltraining op basis van de voorvaltijd. Momenteel is het minimale trainingsvenster 1 kwart (90 dagen). De [lookback-venster](./user-guide.md#lookback-window) biedt een tijdkader waarin wordt aangegeven hoeveel dagen vóór de conversiegebeurtenis de aanraakpunten met betrekking tot deze conversiegebeurtenis moeten worden opgenomen. Deze twee concepten bepalen samen de hoeveelheid inputgegevens (die door dagen wordt gemeten) die voor een toepassing wordt vereist.

Standaard definieert Attribution AI het trainingsvenster als de meest recente 2 kwartalen (6 maanden) en terugkijkvenster als 56 dagen. Met andere woorden, het model houdt rekening met alle gedefinieerde conversiegebeurtenissen die zich in de afgelopen twee kwartalen hebben voorgedaan en zoekt naar alle aanraakpunten die zich hebben voorgedaan binnen 56 dagen vóór de bijbehorende conversiegebeurtenis(sen).

**Formule**:

Minimale lengte van vereiste gegevens = trainingsvenster + terugkijkvenster

>[!TIP]
>
> De minimale gegevenslengte die vereist is voor een toepassing met standaardconfiguraties is: 2 kwartalen (180 dagen) + 56 dagen = 236 dagen.

Voorbeeld :

- U wilt conversiegebeurtenissen die zich in de laatste 90 dagen (3 maanden) hebben voorgedaan, toewijzen en alle aanraakpunten bijhouden die binnen 4 weken vóór de conversiegebeurtenis zijn opgetreden. De gegevensduur van de invoer moet zich uitstrekken over de afgelopen 90 dagen + 28 dagen (4 weken). Het trainingsvenster is 90 dagen en het terugkijkvenster is 28 dagen in totaal 118 dagen.

## Uitvoergegevens Attribution AI

Attribution AI geeft de volgende uitvoer:

- [Ruw granulaat](#raw-granular-scores)
- [Geaggregeerde scores](#aggregated-attribution-scores)

**Voorbeeld van uitvoerschema:**

![](./images/input-output/schema_output.gif)

### Ruw granulaat {#raw-granular-scores}

Attribution AI geeft de toewijzingsscores in het meest granulaire niveau weer, zodat u de scores met elke gewenste scorekolom kunt segmenteren en dichten. Als u deze scores in de gebruikersinterface wilt weergeven, leest u de sectie op [onbewerkte muziekpaden weergeven](#raw-score-path). Als u de scores wilt downloaden met de API, gaat u naar de [scores downloaden in Attribution AI](./download-scores.md) document.

>[!NOTE]
>
> U kunt om het even welke gewenste rapporteringskolom van de inputdataset in de dataset van de score slechts zien als één van beiden van het volgende waar zijn:
> - De rapportkolom is inbegrepen in de configuratiepagina of als deel van touchpoint of configuratie van de omzettingsdefinitie.
> - De rapportkolom is inbegrepen in de extra kolommen van de scoredataset.


In de volgende tabel worden de schemavelden in de voorbeelduitvoer van onbewerkte scores weergegeven:

| Kolomnaam (gegevenstype) | Niet invulbaar | Beschrijving |
| --- | --- | --- |
| timestamp (DateTime) | Onwaar | Het tijdstip waarop een conversiegebeurtenis of -waarneming heeft plaatsgevonden. <br> **Voorbeeld:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | Waar | identityMap van de gebruiker, vergelijkbaar met de CEE XDM-indeling. |
| eventType (String) | Waar | Het primaire gebeurtenistype voor deze tijdreeksverslag. <br> **Voorbeeld:** &quot;Order&quot;, &quot;Purchase&quot;, &quot;Visit&quot; |
| eventMergeId (String) | Waar | Een id om meerdere te correleren of samen te voegen [!DNL Experience Events] samen die in wezen dezelfde gebeurtenis zijn of moeten worden samengevoegd. Dit is bedoeld om vóór inname door de gegevensproducent te worden ingevuld. <br> **Voorbeeld:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (String) | Onwaar | Een unieke id voor de gebeurtenis time-series. <br> **Voorbeeld:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _huurderId (Object) | Onwaar | De objectcontainer op het hoogste niveau die correspondeert met uw tentant-id. <br> **Voorbeeld:** _atsdsnrmmsv2 |
| your_schema_name (Object) | Onwaar | De rij van de score met omzettingsgebeurtenis alle touchpoint gebeurtenissen verbonden aan het en hun meta-gegevens. <br> **Voorbeeld:** Scores Attribution AI - modelnaam__2020 |
| segmentation (String) | Waar | Conversiesegment zoals geo-segmentatie waarop het model is gebouwd. Als segmenten ontbreken, is het segment gelijk aan conversionName. <br> **Voorbeeld:** ORDER_US |
| conversionName (String) | Waar | Naam van de omzetting die tijdens opstelling werd gevormd. <br> **Voorbeeld:** Bestellen, Lead, Bezoek |
| conversie (Object) | Onwaar | Kolommen met omzettingsmetagegevens. |
| dataSource (String) | Waar | Globaal unieke identificatie van een gegevensbron. <br> **Voorbeeld:** Adobe Analytics |
| eventSource (String) | Waar | De bron op het moment dat de werkelijke gebeurtenis plaatsvond. <br> **Voorbeeld:** Adobe.com |
| eventType (String) | Waar | Het primaire gebeurtenistype voor deze tijdreeksverslag. <br> **Voorbeeld:** Volgorde |
| geo (String) | Waar | De geografische locatie waar de conversie heeft plaatsgevonden `placeContext.geo.countryCode`. <br> **Voorbeeld:** VS |
| priceTotal (dubbel) | Waar | Door omrekening verkregen inkomsten <br> **Voorbeeld:** 99,9 |
| product (String) | Waar | De XDM-id van het product zelf. <br> **Voorbeeld:** RX 1080 ti |
| productType (String) | Waar | De weergavenaam van het product zoals deze aan de gebruiker wordt getoond voor deze productweergave. <br> **Voorbeeld:** Gpus |
| hoeveelheid (geheel getal) | Waar | Tijdens de conversie aangekochte hoeveelheid. <br> **Voorbeeld:** 1 1080 ti |
| receiveTimestamp (DateTime) | Waar | Tijdstempel van de conversie ontvangen. <br> **Voorbeeld:** 2020-06-09T00:01:51.000Z |
| skuId (String) | Waar | Stock keeping unit (SKU), de unieke identificator voor een product dat door de verkoper wordt gedefinieerd. <br> **Voorbeeld:** MJ-03-XS-Black |
| timestamp (DateTime) | Waar | Tijdstempel van de conversie. <br> **Voorbeeld:** 2020-06-09T00:01:51.000Z |
| passThrough (Object) | Waar | De extra die de gegevensreeks van de Score Kolommen door gebruiker worden gespecificeerd terwijl het vormen van het model. |
| commerce_order_purchaseCity (String) | Waar | De extra Kolom van de dataset van de Score. <br> **Voorbeeld:** stad: San Jose |
| customerProfile (Object) | Onwaar | Identiteitsgegevens van de gebruiker die wordt gebruikt om het model te bouwen. |
| identity (Object) | Onwaar | Bevat de details van de gebruiker die wordt gebruikt om het model te bouwen zoals `id` en `namespace`. |
| id (String) | Waar | Identiteitskaart van de gebruiker zoals koekje identiteitskaart of identiteitskaart of MCID etc. <br> **Voorbeeld:** 1734876272540865634468320891369597404 |
| namespace (String) | Waar | Naamruimte die wordt gebruikt om de paden en daardoor het model samen te stellen. <br> **Voorbeeld:** steun |
| touchpointsDetail (Object Array) | Waar | De lijst met gegevens van aanraakpunten die leiden tot de conversie die is besteld door | aanraakpunt of tijdstempel. |
| touchpointName (String) | Waar | Naam van touchpoint dat tijdens opstelling werd gevormd. <br> **Voorbeeld:** PAID_SEARCH_CLICK |
| scores (Object) | Waar | Aanraakpuntbijdrage voor deze conversie als score. Voor meer informatie over de scores die in dit object worden geproduceerd, raadpleegt u de [geaggregeerde delingscores](#aggregated-attribution-scores) sectie. |
| touchPoint (Object) | Waar | Metagegevens aanraakpunt. Voor meer informatie over de scores die in dit object worden geproduceerd, raadpleegt u de [geaggregeerde scores](#aggregated-scores) sectie. |

### Onbewerkte muziekpaden weergeven (UI) {#raw-score-path}

U kunt het pad naar de onbewerkte scores weergeven in de gebruikersinterface. Begin door te selecteren **[!UICONTROL Schemas]** in de gebruikersinterface van het Platform zoekt en selecteert u vervolgens in het gedeelte **[!UICONTROL Browse]** tab.

![Schema kiezen](./images/input-output/schemas_browse.png)

Selecteer vervolgens een veld in het dialoogvenster **[!UICONTROL Structure]** het venster van de UI, **[!UICONTROL Field properties]** wordt geopend. Within **[!UICONTROL Field properties]** Dit is het padveld dat wordt toegewezen aan de onbewerkte scores.

![Een schema kiezen](./images/input-output/field_properties.png)


### Geaggregeerde delingsscores {#aggregated-attribution-scores}

Geaggregeerde scores kunnen in CSV-indeling worden gedownload via de gebruikersinterface van het Platform als het datumbereik minder dan 30 dagen bedraagt.

Attribution AI ondersteunt twee categorieën attributiescore, algoritmische en op regels gebaseerde scores.

Attribution AI produceert twee verschillende typen algoritmische scores, incrementeel en beïnvloed. Een beïnvloede score is de fractie van de omzetting die elk marketing aanraakpunt voor verantwoordelijk is. Een incrementele score is de hoeveelheid marginale impact die rechtstreeks wordt veroorzaakt door het marketingaanraakpunt. Het belangrijkste verschil tussen de incrementele score en de beïnvloede score is dat de incrementele score rekening houdt met het basislijneffect. Zij gaat er niet van uit dat een conversie uitsluitend door de voorafgaande marketingaanraakpunten wordt veroorzaakt.

Hier volgt een snel voorbeeld van een Attribution AI-schema-uitvoer uit de Adobe Experience Platform-gebruikersinterface:

![](./images/input-output/schema_screenshot.png)

Zie de tabel hieronder voor meer informatie over elk van deze toewijzingsscores:

| Attributiescores | Beschrijving |
| ----- | ----------- |
| Invloed (algoritmisch) | De beïnvloede score is de fractie van de omzetting die elk marketing aanraakpunt voor verantwoordelijk is. |
| Incrementeel (algoritmisch) | De incrementele score is de hoeveelheid marginale impact die rechtstreeks wordt veroorzaakt door een marketingaanraakpunt. |
| Eerste aanraking | Op regel gebaseerde attributiescore die alle credits toewijst aan het eerste aanraakpunt op een conversiepad. |
| Laatste aanraking | Op regel gebaseerde attributiescore die alle punten toewijst aan het aanraakpunt dat het dichtst bij de conversie ligt. |
| Lineair | Op regel gebaseerde attributiescore die gelijk krediet aan elk aanraakpunt op een conversiepad toewijst. |
| U-vorm | Op regels gebaseerde attributiescore die 40% van het krediet toewijst aan het eerste aanraakpunt en 40% van het krediet aan het laatste aanraakpunt, waarbij de andere aanraakpunten de resterende 20% gelijkmatig verdelen. |
| Tijdverlies | Op regels gebaseerde attributiescore waarbij aanraakpunten die dichter bij de conversie liggen, meer krediet krijgen dan aanraakpunten die verder van de conversie verwijderd zijn. |

**Verwijzing naar ruwe score (toewijzingsscores)**

In de onderstaande tabel worden de toewijzingsscores toegewezen aan de onbewerkte scores. Als u de onbewerkte scores wilt downloaden, gaat u naar de [scores downloaden in Attribution AI](./download-scores.md) documentatie.

| Attributiescores | Referentiekolom ruwe score |
| --- | --- |
| Invloed (algoritmisch) | _huurderID.your_schema_name.element.touchpoint.algorithmInfluenced |
| Incrementeel (algoritmisch) | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmInfluenced |
| Eerste aanraking | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Laatste aanraking | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Lineair | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U-vorm | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.Shape |
| Tijdverlies | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Geaggregeerde scores {#aggregated-scores}

Geaggregeerde scores kunnen in CSV-indeling worden gedownload via de gebruikersinterface van het Platform als het datumbereik minder dan 30 dagen bedraagt. Zie de tabel hieronder voor meer informatie over elk van deze geaggregeerde kolommen.

| Kolomnaam | Restrictie | Niet invulbaar | Beschrijving |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Door gebruiker gedefinieerde en vaste indeling | Onwaar | Datum van klantgebeurtenis in de notatie JJJJ-MM-DD. <br> **Voorbeeld**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Door gebruiker gedefinieerde en vaste indeling | Waar | Datum aanraakpunt voor media in de notatie JJJJ-MM-DD <br> **Voorbeeld**: 21-04-2017 |
| segment (String) | Berekend | Onwaar | Conversiesegment zoals geo-segmentatie waarop het model is gebouwd. In het geval van afwezigheid van segmenten, is het segment gelijk aan conversion_scope. <br> **Voorbeeld**: ORDER_AMER |
| conversion_scope (String) | Door gebruiker gedefinieerd | Onwaar | Naam van de Conversie zoals die door de gebruiker wordt gevormd. <br> **Voorbeeld**: VOLGORDE |
| touchpoint_scope (String) | Door gebruiker gedefinieerd | Waar | Naam van het aanraakpunt zoals geconfigureerd door de gebruiker <br> **Voorbeeld**: PAID_SEARCH_CLICK |
| product (String) | Door gebruiker gedefinieerd | Waar | De XDM-id van het product. <br> **Voorbeeld**: CC |
| product_type (String) | Door gebruiker gedefinieerd | Waar | De weergavenaam van het product zoals deze aan de gebruiker wordt getoond voor deze productweergave. <br> **Voorbeeld**: gpus, laptops |
| geo (String) | Door gebruiker gedefinieerd | Waar | De geografische locatie waar de conversie is uitgevoerd (placeContext.geo.countryCode) <br> **Voorbeeld**: VS |
| event_type (String) | Door gebruiker gedefinieerd | Waar | Het primaire gebeurtenistype voor deze tijdreeksrecord <br> **Voorbeeld**: Betaalde omzetting |
| media_type (String) | ENUM | Onwaar | Beschrijft of het mediatype betaald, bezeten of verdiend is. <br> **Voorbeeld**: BETAALD, EIGENAAR |
| kanaal (String) | ENUM | Onwaar | De `channel._type` eigenschap die wordt gebruikt voor een ruwe classificatie van kanalen met vergelijkbare eigenschappen in [!DNL Consumer Experience Event] XDM. <br> **Voorbeeld**: ZOEKEN |
| action (String) | ENUM | Onwaar | De `mediaAction` eigenschap wordt gebruikt om een type &#39;experience&#39;-mediakactie te bieden. <br> **Voorbeeld**: KLIKKEN |
| campagne_group (String) | Door gebruiker gedefinieerd | Waar | Naam van de campagnegroep waarbij meerdere campagnes zijn gegroepeerd, zoals &#39;50%_DISCOUNT&#39;. <br> **Voorbeeld**: COMMERCIEEL |
| campagne_name (String) | Door gebruiker gedefinieerd | Waar | Naam van de campagne die wordt gebruikt om marketingcampagne zoals &#39;50%_DISCOUNT_USA&#39; of &#39;50%_DISCOUNT_ASIA&#39; te identificeren. <br> **Voorbeeld**: Thanksgiving Sale |

**Verwijzing naar ruwe score (geaggregeerd)**

In de onderstaande tabel worden de geaggregeerde scores toegewezen aan de onbewerkte scores. Als u de onbewerkte scores wilt downloaden, gaat u naar de [scores downloaden in Attribution AI](./download-scores.md) documentatie. Ga naar het gedeelte over [onbewerkte muziekpaden weergeven](#raw-score-path) in dit document.

| Kolomnaam | Referentiekolom Onbewerkte score |
| --- | --- |
| customerevents_date | tijdstempel |
| mediatouchpoints_date | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segment | _huurderID.your_schema_name.segmentation |
| conversion_scope | _huurderID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _huurderID.your_schema_name.touchpointsDetail.element.touchpointName |
| product | _huurderID.your_schema_name.conversion.product |
| product_type | _huurderID.your_schema_name.conversion.product_type |
| geo | _huurderID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| action | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campagne_groep | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.campagneGroup |
| campagne_naam | _huurderID.your_schema_name.touchpointsDetail.element.touchpoint.campagneName |


## Volgende stappen {#next-steps}

Nadat u de gegevens hebt voorbereid en al uw gegevens en schema&#39;s hebt geïnstalleerd, begint u met het volgende: [Gebruikershandleiding voor Attribution AI](./user-guide.md). Deze gids begeleidt u door het creëren van een geval voor Attribution AI.
