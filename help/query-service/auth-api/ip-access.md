---
keywords: Experience Platform; veiligheid; ip-toegang; QS-Auth; API gids; vraagdienst; IP waaiers
title: IP Eindpunt van de Toegang
description: Leer hoe te om IP waaiers voor zandbaktoegang in de Dienst van de Vraag te beheren gebruikend het IP API eindpunt van de Toegang.
role: Developer
source-git-commit: 23e5260133f0f16ac30d14346c227a21f251b7e1
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# IP-toegangseindpunt

Om gegevenstoegang binnen een gespecificeerde zandbak van de Dienst van de Vraag te beveiligen, gebruik het IP eindpunt van de Toegang om toegestane IP waaiers te beheren. U kunt deze API gebruiken om IP waaiers te halen, te vormen of te schrappen verbonden aan identiteitskaart van uw organisatie.

U kunt de volgende handelingen uitvoeren met de API voor IP-toegang:

- **Vets alle IP waaiers**
- **plaats nieuwe IP waaiers**
- **Schrap bestaande IP waaiers**

Dit document behandelt de verzoeken en reacties die u kunt maken en ontvangen van het `/security/ip-access` eindpunt.

>[!NOTE]
>
>U moet een gebruikerstoken hebben om deze API te roepen. Zie [ begonnen gids ](./getting-started.md) voor informatie bij het verwerven van de vereiste waarden voor elk van de kopballen.

## Alle IP-bereiken ophalen {#fetch-all-ip-ranges}

Haal een lijst op van alle IP waaiers die voor uw zandbak worden gevormd. Als geen IP waaiers worden geplaatst, worden alle IPs toegestaan door gebrek, en de reactie keert een lege lijst in `allowedIpRanges` terug.

**API formaat**

```http
GET /security/ip-access
```

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van de toegestane IP-bereiken van de sandbox.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

De volgende tabel bevat een beschrijving en een voorbeeld van de eigenschappen van het reactieschema:

| Eigenschap | Beschrijving | Voorbeeld |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | Organisatie-id voor de sandbox. | `{ORG_ID}` |
| `sandboxName` | Naam van de zandbak waar IP beperkingen van toepassing zijn. | `prod` |
| `channel` | De toegangswijze voor IP beperkingen. Momenteel is de enige toegestane waarde `data_distiller` . Deze waarde betekent dat IP-beperkingen worden toegepast op PSQL- of JDBC-verbindingen. | `data_distiller` |
| `allowedIpRanges` | Lijst van toegelaten IPs in of CIDR of vaste IP formaat. Elke vermelding kan een facultatieve beschrijving bevatten. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>Het veld `allowedIpRanges` kan twee typen IP-specificaties bevatten: <br><ul><li>**CIDR.**: StandaardCIDR aantekening (bijvoorbeeld, `"136.23.110.0/23"`) om IP waaiers te bepalen.</li><li>**Vaste IP**: Enige IPs voor individuele toegangstoestemmingen (bijvoorbeeld, `"101.10.1.1"`).</li></ul>

## Nieuwe IP-bereiken instellen

Overschrijf bestaande IP waaiers door een nieuwe lijst voor de zandbak te plaatsen. Deze verrichting vereist een volledige lijst van IP waaiers, met inbegrip van om het even welke die onveranderd blijven.

**API formaat**

```http
PUT /security/ip-access
```

**Verzoek**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met details van de onlangs gevormde IP waaiers terug.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## IP-bereiken verwijderen {#delete-ip-ranges}

Verwijder alle gevormde IP waaiers voor de zandbak. Deze actie schrapt de IP waaiers en keert de geschrapte IP lijst terug.

>[!NOTE]
>
>De schrappingsverrichting is op organisatie (`imsOrg`) identiteitskaart van toepassing en beïnvloedt alle IP waaiers die voor de zandbak worden gevormd.

**API formaat**

```http
DELETE /security/ip-access
```

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met details van de geschrapte IP waaiers terug.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

