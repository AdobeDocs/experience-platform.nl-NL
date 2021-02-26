---
keywords: Experience Platform;thuis;populaire onderwerpen;het stromen ingestie;ingestie;tijdreeksgegevens;stroom tijdreeksgegevens;
solution: Experience Platform
title: Gegevens uit tijdreeks streamen met API's voor streaming insluiting
topic: zelfstudie
type: Zelfstudie
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
translation-type: tm+mt
source-git-commit: d3531248f8a7116b66f9a7ca00e0eadbc3d9df3d
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 0%

---


# Gegevens uit de tijdreeks streamen met behulp van Streaming Ingestie-API&#39;s

Deze zelfstudie helpt u bij het gebruik van streaming opname-API&#39;s, onderdeel van de Adobe Experience Platform [!DNL Data Ingestion Service] API&#39;s.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van verschillende Adobe Experience Platform-services. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader voor het  [!DNL Platform] organiseren van ervaringsgegevens.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Handleiding](../../xdm/api/getting-started.md) voor ontwikkelaars van het schemaregister: Een uitvoerige gids die elk van de beschikbare eindpunten van  [!DNL Schema Registry] API behandelt en hoe te om vraag aan hen te maken. Dit omvat het kennen van uw `{TENANT_ID}`, die in vraag door dit leerprogramma verschijnt, evenals het weten hoe te schema&#39;s tot stand te brengen, die in het creëren van een dataset voor opname wordt gebruikt.

Bovendien is voor deze zelfstudie vereist dat u al een streamingverbinding hebt gemaakt. Lees voor meer informatie over het maken van een streamingverbinding de zelfstudie [Een streamingverbinding maken](./create-streaming-connection.md).

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan het stromen ingestie APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Stel een schema samen dat van de klasse XDM ExperienceEvent wordt gebaseerd

Om een dataset tot stand te brengen, zult u eerst een nieuw schema moeten creëren dat de [!DNL XDM ExperienceEvent] klasse uitvoert. Voor meer informatie over hoe te om schema&#39;s tot stand te brengen, te lezen gelieve [de ontwikkelaarsgids ](../../xdm/api/getting-started.md) van de Registratie van het schema API.

**API-indeling**

```http
POST /schemaregistry/tenant/schemas
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
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
| `meta:immutableTags` | In dit voorbeeld wordt de tag `union` gebruikt om uw gegevens te behouden in [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van uw onlangs gecreeerd schema terug.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "{SCHEMA_VERSION}",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{TENANT_ID}` | Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. Voor meer informatie over identiteitskaart van de Aannemer, te lezen gelieve [schemaregistratiegids](../../xdm/api/getting-started.md#know-your-tenant-id). |

Let op de `$id` en de `version` attributen, aangezien allebei van deze zullen worden gebruikt wanneer het creëren van uw dataset.

## Een primaire identiteitsdescriptor instellen voor het schema

Vervolgens voegt u een [identiteitsdescriptor](../../xdm/api/descriptors.md) toe aan het hierboven gemaakte schema en gebruikt u het werkadreskenmerk als primaire id. Dit leidt tot twee wijzigingen:

1. Het werk-e-mailadres wordt een verplicht veld. Dit betekent dat berichten die zonder dit veld worden verzonden, niet worden gevalideerd en niet worden ingevoerd.

2. [!DNL Real-time Customer Profile] gebruikt het werk-e-mailadres als id om meer informatie over die persoon samen te voegen.

### Verzoek

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | De `$id` die u eerder ontving toen u het schema samenstelde. Het moet er ongeveer als volgt uitzien: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Identiteitsnaamruimtecodes**
>
> Controleer of de codes geldig zijn. In het bovenstaande voorbeeld wordt &quot;email&quot; gebruikt, een naamruimte met een standaardidentiteit. Andere veelgebruikte standaardnaamruimten vindt u in [Veelgestelde vragen over identiteitsservice](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Als u een aangepaste naamruimte wilt maken, volgt u de stappen die worden beschreven in het naamruimteoverzicht [identity](../../identity-service/home.md).

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 met informatie over de nieuw gemaakte primaire naamruimte voor het schema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Een gegevensset maken voor de gegevens van tijdreeksen

Zodra u uw schema hebt gecreeerd, zult u een dataset moeten tot stand brengen om verslaggegevens in te voeren.

>[!NOTE]
>
>Deze dataset zal voor **[!DNL Real-time Customer Profile]** en **[!DNL Identity]** worden toegelaten door de aangewezen markeringen te plaatsen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 en een array met de id van de nieuwe dataset in de notatie `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## Gegevens uit tijdreeksen opnemen in de streamingverbinding

Met de dataset en het stromen verbinding op zijn plaats, kunt u XDM-Geformatteerde JSON verslagen opnemen om tijdreeksgegevens binnen [!DNL Platform] in te voeren.

**API-indeling**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id`-waarde van de nieuwe streamingverbinding. |
| `synchronousValidation` | Een optionele query-parameter voor ontwikkelingsdoeleinden. Als ingesteld op `true`, kan deze worden gebruikt voor directe feedback om te bepalen of het verzoek is verzonden. Deze waarde wordt standaard ingesteld op `false`. |

**Verzoek**

U kunt tijdreeksgegevens met of zonder de bronnaam in een streamingverbinding invoegen.

In de onderstaande voorbeeldaanvraag worden tijdreeksgegevens met een ontbrekende bronnaam aan het Platform toegevoegd. Als de bronnaam ontbreekt in de gegevens, wordt de bron-id toegevoegd uit de definitie van de streamingverbinding.

>[!IMPORTANT]
>
>U zult uw eigen `xdmEntity._id` en `xdmEntity.timestamp` moeten produceren. Een goede manier om een identiteitskaart te produceren is de functie UUID in de Prep van Gegevens te gebruiken. Meer informatie over de functie UUID vindt u in de [handleiding voor functies van Data Prep](../../data-prep/functions.md). Het `xdmEntity._id` attribuut vertegenwoordigt een uniek herkenningsteken voor het verslag zelf, **not** unieke identiteitskaart van de persoon of het apparaat waarvan verslag het is. De persoon of apparaat-id is specifiek voor alle kenmerken die zijn toegewezen als een persoon of apparaat-id van het schema.
>
>Zowel `xdmEntity._id` als `xdmEntity.timestamp` zijn de enige vereiste gebieden voor tijdreeksgegevens. Bovendien vereist de volgende API-aanroep **not** geen verificatiekoppen.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
            }
        },
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
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
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met details van de zojuist gestreamde [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de eerder gemaakte streamingverbinding. |
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan Adobe de levenscyclus van deze record traceren via verschillende systemen en met foutopsporing. |
| `receivedTimeMs`: Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |
| `synchronousValidation.status` | Aangezien de vraagparameter `synchronousValidation=true` werd toegevoegd, zal deze waarde verschijnen. Als de validatie is voltooid, is de status `pass`. |

## De nieuw ingevoerde tijdreeksgegevens ophalen

Om de eerder opgenomen verslagen te bevestigen, kunt u [[!DNL Profile Access API]](../../profile/api/entities.md) gebruiken om de gegevens van de tijdreeksen terug te winnen. Dit kan worden gedaan gebruikend een verzoek van de GET aan het `/access/entities` eindpunt en het gebruiken van facultatieve vraagparameters. U kunt meerdere parameters gebruiken, gescheiden door ampersands (&amp;).&quot;

>[!NOTE]
>
>Als de id van het samenvoegbeleid niet is gedefinieerd en `schema.name` of `relatedSchema.name` `_xdm.context.profile` is, [!DNL Profile Access] haalt **alle** gerelateerde identiteiten op.

**API-indeling**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `schema.name` | **Vereist.** De naam van het schema dat u opent. |
| `relatedSchema.name` | **Vereist.** Aangezien u tot een toegang hebt  `_xdm.context.experienceevent`, specificeert deze waarde het schema voor de profielentiteit die de gebeurtenissen van de tijdreeks met betrekking hebben. |
| `relatedEntityId` | De id van de verbonden entiteit. Indien opgegeven, moet u ook de naamruimte voor entiteiten opgeven. |
| `relatedEntityIdNS` | De naamruimte van de id die u probeert op te halen. |

**Verzoek**

```shell
curl -X GET \
  https://platform-stage.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 met details over de aangevraagde entiteiten. Zoals u kunt zien, is dit de zelfde tijdreeksgegevens die eerder werden opgenomen.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Volgende stappen

Door dit document te lezen, begrijpt u nu hoe u recordgegevens via streamingverbindingen in [!DNL Platform] kunt opnemen. U kunt proberen meer vraag met verschillende waarden te maken en de bijgewerkte waarden terug te winnen. Daarnaast kunt u uw ingesloten gegevens controleren via [!DNL Platform] UI. Lees voor meer informatie de [handleiding voor het controleren van gegevensinvoer](../quality/monitor-data-ingestion.md).

Lees voor meer informatie over streaming opname in het algemeen het [overzicht van streaming opname](../streaming-ingestion/overview.md).
