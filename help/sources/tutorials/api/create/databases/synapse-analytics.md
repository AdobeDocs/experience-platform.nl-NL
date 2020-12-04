---
keywords: Experience Platform;home;popular topics;Synapse;synapse;Azure Synapse Analytics
solution: Experience Platform
title: Een Azure synapse Analytics-connector maken met de Flow Service API
topic: overview
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Azure synapse Analytics (hierna "Synapse" genoemd) aan Experience Platform te verbinden.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 1%

---


# Een [!DNL Azure Synapse Analytics] aansluiting maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De Azure synapse Analytics-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de Flow Service API gebruikt om u door de stappen te laten lopen waarmee u verbinding wilt maken [!DNL Azure Synapse Analytics] (hierna &quot;[!DNL Synapse]&quot; genoemd) [!DNL Experience Platform].

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Synapse] [!DNL Flow Service] de API.

### Vereiste referenties verzamelen

Als u verbinding wilt [!DNL Flow Service] maken met [!DNL Synapse], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks waarmee verbinding wordt gemaakt [!DNL Synapse]. Het patroon van de [!DNL Synapse] verbindingstekenreeks is `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL Synapse] is: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |

Raadpleeg [dit synapsdocument](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure?toc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Ftoc.json&amp;bc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Fbreadcrumb%2Ftoc.json&amp;tabs=azure-powershell)voor meer informatie over het verkrijgen van een verbindingstekenreeks.

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

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding per [!DNL Synapse] account vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een [!DNL Synapse] verbinding tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor [!DNL Synapse] is `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for Azure Synapse Analytics",
        "description": "Connection for Azure Synapse Analytics",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        },
        "connectionSpec": {
            "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks waarmee verbinding wordt gemaakt [!DNL Synapse]. Het patroon van de [!DNL Synapse] verbindingstekenreeks is `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | De id van de [!DNL Synapse] verbindingsspecificatie is: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw database te verkennen in de volgende zelfstudie.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Synapse] verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u databases kunt [verkennen met behulp van de Flow Service API](../../explore/database-nosql.md).
