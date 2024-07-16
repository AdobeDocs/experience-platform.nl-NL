---
title: Een SFTP-basisverbinding maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met een SFTP-server (Secure File Transfer Protocol) met behulp van de Flow Service API.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# Een SFTP-basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL SFTP] (Veilig Protocol van de Overdracht van het Dossier) tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

>[!IMPORTANT]
>
>Het wordt aangeraden nieuwe regels of regeleinden te vermijden bij het invoeren van JSON-objecten met een [!DNL SFTP] -bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een [!DNL SFTP] -server via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL SFTP] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan de [!DNL SFTP] -server is gekoppeld. |
| `port` | De SFTP-serverpoort waarmee u verbinding maakt. Als deze waarde niet wordt opgegeven, wordt deze standaard ingesteld op `22` . |
| `username` | De gebruikersnaam met toegang tot de [!DNL SFTP] -server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP] -server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als de `privateKeyContent` met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van de inhoud van de persoonlijke sleutel als waarde. |
| `maxConcurrentConnections` | Met deze parameter kunt u een maximumlimiet opgeven voor het aantal gelijktijdige verbindingen dat Platform maakt wanneer verbinding wordt gemaakt met uw SFTP-server. U moet deze waarde instellen op een waarde die kleiner is dan de limiet die door SFTP is ingesteld. **Nota**: Wanneer dit het plaatsen voor een bestaande rekening van SFTP wordt toegelaten, zal het slechts toekomstige dataflows en niet bestaande dataflows beïnvloeden. |
| `folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. [!DNL SFTP] bron, kunt u het omslagweg verstrekken om gebruikerstoegang tot subomslag van uw keus te specificeren. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL SFTP] is: `b7bf2577-4520-42c9-bae9-cad01560f7bc` . |

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL SFTP] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

De [!DNL SFTP] -bron ondersteunt zowel basisverificatie als verificatie via de openbare SSH-sleutel. Tijdens deze stap kunt u ook het pad naar de submap aangeven waartoe u toegang wilt verlenen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL SFTP] -verificatiegegevens op als onderdeel van de aanvraagparameters.

>[!IMPORTANT]
>
>De [!DNL SFTP] schakelaar steunt een sleutel van RSA of DSA type OpenSSH. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"` . Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.maxConcurrentConnections` | Het maximumaantal gezamenlijke verbindingen dat is opgegeven bij het verbinden van Platform met SFTP. Wanneer deze optie is ingeschakeld, moet deze waarde op ten minste 1 worden ingesteld. |
| `auth.params.folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. |
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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `auth.params.passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `auth.params.maxConcurrentConnections` | Het maximumaantal gezamenlijke verbindingen dat is opgegeven bij het verbinden van Platform met SFTP. Wanneer deze optie is ingeschakeld, moet deze waarde op ten minste 1 worden ingesteld. |
| `auth.params.folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. |
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
