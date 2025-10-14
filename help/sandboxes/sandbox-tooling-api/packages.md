---
title: API-eindpunt voor sandbox Tooling Packages
description: Het /packages eindpunt in Sandbox Tooling API staat u toe om pakketten in Adobe Experience Platform programmatically te beheren.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 1d8c29178927c7ee3aceb0b68f97baeaefd9f695
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 1%

---

# Pakketeindpunt

Met gereedschappen voor sandboxen kunt u verschillende artefacten selecteren (ook wel objecten genoemd) en deze exporteren naar een pakket. Een pakket kan uit één enkel artefact of veelvoudige artefacten (zoals datasets of schema&#39;s) bestaan. Artefacten die deel uitmaken van een pakket, moeten afkomstig zijn uit dezelfde sandbox.

Met het `/packages` -eindpunt in de API voor gereedheid voor sandboxen kunt u programmatisch pakketten in uw organisatie beheren, waaronder het publiceren van een pakket en het importeren van een pakket naar een sandbox.

## Een pakket maken {#create}

U kunt een pakket met meerdere artefacten maken door een POST-aanvraag in te dienen bij het eindpunt van `/packages` en tegelijkertijd waarden op te geven voor de naam en het pakkettype van uw pakket.

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
| `sourceSandbox` | De bronsandbox van het pakket. | Object | Nee |
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

Gebruik het eindpunt `/packages` in de API voor gereedschappen in de sandbox om een pakket bij te werken.

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
| `expiry` | Het tijdstempel dat de vervaldatum voor het pakket definieert. De standaardwaarde is 90 dagen vanaf het moment dat de PUT API wordt aangeroepen als de vervaldatum niet is opgegeven in de payload. Het veld voor het verstrijken van de reactie is een tijdperk in UTC-tijd. | Tekenreeks (UTC-tijdstempelindeling) | Nee |

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
| `sourceSandbox` | Source-sandbox moet tot dezelfde organisatie behoren als die is opgegeven in de header van de aanvraag. | Object | Ja |

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

Als u een pakket wilt verwijderen, vraagt u DELETE het `/packages` -eindpunt aan en geeft u de id op van het pakket dat u wilt verwijderen.

**API formaat**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{PACKAGE_ID}` | De id van het pakket dat u wilt verwijderen. |

**Verzoek**

Met de volgende aanvraag wordt het pakket met de id {PACKAGE_ID} verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een geslaagde reactie retourneert een reden die aangeeft dat de pakket-id is verwijderd.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Een pakket publiceren {#publish}

Als u het importeren van een pakket in een sandbox wilt inschakelen, moet u het publiceren. Voer een GET-aanvraag in bij het eindpunt van `/packages` terwijl u de id opgeeft van het pakket dat u wilt publiceren.

**API formaat**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parameter | Beschrijving |
| --- | --- |
| `{PACKAGE_ID}` | De id van het pakket dat u wilt publiceren. |

**Verzoek**

In het volgende verzoek wordt het pakket met de id {PACKAGE_ID} gepubliceerd.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Een pakket opzoeken {#look-up-package}

U kunt een afzonderlijk pakket opzoeken door een GET-aanvraag in te dienen bij het `/packages` -eindpunt dat de overeenkomende id van het pakket bevat in het aanvraagpad.

**API formaat**

```http
GET /packages/{PACKAGE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{PACKAGE_ID}` | De id van het pakket dat u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt informatie voor {PACKAGE_ID} opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

U kunt alle pakketten in uw organisatie weergeven door een GET-aanvraag in te dienen bij het `/packages` -eindpunt.

**API formaat**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie de sectie over [&#x200B; vraagparameters &#x200B;](./appendix.md) voor meer informatie. |

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
| `{PACKAGE_ID}` | De id van het pakket dat u wilt opzoeken. |

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

+++reactie weergeven

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

U kunt een importbewerking voor een pakket verzenden nadat u conflicten hebt gecontroleerd en vervangende items hebt opgegeven door een POST-aanvraag in te dienen bij het `/packages` -eindpunt. Het resultaat wordt opgegeven als een payload, die de importtaak start voor de doelsandbox zoals opgegeven in de payload.

Payload accepteert ook de door de gebruiker opgegeven taaknaam en beschrijving voor de importtaak. Als de door de gebruiker opgegeven naam en beschrijving niet beschikbaar zijn, worden de pakketnaam en beschrijving gebruikt voor de naam en beschrijving van de taak.

**API formaat**

```http
POST /packages/import
```

**Verzoek**

Met de volgende aanvraag worden pakketten opgehaald die moeten worden geïmporteerd. De nuttige lading is een kaart van substituties waar, als een ingang bestaat, de sleutel `artifactId` door het pakket wordt verstrekt, en het alternatief is de waarde. Als de kaart of de nuttige lading **&#x200B;**&#x200B;leeg is, worden geen substituties uitgevoerd.

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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Alle afhankelijke objecten weergeven {#dependent-objects}

Maak een lijst van alle afhankelijke voorwerpen voor de uitgevoerde voorwerpen in een pakket door een POST- verzoek aan het `/packages` eindpunt te doen terwijl het specificeren van identiteitskaart van het pakket.

**API formaat**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parameter | Beschrijving |
| --- | --- |
| `{PACKAGE_ID}` | De id van het pakket. |

**Verzoek**

In de volgende aanvraag worden alle afhankelijke objecten voor de {PACKAGE_ID} weergegeven.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/children \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

U kunt controleren of u machtigingen hebt om pakketartefacten te importeren door een GET-aanvraag in te dienen bij het `/packages` -eindpunt terwijl de id van het pakket en de naam van de doelsandbox wordt opgegeven.

**API formaat**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parameter | Beschrijving |
| --- | --- |
| `{PACKAGE_ID}` | De id van het pakket dat u wilt importeren. |

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

+++reactie weergeven

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
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie de sectie over [&#x200B; vraagparameters &#x200B;](./appendix.md) voor meer informatie. |

**Verzoek**

In het volgende verzoek worden alle taken weergegeven die met succes zijn geïmporteerd.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

## Pakketten delen over organisaties {#org-linking}

Met het eindpunt `/handshake` in de API voor het bewerken van sandboxen kunt u met andere organisaties samenwerken om pakketten te delen.

### Een aanvraag voor delen verzenden {#send-request}

Verzend een verzoek naar een organisatie van de doelpartner voor het delen van goedkeuring door een POST- verzoek aan het `/handshake/bulkCreate` eindpunt te doen. Dit is vereist voordat u persoonlijke pakketten kunt delen.

**API formaat**

```http
POST /handshake/bulkCreate
```

**Verzoek**

Het volgende verzoek stelt in werking delend goedkeuring tussen een organisatie van de doelpartner en de bronorganisatie.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | Een lijst met doelorganisaties waarnaar een verzoek om delen moet worden verzonden. | Array | Ja |
| `sourceIMSDetails` | Details over de bronorganisatie. | Object | Ja |

**Reactie**

Een geslaagde reactie geeft details over uw aanvraag voor delen.

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKING_ID}"
        }
    },
    "failedRequests": {}
}
```

### Ontvangen aanvragen voor delen goedkeuren {#approve-requests}

Goedkeuren van verzoeken om delen van organisaties van doelpartners door een POST-verzoek in te dienen bij het `/handshake/action` eindpunt. Na goedkeuring, kunnen de organisaties van de bronpartner privé pakketten delen.

**API formaat**

```http
POST /handshake/action
```

**Verzoeken**

Het volgende verzoek keurt een aandeelverzoek van een organisatie van de doelpartner goed.

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `linkingID` | De id van het verzoek om delen waarop u reageert. | String | Ja |
| `status` | De actie die wordt ondernomen naar aanleiding van het verzoek om delen. Acceptabele waarden zijn `APPROVED` of `REJECTED` . | String | Ja |
| `reason` | De reden waarom de actie wordt ondernomen. | String | Ja |
| `targetIMSOrgDetails` | De details over de doelorganisatie waar de id waarde identiteitskaart van de doelorganisatie **&#x200B;**&#x200B;zou moeten zijn, zou de naamwaarde de 2&rbrace; NAAM van de doelorganisaties **moeten zijn, en de gebiedwaarde zou de doelorganisaties** REGIO **moeten zijn.** | Object | Ja |

**Reactie**

Een succesvolle reactie retourneert details met betrekking tot het goedgekeurde verzoek om delen.

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### Uitgaande/binnenkomende verzoeken voor delen weergeven {#outgoing-and-incoming-requests}

Maak een lijst van uitgaande en binnenkomende verzoeken van het aandeel door een GET- verzoek aan het `handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING` eindpunt te doen.

**API formaat**

```http
GET handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| Parameter | Geaccepteerde/standaardwaarden |
| --- | --- |
| `property` | Geeft de eigenschap aan waarop moet worden gefilterd, zoals status. Acceptabele waarden voor status zijn: `APPROVED`, `REJECTED` en `IN_PROGRESS` . |
| `start` | De standaardwaarde van start is `0` . |
| `limit` | De standaardwaarde van limit is `20` . |
| `orderBy` | Hiermee sorteert u records in oplopende of aflopende volgorde. |
| `requestType` | Accepteert `INCOMING` of `OUTGOING` . |

**Verzoek**

Het volgende verzoek keert een lijst van alle uitgaande en inkomende aandeelverzoeken terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Reactie**

Een succesvolle reactie keert een lijst van uitgaande en inkomende aandeelverzoeken en hun details terug.

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## Transferpakketten

Gebruik het eindpunt `/transfer` in de API voor gereedschappen in de sandbox om nieuwe aanvragen voor pakketdeling op te halen en te maken.

### Nieuwe aanvraag voor delen {#share-request}

Zoek het pakket van een gepubliceerde bronorganisatie en deel het met een doelorganisatie door een POST- verzoek aan het `/transfer` eindpunt te doen terwijl het verstrekken van pakketidentiteitskaart en identiteitskaart van de doelorganisatie.

**API formaat**

```http
POST /transfer
```

**Verzoek**

Het volgende verzoek haalt een bronorganisatiepakket op en deelt het met een doelorganisatie.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `packageId` | De id van het pakket dat u wilt delen. | String | Ja |
| `targets` | Een lijst met organisaties waarmee een pakket moet worden gemaakt. | Array | Ja |

**Reactie**

Een succesvol antwoord geeft details van het gevraagde pakket en zijn aandeelstatus terug.

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "requestType": "PRIVATE"
    }
]
```

### Aanvraag voor delen ophalen met id {#fetch-transfer-by-id}

Haal de details van een verzoek van het aandeel door een GET- verzoek aan het `/transfer/{TRANSFER_ID}` eindpunt te doen terwijl het verstrekken van identiteitskaart

**API formaat**

```http
GET /transfer/{TRANSFER_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{TRANSFER_ID}` | De id van de overdracht die u wilt ophalen. |

**Verzoek**

Met het volgende verzoek wordt een overdracht opgehaald met de id {TRANSFER_ID} .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Reactie**

Een succesantwoord retourneert details van een aandelenaanvraag.

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "requestType": "PRIVATE"
}
```

### Ophaallijst {#transfers-list}

Haal een lijst van overdrachtsverzoeken door een GET- verzoek aan het `/transfer/list?{QUERY_PARAMETERS}` eindpunt te doen, veranderend de vraagparameters zoals nodig.

**API formaat**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| Parameter | Geaccepteerde/standaardwaarden |
| --- | --- |
| `property` | Geeft de eigenschap aan waarop moet worden gefilterd, zoals status. Acceptabele waarden voor status zijn: `COMPLETED`, `PENDING`, `IN_PROGRESS`, `FAILED` . |
| `start` | De standaardwaarde van start is `0` . |
| `limit` | De standaardwaarde van limit is `20` . |
| `orderBy` | De volgorde accepteert alleen het veld `createdDate` . |

**Verzoek**

Het volgende verzoek haalt een lijst van overdrachtsverzoeken van de verstrekte onderzoeksparameters.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Reactie**

Een succesvolle reactie keert een lijst van alle overdrachtverzoeken van de verstrekte onderzoeksparameters terug.

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### Pakketbeschikbaarheid bijwerken van privé naar openbaar {#update-availability}

Verander een pakket van privé in openbaar door een GET- verzoek aan het `/packages/update` eindpunt te doen. Standaard wordt een pakket gemaakt met persoonlijke beschikbaarheid.

**API formaat**

```http
PUT `/packages/update`
```

**Verzoek**

Het volgende verzoek verandert een pakketbeschikbaarheid van privé in openbaar.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `id` | The id of the package to update. | String | Ja |
| `action` | Om het zicht aan openbaar bij te werken, zou de actiewaarde **UPDATE** moeten zijn. | String | Ja |
| `packageVisbility` | Om het zicht bij te werken, zou de packageVisibility waarde **PUBLIC** moeten zijn. | String | Ja |

**Reactie**

Een geslaagde reactie retourneert details over een pakket en de zichtbaarheid ervan.

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### Verzoek om een openbaar pakket te importeren {#pull-public-package}

Importeer een pakket van een bronorganisatie met openbare beschikbaarheid door een POST-verzoek in te dienen op het `/transfer/pullRequest` eindpunt.

**API formaat**

```http
POST /transfer/pullRequest
```

**Verzoek**

Met het volgende verzoek wordt een pakket geïmporteerd en wordt de beschikbaarheid ervan voor het publiek ingesteld.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `imsOrgId` | De id van de bronorganisatie van het pakket. | String | Ja |
| `packageId` | De id uit het te importeren pakket. | String | Ja |

**Reactie**

Als u met succes reageert, worden details over het geïmporteerde openbare pakket geretourneerd.

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### Openbare pakketten weergeven {#list-public-packages}

Zoek een lijst met pakketten die zichtbaar zijn voor het publiek door een GET-aanvraag in te dienen bij het eindpunt van `/transfer/list?{QUERY_PARAMS}` .

**API formaat**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| Parameter | Geaccepteerde/standaardwaarden |
| --- | --- |
| `property` | Geeft de eigenschap aan waarop moet worden gefilterd, zoals status. Acceptabele waarden voor status zijn: `COMPLETED` en `FAILED` . |
| `start` | De standaardwaarde van start is `0` . |
| `limit` | De standaardwaarde van limit is `20` . |
| `orderBy` | De volgorde accepteert alleen het veld `createdDate` . |
| `requestType` | Accepteert `PUBLIC` of `PRIVATE` . |

**Verzoek**

Het volgende verzoek haalt een lijst van pakketten met openbare beschikbaarheid op.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Reactie**

Een succesvol antwoord geeft een lijst met openbare pakketten en hun details.

+++reactie weergeven

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## Pakketlading kopiëren (#package-payload)

U kunt de lading van een openbaar pakket kopiëren door een GET- verzoek aan het `/packages/payload` eindpunt te doen dat overeenkomstige identiteitskaart van het pakket in de verzoekweg omvat.

**API formaat**

```http
GET /packages/payload/{PACKAGE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{PACKAGE_ID}` | De id van het pakket dat u wilt kopiëren. |

**Verzoek**

Met de volgende aanvraag wordt de lading van een pakket opgehaald met de id {PACKAGE_ID} .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `imsOrdId` | De id van de organisatie waartoe het pakket behoort. | String | Ja |
| `packageId` | De id van het pakket die u wilt laden. | String | Ja |

**Reactie**

Een geslaagde reactie retourneert de lading van het pakket.

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```

## Updates van objectconfiguratie migreren

Gebruik het /packages eindpunt in sandbox tooling API om objecten configuratieupdates te migreren.

### Bewerkingen bijwerken (#update-bewerkingen)

Vergelijk een opgegeven of laatste versie van een pakketmomentopname met de huidige status van de bronsandbox of een eerder gebruikte doelsandbox waarin het pakket is geïmporteerd door een POST-aanvraag in te dienen bij het `/packages/{packageId}/version/compare` -eindpunt, waarbij de pakket-id wordt opgegeven.

***API formaat***

```http
PATCH /packages/{packageId}/version/compare
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `packageId` | De id van het pakket. | String | Ja |

**Verzoek**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/compare/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "triggerNew": true,
      "targetSandbox": "{SANDBOX_NAME}"
  }'
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `triggerNew` | Markering om de nieuwe vergelijkingstaak voor Diff te activeren, zelfs als er al een actieve of voltooide taak bestaat. | Boolean | Nee |
| `targetSandbox` | Geeft de naam aan van de doelsandbox waarmee de diff moet worden berekend. Indien niet opgegeven, wordt de bronsandbox gebruikt als doelsandbox. | String | Nee |

**Reactie**

Een geslaagde reactie voor een eerder voltooide taak retourneert het taakobject met de eerder berekende diff-resultaten. Een nieuw voltooide baan keert JobId terug.

+++Antwoord weergeven (verzonden taak)

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "c4b7d07ae4c646279e2070a31c50bd5c",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "SUCCESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "deltaPackageVersion": {
            "packageId": "{PACKAGE_ID}",
            "currentVersion": 0,
            "validated": false,
            "rootArtifacts": [
                {
                    "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de",
                    "type": "REGISTRY_SCHEMA",
                    "found": false,
                    "count": 0
                }
            ],
            "eximGraphDelta": {
                "vertices": [],
                "pluginDeltas": [
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 2_1738766274074",
                                "newValue": "Custom FieldGroup 2"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    },
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 4_1738766274074",
                                "newValue": "Custom FieldGroup 4"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    }
                ]
            }
        },
        "importReplacementMap": {
            "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
            "5a45f8cd309d5ed5797be9a0af65e89152a51d57a6c74b52": "4ae041fa182d6faf2e7c56463399170d913138a7c5712909",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/b2b7705e770a35341b8bc5ec5e3644d9c7387266777fe4ba": "https://ns.adobe.com/sandboxtoolingstage/schemas/838c4e21ad81543ac14238ac1756012f7f98f0e0bec6b425",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de": "https://ns.adobe.com/sandboxtoolingstage/schemas/9a55692d527169d0239e126137a694ed9db2406c9bcbd06a",
            "8f45c79235c91e7f0c09af676a77d170a34b5ee0ad5de72c": "65d755cc3300674c3cfcec620c59876af07f046884afd359",
            "f04b8e461396ff426f8ba8dc5544f799bf287baa8e0fa5c": "b6fa821ada8cb97cac384f0b0354bbe74209ec97fb6a83a3",
            "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
            "c8304f3cb7986e8c9b613cd8d832125bd867fb4a5aedf67a": "4d21e9bf89ce0042b52d7d41ff177a7697d695e2617d1fc1"
        },
        "schemaFieldMappings": null
    }
}
```

+++

+++Reactie weergeven (nieuw ingediende taak)

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "aa5cfacf35a8478c8cf44a675fab1c30 ",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "IN_PROGRESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "schemaFieldMappings": null
    }
}
```

+++

### Pakketversie bijwerken (#package-versioning)

Voer een upgrade van het pakket uit naar een nieuwe versie met behulp van de meest recente momentopname van de bronsandbox voor elk object door een GET-aanvraag in te dienen bij het `/packages/{packageId}/version/save` -eindpunt en de pakket-id op te geven.

***API formaat***

```http
PATCH /packages/{packageId}/version/save
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `packageId` | De id van het pakket. | String | Ja |

**Verzoek**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/save/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**Reactie**

Een geslaagde reactie retourneert de taakstatus voor de versieupgrade.

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Version Job Package: {JOB_ID}",
    "description": null,
    "visibility": "TENANT",
    "requestType": "VERSION",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPGRADE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### De versiehistorie van het pakket ophalen (#package-version-history)

Haal de versiegeschiedenis van het pakket op, inclusief de tijdstempel en modifier, door een GET-aanvraag in te dienen bij het `/packages/{packageId}/history` -eindpunt en de pakket-id op te geven.

***API formaat***

```http
PATCH /packages/{packageId}/history
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `packageId` | De id van het pakket. | String | Ja |

**Verzoek**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/history/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**Reactie**

Een geslaagde reactie retourneert de versiegeschiedenis van een pakket.

```json
[
    {
        "id": "cb68591a1ed941e191e7f52e33637a26",
        "version": 0,
        "createdDate": 1739516784000,
        "modifiedDate": 1739516784000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 3
    },
    {
        "id": "e26189e6e4df476bb66c3fc3e66a1499",
        "version": 0,
        "createdDate": 1739343268000,
        "modifiedDate": 1739343268000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 2
    },
    {
        "id": "11af34c0eee449ac84ef28c66d9383e3",
        "version": 0,
        "createdDate": 1739343073000,
        "modifiedDate": 1739343073000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 1
    }
]
```

### Een updatetaak verzenden (#submit-update)

Verhoog nieuwe updates in de doelsandboxobjecten door een PATCH-aanvraag in te dienen bij het eindpunt van `/packages/{packageId}/import` en de pakket-id op te geven.

***API formaat***

```http
PATCH /packages/{packageId}/import
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `packageId` | De id van het pakket. | String | Ja |

**Verzoek**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "id": "50fd94f8072b4f248737a2b57b41058f",
      "name": "Test Update",
      "destinationSandbox": {
        "name": "test-sandbox-sbt",
        "imsOrgId": "{ORG_ID}"
      },
      "overwriteMappings": {
        "https://ns.adobe.com/sandboxtoolingstage/schemas/327a48c83a5359f8160420a00d5a07f0ba8631a1fd466f9e" : {
            "id" : "https://ns.adobe.com/sandboxtoolingstage/schemas/e346bb2cd7b26576cb51920d214aebbd42940a9bf94a75cd",
            "type" : "REGISTRY_SCHEMA"
        }
      }
  }'
```

**Reactie**

Een geslaagde reactie retourneert de taak-id voor de update.

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Update Job Name",
    "description": "Update Job Description",
    "visibility": "TENANT",
    "requestType": "IMPORT",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPDATE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "amanda-1",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### Update en overschrijving uitschakelen voor een pakket (#disable-update)

Schakel update en overschrijving uit voor pakketten die ze niet ondersteunen door een GET-aanvraag in te dienen bij het `/packages/{packageId}/?{QUERY_PARAMS}` -eindpunt en de pakket-id op te geven.

***API formaat***

```http
PATCH /packages/{packageId}?{QUERY_PARAMS}
```

| Eigenschap | Beschrijving | Type | Vereist |
| --- | --- | --- | --- |
| `packageId` | De id van het pakket. | String | Ja |
| {QUERY_PARAM} | De getCapabilites-queryparameter. Deze moet worden ingesteld op `true` of `false` | Boolean | Ja |

**Verzoek**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}?getCapabilities=true'/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**Reactie**

Een succesvol antwoord geeft een lijst van de mogelijkheden van het pakket terug.

```json
{
    "id": "80230dde96574a828191144709bb9b51",
    "version": 3,
    "createdDate": 1749808582000,
    "modifiedDate": 1749808648000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "Ankit_Primary_Descriptor_Test",
    "description": "RestPackage",
    "imsOrgId": "{ORG_ID}",
    "clientId": "usecasebuilder",
    "packageType": "PARTIAL",
    "expiry": 1757584598000,
    "publishDate": 1749808648000,
    "status": "PUBLISHED",
    "packageVisibility": "PRIVATE",
    "latestPackageVersion": 0,
    "packageAccessType": "TENANT",
    "artifactsList": [
        {
            "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/1c767056056de64d8030380d1b9f570d26bc15501a1e0e95",
            "altId": null,
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "atul-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "packageCapabilities": {
        "capabilities": [
            "VERSIONABLE"
        ]
    }
}
```
