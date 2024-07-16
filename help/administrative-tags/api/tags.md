---
title: Eindpunt van Unified Tags
description: Leer hoe u tagcategorieën en -tags kunt maken, bijwerken, beheren en verwijderen met de Adobe Experience Platform API's.
role: Developer
exl-id: 6687d1da-a5e4-435a-9f99-1b0f9ac98088
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 1%

---

# Het eindpunt van Unified Labels

>[!IMPORTANT]
>
>De eindpunt-URL voor deze set eindpunten is `https://experience.adobe.io` .

Tags zijn een mogelijkheid waarmee u metagegevenstaxonomieën kunt beheren en bedrijfsobjecten kunt classificeren voor een eenvoudigere detectie en categorisering. Vervolgens kunt u deze tags in andere groepen ordenen door ze aan de categorieën tags toe te voegen.

Deze handleiding bevat informatie die u helpt meer inzicht te krijgen in tags en tagcategorieën en voorbeelden van API-aanroepen voor het uitvoeren van basishandelingen met behulp van de API.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de Adobe Experience Platform API&#39;s. Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen

### Woordenlijst

De volgende verklarende woordenlijst benadrukt het verschil tussen a **markering** en a **markeringscategorie**.

- **Markering**: Een markering staat u toe om de meta-gegevenstaxonomie voor bedrijfsvoorwerpen te beheren, toestaand u om deze voorwerpen voor gemakkelijkere ontdekking en categorisering te classificeren.
   - **Niet gecategoriseerde markering**: Een niet gecategoriseerde markering is een markering die niet tot een markeringscategorie behoort. Door gebrek, zullen de gecreeerde markeringen uncategorized.
- **categorie van de Markering**: Een markeringscategorie staat u toe om uw markeringen in zinvolle reeksen te groeperen, toestaand u om meer context aan het doel van de markering te verstrekken.

## Een lijst met tagcategorieën ophalen {#get-tag-categories}

U kunt een lijst ophalen met tagcategorieën die tot uw organisatie behoren door een aanvraag voor een GET in te dienen bij het eindpunt van `/tagCategory` .

**API formaat**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

De volgende optionele queryparameters kunnen worden gebruikt bij het ophalen van tagcategorieën.

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `start` | De locatie waar de lijst met resultaten begint. U kunt dit gebruiken om de beginindex voor paginering van resultaten aan te geven. | `start=a` |
| `limit` | Het maximumaantal tagcategorieën dat u per pagina wilt ophalen. | `limit=20` |
| `property` | Het kenmerk waarop u wilt filteren bij het ophalen van tagcategorieën. Tot de ondersteunde waarden behoren: &lt;ul≥<li>`name`: De naam van de tagcategorie.</li></ul> | `property=name==category` |
| `sortBy` | De volgorde waarin de tagcategorieën worden gesorteerd. Tot de ondersteunde waarden behoren `name` , `createdAt` en `modifiedAt` . | `sortBy=name` |
| `sortOrder` | De richting waarin de tagcategorieën worden gesorteerd. Tot de ondersteunde waarden behoren `asc` en `desc` . | `sortOrder=asc` |

**Verzoek**

+++Een voorbeeldverzoek om alle tagcategorieën in uw organisatie weer te geven

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van alle tagcategorieën voor uw organisatie.

+++A voorbeeldreactie die een lijst van alle markeringscategorieën in uw organisatie bevat.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## Een nieuwe tagcategorie maken {#create-tag-category}

>[!IMPORTANT]
>
>Alleen de systeembeheerder en de productbeheerder kunnen deze API-aanroep gebruiken.

U kunt een nieuwe tagcategorie maken door een aanvraag voor een POST in te dienen bij het eindpunt van `/tagCategory` .

**API formaat**

```http
POST /tagCategory
```

**Verzoek**

+++Een voorbeeldverzoek om een nieuwe tagcategorie te maken.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de tagcategorie die u wilt maken. |
| `description` | Een beschrijving van de tagcategorie die u wilt maken. |

+++

**Reactie**

Een voorbeeldreactie retourneert HTTP-status 200 met details van de nieuwe tagcategorie.

+++Een voorbeeldreactie met details van de zojuist gemaakte tagcategorie.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Een specifieke tagcategorie ophalen {#get-tag-category}

U kunt een specifieke tagcategorie ophalen die tot uw organisatie behoort door een GET-aanvraag in te dienen bij het eindpunt van `/tagCategory` en de id van de tagcategorie op te geven.

**API formaat**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | De id van de tagcategorie die u ophaalt. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke tagcategorie op te halen

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met details van de opgegeven tagcategorie.

+++A voorbeeldreactie die details van de gespecificeerde markeringscategorie bevat.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De id van de gewenste tagcategorie. |
| `name` | De naam van de gewenste tagcategorie. |
| `description` | De beschrijving van de gewenste tagcategorie. |
| `createdBy` | De id van de gebruiker die de tagcategorie heeft gemaakt. |
| `createdAt` | De tijdstempel van wanneer de tagcategorie is gemaakt. |
| `modifiedBy` | De id van de gebruiker die de tagcategorie voor het laatst heeft bijgewerkt. |
| `modifiedAt` | De tijdstempel van wanneer de tagcategorie voor het laatst is bijgewerkt. |
| `tagCount` | Het aantal tags dat bij de tagcategorie hoort. |

+++

## Een specifieke tagcategorie bijwerken {#update-tag-category}

>[!IMPORTANT]
>
>Alleen de systeembeheerder en de productbeheerder kunnen deze API-aanroep gebruiken.

U kunt details van een specifieke markeringscategorie bijwerken die tot uw organisatie behoort door een verzoek van de PATCH aan het `/tagCategory` eindpunt en het specificeren van identiteitskaart van de markeringscategorie te richten.

**API formaat**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | De id van de tagcategorie die u ophaalt. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke tagcategorie bij te werken

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `op` | De bewerking die is voltooid. Als u een specifieke tagcategorie wilt bijwerken, stelt u deze waarde in op `replace` . |
| `path` | Het pad van het veld dat wordt bijgewerkt. Tot de ondersteunde waarden behoren `name` en `description` . |
| `value` | De bijgewerkte waarde van het veld dat u wilt bijwerken. |
| `from` | De oorspronkelijke waarde van het veld dat u wilt bijwerken. |

+++

**Reactie**

Een geslaagde reactie HTTP status 200 met informatie over uw onlangs bijgewerkte markeringscategorie.

+++A voorbeeldreactie met details van uw onlangs bijgewerkte tagcategorie.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Een specifieke tagcategorie verwijderen {#delete-tag-category}

>[!IMPORTANT]
>
>Alleen de systeembeheerder en de productbeheerder kunnen deze API-aanroep gebruiken.

U kunt een specifieke tagcategorie verwijderen die tot uw organisatie behoort door een DELETE-aanvraag in te dienen bij het `/tagCategory` -eindpunt en de id van de tagcategorie op te geven.

**API formaat**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | De id van de tagcategorie die u ophaalt. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke tagcategorie te verwijderen

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege reactie.

## Een lijst met tags ophalen {#get-tags}

U kunt een lijst ophalen met tags die bij uw organisatie horen door een aanvraag voor een GET in te dienen bij het `/tags` -eindpunt en de id van de tagcategorie.

**API formaat**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

De volgende optionele queryparameters kunnen worden gebruikt bij het ophalen van tags.

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `start` | De locatie waar de lijst met resultaten begint. U kunt dit gebruiken om de beginindex voor paginering van resultaten aan te geven. | `start=a` |
| `limit` | Het maximumaantal tags dat u per pagina wilt ophalen. | `limit=20` |
| `property` | Het kenmerk waarop u wilt filteren bij het ophalen van tags. Tot de ondersteunde waarden behoren:<ul><li>`name`: De naam van de tag.</li><li>`archived`: Of de tags gearchiveerd of niet gearchiveerd zijn. U kunt deze waarde instellen op `true` of `false` .</li><li>`tagCategoryId`: De id van de tagcategorie waartoe de tag behoort.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | De volgorde waarin de tags worden gesorteerd. Tot de ondersteunde waarden behoren `name` , `createdAt` en `modifiedAt` . | `sortBy=name` |
| `sortOrder` | De richting waarin de tagcategorieën worden gesorteerd. Tot de ondersteunde waarden behoren `asc` en `desc` . | `sortOrder=asc` |


**Verzoek**

+++Een voorbeeldverzoek om alle tags op te halen die tot een bepaalde tagcategorie behoren

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met details van de tags die tot die tagcategorie behoren.

+++ Een voorbeeldreactie die details van de gevraagde labels bevat.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## Een nieuwe tag maken {#create-tag}

>[!IMPORTANT]
>
>Alleen de systeembeheerder en de productbeheerder kunnen deze API-aanroep gebruiken om een nieuwe tag te maken in een opgegeven tagcategorie.
>
>Als u een niet-gecategoriseerde markering creeert, hebt u **** geen beheerdertoestemmingen nodig.

U kunt een nieuwe tag maken door een POST aan te vragen bij het eindpunt van `/tags` .

**API formaat**

```http
POST /tags
```

**Verzoek**

+++Een voorbeeldverzoek om een nieuwe tag te maken.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | **Vereiste**. De naam van de tag die u wilt maken. |
| `tagCategoryId` | *Facultatief*. De id van de tagcategorie waartoe de tag moet behoren. Als u deze optie niet opgeeft, wordt de tag gemaakt als onderdeel van de categorie Niet gecategoriseerd. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 met details van de nieuwe tag.

+++Een voorbeeldreactie met details van de nieuwe tag.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `name` | De naam van de nieuwe tag. |
| `id` | De id van de nieuwe tag. |
| `org` | De id van de organisatie waartoe de tag behoort. |
| `createdAt` | De tijdstempel van wanneer de tag is gemaakt. |
| `createdBy` | De id van de gebruiker die de tag heeft gemaakt. |
| `modifiedAt` | De tijdstempel van wanneer de tag voor het laatst is bijgewerkt. |
| `modifiedBy` | De id van de gebruiker die de tag het laatst heeft bijgewerkt. |
| `tagCategoryId` | De id van de tagcategorie waartoe de tag behoort. |
| `tagCategoryName` | De naam van de tagcategorie waartoe de tag behoort. |

+++

## Een specifieke tag ophalen {#get-tag}

U kunt een specifieke tag ophalen die tot uw organisatie behoort door een aanvraag voor een GET in te dienen bij het `/tags` -eindpunt en de id op te geven van de tag die u wilt ophalen.

**API formaat**

```http
GET /tags/{TAG_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TAG_ID}` | De id van de tag die u ophaalt. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke tag op te halen

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met details van de opgegeven tag.

+++A monsterreactie die details van de gespecificeerde markering bevat.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `name` | De naam van de tag die u hebt opgehaald. |
| `id` | De id van de tag die u hebt opgehaald. |
| `org` | De id van de organisatie waartoe de tag behoort. |
| `createdAt` | De tijdstempel van wanneer de tag is gemaakt. |
| `createdBy` | De id van de gebruiker die de tag heeft gemaakt. |
| `modifiedAt` | De tijdstempel van wanneer de tag voor het laatst is bijgewerkt. |
| `modifiedBy` | De id van de gebruiker die de tag het laatst heeft bijgewerkt. |
| `tagCategoryId` | De id van de tagcategorie waartoe de tag behoort. |
| `tagCategoryName` | De naam van de tagcategorie waartoe de tag behoort. |
| `archived` | De archiveringsstatus van de tag. Indien ingesteld op `true` , betekent dit dat de tag wordt gearchiveerd. |

+++

## Tags valideren {#validate-tags}

U kunt controleren of er tags bestaan door een aanvraag voor een POST in te dienen bij het eindpunt van `/tags/validate` .

**API formaat**

```http
POST /tags/validate
```

**Verzoek**

+++Een voorbeeldverzoek om de opgegeven tag-id&#39;s te valideren.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `ids` | Een array die een lijst bevat met tag-id&#39;s die u wilt valideren. |
| `entity` | De entiteit die de validatie aanvraagt. U kunt de `{API_KEY}` -waarde voor deze parameter gebruiken. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met informatie over welke tags geldig en ongeldig zijn.

+++A voorbeeldreactie met geldige en ongeldige codes.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `invalidTags` | Een array die een lijst met ongeldige tag-id&#39;s bevat. |
| `validTags` | Een array die een lijst met geldige tag-id&#39;s bevat. |

+++

## Een specifieke tag bijwerken {#update-tag}

U kunt een opgegeven tag bijwerken door een PATCH-aanvraag in te dienen bij het `/tags` -eindpunt en de id op te geven van de tag die u wilt bijwerken.

**API formaat**

```http
PATCH /tags/{TAG_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TAG_ID}` | De id van de tag die u bijwerkt. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke tag bij te werken

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `op` | De bewerking die moet worden uitgevoerd. In dit geval wordt deze altijd ingesteld op `replace` . |
| `path` | Het pad van het veld dat wordt bijgewerkt. Tot de ondersteunde waarden behoren `name` , `archived` en `tagCategoryId` . |
| `value` | De bijgewerkte waarde van het veld dat u wilt bijwerken. |
| `from` | De oorspronkelijke waarde van het veld dat u wilt bijwerken. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 200 met details van de zojuist bijgewerkte tag.

+++A voorbeeldreactie die details van de bijgewerkte markering bevat.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## Een specifieke tag verwijderen {#delete-tag}

>[!IMPORTANT]
>
>Alleen de systeembeheerder en de productbeheerder kunnen deze API-aanroep gebruiken.
>
>Bovendien, kan de markering **niet** met om het even welke bedrijfsvoorwerpen worden geassocieerd en **moet** worden gearchiveerd alvorens u de markering kunt schrappen. U kunt de markering archiveren door het [ eindpunt van de updatemarkering ](#update-tag) te gebruiken.

U kunt een specifieke tag verwijderen door een DELETE-tag op te geven aan het eindpunt van `/tags` en de id op te geven van het label dat u wilt verwijderen.

**API formaat**

```http
DELETE /tags/{TAG_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TAG_ID}` | De id van de tag die u verwijdert. |

**Verzoek**

+++Een voorbeeldverzoek om een specifieke tag te verwijderen

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege reactie.

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u meer inzicht in het maken, beheren en verwijderen van tags en tagcategorieën met behulp van de Adobe Experience Platform API&#39;s. Voor meer informatie bij het beheren van markeringen die UI gebruiken, te lezen gelieve [ het leiden de gids van markeringen ](../ui/managing-tags.md). Voor meer informatie bij het beheren van markeringscategorieën die UI gebruiken, te lezen gelieve de [ gids van de markeringscategorieën ](../ui/tags-categories.md).
