---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Service Cloud;oracle service cloud
title: Creëer een Cloud Source Connection van de Dienst van het Oracle gebruikend de Dienst API van de Stroom
description: Leer hoe u Adobe Experience Platform met de Flow Service API kunt verbinden met Oracle Service Cloud.
source-git-commit: 078a266967cd7b0818f958283a58a8af4c886a21
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# (bèta) Maak een Cloud-bronverbinding voor Oracles met de [!DNL Flow Service] API

>[!NOTE]
>
>De Oracle Service Cloud-bron is in bèta. Zie de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor de Wolk van de Dienst van het Oracle tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met de Oracle Service Cloud via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] Als u verbinding wilt maken met Oracle Service Cloud, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De host-URL van uw Oracle Service Cloud-instantie. |
| `username` | De gebruikersnaam voor uw Oracle Service Cloud-gebruikersaccount. |
| `password` | Het wachtwoord voor uw Oracle Service Cloud-account. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor de Cloud van de Dienst van het Oracle is: `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

Raadpleeg voor meer informatie over het verifiëren van uw Oracle Service Cloud-account de [[!DNL Oracle] handleiding voor verificatie](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw de authentificatiegeloofsbrieven van de Wolk van de Dienst van het Oracle als deel van de verzoekparameters.

**API-indeling**

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
| `connectionSpec.id` | De Oracle Service Cloud-verbindingsspecificatie-id: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke id (`id`). Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een basisverbinding van de Cloud van de Dienst van het Oracle tot stand gebracht gebruikend [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een dataflow om de gegevens van het klantsucces naar het Platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/customer-success.md)
