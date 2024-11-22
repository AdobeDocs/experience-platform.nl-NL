---
title: Eindpunt van mappen
description: Leer hoe u mappen maakt, bijwerkt, beheert en verwijdert met de Adobe Experience Platform API's.
role: Developer
exl-id: ee43d699-725d-4ffd-a71b-049eeb3b4d7c
source-git-commit: 78aa48701abaadea963b25e390aa96d7b31386f4
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# Mappen, eindpunt

>[!IMPORTANT]
>
>De eindpunt-URL voor deze set eindpunten is `https://experience.adobe.io` .

De omslagen zijn een capaciteit die u uw bedrijfsvoorwerpen voor gemakkelijkere navigatie en categorisering laat beter organiseren.

Deze handleiding bevat informatie die u helpt meer inzicht te krijgen in mappen en voorbeeld-API-aanroepen voor het uitvoeren van basishandelingen met de API.

## Aan de slag

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met mappen ophalen {#list}

U kunt een lijst van omslagen terugwinnen die tot uw organisatie behoren door een verzoek van de GET tot het `/folder` eindpunt te richten en het omslagtype en ouderomslag identiteitskaart te specificeren.

**API formaat**

```http
GET /folders/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Het type objecten dat zich in de map bevindt. Tot de ondersteunde waarden behoren `segment` en `dataset` . |
| `{PARENT_FOLDER_ID}` | De id van de bovenliggende map waarvan u de lijst met mappen ophaalt. Als u een lijst met alle bovenliggende mappen wilt weergeven, gebruikt u de map-id `root` . |

**Verzoek**

+++A steekproefverzoek om van alle top-level datasetomslagen een lijst te maken

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een lijst van alle top-level omslagen voor dataset in uw organisatie terug.

+++A steekproefreactie die een lijst van alle top-level omslagen voor dataset in uw organisatie bevat.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## Nieuwe map maken {#create}

U kunt een nieuwe omslag tot stand brengen door een verzoek van de POST aan het `/folder` eindpunt te richten en het omslagtype te specificeren.

**API formaat**

```http
POST /folders/{FOLDER_TYPE}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Het type objecten dat zich in de map bevindt. Tot de ondersteunde waarden behoren `segment` en `dataset` . |

**Verzoek**

+++Een voorbeeldverzoek om een nieuwe map te maken.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folders/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de map die u wilt maken. |
| `parentId` | De id van de bovenliggende map. |

+++

**Reactie**

Een succesvol antwoord retourneert HTTP-status 200 met details van de nieuwe map.

+++Een voorbeeldreactie die details van uw onlangs gecreeerde omslag bevat.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De id van de nieuwe map. |
| `createdBy` | De id van de gebruiker die de map heeft gemaakt. |
| `createdAt` | De tijdstempel van wanneer de map is gemaakt. |
| `modifiedBy` | De id van de gebruiker die de map als laatste heeft gewijzigd. |
| `modifiedAt` | De tijdstempel van wanneer de map voor het laatst is bijgewerkt. |

+++

## Een specifieke map ophalen {#get}

U kunt een specifieke omslag terugwinnen die tot uw organisatie behoort door een verzoek van de GET tot het `/folder` eindpunt te richten en het omslagtype en identiteitskaart van de omslag te specificeren.

**API formaat**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Het type objecten dat zich in de map bevindt. Tot de ondersteunde waarden behoren `segment` en `dataset` . |
| `{FOLDER_ID}` | De id van de map die u ophaalt. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke map op te halen

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met details van de gevraagde map.

+++A voorbeeldreactie die details van de gevraagde omslag bevat.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De id van de aangevraagde map. |
| `name` | De naam van de aangevraagde map. |
| `parentId` | De id van de bovenliggende map. |
| `createdBy` | De id van de gebruiker die de map heeft gemaakt. |
| `createdAt` | De tijdstempel van wanneer de map is gemaakt. |
| `modifiedBy` | De id van de gebruiker die de map voor het laatst heeft bijgewerkt. |
| `modifiedAt` | De tijdstempel van wanneer de map voor het laatst is bijgewerkt. |
| `status` | De status van de aangevraagde map. Tot de ondersteunde waarden behoren `IN_USE` en `ARCHIVED` . |

+++

## Een opgegeven map valideren {#validate}

U kunt valideren of een map objecten kan bevatten door een GET-aanvraag in te dienen bij het `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` -eindpunt en zowel het maptype als de id op te geven.

**API formaat**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Het type objecten dat zich in de map bevindt. Tot de ondersteunde waarden behoren `segment` en `dataset` . |
| `{FOLDER_ID}` | De id van de map die u valideert. |

**Verzoek**

+++A voorbeeldverzoek om een specifieke map te valideren

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde status retourneert HTTP status 200 met details over de map die u valideert.

+++A voorbeeldreactie bevat details van de gevalideerde map

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## Een specifieke map bijwerken {#update}

U kunt de details van een specifieke omslag bijwerken die tot uw organisatie behoort door een verzoek van de PATCH aan het `/folder` eindpunt te richten en het omslagtype en identiteitskaart van de omslag te specificeren.

**API formaat**

```http
PATCH /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Het type objecten dat zich in de map bevindt. Tot de ondersteunde waarden behoren `segment` en `dataset` . |
| `{FOLDER_ID}` | De id van de map die u bijwerkt. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke map bij te werken

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP-status 200 met informatie over de nieuwe map.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## Een specifieke map verwijderen {#delete}

U kunt een specifieke map die tot uw organisatie behoort, verwijderen door een DELETE-aanvraag in te dienen bij de `/folder` en het maptype en de map-id op te geven.

***API formaat**

```http
DELETE /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Het type objecten dat zich in de map bevindt. Tot de ondersteunde waarden behoren `segment` en `dataset` . |
| `{FOLDER_ID}` | De id van de map die u verwijdert. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke map te verwijderen

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met een berichttekst waarin u wordt geïnformeerd over de verwijdering van de map.

```json
{
    "message": "delete request accepted successfully"
}
```

## Volgende stappen

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u mappen kunt maken, beheren en verwijderen met de Adobe Experience Platform API.
