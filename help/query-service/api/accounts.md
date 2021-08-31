---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;api gids;de dienst van de vraag;de rekeningen van de vraagdienst;rekeningen van de rekeningen van de;vraag;
solution: Experience Platform
title: Accounts-API-eindpunt
topic-legacy: connection parameters
description: U kunt een account voor Query Service maken voor een blijvende verbinding.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 391b1943f1c941188b370e62ec86216367aa747f
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---

# Rekeningeindpunt

In de Dienst van de Vraag van Adobe Experience Platform, worden de rekeningen gebruikt om niet-vervallende geloofsbrieven tot stand te brengen die u met externe SQL cliënten kunt gebruiken. U kunt het `/accounts` eindpunt in de Dienst API van de Vraag gebruiken, die u toestaat om programmatically uw de integratierekeningen van de Dienst van de Vraag tot stand te brengen terug te winnen, uit te geven en te schrappen (die ook als technische rekening wordt bekend).

## Aan de slag

De eindpunten die in deze gids worden gebruikt maken deel uit van de Dienst API van de Vraag. Voordat u verdergaat, bekijkt u eerst de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om oproepen aan API, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen met succes te maken.

## Een account maken

U kunt een de integratierekening van de Dienst van de Vraag tot stand brengen door een verzoek van de POST aan het `/accounts` eindpunt te doen.

**API-indeling**

```http
POST /accounts
```

**Verzoek**

Het volgende verzoek zal tot een nieuwe de integratierekening van de Dienst van de Vraag voor uw organisatie IMS leiden.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `accountName` | **** RequiredThe name of the Query Service integration account. |
| `assignedToUser` | **** RequiredDe Adobe ID waarvoor de de integratierekening van de Dienst van de Vraag zal worden gecreeerd. |
| `credential` | *(Facultatief)* de referentie die voor de integratie van de Dienst van de Vraag wordt gebruikt. Als deze optie niet is opgegeven, genereert het systeem automatisch een referentie voor u. |
| `description` | *(Optioneel)* Een beschrijving voor het integratieaccount van Query Service. |

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP, met details van uw onlangs gecreeerde de integratierekening van de Dienst van de Vraag terug. U kunt deze accountdetails gebruiken om de Query Service te verbinden met externe clients.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `technicalAccountName` | De naam van uw de integratierekening van de Dienst van de Vraag. |
| `technicalAccountId` | De id van uw de integratierekening van de Dienst van de Vraag. Dit, samen met `credential`, stelt uw wachtwoord voor uw rekening samen. |
| `credential` | De referentie van uw de integratierekening van de Dienst van de Vraag. Dit, samen met `technicalAccountId`, stelt uw wachtwoord voor uw rekening samen. |

## Een account bijwerken

U kunt uw de integratierekening van de Dienst van de Vraag bijwerken door een verzoek van de PUT aan het `/accounts` eindpunt te doen.

**API-indeling**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{ACCOUNT_ID}` | De id van de de integratierekening van de Dienst van de Vraag u wilt bijwerken. |

**Verzoek**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `accountName` | *(Optioneel)* De bijgewerkte naam voor de integratieaccount van Query Service. |
| `assignedToUser` | *(Optioneel)* De bijgewerkte Adobe ID waaraan de integratieaccount van Query Service is gekoppeld. |
| `credential` | *(Optioneel)* De bijgewerkte referentie voor uw Query Service-account. |
| `description` | *(Optioneel)* De bijgewerkte beschrijving voor de integratieaccount van Query Service. |

**Antwoord**

Een succesvolle reactie keert HTTP status 200 met informatie over uw onlangs bijgewerkte de integratierekening van de Dienst van de Vraag terug.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## Alle accounts weergeven

U kunt een lijst van alle de integratierekeningen van de Dienst van de Vraag terugwinnen door een verzoek van de GET aan het `/accounts` eindpunt te doen.

**API-indeling**

```http
GET /accounts
```

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met een lijst van alle de integratierekeningen van de Dienst van de Vraag terug.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## Een account verwijderen

U kunt uw de integratierekening van de Dienst van de Vraag schrappen door een verzoek van DELETE aan het `/accounts` eindpunt te doen.

**API-indeling**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{ACCOUNT_ID}` | De id van de de integratierekening van de Dienst van de Vraag u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een bericht dat aangeeft dat de account is verwijderd.

```json
{
    "result": "Success"
}
```
