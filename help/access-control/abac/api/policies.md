---
keywords: Experience Platform;huis;populaire onderwerpen;api;Op attributen-Gebaseerd Toegangsbeheer;op attributen-gebaseerd toegangsbeheer
solution: Experience Platform
title: API-eindpunt voor toegangsbeheerbeleid
description: Het /policies eindpunt in op attributen-Gebaseerde Controle API van de Toegang staat u toe om beleid in Adobe Experience Platform programmatically te beheren.
role: Developer
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Doel van toegangsbeheerbeleid

>[!NOTE]
>
>Als een gebruikerstoken wordt overgegaan, dan moet de gebruiker van het teken een &quot;org admin&quot;rol voor gevraagde org hebben.

Het beleid van de toegangscontrole is verklaringen die attributen samenbrengen om toelaatbare en ontoelaatbare acties te vestigen. Dit beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. Het `/policies` eindpunt in op attribuut-gebaseerde toegangsbeheer API staat u toe om beleid, met inbegrip van informatie over de regels programmatically te beheren die hen evenals hun respectieve onderwerpvoorwaarden beheersen.

>[!IMPORTANT]
>
>Dit eindpunt moet niet met het `/policies` eindpunt in de [ Dienst API van het Beleid ](../../../data-governance/api/policies.md) worden verward, dat wordt gebruikt om het beleid van het gegevensgebruik te beheren.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van op attribuut-gebaseerde toegangsbeheer API. Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een lijst met beleidsregels ophalen {#list}

Maak een verzoek van de GET aan het `/policies` eindpunt om van al bestaand beleid in uw organisatie een lijst te maken.

**API formaat**

```http
GET /policies
```

**Verzoek**

Het volgende verzoek wint een lijst van bestaand beleid terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een geslaagde reactie retourneert een lijst met bestaande beleidsregels.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met een beleid. Deze id wordt automatisch gegenereerd en kan worden gebruikt om een beleid op te zoeken, bij te werken en te verwijderen. |
| `imsOrgId` | De organisatie waar het betwiste beleid toegankelijk is. |
| `createdBy` | De id van de gebruiker die het beleid heeft gemaakt. |
| `createdAt` | Het tijdstip waarop het beleid is gemaakt. De eigenschap `createdAt` wordt weergegeven in een tijdstempel van één tijdperk. |
| `modifiedBy` | De id van de gebruiker die het beleid voor het laatst heeft bijgewerkt. |
| `modifiedAt` | De tijd waarop het beleid voor het laatst is bijgewerkt. De eigenschap `modifiedAt` wordt weergegeven in een tijdstempel van één tijdperk. |
| `name` | De naam van het beleid. |
| `description` | (Optioneel) Een eigenschap die kan worden toegevoegd voor meer informatie over een bepaald beleid. |
| `status` | De huidige status van een beleid. Deze eigenschap definieert of een beleid momenteel `active` of `inactive` is. |
| `subjectCondition` | De voorwaarden die op een onderwerp van toepassing zijn. Een onderwerp is een gebruiker met bepaalde attributen die om toegang tot een middel vragen om een actie uit te voeren. In dit geval is `subjectCondition` queryachtige voorwaarden die worden toegepast op de onderwerpkenmerken. |
| `rules` | De set regels die een beleid definiëren. De regels bepalen welke kenmerkcombinaties worden geoorloofd opdat het onderwerp een actie aan het middel met succes uitvoert. |
| `rules.effect` | Het effect dat ontstaat na het overwegen van waarden voor `action` , `condition` en `resource` . Mogelijke waarden zijn: `permit` , `deny` of `indeterminate` . |
| `rules.resource` | Het element dat of het object dat een onderwerp kan of kan benaderen.  Bronnen kunnen bestanden, toepassingen, servers of zelfs API&#39;s zijn. |
| `rules.condition` | De voorwaarden die op een bron worden toegepast. Bijvoorbeeld, als een middel een schema is, dan kan een schema bepaalde etiketten hebben op het worden toegepast die tot bijdragen of een actie tegen dat schema toelaatbaar of ontoelaatbaar is. |
| `rules.action` | De handeling die een onderwerp mag uitvoeren tegen een bron met vragen. Mogelijke waarden zijn: `read` , `create` , `edit` en `delete` . |

## Beleidsdetails opzoeken op ID {#lookup}

Maak een verzoek van de GET aan het `/policies` eindpunt terwijl het verstrekken van een beleidsidentiteitskaart in de verzoekweg om informatie over dat individuele beleid terug te winnen.

**API formaat**

```http
GET /policies/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {POLICY_ID} | De id van het beleid dat u wilt ophalen. |

**Verzoek**

Het volgende verzoek wint informatie over een individueel beleid terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een succesvol verzoek keert informatie over gevraagde beleidsidentiteitskaart terug.

```json
{
  "policies": [
    {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
      "createdBy": "example@AdobeID",
      "createdAt": 1652892767559,
      "modifiedBy": "example@AdobeID",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/xql/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.read",
            "com.adobe.action.write",
            "com.adobe.action.view"
          ]
        },
        {
          "effect": "Permit",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/*/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.delete"
          ]
        },
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
          "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
          "actions": [
            "com.adobe.action.write"
          ]
        }
      ],
      "etag": "\"0300593f-0000-0200-0000-62852ff80000\""
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met een beleid. Deze id wordt automatisch gegenereerd en kan worden gebruikt om een beleid op te zoeken, bij te werken en te verwijderen. |
| `imsOrgId` | De organisatie waar het betwiste beleid toegankelijk is. |
| `createdBy` | De id van de gebruiker die het beleid heeft gemaakt. |
| `createdAt` | Het tijdstip waarop het beleid is gemaakt. De eigenschap `createdAt` wordt weergegeven in een tijdstempel van één tijdperk. |
| `modifiedBy` | De id van de gebruiker die het beleid voor het laatst heeft bijgewerkt. |
| `modifiedAt` | De tijd waarop het beleid voor het laatst is bijgewerkt. De eigenschap `modifiedAt` wordt weergegeven in een tijdstempel van één tijdperk. |
| `name` | De naam van het beleid. |
| `description` | (Optioneel) Een eigenschap die kan worden toegevoegd voor meer informatie over een bepaald beleid. |
| `status` | De huidige status van een beleid. Deze eigenschap definieert of een beleid momenteel `active` of `inactive` is. |
| `subjectCondition` | De voorwaarden die op een onderwerp van toepassing zijn. Een onderwerp is een gebruiker met bepaalde attributen die om toegang tot een middel vragen om een actie uit te voeren. In dit geval is `subjectCondition` queryachtige voorwaarden die worden toegepast op de onderwerpkenmerken. |
| `rules` | De set regels die een beleid definiëren. De regels bepalen welke kenmerkcombinaties worden geoorloofd opdat het onderwerp een actie aan het middel met succes uitvoert. |
| `rules.effect` | Het effect dat ontstaat na het overwegen van waarden voor `action` , `condition` en `resource` . Mogelijke waarden zijn: `permit` , `deny` of `indeterminate` . |
| `rules.resource` | Het element dat of het object dat een onderwerp kan of kan benaderen.  Bronnen kunnen bestanden, toepassingen, servers of zelfs API&#39;s zijn. |
| `rules.condition` | De voorwaarden die op een bron worden toegepast. Bijvoorbeeld, als een middel een schema is, dan kan een schema bepaalde etiketten hebben op het worden toegepast die tot bijdragen of een actie tegen dat schema toelaatbaar of ontoelaatbaar is. |
| `rules.action` | De handeling die een onderwerp mag uitvoeren tegen een bron met vragen. Mogelijke waarden zijn: `read` , `create` , `edit` en `delete` . |


## Een beleid maken {#create}

Om een nieuw beleid tot stand te brengen, doe een verzoek van de POST aan het `/policies` eindpunt.

**API formaat**

```http
POST /policies
```

**Verzoek**

Met de volgende aanvraag wordt een nieuw beleid gemaakt met de naam `acme-integration-policy` .

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "com.adobe.action.read"
          ]
        }
      ]
    }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De naam van het beleid. |
| `description` | (Optioneel) Een eigenschap die kan worden toegevoegd voor meer informatie over een bepaald beleid. |
| `imsOrgId` | De organisatie die het beleid bevat. |
| `rules` | De set regels die een beleid definiëren. De regels bepalen welke kenmerkcombinaties worden geoorloofd opdat het onderwerp een actie aan het middel met succes uitvoert. |
| `rules.effect` | Het effect dat ontstaat na het overwegen van waarden voor `action` , `condition` en `resource` . Mogelijke waarden zijn: `permit` , `deny` of `indeterminate` . |
| `rules.resource` | Het element dat of het object dat een onderwerp kan of kan benaderen.  Bronnen kunnen bestanden, toepassingen, servers of zelfs API&#39;s zijn. |
| `rules.condition` | De voorwaarden die op een bron worden toegepast. Bijvoorbeeld, als een middel een schema is, dan kan een schema bepaalde etiketten hebben op het worden toegepast die tot bijdragen of een actie tegen dat schema toelaatbaar of ontoelaatbaar is. |
| `rules.action` | De handeling die een onderwerp mag uitvoeren tegen een bron met vragen. Mogelijke waarden zijn: `read` , `create` , `edit` en `delete` . |

**Reactie**

Een succesvol verzoek keert het pas gecreëerde beleid, met inbegrip van zijn unieke beleidsidentiteitskaart en bijbehorende regels terug.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met een beleid. Deze id wordt automatisch gegenereerd en kan worden gebruikt om een beleid op te zoeken, bij te werken en te verwijderen. |
| `name` | De naam van een beleid. |
| `rules` | De set regels die een beleid definiëren. De regels bepalen welke kenmerkcombinaties worden geoorloofd opdat het onderwerp een actie aan het middel met succes uitvoert. |
| `rules.effect` | Het effect dat ontstaat na het overwegen van waarden voor `action` , `condition` en `resource` . Mogelijke waarden zijn: `permit` , `deny` of `indeterminate` . |
| `rules.resource` | Het element dat of het object dat een onderwerp kan of kan benaderen.  Bronnen kunnen bestanden, toepassingen, servers of zelfs API&#39;s zijn. |
| `rules.condition` | De voorwaarden die op een bron worden toegepast. Bijvoorbeeld, als een middel een schema is, dan kan een schema bepaalde etiketten hebben op het worden toegepast die tot bijdragen of een actie tegen dat schema toelaatbaar of ontoelaatbaar is. |
| `rules.action` | De handeling die een onderwerp mag uitvoeren tegen een bron met vragen. Mogelijke waarden zijn: `read` , `create` , `edit` en `delete` . |


## Een beleid bijwerken op basis van beleids-id {#put}

Om de regels van een individueel beleid bij te werken, doe een verzoek van de PUT aan het `/policies` eindpunt terwijl het verstrekken van identiteitskaart van het beleid dat u in de verzoekweg wilt bijwerken.

**API formaat**

```http
PUT /policies/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {POLICY_ID} | De id van het beleid dat u wilt bijwerken. |

**Verzoek**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "com.adobe.action.read"
        ]
      }
    ]
  }'
```

**Reactie**

Een geslaagde reactie retourneert het bijgewerkte beleid.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Beleidseigenschappen bijwerken {#patch}

Om de eigenschappen van een individueel beleid bij te werken, doe een verzoek van PATCH aan het `/policies` eindpunt terwijl het verstrekken van identiteitskaart van het beleid dat u in de verzoekweg wilt bijwerken.

**API formaat**

```http
PATCH /policies/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {POLICY_ID} | De id van het beleid dat u wilt bijwerken. |

**Verzoek**

De volgende aanvraag vervangt de waarde van `/description` in beleids-id `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
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

Een succesvolle reactie keert identiteitskaart van het gevraagd beleid met bijgewerkte beschrijving terug.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Een beleid verwijderen {#delete}

Om een beleid te schrappen, doe een verzoek van DELETE aan het `/policies` eindpunt terwijl het verstrekken van identiteitskaart van het beleid u wilt schrappen.

**API formaat**

```http
DELETE /policies/{POLICY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| {POLICY_ID} | De id van het beleid dat u wilt verwijderen. |

**Verzoek**

Met de volgende aanvraag wordt het beleid met de id `c3863937-5d40-448d-a7be-416e538f955e` verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan het beleid te proberen. U ontvangt de HTTP-status 404 (Niet gevonden) omdat het beleid is verwijderd uit het beheer.
