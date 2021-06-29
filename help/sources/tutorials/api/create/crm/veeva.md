---
keywords: Experience Platform;thuis;populaire onderwerpen;veeva crm;Veeva CRM;Veeva CRM;
solution: Experience Platform
title: Een Veeva CRM-basisverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met Veeva CRM met behulp van de Flow Service API.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 9bd241d5f986759268edd072cee72d02f40f858f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# (Beta) Maak een [!DNL Veeva CRM] basisverbinding met de API [!DNL Flow Service]

>[!NOTE]
>
>De bron [!DNL Veeva CRM] is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL Veeva CRM] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met [!DNL Veeva CRM] met de [!DNL Flow Service]-API tot stand te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL Veeva CRM], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `environmentUrl` | De URL van de instantie [!DNL Veeva CRM]. |
| `username` | De gebruikersnaam van uw [!DNL Veeva CRM]-account. |
| `password` | De wachtwoordwaarde van uw [!DNL Veeva CRM]-account. |
| `securityToken` | Het beveiligingstoken voor uw [!DNL Veeva CRM]-instantie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Veeva CRM] is: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Raadpleeg dit [[!DNL Veeva CRM] document](https://developer.veevacrm.com/api/#order-management-rest-api) voor meer informatie over deze waarden.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Veeva CRM] authentificatiegeloofsbrieven als deel van de verzoekparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De naam van uw [!DNL Veeva CRM] basisverbinding. U kunt deze naam gebruiken om uw [!DNL Veeva CRM] basisverbinding te zoeken. |
| `description` | Een optionele beschrijving voor uw [!DNL Veeva CRM] basisverbinding. |
| `auth.specName` | Het verificatietype dat voor de verbinding wordt gebruikt. |
| `auth.params.environmentUrl` | De URL van de instantie [!DNL Veeva CRM]. |
| `auth.params.username` | De gebruikersnaam van uw [!DNL Veeva CRM]-account. |
| `auth.params.password` | De wachtwoordwaarde van uw [!DNL Veeva CRM]-account. |
| `auth.params.securityToken` | Het beveiligingstoken voor uw [!DNL Veeva CRM]-instantie. |
| `connectionSpec.id` | De verbindingsspecificatie-id voor [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen hebt u een [!DNL Veeva CRM] basisverbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken wanneer u leert hoe u CRM-systemen kunt [verkennen met behulp van de Flow Service API](../../explore/crm.md).
