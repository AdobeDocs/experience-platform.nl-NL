---
title: Behoud de Dataset van de Gebeurtenis van de Ervaring in het meer van Gegevens beheren gebruikend TTL
description: Leer hoe u het behoud van de Experience Event-gegevensset in het datumpomeer kunt evalueren, instellen en beheren met TL-configuraties (Time-to-Live) met Adobe Experience Platform API's. In deze handleiding wordt uitgelegd hoe de vervaldatum van TTL op rijniveau het beleid voor gegevensbewaring ondersteunt, de opslagefficiëntie optimaliseert en een effectief beheer van de levenscyclus van gegevens garandeert. Het verstrekt ook gebruiksgevallen en beste praktijken om u te helpen TTL effectief toepassen.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 0%

---

# Behoud van de Dataset van de Gebeurtenis van de Ervaring beheren in het gegevenspeer gebruikend TTL

Efficiënt gegevensbeheer is van essentieel belang voor optimale prestaties, kostenbeheersing en gegevensintegriteit. De Behoud Tijd-aan-Levende van de Dataset van de Gebeurtenis van de Ervaring (TTL) om rij-vlakke verval af te dwingen, automatisch verwijderend verslagen uit datasets in het gegevenspeer terwijl het verzekeren van optimale opslagefficiency en gegevensrelevantie.

Deze gids verklaart hoe te om TTL te evalueren, te plaatsen en te beheren gebruikend de Dienst API van de Catalogus. U zult leren wanneer en waarom om TTL toe te passen, hoe te om de waarden van TTL te vormen en bij te werken gebruikend API vraag, en beste praktijken om efficiënte implementatie te verzekeren.

>[!IMPORTANT]
>
> TTL is ontworpen om beheer van de gegevenslevenscyclus en opslagefficiency te optimaliseren. Het is geen nalevingsinstrument en mag niet worden gebruikt voor regelgevingsvereisten. De naleving vereist vaak bredere strategieën voor gegevensbeheer.

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
>
>De configuraties van TTL helpen u opslag optimaliseren die op aanspraken wordt gebaseerd. Hoewel gegevens uit de profielopslag (gebruikt in Real-Time CDP) na 30 dagen als &#39;stale&#39; en &#39;verwijder&#39; kunnen worden beschouwd, kunnen dezelfde gebeurtenisgegevens in het datumpomeer gedurende 12-13 maanden (of langer op basis van &#39;machtiging&#39;) beschikbaar blijven voor gebruik door Analytics en Data Distiller.

### Voorbeeld van industrie {#industry-example}

Neem bijvoorbeeld een service voor videostreaming die gebruikersinteracties bijhoudt, zoals videoweergaven, zoekopdrachten en aanbevelingen. Terwijl recente betrokkenheidsgegevens van cruciaal belang zijn voor personalisatie, verliezen oudere activiteitenlogboeken (bijvoorbeeld interacties van meer dan een jaar geleden) de relevantie. Door rijverloop te gebruiken, verwijdert Experience Platform automatisch verouderde logboeken, die ervoor zorgen slechts huidige en zinvolle gegevens voor analyses en aanbevelingen worden gebruikt.

## Evalueer de geschiktheid van TTL

Alvorens een behoudbeleid toe te passen, bepaal of uw dataset een goede kandidaat voor rij-vlakke afloop is. Overweeg het volgende:

- relevantie van gegevens in de loop van de tijd: verschaffen oudere gegevens waarde of wordt het verouderd?
- Effect op downstreamprocessen: heeft het verwijderen van gegevens gevolgen voor rapportage, analyse of integratie?
- Opslagkosten versus retentiewaarde: rechtvaardigt de waarde van oudere gegevens de opslagkosten?

Indien historische gegevens van essentieel belang zijn voor langetermijnanalyse of bedrijfsactiviteiten, is TTL wellicht niet de juiste aanpak. Als u deze factoren controleert, zorgt u ervoor dat TTL wordt afgestemd op de behoeften voor gegevensopslag zonder dat dit negatieve gevolgen heeft voor de beschikbaarheid van gegevens.

## Uw vragen plannen

Alvorens TTL toe te passen, gebruik vragen om datasetgrootte en relevantie te analyseren. Het runnen van gerichte vragen helpt bepalen hoeveel gegevens onder verschillende configuraties van TTL worden behouden of worden verwijderd.

De volgende SQL-query telt bijvoorbeeld het aantal records dat in de laatste 30 dagen is gemaakt:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

Het runnen van gelijkaardige vragen voor verschillende tijdintervallen helpt de montages van TTL bevestigen en verzekeren zij opslagefficiency en gegevenstoegankelijkheid in evenwicht brengen.

## Aan de slag met TTL-beheer

Voordat u de bewaring van de Dataset van de Gebeurtenis van de Ervaring kunt evalueren, instellen en beheren met de API van de Catalogusservice, moet u begrijpen hoe u uw verzoeken correct opmaakt. Dit omvat het kennen van de API wegen, het verstrekken van vereiste kopballen, en het formatteren verzoeklading. Verwijs naar de [ Begonnen gids van de Dienst API van de Catalogus ](../api/getting-started.md) voor deze essentiële informatie.

>[!NOTE]
>
>Dit document behandelt rij-vlakke afloop, die individuele verlopen rijen binnen een dataset schrapt terwijl het houden van de dataset zelf intact. Het is niet op datasetvervaldatum van toepassing, die volledige datasets verwijdert en door een afzonderlijke eigenschap wordt beheerd. Voor dataset-vlakke afloop, verwijs naar de [ API documentatie van de datasetvervaldatum ](../../hygiene/api/dataset-expiration.md).

### Hoe te om huidige montages van TTL te controleren

Om met uw beheer van TTL te beginnen, controleer eerst huidige montages van TTL. Maak een GET verzoek aan het `/ttl/{datasetId}` eindpunt om de standaard, maximum, en minimum montages van TTL voor een dataset terug te winnen. Deze stap is noodzakelijk omdat de regels van TTL gebaseerd op het datasettype kunnen variëren.

>[!TIP]
>
>De Experience Platform Gateway-URL en het basispad voor de Catalog Service API zijn: `https://platform.adobe.io/data/foundation/catalog` .

**API formaat**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | Een door het systeem gegenereerde tekenreeks die een gegevensset uniek identificeert. Als u een gegevensset-id wilt zoeken, gebruikt u het eindpunt `/datasets` . Zie de [ gids van de lijstcatalogusvoorwerpen API ](../api/list-objects.md) voor instructies bij het filtreren van reacties voor relevante datasets. |

**Verzoek**

Het volgende verzoek wint de montages van TTL van uw organisatie voor een bepaalde dataset terug.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/5ba9452f7de80408007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Reactie**

Een succesvolle reactie keert de configuratie van TTL voor de dataset, met inbegrip van het gebrek, maximum, en minimumwaarden van TTL voor zowel `adobe_lakeHouse` als `adobe_unifiedProfile` opslag terug.

+++Selecteren om het antwoord weer te geven

```json
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P30D"
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Eigenschap | Beschrijving |
|--------------|-------------|
| `defaultValue` | De standaard toegepaste periode van TTL als geen aangepaste TTL wordt geplaatst. |
| `maxValue` | De langste TTL die voor de dataset wordt toegestaan. Indien null, is er geen maximumlimiet. |
| `minValue` | De kortste TTL stond toe om naleving van systeembeleid te verzekeren. |

<!-- Q) what is the default Max and Min values and are they system-imposed? -->

### Hoe te om TTL voor een dataset te plaatsen {#set-ttl}

>[!IMPORTANT]
>
>Rij-vervaldatum kan slechts op gebeurtenisdatasets worden toegepast die een tijdreeksschema gebruiken. Voordat u TTL instelt, controleert u of het schema van de gegevensset `https://ns.adobe.com/xdm/data/time-series` wordt uitgebreid om ervoor te zorgen dat de API-aanvraag succesvol is. Gebruik de API voor schemaregistratie om de schemagegevens op te halen en de eigenschap `meta:extends` te verifiëren. Verwijs naar de [ documentatie van het eindpunt van het Schema ](../../xdm/api/schemas.md#lookup) voor begeleiding op hoe te om dit te doen.

Om het Behouden van de Dataset van de Gebeurtenis van de Ervaring voor uw dataset te vormen, plaats een nieuwe waarde van TTL door een verzoek van PATCH aan het `/v2/datasets/{ID}` eindpunt te doen.

**API formaat**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | Identiteitskaart van de dataset u de waarde van TTL voor wilt bijwerken. |

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt `ttlValue` ingesteld op `P3M` . Hierdoor worden records ouder dan drie maanden automatisch verwijderd. U kunt de bewaarperiode aanpassen aan uw bedrijfsbehoeften met behulp van waarden zoals `P6M` gedurende zes maanden of `P12M` gedurende één jaar.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

Een succesvolle reactie toont de configuratie van TTL voor de dataset. Dit bevat details over verloopinstellingen op rijniveau voor zowel `adobe_lakeHouse` als `adobe_unifiedProfile` -opslag.

+++Selecteren om het antwoord weer te geven

```JSON
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Eigenschap | Beschrijving |
|----------------------------------|-------------|
| `extensions` | Een container voor aanvullende metagegevens die betrekking hebben op de gegevensset. |
| `extensions.adobe_lakeHouse` | Specificeert montages met betrekking tot opslagarchitectuur, met inbegrip van rij-vlakke vervalconfiguraties |
| `rowExpiration` | Het object bevat TTL-instellingen die de retentieperiode voor de gegevensset definiëren. |
| `rowExpiration.ttlValue` | Bepaalt de duur alvorens de verslagen in de dataset automatisch worden verwijderd. Gebruikt de notatie ISO-8601 punt (bijvoorbeeld `P3M` gedurende 3 maanden of `P30D` gedurende één week). |
| `rowExpiration.valueStatus` | De tekenreeks geeft aan of de TTL-instelling een standaardsysteemwaarde is of een aangepaste waarde die door een gebruiker is ingesteld. Mogelijke waarden zijn: `default` , `custom` . |
| `rowExpiration.setBy` | Geeft aan wie de TTL-instelling het laatst heeft gewijzigd. Mogelijke waarden zijn: `user` (handmatig ingesteld) of `service` (automatisch toegewezen). |
| `rowExpiration.updated` | De tijdstempel van de laatste TTL-update. Deze waarde geeft aan wanneer de TTL-instelling voor het laatst is gewijzigd. |

### TTL bijwerken {#update-ttl}

Breid of verkort de bewaartermijn uit om uw bedrijfsbehoeften aan te passen door TTL aan te passen. Wanneer het platform voor videostreaming bijvoorbeeld eerder wordt genoemd, kan het platform de TTL aanvankelijk instellen op drie maanden om ervoor te zorgen dat er nieuwe betrokkenheidsgegevens beschikbaar zijn voor personalisatie. Als uit hun analyse echter blijkt dat interactiepatronen ouder dan drie maanden nog steeds waardevolle inzichten opleveren, kunnen zij de periode van de GVTO verlengen tot zes maanden om oudere registers bij te houden voor betere aanbevolen modellen.

Als u een bestaande TTL-waarde wilt wijzigen, gebruikt u de methode `PATCH` op het `/v2/datasets/{DATASET_ID}` -eindpunt.

#### API-indeling

```http
PATCH /v2/datasets/{DATASET_ID}
```

**Verzoek**

In het volgende verzoek wordt de TTL bijgewerkt tot zes maanden (`P6M`) die de periode van het registreren vóór automatische schrapping verlengen.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

<!-- Q) For Clarity, should this example show both data stores being updated by expanding the example payload above? -->

**Reactie**

```JSON
{  "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
              "ttlValue": "P6M",
              "valueStatus": "custom",
              "setBy": "user",
              "updated": "1737977766499"
            }
        },
        "adobe_unifiedProfile": {
            "rowExpiration": {
                "ttlValue": "P3M",
                "valueStatus": "custom",
                "setBy": "user",
                "updated": "17379754766355"
            }
        }
    }
}
```

## Aanbevolen procedures voor het instellen van TTL {#best-practices}

Het kiezen van de juiste TTL-waarde is van cruciaal belang om ervoor te zorgen dat uw beleid voor het bewaren van gegevens van de Dataset van de Gebeurtenis een evenwicht biedt tussen gegevensbewaring, opslagefficiëntie en analytische behoeften. Een TTL die te kort is kan gegevensverlies veroorzaken, terwijl één die te lang is kan opslagkosten en onnodige gegevensaccumulatie verhogen. Zorg ervoor dat TTL zich aan het doel van uw dataset door te overwegen richt hoe vaak de gegevens worden betreden en hoe lang het relevant blijft.

De lijst hieronder verstrekt gemeenschappelijke aanbevelingen van TTL die op datasettype en gebruikspatronen worden gebaseerd:

| Type gegevensset | Aanbevolen TTL | Gebruiksscenario&#39;s |
|-----------------------------|------------------------|-------------------|
| Veelgebruikte gegevenssets | 30-90 dagen | Logbestanden voor betrokkenheid van gebruikers, klikstreamgegevens van websites, gegevens over prestaties van campagnes op korte termijn. |
| Gegevensbestanden archiveren | 1 jaar of meer | Logboeken van financiële transacties, nalevingsgegevens, trendanalyse op lange termijn, gegevensreeksen voor opleiding van machinaal leren. |
| Door toepassingen beheerde gegevenssets | Tot 13 maanden | De systeem-beheerde datasets hebben vooraf bepaalde beperkingen van TTL, die automatisch worden afgedwongen om aan systeem-opgelegde grenzen te voldoen. |
| Door de klant beheerde gegevenssets | 30 dagen - Max TTL | Datasets die zijn gemaakt via de UI, API&#39;s of Data Distiller. De GVTO moet ten minste 30 dagen zijn en binnen de vastgestelde maximale TTL liggen. |

Controleer periodiek de montages van TTL om ervoor te zorgen zij zich aan uw opslagbeleid, analytische behoeften, en bedrijfsvereisten blijven richten.

### Belangrijke overwegingen bij het instellen van TTL

<!-- What are the default TTL limits for system-generated Profile Store and data lake datasets? -->

<!-- Q) Are the limits: 90 days for data in the Profile store and 13 months for data in the data lake? This is true for Journey Optimizer. -->

Volg deze beste praktijken om ervoor te zorgen dat de montages van TTL zich aan uw strategie van het gegevensbehoud richten:

- Wijzigingen in TTL regelmatig controleren. Elke update van TTL activeert een controlegebeurtenis. De controlelogboeken van het gebruik om de wijzigingen van TTL voor naleving, gegevensbeheer, en het oplossen van problemendoeleinden te volgen.
- Verwijder TTL als de gegevens voor onbepaalde tijd moeten worden bewaard. Als u TTL wilt uitschakelen, stelt u `ttlValue` in op `null` . Hiermee voorkomt u automatische vervaldatums en behoudt u alle records permanent. Houd rekening met de gevolgen voor de opslag voordat u deze wijziging aanbrengt.

<!-- Q) Are there any specific system constraints or impacts of setting TTL to null? -->

## Beperkingen van TTL {#limitations}

Houd rekening met de volgende beperkingen bij het gebruik van TTL:

- **het Behouden van de Dataset van de Gebeurtenis van de Ervaring gebruikend TTL is op rij-vlakke afloop**, niet datasetschrapping van toepassing. TTL verwijdert verslagen die op een bepaalde bewaartermijn worden gebaseerd maar schrapt geen volledige datasets. Om een dataset te verwijderen, gebruik het [ eindpunt van de gegevenssetvervalsing ](../../hygiene/api/dataset-expiration.md) of handschrapping.
- **TTL kan niet worden verwijderd**, slechts worden bijgewerkt. Zodra toegepast, kan TTL niet worden geschrapt, maar u kunt [ de behoudperiode ](#update-ttl) wijzigen om het te verlengen of te verkorten. Om gegevens voor onbepaalde tijd te behouden, plaats voldoende lange TTL in plaats van het proberen om het te verwijderen.
- **TTL is geen nalevingshulpmiddel**. TTL optimaliseert opslag en gegevenslevenscyclusbeheer maar voldoet niet aan de vereisten van de regelgevende gegevensbewaring. Omwille van de naleving moeten bredere strategieën voor gegevensbeheer worden geïmplementeerd.

## Veelgestelde vragen over beleid voor gegevensbewaring {#faqs}

In deze sectie worden antwoorden gegeven op veelgestelde vragen over het beleid voor het bewaren van gegevenssets in Adobe Experience Platform.

### Op welke soorten datasets kan ik de regels van het behoudbeleid toepassen?

+++Antwoord
U kunt retentiebeleid toepassen op gegevenssets die zijn gemaakt met de klasse XDM ExperienceEvent. Voor de diensten van het Profiel, zijn het behoudbeleid slechts van toepassing op de datasets van de Gebeurtenis van de Ervaring die profiel-toegelaten zijn geweest.
+++

### Hoe snel zal de baan van het Behoud Dataset gegevens van de diensten van het gegevenspeer schrappen?

+++Antwoord
Dataset-TTL&#39;s worden wekelijks geëvalueerd en verwerkt, waarbij alle verlopen records worden verwijderd. Een gebeurtenis wordt als verlopen beschouwd als deze meer dan 30 dagen geleden in Experience Platform is ingeslikt (innamedatum > 30 dagen) en de gebeurtenisdatum ervan de gedefinieerde retentieperiode (TTL) overschrijdt.
+++

### Hoe snel zal de baan van het Behoud Dataset gegevens van de diensten van het Profiel schrappen?

+++Antwoord
Nadat een retentiebeleid is ingesteld, worden bestaande gebeurtenissen in Experience Platform onmiddellijk verwijderd als de tijdstempel van de gebeurtenis de retentieperiode (TTL) overschrijdt. Nieuwe gebeurtenissen worden verwijderd als de tijdstempel langer is dan de retentieperiode.

Als u bijvoorbeeld op 15 mei een vervalbeleid van 30 dagen toepast, gebeurt het volgende:

- Nieuwe gebeurtenissen krijgen een vervaldatum van 30 dagen wanneer ze worden opgenomen.
- Bestaande gebeurtenissen met een tijdstempel die ouder is dan 15 april, worden onmiddellijk verwijderd.
- Bestaande gebeurtenissen met een tijdstempel na 15 april verlopen 30 dagen na hun tijdstempel (een gebeurtenis vanaf 18 april wordt bijvoorbeeld op 18 mei verwijderd).
+++

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
