---
title: Een SFTP-basisverbinding maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met een SFTP-server (Secure File Transfer Protocol) met behulp van de Flow Service API.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Een SFTP-basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL SFTP] (Veilig Protocol van de Overdracht van het Dossier) tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

>[!IMPORTANT]
>
>Het wordt aangeraden nieuwe regels of regeleinden te vermijden bij het invoeren van JSON-objecten met een [!DNL SFTP] -bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een [!DNL SFTP] -server via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Lees de [[!DNL SFTP]  authentificatiegids ](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) voor gedetailleerde stappen op hoe te om uw authentificatiegeloofsbrieven terug te winnen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL SFTP] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

De [!DNL SFTP] -bron ondersteunt zowel basisverificatie als verificatie via de openbare SSH-sleutel. Tijdens deze stap kunt u ook het pad naar de submap aangeven waartoe u toegang wilt verlenen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL SFTP] -verificatiegegevens op als onderdeel van de aanvraagparameters.

>[!IMPORTANT]
>
>De [!DNL SFTP] -connector ondersteunt `ed25519` , `RSA` - of `DSA` OpenSSH-toets. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"` . Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

**API formaat**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.host` | De hostnaam van uw SFTP-server. |
| `auth.params.port` | De poort van de SFTP-server. Deze gehele waarde is standaard ingesteld op 22. |
| `auth.params.username` | De gebruikersnaam die aan uw SFTP-server is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw SFTP-server is gekoppeld. |
| `auth.params.maxConcurrentConnections` | Het maximumaantal gezamenlijke verbindingen dat is opgegeven bij het verbinden van Experience Platform met SFTP. Wanneer deze optie is ingeschakeld, moet deze waarde op ten minste 1 worden ingesteld. |
| `auth.params.folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. |
| `auth.params.disableChunking` | Een booleaanse waarde die wordt gebruikt om te bepalen of uw SFTP-server chunking ondersteunt. |
| `connectionSpec.id` | De specificatie-id voor de SFTP-serververbinding: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Response

Een succesvolle reactie keert unieke herkenningsteken (`id`) van de pas gecreëerde verbinding terug. Deze id is vereist om uw SFTP-server te verkennen in de volgende zelfstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB  SSH openbare zeer belangrijke authentificatie ]

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
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.host` | De hostnaam van de [!DNL SFTP] -server. |
| `auth.params.port` | De poort van de SFTP-server. Deze gehele waarde is standaard ingesteld op 22. |
| `auth.params.username` | De gebruikersnaam die aan de [!DNL SFTP] -server is gekoppeld. |
| `auth.params.privateKeyContent` | De Base64-gecodeerde inhoud van de privé sleutel van SSH. De ondersteunde OpenSSH-sleuteltypen zijn `ed25519` , `RSA` en `DSA` . |
| `auth.params.passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `auth.params.maxConcurrentConnections` | Het maximumaantal gezamenlijke verbindingen dat is opgegeven bij het verbinden van Experience Platform met SFTP. Wanneer deze optie is ingeschakeld, moet deze waarde op ten minste 1 worden ingesteld. |
| `auth.params.folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. |
| `auth.params.disableChunking` | Een booleaanse waarde die wordt gebruikt om te bepalen of uw SFTP-server chunking ondersteunt. |
| `connectionSpec.id` | De [!DNL SFTP] server connection specification ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Response

Een succesvolle reactie keert unieke herkenningsteken (`id`) van de pas gecreëerde verbinding terug. Deze id is vereist om uw SFTP-server te verkennen in de volgende zelfstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL SFTP] -verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsidentiteitskaart gebruiken om [ wolkenopslag te onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
