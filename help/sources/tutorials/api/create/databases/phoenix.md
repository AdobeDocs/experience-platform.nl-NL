---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Phoenix-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: c00edf487404e1d08bc86cb6692325f536964af6

---


# Een Phoenix-connector maken met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om een Phoenix-database te verbinden met Experience Platform.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met Phoenix te verbinden gebruikend de Dienst API van de Stroom.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met Phoenix te verbinden, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de Phoenix-server. |
| `username` | De gebruikersnaam die u gebruikt om tot de Server van Phoenix toegang te hebben. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |
| `port` | De TCP-poort die de Phoenix-server gebruikt om te luisteren naar clientverbindingen. Als u verbinding maakt met Azure HDInsights, geeft u poort 443 op. |
| `httpPath` | De gedeeltelijke URL die overeenkomt met de Phoenix-server. Specificeer /hbasephoenix0 als het gebruiken van Azure HDInsights cluster. |
| `enableSsl` | Een booleaanse waarde. Geeft aan of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor Phoenix is: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Raadpleeg [dit Phoenix-document](https://python-phoenixdb.readthedocs.io/en/latest/api.html)voor meer informatie over aan de slag gaan.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../../../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief die van de Flow Service, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per Phoenix-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een verbinding tot stand te brengen Phoenix, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het POST- verzoek worden verstrekt. De verbindingsspecificatie-id voor Phoenix is `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | De host van de Phoenix-server. |
| `auth.params.username` | De gebruikersnaam die aan uw Phoenix-verbinding is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw verbinding Phoenix wordt gekoppeld. |
| `auth.params.port` | De TCP-poort voor uw Phoenix-verbinding. |
| `auth.params.httpPath` | Het gedeeltelijke http-pad voor uw Phoenix-verbinding. |
| `auth.params.enableSsl` | De booleaanse waarde die opgeeft of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De Phoenix-specificatie-id: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een Phoenix-verbinding gemaakt met de Flow Service API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u databases kunt [verkennen met behulp van de Flow Service API](../../explore/database-nosql.md).