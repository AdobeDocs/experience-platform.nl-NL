---
keywords: Experience Platform;home;popular topics; flow service; update connections
solution: Experience Platform
title: Een verbinding verwijderen met de Flow Service API
topic: overview
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het verwijderen van een verbinding met de Flow Service API.
translation-type: tm+mt
source-git-commit: 9c807270181084a94f288c248a678821ca58e194
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---


# Een verbinding verwijderen met de Flow Service API

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van [!DNL Platform] services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie worden de stappen beschreven voor het verwijderen van het gebruik van de [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Voor deze zelfstudie moet u een geldige verbinding-id hebben. Als u geen geldige verbinding-id hebt, selecteert u de gewenste connector in het overzicht [van](../../home.md) bronnen en volgt u de stappen die worden beschreven voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om de verbindingsgegevens met de [!DNL Flow Service] API te kunnen bijwerken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Verbindingsdetails opzoeken

>[!NOTE]
>Deze zelfstudie gebruikt de bronconnector [van](../../connectors/cloud-storage/blob.md) Azure Blob als voorbeeld, maar de stappen die worden beschreven, zijn van toepassing op alle [beschikbare bronconnectors](../../home.md).

De eerste stap bij het bijwerken van uw verbindingsgegevens is het ophalen van verbindingsgegevens met behulp van uw verbindings-id.

**API-indeling**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` waarde voor de verbinding die u wilt ophalen. |

**Verzoek**

In het volgende voorbeeld wordt informatie over uw verbinding-id opgehaald.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de huidige details van de verbinding, inclusief de referenties, unieke id (`id`) en versie.

```json
{
    "items": [
        {
            "createdAt": 1603514659165,
            "updatedAt": 1603514659165,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "dd3631cd-d0ea-4fea-b631-cdd0ea6fea21",
            "name": "Test Azure Blob Connector",
            "description": "A test connector for Azure Blob",
            "connectionSpec": {
                "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "ConnectionString",
                "params": {
                    "connectionString": "xxxx"
                }
            },
            "version": "\"07001eed-0000-0200-0000-5f93b1250000\"",
            "etag": "\"07001eed-0000-0200-0000-5f93b1250000\""
        }
    ]
}
```

## Verbinding verwijderen

Zodra u een bestaande verbindingsidentiteitskaart hebt, voer een verzoek van de DELETE aan [!DNL Flow Service] API uit.

**API-indeling**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` waarde voor de verbinding die u wilt bijwerken. |

**Verzoek**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan de verbinding te proberen.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de [!DNL Flow Service] API gebruikt om bestaande accounts te verwijderen.

Raadpleeg de zelfstudie over het [verwijderen van accounts in de gebruikersinterface voor informatie over het uitvoeren van deze bewerkingen in de gebruikersinterface](../../tutorials/ui/delete-accounts.md)
