---
keywords: Experience Platform;home;populaire onderwerpen;SFTP;sftp;Secure File Transfer Protocol;Secure File Transfer Protocol
solution: Experience Platform
title: Een SFTP-basisverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een SFTP-server (Secure File Transfer Protocol) met behulp van de Flow Service API.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# Een SFTP-basisverbinding maken met de [!DNL Flow Service]-API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL SFTP] (Secure File Transfer Protocol) tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

>[!IMPORTANT]
>
>Het wordt aanbevolen nieuwe regels of regeleinden te vermijden bij het opnemen van JSON-objecten met een [!DNL SFTP]-bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met een [!DNL SFTP]-server met de [!DNL Flow Service]-API tot stand te kunnen brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL SFTP], moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP adres verbonden aan uw [!DNL SFTP] server. |
| `username` | De gebruikersnaam met toegang tot uw [!DNL SFTP]-server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP]-server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als `privateKeyContent` met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met passphrase van de inhoud van de persoonlijke sleutel als waarde. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL SFTP] is: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL SFTP] authentificatiegeloofsbrieven als deel van de verzoekparameters.

### Een [!DNL SFTP]-verbinding maken met basisverificatie

Als u een [!DNL SFTP]-basisverbinding wilt maken met behulp van basisverificatie, dient u een POST-aanvraag in bij de [!DNL Flow Service]-API en geeft u waarden op voor `host`, `userName` en `password` van uw verbinding.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL SFTP] gebruikend basisauthentificatie:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
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
| `auth.params.username` | De gebruikersnaam die aan uw SFTP-server is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw SFTP-server is gekoppeld. |
| `connectionSpec.id` | De specificatie-id van de SFTP-serververbinding: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde verbinding terug. Deze id is vereist om uw SFTP-server te verkennen in de volgende zelfstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Een [!DNL SFTP]-verbinding maken met behulp van SSH-verificatie met openbare sleutel

Als u een [!DNL SFTP]-basisverbinding wilt maken met behulp van SSH-verificatie met openbare sleutel, dient u een verzoek in bij de [!DNL Flow Service]-API en geeft u waarden op voor `host`, `userName`, `privateKeyContent` en `passPhrase` van uw POST.

>[!IMPORTANT]
>
>De [!DNL SFTP] schakelaar steunt een sleutel van RSA of van het type DSA OpenSSH. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"`. Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL SFTP] gebruikend de openbare zeer belangrijke authentificatie van SSH:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
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
| `auth.params.host` | De hostnaam van uw [!DNL SFTP]-server. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL SFTP]-server is gekoppeld. |
| `auth.params.privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `auth.params.passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `connectionSpec.id` | De [!DNL SFTP]-specificatie-id voor serververbinding: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde verbinding terug. Deze id is vereist om uw [!DNL SFTP]-server in de volgende zelfstudie te verkennen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen hebt u een [!DNL SFTP]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. Met deze verbindings-id kunt u [cloudopslag verkennen met de Flow Service API](../../explore/cloud-storage.md) of [Inst Parquet-gegevens met behulp van de Flow Service API](../../cloud-storage-parquet.md).
