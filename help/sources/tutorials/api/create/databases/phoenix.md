---
keywords: Experience Platform;home;populaire onderwerpen;Phoenix;phoenix
solution: Experience Platform
title: Een Phoenix Source Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Phoenix-database met de Flow Service API met Adobe Experience Platform kunt verbinden.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# Een [!DNL Phoenix]-bronverbinding maken met de [!DNL Flow Service]-API

>[!NOTE]
>
>De [!DNL Phoenix] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te leiden om een [!DNL Phoenix] gegevensbestand aan [!DNL Experience Platform] te verbinden.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met [!DNL Phoenix] met de [!DNL Flow Service]-API tot stand te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL Phoenix], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Phoenix]-server. |
| `username` | De gebruikersnaam die u gebruikt om toegang te krijgen tot [!DNL Phoenix] Server. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |
| `port` | De TCP-poort die de [!DNL Phoenix]-server gebruikt om te luisteren naar clientverbindingen. Als u verbinding maakt met [!DNL Azure] HDInsights, geeft u poort 443 op. |
| `httpPath` | De gedeeltelijke URL die overeenkomt met de [!DNL Phoenix]-server. Specificeer /hbasephoenix0 als het gebruiken van [!DNL Azure] cluster HDInsights. |
| `enableSsl` | Een booleaanse waarde. Geeft aan of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL Phoenix] is: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Zie [dit Phoenix-document](https://python-phoenixdb.readthedocs.io/en/latest/api.html) voor meer informatie over aan de slag gaan.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL Phoenix]-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een [!DNL Phoenix] verbinding tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor [!DNL Phoenix] is `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

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
| `auth.params.host` | De host van de [!DNL Phoenix]-server. |
| `auth.params.username` | De gebruikersnaam die is gekoppeld aan uw [!DNL Phoenix]-verbinding. |
| `auth.params.password` | Het wachtwoord dat is gekoppeld aan uw [!DNL Phoenix]-verbinding. |
| `auth.params.port` | De TCP-poort voor uw [!DNL Phoenix]-verbinding. |
| `auth.params.httpPath` | Het gedeeltelijke http pad voor uw [!DNL Phoenix] verbinding. |
| `auth.params.enableSsl` | De booleaanse waarde die opgeeft of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De [!DNL Phoenix] ID van de verbindingsspecificatie: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen hebt u een [!DNL Phoenix]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u databases kunt [verkennen met behulp van de Flow Service API](../../explore/database-nosql.md).
