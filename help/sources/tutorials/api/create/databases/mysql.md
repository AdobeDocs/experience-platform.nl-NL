---
title: MySQL met Experience Platform verbinden met behulp van de Flow Service API
description: Leer hoe u uw MySQL-database met API's kunt verbinden met Experience Platform.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL MySQL]

Lees deze gids om te leren hoe te om uw [!DNL MySQL] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL MySQL] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Lees het [[!DNL MySQL]  overzicht &#x200B;](../../../../connectors/databases/mysql.md#prerequisites) voor informatie over authentificatie.

### Experience Platform API&#39;s gebruiken

Lees de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md) voor informatie over hoe te met succes vraag aan Experience Platform APIs maken.

## Verbind [!DNL MySQL] met Experience Platform op Azure {#azure}

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL MySQL] -account kunt verbinden met Experience Platform on Azure.

### Een basisverbinding maken voor [!DNL MySQL] op Experience Platform in Azure {#azure-base}

Een basisverbinding koppelt uw bron aan Experience Platform, die authentificatiedetails, verbindingsstatus, en een unieke identiteitskaart opslaat. Met deze id kunt u door bronbestanden bladeren en specifieke items identificeren die u wilt invoeren, inclusief de gegevenstypen en indelingen.

**API formaat**

```https
POST /connections
```

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de verificatiegegevens van [!DNL MySQL] op als onderdeel van de aanvraagparameters.

>[!BEGINTABS]

>[!TAB  Reeks gebaseerde authentificatie van de Verbinding ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL MySQL] gemaakt met verificatie op basis van een verbindingstekenreeks.

+++aanvraagvoorbeeld weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.connectionString` | De [!DNL MySQL] verbindingstekenreeks die aan uw account is gekoppeld. Het patroon van de [!DNL MySQL] verbindingstekenreeks is: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` . |
| `connectionSpec.id` | The [!DNL MySQL] connection specification ID: `26d738e0-8963-47ea-aadf-c60de735468a` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB  Basisauthentificatie ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor een [!DNL MySQL] -bron gemaakt met behulp van basisverificatie.

+++aanvraagvoorbeeld weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "DISABLED"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.server` | De naam of IP van uw [!DNL MySQL] database. |
| `auth.params.database` | De naam van uw database. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw database. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw database. |
| `auth.params.sslMode` | De methode waarmee gegevens tijdens gegevensoverdracht worden gecodeerd. |
| `connectionSpec.id` | De [!DNL MySQL] -id van de verbindingsspecificatie is: `26d738e0-8963-47ea-aadf-c60de735468a` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Verbinden [!DNL MySQL] met Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../../../landing/multi-cloud.md).

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL MySQL] -account kunt verbinden met Experience Platform op AWS.

### Een basisverbinding maken voor [!DNL MySQL] op Experience Platform op AWS {#aws-base}

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL MySQL] gemaakt om verbinding te maken met Experience Platform op AWS.

+++aanvraagvoorbeeld weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.server` | De naam of IP van uw [!DNL MySQL] database. |
| `auth.params.database` | De naam van uw database. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw database. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw database. |
| `auth.params.sslMode` | Een Booleaanse waarde die bepaalt of SSL wordt afgedwongen, afhankelijk van uw serverondersteuning. Deze configuratie is standaard ingesteld op `false` . |
| `connectionSpec.id` | De [!DNL MySQL] -id van de verbindingsspecificatie is: `26d738e0-8963-47ea-aadf-c60de735468a` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Een gegevensstroom maken voor [!DNL MySQL] -gegevens

Nu u met succes uw [!DNL MySQL] gegevensbestand hebt verbonden, kunt u [&#x200B; nu tot een dataflow leiden en gegevens van uw gegevensbestand in Experience Platform &#x200B;](../../collect/database-nosql.md) opnemen.