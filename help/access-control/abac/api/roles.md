---
keywords: Experience Platform;home;populaire onderwerpen;api;Op kenmerk-Gebaseerd Toegangsbeheer;op attributen-gebaseerd toegangsbeheer
solution: Experience Platform
title: Rollen API-eindpunt
description: Het /rollen eindpunt in op attributen-Gebaseerde Controle API van de Toegang staat u toe om rollen in Adobe Experience Platform programmatically te beheren.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# Het eindpunt van rollen

>[!NOTE]
>
>Als een gebruikerstoken wordt overgegaan, dan moet de gebruiker van het teken een &quot;org admin&quot;rol voor gevraagde org hebben.

De rollen bepalen de toegang die een beheerder, een specialist, of een eindgebruiker aan middelen in uw organisatie moet hebben. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben.

Het `/roles` eindpunt in op attribuut-gebaseerde toegangsbeheer API staat u toe om rollen in uw organisatie programmatically te beheren.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van op attribuut-gebaseerde toegangsbeheer API. Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API met succes te maken.

## Een lijst met rollen ophalen {#list}

U kunt alle bestaande rollen weergeven die tot uw organisatie behoren door een GET-aanvraag in te dienen bij het `/roles` -eindpunt.

**API formaat**

```http
GET /roles/
```

**Verzoek**

Het volgende verzoek wint een lijst van rollen terug die tot uw organisatie behoren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een succesvolle reactie keert een lijst van rollen in uw organisatie, met inbegrip van informatie over hun respectieve roltype, toestemmingsreeksen, en onderwerpattributen terug.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met de rol. Deze id wordt automatisch gegenereerd. |
| `name` | De naam van uw rol. |
| `description` | Het beschrijvingsbezit verstrekt extra informatie over uw rol. |
| `roleType` | Het aangewezen type van de rol. De mogelijke waarden voor het roltype zijn: `user-defined` en `system-defined` . |
| `permissionSets` | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| `sandboxes` | Met deze eigenschap worden de sandboxen binnen uw organisatie weergegeven die zijn ingericht voor een bepaalde rol. |
| `subjectAttributes` | De kenmerken die de correlatie aangeven tussen een onderwerp en de Experience Platform-bronnen waartoe ze toegang hebben. |
| `subjectAttributes.labels` | Hiermee geeft u de labels voor gegevensgebruik weer die op de gevraagde rol zijn toegepast. |

## Rol opzoeken {#lookup}

U kunt een afzonderlijke rol opzoeken door een GET-aanvraag in te dienen die de bijbehorende `roleId` bevat in het aanvraagpad.

**API formaat**

```http
GET /roles/{ROLE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {ROLE_ID} | De id van de rol die u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt informatie voor `{ROLE_ID}` opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een succesvolle reactie keert details voor gevraagde rol identiteitskaart, met inbegrip van informatie over zijn roltype, toestemmingsreeksen, en onderwerpattributen terug.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met de rol. Deze id wordt automatisch gegenereerd. |
| `name` | De naam van uw rol. |
| `description` | Het beschrijvingsbezit verstrekt extra informatie over uw rol. |
| `roleType` | Het aangewezen type van de rol. De mogelijke waarden voor het roltype zijn: `user-defined` en `system-defined` . |
| `permissionSets` | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| `sandboxes` | Met deze eigenschap worden de sandboxen binnen uw organisatie weergegeven die zijn ingericht voor een bepaalde rol. |
| `subjectAttributes` | De kenmerken die de correlatie aangeven tussen een onderwerp en de Experience Platform-bronnen waartoe ze toegang hebben. |
| `subjectAttributes.labels` | Hiermee geeft u de labels voor gegevensgebruik weer die op de gevraagde rol zijn toegepast. |

## Onderwerpen opzoeken op rol-id

U kunt onderwerpen ook ophalen door een GET-aanvraag in te dienen bij het eindpunt van `/roles` terwijl u een {ROLE_ID} opgeeft.

**API formaat**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parameter | Beschrijving |
| --- | --- |
| {ROLE_ID} | De id van de rol die is gekoppeld aan de onderwerpen die u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag worden onderwerpen opgehaald die aan `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809` zijn gekoppeld.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een succesvolle reactie retourneert de onderwerpen die aan de betrokken rol-id zijn gekoppeld, inclusief de overeenkomstige onderwerp-id en het bijbehorende onderwerptype.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `roleId` | De rol-id die is gekoppeld aan het onderwerp waarnaar wordt gevraagd. |
| `subjectType` | Het type van het onderwerp waarnaar wordt gevraagd. |
| `subjectId` | De id die overeenkomt met het onderwerp in kwestie. |

## Een rol maken {#create}

Om een nieuwe rol tot stand te brengen, doe een POST- verzoek aan het `/roles` eindpunt terwijl het verstrekken van waarden voor de naam van uw rol, beschrijving, en roltype.

**API formaat**

```http
POST /roles/
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw rol. Zorg ervoor dat de naam van uw rol beschrijvend is aangezien u dit kunt gebruiken om informatie over uw rol op te zoeken. |
| `description` | (Optioneel) Een beschrijvende waarde die u kunt opnemen voor meer informatie over uw rol. |
| `roleType` | Het aangewezen type van de rol. De mogelijke waarden voor het roltype zijn: `user-defined` en `system-defined` . |

**Reactie**

Een succesvolle reactie keert uw onlangs gecreëerde rol, met zijn overeenkomstige rol identiteitskaart, evenals informatie over zijn roltype, toestemmingsreeksen, en onderwerpattributen terug.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met de rol. Deze id wordt automatisch gegenereerd. |
| `name` | De naam van uw rol. |
| `description` | Het beschrijvingsbezit verstrekt extra informatie over uw rol. |
| `roleType` | Het aangewezen type van de rol. De mogelijke waarden voor het roltype zijn: `user-defined` en `system-defined` . |
| `permissionSets` | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| `sandboxes` | Met deze eigenschap worden de sandboxen binnen uw organisatie weergegeven die zijn ingericht voor een bepaalde rol. |
| `subjectAttributes` | De kenmerken die de correlatie aangeven tussen een onderwerp en de Experience Platform-bronnen waartoe ze toegang hebben. |
| `subjectAttributes.labels` | Hiermee geeft u de labels voor gegevensgebruik weer die op de gevraagde rol zijn toegepast. |

## Een rol bijwerken {#patch}

U kunt de eigenschappen van een rol bijwerken door een PATCH-aanvraag in te dienen bij het `/roles` -eindpunt terwijl de bijbehorende rol-id en waarden worden opgegeven voor de bewerkingen die u wilt toepassen.

**API formaat**

```http
PATCH /roles/{ROLE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {ROLE_ID} | De id van de rol die u wilt bijwerken. |

**Verzoek**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| Bewerkingen | Beschrijving |
| --- | --- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de rol bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een geslaagde reactie retourneert de bijgewerkte rol, inclusief nieuwe waarden voor de eigenschappen die u wilt bijwerken.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met de rol. Deze id wordt automatisch gegenereerd. |
| `name` | De naam van uw rol. |
| `description` | Het beschrijvingsbezit verstrekt extra informatie over uw rol. |
| `roleType` | Het aangewezen type van de rol. De mogelijke waarden voor het roltype zijn: `user-defined` en `system-defined` . |
| `permissionSets` | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| `sandboxes` | Met deze eigenschap worden de sandboxen binnen uw organisatie weergegeven die zijn ingericht voor een bepaalde rol. |
| `subjectAttributes` | De kenmerken die de correlatie aangeven tussen een onderwerp en de Experience Platform-bronnen waartoe ze toegang hebben. |
| `subjectAttributes.labels` | Hiermee geeft u de labels voor gegevensgebruik weer die op de gevraagde rol zijn toegepast. |

## Rollen bijwerken op rol-id {#put}

U kunt een rol bijwerken door een PUT-aanvraag in te dienen bij het `/roles` -eindpunt en de rol-id op te geven die overeenkomt met de rol die u wilt bijwerken.

**API formaat**

```http
PUT /roles/{ROLE_ID}
```

**Verzoek**

Met de volgende aanvraag worden de naam, beschrijving en het roltype voor rol-id bijgewerkt: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809` .

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De bijgewerkte naam van een rol. |
| `description` | De bijgewerkte beschrijving van een rol. |
| `roleType` | Het aangewezen type van de rol. De mogelijke waarden voor het roltype zijn: `user-defined` en `system-defined` . |

**Reactie**

Een succesvolle reactie keert uw bijgewerkte rol, met inbegrip van nieuwe waarden voor zijn naam, beschrijving, en roltype terug.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met de rol. Deze id wordt automatisch gegenereerd. |
| `name` | De naam van uw rol. |
| `description` | Het beschrijvingsbezit verstrekt extra informatie over uw rol. |
| `roleType` | Het aangewezen type van de rol. De mogelijke waarden voor het roltype zijn: `user-defined` en `system-defined` . |
| `permissionSets` | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| `sandboxes` | Met deze eigenschap worden de sandboxen binnen uw organisatie weergegeven die zijn ingericht voor een bepaalde rol. |
| `subjectAttributes` | De kenmerken die de correlatie aangeven tussen een onderwerp en de Experience Platform-bronnen waartoe ze toegang hebben. |
| `subjectAttributes.labels` | Hiermee geeft u de labels voor gegevensgebruik weer die op de gevraagde rol zijn toegepast. |

## Onderwerp bijwerken op rol-id

Om de onderwerpen bij te werken verbonden aan een rol, doe een PATCH verzoek aan het `/roles` eindpunt terwijl het verstrekken van rolidentiteitskaart van de onderwerpen u wilt bijwerken.

**API formaat**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Parameter | Beschrijving |
| --- | --- |
| {ROLE_ID} | De id van de rol die is gekoppeld aan de onderwerpen die u wilt bijwerken. |

**Verzoek**

De volgende aanvraag werkt de onderwerpen bij die aan `{ROLE_ID}` zijn gekoppeld.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| Bewerkingen | Beschrijving |
| --- | --- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de rol bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een succesvolle reactie retourneert uw bijgewerkte rol, inclusief nieuwe waarden voor de onderwerpen.

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## Een rol verwijderen {#delete}

Als u een rol wilt verwijderen, vraagt u DELETE het `/roles` -eindpunt aan en geeft u de id op van de rol die u wilt verwijderen.

**API formaat**

```http
DELETE /roles/{ROLE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {ROLE_ID} | De id van de rol die u wilt verwijderen. |

**Verzoek**

Met het volgende verzoek wordt de rol met de id `{ROLE_ID}` verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de verwijdering bevestigen door een opzoekverzoek (GET) in te dienen bij de rol. U ontvangt de HTTP-status 404 (Niet gevonden) omdat de rol uit het beheer is verwijderd.

## API-referentie toevoegen {#apicredential}

Als u API-referentie wilt toevoegen, vraagt u een PATCH-aanvraag naar het eindpunt van `/roles` en geeft u de rol-id van de onderwerpen op.

**API formaat**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| Bewerkingen | Beschrijving |
| --- | --- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de rol bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Het pad van de parameter die moet worden toegevoegd. |
| `value` | De waarde waarmee u de parameter wilt toevoegen. |

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.
