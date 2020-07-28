---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een verbinding van de de gegevenssetbasis van het Experience Platform gebruikend de Dienst API van de Stroom
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# Een basisverbinding voor een [!DNL Experience Platform] gegevensset maken met de [!DNL Flow Service] API

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Om gegevens van een derdebron aan te sluiten [!DNL Platform], moet een datasetbasisverbinding eerst worden gevestigd.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te lopen om een gegevenssetbasisverbinding tot stand te brengen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

* [XDM-systeem](../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Handleiding](../../../xdm/api/getting-started.md)voor ontwikkelaars van het schemaregister: Omvat belangrijke informatie die u moet weten om vraag aan de Registratie API van het Schema met succes uit te voeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).
* [Catalogusservice](../../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen [!DNL Experience Platform].
* [Inname](../../../ingestion/batch-ingestion/overview.md)in batch: Met de API voor batchinvoer kunt u gegevens als batchbestanden in het Experience Platform invoeren.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met het meer van Gegevens te verbinden gebruikend [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Verbindingsspecificaties opzoeken

De eerste stap in het creëren van een verbinding van de datasetbasis is een reeks verbindingsspecificaties van binnen terug te winnen [!DNL Flow Service].

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. U kunt verbindingsspecificaties voor een gegevenssetbasisverbinding opzoeken door een verzoek van de GET uit te voeren en vraagparameters te gebruiken.

Het verzenden van een verzoek van de GET zonder vraagparameters zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` om informatie voor uw gegevenssetbasisverbinding te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Verzoek**

Het volgende verzoek wint de verbindingsspecificaties voor een gegevenssetbasisverbinding terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de verbindingsspecificaties en de unieke id (`id`) die vereist zijn om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Een databaseverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Slechts één gegevenssetbasisverbinding wordt vereist aangezien het kan worden gebruikt om veelvoudige bronschakelaars tot stand te brengen om verschillende gegevens in te brengen.

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
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| ------------- | --------------- |
| `connectionSpec.id` | De verbindingsspecificatie die in de vorige stap is `id` opgehaald. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om een doelverbinding te maken en gegevens van een externe bronconnector in te voeren.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding van de datasetbasis tot stand gebracht gebruikend [!DNL Flow Service] API, en hebt u de unieke waarde van identiteitskaart van de verbinding verkregen. U kunt deze basisverbinding gebruiken om een doelverbinding tot stand te brengen. De volgende zelfstudies lopen door de stappen om een doelverbinding tot stand te brengen, afhankelijk van de categorie van bronschakelaar u gebruikt:

* [Cloud-opslag](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Klant geslaagd](./collect/customer-success.md)
* [Database](./collect/database-nosql.md)