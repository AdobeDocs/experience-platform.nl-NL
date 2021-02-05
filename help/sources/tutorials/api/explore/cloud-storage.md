---
keywords: Experience Platform;home;populaire onderwerpen;cloudopslag;Cloudopslag
solution: Experience Platform
title: Een hardop opslagsysteem verkennen met de Flow Service API
topic: overview
description: Deze zelfstudie gebruikt de Flow Service API om een extern cloudopslagsysteem te verkennen.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# Een systeem voor cloudopslag verkennen met de [!DNL Flow Service]-API

In deze zelfstudie wordt de [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) gebruikt om een extern cloudopslagsysteem te verkennen.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om een verbinding met een cloudopslagsysteem met de API [!DNL Flow Service] tot stand te brengen.

### Verbindings-id verkrijgen

Als u een externe cloudopslag wilt verkennen met behulp van [!DNL Platform] API&#39;s, moet u over een geldige verbinding-id beschikken. Als u nog geen verbinding hebt voor de opslag waarmee u wilt werken, kunt u een verbinding maken via de volgende zelfstudies:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../create/cloud-storage/adls-gen2.md)
* [Azure-bestandsopslag](../create/cloud-storage/azure-file-storage.md)
* [FTP](../create/cloud-storage/ftp.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [SFTP](../create/cloud-storage/sftp.md)

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Ontdek uw cloudopslag

Met de verbinding-id voor uw cloudopslag kunt u bestanden en mappen verkennen door GET-aanvragen uit te voeren. Wanneer u GET-aanvragen uitvoert om uw cloudopslag te verkennen, moet u de queryparameters opnemen die in de onderstaande tabel worden vermeld:

| Parameter | Beschrijving |
| --------- | ----------- |
| `objectType` | Het type object dat u wilt verkennen. Stel deze waarde in op: <ul><li>`folder`: Een specifieke map verkennen</li><li>`root`: Verken de hoofdmap.</li></ul> |
| `object` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. |

Gebruik de volgende vraag om de weg van het dossier te vinden u in [!DNL Platform] wilt brengen:

**API-indeling**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONNECTION_ID}` | De verbindings-id voor de bronaansluiting van de cloud. |
| `{PATH}` | Het pad van een map. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert een array met bestanden en mappen die in de gevraagde map zijn gevonden. Neem nota van het `path` bezit van het dossier u wenst uploadt, aangezien u het in de volgende stap moet verstrekken om zijn structuur te inspecteren.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## De structuur van een bestand Inspect

Om de structuur van gegevensdossier van uw cloudopslag te inspecteren, voer een verzoek van de GET uit terwijl het verstrekken van de weg van het dossier en type als vraagparameter.

U kunt de structuur van een CSV- of TSV-bestand inspecteren door een aangepast scheidingsteken op te geven als een zoekomtrek. Elke waarde van één teken is een toegestaan kolomscheidingsteken. Indien niet opgegeven, wordt een komma `(,)` gebruikt als standaardwaarde.

**API-indeling**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=;
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=\t
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De verbindings-id van de bronconnector van de cloudopslag. |
| `{FILE_PATH}` | Het pad naar het bestand dat u wilt inspecteren. |
| `{FILE_TYPE}` | Het type bestand. Tot de ondersteunde bestandstypen behoren:<ul><li>DELIMITED</code>: Waarde gescheiden door scheidingstekens. DSV-bestanden moeten door komma&#39;s van elkaar worden gescheiden.</li><li>JSON</code>: JavaScript-objectnotatie. JSON-bestanden moeten XDM-compatibel zijn</li><li>PARQUET</code>: Apache Parquet. Parketbestanden moeten XDM-compatibel zijn.</li></ul> |
| `columnDelimiter` | De waarde van één teken die u hebt opgegeven als kolomscheidingsteken voor het inspecteren van CSV- of TSV-bestanden. Als de parameter niet opgegeven is, wordt de waarde standaard ingesteld op een komma `(,)`. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord geeft de structuur van het gevraagde dossier met inbegrip van lijstnamen en gegevenstypes terug.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u uw cloudopslagsysteem verkend, het pad gevonden van het bestand dat u wilt inbrengen naar [!DNL Platform] en de structuur ervan bekeken. U kunt deze informatie in de volgende zelfstudie gebruiken om gegevens van uw cloudopslag te verzamelen en in Platform te brengen](../collect/cloud-storage.md).[