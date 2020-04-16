---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een systeem voor cloudopslag verkennen met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 7cd9bec7336d0e1d9f3036cf862633f498002af8

---


# Een systeem voor cloudopslag verkennen met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om een cloudopslagsysteem van derden te verkennen.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten om een verbinding met een cloudopslagsysteem met de Flow Service API tot stand te brengen.

### Een basisverbinding verkrijgen

Als u een externe cloudopslag wilt verkennen met Platform-API&#39;s, moet u beschikken over een geldige basis-verbindings-id. Als u nog geen basisverbinding hebt voor de opslag waarmee u wilt werken, kunt u een verbinding maken via de volgende zelfstudies:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief de bronnen die bij Flow Service horen, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Ontdek uw cloudopslag

Met de basisverbinding voor uw cloudopslag kunt u bestanden en mappen verkennen door GET-aanvragen uit te voeren. Wanneer het uitvoeren van GET verzoeken om uw wolkenopslag te onderzoeken, moet u de vraagparameters omvatten die in de lijst hieronder worden vermeld:

| Parameter | Beschrijving |
| --------- | ----------- |
| `objectType` | Het type object dat u wilt verkennen. Stel deze waarde in op: <ul><li>`folder`: Een specifieke map verkennen</li><li>`root`: Verken de hoofdmap.</li></ul> |
| `object` | Deze parameter is alleen vereist wanneer een specifieke map wordt weergegeven. Zijn waarde vertegenwoordigt de weg van de folder u wenst te onderzoeken. |

Gebruik de volgende vraag om de weg van het dossier te vinden u in Platform wilt brengen:

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van een basisverbinding voor cloudopslag. |
| `{PATH}` | Het pad van een map. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert een array met bestanden en mappen die in de gevraagde map zijn gevonden. Let op de `path` eigenschap van het bestand dat u wilt uploaden, aangezien u deze in de volgende stap moet opgeven om de structuur te controleren.

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

## De structuur van een bestand controleren

Om de structuur van gegevensdossier van uw cloudopslag te inspecteren, voer een GET verzoek uit terwijl het verstrekken van de weg van het dossier als vraagparameter.

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van een basisverbinding voor cloudopslag. |
| `{FILE_PATH}` | Pad naar een bestand. |
| `{FILE_TYPE}` | Het type bestand. Tot de ondersteunde bestandstypen behoren:<ul><li>BEPERKT</code>: Waarde gescheiden door scheidingstekens. DSV-bestanden moeten door komma&#39;s van elkaar worden gescheiden.</li><li>JSON</code>: JavaScript-objectnotatie. JSON-bestanden moeten XDM-compatibel zijn</li><li>PARQUET</code>: Apache Parquet. Parketbestanden moeten XDM-compatibel zijn.</li></ul> |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

Aan de hand van deze zelfstudie hebt u uw cloudopslagsysteem verkend, het pad gevonden van het bestand dat u naar Platform wilt overbrengen en de structuur ervan bekeken. U kunt deze informatie in de volgende zelfstudie gebruiken om gegevens te [verzamelen van uw cloudopslag en deze over te brengen naar Platform](../collect/cloud-storage.md).