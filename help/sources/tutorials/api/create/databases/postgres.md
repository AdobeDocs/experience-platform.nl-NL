---
title: Connect PostSQL aan Experience Platform met behulp van de Flow Service API
description: Leer hoe te om uw  [!DNL PostgreSQL]  gegevensbestand met Experience Platform te verbinden gebruikend APIs.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL PostgreSQL]

Lees deze gids om te leren hoe te om uw [!DNL PostgreSQL] gegevensbestand met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL PostgreSQL] via de [!DNL Flow Service] API.

### Experience Platform API&#39;s gebruiken

Lees de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md) voor informatie over hoe te met succes vraag aan Experience Platform APIs maken.

### Vereiste referenties verzamelen

Lees het [[!DNL PostgreSQL]  overzicht ](../../../../connectors/databases/postgres.md) voor meer informatie over authentificatie.

### SSL-versleuteling inschakelen voor uw verbindingstekenreeks

U kunt SSL-codering inschakelen voor de [!DNL PostgreSQL] -verbindingstekenreeks door uw verbindingstekenreeks toe te voegen met de volgende eigenschappen:

| Eigenschap | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `EncryptionMethod` | Hiermee kunt u SSL-codering inschakelen voor uw [!DNL PostgreSQL] -gegevens. | <uL><li>`EncryptionMethod=0` (Uitgeschakeld)</li><li>`EncryptionMethod=1` (Ingeschakeld)</li><li>`EncryptionMethod=6` (RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Hiermee wordt het certificaat gevalideerd dat door de [!DNL PostgreSQL] -database wordt verzonden wanneer `EncryptionMethod` wordt toegepast. | <uL><li>`ValidationServerCertificate=0` (Uitgeschakeld)</li><li>`ValidationServerCertificate=1` (Ingeschakeld)</li></ul> |

Hier volgt een voorbeeld van een [!DNL PostgreSQL] verbindingstekenreeks die is toegevoegd met SSL-codering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1` .

## Verbind [!DNL PostgreSQL] met Experience Platform op Azure {#azure}

Lees de onderstaande stappen om te leren hoe u uw [!DNL PostgreSQL] -account kunt verbinden met Experience Platform on Azure.

### Een basisverbinding maken {#azure-base}

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL PostgreSQL] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB  Op sleutel gebaseerde authentificatie van de Rekening ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL PostgreSQL] gemaakt met verificatie op basis van accountsleutels:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| ------------- | --------------- |
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL PostgreSQL] account is gekoppeld. Het patroon van de [!DNL PostgreSQL] verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}` . |
| `connectionSpec.id` | De [!DNL PostgreSQL] verbindingsspecificatie-id&#39;s: `74a1c565-4e59-48d7-9d67-7c03b8a13137` . |

+++

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde basisverbinding terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB  Basisauthentificatie ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL PostgreSQL] gemaakt met behulp van basisverificatie:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "Allow"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| ---| --- |
| `auth.params.server` | De naam of het IP-adres van uw [!DNL PostgreSQL] -database. |
| `auth.params.port` | Het poortnummer van de databaseserver. |
| `auth.params.database` | De naam van de [!DNL PostgreSQL] -database. |
| `auth.params.username` | De gebruikersnaam die is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `auth.params.password` | Het wachtwoord dat is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `auth.params.sslMode` | De methode waarmee gegevens tijdens gegevensoverdracht worden gecodeerd. De beschikbare waarden zijn: `Disable` , `Allow` , `Prefer` , `Verify Ca` en `Verify Full` . |
| `connectionSpec.id` | De [!DNL PostgreSQL] verbindingsspecificatie-id&#39;s: `74a1c565-4e59-48d7-9d67-7c03b8a13137` . |

+++

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde basisverbinding terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Verbinden [!DNL PostgreSQL] met Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../../landing/multi-cloud.md).

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL PostgreSQL] -database kunt verbinden met Experience Platform op AWS.

### Een basisverbinding maken {#aws-base}

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL PostgreSQL] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL PostgreSQL] gemaakt om verbinding te maken met Experience Platform op AWS.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| ---| --- |
| `auth.params.server` | De naam of het IP-adres van uw [!DNL PostgreSQL] -database. |
| `auth.params.port` | Het poortnummer van de databaseserver. |
| `auth.params.database` | De naam van de [!DNL PostgreSQL] -database. |
| `auth.params.username` | De gebruikersnaam die is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `auth.params.password` | Het wachtwoord dat is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `sslMode` | Een Booleaanse waarde die bepaalt of SSL wordt afgedwongen, afhankelijk van uw serverondersteuning. Deze configuratie is standaard ingesteld op `false` . |
| `connectionSpec.id` | De [!DNL PostgreSQL] verbindingsspecificatie-id&#39;s: `74a1c565-4e59-48d7-9d67-7c03b8a13137` . |

+++

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde basisverbinding terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## Volgende stappen

Nu u een verbinding hebt gemaakt tussen uw [!DNL PostgreSQL] -database en Experience Platform, kunt u nu verdergaan en de [!DNL PostgreSQL] -gegevens naar Experience Platform overbrengen. Raadpleeg de volgende documentatie voor meer informatie:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
