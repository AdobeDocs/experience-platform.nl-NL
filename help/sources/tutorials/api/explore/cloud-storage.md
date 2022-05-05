---
keywords: Experience Platform;home;populaire onderwerpen;cloudopslag;Cloudopslag
title: Een Cloud Storage-map verkennen met de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om een extern cloudopslagsysteem te verkennen.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 1333eac5e022ef32f051120496154a88e2f9324e
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# Ontdek uw mappen voor cloudopslag met de [!DNL Flow Service] API

Deze zelfstudie bevat stappen voor het verkennen en voorvertonen van de structuur en inhoud van uw cloudopslag met de [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>Als u uw cloudopslag wilt verkennen, moet u al beschikken over een geldige basis-verbindings-id voor een bron voor cloudopslag. Als u deze id niet hebt, raadpleegt u de [overzicht van bronnen](../../../home.md#cloud-storage) voor een lijst met bronnen voor cloudopslag waarmee u een basisverbinding kunt maken.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../landing/api-guide.md).

## Ontdek uw mappen voor cloudopslag

U kunt informatie over de structuur van uw mappen voor cloudopslag opvragen door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API terwijl het verstrekken van de identiteitskaart van de basisverbinding van uw bron.

Wanneer u GET-aanvragen uitvoert om uw cloudopslag te verkennen, moet u de queryparameters opnemen die in de onderstaande tabel worden vermeld:

| Parameter | Beschrijving |
| --------- | ----------- |
| `objectType` | Het type object dat u wilt verkennen. Stel deze waarde in op: <ul><li>`folder`: Een specifieke map verkennen</li><li>`root`: Verken de hoofdmap.</li></ul> |
| `object` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. |


**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert een array met bestanden en mappen die in de gevraagde map zijn gevonden. De `path` eigenschap van het bestand dat u wilt uploaden, aangezien u dit in de volgende stap moet opgeven om de structuur te controleren.

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

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De verbindings-id van de bronconnector van de cloudopslag. |
| `{FILE_PATH}` | Het pad naar het bestand dat u wilt inspecteren. |
| `{FILE_TYPE}` | Het type bestand. Tot de ondersteunde bestandstypen behoren:<ul><li>AFGELEGD</code>: Waarde gescheiden door scheidingstekens. DSV-bestanden moeten door komma&#39;s van elkaar worden gescheiden.</li><li>JSON</code>: JavaScript-objectnotatie. JSON-bestanden moeten XDM-compatibel zijn</li><li>PARQUET</code>: Apache Parquet. Parketbestanden moeten XDM-compatibel zijn.</li></ul> |
| `{QUERY_PARAMS}` | Optionele queryparameters die kunnen worden gebruikt om resultaten te filteren. Zie de sectie over [queryparameters](#query) voor meer informatie . |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

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

De [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) ondersteunt het gebruik van queryparameters voor het voorvertonen en inspecteren van verschillende bestandstypen.

| Parameter | Beschrijving |
| --------- | ----------- |
| `columnDelimiter` | De waarde van één teken die u hebt opgegeven als kolomscheidingsteken voor het inspecteren van CSV- of TSV-bestanden. Als de parameter niet opgegeven is, wordt de waarde standaard ingesteld op een komma `(,)`. |
| `compressionType` | Een vereiste queryparameter voor het voorvertonen van een gecomprimeerd, gescheiden of JSON-bestand. De ondersteunde gecomprimeerde bestanden zijn: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Volgende stappen

Aan de hand van deze zelfstudie hebt u uw cloudopslagsysteem verkend en hebt u het pad gevonden van het bestand waarnaar u wilt overbrengen [!DNL Platform]en de structuur ervan bekijken. U kunt deze informatie in de volgende zelfstudie gebruiken om [gegevens verzamelen van uw cloudopslag en deze in Platform brengen](../collect/cloud-storage.md).
