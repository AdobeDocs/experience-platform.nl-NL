---
title: Versleutelde gegevensinsluiting
description: Leer hoe u gecodeerde bestanden via batchbronnen voor cloudopslag kunt opnemen met de API.
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: 9a5599473f874d86e2b3c8449d1f4d0cf54b672c
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# Versleutelde gegevensinvoer

U kunt gecodeerde gegevensbestanden via batchbronnen voor cloudopslag opnemen in Adobe Experience Platform. Met gecodeerde gegevensinvoer kunt u gebruikmaken van asymmetrische coderingsmechanismen om batchgegevens veilig naar het Experience Platform over te brengen. Momenteel, zijn de gesteunde asymmetrische encryptiemechanismen PGP en GPG.

De gecodeerde gegevensinvoer verloopt als volgt:

1. [ creeer een encryptiesleutel gebruikend Experience Platform APIs ](#create-encryption-key-pair). Het sleutelpaar bestaat uit een persoonlijke sleutel en een openbare sleutel. Als u een id hebt gemaakt, kunt u de openbare sleutel samen met de bijbehorende id voor de openbare sleutel en de Vervaltijd kopiëren of downloaden. Tijdens dit proces wordt de persoonlijke sleutel door het Experience Platform in een veilige kluis opgeslagen. **NOTA:** de openbare sleutel in de reactie is Base64-Gecodeerd en moet voorafgaand aan het gebruiken worden gedecodeerd.
2. Gebruik de openbare sleutel om het gegevensbestand te coderen dat u wilt opnemen.
3. Plaats het gecodeerde bestand in de cloudopslag.
4. Zodra het gecodeerde dossier klaar is, [ creeer een bronverbinding en een dataflow voor uw bron van de wolkenopslag ](#create-a-dataflow-for-encrypted-data). Tijdens de stap voor het maken van flow moet u een parameter `encryption` opgeven en uw openbare-sleutelid opnemen.
5. Het Experience Platform wint de privé sleutel van de veilige kluis terug om de gegevens op het tijdstip van inname te decrypteren.

>[!IMPORTANT]
>
>De maximale grootte van één gecodeerd bestand is 1 GB. U kunt bijvoorbeeld gegevens van 2 GB invoeren in één gegevensstroom, maar elk afzonderlijk bestand in die gegevens mag niet groter zijn dan 1 GB.

Dit document bevat stappen voor het genereren van een sleutelpaar voor versleuteling van gegevens en het invoeren van gecodeerde gegevens naar het Experience Platform met behulp van bronnen voor cloudopslag.

## Aan de slag {#get-started}

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
   * [ de opslagbronnen van de Wolk ](../api/collect/cloud-storage.md): Creeer een gegevensstroom om partijgegevens van uw bron van de wolkenopslag aan Experience Platform te brengen.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).

### Ondersteunde bestandsextensies voor gecodeerde bestanden {#supported-file-extensions-for-encrypted-files}

De lijst met ondersteunde bestandsextensies voor gecodeerde bestanden is:

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>De gecodeerde bestandsinvoer in Adobe Experience Platform Sources ondersteunt openPGP en geen specifieke merkgebonden versie van PGP.

## Versleutelingssleutelpaar maken {#create-encryption-key-pair}

>[!IMPORTANT]
>
>Coderingssleutels zijn specifiek voor een bepaalde sandbox. Daarom moet u nieuwe encryptiesleutels tot stand brengen als u gecodeerde gegevens in een verschillende zandbak, binnen uw organisatie wilt opnemen.

De eerste stap bij het invoeren van gecodeerde gegevens in het Experience Platform is het maken van een sleutelpaar voor codering door een verzoek voor een POST in te dienen bij het `/encryption/keys` -eindpunt van de [!DNL Connectors] API.

**API formaat**

```http
POST /data/foundation/connectors/encryption/keys
```

**Verzoek**

+++Voorbeeldverzoek weergeven

Het volgende verzoek produceert een encryptiesleutel gebruikend het PGP encryptiealgoritme.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-encryption",
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De naam van het sleutelpaar voor versleuteling. |
| `encryptionAlgorithm` | Het type van encryptiealgoritme dat u gebruikt. De ondersteunde coderingstypen zijn `PGP` en `GPG` . |
| `params.passPhrase` | Passphrase verstrekt een extra laag van bescherming voor uw encryptiesleutels. Op verwezenlijking, slaat het Experience Platform passphrase in een verschillend veilige kluis van de openbare sleutel op. U moet een niet-lege tekenreeks opgeven als een wachtwoordzin. |

+++

**Reactie**

+++Voorbeeldreactie van weergave

Een succesvolle reactie keert uw Base64-Gecodeerde openbare sleutel, openbare zeer belangrijke identiteitskaart, en de vervaltijd van uw sleutels terug. De verlooptijd wordt automatisch ingesteld op 180 dagen na de datum waarop de sleutel wordt gegenereerd. Vervaltijd kan momenteel niet worden geconfigureerd.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `publicKey` | De openbare sleutel wordt gebruikt om de gegevens in uw cloudopslag te coderen. Deze sleutel komt overeen met de persoonlijke sleutel die ook tijdens deze stap is gemaakt. De persoonlijke sleutel gaat echter onmiddellijk naar Experience Platform. |
| `publicKeyId` | De openbare sleutel-id wordt gebruikt om een gegevensstroom te maken en uw gecodeerde gegevens voor cloudopslag in te voeren in het Experience Platform. |
| `expiryTime` | De vervaltijd bepaalt de vervaldatum van uw encryptie zeer belangrijke paar. Deze datum wordt automatisch ingesteld op 180 dagen na de datum waarop de sleutel is gegenereerd en wordt weergegeven in een unieke tijdstempelindeling. |

+++

### Coderingssleutels ophalen {#retrieve-encryption-keys}

Als u alle coderingssleutels in uw organisatie wilt ophalen, vraagt u een GET aan bij `/encryption/keys` endpoit=nt.

**API formaat**

```http
GET /data/foundation/connectors/encryption/keys
```

**Verzoek**

+++Voorbeeldverzoek weergeven

Het volgende verzoek wint alle encryptiesleutels in uw organisatie terug.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Reactie**

+++Voorbeeldreactie van weergave

Een geslaagde reactie retourneert uw versleutelingsalgoritme, naam, openbare sleutel, id van de openbare sleutel, sleuteltype en de bijbehorende vervaltijd van de sleutels.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Coderingssleutels ophalen met id {#retrieve-encryption-keys-by-id}

Als u een specifieke set coderingssleutels wilt ophalen, vraagt u een GET naar het `/encryption/keys` -eindpunt en geeft u uw openbare-sleutel-id op als een headerparameter.

**API formaat**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Verzoek**

+++Voorbeeldverzoek weergeven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Reactie**

+++Voorbeeldreactie van weergave

Een geslaagde reactie retourneert uw versleutelingsalgoritme, naam, openbare sleutel, id van de openbare sleutel, sleuteltype en de bijbehorende vervaltijd van de sleutels.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Door klant beheerd sleutelpaar maken {#create-customer-managed-key-pair}

U kunt desgewenst een sleutelpaar voor handtekeningverificatie maken om uw gecodeerde gegevens te ondertekenen en in te voeren.

Tijdens dit stadium, moet u uw eigen privé sleutel en openbare zeer belangrijke combinatie produceren en dan uw privé sleutel gebruiken om uw gecodeerde gegevens te ondertekenen. Daarna, moet u uw openbare sleutel in Base64 coderen en dan het delen aan Experience Platform opdat Platform uw handtekening verifieert.

### Uw openbare sleutel delen op Experience Platform

Om uw openbare sleutel te delen, doe een verzoek van de POST aan het `/customer-keys` eindpunt terwijl het verstrekken van uw encryptiealgoritme en uw Base64-Gecodeerde openbare sleutel.

**API formaat**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Verzoek**

+++Voorbeeldverzoek weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-sign-verification-keys"
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}},
      "params": {
          "passPhrase": {{PASS_PHRASE}}
      }
    }'
```

| Parameter | Beschrijving |
| --- | --- |
| `encryptionAlgorithm` | Het type van encryptiealgoritme dat u gebruikt. De ondersteunde coderingstypen zijn `PGP` en `GPG` . |
| `publicKey` | De openbare sleutel die aan uw klant beheerde sleutels beantwoordt die voor het ondertekenen van uw gecodeerd worden gebruikt. Deze sleutel moet Base64-Gecodeerd zijn. |

+++

**Reactie**

+++Voorbeeldreactie van weergave

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Eigenschap | Beschrijving |
| --- | --- |
| `publicKeyId` | Deze openbare zeer belangrijke identiteitskaart is teruggekeerd in antwoord op het delen van uw klant beheerde sleutel met Experience Platform. U kunt deze openbare sleutel-id opgeven als de sleutel-id voor ondertekeningsverificatie wanneer u een gegevensstroom maakt voor ondertekende en gecodeerde gegevens. |

+++

### Ontvang klant geleid zeer belangrijk paar

Om uw klant beheerde sleutels terug te winnen, doe een verzoek van de GET aan het `/customer-keys` eindpunt.

**API formaat**

```http
GET /data/foundation/connectors/encryption/customer-keys
```

**Verzoek**

+++Voorbeeldverzoek weergeven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Reactie**

+++Voorbeeldreactie van weergave

```json
[
    {
        "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
        "name": "{NAME}",
        "publicKeyId": "{PUBLIC_KEY_ID}",
        "publicKey": "{PUBLIC_KEY}",
        "keyType": "{KEY_TYPE}",
    }
]
```

+++

## Sluit de bron voor cloudopslag aan op het Experience Platform met behulp van de API van [!DNL Flow Service]

Nadat u de coderingssleutel hebt opgehaald, kunt u nu doorgaan en een bronverbinding voor de bron van de cloudopslag maken en uw gecodeerde gegevens naar het platform overbrengen.

Eerst, moet u een basisverbinding tot stand brengen om uw bron tegen Platform voor authentiek te verklaren. Als u een basisverbinding wilt maken en de bron wilt verifiëren, selecteert u de gewenste bron in de onderstaande lijst:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure-bestandsopslag](../api/create/cloud-storage/azure-file-storage.md)
* [Gegevenslandingszone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud Storage](../api/create/cloud-storage/google.md)
* [Oracle Object Storage](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Na het creëren van een basisverbinding, moet u dan de stappen volgen die in het leerprogramma voor [ worden geschetst creërend een bronverbinding voor een bron van de wolkenopslag ](../api/collect/cloud-storage.md) om een bronverbinding, een doelverbinding, en een afbeelding tot stand te brengen.

## Een gegevensstroom maken voor gecodeerde gegevens {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>U moet over het volgende beschikken om een gegevensstroom voor gecodeerde gegevensinvoer te kunnen maken:
>
>* [ Openbare zeer belangrijke identiteitskaart ](#create-encryption-key-pair)
>* [ de verbindingsidentiteitskaart van Source ](../api/collect/cloud-storage.md#source)
>* [ identiteitskaart van de Verbinding van het Doel ](../api/collect/cloud-storage.md#target)
>* [ Uitwisselingsidentiteitskaart ](../api/collect/cloud-storage.md#mapping)

Als u een gegevensstroom wilt maken, vraagt u een POST naar het `/flows` -eindpunt van de [!DNL Flow Service] API. Als u gecodeerde gegevens wilt invoeren, moet u een `encryption` -sectie toevoegen aan de eigenschap `transformations` en de `publicKeyId` opnemen die in een eerdere stap is gemaakt.

**API formaat**

```http
POST /flows
```

>[!BEGINTABS]

>[!TAB  creeer een dataflow voor gecodeerde gegevensopname ]

**Verzoek**

+++Voorbeeldverzoek weergeven

Met de volgende aanvraag wordt een gegevensstroom gemaakt voor het invoeren van gecodeerde gegevens voor een bron voor cloudopslag.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `flowSpec.id` | De flow-specificatie-id die overeenkomt met bronnen voor cloudopslag. |
| `sourceConnectionIds` | De bron-verbindings-id. Deze id vertegenwoordigt de overdracht van gegevens van bron naar Platform. |
| `targetConnectionIds` | De doel-verbindings-id. Deze id geeft aan waar de gegevens terechtkomen nadat deze naar Platform zijn overgebracht. |
| `transformations[x].params.mappingId` | De toewijzing-id. |
| `transformations.name` | Wanneer u gecodeerde bestanden invoegt, moet u `Encryption` opgeven als extra transformatieparameter voor de gegevensstroom. |
| `transformations[x].params.publicKeyId` | De openbare sleutel-id die u hebt gemaakt. Deze id is de helft van het sleutelpaar voor codering van uw gegevens voor cloudopslag. |
| `scheduleParams.startTime` | De begintijd voor de gegevensstroom in tijdperk. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day` of `week` . |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie is ingesteld op `once` en moet groter zijn dan of gelijk zijn aan `15` voor andere frequentiewaarden. |

+++

**Reactie**

+++Voorbeeldreactie van weergave

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow voor uw gecodeerde gegevens terug.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB  creeer een dataflow om gecodeerde en ondertekende gegevens in te nemen ]

**Verzoek**

+++Voorbeeldverzoek weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `params.signVerificationKeyId` | De sleutel-id voor tekenverificatie is hetzelfde als de openbare-sleutelid die is opgehaald na het delen van de openbare sleutel met Base64-codering met Experience Platform. |

+++

**Reactie**

+++Voorbeeldreactie van weergave

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow voor uw gecodeerde gegevens terug.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### Versleutelingssleutels verwijderen {#delete-encryption-keys}

Als u de coderingssleutels wilt verwijderen, vraagt u een DELETE aan bij het `/encryption/keys` -eindpunt en geeft u uw openbare-sleutel-id op als een headerparameter.

**API formaat**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Verzoek**

+++Voorbeeldverzoek weergeven

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

### Coderingssleutels valideren {#validate-encryption-keys}

Om uw encryptiesleutels te bevestigen, doe een verzoek van de GET aan het `/encryption/keys/validate/` eindpunt en verstrek openbare zeer belangrijke identiteitskaart die u als kopbalparameter wilt bevestigen.

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**Verzoek**

+++Voorbeeldverzoek weergeven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Reactie**

Een succesvol antwoord geeft een bevestiging dat je id&#39;s geldig of ongeldig zijn.

>[!BEGINTABS]

>[!TAB  Geldig ]

Een geldige openbare - sleutelidentiteitskaart keert een status van `Active` samen met uw openbare belangrijkste identiteitskaart terug

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB  ongeldig ]

Een ongeldige openbare - sleutelidentiteitskaart keert een status van `Expired` samen met uw openbare belangrijkste identiteitskaart terug

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## Beperkingen op terugkerende inname {#restrictions-on-recurring-ingestion}

Inname van gecodeerde gegevens ondersteunt geen inname van terugkerende of meervoudige mappen in bronnen. Alle gecodeerde bestanden moeten in één map staan. Jokertekens met meerdere mappen in één bronpad worden ook niet ondersteund.

Hieronder ziet u een voorbeeld van een ondersteunde mapstructuur, waarbij het bronpad `/ACME-customers/*.csv.gpg` is.

In dit scenario worden de vetgedrukte bestanden in het Experience Platform opgenomen.

* ACME-klanten
   * **File1.csv.gpg**
   * File2.json.gpg
   * **File3.csv.gpg**
   * File4.json
   * **File5.csv.gpg**

Hieronder ziet u een voorbeeld van een niet-ondersteunde mapstructuur waarbij het bronpad `/ACME-customers/*` is.

In dit scenario, zal de stroomlooppas ontbreken en een foutenmelding terugkeren erop wijzend dat de gegevens niet uit de bron kunnen worden gekopieerd.

* ACME-klanten
   * File1.csv.gpg
   * File2.json.gpg
   * Submap1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* ACME-loyaliteit
   * File6.csv.gpg


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een sleutelpaar voor codering van uw gegevens voor cloudopslag gemaakt en een gegevensstroom voor het opnemen van gecodeerde gegevens via de [!DNL Flow Service API] . Voor statusupdates op de volledigheid van uw gegevensstroom, fouten, en metriek, lees de gids op [ controle uw gegevensstroom gebruikend  [!DNL Flow Service]  API ](./monitor.md).