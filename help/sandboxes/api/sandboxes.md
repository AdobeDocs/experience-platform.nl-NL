---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-ontwikkelaarsgids
solution: Experience Platform
title: API-eindpunt voor sandboxbeheer
topic-legacy: developer guide
description: Met het eindpunt /sandboxen in de sandbox-API kunt u sandboxen in Adobe Experience Platform programmatisch beheren.
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 1%

---

# Sandbox-beheereindpunt

Sandboxen in Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving. De `/sandboxes` in de [!DNL Sandbox] Met API kunt u sandboxen in Platform programmatisch beheren.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Een lijst met sandboxen ophalen {#list}

U kunt alle sandboxen weergeven die tot uw IMS-organisatie behoren (actief of anderszins) door een aanvraag voor een GET in te dienen bij de `/sandboxes` eindpunt.

**API-indeling**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie de sectie over [queryparameters](./appendix.md#query) voor meer informatie . |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met sandboxen die tot uw organisatie behoren, inclusief details zoals `name`, `title`, `state`, en `type`.

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
| `type` | Het type sandbox. Tot de momenteel ondersteunde sandboxtypen behoren: `development` en `production`. |
| `isDefault` | Een Booleaanse eigenschap die aangeeft of deze sandbox de standaardproductiesandbox voor de organisatie is. |
| `eTag` | Een id voor een specifieke versie van de sandbox. Deze waarde wordt gebruikt voor versiebeheer en caching-efficiëntie en wordt telkens bijgewerkt wanneer een wijziging in de sandbox wordt aangebracht. |

## Sandbox opzoeken {#lookup}

U kunt een afzonderlijke sandbox opzoeken door een aanvraag voor een GET in te dienen die de sandbox bevat `name` eigenschap in het aanvraagpad.

**API-indeling**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` eigenschap van de sandbox die u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt een sandbox met de naam &quot;dev-2&quot; opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwoord**

Als de reactie is gelukt, worden de details van de sandbox, inclusief de sandbox, geretourneerd `name`, `title`, `state`, en `type`.

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
| `state` | De huidige verwerkingsstatus van de sandbox. De status van een sandbox kan een van de volgende zijn: <ul><li>**maken**: De sandbox is gemaakt, maar wordt nog steeds door het systeem ingericht.</li><li>**actief**: De sandbox wordt gemaakt en actief.</li><li>**mislukt**: Door een fout kon de sandbox niet door het systeem worden ingericht en is deze uitgeschakeld.</li><li>**verwijderd**: De sandbox is handmatig uitgeschakeld.</li></ul> |
| `type` | Het type sandbox. Tot de huidige ondersteunde sandboxtypen behoren: `development` en `production`. |
| `isDefault` | Een Booleaanse eigenschap die aangeeft of deze sandbox de standaardsandbox voor de organisatie is. Dit is doorgaans de productiesandbox. |
| `eTag` | Een id voor een specifieke versie van de sandbox. Deze waarde wordt gebruikt voor versiebeheer en caching-efficiëntie en wordt telkens bijgewerkt wanneer een wijziging in de sandbox wordt aangebracht. |

## Een sandbox maken {#create}

>[!NOTE]
>
>Wanneer een nieuwe sandbox wordt gemaakt, moet u die nieuwe sandbox eerst aan uw productprofiel toevoegen in [Adobe Admin Console](https://adminconsole.adobe.com/) voordat u de nieuwe sandbox kunt gaan gebruiken. Zie de documentatie op [het beheren van toestemmingen voor een productprofiel](../../access-control/ui/permissions.md) voor informatie over hoe u een sandbox kunt toevoegen aan een productprofiel.

U kunt een nieuwe ontwikkelings- of productiestandaard maken door een POST aan te vragen bij de `/sandboxes` eindpunt.

### Een ontwikkelingssandbox maken

Als u een ontwikkelingssandbox wilt maken, moet u een `type` kenmerk met een waarde van `development` in de aanvraaglading.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | Het type sandbox dat moet worden gemaakt. Voor een niet-productiesandbox moet deze waarde `development`. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe sandbox, waarbij wordt getoond dat deze `state` is &quot;maken&quot;.

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
>Sandboxen nemen ongeveer 30 seconden in beslag om door het systeem te worden ingericht, waarna hun `state` wordt &quot;actief&quot; of &quot;mislukt&quot;.

### Een productiesandbox maken

Als u een productiesandbox wilt maken, moet u een `type` kenmerk met een waarde van `production` in de aanvraaglading.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | Het type sandbox dat moet worden gemaakt. Voor een productiesandbox moet deze waarde `production`. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe sandbox, waarbij wordt getoond dat deze `state` is &quot;maken&quot;.

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
>Sandboxen nemen ongeveer 30 seconden in beslag om door het systeem te worden ingericht, waarna hun `state` wordt &quot;actief&quot; of &quot;mislukt&quot;.

## Een sandbox bijwerken {#put}

U kunt een of meer velden in een sandbox bijwerken door een PATCH-verzoek in te dienen dat de sandbox `name` in de verzoekweg en het bezit in de verzoeklading bij te werken.

>[!NOTE]
>
>Momenteel alleen de sandbox `title` eigenschap kan worden bijgewerkt.

**API-indeling**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` eigenschap van de sandbox die u wilt bijwerken. |

**Verzoek**

De volgende aanvraag werkt de `title` eigenschap van de sandbox met de naam &quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Sandboxen hebben een functie voor fabrieksinstellingen waarmee alle niet-standaardbronnen uit een sandbox worden verwijderd. U kunt een sandbox opnieuw instellen door een PUT-aanvraag in te dienen die de sandbox bevat `name` in het aanvraagpad.

**API-indeling**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` eigenschap van de sandbox die u wilt herstellen. |
| `validationOnly` | Een optionele parameter waarmee u een controle voorafgaand aan de vlucht kunt uitvoeren op de sandbox-herstelbewerking zonder de eigenlijke aanvraag in te dienen. Deze parameter instellen op `validationOnly=true` om te controleren of de sandbox die u wilt herstellen Adobe Analytics-, Adobe Audience Manager- of segmentdelingsgegevens bevat. |

**Verzoek**

Met de volgende aanvraag wordt een sandbox met de naam &quot;acme-dev&quot; opnieuw ingesteld.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Als de reactie succesvol was, worden de details van de bijgewerkte sandbox geretourneerd, waarbij wordt getoond dat de `state` is &quot;opnieuw instellen&quot;.

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

De standaardproductiesandbox en door de gebruiker gemaakte productiessandboxen kunnen niet opnieuw worden ingesteld als de identiteitsgrafiek die erin wordt gehost, ook door Adobe Analytics wordt gebruikt voor de [Cross-Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) -functie, of als de identiteitsgrafiek die erin wordt gehost, ook door Adobe Audience Manager wordt gebruikt voor de [Op mensen gebaseerde Doelen (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) gebruiken.

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

U kunt doorgaan met het opnieuw instellen van een productiesandbox die wordt gebruikt voor bidirectioneel delen van segmenten met [!DNL Audience Manager] of [!DNL Audience Core Service] door de `ignoreWarnings` aan uw verzoek.

**API-indeling**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` eigenschap van de sandbox die u wilt herstellen. |
| `ignoreWarnings` | Een optionele parameter waarmee u de validatiecontrole kunt overslaan en het opnieuw instellen van een productiesandbox kunt forceren die wordt gebruikt voor bidirectioneel segmentdelen met [!DNL Audience Manager] of [!DNL Audience Core Service]. Deze parameter kan niet worden toegepast op een standaardproductiesandbox. |

**Verzoek**

In het volgende verzoek wordt een productiesandbox met de naam &quot;acme&quot; opnieuw ingesteld.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Antwoord**

Als de reactie succesvol was, worden de details van de bijgewerkte sandbox geretourneerd, waarbij wordt getoond dat de `state` is &quot;opnieuw instellen&quot;.

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

U kunt een sandbox verwijderen door een DELETE-aanvraag in te dienen die de sandbox `name` in het aanvraagpad.

>[!NOTE]
>
>Door deze API-aanroep te maken worden de sandboxen bijgewerkt `status` eigenschap &quot;delete&quot; aan en deactiveert deze. Met GET-aanvragen kunnen de gegevens van de sandbox nog steeds worden opgehaald nadat deze zijn verwijderd.

**API-indeling**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` van de sandbox die u wilt verwijderen. |
| `validationOnly` | Een optionele parameter waarmee u een controle voorafgaand aan de vlucht kunt uitvoeren op de sandbox-verwijderbewerking zonder de eigenlijke aanvraag in te dienen. Deze parameter instellen op `validationOnly=true` om te controleren of de sandbox die u wilt herstellen Adobe Analytics-, Adobe Audience Manager- of segmentdelingsgegevens bevat. |
| `ignoreWarnings` | Een optionele parameter waarmee u de validatiecontrole kunt overslaan en de verwijdering van een door de gebruiker gemaakte productiesandbox kunt forceren die wordt gebruikt voor bidirectioneel segmentdelen met [!DNL Audience Manager] of [!DNL Audience Core Service]. Deze parameter kan niet worden toegepast op een standaardproductiesandbox. |

**Verzoek**

Met het volgende verzoek wordt een productiesandbox met de naam &quot;acme&quot; verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Met een succesvol antwoord worden de bijgewerkte gegevens van de sandbox geretourneerd, waarbij wordt getoond dat de sandbox `state` wordt &quot;verwijderd&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
