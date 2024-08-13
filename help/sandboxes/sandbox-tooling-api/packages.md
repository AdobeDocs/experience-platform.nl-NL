---
title: API-eindpunt voor sandbox Tooling Packages
description: Het /packages eindpunt in Sandbox Tooling API staat u toe om pakketten in Adobe Experience Platform programmatically te beheren.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: f81e15ccfd89e2d0cb450f596743341264187f52
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 1%

---

# Pakketeindpunt

Met gereedschappen voor sandboxen kunt u verschillende artefacten selecteren (ook wel objecten genoemd) en deze exporteren naar een pakket. Een pakket kan uit één enkel artefact of veelvoudige artefacten (zoals datasets of schema&#39;s) bestaan. Artefacten die deel uitmaken van een pakket, moeten afkomstig zijn uit dezelfde sandbox.

Met het `/packages` -eindpunt in de API voor gereedheid voor sandboxen kunt u programmatisch pakketten in uw organisatie beheren, waaronder het publiceren van een pakket en het importeren van een pakket naar een sandbox.

## Een pakket maken {#create}

U kunt een multi-artefactenpakket tot stand brengen, door een verzoek van de POST aan het `/packages` eindpunt terwijl het verstrekken van waarden voor de naam en het pakkettype van uw pakket.

**API formaat**

```http
POST /packages/
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `name` | De naam van het pakket. | String | Ja |
| `description` | Een beschrijving voor meer informatie over het pakket. | String | Nee |
| `packageType` | Het pakkettype is **GEDEELTELIJK** om erop te wijzen u specifieke artefacten in een pakket omvat. | String | JA |
| `sourceSandbox` | De bronsandbox van het pakket. | String | Nee |
| `expiry` | Het tijdstempel dat de vervaldatum voor het pakket definieert. De standaardwaarde is 90 dagen vanaf de aanmaakdatum. Het veld voor het verstrijken van de reactie is een tijdperk in UTC-tijd. | Tekenreeks (UTC-tijdstempelindeling) | Nee |
| `artifacts` | Een lijst met artefacten die naar het pakket moeten worden geëxporteerd. De `artifacts` waarde zou **ongeldig** of **leeg** moeten zijn, wanneer `packageType` `FULL` is. | Array | Nee |

**Reactie**

Een geslaagde reactie retourneert het zojuist gemaakte pakket. De reactie bevat de overeenkomende pakket-id en informatie over de status, de vervaldatum en de lijst met artefacten.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Een pakket bijwerken {#update}

U kunt een pakket bijwerken door een PUT aan het `/packages` eindpunt te vragen.

### Artefacten toevoegen aan een pakket {#add-artifacts}

Om artefacten aan een pakket toe te voegen, moet u `id` verstrekken en **omvatten VOEGT** voor `action` toe.

**API formaat**

```http
PUT /packages/
```

**Verzoek**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| Eigenschap | Beschrijving | Type | Verplicht |
| --- | --- | --- | --- |
| `id` | De id van het pakket dat moet worden bijgewerkt. | String | Ja |
| `action` | Om artefacten in het pakket toe te voegen, zou de actiewaarde **moeten zijn ADD**. Deze actie wordt gesteund voor slechts **GEDEELTELIJKE** pakkettypes. | String | Ja |
| `artifacts` | Een lijst met artefacten die in het pakket moeten worden toegevoegd. Er zou geen verandering in het pakket zijn als de lijst **ongeldig** of **leeg** is. Artefacten worden gedupliceerd voordat ze aan het pakket worden toegevoegd. Zie de onderstaande tabel voor een volledige lijst met ondersteunde artefacten. | Array | Nee |
| `expiry` | Het tijdstempel dat de vervaldatum voor het pakket definieert. De standaardwaarde is 90 dagen vanaf het moment dat de PUT-API wordt aangeroepen als de vervaldatum niet is opgegeven in de payload. Het veld voor het verstrijken van de reactie is een tijdperk in UTC-tijd. | Tekenreeks (UTC-tijdstempelindeling) | Nee |

De volgende artefacttypen worden momenteel ondersteund.

| Artefact | Platform | Object | Partiële stroom | Volledige sandbox |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | Journeys | Ja | Nee |
| `ID_NAMESPACE` | Klantgegevensplatform | Identiteiten | Ja | Ja |
| `REGISTRY_DATATYPE` | Klantgegevensplatform | Gegevenstype | Ja | Ja |
| `REGISTRY_CLASS` | Klantgegevensplatform | Klasse | Ja | Ja |
| `REGISTRY_MIXIN` | Klantgegevensplatform | Veldgroep | Ja | Ja |
| `REGISTRY_SCHEMA` | Klantgegevensplatform | Schema&#39;s | Ja | Ja |
| `CATALOG_DATASET` | Klantgegevensplatform | Gegevenssets | Ja | Ja |
| `DULE_CONSENT_POLICY` | Klantgegevensplatform | Beleid inzake instemming en bestuur | Ja | Ja |
| `PROFILE_SEGMENT` | Klantgegevensplatform | Doelgroepen | Ja | Ja |
| `FLOW` | Klantgegevensplatform | Bronnen, gegevensstroom | Ja | Ja |

**Reactie**

Een geslaagde reactie retourneert het bijgewerkte pakket. De reactie bevat de overeenkomende pakket-id en informatie over de status, de vervaldatum en de lijst met artefacten.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Artefacten uit een pakket verwijderen {#delete-artifacts}

Om artefacten van een pakket te schrappen, moet u `id` verstrekken en **DELETE** voor `action` omvatten.


**API formaat**

```http
PUT /packages/
```

**Verzoek**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| Eigenschap | Beschrijving | Type | Verplicht |
| --- | --- | --- | --- |
| `id` | De id van het pakket dat moet worden bijgewerkt. | String | Ja |
| `action` | Om artefacten van een pakket te schrappen, zou de actiewaarde **DELETE** moeten zijn. Deze actie wordt gesteund voor slechts **GEDEELTELIJKE** pakkettypes. | String | Ja |
| `artifacts` | Een lijst met artefacten die uit het pakket moeten worden verwijderd. Er zou geen verandering in het pakket zijn als de lijst **ongeldig** of **leeg** is. | Array | Nee |

**Reactie**

Een geslaagde reactie retourneert het bijgewerkte pakket. De reactie bevat de overeenkomende pakket-id en informatie over de status, de vervaldatum en de lijst met artefacten.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Metagegevensvelden in een pakket bijwerken {#update-metadata}

>[!NOTE]
>
>De **actie van de UPDATE** wordt gebruikt om de gebieden van pakketmeta-gegevens van het pakket bij te werken en **kan** niet worden gebruikt om artefacten aan een pakket toe te voegen/te schrappen.

Om de meta-gegevensgebieden in een pakket bij te werken, moet u `id` verstrekken en **UPDATE** voor `action` omvatten.

**API formaat**

```http
PUT /packages/
```

**Verzoek**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| Eigenschap | Beschrijving | Type | Verplicht |
| --- | --- | --- | --- |
| `id` | De id van het pakket dat moet worden bijgewerkt. | String | Ja |
| `action` | Om de meta-gegevensgebieden in een pakket bij te werken, zou de actiewaarde **UPDATE** moeten zijn. Deze actie wordt gesteund voor slechts **GEDEELTELIJKE** pakkettypes. | String | Ja |
| `name` | De bijgewerkte naam van het pakket. Dubbele pakketnamen zijn niet toegestaan. | Array | Ja |
| `sourceSandbox` | Source-sandbox moet tot dezelfde organisatie behoren als die is opgegeven in de header van de aanvraag. | String | Ja |

**Reactie**

Een geslaagde reactie retourneert het bijgewerkte pakket. De reactie bevat de overeenkomende pakket-id en informatie over de beschrijving, status, vervaldatum en lijst met artefacten.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Een pakket verwijderen {#delete}

Als u een pakket wilt verwijderen, vraagt u een DELETE-aanvraag naar het `/packages` -eindpunt en geeft u de id op van het pakket dat u wilt verwijderen.

**API formaat**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {PACKAGE_ID} | De id van het pakket dat u wilt verwijderen. |

**Verzoek**

Met de volgende aanvraag wordt het pakket met de id {PACKAGE_ID} verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Reactie**

Een geslaagde reactie retourneert een reden die aangeeft dat de pakket-id is verwijderd.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publish een pakket {#publish}

Als u het importeren van een pakket in een sandbox wilt inschakelen, moet u het publiceren. Breng een verzoek van de GET tot het `/packages` eindpunt terwijl het specificeren van identiteitskaart van het pakket u wilt publiceren.

**API formaat**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parameter | Beschrijving |
| --- | --- |
| {PACKAGE_ID} | De id van het pakket dat u wilt publiceren. |

**Verzoek**

In het volgende verzoek wordt het pakket met de id {PACKAGE_ID} gepubliceerd.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Eigenschap | Beschrijving | Type | Verplicht |
| --- | --- | --- | --- |
| `expiryPeriod` | Deze door de gebruiker opgegeven tijdsperiode definieert de vervaldatum van het pakket (in dagen) vanaf het moment dat het pakket werd gepubliceerd. Deze waarde mag niet negatief zijn.<br> Als er geen waarde is opgegeven, wordt de standaardwaarde berekend als 90 (dagen) vanaf de publicatiedatum. | Geheel | Nee |

**Reactie**

Een geslaagde reactie retourneert het gepubliceerde pakket.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Een pakket opzoeken {#look-up-package}

U kunt een afzonderlijk pakket opzoeken door een verzoek van de GET te richten aan het `/packages` eindpunt dat overeenkomstige identiteitskaart van het pakket in de verzoekweg omvat.

**API formaat**

```http
GET /packages/{PACKAGE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {PACKAGE_ID} | De id van het pakket dat u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt informatie voor {PACKAGE_ID} opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Reactie**

Een geslaagde reactie retourneert details voor de id van het gevraagde pakket. Het antwoord bevat de naam, beschrijving, publicatiedatum en vervaldatum, de bronsandbox van het pakket en een lijst met artefacten.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## Lijstpakketten {#list-packages}

U kunt van alle pakketten in uw organisatie een lijst maken, door een verzoek van de GET tot het `/packages` eindpunt te richten.

**API formaat**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| {QUERY_PARAMS} | Optionele queryparameters om resultaten te filteren op. Zie de sectie over [ vraagparameters ](./appendix.md) voor meer informatie. |

**Verzoek**

Met de volgende aanvraag wordt informatie over de pakketten opgehaald op basis van de {QUERY_PARAMS} .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een geslaagde reactie retourneert een lijst met pakketten die bij uw organisatie horen, inclusief details zoals naam, status, vervaldatum en lijst met artefacten.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## Een pakket importeren {#import}

Dit eindpunt wordt gebruikt om de conflicterende objecten in de opgegeven doelsandbox op te halen. Conflicterende objecten vertegenwoordigen vergelijkbare objecten die al aanwezig zijn in de doelsandbox.

**API formaat**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| Parameter | Beschrijving |
| --- | --- |
| {PACKAGE_ID} | De id van het pakket dat u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt de {PACKAGE_ID} geïmporteerd.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Conflicten worden geretourneerd in de reactie. In het antwoord wordt het oorspronkelijke pakket plus het fragment `alternatives` weergegeven als een array die op volgorde is geordend.

Reactie weergeven+++

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## Importeren verzenden {#submit-import}

>[!NOTE]
>
>Het is inherent aan conflictoplossing dat het alternatieve artefact al bestaat in de doelsandbox.

U kunt een importbewerking voor een pakket verzenden nadat u conflicten hebt gecontroleerd en vervangende items hebt opgegeven door een aanvraag voor POST in te dienen bij het `/packages` -eindpunt. Het resultaat wordt opgegeven als een payload, die de importtaak start voor de doelsandbox zoals opgegeven in de payload.

Payload accepteert ook de door de gebruiker opgegeven taaknaam en beschrijving voor de importtaak. Als de door de gebruiker opgegeven naam en beschrijving niet beschikbaar zijn, worden de pakketnaam en beschrijving gebruikt voor de naam en beschrijving van de taak.

**API formaat**

```http
POST /packages/import
```

**Verzoek**

Met de volgende aanvraag worden pakketten opgehaald die moeten worden geïmporteerd. De nuttige lading is een kaart van substituties waar, als een ingang bestaat, de sleutel `artifactId` door het pakket wordt verstrekt, en het alternatief is de waarde. Als de kaart of de nuttige lading **** leeg is, worden geen substituties uitgevoerd.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| Eigenschap | Beschrijving | Type | Verplicht |
| --- | --- | --- | --- |
| `alternatives` | `alternatives` geeft de toewijzing van bronsandboxartefacten aan de bestaande doelsandboxartefacten aan. Omdat deze elementen al aanwezig zijn, voorkomt de importtaak dat deze artefacten in de doelsandbox worden gemaakt. | String | Nee |

**Reactie**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Alle afhankelijke objecten weergeven {#dependent-objects}

Maak een lijst van alle afhankelijke voorwerpen voor de uitgevoerde voorwerpen in een pakket door een verzoek van de POST aan het `/packages` eindpunt terwijl het specificeren van identiteitskaart van het pakket.

**API formaat**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parameter | Beschrijving |
| --- | --- |
| {PACKAGE_ID} | De id van het pakket. |

**Verzoek**

In de volgende aanvraag worden alle afhankelijke objecten voor de {PACKAGE_ID} weergegeven.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**Reactie**

Een geslaagde reactie retourneert een lijst met onderliggende objecten voor de objecten.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## Op rollen gebaseerde machtigingen controleren om alle pakketartefacten te importeren {#role-based-permissions}

U kunt controleren of u machtigingen hebt om pakketartefacten te importeren door een GET-aanvraag in te dienen bij het eindpunt `/packages` terwijl de id van het pakket en de naam van de doelsandbox wordt opgegeven.

**API formaat**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parameter | Beschrijving |
| --- | --- |
| {PACKAGE_ID} | De id van het pakket dat u wilt importeren. |

**Verzoek**

Met de volgende aanvraag worden uw machtigingen voor de {PACKAGE_ID} en sandbox gecontroleerd.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvol antwoord keert middeltoestemmingen voor de doelzandbak, met inbegrip van een lijst van vereiste toestemmingen, ontbrekende toestemmingen, type van artefact, en een besluit terug over of de verwezenlijking wordt toegestaan.

Reactie weergeven+++

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## Uitvoer-/importtaken weergeven {#list-jobs}

U kunt huidige export-/importtaken weergeven door een GET-aanvraag in te dienen bij het `/packages` -eindpunt.

**API formaat**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| {QUERY_PARAMS} | Optionele queryparameters om resultaten te filteren op. Zie de sectie over [ vraagparameters ](./appendix.md) voor meer informatie. |

**Verzoek**

In het volgende verzoek worden alle taken weergegeven die met succes zijn geïmporteerd.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Reactie**

Met een geslaagde reactie worden alle geslaagde importtaken geretourneerd.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```
