---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-ontwikkelaarsgids
solution: Experience Platform
title: API-eindpunt voor sandboxbeheer
topic-legacy: developer guide
description: Met het eindpunt /sandboxen in de sandbox-API kunt u sandboxen in Adobe Experience Platform programmatisch beheren.
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---

# Sandbox-beheereindpunt

Sandboxen in Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving. Met het `/sandboxes`-eindpunt in de [!DNL Sandbox]-API kunt u sandboxen in Platform programmatisch beheren.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een Experience Platform-API te kunnen uitvoeren.

## Een lijst met sandboxen ophalen {#list}

U kunt alle sandboxen weergeven die tot uw IMS-organisatie behoren (actief of anderszins) door een aanvraag voor een GET in te dienen bij het `/sandboxes`-eindpunt.

**API-indeling**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie de sectie over [queryparameters](./appendix.md#query) voor meer informatie. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met sandboxen die tot uw organisatie behoren, inclusief details zoals `name`, `title`, `state` en `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de sandbox. Deze eigenschap wordt gebruikt voor opzoekdoeleinden in API-aanroepen. |
| `title` | De weergavenaam voor de sandbox. |
| `state` | De huidige verwerkingsstatus van de sandbox. De status van een sandbox kan een van de volgende zijn: <br/><ul><li>`creating`: De sandbox is gemaakt, maar wordt nog steeds door het systeem ingericht.</li><li>`active`: De sandbox wordt gemaakt en actief.</li><li>`failed`: Door een fout kon de sandbox niet door het systeem worden ingericht en is deze uitgeschakeld.</li><li>`deleted`: De sandbox is handmatig uitgeschakeld.</li></ul> |
| `type` | Het type sandbox. Tot de momenteel ondersteunde sandboxtypen behoren `development` en `production`. |
| `isDefault` | Een Booleaanse eigenschap die aangeeft of deze sandbox de standaardproductiesandbox voor de organisatie is. |
| `eTag` | Een id voor een specifieke versie van de sandbox. Deze waarde wordt gebruikt voor versiebeheer en caching-efficiëntie en wordt telkens bijgewerkt wanneer een wijziging in de sandbox wordt aangebracht. |

## Sandbox opzoeken {#lookup}

U kunt een afzonderlijke sandbox opzoeken door een verzoek in te dienen om de eigenschap `name` van de sandbox op te nemen in het aanvraagpad.

**API-indeling**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De eigenschap `name` van de sandbox die u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt een sandbox met de naam &quot;dev-2&quot; opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwoord**

Een geslaagde reactie retourneert de details van de sandbox, inclusief `name`, `title`, `state` en `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de sandbox. Deze eigenschap wordt gebruikt voor opzoekdoeleinden in API-aanroepen. |
| `title` | De weergavenaam voor de sandbox. |
| `state` | De huidige verwerkingsstatus van de sandbox. De status van een sandbox kan een van de volgende zijn: <ul><li>**maken**: De sandbox is gemaakt, maar wordt nog steeds door het systeem ingericht.</li><li>**actief**: De sandbox wordt gemaakt en actief.</li><li>**mislukt**: Door een fout kon de sandbox niet door het systeem worden ingericht en is deze uitgeschakeld.</li><li>**geschrapt**: De sandbox is handmatig uitgeschakeld.</li></ul> |
| `type` | Het type sandbox. Tot de huidige ondersteunde sandboxtypen behoren: `development` en `production`. |
| `isDefault` | Een Booleaanse eigenschap die aangeeft of deze sandbox de standaardsandbox voor de organisatie is. Dit is doorgaans de productiesandbox. |
| `eTag` | Een id voor een specifieke versie van de sandbox. Deze waarde wordt gebruikt voor versiebeheer en caching-efficiëntie en wordt telkens bijgewerkt wanneer een wijziging in de sandbox wordt aangebracht. |

## Een sandbox maken {#create}

U kunt een nieuwe ontwikkeling of productiestandaard tot stand brengen door een verzoek van de POST aan het `/sandboxes` eindpunt te doen.

### Een ontwikkelingssandbox maken

Als u een ontwikkelingssandbox wilt maken, moet u een `type`-kenmerk met de waarde `development` in de payload van de aanvraag opgeven.

**API-indeling**

```http
POST /sandboxes
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe ontwikkelingssandbox gemaakt met de naam &quot;acme-dev&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De id die wordt gebruikt voor toegang tot de sandbox in toekomstige aanvragen. Deze waarde moet uniek zijn, en de beste praktijken moeten het zo beschrijvend mogelijk maken. Deze waarde mag geen spaties of speciale tekens bevatten. |
| `title` | Een leesbare naam die voor weergavedoeleinden in de gebruikersinterface van het Platform wordt gebruikt. |
| `type` | Het type sandbox dat moet worden gemaakt. Voor een niet-productiesandbox, moet deze waarde `development` zijn. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe sandbox, waarbij wordt getoond dat de `state` &#39;maakt&#39;.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Sandboxen nemen ongeveer 30 seconden in beslag om door het systeem te worden ingericht, waarna hun `state` &quot;actief&quot; of &quot;mislukt&quot; worden.

### Een productiesandbox maken

Als u een productiesandbox wilt maken, moet u een `type`-kenmerk met de waarde `production` in de payload van de aanvraag opgeven.

**API-indeling**

```http
POST /sandboxes
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe productiesandbox gemaakt met de naam &quot;acme&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De id die wordt gebruikt voor toegang tot de sandbox in toekomstige aanvragen. Deze waarde moet uniek zijn, en de beste praktijken moeten het zo beschrijvend mogelijk maken. Deze waarde mag geen spaties of speciale tekens bevatten. |
| `title` | Een leesbare naam die voor weergavedoeleinden in de gebruikersinterface van het Platform wordt gebruikt. |
| `type` | Het type sandbox dat moet worden gemaakt. Voor een productiesandbox moet deze waarde `production` zijn. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe sandbox, waarbij wordt getoond dat de `state` &#39;maakt&#39;.

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>Sandboxen nemen ongeveer 30 seconden in beslag om door het systeem te worden ingericht, waarna hun `state` &quot;actief&quot; of &quot;mislukt&quot; worden.

## Een sandbox bijwerken {#put}

U kunt een of meer velden in een sandbox bijwerken door een PATCH-verzoek in te dienen dat de sandbox `name` bevat in het aanvraagpad en de eigenschap die moet worden bijgewerkt in de aanvraaglading.

>[!NOTE]
>
>Momenteel kan alleen de eigenschap `title` van een sandbox worden bijgewerkt.

**API-indeling**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De eigenschap `name` van de sandbox die u wilt bijwerken. |

**Verzoek**

Met het volgende verzoek wordt de eigenschap `title` van de sandbox met de naam &quot;acme&quot; bijgewerkt.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) met de details van de zojuist bijgewerkte sandbox.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Een sandbox opnieuw instellen {#reset}

Sandboxen hebben een functie voor fabrieksinstellingen waarmee alle niet-standaardbronnen uit een sandbox worden verwijderd. U kunt een sandbox opnieuw instellen door een verzoek voor een PUT in te dienen dat de sandbox `name` bevat in het aanvraagpad.

**API-indeling**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De eigenschap `name` van de sandbox die u wilt herstellen. |
| `validationOnly` | Een optionele parameter waarmee u een controle voorafgaand aan de vlucht kunt uitvoeren op de sandbox-herstelbewerking zonder de eigenlijke aanvraag in te dienen. Stel deze parameter in op `validationOnly=true` om te controleren of de sandbox die u wilt herstellen gegevens bevat over het delen van Adobe Analytics, Adobe Audience Manager of segmenten. |

**Verzoek**

Met de volgende aanvraag wordt een sandbox met de naam &quot;acme-dev&quot; opnieuw ingesteld.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `action` | Deze parameter moet in de payload van de aanvraag worden opgegeven met de waarde &quot;reset&quot; om de sandbox opnieuw in te stellen. |

**Antwoord**

>[!NOTE]
>
>Wanneer een sandbox opnieuw is ingesteld, duurt het ongeveer 30 seconden voordat het systeem de sandbox heeft ingericht.

Een succesvol antwoord retourneert de details van de bijgewerkte sandbox, waarbij wordt getoond dat `state` opnieuw wordt ingesteld.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

De standaardproductiesandbox en door de gebruiker gemaakte productiesandboxen kunnen niet opnieuw worden ingesteld als de identiteitsgrafiek die erin wordt gehost, ook door Adobe Analytics wordt gebruikt voor de functie [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html), of als de identiteitsgrafiek die hierin wordt gehost, ook door Adobe Audience Manager wordt gebruikt voor de functie [People Based Destination (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).

Hieronder volgt een lijst met mogelijke uitzonderingen die kunnen voorkomen dat een sandbox opnieuw wordt ingesteld:

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

U kunt doorgaan met het herstellen van een productiestandaard die wordt gebruikt voor bidirectioneel segmentdelen met [!DNL Audience Manager] of [!DNL Audience Core Service] door de parameter `ignoreWarnings` aan uw verzoek toe te voegen.

**API-indeling**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De eigenschap `name` van de sandbox die u wilt herstellen. |
| `ignoreWarnings` | Een optionele parameter waarmee u de validatiecontrole kunt overslaan en de voorinstelling van een productiesandbox kunt forceren die wordt gebruikt voor bidirectioneel segmentdelen met [!DNL Audience Manager] of [!DNL Audience Core Service]. Deze parameter kan niet worden toegepast op een standaardproductiesandbox. |

**Verzoek**

In het volgende verzoek wordt een productiesandbox met de naam &quot;acme&quot; opnieuw ingesteld.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Antwoord**

Een succesvol antwoord retourneert de details van de bijgewerkte sandbox, waarbij wordt getoond dat `state` opnieuw wordt ingesteld.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## Een sandbox verwijderen {#delete}

>[!IMPORTANT]
>
>De standaardproductiesandbox kan niet worden verwijderd.

U kunt een sandbox verwijderen door een DELETE-verzoek in te dienen dat de sandbox `name` bevat in het aanvraagpad.

>[!NOTE]
>
>Als u deze API-aanroep maakt, wordt de eigenschap `status` van de sandbox bijgewerkt naar &quot;verwijderd&quot; en wordt deze gedeactiveerd. Met GET-aanvragen kunnen de gegevens van de sandbox nog steeds worden opgehaald nadat deze zijn verwijderd.

**API-indeling**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` van de sandbox die u wilt verwijderen. |
| `validationOnly` | Een optionele parameter waarmee u een controle voorafgaand aan de vlucht kunt uitvoeren op de sandbox-verwijderbewerking zonder de eigenlijke aanvraag in te dienen. Stel deze parameter in op `validationOnly=true` om te controleren of de sandbox die u wilt herstellen gegevens bevat over het delen van Adobe Analytics, Adobe Audience Manager of segmenten. |
| `ignoreWarnings` | Een optionele parameter waarmee u de validatiecontrole kunt overslaan en de verwijdering kunt forceren van een door de gebruiker gemaakte productiesandbox die wordt gebruikt voor bidirectioneel segmentdelen met [!DNL Audience Manager] of [!DNL Audience Core Service]. Deze parameter kan niet worden toegepast op een standaardproductiesandbox. |

**Verzoek**

Met het volgende verzoek wordt een productiesandbox met de naam &quot;acme&quot; verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een succesvol antwoord retourneert de bijgewerkte details van de sandbox, waarbij wordt getoond dat `state` wordt &quot;verwijderd&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
