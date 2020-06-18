---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Azure File Storage-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: c843ebb72ee3f1e8d2233dd2be4021403417813b
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# Een Azure File Storage-connector maken met de Flow Service API

>[!NOTE]
>De Azure File Storage-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De Dienst van de stroom wordt gebruikt om klantengegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Azure File Storage te verbinden met Experience Platform.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om een verbinding met Azure File Storage met de Flow Service API tot stand te brengen.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met de Azure Opslag van het Dossier te verbinden, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van de Azure File Storage-instantie waartoe u toegang hebt. |
| `userId` | De gebruiker met voldoende toegang tot het Azure eindpunt van de Opslag van het Dossier. |
| `password` | Het wachtwoord voor uw Azure File Storage-instantie |
| Verbindingsspecificatie-id | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor Azure File Storage is: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Raadpleeg [dit Azure File Storage-document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)voor meer informatie over hoe u aan de slag gaat.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u eerst het [authentificatieleerprogramma](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform, inclusief die van de Flow Service, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding vereist per Azure File Storage-account, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe Azure File Storage-verbinding gemaakt, geconfigureerd door de eigenschappen die in de payload worden opgegeven:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | Het eindpunt van de Azure File Storage-instantie waartoe u toegang hebt. |
| `auth.params.userId` | De gebruiker met voldoende toegang tot het Azure eindpunt van de Opslag van het Dossier. |
| `auth.params.password` | De Azure File Storage-toegangssleutel. |
| `connectionSpec.id` | De Azure-ID van de bestandsopslagverbinding: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een Azure File Storage-verbinding gemaakt met de Flow Service API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken als u leert hoe u een externe cloudopslag kunt [verkennen met de Flow Service API](../../explore/cloud-storage.md).
