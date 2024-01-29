---
title: Creeer een Verbinding van de Basis van de Snowflake gebruikend de Dienst API van de Stroom
description: Leer hoe u Adobe Experience Platform met Snowflake kunt verbinden met behulp van de Flow Service API.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Een [!DNL Snowflake] basisverbinding met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De [!DNL Snowflake] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Gebruik de volgende zelfstudie om te leren hoe u een basisverbinding maakt voor [!DNL Snowflake] met de [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

De volgende sectie bevat aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Snowflake] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

U moet waarden opgeven voor de volgende referentie-eigenschappen om uw [!DNL Snowflake] bron.

>[!BEGINTABS]

>[!TAB Verificatie met accountsleutel]

| Credentials | Beschrijving |
| ---------- | ----------- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor een ander account [!DNL Snowflake] organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name`. Voor meer informatie over accountnamen leest u de [!DNL Snowflake] documentatie over [account-id&#39;s](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] Het pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens naar Platform. |
| `database` | De [!DNL Snowflake] Het gegevensbestand bevat de gegevens u het Platform wilt brengen. |
| `username` | De gebruikersnaam voor de [!DNL Snowflake] account. |
| `password` | Het wachtwoord voor de [!DNL Snowflake] gebruikersaccount. |
| `role` | De standaardtoegangsbeheerrol die in de [!DNL Snowflake] sessie. De rol zou een bestaande moeten zijn die reeds aan de gespecificeerde gebruiker is toegewezen. De standaardrol is `PUBLIC`. |
| `connectionString` | De verbindingstekenreeks waarmee u verbinding maakt met uw [!DNL Snowflake] -instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Verificatie sleutelpaar]

Om zeer belangrijk-paarauthentificatie te gebruiken, moet u een zeer belangrijk paar met 2048 bits RSA produceren en dan de volgende waarden verstrekken wanneer het creëren van een rekening voor uw [!DNL Snowflake] bron.

| Credentials | Beschrijving |
| --- | --- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor een ander account [!DNL Snowflake] organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name`. Voor meer informatie over accountnamen leest u de [!DNL Snowflake] documentatie over [account-id&#39;s](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | De gebruikersnaam van uw [!DNL Snowflake] account. |
| `privateKey` | De [!DNL Base64-]gecodeerde persoonlijke sleutel van uw [!DNL Snowflake] account. U kunt gecodeerde of niet-gecodeerde persoonlijke sleutels genereren. Als u een gecodeerde persoonlijke sleutel gebruikt, moet u ook een persoonlijke-sleutelwachtwoord opgeven wanneer u verificatie uitvoert op basis van een Experience Platform. |
| `privateKeyPassphrase` | Persoonlijke sleutel passphrase is een extra laag van veiligheid die u moet gebruiken wanneer het voor authentiek verklaren met een gecodeerde privé sleutel. U hoeft de wachtwoordzin niet op te geven als u een niet-gecodeerde persoonlijke sleutel gebruikt. |
| `database` | De [!DNL Snowflake] database die de gegevens bevat die u aan het Experience Platform wilt toevoegen. |
| `warehouse` | De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] magazijn is onafhankelijk van elkaar en moet individueel worden benaderd wanneer gegevens naar het Experience Platform worden overgebracht. |

Voor meer informatie over deze waarden raadpleegt u de [[!DNL Snowflake] sleutel-paar authentificatiegids](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>U moet de instelling `PREVENT_UNLOAD_TO_INLINE_URL` markeren naar `FALSE` om gegevens uit uw [!DNL Snowflake] database naar Experience Platform.

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL Snowflake] verificatiegegevens als onderdeel van de aanvraaginstantie.

**API-indeling**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB ConnectionString]

+++verzoek

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Snowflake]:

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
| `auth.params.connectionString` | De verbindingstekenreeks waarmee u verbinding maakt met uw [!DNL Snowflake] -instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | De [!DNL Snowflake] Verbindingsspecificatie-id: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Response

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB Sleutelparverificatie met gecodeerde persoonlijke sleutel]

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
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Snowflake] account. |
| `auth.params.database` | De [!DNL Snowflake] database vanaf waar de gegevens worden opgehaald. |
| `auth.params.privateKey` | De [!DNL Base64-]gecodeerde gecodeerde gecodeerde persoonlijke sleutel van uw [!DNL Snowflake] account. |
| `auth.params.privateKeyPassphrase` | De passphrase die met uw privé sleutel beantwoordt. |
| `auth.params.warehouse` | De [!DNL Snowflake] opslagruimte die u gebruikt. |
| `connectionSpec.id` | De [!DNL Snowflake] Verbindingsspecificatie-id: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Response

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB Sleutelpaarverificatie met niet-gecodeerde persoonlijke sleutel]

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
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Snowflake] account. |
| `auth.params.database` | De [!DNL Snowflake] database vanaf waar de gegevens worden opgehaald. |
| `auth.params.privateKey` | De [!DNL Base64-]gecodeerde niet-gecodeerde persoonlijke sleutel van uw [!DNL Snowflake] account. |
| `auth.params.warehouse` | De [!DNL Snowflake] opslagruimte die u gebruikt. |
| `connectionSpec.id` | De [!DNL Snowflake] Verbindingsspecificatie-id: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Response

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

Aan de hand van deze zelfstudie hebt u een [!DNL Snowflake] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/database-nosql.md)
