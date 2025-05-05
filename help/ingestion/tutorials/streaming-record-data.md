---
keywords: Experience Platform;home;populaire onderwerpen;streaming opname;inname;record gegevens;stream recordgegevens;
solution: Experience Platform
title: Gegevens stroomrecord met API's voor streaming-insluiting
type: Tutorial
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---


# Gegevens voor stroomrecord streamen met API&#39;s voor streaming insluiting

Deze zelfstudie helpt u bij het gebruik van streaming opname-API&#39;s, onderdeel van de Adobe Experience Platform [!DNL Data Ingestion Service] API&#39;s.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van verschillende Adobe Experience Platform-services. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] ervaringsgegevens ordent.
   - [ de ontwikkelaarsgids van de Registratie van het Schema ](../../xdm/api/getting-started.md): Een uitvoerige gids die elk van de beschikbare eindpunten van [!DNL Schema Registry] API behandelt en hoe te om vraag aan hen te maken. Dit omvat het kennen van uw `{TENANT_ID}`, die in vraag door dit leerprogramma verschijnt, evenals het weten hoe te om schema&#39;s tot stand te brengen, die in het creëren van een dataset voor opname wordt gebruikt.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, consumentenprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../landing/api-guide.md).

## Een schema samenstellen dat is gebaseerd op de klasse [!DNL XDM Individual Profile]

Om een dataset tot stand te brengen, zult u eerst een nieuw schema moeten creëren dat de [!DNL XDM Individual Profile] klasse uitvoert. Voor meer informatie over hoe te om schema&#39;s tot stand te brengen, te lezen gelieve de [ gids van de ontwikkelaar van de Registratie API van het Schema ](../../xdm/api/getting-started.md).

**API formaat**

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
| `meta:immutableTags` | In dit voorbeeld wordt de tag `union` gebruikt om uw gegevens in [[!DNL Real-Time Customer Profile]](../../profile/home.md) te behouden. |

**Reactie**

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
| `{TENANT_ID}` | Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw organisatie bevinden. Voor meer informatie over identiteitskaart van de Aannemer, gelieve de [ gids van de schemaregistratie ](../../xdm/api/getting-started.md#know-your-tenant-id) te lezen. |

Let op de attributen `$id` en `version` , aangezien beide worden gebruikt bij het maken van uw dataset.

## Een primaire identiteitsdescriptor instellen voor het schema

Daarna, voeg een [ identiteitsbeschrijver ](../../xdm/api/descriptors.md) aan het hierboven gecreeerd schema toe, gebruikend het werk e-mailadresattribuut als primaire herkenningsteken. Dit leidt tot twee wijzigingen:

1. Het werk-e-mailadres wordt een verplicht veld. Dit betekent dat berichten die zonder dit veld worden verzonden, niet worden gevalideerd en niet worden ingevoerd.

2. [!DNL Real-Time Customer Profile] gebruikt het werk-e-mailadres als id om meer informatie over die persoon te koppelen.

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
>&#x200B; **Codes van Namespace van de Identiteit**
>
> Controleer of de codes geldig zijn. In het bovenstaande voorbeeld wordt &quot;email&quot; gebruikt, een naamruimte met een standaardidentiteit. Andere algemeen gebruikte standaardidentiteitsnamespaces kunnen binnen de [ Veelgestelde vragen van de Dienst van de Identiteit ](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform) worden gevonden.
>
> Als u een douane zou willen tot stand brengen namespace, volg de stappen die in het [ overzicht van identiteitsnaamruimte ](../../identity-service/home.md) worden geschetst.

**Reactie**

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
>Deze gegevensset wordt ingeschakeld voor **[!DNL Real-Time Customer Profile]** en **[!DNL Identity Service]** .

**API formaat**

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

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 en een array met de id van de nieuwe dataset in de indeling `@/dataSets/{DATASET_ID}` .

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Een streamingverbinding maken

Na het creëren van uw schema en dataset, kunt u een het stromen verbinding tot stand brengen

Voor meer informatie bij het creëren van een het stromen verbinding, te lezen gelieve [ een het stromen verbindingsleerprogramma ](./create-streaming-connection.md) creëren.

## Recordgegevens opnemen in de streamingverbinding {#ingest-data}

Met de gegevensset en streamingverbinding op zijn plaats kunt u JSON-records met XDM-indeling invoeren om recordgegevens in [!DNL Experience Platform] in te voeren.

**API formaat**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `inletId` -waarde van de eerder gemaakte streamingverbinding. |
| `syncValidation` | Een optionele query-parameter voor ontwikkelingsdoeleinden. Indien ingesteld op `true` , kan dit worden gebruikt voor directe feedback om te bepalen of de aanvraag is verzonden. Deze waarde wordt standaard ingesteld op `false` . Houd er rekening mee dat als u deze queryparameter instelt op `true` , de snelheid van de aanvraag beperkt blijft tot 60 keer per minuut per `CONNECTION_ID` . |

**Verzoek**

U kunt recordgegevens met of zonder de bronnaam in een streamingverbinding invoegen.

In de onderstaande voorbeeldaanvraag wordt een record met een ontbrekende bronnaam opgenomen in Experience Platform. Als de bronnaam van een record ontbreekt, wordt de bron-id toegevoegd uit de definitie van de streamingverbinding.

>[!NOTE]
>
>De volgende API vraag **&#x200B;**&#x200B;vereist geen authentificatiekopballen.

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
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
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

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met details van het net gestreamde bestand [!DNL Profile] .

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
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan Adobe de levenscyclus van deze record volgen via verschillende systemen en met foutopsporing. |
| `receivedTimeMs` | Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |
| `syncValidation.status` | Aangezien de queryparameter `syncValidation=true` is toegevoegd, wordt deze waarde weergegeven. Als de validatie is gelukt, is de status `pass` . |

## De nieuw opgenomen recordgegevens ophalen

Als u de eerder opgenomen records wilt valideren, gebruikt u de [[!DNL Profile Access API]](../../profile/api/entities.md) om de recordgegevens op te halen.

>[!NOTE]
>
>Als identiteitskaart van het fusiebeleid niet wordt bepaald en `schema.name` of `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] zal **alle** verwante identiteiten halen.

**API formaat**

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

U kunt de eerder opgenomen recordgegevens bekijken met het volgende GET-verzoek.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

Door dit document te lezen, begrijpt u nu hoe u recordgegevens via streamingverbindingen in [!DNL Experience Platform] kunt opnemen. U kunt proberen meer vraag met verschillende waarden te maken en de bijgewerkte waarden terug te winnen. Bovendien kunt u uw ingesloten gegevens controleren via de gebruikersinterface van [!DNL Experience Platform] . Voor meer informatie, te lezen gelieve de [ controle gegevensopname ](../quality/monitor-data-ingestion.md) gids.

Voor meer informatie over het stromen ingestie in het algemeen, te lezen gelieve het [ stromen ingestitieoverzicht ](../streaming-ingestion/overview.md).
