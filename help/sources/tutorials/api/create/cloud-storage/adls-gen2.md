---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;azure data lake storage;Azure
solution: Experience Platform
title: Maak een Azure Data Lake Storage Gen2-connector met de Flow Service API
topic: overview
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform aan Azure Data Lake Storage Gen2 (hierna "ADLS Gen2" genoemd) te verbinden.
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# Een [!DNL Azure] Data Lake Storage Gen2-connector maken met de [!DNL Flow Service] API

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de [!DNL Flow Service]-API gebruikt om u door de stappen te laten lopen om [!DNL Experience Platform] te verbinden met [!DNL Azure] Data Lake Storage Gen2 (hierna &quot;ADLS Gen2&quot; genoemd).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele instantie van het Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om tot een bron van ADLS Gen2 te leiden schakelaar gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met ADLS Gen2 als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De adres-URL. |
| `servicePrincipalId` | De client-id van de toepassing. |
| `servicePrincipalKey` | De sleutel van de toepassing. |
| `tenant` | De huurdersinformatie die uw toepassing bevat. |

Raadpleeg [dit ADLS Gen2-document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage) voor meer informatie over deze waarden.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](../../../../../tutorials/authentication.md) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per ADLS Gen2-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken die verschillende gegevens kunnen inbrengen.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een verbinding tot stand te brengen ADLS-Gen2, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor ADLS-Gen2 is `0ed90a81-07f4-4586-8190-b40eccef1c5a`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.url` | Het URL-eindpunt voor uw ADLS Gen2-account. |
| `auth.params.servicePrincipalId` | De service principal ID van uw ADLS Gen2-account. |
| `auth.params.servicePrincipalKey` | De belangrijkste servicetoets van uw ADLS Gen2-account. |
| `auth.params.tenant` | De huurdersinformatie van uw account van ADLS Gen2. |
| `connectionSpec.id` | De ID van de ADLS Gen2-verbindingsspecificatie: `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw cloudopslag in de volgende stap te verkennen.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een ADLS Gen2-verbinding gemaakt met behulp van API&#39;s en is een unieke id opgehaald als onderdeel van de responsstructuur. Met deze verbindings-id kunt u [cloudopslag verkennen met de Flow Service API](../../explore/cloud-storage.md) of [ingest parketgegevens met behulp van de Flow Service API](../../cloud-storage-parquet.md).
