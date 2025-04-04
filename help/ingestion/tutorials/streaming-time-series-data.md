---
keywords: Experience Platform;home;populaire onderwerpen;streamingopname;insluiten;tijdreeksgegevens;streamtijdreeksgegevens;
solution: Experience Platform
title: Gegevens uit tijdreeks streamen met API's voor streaming insluiting
type: Tutorial
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---

# Gegevens uit de tijdreeks streamen met behulp van Streaming Ingestie-API&#39;s

Deze zelfstudie helpt u bij het gebruik van streaming opname-API&#39;s, onderdeel van de Adobe Experience Platform [!DNL Data Ingestion Service] API&#39;s.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van verschillende Adobe Experience Platform-services. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] ervaringsgegevens ordent.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, consumentenprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
- [ de ontwikkelaarsgids van de Registratie van het Schema ](../../xdm/api/getting-started.md): Een uitvoerige gids die elk van de beschikbare eindpunten van [!DNL Schema Registry] API behandelt en hoe te om vraag aan hen te maken. Dit omvat het kennen van uw `{TENANT_ID}`, die in vraag door dit leerprogramma verschijnt, evenals het weten hoe te om schema&#39;s tot stand te brengen, die in het creëren van een dataset voor opname wordt gebruikt.

Bovendien is voor deze zelfstudie vereist dat u al een streamingverbinding hebt gemaakt. Voor meer informatie bij het creëren van een het stromen verbinding, te lezen gelieve [ een het stromen verbindingsleerprogramma ](./create-streaming-connection.md) creëren.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../landing/api-guide.md).

## Stel een schema samen dat van de klasse XDM ExperienceEvent wordt gebaseerd

Om een dataset tot stand te brengen, zult u eerst een nieuw schema moeten creëren dat de [!DNL XDM ExperienceEvent] klasse uitvoert. Voor meer informatie over hoe te om schema&#39;s tot stand te brengen, te lezen gelieve de [ gids van de ontwikkelaar van de Registratie API van het Schema ](../../xdm/api/getting-started.md).

**API formaat**

```http
POST /schemaregistry/tenant/schemas
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `meta:immutableTags` | In dit voorbeeld wordt de tag `union` gebruikt om uw gegevens in [[!DNL Real-Time Customer Profile]](../../profile/home.md) te behouden. |

**Reactie**

Een succesvolle reactie keert status 201 van HTTP met details van uw onlangs gecreeerd schema terug.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
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
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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
| `{SCHEMA_REF_ID}` | De `$id` die u eerder hebt ontvangen toen u het schema samenstelde. Het moet er ongeveer als volgt uitzien: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; **Codes Namespace van de Identiteit**
>
> Controleer of de codes geldig zijn. In het bovenstaande voorbeeld wordt &quot;email&quot; gebruikt, een naamruimte met een standaardidentiteit. Andere algemeen gebruikte standaardidentiteitsnamespaces kunnen binnen de [ Veelgestelde vragen van de Dienst van de Identiteit ](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform) worden gevonden.
>
> Als u een douane zou willen tot stand brengen namespace, volg de stappen die in het [ overzicht van identiteitsnaamruimte ](../../identity-service/home.md) worden geschetst.

**Reactie**

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
    "imsOrg": "{ORG_ID}"
}
```

## Een gegevensset maken voor de gegevens van tijdreeksen

Zodra u uw schema hebt gecreeerd, zult u een dataset moeten tot stand brengen om verslaggegevens in te voeren.

>[!NOTE]
>
>Deze gegevensset wordt ingeschakeld voor **[!DNL Real-Time Customer Profile]** en **[!DNL Identity]** door de juiste codes in te stellen.

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
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
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
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```


## Een streamingverbinding maken

Na het creëren van uw schema en dataset, zult u een het stromen verbinding moeten tot stand brengen om uw gegevens in te voeren.

Voor meer informatie bij het creëren van een het stromen verbinding, te lezen gelieve [ een het stromen verbindingsleerprogramma ](./create-streaming-connection.md) creëren.

## Gegevens uit tijdreeksen opnemen in de streamingverbinding

Met de dataset, het stromen verbinding, en dataflow gecreeerd, kunt u XDM-Geformatteerde JSON verslagen opnemen om tijdreeksgegevens binnen [!DNL Experience Platform] in te voeren.

**API formaat**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` -waarde van de nieuwe streamingverbinding. |
| `syncValidation` | Een optionele query-parameter voor ontwikkelingsdoeleinden. Indien ingesteld op `true` , kan dit worden gebruikt voor directe feedback om te bepalen of de aanvraag is verzonden. Deze waarde wordt standaard ingesteld op `false` . Houd er rekening mee dat als u deze queryparameter instelt op `true` , de snelheid van de aanvraag beperkt blijft tot 60 keer per minuut per `CONNECTION_ID` . |

**Verzoek**

U kunt tijdreeksgegevens met of zonder de bronnaam in een streamingverbinding invoegen.

In de onderstaande voorbeeldaanvraag worden gegevens uit tijdreeksen met een ontbrekende bronnaam opgenomen in Experience Platform. Als de bronnaam ontbreekt in de gegevens, wordt de bron-id toegevoegd uit de definitie van de streamingverbinding.

Zowel `xdmEntity._id` als `xdmEntity.timestamp` zijn vereiste velden voor tijdreeksgegevens. Het `xdmEntity._id` attribuut vertegenwoordigt een uniek herkenningsteken voor het verslag zelf, **niet** een unieke identiteitskaart van de persoon of het apparaat waarvan verslag het is.

U moet uw eigen `xdmEntity._id` en `xdmEntity.timestamp` voor de record genereren op een manier die consistent blijft als de record ooit opnieuw moet worden opgenomen. In het ideale geval bevat uw bronsysteem deze waarden. Als een id niet beschikbaar is, kunt u waarden van andere velden in de record samenvoegen om een unieke waarde te maken die consistent opnieuw kan worden gegenereerd op basis van de record bij opnieuw invoegen.

>[!NOTE]
>
>De volgende API vraag **** vereist geen authentificatiekopballen.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
    "datasetId": "{DATASET_ID}",
    "flowId": "{FLOW_ID}",
    "imsOrgID": "{ORG_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            },
        "identityMap": {
                "Email": [
                  {
                    "id": "acme_user@gmail.com",
                    "primary": true
                  }
                ]
              },
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
    "datasetId": "{DATASET_ID}",
    "flowId": "{FLOW_ID}",
    "imsOrgID": "{ORG_ID}",
      "source": {
        "name": "ACME source"
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
| `{CONNECTION_ID}` | De `inletId` van de eerder gemaakte streamingverbinding. |
| `xactionId` | Een unieke id die op de server is gegenereerd voor de record die u zojuist hebt verzonden. Met deze id kan Adobe de levenscyclus van deze record volgen via verschillende systemen en met foutopsporing. |
| `receivedTimeMs`: Een tijdstempel (tijdperk in milliseconden) dat aangeeft op welk tijdstip de aanvraag is ontvangen. |
| `syncValidation.status` | Aangezien de queryparameter `syncValidation=true` is toegevoegd, wordt deze waarde weergegeven. Als de validatie is gelukt, is de status `pass` . |

## De nieuw ingevoerde tijdreeksgegevens ophalen

Als u de eerder opgenomen records wilt valideren, gebruikt u de [[!DNL Profile Access API]](../../profile/api/entities.md) om de gegevens van de tijdreeks op te halen. Dit kan worden gedaan gebruikend een verzoek van GET aan het `/access/entities` eindpunt en het gebruiken van facultatieve vraagparameters. U kunt meerdere parameters gebruiken, gescheiden door ampersands (&amp;).&quot;

>[!NOTE]
>
>Als identiteitskaart van het fusiebeleid niet wordt bepaald en `schema.name` of `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] zal **alle** verwante identiteiten halen.

**API formaat**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `schema.name` | **Vereist.** De naam van het schema dat u opent. |
| `relatedSchema.name` | **Vereist.** Aangezien u een `_xdm.context.experienceevent` opent, geeft deze waarde het schema op voor de profielentiteit waaraan de gebeurtenissen uit de tijdreeks zijn gerelateerd. |
| `relatedEntityId` | De id van de verbonden entiteit. Indien opgegeven, moet u ook de naamruimte voor entiteiten opgeven. |
| `relatedEntityIdNS` | De naamruimte van de id die u probeert op te halen. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Reactie**

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

Door dit document te lezen, begrijpt u nu hoe u recordgegevens via streamingverbindingen in [!DNL Experience Platform] kunt opnemen. U kunt proberen meer vraag met verschillende waarden te maken en de bijgewerkte waarden terug te winnen. Bovendien kunt u uw ingesloten gegevens controleren via de gebruikersinterface van [!DNL Experience Platform] . Voor meer informatie, te lezen gelieve de [ controle gegevensopname ](../quality/monitor-data-ingestion.md) gids.

Voor meer informatie over het stromen ingestie in het algemeen, te lezen gelieve het [ stromen ingestitieoverzicht ](../streaming-ingestion/overview.md).
