---
keywords: Experience Platform;import verpakt recept;Data Science Workspace;populaire onderwerpen;recepten;api;sensei machine learning;create engine
solution: Experience Platform
title: Een gecomprimeerde ontvanger importeren met de API voor leren van de Sensei-computer
type: Tutorial
description: Deze zelfstudie gebruikt de API voor het leren van Sensei-machines om een engine te maken, die ook wel een recept in de gebruikersinterface wordt genoemd.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 0%

---

# Een verpakt recept importeren met de API voor leren van Sensei Machine

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Dit leerprogramma gebruikt [[!DNL Sensei Machine Learning API] &#x200B;](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) om een [&#x200B; Motor &#x200B;](../api/engines.md) tot stand te brengen, die ook als Ontvanger in het gebruikersinterface wordt bekend.

Voordat u aan de slag gaat, moet u weten dat Adobe Experience Platform [!DNL Data Science Workspace] verschillende termen gebruikt om te verwijzen naar vergelijkbare elementen in de API en de gebruikersinterface. De API-termen worden in deze zelfstudie gebruikt en in de volgende tabel worden de corresponderende termen beschreven:

| UI-term | API-term |
| ---- | ---- |
| Recipe | [&#x200B; Motor &#x200B;](../api/engines.md) |
| Model | [&#x200B; MLInstance &#x200B;](../api/mlinstances.md) |
| Opleiding en evaluatie | [&#x200B; Experiment &#x200B;](../api/experiments.md) |
| Service | [&#x200B; MLService &#x200B;](../api/mlservices.md) |

Een motor bevat machine het leren algoritmen en logica om specifieke problemen op te lossen. In het onderstaande diagram ziet u een visualisatie van de API-workflow in [!DNL Data Science Workspace] . Deze zelfstudie richt zich op het maken van een engine, het brein van een model voor machinaal leren.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Aan de slag

Voor deze zelfstudie is een Recipe-bestand in het pakket vereist in de vorm van een docker-URL. Volg de [&#x200B; brondossiers van het Pakket in een Ontvanger &#x200B;](./package-source-files-recipe.md) leerprogramma om een verpakt Ontvanger dossier tot stand te brengen of uw te verstrekken.

- `{DOCKER_URL}`: Een URL-adres naar een Docker-afbeelding van een intelligente service.

Dit leerprogramma vereist u om de [&#x200B; Authentificatie aan zelfstudie van Adobe Experience Platform &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Experience Platform] APIs met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- `{ACCESS_TOKEN}`: De specifieke tokenwaarde voor toonder die na verificatie wordt opgegeven.
- `{ORG_ID}`: Uw organisatiereferenties zijn gevonden in uw unieke Adobe Experience Platform-integratie.
- `{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.

## Een engine maken

De motoren kunnen worden gecreeerd door een POST- verzoek aan het /engines eindpunt te maken. De gemaakte engine wordt geconfigureerd op basis van de vorm van het pakketbestand Recipe dat moet worden opgenomen als onderdeel van de API-aanvraag.

### Een engine maken met een docker-URL {#create-an-engine-with-a-docker-url}

Als u een engine wilt maken met een pakketbestand Recipe dat is opgeslagen in een Docker-container, moet u de docker-URL opgeven voor het pakketbestand Recipe.

>[!CAUTION]
>
> Gebruik de onderstaande aanvraag als u [!DNL Python] of R gebruikt. Als u PySpark of Scala gebruikt, gebruik het PySpark/Scala- verzoekvoorbeeld dat onder het Python/R voorbeeld wordt gevestigd.

**API formaat**

```http
POST /engines
```

**Verzoek Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `engine.name` | De gewenste naam voor de engine. Recipe die overeenkomt met deze engine, neemt deze waarde over die in de gebruikersinterface van [!DNL Data Science Workspace] moet worden weergegeven als de naam van de ontvanger. |
| `engine.description` | Een facultatieve beschrijving voor de motor. Recipe die overeenkomt met deze engine, neemt deze waarde over die in de gebruikersinterface van [!DNL Data Science Workspace] moet worden weergegeven als de beschrijving van de ontvanger. Verwijder deze eigenschap niet. Laat deze waarde een lege tekenreeks zijn als u geen beschrijving opgeeft. |
| `engine.type` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is ontwikkeld. Wanneer een docker-URL wordt opgegeven om een engine te maken, is `type` ofwel `Python` , `R` , `PySpark` , `Spark` (Scala) of `Tensorflow` . |
| `artifacts.default.image.location` | Uw `{DOCKER_URL}` komt hier. Een volledige docker-URL heeft de volgende structuur: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Een extra naam voor het Docker-afbeeldingsbestand. Verwijder deze eigenschap niet. Laat deze waarde een lege tekenreeks zijn als u ervoor kiest geen extra bestandsnaam voor een Docker-afbeelding op te geven. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van deze engine. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is ontwikkeld. Wanneer een docker-URL wordt opgegeven om een engine te maken, is `executionType` ofwel `Python` , `R` , `PySpark` , `Spark` (Scala) of `Tensorflow` . |

**Verzoek PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Schaal van het Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde Motor met inbegrip van zijn uniek herkenningsteken (`id`) bevat. De volgende voorbeeldreactie is voor een [!DNL Python] Motor. De toetsen `executionType` en `type` veranderen op basis van de opgegeven POST.

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

Een succesvolle reactie toont een nuttige lading JSON met informatie betreffende de pas gecreëerde Motor. De sleutel `id` vertegenwoordigt het unieke herkenningsteken van de Motor en wordt vereist in het volgende leerprogramma om een MLInstance tot stand te brengen. Controleer of de engine-id is opgeslagen voordat u verdergaat met de volgende stappen.

## Volgende stappen {#next-steps}

U hebt een engine gemaakt met de API en er is een unieke engine-id verkregen als onderdeel van de responsstructuur. U kunt dit herkenningsteken van de Motor in het volgende leerprogramma gebruiken aangezien u leert hoe te [&#x200B; creëren, een Model te trainen en te evalueren gebruikend API &#x200B;](./train-evaluate-model-api.md).
