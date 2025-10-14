---
keywords: Experience Platform;home;populaire onderwerpen;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Een Apache Cassandra Source-verbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Apache Cassandra met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Een [!DNL Apache Cassandra] bronverbinding maken met de [!DNL Flow Service] API

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen om [!DNL Apache Cassandra] (hierna &quot;Cassandra&quot; genoemd) aan [!DNL Experience Platform] te verbinden.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met Cassandra met de API [!DNL Flow Service] .

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Cassandra] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Cassandra] -server. |
| `port` | De TCP-poort die de [!DNL Cassandra] -server gebruikt om te luisteren naar clientverbindingen. De standaardpoort is `9042` . |
| `username` | De gebruikersnaam die wordt gebruikt voor verbinding met de [!DNL Cassandra] -server voor verificatie. |
| `password` | Het wachtwoord waarmee verbinding moet worden gemaakt met de [!DNL Cassandra] -server voor verificatie. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4` . |

Voor meer informatie over begonnen worden, verwijs naar [&#x200B; dit document van Cassandra &#x200B;](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot de [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL Cassandra] -account is slechts één connector vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken die verschillende gegevens kunnen inbrengen.

**API formaat**

```http
POST /connections
```

**Verzoek**

Als u een [!DNL Cassandra] -verbinding wilt maken, moet de unieke id van de verbindingsspecificatie worden opgegeven als onderdeel van de POST-aanvraag. De verbindingsspecificatie-id voor [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4` .

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | Het IP-adres of de hostnaam van de [!DNL Cassandra] -server. |
| `auth.params.port` | De TCP-poort die de [!DNL Cassandra] -server gebruikt om te luisteren naar clientverbindingen. De standaardpoort is `9042` . |
| `auth.params.username` | De gebruikersnaam die wordt gebruikt voor verbinding met de [!DNL Cassandra] -server voor verificatie. |
| `auth.params.password` | Het wachtwoord waarmee verbinding moet worden gemaakt met de [!DNL Cassandra] -server voor verificatie. |
| `connectionSpec.id` | De [!DNL Cassandra] connection spec ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Cassandra] -verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze identiteitskaart in het volgende leerprogramma gebruiken aangezien u leert hoe te [&#x200B; gegevensbestanden onderzoeken gebruikend de Dienst API van de Stroom &#x200B;](../../explore/database-nosql.md).
