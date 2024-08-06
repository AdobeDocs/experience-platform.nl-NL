---
keywords: Experience Platform;in een pakket opgenomen recept importeren;Data Science Workspace;populaire onderwerpen;recepten;api;sensei machine learning;create engine
solution: Experience Platform
title: Een gecomprimeerde ontvanger importeren met de Sensei Machine Learning-API
type: Tutorial
description: In deze zelfstudie wordt de Sensei Machine Learning-API gebruikt om een engine te maken, die ook wel een ontvanger in de gebruikersinterface wordt genoemd.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 0%

---

# Importeer een verpakt recept met de Sensei Machine Learning API

>[!NOTE]
>
>Data Science Workspace is niet meer verkrijgbaar.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten voor Data Science Workspace.

Dit leerprogramma gebruikt [[!DNL Sensei Machine Learning API] ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) om een [ Motor ](../api/engines.md) tot stand te brengen, die ook als Ontvanger in het gebruikersinterface wordt bekend.

Voordat u aan de slag gaat, moet u weten dat Adobe Experience Platform [!DNL Data Science Workspace] verschillende termen gebruikt om te verwijzen naar vergelijkbare elementen in de API en de UI. In deze zelfstudie worden de API-termen gebruikt en in de volgende tabel worden de bijbehorende termen beschreven:

| UI-term | API-term |
| ---- | ---- |
| Recipe | [ Motor ](../api/engines.md) |
| Model | [ MLInstance ](../api/mlinstances.md) |
| Opleiding en evaluatie | [ Experiment ](../api/experiments.md) |
| Service | [ MLService ](../api/mlservices.md) |

Een engine bevat machine-learningalgoritmen en logica om specifieke problemen op te lossen. In het onderstaande diagram ziet u een visualisatie van de API-workflow in [!DNL Data Science Workspace] . Deze zelfstudie richt zich op het creëren van een Engine, het brein van een machine-learningmodel.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Aan de slag

Voor deze zelfstudie is een ontvangerbestand in een pakket nodig in de vorm van een docker-URL. Volg de [ Van het Pakket brondossiers in een Ontvanger ](./package-source-files-recipe.md) leerprogramma om een pakket te creëren Ontvangt dossier of uw te verstrekken.

- `{DOCKER_URL}`: Een URL-adres naar een dockerafbeelding van een intelligente service.

Dit leerprogramma vereist u om de [ Authentificatie aan het leerprogramma van Adobe Experience Platform ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Platform] APIs met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt weergegeven:

- `{ACCESS_TOKEN}`: uw specifieke togertokenwaarde die u na verificatie opgeeft.
- `{ORG_ID}`: uw organisatiegegevens zijn gevonden in uw unieke Adobe Experience Platform-integratie.
- `{API_KEY}`: uw specifieke API-sleutelwaarde in uw unieke Adobe Experience Platform-integratie.

## Een engine maken

De motoren kunnen worden gecreeerd door een verzoek van de POST aan het /engines eindpunt te doen. De gemaakte engine wordt geconfigureerd op basis van de vorm van het pakketbestand met ontvangers die moet worden opgenomen als onderdeel van de API-aanvraag.

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
| `engine.name` | De gewenste naam voor de engine. De ontvanger die overeenkomt met deze engine neemt deze waarde over die in de gebruikersinterface van [!DNL Data Science Workspace] wordt weergegeven als de naam van de ontvanger. |
| `engine.description` | Een optionele beschrijving voor de engine. De ontvanger die overeenkomt met deze engine neemt deze waarde over die in de gebruikersinterface van [!DNL Data Science Workspace] moet worden weergegeven als de beschrijving van de ontvanger. Verwijder deze eigenschap niet. Gebruik een lege tekenreeks als u geen beschrijving wilt opgeven. |
| `engine.type` | Het uitvoeringstype van de engine. Deze waarde komt overeen met de taal waarin de dockerafbeelding is ontwikkeld. Wanneer een docker-URL wordt opgegeven om een engine te maken, is `type` ofwel `Python` , `R` , `PySpark` , `Spark` (Scala) of `Tensorflow` . |
| `artifacts.default.image.location` | Uw `{DOCKER_URL}` komt hier. Een volledige docker-URL heeft de volgende structuur: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Een extra naam voor het Docker-afbeeldingsbestand. Verwijder deze eigenschap niet, laat deze waarde een lege tekenreeks zijn als u ervoor kiest om geen extra bestandsnaam voor de Docker-afbeelding op te geven. |
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
| `name` | De gewenste naam voor de engine. De ontvanger die overeenkomt met deze engine, neemt deze waarde over die in de gebruikersinterface moet worden weergegeven als de naam van de ontvanger. |
| `description` | Een optionele beschrijving voor de engine. De ontvanger die overeenkomt met deze engine neemt deze waarde over die in de gebruikersinterface moet worden weergegeven als beschrijving van de ontvanger. Deze eigenschap is vereist. Als u geen beschrijving wilt opgeven, stelt u de waarde ervan in op een lege tekenreeks. |
| `type` | Het uitvoeringstype van de engine. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;PySpark&quot;. |
| `mlLibrary` | Een veld dat is vereist bij het maken van engines voor PySpark- en Scala-formaten. |
| `artifacts.default.image.location` | De locatie van de Docker-afbeelding die is gekoppeld aan een Docker-URL. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van de engine. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;Spark&quot;. |

**Verzoek Scala**

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
| `name` | De gewenste naam voor de engine. De ontvanger die overeenkomt met deze engine, neemt deze waarde over die in de gebruikersinterface moet worden weergegeven als de naam van de ontvanger. |
| `description` | Een optionele beschrijving voor de engine. De ontvanger die overeenkomt met deze engine neemt deze waarde over die in de gebruikersinterface moet worden weergegeven als beschrijving van de ontvanger. Deze eigenschap is vereist. Als u geen beschrijving wilt opgeven, stelt u de waarde ervan in op een lege tekenreeks. |
| `type` | Het uitvoeringstype van de engine. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;Spark&quot;. |
| `mlLibrary` | Een gebied dat wordt vereist wanneer het creëren van motoren voor PySpark en Scala recepten. |
| `artifacts.default.image.location` | De locatie van de Docker-afbeelding waarnaar een Docker-URL verwijst. |
| `artifacts.default.image.executionType` | Het uitvoeringstype van de motor. Deze waarde komt overeen met de taal waarin de Docker-afbeelding is gebaseerd op &quot;Spark&quot;. |

**Reactie**

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde Motor met inbegrip van zijn uniek herkenningsteken bevat (`id`). De volgende voorbeeldreactie is voor een [!DNL Python] Engine. De toetsen `executionType` en `type` veranderen op basis van de opgegeven POST.

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

Een geslaagde reactie laat een JSON-lading zien met informatie over de nieuwe engine. De sleutel `id` vertegenwoordigt de unieke engine-id en is vereist in de volgende zelfstudie om een MLInstance te maken. Zorg ervoor dat de engine-id is opgeslagen voordat u doorgaat met de volgende stappen.

## Volgende stappen {#next-steps}

U hebt een engine gemaakt met behulp van de API en er is een unieke engine-id verkregen als onderdeel van de hoofdtekst van de respons. U kunt dit herkenningsteken van de Motor in het volgende leerprogramma gebruiken aangezien u leert om [ te creëren, een Model te trainen en te evalueren gebruikend API ](./train-evaluate-model-api.md).
