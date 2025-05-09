---
title: Behoud de Dataset van de Gebeurtenis van de Ervaring in het meer van Gegevens beheren gebruikend TTL
description: Leer hoe u het behoud van de Experience Event-gegevensset in het datumpomeer kunt evalueren, instellen en beheren met TL-configuraties (Time-to-Live) met Adobe Experience Platform API's. In deze handleiding wordt uitgelegd hoe de vervaldatum van TTL op rijniveau het beleid voor gegevensbewaring ondersteunt, de opslagefficiëntie optimaliseert en een effectief beheer van de levenscyclus van gegevens garandeert. Het verstrekt ook gebruiksgevallen en beste praktijken om u te helpen TTL effectief toepassen.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 13db0477c0f42d0808647937d40c25b47a270894
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 0%

---

# Behoud van de Dataset van de Gebeurtenis van de Ervaring beheren in het gegevenspeer gebruikend TTL

Efficiënt gegevensbeheer is van essentieel belang voor optimale prestaties, kostenbeheersing en gegevensintegriteit. De Behoud Tijd-aan-Levende van de Dataset van de Gebeurtenis van de Ervaring (TTL) om rij-vlakke verval af te dwingen, automatisch verwijderend verslagen uit datasets in het gegevenspeer terwijl het verzekeren van optimale opslagefficiency en gegevensrelevantie.

Deze gids verklaart hoe te om TTL te evalueren, te plaatsen en te beheren gebruikend de Dienst API van de Catalogus. U zult leren wanneer en waarom om TTL toe te passen, hoe te om de waarden van TTL te vormen en bij te werken gebruikend API vraag, en beste praktijken om efficiënte implementatie te verzekeren.

>[!IMPORTANT]
>
>TTL is ontworpen om beheer van de gegevenslevenscyclus en opslagefficiency te optimaliseren. Het is geen nalevingsinstrument en mag niet worden gebruikt voor regelgevingsvereisten. De naleving vereist vaak bredere strategieën voor gegevensbeheer.

## Waarom TTL voor rij-vlakke gegevensbeheer gebruiken

Naarmate datasets groeien, wordt een efficiënt gegevensbeheer steeds belangrijker om de prestaties te behouden, de kosten te beheersen en de gegevens relevant te houden. Op TTL-Gebaseerde rij-vlakke gegevensvervalsing automatiseert gegevensschoonmaak door verouderde verslagen zonder handinterventie te verwijderen om opslag te helpen optimaliseren en systeemefficiency te verbeteren.

TTL is nuttig wanneer het beheren van tijd-gevoelige gegevens die relevantie in tijd verliezen. Overweeg het uitvoeren van TTL als u moet:

- Verlaag de opslagkosten door verouderde records automatisch te verwijderen.
- Verbeter vraagprestaties door irrelevante gegevens te minimaliseren.
- Behoud de gegevenshygiëne door alleen relevante informatie te bewaren.
- Optimaliseer het bewaren van gegevens om bedrijfsdoelstellingen te steunen.

>[!NOTE]
>
>De Behoud van de Dataset van de Gebeurtenis van de ervaring is op gebeurtenisgegevens van toepassing die in het gegevensmeer worden opgeslagen. Als u behoud in Real-Time Customer Data Platform beheert, overweeg het gebruiken van [ Verlopen van de Gebeurtenis van de Ervaring ](../../profile/event-expirations.md) en [ de Zijdeloze Verlopen van het Profiel ](../../profile/pseudonymous-profiles.md) naast de montages van het het behoud van het gegevensmeer.

Gebruik TTL-configuraties om opslag te optimaliseren op basis van rechten. Hoewel gegevens uit de profielopslag (gebruikt in Real-Time CDP) na 30 dagen als &#39;stale&#39; en &#39;verwijder&#39; kunnen worden beschouwd, kunnen dezelfde gebeurtenisgegevens in het datumpomeer gedurende 12-13 maanden (of langer op basis van &#39;machtiging&#39;) beschikbaar blijven voor gebruik door Analytics en Data Distiller.

>[!TIP]
>
>De rechten hebben betrekking op de opslag- en bewaarrechten die zijn vastgelegd in uw Adobe-abonnement- en -licentieovereenkomsten.

### Voorbeeld van industrie {#industry-example}

Neem bijvoorbeeld een service voor videostreaming die gebruikersinteracties bijhoudt, zoals videoweergaven, zoekopdrachten en aanbevelingen. Terwijl recente betrokkenheidsgegevens van cruciaal belang zijn voor personalisatie, verliezen oudere activiteitenlogboeken (bijvoorbeeld interacties van meer dan een jaar geleden) de relevantie. Door rijverloop te gebruiken, verwijdert Experience Platform automatisch verouderde logboeken, die ervoor zorgen slechts huidige en zinvolle gegevens voor analyses en aanbevelingen worden gebruikt.

## Evalueer de geschiktheid van TTL {#evaluate-ttl-suitability}

Alvorens een behoudbeleid toe te passen, bepaal of uw dataset een goede kandidaat voor rij-vlakke afloop is. Overweeg het volgende:

- relevantie van gegevens in de loop van de tijd: verschaffen oudere gegevens waarde of wordt het verouderd?
- Effect op downstreamprocessen: heeft het verwijderen van gegevens gevolgen voor rapportage, analyse of integratie?
- Opslagkosten versus retentiewaarde: rechtvaardigt de waarde van oudere gegevens de opslagkosten?

Indien historische gegevens van essentieel belang zijn voor langetermijnanalyse of bedrijfsactiviteiten, is TTL wellicht niet de juiste aanpak. Als u deze factoren controleert, zorgt u ervoor dat TTL wordt afgestemd op de behoeften voor gegevensopslag zonder dat dit negatieve gevolgen heeft voor de beschikbaarheid van gegevens.

## Aanbevolen procedures voor het instellen van TTL {#best-practices}

Selecteer de juiste TTL-waarde om ervoor te zorgen dat het beleid voor het bewaren van gegevens van de Dataset van de Gebeurtenis een evenwicht biedt tussen gegevensbewaring, opslagefficiëntie en analytische behoeften. Een TTL die te kort is kan gegevensverlies veroorzaken, terwijl één die te lang is kan opslagkosten en onnodige gegevensaccumulatie verhogen. Zorg ervoor dat TTL zich aan het doel van uw dataset door te overwegen richt hoe vaak de gegevens worden betreden en hoe lang het relevant blijft.

De lijst hieronder verstrekt gemeenschappelijke aanbevelingen van TTL die op datasettype en gebruikspatronen worden gebaseerd:

| Type gegevensset | Aanbevolen TTL | Gebruiksscenario&#39;s |
|-----------------------------|------------------------|-------------------|
| Veelgebruikte gegevenssets | 30-90 dagen | Logbestanden voor betrokkenheid van gebruikers, klikstreamgegevens van websites, gegevens over prestaties van campagnes op korte termijn. |
| Gegevensbestanden archiveren | 1 jaar of meer | Logboeken van financiële transacties, nalevingsgegevens, trendanalyse op lange termijn, gegevensreeksen voor opleiding van machinaal leren. |
| Door toepassingen beheerde gegevenssets | Tot 13 maanden | De systeem-beheerde datasets hebben vooraf bepaalde beperkingen van TTL, die automatisch worden afgedwongen om aan systeem-opgelegde grenzen te voldoen. |
| Door de klant beheerde gegevenssets | 30 dagen - Max TTL | Datasets die zijn gemaakt via de UI, API&#39;s of Data Distiller. De GVTO moet ten minste 30 dagen zijn en binnen de vastgestelde maximale TTL liggen. |

Controleer periodiek de montages van TTL om ervoor te zorgen zij zich aan uw opslagbeleid, analytische behoeften, en bedrijfsvereisten blijven richten.

### Belangrijke overwegingen bij het instellen van TTL {#key-considerations}

Volg deze beste praktijken om ervoor te zorgen dat de montages van TTL zich aan uw strategie van het gegevensbehoud richten:

- Wijzigingen in TTL regelmatig controleren. Elke update van TTL activeert een controlegebeurtenis. De controlelogboeken van het gebruik om de wijzigingen van TTL voor naleving, gegevensbeheer, en het oplossen van problemendoeleinden te volgen.
- Schakel TTL uit als de gegevens voor onbepaalde tijd moeten worden bewaard. Als u TTL wilt uitschakelen, stelt u `ttlValue` in op `null` . Hiermee voorkomt u automatische vervaldatums en behoudt u alle records permanent. Houd rekening met de gevolgen voor de opslag voordat u deze wijziging aanbrengt.

## Beperkingen van TTL {#limitations}

Houd rekening met de volgende beperkingen bij het gebruik van TTL:

- **het Behouden van de Dataset van de Gebeurtenis van de Ervaring gebruikend TTL is op rij-vlakke afloop**, niet datasetschrapping van toepassing. TTL verwijdert verslagen die op een bepaalde bewaartermijn worden gebaseerd maar schrapt geen volledige datasets. Om een dataset te verwijderen, gebruik het [ eindpunt van de gegevenssetvervalsing ](../../hygiene/api/dataset-expiration.md) of handschrapping.
- **de configuratie van TTL blijft actief tot uitdrukkelijk gehandicapt**. De configuratie blijft van kracht tot u het onbruikbaar maakt. Als u TTL uitschakelt, wordt de vervaldatum beëindigd en blijven alle records in de gegevensset behouden.
- **TTL is geen nalevingshulpmiddel**. Terwijl TTL opslag en levenscyclusbeheer optimaliseert, moet u bredere beheersstrategieën uitvoeren om regelgevende naleving te verzekeren.

## De grootte en relevantie van gegevenssets analyseren voordat u TTL toepast {#analyze-dataset-size}

Alvorens TTL toe te passen, gebruik vragen om datasetgrootte en relevantie te analyseren. Voer gerichte query&#39;s uit (zoals het tellen van records binnen specifieke datumbereiken) om een voorvertoning te bekijken van de impact van verschillende TTL-waarden. Gebruik deze informatie vervolgens om een optimale retentieperiode te kiezen waarin het nut en de kosteneffectiviteit van de gegevens op elkaar worden afgestemd.

![ een visuele werkschema voor het uitvoeren van TTL op de Datasets van de Gebeurtenis van de Ervaring. De stappen omvatten: beoordelen gegevenslevensduur en effect van verwijdering, bevestigen de montages van TTL met vragen, vormen TTL door de Dienst API van de Catalogus, en controleren onophoudelijk de gevolgen van TTL en maken aanpassingen.](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

Het runnen van gerichte vragen helpt bepalen hoeveel gegevens onder verschillende configuraties van TTL worden behouden of worden verwijderd. De volgende SQL-query telt bijvoorbeeld het aantal records dat in de laatste 30 dagen is gemaakt:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

Het runnen van gelijkaardige vragen voor verschillende tijdintervallen helpt de montages van TTL bevestigen en verzekeren zij opslagefficiency en gegevenstoegankelijkheid in evenwicht brengen.

## Aan de slag met TTL-beheer

Voordat u de bewaring van de Dataset van de Gebeurtenis van de Ervaring kunt evalueren, instellen en beheren met de API van de Catalogusservice, moet u begrijpen hoe u uw verzoeken correct opmaakt. Dit omvat het kennen van de API wegen, het verstrekken van vereiste kopballen, en het formatteren verzoeklading. Verwijs naar de [ Begonnen gids van de Dienst API van de Catalogus ](../api/getting-started.md) voor deze essentiële informatie.

>[!NOTE]
>
>Dit document behandelt rij-vlakke afloop, die individuele verlopen rijen binnen een dataset schrapt terwijl het houden van de dataset zelf intact. Het is niet op datasetvervaldatum van toepassing, die volledige datasets verwijdert en door een afzonderlijke eigenschap wordt beheerd. Voor dataset-vlakke afloop, verwijs naar de [ API documentatie van de datasetvervaldatum ](../../hygiene/api/dataset-expiration.md).

### Controleer uw beperkingen van TTL {#check-ttl-constraints}

Gebruik het eindpunt van de API van de Hygiëne van Gegevens `/ttl/{DATASET_ID}` helpen configuraties plannen TTL. Dit eindpunt keert de minimum en maximumwaarden van TTL terug die voor uw organisatie, samen met een geadviseerde waarde (`defaultValue`) voor het datasettype worden gesteund.

Zie de Adobe Developer [ documentatie van de Hygiëne API van Gegevens ](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl) voor meer informatie.

Om [ te controleren TTL momenteel toegepast op een dataset ](#check-applied-ttl-values), doe een verzoek van GET aan het [ de dienstAPI van de Catalogus ](https://developer.adobe.com/experience-platform-apis/references/catalog/) `/dataSets/{DATASET_ID}` eindpunt in plaats daarvan.

>[!TIP]
>
>De Experience Platform Gateway-URL en het basispad voor de Catalog Service API zijn: `https://platform.adobe.io/data/foundation/catalog` . Het basispad voor de API voor gegevenshygiëne is: `https://platform.adobe.io/data/core/hygiene`

**API formaat**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | Een door het systeem gegenereerde tekenreeks die een gegevensset uniek identificeert. Als u een gegevensset-id wilt zoeken, gebruikt u het eindpunt `/datasets` . Zie de [ gids van de lijstcatalogusvoorwerpen API ](../api/list-objects.md) voor instructies bij het filtreren van reacties voor relevante datasets. |

**Verzoek**

Het volgende verzoek wint de beperkingen van TTL van uw organisatie voor een bepaalde dataset terug.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Reactie**

Een succesvolle reactie keert de geadviseerde, maximum, en minimumwaarden van TTL terug die op de aanspraken van uw organisatie, samen met voorgestelde TTL (`defaultValue`) voor de dataset worden gebaseerd. Deze `defaultValue` is een aanbevolen TTL-duur, alleen ter begeleiding. Het wordt niet toegepast tenzij uitdrukkelijk gevormd door u. De reactie bevat geen aangepaste TTL-waarden die mogelijk al zijn ingesteld. Om huidige TTL voor een dataset te bekijken, gebruik het GET `/catalog/dataSets/{DATASET_ID}` eindpunt.

+++Selecteren om het antwoord weer te geven

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| Eigenschap | Beschrijving |
|--------------|-------------|
| `defaultValue` | Een geadviseerde waarde van TTL voor uw dataset. Deze waarde wordt **niet** automatisch toegepast. U moet uitdrukkelijk plaatsen TTL voor het van kracht worden. |
| `maxValue` | De maximale TTL-duur die wordt toegestaan door de machtiging van uw organisatie. Doorgaans is deze duur 10 jaar (`P10Y`). |
| `minValue` | De minimale TTL-duur die wordt toegestaan door de machtiging van uw organisatie. Doorgaans is deze duur 30 dagen (`P30D`). |

### Hoe te om toegepaste waarden van TTL te controleren {#check-applied-ttl-values}

Om de huidige waarde van TTL te controleren die op een dataset is toegepast, gebruik de volgende API vraag:

```http
GET /dataSets/{DATASET_ID}
```

Deze aanroep retourneert de huidige `ttlValue` (indien ingesteld) sectie `extensions.adobe_lakeHouse.rowExpiration` .

**Verzoek**

Het volgende verzoek wint de waarde van TTL van uw organisatie voor een bepaalde dataset terug.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie omvat het `extensions` voorwerp, dat de huidige configuratie van TTL bevat die op de dataset wordt toegepast. Het onderstaande voorbeeld is afgekapt voor bondigheid.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### TTL voor een dataset instellen of bijwerken {#set-update-ttl}

>[!IMPORTANT]
>
>Op TTL-Gebaseerde rij-vlakke afloop kan slechts op gebeurtenisdatasets worden toegepast die een tijdreeksschema gebruiken. Dit omvat datasets die op de standaard klasse XDM ExperienceEvent evenals douaneschema&#39;s worden gebaseerd die het schema van de Reeks van de Tijd uitbreiden (`https://ns.adobe.com/xdm/data/time-series`).
>
>Alvorens u TTL toepast, gebruik de Registratie API van het Schema om te verifiëren dat het schema van de dataset de correcte uitbreiding door het `meta:extends` bezit te controleren omvat. Zie de [ documentatie van het eindpunt van het Schema ](../../xdm/api/schemas.md#lookup) voor begeleiding op hoe te om dit te doen.

U kunt het Behouden van de Dataset van de Gebeurtenis van de Ervaring vormen door een nieuwe TTL te plaatsen of een bestaande TTL bij te werken gebruikend de zelfde API methode. Gebruik een PATCH-aanvraag voor het `/v2/datasets/{DATASET_ID}` -eindpunt om TTL toe te passen of aan te passen.

**API formaat**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | Identiteitskaart van de dataset u de waarde van TTL voor wilt bijwerken. |

**Verzoek**

In het onderstaande voorbeeld wordt `ttlValue` ingesteld op `P3M` . Dit betekent dat records ouder dan drie maanden automatisch worden verwijderd. Pas de bewaarperiode aan uw bedrijfsbehoeften aan (bijvoorbeeld `P6M` gedurende zes maanden of `P12M` gedurende één jaar).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

| Eigenschap | Beschrijving |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | Bepaalt de duur alvorens de verslagen in de dataset automatisch worden verwijderd. Gebruikt de notatie ISO-8601 punt (bijvoorbeeld `P3M` gedurende 3 maanden of `P30D` gedurende 30 dagen). |

**Reactie**

Een succesvolle reactie keert een verwijzing naar de bijgewerkte dataset terug maar omvat niet uitdrukkelijk de montages van TTL. Om de configuratie van TTL te bevestigen, doe een follow-up `GET /dataSets/{DATASET_ID}` verzoek.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### Voorbeeldscenario {#example-scenario}

Overweeg een videostreamingplatform dat de TTL aanvankelijk op drie maanden zet om nieuwe betrokkenheidsgegevens voor personalisatie te verzekeren. Als uit een latere analyse echter blijkt dat oudere interacties nog steeds waardevolle inzichten opleveren, kan de GVTO tot zes maanden worden verlengd met het volgende verzoek:

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

## Veelgestelde vragen over beleid voor gegevensbewaring {#faqs}

In deze veelgestelde vragen wordt ingegaan op praktische vragen over banen voor gegevenssetbehoud, de onmiddellijke gevolgen van veranderingen van TTL, terugwinningsopties, en hoe de bewaartermijnen tussen de diensten van het Platform verschillen.

### Op welke soorten datasets kan ik de regels van het behoudbeleid toepassen?

+++Antwoord
U kunt op TTL-Gebaseerd behoudbeleid op om het even welke dataset toepassen die tijd-reeksen gedrag gebruikt. Dit omvat datasets die op de standaardklasse XDM ExperienceEvent worden gebaseerd, evenals douaneschema&#39;s die worden ontworpen om tijd-reeksgegevens te vangen.

Voor de vervaldatum op rijniveau gelden de volgende technische voorwaarden:

- Het schema moet worden ontworpen om tijd-reeksgegevens te vangen.
- Het schema moet een tijdstempelveld bevatten dat wordt gebruikt om de vervaldatum te evalueren.
- In de gegevensset moeten gegevens op gebeurtenisniveau worden opgeslagen, meestal met behulp van de klasse XDM ExperienceEvent of door deze uit te breiden.
- De dataset moet in de Dienst van de Catalogus worden geregistreerd, aangezien de montages van TTL via `extensions.adobe_lakeHouse.rowExpiration` worden toegepast.
- TTL-waarden moeten de ISO-8601-duurnotatie gebruiken (bijvoorbeeld `P30D`, `P6M`, `P1Y`).
+++

### Hoe snel zal de baan van het Behoud Dataset gegevens van de diensten van het gegevenspeer schrappen?

+++Antwoord
Dataset-TTL&#39;s worden elke 30 dagen geëvalueerd en verwerkt, waarbij alle verlopen records worden verwijderd. Een gebeurtenis wordt als verlopen beschouwd als deze meer dan 30 dagen geleden in Experience Platform is ingeslikt (innamedatum > 30 dagen) en de gebeurtenisdatum ervan de gedefinieerde retentieperiode (TTL) overschrijdt.
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### Kan ik verschillende bewaarbeleid voor de diensten van het gegevensmeer en van het Profiel plaatsen?

+++Antwoord
Ja, u kunt verschillende behoudsbeleid voor de diensten van het gegevensmeer en van het Profiel plaatsen. De retentieperiode voor profiel mag echter niet korter zijn dan die voor data Lake.
+++

### Hoe kan ik mijn huidige gegevenssetgebruik controleren?

+++Antwoord
U kunt de nieuwste opslaggrootte van gegevenssets controleren voor gegevens in de bestanden Meer en Profiel als aparte maateenheden in de inventariswerkruimte van [!UICONTROL Dataset] . Sorteer de kolommen om de grootste datasets te identificeren en te verifiëren dat het behoudbeleid wordt toegepast.

Raadpleeg het dashboard Licentiegebruik voor informatie over gebruik op sandboxniveau. Zie de [ documentatie van het Gebruik van de Vergunning ](../../dashboards/guides/license-usage.md) voor details.
+++

### Hoe kan ik controleren of de functie voor het bewaren van gegevens is gelukt?

+++Antwoord
U kunt de laatste baan van het gegevensbehoud verifiëren door zijn timestamp in de [ Configuratie UI van het Behoud van de Dataset ](./user-guide.md#data-retention-policy) of op de pagina van de Inventaris van Gegevens te controleren.

U kunt ook een GET-aanvraag indienen bij het volgende eindpunt:

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

De reactie bevat de eigenschap `extensions.adobe_lakeHouse.rowExpiration.lastCompleted` die de Unix-tijdstempel (in milliseconden) aangeeft wanneer de meest recente TTL-taak is voltooid.

Historische rapportage van gegevenssetgebruik is momenteel niet beschikbaar.
+++

### Kan ik verwijderde gegevens herstellen?

+++Antwoord
Neen, zodra een bewaarbeleid wordt toegepast, worden om het even welke gegevens ouder dan de bewaarperiode permanent geschrapt en kunnen niet worden teruggekregen.
+++

### Wat is minimum TTL I kan vormen op een dataset van de Gebeurtenis van de Ervaring van het gegevensmeer?

+++Antwoord
De minimale TTL voor een gegevensmeerervaringsgegevensset is 30 dagen. Het datumpeer functioneert als verwerkings steun en terugwinningssysteem tijdens eerste opname en verwerking. Daarom moeten de gegevens in het datumpeer gedurende ten minste 30 dagen na inname bewaard blijven voordat ze kunnen verlopen.
+++

### Wat als ik sommige gebieden van het gegevensmeer langer dan mijn beleid van TTL moet behouden?

+++Antwoord
Gebruik Data Distiller om specifieke velden buiten de TTL van uw dataset te behouden terwijl u binnen uw gebruiksgrenzen blijft. Creeer een baan die regelmatig slechts de noodzakelijke gebieden aan een afgeleide dataset schrijft. Deze workflow zorgt voor compatibiliteit met een kortere TTL en bewaart kritieke gegevens voor uitgebreid gebruik.

Voor meer details, zie [ afgeleide datasets met SQL gids ](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md) creëren.
+++

## Volgende stappen {#next-steps}

Nu u hebt geleerd hoe te om de montages van TTL voor rij-vlakke afloop te beheren, herzie de volgende documentatie om uw inzicht in het beheer van TTL te bevorderen:

- De banen van het behoud: Leer om datasettermijnen in Experience Platform UI met de [ gids UI van de gegevenslevenscyclus te plannen en te automatiseren ](../../hygiene/ui/dataset-expiration.md), of configuraties van het Behoud van de Dataset te controleren en te verifiëren dat de verlopen verslagen worden geschrapt.
- [ het eindpuntgids van de Vervalsing API van de Dataset ](../../hygiene/api/dataset-expiration.md): Ontdek hoe te om volledige datasets eerder dan enkel rijen te schrappen. Leer hoe u het verlopen van gegevenssets kunt plannen, beheren en automatiseren met behulp van de API voor een efficiënte gegevensopslag.
- [ overzicht van het het gebruiksbeleid van gegevens ](../../data-governance/policies/overview.md): Leer hoe te om uw strategie van het gegevensbehoud met bredere nalevingsvereisten en marketing gebruiksbeperkingen te richten.
