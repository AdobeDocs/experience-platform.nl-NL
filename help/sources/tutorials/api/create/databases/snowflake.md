---
title: Creeer een Verbinding van de Basis van de Snowflake gebruikend de Dienst API van de Stroom
description: Leer hoe u Adobe Experience Platform met Snowflake kunt verbinden met behulp van de Flow Service API.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: d89e0c81bd250e41a863b8b28d358cc6ddea1c37
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 2%

---

# Een [!DNL Snowflake] basisverbinding maken met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De [!DNL Snowflake] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Gebruik het volgende leerprogramma leren hoe te om een basisverbinding voor [!DNL Snowflake] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

In de volgende sectie vindt u aanvullende informatie die u moet weten als u verbinding wilt maken met [!DNL Snowflake] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

U moet waarden opgeven voor de volgende referentie-eigenschappen om de [!DNL Snowflake] -bron te verifiëren.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

| Credentials | Beschrijving |
| ---------- | ----------- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de gids bij [ het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Platform overbrengt. |
| `database` | De [!DNL Snowflake] -database bevat de gegevens die u voor het platform wilt gebruiken. |
| `username` | De gebruikersnaam voor de [!DNL Snowflake] -account. |
| `password` | Het wachtwoord voor de [!DNL Snowflake] -gebruikersaccount. |
| `role` | De standaardtoegangsbeheerrol die in de [!DNL Snowflake] -sessie moet worden gebruikt. De rol zou een bestaande moeten zijn die reeds aan de gespecificeerde gebruiker is toegewezen. De standaardrol is `PUBLIC` . |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Snowflake] . Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB  zeer belangrijk-paar authentificatie ]

Als u sleutelparverificatie wilt gebruiken, moet u een 2048-bits RSA-sleutelpaar genereren en de volgende waarden opgeven wanneer u een account voor uw [!DNL Snowflake] -bron maakt.

| Credentials | Beschrijving |
| --- | --- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de gids bij [ het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| `privateKey` | De [!DNL Base64-] gecodeerde privé sleutel van uw [!DNL Snowflake] rekening. U kunt gecodeerde of niet-gecodeerde persoonlijke sleutels genereren. Als u een gecodeerde persoonlijke sleutel gebruikt, moet u ook een persoonlijke-sleutelwachtwoord opgeven wanneer u verificatie uitvoert op basis van een Experience Platform. Lees de gids op [ het terugwinnen van uw  [!DNL Snowflake]  privé sleutel ](../../../../connectors/databases/snowflake.md) voor meer informatie. |
| `privateKeyPassphrase` | Persoonlijke sleutel passphrase is een extra laag van veiligheid die u moet gebruiken wanneer het voor authentiek verklaren met een gecodeerde privé sleutel. U hoeft de wachtwoordzin niet op te geven als u een niet-gecodeerde persoonlijke sleutel gebruikt. |
| `database` | De [!DNL Snowflake] -database die de gegevens bevat die u aan het Experience Platform wilt toevoegen. |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar het Experience Platform overbrengt. |

Voor meer informatie over deze waarden, verwijs de [[!DNL Snowflake]  sleutel-paar authentificatiegids ](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>U moet de markering `PREVENT_UNLOAD_TO_INLINE_URL` instellen op `FALSE` om het verwijderen van gegevens uit uw [!DNL Snowflake] -database naar het Experience Platform toe te staan.

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Snowflake] -verificatiegegevens op als onderdeel van de aanvraaginstantie.

**API formaat**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB  ConnectionString ]

+++verzoek

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Snowflake] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Snowflake] . Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` . |
| `connectionSpec.id` | The [!DNL Snowflake] connection specification ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3` . |

+++

+++Response

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB  zeer belangrijk-paar authentificatie met gecodeerde privé sleutel ]

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.account` | De naam van uw [!DNL Snowflake] account. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Snowflake] -account is gekoppeld. |
| `auth.params.database` | De [!DNL Snowflake] -database vanwaar de gegevens worden opgehaald. |
| `auth.params.privateKey` | De [!DNL Base64-] gecodeerde gecodeerde gecodeerde privé sleutel van uw [!DNL Snowflake] rekening. |
| `auth.params.privateKeyPassphrase` | De passphrase die met uw privé sleutel beantwoordt. |
| `auth.params.warehouse` | Het [!DNL Snowflake] -pakhuis dat u gebruikt. |
| `connectionSpec.id` | The [!DNL Snowflake] connection specification ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3` . |

+++

+++Response

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB  zeer belangrijk-paar authentificatie met niet gecodeerde privé sleutel ]

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.account` | De naam van uw [!DNL Snowflake] account. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Snowflake] -account is gekoppeld. |
| `auth.params.database` | De [!DNL Snowflake] -database vanwaar de gegevens worden opgehaald. |
| `auth.params.privateKey` | De [!DNL Base64-] gecodeerde niet gecodeerde privé sleutel van uw [!DNL Snowflake] rekening. |
| `auth.params.warehouse` | Het [!DNL Snowflake] -pakhuis dat u gebruikt. |
| `connectionSpec.id` | The [!DNL Snowflake] connection specification ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3` . |

+++

+++Response

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

Aan de hand van deze zelfstudie hebt u een [!DNL Snowflake] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
