---
keywords: Experience Platform;home;populaire onderwerpen;streaming opname;inname;record gegevens;stream recordgegevens;
solution: Experience Platform
title: Gegevens stroomrecord met API's voor streaming-insluiting
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 0%

---


# Gegevens voor stroomrecord streamen met API&#39;s voor streaming insluiting

Deze zelfstudie helpt u bij het gebruik van streaming opname-API&#39;s, onderdeel van de Adobe Experience Platform [!DNL Data Ingestion Service] API&#39;s.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van verschillende Adobe Experience Platform-services. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert ervaringsgegevens.
   - [Handleiding voor ontwikkelaars van het schema Register](../../xdm/api/getting-started.md): Een uitgebreide gids die elk van de beschikbare eindpunten van [!DNL Schema Registry] API en hoe te om tot hen te richten. Hieronder valt ook het weten van uw `{TENANT_ID}`, die in vraag door dit leerprogramma verschijnt, evenals het weten hoe te schema&#39;s tot stand te brengen, die in het creëren van een dataset voor opname wordt gebruikt.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan het stromen ingestie APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Stel een schema samen dat van wordt gebaseerd [!DNL XDM Individual Profile] class

Om een dataset tot stand te brengen, zult u eerst een nieuw schema moeten creëren dat uitvoert [!DNL XDM Individual Profile] klasse. Lees voor meer informatie over het maken van schema&#39;s de [Handleiding voor ontwikkelaars van de API voor schemaregister](../../xdm/api/getting-started.md).

**API-indeling**

```http
POST /schemaregistry/tenant/schemas
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `title` | De naam die u voor het schema wilt gebruiken. Deze naam moet uniek zijn. |
| `description` | Een betekenisvolle beschrijving van het schema dat u maakt. |
| `meta:immutableTags` | In dit voorbeeld wordt `union` -tag wordt gebruikt om uw gegevens door te zetten in [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van uw onlangs gecreeerd schema terug.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{TENANT_ID}` | Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. Voor meer informatie over de huurder-id leest u de [schemaregistergids](../../xdm/api/getting-started.md#know-your-tenant-id). |

Neem nota van het `$id` en de `version` attributen, aangezien allebei van deze zullen worden gebruikt wanneer het creëren van uw dataset.

## Een primaire identiteitsdescriptor instellen voor het schema

Voeg vervolgens een [identiteitsbeschrijving](../../xdm/api/descriptors.md) naar het hierboven gemaakte schema, waarbij het werkadreskenmerk als primaire id wordt gebruikt. Dit leidt tot twee wijzigingen:

1. Het werk-e-mailadres wordt een verplicht veld. Dit betekent dat berichten die zonder dit veld worden verzonden, niet worden gevalideerd en niet worden ingevoerd.

2. [!DNL Real-time Customer Profile] gebruikt het werk-e-mailadres als id om meer informatie over die persoon te koppelen.

### Verzoek

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | De `$id` die u eerder hebt ontvangen toen u het schema samenstelde. Het moet er ongeveer als volgt uitzien: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Naamruimtecodes id**
>
> Controleer of de codes geldig zijn. In het bovenstaande voorbeeld wordt &quot;email&quot; gebruikt, een naamruimte met een standaardidentiteit. Andere veelgebruikte standaardnaamruimten vindt u in het dialoogvenster [Veelgestelde vragen over identiteitsservice](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Als u een aangepaste naamruimte wilt maken, voert u de stappen uit die in het dialoogvenster [Overzicht van naamruimte in identiteit](../../identity-service/home.md).

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met informatie over de nieuwe primaire identiteitsdescriptor voor het schema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## Een gegevensset maken voor recordgegevens

Zodra u uw schema hebt gecreeerd, zult u een dataset moeten tot stand brengen om verslaggegevens in te voeren.

>[!NOTE]
>
>Deze gegevensset wordt ingeschakeld voor **[!DNL Real-time Customer Profile]** en **[!DNL Identity Service]**.

**API-indeling**

```http
POST /catalog/dataSets
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Antwoord**

Een succesvolle reactie keert HTTP status 201 en een serie terug die identiteitskaart van de pas gecreëerde dataset in het formaat bevatten `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Een streamingverbinding maken

Na het creëren van uw schema en dataset, kunt u een het stromen verbinding tot stand brengen

Voor meer informatie over het maken van een streamingverbinding leest u de [een zelfstudie over streamingverbindingen maken](./create-streaming-connection.md).

## Recordgegevens opnemen in de streamingverbinding {#ingest-data}

Met de dataset en het stromen verbinding op zijn plaats, kunt u XDM-Geformatteerde JSON- verslagen opnemen om verslaggegevens in in te nemen [!DNL Platform].

**API-indeling**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `inletId` De waarde van de eerder gemaakte streamingverbinding. |
| `syncValidation` | Een optionele query-parameter voor ontwikkelingsdoeleinden. Indien ingesteld op `true`, kan deze worden gebruikt voor directe feedback om te bepalen of de aanvraag is verzonden. Deze waarde is standaard ingesteld op `false`. Let op: als u deze queryparameter instelt op `true` dat het tarief van het verzoek beperkt zal zijn tot 60 keer per minuut per minuut `CONNECTION_ID`. |

**Verzoek**

U kunt recordgegevens met of zonder de bronnaam in een streamingverbinding invoegen.

In de onderstaande voorbeeldaanvraag wordt een record met een ontbrekende bronnaam aan het Platform toegevoegd. Als de bronnaam van een record ontbreekt, wordt de bron-id toegevoegd uit de definitie van de streamingverbinding.

>[!NOTE]
>
>De volgende API-aanroep doet dit **niet** vereist alle verificatieheaders.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

Als u een bronnaam wilt omvatten, toont het volgende voorbeeld hoe u het zou omvatten.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 200 met details van de zojuist gestreamde [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de eerder gemaakte streamingverbinding. |
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan Adobe de levenscyclus van deze record traceren via verschillende systemen en met foutopsporing. |
| `receivedTimeMs` | Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |
| `syncValidation.status` | Omdat de parameter query `syncValidation=true` is toegevoegd, wordt deze waarde weergegeven. Als de validatie is gelukt, wordt de status `pass`. |

## De nieuw opgenomen recordgegevens ophalen

Om de eerder opgenomen verslagen te bevestigen, kunt u gebruiken [[!DNL Profile Access API]](../../profile/api/entities.md) om de recordgegevens op te halen.

>[!NOTE]
>
>Als de beleid-id voor samenvoegen niet is gedefinieerd en de instelling `schema.name` of `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] wordt opgehaald **alles** verwante identiteiten.

**API-indeling**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `schema.name` | **Vereist.** De naam van het schema dat u opent. |
| `entityId` | De id van de entiteit. Indien opgegeven, moet u ook de naamruimte voor entiteiten opgeven. |
| `entityIdNS` | De naamruimte van de id die u probeert op te halen. |

**Verzoek**

U kunt de eerder opgenomen recordgegevens met de volgende GET-aanvraag bekijken.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 met details over de aangevraagde entiteiten. Zoals u kunt zien, is dit dezelfde record die eerder met succes is opgenomen.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## Volgende stappen

Door dit document te lezen, begrijpt u nu hoe u recordgegevens kunt invoeren in [!DNL Platform] via streamingverbindingen. U kunt proberen meer vraag met verschillende waarden te maken en de bijgewerkte waarden terug te winnen. Bovendien kunt u beginnen uw ingesloten gegevens te controleren door [!DNL Platform] UI. Lees voor meer informatie de [controle gegevensinvoer](../quality/monitor-data-ingestion.md) hulplijn.

Lees voor meer informatie over streamingopname in het algemeen de [overzicht van streaming opname](../streaming-ingestion/overview.md).
