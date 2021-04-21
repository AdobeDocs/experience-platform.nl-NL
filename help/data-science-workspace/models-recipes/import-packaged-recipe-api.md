---
keywords: Experience Platform;in een pakket opgenomen recept importeren;Data Science Workspace;populaire onderwerpen;recepten;api;sensei machine leren;engine maken
solution: Experience Platform
title: Een gecomprimeerde ontvanger importeren met de API voor leren van de Sensei-machine
topic-legacy: tutorial
type: Tutorial
description: In deze zelfstudie wordt de API voor leren van Sensei-machines gebruikt om een engine te maken die ook wel een recept in de gebruikersinterface wordt genoemd.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Een verpakt recept importeren met de API voor leren van Sensei-machines

In deze zelfstudie wordt [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) gebruikt om een [Engine](../api/engines.md) te maken, ook wel een Recipe genoemd in de gebruikersinterface.

Voordat u aan de slag gaat, is het belangrijk om te weten dat Adobe Experience Platform [!DNL Data Science Workspace] verschillende termen gebruikt om te verwijzen naar vergelijkbare elementen in de API en de UI. De API-termen worden in deze zelfstudie gebruikt en in de volgende tabel worden de corresponderende termen beschreven:

| UI-term | API-term |
| ---- | ---- |
| Recipe | [Engine](../api/engines.md) |
| Model | [MLInstance](../api/mlinstances.md) |
| Opleiding en evaluatie | [Experimenteer](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Een motor bevat machine het leren algoritmen en logica om specifieke problemen op te lossen. Het diagram hieronder verstrekt een visualisatie die het API werkschema in [!DNL Data Science Workspace] toont. Deze zelfstudie richt zich op het maken van een engine, het brein van een model voor machinaal leren.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Aan de slag

Voor deze zelfstudie is een Recipe-bestand in het pakket vereist in de vorm van een docker-URL. Volg de [Brondossiers van het Pakket in een Recipe](./package-source-files-recipe.md) leerprogramma om een verpakt Recipe dossier tot stand te brengen of uw te verstrekken.

- `{DOCKER_URL}`: Een adres URL aan een beeld van de Dokker van de intelligente dienst.

Deze zelfstudie vereist dat u de [Verificatie naar Adobe Experience Platform-zelfstudie](https://www.adobe.com/go/platform-api-authentication-en) hebt voltooid om aanroepen naar [!DNL Platform] API&#39;s te kunnen uitvoeren. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- `{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.
- `{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.
- `{API_KEY}`: Uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.

## Een engine maken

De motoren kunnen worden gecreeerd door een verzoek van de POST aan het /engines eindpunt te doen. De gemaakte engine wordt geconfigureerd op basis van de vorm van het pakketbestand Recipe dat moet worden opgenomen als onderdeel van de API-aanvraag.

### Een engine maken met een docker-URL {#create-an-engine-with-a-docker-url}

Als u een engine wilt maken met een pakketbestand Recipe dat is opgeslagen in een Docker-container, moet u de docker-URL opgeven voor het pakketbestand Recipe.

>[!CAUTION]
>
> Als u [!DNL Python] of R gebruikt gebruik hieronder het verzoek. Als u PySpark of Scala gebruikt, gebruik het PySpark/Scala- verzoekvoorbeeld dat onder het Python/R voorbeeld wordt gevestigd.

**API-indeling**

```http
POST /engines
```

**Python/R aanvragen**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Eigenschap | Beschrijving |
| -------  | ----------- |
| `engine.name` | De gewenste naam voor de engine. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in [!DNL Data Science Workspace] gebruikersinterface als naam van de Ontvanger moet worden getoond. |
| `engine.description` | Een facultatieve beschrijving voor de motor. Recipe die aan deze Motor beantwoordt zal deze waarde erven die in [!DNL Data Science Workspace] gebruikersinterface als beschrijving van de Ontvanger moet worden getoond. Verwijder deze eigenschap niet. Laat deze waarde een lege tekenreeks zijn als u geen beschrijving opgeeft. |
| `engine.type` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is ontwikkeld. Wanneer een docker-URL wordt opgegeven om een engine te maken, `type` `Python`, `R`, `PySpark`, `Spark` (Scala) of `Tensorflow` is. |
| `artifacts.default.image.location` | Uw `{DOCKER_URL}` gaat hier. Een volledige docker-URL heeft de volgende structuur: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Een extra naam voor het Docker-afbeeldingsbestand. Verwijder deze eigenschap niet. Laat deze waarde een lege tekenreeks zijn als u ervoor kiest geen extra bestandsnaam voor een Docker-afbeelding op te geven. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van deze engine. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is ontwikkeld. Wanneer een docker-URL wordt opgegeven om een engine te maken, `executionType` `Python`, `R`, `PySpark`, `Spark` (Scala) of `Tensorflow` is. |

**Request PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
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
| `type` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;PySpark&quot;. |
| `mlLibrary` | Een gebied dat wordt vereist wanneer het creëren van motoren voor PySpark en Scala recepten. |
| `artifacts.default.image.location` | De locatie van de Docker-afbeelding waarnaar een Docker-URL verwijst. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;Spark&quot;. |

**Schaalaanvraag**

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
| `type` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;Spark&quot;. |
| `mlLibrary` | Een gebied dat wordt vereist wanneer het creëren van motoren voor PySpark en Scala recepten. |
| `artifacts.default.image.location` | De locatie van de Docker-afbeelding waarnaar een Docker-URL verwijst. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;Spark&quot;. |

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde Motor met inbegrip van zijn uniek herkenningsteken (`id`) bevat. De volgende voorbeeldreactie is voor een [!DNL Python] Motor. De `executionType` en `type` sleutels veranderen gebaseerd op de geleverde POST.

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Een succesvolle reactie toont een JSON nuttige lading met informatie betreffende de pas gecreëerde Motor. De `id` sleutel vertegenwoordigt het unieke herkenningsteken van de Motor en wordt vereist in het volgende leerprogramma om een MLInstance tot stand te brengen. Controleer of de engine-id is opgeslagen voordat u verdergaat met de volgende stappen.

## Volgende stappen {#next-steps}

U hebt een engine gemaakt met de API en er is een unieke engine-id verkregen als onderdeel van de responsstructuur. U kunt deze engine-id gebruiken in de volgende zelfstudie terwijl u leert hoe u een model kunt maken, trainen en evalueren met behulp van de API](./train-evaluate-model-api.md).[
