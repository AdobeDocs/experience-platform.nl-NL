---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: 5aad9fa71051a58fe1c4678553f47077d81d23fc

---


# Edge-bestemmingen en -prognoses

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Met het Adobe Experience Platform hebt u in real-time toegang tot gegevens via zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. Adobe-toepassingen zoals Adobe Target en Adobe Campaign maken bijvoorbeeld gebruik van randen om klanten in real-time persoonlijke ervaringen te bieden. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Deze handleiding bevat gedetailleerde instructies voor het gebruik van de Real-Time Customer Profile API voor het werken met randprojecties, inclusief bestemmingen en configuraties.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van Real-time API van het Profiel van de Klant. Lees voordat u verdergaat de handleiding voor ontwikkelaars van [realtime klantprofiel](getting-started.md). Met name bevat de sectie [Aan de](getting-started.md#getting-started) slag van de handleiding voor ontwikkelaars van profielen koppelingen naar verwante onderwerpen, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar API&#39;s van het Experience Platform met succes uit te voeren.

## Projectiebestemmingen

Een projectie kan naar een of meer randen worden gerouteerd door de locaties op te geven waar gegevens moeten worden verzonden. Elke projectiebestemming die wordt gecreeerd heeft een unieke identiteitskaart die dan wordt gebruikt om de projectieconfiguratie tot stand te brengen.

### Alle doelen weergeven

U kunt van de randbestemmingen een lijst maken die reeds voor uw organisatie door een GET verzoek aan het `/config/destinations` eindpunt te maken zijn gecreeerd.

**API-indeling**

```http
GET /config/destinations
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie bevat een `projectionDestinations` array met de details voor elke bestemming die als een afzonderlijk object binnen de array wordt weergegeven. Als er geen projecties zijn geconfigureerd, retourneert de `projectionDestinations` array leeg.

>[!NOTE]
>Deze reactie is verkort voor ruimte en toont slechts twee bestemmingen.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| Eigenschap | Beschrijving |
|---|---|
| `_links.self.href` | Op het hoogste niveau, past de weg aan die wordt gebruikt om het GET verzoek te maken. Binnen elk individueel bestemmingsvoorwerp, kan dit weg in een GET verzoek worden gebruikt om de details van een specifieke bestemming direct te zoeken. |
| `id` | Binnen elk bestemmingsvoorwerp, `"id"` toont read-only, systeem-geproduceerde unieke identiteitskaart voor de bestemming. Deze ID wordt gebruikt wanneer het van verwijzingen voorzien van een specifieke bestemming en wanneer het creëren van projectieconfiguraties. |

Voor meer informatie betreffende de attributen van een individuele bestemming, gelieve de sectie te zien over het [creëren van een bestemming](#create-a-destination) die volgt.

### Een doel maken {#create-a-destination}

Als de bestemming u vereist niet reeds bestaat, kunt u een nieuwe projectiebestemming tot stand brengen door een POST- verzoek aan het `/config/destinations` eindpunt te doen.

**API-indeling**

```http
POST /config/destinations
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe randbestemming gemaakt.

>[!NOTE]
>Voor het POST-verzoek om een bestemming te maken is een specifieke `Content-Type` koptekst vereist, zoals hieronder wordt weergegeven. Het gebruik van een onjuiste `Content-Type` header resulteert in een HTTP Status 415 (Unsupported Media Type)-fout.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

|Eigenschap|Beschrijving||`type` **(Vereist)** |Het type bestemming dat moet worden gecreëerd. De enige toegelaten waarde, &quot;EDGE&quot;, leidt tot een randbestemming.||`dataCenters` **(Vereist)** |Een tekenreeks die de randen opsomt waarnaar de projecties moeten worden gerouteerd. Kan een of meer van de volgende waarden bevatten: &quot;OR1&quot; - Western United States, &quot;VA5&quot; - Eastern United States, &quot;NLD1&quot; - EMEA.||`ttl` **(Vereist)** |Geeft aan dat de projectie vervalt. Geaccepteerd waardebereik: 600 tot 604800. Standaardwaarde: 3600.||`replicationPolicy` **(Vereist)** |Bepaalt het gedrag van de gegevensreplicatie van de hub aan de randen.  Ondersteunde waarden: PROACTIEF, REACTIEF. Standaardwaarde: REACTIEF.|

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe randdoel, inclusief de alleen-lezen, door het systeem gegenereerde unieke id (`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| Eigenschap | Beschrijving |
|---|---|
| `self.href` | Dit pad wordt gebruikt om de bestemming rechtstreeks op te zoeken (GET) en kan ook worden gebruikt om de bestemming bij te werken (PUT) of te verwijderen (DELETE). |
| `id` | De alleen-lezen, door het systeem gegenereerde unieke id voor de bestemming. Deze id wordt gebruikt om rechtstreeks naar de bestemming te verwijzen en wanneer het creëren van projectieconfiguraties. |
| `version` | Deze alleen-lezen waarde toont de huidige versie van het doel. Wanneer een doel wordt bijgewerkt, wordt het versienummer automatisch verhoogd. |

### Een doel weergeven

Als u unieke identiteitskaart van een projectiebestemming kent, kunt u een raadplegingsverzoek uitvoeren om zijn details te bekijken. Dit wordt gedaan door een GET verzoek aan het `/config/destinations` eindpunt en met inbegrip van identiteitskaart van de bestemming in de verzoekweg te doen.

**API-indeling**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DESTINATION_ID}` | De unieke id van de projectiebestemming die u wilt weergeven. |

**Verzoek**

Het volgende verzoek voert een raadpleging (GET) uit om de bestemming voor identiteitskaart te bekijken die in de verzoekweg wordt verstrekt.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het reactieobject geeft de details van de projectiebestemming weer. Het `id` attribuut zou identiteitskaart van de projectiebestemming moeten aanpassen die in het verzoek werd verstrekt.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### Een doel bijwerken

Een bestaande bestemming kan worden bijgewerkt door een PPUT- verzoek aan het `/config/destinations` eindpunt en met inbegrip van identiteitskaart van de bestemming die in de verzoekweg moet worden bijgewerkt te doen. Deze bewerking _herschrijft_ in wezen de bestemming en daarom moeten in de hoofdtekst van het verzoek dezelfde kenmerken worden opgegeven als bij het maken van een nieuwe bestemming.

>[!CAUTION]
>De API-reactie op het updateverzoek is onmiddellijk, maar de wijzigingen in de projecties worden asynchroon toegepast. Met andere woorden, er is een tijdverschil tussen wanneer de update aan de definitie van de bestemming wordt gemaakt en wanneer het wordt toegepast.

**API-indeling**

```
PUT /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DESTINATION_ID}` | De unieke id van de projectiebestemming die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt de bestaande bestemming bij om een tweede plaats (`dataCenters`) te omvatten.

>[!IMPORTANT]
>Voor de PUT-aanvraag is een specifieke `Content-Type` header nodig, zoals hieronder wordt weergegeven. Het gebruik van een onjuiste `Content-Type` header resulteert in een HTTP Status 415 (Unsupported Media Type)-fout.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `currentVersion` | De huidige versie van de bestaande bestemming. De waarde van het `version` attribuut wanneer het uitvoeren van een raadplegingsverzoek voor de bestemming. |

**Antwoord**

De reactie omvat de bijgewerkte details voor de bestemming, met inbegrip van zijn identiteitskaart en nieuwe `version` van de bestemming.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### Een doel verwijderen

Als uw organisatie niet meer een projectiebestemming vereist, kan het worden geschrapt door een verzoek van de VERWIJDERING aan het `/config/destinations` eindpunt en met inbegrip van identiteitskaart van de bestemming te maken die u wenst om in de verzoekweg te schrappen.

>[!CAUTION]
>De API-reactie op het verwijderingsverzoek is onmiddellijk, maar de werkelijke wijzigingen in de gegevens aan de randen worden asynchroon uitgevoerd. Met andere woorden, de profielgegevens worden verwijderd van alle randen (de `dataCenters` opgegeven randen in de projectiebestemming), maar het proces duurt even voordat het is voltooid.

**API-indeling**

```
DELETE /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DESTINATION_ID}` | De unieke id van de projectiebestemming die u wilt verwijderen. |


**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De verwijderaanvraag retourneert HTTP-status 204 (Geen inhoud) en een lege antwoordinstantie. U kunt bevestigen dat de schrapping door een raadplegingsverzoek voor de bestemming door zijn identiteitskaart uit te voeren succesvol was. De zoekopdracht moet HTTP-status 404 (Niet gevonden) retourneren.

## Projectieconfiguraties

Projectieconfiguraties bieden informatie over de gegevens die aan elke rand beschikbaar moeten zijn. In plaats van een schema van het Model van de Gegevens van de Ervaring (XDM) aan de rand te projecteren, verstrekt een projectie slechts specifieke gegevens, of gebieden, van het schema. Uw organisatie kan meer dan één projectieconfiguratie voor elk schema bepalen XDM.

### Alle projectieconfiguraties weergeven

U kunt van alle projectieconfiguraties een lijst maken die voor uw organisatie door een GET verzoek aan het `/config/projections` eindpunt te maken zijn gecreeerd. U kunt facultatieve parameters aan de verzoekweg ook toevoegen om tot projectieconfiguraties voor een bepaald schema toegang te hebben of een individuele projectie door zijn naam te zoeken.

**API-indeling**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parameter | Beschrijving |
|---|---|
| `{SCHEMA_NAME}` | De naam van de schemaklasse verbonden aan de projectieconfiguratie u wilt toegang hebben. |
| `{PROJECTION_NAME}` | De naam van de projectieconfiguratie waartoe u toegang wilt hebben. |

>[!NOTE]
>`schemaName` is vereist wanneer het gebruiken van de `name` parameter, aangezien een naam van de projectieconfiguratie slechts uniek in de context van een schemaklasse is.

**Verzoek**

De volgende aanvraag bevat een lijst met alle projectieconfiguraties die zijn gekoppeld aan de XDM-schemacategorie Persoonlijk profiel (Experience Data Model). Voor meer informatie over XDM en zijn rol binnen Platform, gelieve te beginnen door het [XDM systeemoverzicht](../../xdm/home.md)te lezen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met projectieconfiguraties binnen het `_embedded` hoofdkenmerk, opgenomen in de `projectionConfigs` array. Als er geen projectieconfiguraties zijn gemaakt voor uw organisatie, is de `projectionConfigs` array leeg.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### Een projectieconfiguratie maken

U kunt (POST) een nieuwe projectieconfiguratie tot stand brengen die zal dicteren welke gebieden XDM op de randen ter beschikking worden gesteld.

**API-indeling**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parameter | Beschrijving |
|---|---|
| `{SCHEMA_NAME}` | De naam van de schemaklasse verbonden aan de projectieconfiguratie u wilt toegang hebben. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `selector` | Een tekenreeks die een lijst bevat met eigenschappen in het schema die moeten worden gerepliceerd naar de randen. De beste werkwijzen voor het werken met kiezers zijn beschikbaar in de sectie [Kiezers](#selectors) van dit document. |
| `name` | Een beschrijvende naam voor de nieuwe projectieconfiguratie. |
| `destinationId` | De id voor de randbestemming waarnaar de gegevens worden geprojecteerd. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde projectieconfiguratie terug.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## Kiezers {#selectors}

Een kiezer is een door komma&#39;s gescheiden lijst met XDM-veldnamen. In een projectieconfiguratie geeft de kiezer de eigenschappen aan die in projecties moeten worden opgenomen. De indeling van de `selector` parameterwaarde is losjes gebaseerd op de XPath-syntaxis. Hieronder wordt een overzicht gegeven van de ondersteunde syntaxis, met aanvullende voorbeelden ter referentie.

### Ondersteunde syntaxis

* Gebruik komma&#39;s om meerdere velden te selecteren. Gebruik geen spaties.
* Gebruik puntnotatie om geneste velden te selecteren.
   * Als u bijvoorbeeld een veld met de naam wilt selecteren `field` dat in een veld met de naam `foo`is genest, gebruikt u de kiezer `foo.field`.
* Bij het opnemen van een veld dat subvelden bevat, worden ook alle subvelden standaard geprojecteerd. U kunt de subvelden die worden geretourneerd echter filteren met haakjes `"( )"`.
   * Bijvoorbeeld, `addresses(type,city.country)` keert slechts het adrestype en het land terug waarin de adresstad voor elk `addresses` serieelement wordt gevestigd.
   * Het bovenstaande voorbeeld is gelijk aan `addresses.type,addresses.city.country`.

>[!NOTE]
>Zowel puntnotatie als haakjesnotatie worden ondersteund voor het verwijzen naar subvelden. Het is echter aan te raden puntnotatie te gebruiken, omdat deze beknopter is en een betere illustratie van de veldhiërarchie biedt.

* Elk veld in een kiezer wordt opgegeven ten opzichte van de hoofdmap van de reactie.
   * Als de gegevens een inzameling van middelen zijn, zal de projectie een serie van middelen omvatten.
   * Als de gegevens één bron zijn, bevat de projectie velden die relatief zijn ten opzichte van die bron.
   * Als het veld dat u selecteert een array is (of deel uitmaakt van), bevat de projectie het geselecteerde gedeelte van alle elementen in de array.

### Voorbeelden van de parameter selector

In de volgende voorbeelden worden voorbeeldparameters weergegeven, gevolgd door de gestructureerde waarden die ze vertegenwoordigen. `selector`

**person.lastName**

Retourneert het `lastName` subveld van het `person` object in de gevraagde bron.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**adressen**

Retourneert alle elementen in de `addresses` array, inclusief alle velden in elk element, maar geen andere velden.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName,adressen**

Retourneert het `person.lastName` veld en alle elementen in de `addresses` array.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**adressen.city**

Retourneert alleen het stadsveld voor alle elementen in de array adressen.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>Wanneer een genest veld wordt geretourneerd, worden in de projectie de bovenliggende objecten opgenomen. De bovenliggende velden bevatten geen andere onderliggende velden, tenzij deze ook expliciet zijn geselecteerd.

**adressen (type,plaats)**

Retourneert alleen de waarden van de waarden `type` en `city` velden voor elk element in de `addresses` array. Alle andere subvelden in elk `addresses` element worden uitgefilterd.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## Volgende stappen

Deze gids heeft u de stappen getoond betrokken om randprojecties en bestemmingen te vormen, met inbegrip van hoe te om de `selector` parameter behoorlijk te formatteren. U kunt nu nieuwe randbestemmingen en prognoses maken die specifiek zijn voor de behoeften van uw organisatie. Zie de handleiding voor ontwikkelaars van de [realtime-API voor klantprofielen voor meer informatie over extra acties die beschikbaar zijn via de profiel-API](getting-started.md).