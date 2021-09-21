---
keywords: Experience Platform;thuis;populaire onderwerpen;Snowflake;snowflake
solution: Experience Platform
title: Een Snowflake Base-verbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform met de Flow Service API kunt verbinden met Snowflake.
source-git-commit: 5e2301a409f04bd4e23888648f244918b871f0ad
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Een [!DNL Snowflake] basisverbinding maken met de [!DNL Flow Service]-API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL Snowflake] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

De volgende sectie bevat aanvullende informatie die u moet weten om een verbinding met [!DNL Snowflake] met de API [!DNL Flow Service] tot stand te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL Snowflake], moet u de volgende verbindingseigenschappen opgeven:

| Credentials | Beschrijving |
| --- | --- |
| `account` | De [!DNL Snowflake]-account die u wilt verbinden met Platform. |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens over aan Platform. |
| `database` | De [!DNL Snowflake] bevat de gegevens die u het Platform wilt brengen. |
| `username` | De gebruikersnaam voor de [!DNL Snowflake]-account. |
| `password` | Het wachtwoord voor de [!DNL Snowflake] gebruikersaccount. |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met uw [!DNL Snowflake]-instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Snowflake] is `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Raadpleeg dit [[!DNL Snowflake] document](https://docs.snowflake.com/en/user-guide/oauth-custom.html) voor meer informatie over aan de slag gaan.

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Snowflake] authentificatiegeloofsbrieven als deel van het verzoeklichaam.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL Snowflake]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Snowflake base connection",
        "description": "Snowflake base connection",
        "auth": {
            "specName": "Basic Authentication for Snowflake,
            "params": {
                "connectionString": "{CONNECTION_STRING}"
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
| `auth.params.connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met uw [!DNL Snowflake]-instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | De [!DNL Snowflake] ID van de verbindingsspecificatie: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Antwoord**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Door deze zelfstudie te volgen hebt u een [!DNL Snowflake]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsID in de volgende zelfstudie gebruiken aangezien u leert hoe te om [gegevensbestanden te onderzoeken gebruikend de Dienst API van de Stroom](../../explore/database-nosql.md).