---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Een SFTP-connector maken met de Flow Service API
topic: overview
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform te verbinden met een SFTP-server (Secure File Transfer Protocol).
translation-type: tm+mt
source-git-commit: 71653681a0f4b31319bd352202bf55fb3947a455
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---


# Een SFTP-connector maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De SFTP-connector bevindt zich in bèta. De functies en documentatie kunnen worden gewijzigd. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen om verbinding te maken [!DNL Experience Platform] met een SFTP-server (Secure File Transfer Protocol).

Als u liever de gebruikersinterface in wilt gebruiken, [!DNL Experience Platform]biedt de [UI-zelfstudie](../../../ui/create/cloud-storage/ftp-sftp.md) stapsgewijze instructies voor het uitvoeren van vergelijkbare acties.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een SFTP-server met behulp van de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Als u verbinding wilt maken [!DNL Flow Service] met SFTP, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan uw SFTP-server is gekoppeld. |
| `username` | De gebruikersnaam met toegang tot uw SFTP-server. |
| `password` | Het wachtwoord voor uw SFTP-server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. De OpenSSH-indeling (RSA/DSA) voor de persoonlijke sleutel van SSH. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot de [!DNL Flow Service]sandboxen behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per SFTP-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken die verschillende gegevens kunnen inbrengen.

### Een SFTP-verbinding maken met behulp van basisverificatie

Om een verbinding tot stand te brengen SFTP gebruikend basisauthentificatie, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van waarden voor uw verbinding `host`, `userName`, en `password`.

**API-indeling**

```http
POST /connections
```

**Verzoek**

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

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe verbinding. Deze id is vereist om uw SFTP-server te verkennen in de volgende zelfstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Een SFTP-verbinding maken met SSH-verificatie met openbare sleutel

Om een verbinding tot stand te brengen SFTP gebruikend de openbare zeer belangrijke authentificatie van SSH, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van waarden voor uw verbinding `host`, `userName`, `privateKeyContent`, en `passPhrase`.

**API-indeling**

```http
POST /connections
```

**Verzoek**

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
| `auth.params.host` | De hostnaam van uw SFTP-server. |
| `auth.params.username` | De gebruikersnaam die aan uw SFTP-server is gekoppeld. |
| `auth.params.privateKeyContent` | De basis64 gecodeerde inhoud van de privé sleutel van SSH. De OpenSSH-indeling (RSA/DSA) voor de persoonlijke sleutel van SSH. |
| `auth.params.passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `connectionSpec.id` | De specificatie-id van de SFTP-serververbinding: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe verbinding. Deze id is vereist om uw SFTP-server te verkennen in de volgende zelfstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een SFTP-verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindings-id gebruiken om cloudopslag te [verkennen met de Flow Service API](../../explore/cloud-storage.md) of [ingest parketgegevens met de Flow Service API](../../cloud-storage-parquet.md).
