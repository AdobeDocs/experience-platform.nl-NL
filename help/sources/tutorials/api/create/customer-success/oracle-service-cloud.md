---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Service Cloud;oracle service cloud
title: Een Oracle Service Cloud Source Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform met de Flow Service API kunt verbinden met Oracle Service Cloud.
exl-id: 00c0bc9c-a740-4bab-a882-2cfed8abe758
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Een Oracle Service Cloud-bronverbinding maken met de [!DNL Flow Service] API

>[!WARNING]
>
>De bron [!DNL Oracle Service Cloud] wordt eind juni 2025 vervangen.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor de Wolk van de Dienst van het Oracle tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met de Oracle Service Cloud met de API [!DNL Flow Service] .

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met Oracle Service Cloud als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De host-URL van uw Oracle Service Cloud-instantie. |
| `username` | De gebruikersnaam voor uw Oracle Service Cloud-gebruikersaccount. |
| `password` | Het wachtwoord voor uw Oracle Service Cloud-account. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor Oracle Service Cloud is: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` . |

Voor meer informatie bij het voor authentiek verklaren van uw rekening van de Wolk van de Dienst van het Oracle, verwijs naar de [[!DNL Oracle]  gids op authentificatie ](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw de authentificatiegeloofsbrieven van de Wolk van de Dienst van het Oracle als deel van de verzoekparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor de Cloud van de service Oracle gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | De host-URL van uw Oracle Service Cloud-instantie. |
| `auth.params.username` | De gebruikersnaam die is gekoppeld aan uw Oracle Service Cloud-account. |
| `auth.params.password` | Het wachtwoord dat is gekoppeld aan uw Oracle Service Cloud-account. |
| `connectionSpec.id` | De Oracle Service Cloud connection specification ID: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een basisverbinding met de Oracle Service Cloud gemaakt met de API [!DNL Flow Service] . U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van het klantensucces aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/customer-success.md)
