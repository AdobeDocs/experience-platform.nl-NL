---
keywords: Experience Platform;home;populaire onderwerpen; File Transfer Protocol; protocol voor bestandsoverdracht
solution: Experience Platform
title: Een FTP-basisverbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een FTP-server (File Transfer Protocol) met behulp van de Flow Service API.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Een FTP-basisverbinding maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De FTP-connector bevindt zich in bèta. De functies en documentatie kunnen worden gewijzigd. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL FTP] (het Protocol van de Overdracht van het Dossier) tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een [!DNL FTP] -server via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL FTP] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan de [!DNL FTP] -server is gekoppeld. |
| `username` | De gebruikersnaam met toegang tot de [!DNL FTP] -server. |
| `password` | Het wachtwoord voor uw [!DNL FTP] -server. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL FTP] is: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` . |

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL FTP] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL FTP] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.host` | De hostnaam van uw FTP-server. |
| `auth.params.username` | De gebruikersnaam die aan uw FTP-server is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw FTP-server is gekoppeld. |
| `connectionSpec.id` | De specificatie-id voor de FTP-serververbinding: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Reactie**

Een succesvolle reactie keert unieke herkenningsteken (`id`) van de pas gecreëerde verbinding terug. Deze id is vereist om uw FTP-server te verkennen in de volgende zelfstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een FTP-verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsidentiteitskaart gebruiken om [ wolkenopslag te onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
