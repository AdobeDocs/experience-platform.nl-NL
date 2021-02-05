---
keywords: Experience Platform;ontwikkelaarshandleiding;eindpunt;Data Science Workspace;populaire onderwerpen;engines;sensei machine learning api
solution: Experience Platform
title: Engine API-eindpunt
topic: Developer guide
description: Motoren vormen de basis voor het leren van machines Modellen in de werkruimte van de wetenschap van gegevens. Zij bevatten machinaal leeralgoritmen die specifieke problemen oplossen, eigenschappijpleidingen om eigenschapengineering uit te voeren, of allebei.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---


# Het eindpunt Motoren

Motoren vormen de basis voor het leren van machines Modellen in de werkruimte van de wetenschap van gegevens. Zij bevatten machinaal leeralgoritmen die specifieke problemen oplossen, eigenschappijpleidingen om eigenschapengineering uit te voeren, of allebei.

## Zoek uw registratie van de Docker

>[!TIP]
>
>Als u geen Docker URL hebt, bezoek [de brondossiers van het Pakket in een recept](../models-recipes/package-source-files-recipe.md) leerprogramma voor een geleidelijke analyse bij het creëren van een gastheer URL van het Docker.

Uw Docker-registergegevens zijn vereist voor het uploaden van een pakket Recipe-bestand, inclusief de URL van de Docker-host, gebruikersnaam en wachtwoord. U kunt deze informatie opzoeken door de volgende GET-aanvraag uit te voeren:

**API-indeling**

```https
GET /engines/dockerRegistry
```

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een nuttige lading terug die de details van uw registratie van de Dokker met inbegrip van de Docker URL (`host`), gebruikersbenaming (`username`), en wachtwoord (`password`) bevat.

>[!NOTE]
>
>Uw Docker wachtwoord verandert wanneer uw `{ACCESS_TOKEN}` wordt bijgewerkt.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Een engine maken met Docker-URL&#39;s {#docker-image}

U kunt een Motor tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van zijn meta-gegevens en een Dokker URL die verwijzingen een beeld van de Dokker in meerdelige vormen.

**API-indeling**

```https
POST /engines
```

**Python/R aanvragen**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De gewenste naam voor de engine. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in UI als naam van de Ontvanger moet worden getoond. |
| `description` | Een facultatieve beschrijving voor de motor. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in UI als beschrijving van de Ontvanger moet worden getoond. Deze eigenschap is vereist. Als u geen beschrijving wilt opgeven, stelt u de waarde in op een lege tekenreeks. |
| `type` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is opgebouwd en kan &#39;Python&#39;, &#39;R&#39; of &#39;Tensorflow&#39; zijn. |
| `algorithm` | Een tekenreeks die het type algoritme voor machinaal leren opgeeft. Tot de ondersteunde typen algoritmen behoren &#39;Classificatie&#39;, &#39;Regression&#39; of &#39;Aangepast&#39;. |
| `artifacts.default.image.location` | De locatie van de Docker-afbeelding waarnaar een Docker-URL verwijst. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is opgebouwd en kan &#39;Python&#39;, &#39;R&#39; of &#39;Tensorflow&#39; zijn. |

**Request PySpark/Scala**

Wanneer het doen van een verzoek om PySpark recepten, `executionType` en `type` is &quot;PySpark&quot;. Wanneer het doen van een verzoek om Scala recepten, `executionType` en `type` is &quot;Vonk&quot;. In het volgende Scala-receptvoorbeeld wordt Spark gebruikt:

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De gewenste naam voor de engine. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in UI als naam van de Ontvanger moet worden getoond. |
| `description` | Een facultatieve beschrijving voor de motor. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in UI als beschrijving van de Ontvanger moet worden getoond. Deze eigenschap is vereist. Als u geen beschrijving wilt opgeven, stelt u de waarde in op een lege tekenreeks. |
| `type` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarop de Docker-afbeelding is gebaseerd. De waarde kan aan Vonk of PySpark worden geplaatst. |
| `mlLibrary` | Een gebied dat wordt vereist wanneer het creëren van motoren voor PySpark en Scala recepten. Dit veld moet worden ingesteld op `databricks-spark`. |
| `artifacts.default.image.location` | De locatie van de Docker-afbeelding. Alleen Azure ACR of Public (niet-geverifieerd) Dockerhub wordt ondersteund. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarop de Docker-afbeelding is gebaseerd. Dit kan &quot;Vonk&quot;of &quot;PySpark&quot;zijn. |

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde Motor met inbegrip van zijn uniek herkenningsteken (`id`) bevat. De volgende voorbeeldreactie is voor een Python Engine. Alle antwoorden van de Motor volgen dit formaat:

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Creeer een motor van de eigenschappijpleiding gebruikend de Url {#feature-pipeline-docker} van de Dokker

U kunt een Motor van de eigenschappijpleiding tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van zijn meta-gegevens en een Dok URL die verwijzingen een beeld van het Dokker.

**API-indeling**

```https
POST /engines
```

**Verzoek**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `type` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarop de Docker-afbeelding is gebaseerd. De waarde kan aan Vonk of PySpark worden geplaatst. |
| `algorithm` | Het algoritme dat wordt gebruikt, plaats deze waarde aan `fp` (eigenschappijpleiding). |
| `name` | De gewenste naam voor de motor van de eigenschappijpleiding. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in UI als naam van de Ontvanger moet worden getoond. |
| `description` | Een facultatieve beschrijving voor de motor. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in UI als beschrijving van de Ontvanger moet worden getoond. Deze eigenschap is vereist. Als u geen beschrijving wilt opgeven, stelt u de waarde in op een lege tekenreeks. |
| `mlLibrary` | Een gebied dat wordt vereist wanneer het creëren van motoren voor PySpark en Scala recepten. Dit veld moet worden ingesteld op `databricks-spark`. |
| `artifacts.default.image.location` | De locatie van de Docker-afbeelding. Alleen Azure ACR of Public (niet-geverifieerd) Dockerhub wordt ondersteund. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarop de Docker-afbeelding is gebaseerd. Dit kan &quot;Vonk&quot;of &quot;PySpark&quot;zijn. |
| `artifacts.default.image.packagingType` | Het verpakkingstype van de motor. Deze waarde moet worden ingesteld op `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Uw `pipeline.json` parameters van het configuratiedossier. |

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde motor van de eigenschappijpleiding met inbegrip van zijn uniek herkenningsteken (`id`) bevat. De volgende voorbeeldreactie is voor een PySpark eigenschappijpleidingsmotor.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## Een lijst met motoren ophalen

U kunt een lijst van Motoren terugwinnen door één enkel verzoek van de GET uit te voeren. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activa herwinning](./appendix.md#query).

**API-indeling**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met engines en hun details.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### Een specifieke engine {#retrieve-specific} ophalen

U kunt de details van een specifieke Motor terugwinnen door een verzoek van de GET uit te voeren dat identiteitskaart van de gewenste Motor in de verzoekweg omvat.

**API-indeling**

```https
GET /engines/{ENGINE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENGINE_ID}` | De id van een bestaande engine. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van de gewenste Motor bevatten.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## Een engine bijwerken

U kunt een bestaande Motor wijzigen en bijwerken door zijn eigenschappen door een verzoek van de PUT te beschrijven dat identiteitskaart van de doelmotor in de verzoekweg omvat en een nuttige lading te verstrekken JSON die bijgewerkte eigenschappen bevat.

>[!NOTE]
>
>Om het succes van dit verzoek van de PUT te verzekeren, wordt gesuggereerd dat eerst u een verzoek van de GET aan [terugwinning de Motor door ID](#retrieve-specific) uitvoert. Pas vervolgens het geretourneerde JSON-object aan en werk dit bij en pas het gehele gewijzigde JSON-object toe als de payload voor het verzoek om PUT.

De volgende voorbeeld-API-aanroep werkt de naam en beschrijving van een engine bij terwijl deze in eerste instantie deze eigenschappen heeft:

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**API-indeling**

```https
PUT /engines/{ENGINE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENGINE_ID}` | De id van een bestaande engine. |

**Verzoek**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**Antwoord**

Een succesvolle reactie keert een lading terug die de bijgewerkte details van de Motor bevat.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Een engine verwijderen

U kunt een Motor schrappen door een verzoek van DELETE uit te voeren terwijl het specificeren van identiteitskaart van de doelmotor in de verzoekweg. Als een engine wordt verwijderd, worden alle MLInstances die naar die engine verwijzen, met inbegrip van alle experimenten en experimentele tests die tot die MLInstances behoren, trapsgewijs verwijderd.

**API-indeling**

```https
DELETE /engines/{ENGINE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENGINE_ID}` | De id van een bestaande engine. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
