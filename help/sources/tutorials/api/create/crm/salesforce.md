---
keywords: Experience Platform;thuis;populaire onderwerpen;Salesforce;salesforce
solution: Experience Platform
title: Een Salesforce Base-verbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een Salesforce-account met behulp van de Flow Service API.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 8035539321f5016521208aa110a4ee2881cb5d1e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Een [!DNL Salesforce] basisverbinding maken met de [!DNL Flow Service]-API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL Salesforce] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om [!DNL Platform] met de API van [!DNL Flow Service] te kunnen verbinden met een [!DNL Salesforce]-account.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL Salesforce], moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `environmentUrl` | De URL van de broninstantie [!DNL Salesforce]. |
| `username` | De gebruikersnaam voor de [!DNL Salesforce]-gebruikersaccount. |
| `password` | Het wachtwoord voor de [!DNL Salesforce] gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de [!DNL Salesforce]-gebruikersaccount. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL AdWords] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Voor meer informatie over aan de slag gaan, bezoek [dit document van Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Salesforce] authentificatiegeloofsbrieven als deel van de verzoekparameters.


**API-indeling**

```http
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL Salesforce]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Salesforce]-account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat is gekoppeld aan uw [!DNL Salesforce]-account. |
| `auth.params.securityToken` | Het beveiligingstoken dat aan uw [!DNL Salesforce]-account is gekoppeld. |
| `connectionSpec.id` | De [!DNL Salesforce] ID van de verbindingsspecificatie: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**Antwoord**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen hebt u een [!DNL Salesforce]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken wanneer u leert hoe u CRM-systemen kunt [verkennen met behulp van de Flow Service API](../../explore/crm.md).
