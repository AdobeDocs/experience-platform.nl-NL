---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Edge Projection API-eindpunten
topic-legacy: guide
type: Documentation
description: Met Adobe Experience Platform kunt u in real-time zorgen voor een gecoördineerde, consistente en gepersonaliseerde ervaring voor uw klanten op meerdere kanalen, door de juiste gegevens direct beschikbaar te maken en voortdurend bij te werken naarmate de wijzigingen zich voordoen. Dit wordt gedaan door het gebruik van randen, een geografisch geplaatste server die gegevens opslaat en het gemakkelijk toegankelijk voor toepassingen maakt.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 0%

---

# Edge-projectieconfiguraties en eindpunten van doelen

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in echt te drijven - tijd, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Adobe Experience Platform biedt realtime toegang tot gegevens via het gebruik van zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. Bijvoorbeeld, gebruiken de toepassingen van de Adobe zoals Adobe Target en Adobe Campaign randen om gepersonaliseerde klantenervaringen in echt te verstrekken - tijd. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Deze handleiding bevat gedetailleerde instructies voor het gebruik van de [!DNL Real-time Customer Profile] API om met randprojecties, met inbegrip van bestemmingen en configuraties te werken.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Controleer voordat je doorgaat de [gids Aan de slag](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

>[!NOTE]
>
>De verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een `Content-Type` header. Meer dan één `Content-Type` wordt gebruikt in dit document. Gelieve te letten speciaal op de kopballen in de steekproefvraag om ervoor te zorgen u de correcte gebruikt `Content-Type` voor elk verzoek.

## Projectiebestemmingen

Een projectie kan naar een of meer randen worden gerouteerd door de locaties op te geven waar gegevens moeten worden verzonden. Elke projectiebestemming die wordt gecreeerd heeft een unieke identiteitskaart die dan wordt gebruikt om de projectieconfiguratie tot stand te brengen.

### Alle doelen weergeven

U kunt een lijst maken van de randbestemmingen die reeds voor uw organisatie door een verzoek van de GET aan te richten `/config/destinations` eindpunt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie omvat een `projectionDestinations` array met de details voor elk doel weergegeven als een afzonderlijk object binnen de array. Als er geen projecties zijn geconfigureerd, wordt de `projectionDestinations` array retourneert leeg.

>[!NOTE]
>
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
| `_links.self.href` | Op het hoogste niveau, past de weg aan die wordt gebruikt om het verzoek van de GET te doen. Binnen elk individueel bestemmingsvoorwerp, kan dit weg in een verzoek van de GET worden gebruikt om de details van een specifieke bestemming direct te zoeken. |
| `id` | Binnen elk doelobject wordt het `"id"` toont read-only, systeem-geproduceerde unieke identiteitskaart voor de bestemming. Deze ID wordt gebruikt wanneer het van verwijzingen voorzien van een specifieke bestemming en wanneer het creëren van projectieconfiguraties. |

Voor meer informatie over de kenmerken van een individuele bestemming raadpleegt u de sectie over [een doel maken](#create-a-destination) dat volgt .

### Een doel maken {#create-a-destination}

Als de bestemming u vereist niet reeds bestaat, kunt u een nieuwe projectiebestemming tot stand brengen door een verzoek van de POST aan het `/config/destinations` eindpunt.

**API-indeling**

```http
POST /config/destinations
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe randbestemming gemaakt.

>[!NOTE]
>
>Het verzoek van de POST om een bestemming tot stand te brengen vereist een specifieke `Content-Type` header, zoals hieronder weergegeven. Onjuist gebruiken `Content-Type` resulteert in een HTTP Status 415 (Unsupported Media Type) fout.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Eigenschap | Beschrijving |
|---|---|
| `type` **(Vereist)** | Het type doel dat moet worden gemaakt. De enige toegelaten waarde, &quot;EDGE&quot;, leidt tot een randbestemming. |
| `dataCenters` **(Vereist)** | Een tekenreeks-array die de randen opsomt waarnaar projecties moeten worden gerouteerd. Kan een of meer van de volgende waarden bevatten: &quot;OR1&quot; - Western United States, &quot;VA5&quot; - Eastern United States, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Vereist)** | Geeft aan dat de projectie vervalt. Geaccepteerd waardebereik: 600 tot 604800. Standaardwaarde: 3600. |
| `replicationPolicy` **(Vereist)** | Bepaalt het gedrag van de gegevensreplicatie van de hub aan de randen.  Ondersteunde waarden: PROACTIEF, REACTIEF. Standaardwaarde: REACTIEF. |

**Antwoord**

Een succesvol antwoord retourneert de details van het nieuwe randdoel, inclusief de alleen-lezen, door het systeem gegenereerde unieke id (`id`).

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
| `self.href` | Deze weg wordt gebruikt aan raadpleging (GET) de bestemming direct en kan ook voor het bijwerken (PUT) of het schrappen (DELETE) van de bestemming worden gebruikt. |
| `id` | De alleen-lezen, door het systeem gegenereerde unieke id voor de bestemming. Deze id wordt gebruikt om rechtstreeks naar de bestemming te verwijzen en wanneer het creëren van projectieconfiguraties. |
| `version` | Deze alleen-lezen waarde toont de huidige versie van het doel. Wanneer een doel wordt bijgewerkt, wordt het versienummer automatisch verhoogd. |

### Een doel weergeven

Als u unieke identiteitskaart van een projectiebestemming kent, kunt u een raadplegingsverzoek uitvoeren om zijn details te bekijken. Dit gebeurt door een verzoek van de GET aan `/config/destinations` eindpunt en met inbegrip van identiteitskaart van de bestemming in de verzoekweg.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het reactieobject geeft de details van de projectiebestemming weer. De `id` attribuut zou identiteitskaart van de projectiebestemming moeten aanpassen die in het verzoek werd verstrekt.

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

Een bestaande bestemming kan worden bijgewerkt door een verzoek van de PUT aan `/config/destinations` eindpunt en met inbegrip van identiteitskaart van de bestemming die in de verzoekweg moet worden bijgewerkt. Deze verrichting herschrijft hoofdzakelijk de bestemming, daarom moeten de zelfde attributen in het lichaam van het verzoek worden verstrekt zoals wanneer het creëren van een nieuwe bestemming wordt verstrekt.

>[!CAUTION]
>
>De API-reactie op het updateverzoek is onmiddellijk, maar de wijzigingen in de projecties worden asynchroon toegepast. Met andere woorden, er is een tijdverschil tussen wanneer de update aan de definitie van de bestemming wordt gemaakt en wanneer het wordt toegepast.

**API-indeling**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DESTINATION_ID}` | De unieke id van de projectiebestemming die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt de bestaande bestemming bij om een tweede plaats (`dataCenters`).

>[!IMPORTANT]
>
>Het verzoek van de PUT vereist een specifieke `Content-Type` header, zoals hieronder weergegeven. Onjuist gebruiken `Content-Type` resulteert in een HTTP Status 415 (Unsupported Media Type) fout.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `currentVersion` | De huidige versie van de bestaande bestemming. De waarde van de `version` attribuut wanneer het uitvoeren van een raadplegingsverzoek voor de bestemming. |

**Antwoord**

De reactie bevat de bijgewerkte gegevens voor de bestemming, inclusief de id en de nieuwe `version` van de bestemming.

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

Als uw organisatie niet langer een projectiebestemming vereist, kan het worden geschrapt door een verzoek van de DELETE aan te richten `/config/destinations` eindpunt en met inbegrip van identiteitskaart van de bestemming die u wenst om in de verzoekweg te schrappen.

>[!CAUTION]
>
>De API-reactie op het verwijderingsverzoek is onmiddellijk, maar de werkelijke wijzigingen in de gegevens aan de randen worden asynchroon uitgevoerd. Met andere woorden, de profielgegevens worden uit alle randen verwijderd (de `dataCenters` opgegeven in de projectiebestemming), maar het proces duurt langer.

**API-indeling**

```http
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De verwijderaanvraag retourneert HTTP-status 204 (Geen inhoud) en een lege antwoordinstantie. U kunt bevestigen dat de schrapping door een raadplegingsverzoek voor de bestemming door zijn identiteitskaart uit te voeren succesvol was. De zoekopdracht moet HTTP-status 404 (Niet gevonden) retourneren.

## Projectieconfiguraties

Projectieconfiguraties bieden informatie over de gegevens die aan elke rand beschikbaar moeten zijn. In plaats van een complete [!DNL Experience Data Model] (XDM) schema aan de rand, verstrekt een projectie slechts specifieke gegevens, of gebieden, van het schema. Uw organisatie kan meer dan één projectieconfiguratie voor elk schema bepalen XDM.

### Alle projectieconfiguraties weergeven

U kunt alle projectieconfiguraties die voor uw organisatie zijn gemaakt, weergeven door een GET-aanvraag in te dienen bij de `/config/projections` eindpunt. U kunt facultatieve parameters aan de verzoekweg ook toevoegen om tot projectieconfiguraties voor een bepaald schema toegang te hebben of een individuele projectie door zijn naam te zoeken.

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
>
>`schemaName` is vereist wanneer u de `name` parameter, aangezien een naam van de projectieconfiguratie slechts uniek in de context van een schemaklasse is.

**Verzoek**

Het volgende verzoek maakt een lijst van alle projectieconfiguraties verbonden aan de [!DNL Experience Data Model] schema-klasse, [!DNL XDM Individual Profile]. Voor meer informatie over XDM en zijn rol binnen [!DNL Platform], te beginnen met het lezen van de [XDM System, overzicht](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van projectieconfiguraties binnen de wortel terug `_embedded` kenmerk, opgenomen in de `projectionConfigs` array. Als er geen projectieconfiguraties zijn gemaakt voor uw organisatie, `projectionConfigs` array is leeg.

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

>[!NOTE]
>
>Het verzoek van de POST om een configuratie tot stand te brengen vereist een specifieke `Content-Type` header, zoals hieronder weergegeven. Onjuist gebruiken `Content-Type` resulteert in een HTTP Status 415 (Unsupported Media Type) fout.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `selector` | Een tekenreeks die een lijst bevat met eigenschappen in het schema die moeten worden gerepliceerd naar de randen. De beste werkwijzen voor het werken met kiezers zijn beschikbaar in het dialoogvenster [Kiezers](#selectors) van dit document. |
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

Een kiezer is een door komma&#39;s gescheiden lijst met XDM-veldnamen. In een projectieconfiguratie geeft de kiezer de eigenschappen aan die in projecties moeten worden opgenomen. Het formaat van de `selector` De parameterwaarde wordt losjes gebaseerd op de syntaxis van XPath. Hieronder wordt een overzicht gegeven van de ondersteunde syntaxis, met aanvullende voorbeelden ter referentie.

### Ondersteunde syntaxis

* Gebruik komma&#39;s om meerdere velden te selecteren. Gebruik geen spaties.
* Gebruik puntnotatie om geneste velden te selecteren.
   * Als u bijvoorbeeld een veld met de naam `field` dat genest is in een veld met de naam `foo`, gebruik de kiezer `foo.field`.
* Bij het opnemen van een veld dat subvelden bevat, worden ook alle subvelden standaard geprojecteerd. U kunt echter wel de subvelden filteren die worden geretourneerd door haakjes te gebruiken `"( )"`.
   * Bijvoorbeeld: `addresses(type,city.country)` retourneert alleen het adrestype en het land waarin de adresstad zich voor elke instantie bevindt `addresses` arrayelement.
   * Het bovenstaande voorbeeld is gelijk aan `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Zowel puntnotatie als haakjesnotatie worden ondersteund voor het verwijzen naar subvelden. Het is echter aan te raden puntnotatie te gebruiken, omdat deze beknopter is en een betere illustratie van de veldhiërarchie biedt.

* Elk veld in een kiezer wordt opgegeven ten opzichte van de hoofdmap van de reactie.
   * Als de gegevens een inzameling van middelen zijn, zal de projectie een serie van middelen omvatten.
   * Als de gegevens één bron zijn, bevat de projectie velden die relatief zijn ten opzichte van die bron.
   * Als het veld dat u selecteert een array is (of deel uitmaakt van), bevat de projectie het geselecteerde gedeelte van alle elementen in de array.

### Voorbeelden van de parameter selector

In het volgende voorbeeld ziet u een voorbeeld `selector` parameters, gevolgd door de gestructureerde waarden die ze vertegenwoordigen.

**person.lastName**

Hiermee wordt het `lastName` subveld van de `person` -object in de gevraagde bron.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**adressen**

Hiermee worden alle elementen in het dialoogvenster geretourneerd `addresses` array, met inbegrip van alle gebieden in elk element, maar geen andere gebieden.

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

Hiermee wordt het `person.lastName` en alle elementen in het `addresses` array.

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
>
>Wanneer een genest veld wordt geretourneerd, worden in de projectie de bovenliggende objecten opgenomen. De bovenliggende velden bevatten geen andere onderliggende velden, tenzij deze ook expliciet zijn geselecteerd.

**adressen (type,plaats)**

Retourneert alleen de waarden van het dialoogvenster `type` en `city` velden voor elk element in het dialoogvenster `addresses` array. Alle andere subvelden in elk subveld `addresses` element wordt uitgefilterd.

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

Deze gids heeft u de stappen getoond betrokken om prognoses en bestemmingen te vormen, met inbegrip van hoe te behoorlijk formatteren `selector` parameter. U kunt nieuwe projectiebestemmingen en configuraties nu tot stand brengen specifiek voor de behoeften van uw organisatie.
