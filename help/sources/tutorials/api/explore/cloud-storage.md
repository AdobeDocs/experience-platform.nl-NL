---
keywords: Experience Platform;home;populaire onderwerpen;cloudopslag;Cloudopslag
title: Een Cloud Storage-map verkennen met de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om een extern cloudopslagsysteem te verkennen.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 9b9803b4d2aeb2a86ef980f34ee34909679ea3d9
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Ontdek uw mappen voor cloudopslag met de API van [!DNL Flow Service]

Deze zelfstudie bevat stappen voor het verkennen en voorvertonen van de structuur en inhoud van uw cloudopslag met de [[!DNL Flow Service] ](https://www.adobe.io/experience-platform-apis/references/flow-service/) -API.

>[!NOTE]
>
>Als u uw cloudopslag wilt verkennen, moet u al beschikken over een geldige basis-verbindings-id voor een bron voor cloudopslag. Als u dit identiteitskaart niet hebt, dan zie het [ overzicht van bronnen ](../../../home.md#cloud-storage) voor een lijst van de bronnen van de wolkenopslag die u een basisverbinding kunt tot stand brengen met.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../landing/api-guide.md).

## Ontdek uw mappen voor cloudopslag

U kunt informatie over de structuur van uw mappen voor cloudopslag ophalen door een aanvraag voor een GET in te dienen bij de API van [!DNL Flow Service] en de basis-verbindings-id van uw bron op te geven.

Wanneer u GET-aanvragen uitvoert om uw cloudopslag te verkennen, moet u de queryparameters opnemen die in de onderstaande tabel worden vermeld:

| Parameter | Beschrijving |
| --------- | ----------- |
| `objectType` | Het type object dat u wilt verkennen. Stel deze waarde in op: <ul><li>`folder`: een specifieke map verkennen</li><li>`root` : verken de hoofdmap.</li></ul> |
| `object` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. |


**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbindings-id van de bron voor cloudopslag. |
| `{PATH}` | Het pad van een map. |

**Verzoek**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord retourneert een array met bestanden en mappen die in de gevraagde map zijn gevonden. Let op de eigenschap `path` van het bestand dat u wilt uploaden, aangezien u dit in de volgende stap moet opgeven om de structuur te controleren.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een bestand Inspect

Om de structuur van gegevensdossier van uw cloudopslag te inspecteren, voer een verzoek van de GET uit terwijl het verstrekken van de weg van het dossier en type als vraagparameter.

U kunt de structuur van een gegevensbestand van uw bron van de wolkenopslag inspecteren door een verzoek van de GET uit te voeren terwijl het verstrekken van de weg en het type van het dossier. U kunt ook verschillende bestandstypen inspecteren, zoals CSV, TSV of gecomprimeerde JSON en gescheiden bestanden door de bestandstypen op te geven als onderdeel van de queryparameters.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&fileType=delimited&encoding=ISO-8859-1;
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De verbindings-id van de bronaansluiting voor de cloud. |
| `{FILE_PATH}` | Het pad naar het bestand dat u wilt inspecteren. |
| `{FILE_TYPE}` | Het type bestand. Tot de ondersteunde bestandstypen behoren:<ul><li><code> DELIMITED</code>: door scheidingstekens gescheiden waarde. DSV-bestanden moeten door komma&#39;s van elkaar worden gescheiden.</li><li><code> JSON</code>: JavaScript Object Notation. JSON-bestanden moeten XDM-compatibel zijn</li><li><code> PARQUET</code>: Apache Parquet. Parketbestanden moeten XDM-compatibel zijn.</li></ul> |
| `{QUERY_PARAMS}` | Optionele queryparameters die kunnen worden gebruikt om resultaten te filteren. Zie de sectie over [ vraagparameters ](#query) voor meer informatie. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord geeft de structuur van het gevraagde dossier met inbegrip van lijstnamen en gegevenstypes terug.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Query-parameters gebruiken {#query}

[[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/) steunt het gebruik van vraagparameters aan voorproef en inspecteer verschillende dossiertypes.

| Parameter | Beschrijving |
| --------- | ----------- |
| `columnDelimiter` | De waarde van één teken die u hebt opgegeven als kolomscheidingsteken voor het inspecteren van CSV- of TSV-bestanden. Wanneer de parameter niet is opgegeven, wordt voor de waarde een komma `(,)` gebruikt. |
| `compressionType` | Een vereiste queryparameter voor het voorvertonen van een gecomprimeerd, gescheiden of JSON-bestand. De volgende bestanden worden ondersteund: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Definieert welk coderingstype moet worden gebruikt bij het renderen van de voorvertoning. De volgende coderingstypen worden ondersteund: `UTF-8` en `ISO-8859-1` . **Nota**: De `encoding` parameter is slechts beschikbaar wanneer het opnemen van afgebakende Csv- dossiers. Andere bestandstypen worden met de standaardcodering `UTF-8` opgenomen. |

## Volgende stappen

Aan de hand van deze zelfstudie hebt u uw cloudopslagsysteem verkend, het pad gevonden van het bestand dat u wilt introduceren in [!DNL Platform] en de structuur ervan bekeken. U kunt deze informatie in het volgende leerprogramma gebruiken [ gegevens van uw wolkenopslag verzamelen en het brengen in Platform ](../collect/cloud-storage.md).
