---
title: Versleutelde gegevensinsluiting
description: Leer hoe u gecodeerde bestanden via batchbronnen voor cloudopslag kunt opnemen met de API.
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---

# Versleutelde gegevensinvoer

Met Adobe Experience Platform kunt u gecodeerde bestanden opnemen via batchbronnen voor cloudopslag. Met gecodeerde gegevensinvoer kunt u gebruikmaken van asymmetrische coderingsmechanismen om batchgegevens veilig naar het Experience Platform over te brengen. Momenteel, zijn de gesteunde asymmetrische encryptiemechanismen PGP en GPG.

De gecodeerde gegevensinvoer verloopt als volgt:

1. [Een sleutelpaar maken met Experience Platform-API&#39;s](#create-encryption-key-pair). Het sleutelpaar bestaat uit een persoonlijke sleutel en een openbare sleutel. Als u een id hebt gemaakt, kunt u de openbare sleutel samen met de bijbehorende id voor de openbare sleutel en de Vervaltijd kopiëren of downloaden. Tijdens dit proces wordt de persoonlijke sleutel door het Experience Platform in een veilige kluis opgeslagen. **OPMERKING:** De openbare sleutel in de reactie is Base64-Gecodeerd en moet voorafgaand aan het gebruiken worden gedecrypteerd.
2. Gebruik de openbare sleutel om het gegevensbestand te coderen dat u wilt opnemen.
3. Plaats het gecodeerde bestand in de cloudopslag.
4. Zodra het gecodeerde bestand gereed is, [een bronverbinding en een gegevensstroom maken voor uw bron voor cloudopslag](#create-a-dataflow-for-encrypted-data). Tijdens de stap voor het maken van flow moet u een `encryption` en neem uw openbare sleutel-id op.
5. Het Experience Platform wint de privé sleutel van de veilige kluis terug om de gegevens op het tijdstip van inname te decrypteren.

>[!IMPORTANT]
>
>De maximale grootte van één gecodeerd bestand is 1 GB. U kunt bijvoorbeeld gegevens van 2 GB invoeren in één gegevensstroom, maar elk afzonderlijk bestand in die gegevens mag niet groter zijn dan 1 GB.

Dit document bevat stappen voor het genereren van een sleutelpaar voor versleuteling van gegevens en het invoeren van gecodeerde gegevens naar het Experience Platform met behulp van bronnen voor cloudopslag.

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
   * [Opslagbronnen voor cloud](../api/collect/cloud-storage.md): Maak een gegevensstroom om batchgegevens van uw cloudopslagbron naar het Experience Platform te brengen.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

### Ondersteunde bestandsextensies voor gecodeerde bestanden

De lijst met ondersteunde bestandsextensies voor gecodeerde bestanden ziet er als volgt uit:

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

De eerste stap bij het opnemen van gecodeerde gegevens in het Experience Platform is het maken van uw sleutelpaar door een verzoek van de POST aan het `/encryption/keys` het eindpunt van de [!DNL Connectors] API.

**API-indeling**

```http
POST /data/foundation/connectors/encryption/keys
```

**Verzoek**

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
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `encryptionAlgorithm` | Het type van encryptiealgoritme dat u gebruikt. De ondersteunde coderingstypen zijn `PGP` en `GPG`. |
| `params.passPhrase` | Passphrase verstrekt een extra laag van bescherming voor uw encryptiesleutels. Op verwezenlijking, slaat het Experience Platform passphrase in een verschillend veilige kluis van de openbare sleutel op. U moet een niet-lege tekenreeks opgeven als een wachtwoordzin. |

**Antwoord**

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

+++ (Optioneel) Een paar verificatietoetsen voor ondertekening maken voor ondertekende gegevens

### Door klant beheerd sleutelpaar maken

U kunt desgewenst een sleutelpaar voor handtekeningverificatie maken om uw gecodeerde gegevens te ondertekenen en in te voeren.

Tijdens dit stadium, moet u uw eigen privé sleutel en openbare zeer belangrijke combinatie produceren en dan uw privé sleutel gebruiken om uw gecodeerde gegevens te ondertekenen. Daarna, moet u uw openbare sleutel in Base64 coderen en dan het delen aan Experience Platform opdat het Platform uw handtekening verifieert.

### Uw openbare sleutel delen op Experience Platform

Om uw openbare sleutel te delen, doe een verzoek van de POST aan `/customer-keys` eindpunt terwijl het verstrekken van uw encryptiealgoritme en uw Base64-Gecodeerde openbare sleutel.

**API-indeling**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}}
    }'
```

| Parameter | Beschrijving |
| --- | --- |
| `encryptionAlgorithm` | Het type van encryptiealgoritme dat u gebruikt. De ondersteunde coderingstypen zijn `PGP` en `GPG`. |
| `publicKey` | De openbare sleutel die aan uw klant beheerde sleutels beantwoordt die voor het ondertekenen van uw gecodeerd worden gebruikt. Deze sleutel moet Base64-Gecodeerd zijn. |

**Antwoord**

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Eigenschap | Beschrijving |
| --- | --- |
| `publicKeyId` | Deze openbare zeer belangrijke identiteitskaart is teruggekeerd in antwoord op het delen van uw klant beheerde sleutel met Experience Platform. U kunt deze openbare sleutel-id opgeven als de sleutel-id voor ondertekeningsverificatie wanneer u een gegevensstroom maakt voor ondertekende en gecodeerde gegevens. |

+++

## Sluit de bron voor cloudopslag aan op het Experience Platform met de [!DNL Flow Service] API

Nadat u de coderingssleutel hebt opgehaald, kunt u nu doorgaan en een bronverbinding voor de bron van de cloudopslag maken en de gecodeerde gegevens naar het Platform brengen.

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

Nadat u een basisverbinding hebt gemaakt, moet u de in de zelfstudie beschreven stappen volgen voor [een bronverbinding maken voor een bron voor cloudopslag](../api/collect/cloud-storage.md) om een bronverbinding, een doelverbinding, en een afbeelding tot stand te brengen.

## Een gegevensstroom maken voor gecodeerde gegevens {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>U moet over het volgende beschikken om een gegevensstroom voor gecodeerde gegevensinvoer te kunnen maken:
>
>* [Openbare sleutel-id](#create-encryption-key-pair)
>* [Bronverbinding-id](../api/collect/cloud-storage.md#source)
>* [Doel-verbindings-id](../api/collect/cloud-storage.md#target)
>* [Toewijzing-id](../api/collect/cloud-storage.md#mapping)

Om een gegevensstroom tot stand te brengen, doe een verzoek van de POST aan `/flows` het eindpunt van de [!DNL Flow Service] API. Als u gecodeerde gegevens wilt invoeren, moet u een `encryption` aan de `transformations` en neemt de `publicKeyId` die in een eerdere stap is gemaakt.

**API-indeling**

```http
POST /flows
```

**Verzoek**

>[!BEGINTABS]

>[!TAB Een gegevensstroom maken voor gecodeerde gegevensinvoer]

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
| `targetConnectionIds` | De doel-verbindings-id. Deze id geeft aan waar de gegevens terechtkomen nadat deze naar het Platform zijn overgebracht. |
| `transformations[x].params.mappingId` | De toewijzing-id. |
| `transformations.name` | Wanneer u gecodeerde bestanden opgeeft, moet u `Encryption` als een aanvullende transformatieparameter voor uw gegevensstroom. |
| `transformations[x].params.publicKeyId` | De openbare sleutel-id die u hebt gemaakt. Deze id is de helft van het sleutelpaar voor codering van uw gegevens voor cloudopslag. |
| `scheduleParams.startTime` | De begintijd voor de gegevensstroom in tijdperk. |
| `scheduleParams.frequency` | De frequentie waarmee de gegevensstroom gegevens zal verzamelen. Acceptabele waarden zijn: `once`, `minute`, `hour`, `day`, of `week`. |
| `scheduleParams.interval` | Het interval geeft de periode aan tussen twee opeenvolgende flowrun. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul. Interval is niet vereist wanneer de frequentie wordt ingesteld als `once` en moet groter zijn dan of gelijk zijn aan `15` voor andere frequentiewaarden. |


>[!TAB Een gegevensstroom maken om gecodeerde en ondertekende gegevens in te voeren]

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

>[!ENDTABS]

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom voor uw gecodeerde gegevens.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een sleutelpaar voor codering van uw gegevens voor cloudopslag gemaakt en een gegevensstroom voor het opnemen van gecodeerde gegevens via de [!DNL Flow Service API]. Lees de handleiding voor statusupdates over de volledigheid, fouten en metriek van uw gegevensstroom [uw gegevensstroom controleren met de [!DNL Flow Service] API](./monitor.md).
