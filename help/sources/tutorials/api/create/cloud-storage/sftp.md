---
keywords: Experience Platform;home;populaire onderwerpen;SFTP;sftp;Secure File Transfer Protocol;Secure File Transfer Protocol
solution: Experience Platform
title: Een SFTP-basisverbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een SFTP-server (Secure File Transfer Protocol) met behulp van de Flow Service API.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 0%

---

# Een SFTP-basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL SFTP] (Secure File Transfer Protocol) met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

>[!IMPORTANT]
>
>Het wordt aanbevolen nieuwe regels of regeleinden te vermijden bij het innemen van JSON-objecten met een [!DNL SFTP] bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met een [!DNL SFTP] server die de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om verbinding te maken met [!DNL SFTP]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of IP adres verbonden aan uw [!DNL SFTP] server. |
| `port` | De SFTP-serverpoort waarmee u verbinding maakt. Indien niet opgegeven, wordt de waarde standaard ingesteld op `22`. |
| `username` | De gebruikersnaam met toegang tot uw [!DNL SFTP] server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP] server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als de `privateKeyContent` is met een wachtwoord beveiligd, moet deze parameter worden gebruikt met passphrase van de inhoud van de persoonlijke sleutel als waarde. |
| `maxConcurrentConnections` | Met deze parameter kunt u een maximumlimiet opgeven voor het aantal gelijktijdige verbindingen dat Platform maakt wanneer verbinding wordt gemaakt met uw SFTP-server. U moet deze waarde instellen op een waarde die kleiner is dan de limiet die door SFTP is ingesteld. **Opmerking**: Als deze instelling is ingeschakeld voor een bestaande SFTP-account, heeft dit alleen invloed op toekomstige gegevensstromen en niet op bestaande gegevensstromen. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL SFTP] is: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

De [!DNL SFTP] de bron steunt zowel basisauthentificatie als authentificatie via SSH openbare sleutel.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL SFTP] verificatiereferenties als onderdeel van de aanvraagparameters.

>[!IMPORTANT]
>
>De [!DNL SFTP] de schakelaar steunt een RSA of DSA type OpenSSH sleutel. Zorg ervoor dat de inhoud van uw sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"`. Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL SFTP]:

>[!BEGINTABS]

>[!TAB Basisverificatie]

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
              "maxConcurrentConnections": 1
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
| `auth.params.port` | De poort van de SFTP-server. Deze geheel-getalwaarde is standaard ingesteld op 22. |
| `auth.params.username` | De gebruikersnaam die aan uw SFTP-server is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw SFTP-server is gekoppeld. |
| `auth.params.maxConcurrentConnections` | Het maximumaantal gezamenlijke verbindingen dat is opgegeven bij het verbinden van Platform met SFTP. Wanneer deze optie is ingeschakeld, moet deze waarde op ten minste 1 worden ingesteld. |
| `connectionSpec.id` | De specificatie-id van de SFTP-serververbinding: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB SSH-verificatie met openbare sleutel]

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
              "maxConcurrentConnections": 1

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
| `auth.params.host` | De hostnaam van uw [!DNL SFTP] server. |
| `auth.params.port` | De poort van de SFTP-server. Deze geheel-getalwaarde is standaard ingesteld op 22. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL SFTP] server. |
| `auth.params.privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `auth.params.passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `auth.params.maxConcurrentConnections` | Het maximumaantal gezamenlijke verbindingen dat is opgegeven bij het verbinden van Platform met SFTP. Wanneer deze optie is ingeschakeld, moet deze waarde op ten minste 1 worden ingesteld. |
| `connectionSpec.id` | De [!DNL SFTP] server connection specification ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe verbinding. Deze id is vereist om uw SFTP-server te verkennen in de volgende zelfstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL SFTP] verbinding met de [!DNL Flow Service] API en hebben de unieke id-waarde van de verbinding verkregen. U kunt deze verbindings-id gebruiken om [verkennen van cloudopslag met de Flow Service API](../../explore/cloud-storage.md).
