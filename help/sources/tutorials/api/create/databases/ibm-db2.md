---
keywords: Experience Platform;home;populaire onderwerpen;IBM [!DNL IBM DB2];IBM;ibm [!DNL IBM DB2];[!DNL IBM DB2];[!DNL IBM DB2]
solution: Experience Platform
title: Een IBM [!DNL IBM DB2] Basisverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u IBM [!DNL IBM DB2] met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Een IBM [!DNL IBM DB2]-basisverbinding maken met de [!DNL Flow Service]-API

>[!NOTE]
>
>De IBM [!DNL IBM DB2]-connector bevindt zich in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL IBM DB2] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele instantie van het Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met [!DNL IBM DB2] met de [!DNL Flow Service]-API tot stand te brengen.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `server` | De naam van de [!DNL IBM DB2]-server. U kunt het poortnummer opgeven na de servernaam die is gescheiden door een dubbele punt. Bijvoorbeeld: server:poort. |
| `database` | De naam van de [!DNL IBM DB2]-database. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de [!DNL IBM DB2]-database. |
| `password` | Het wachtwoord voor de gebruikersaccount die u voor de gebruikersnaam hebt opgegeven. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL IBM DB2] is `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

Raadpleeg [this [!DNL IBM DB2] document](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html) voor meer informatie over aan de slag gaan.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL IBM DB2] authentificatiegeloofsbrieven als deel van de verzoekparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL IBM DB2]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die is gekoppeld aan uw [!DNL IBM DB2]-account. |
| `connectionSpec.id` | De [!DNL IBM DB2] ID van de verbindingsspecificatie: `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een IBM [!DNL IBM DB2]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u databases kunt [verkennen met behulp van de Flow Service API](../../explore/database-nosql.md).
