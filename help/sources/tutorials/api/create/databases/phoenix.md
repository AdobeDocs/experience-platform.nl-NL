---
keywords: Experience Platform;home;populaire onderwerpen;Phoenix;phoenix
solution: Experience Platform
title: Een Phoenix Base-verbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Phoenix-database met de Flow Service API met Adobe Experience Platform kunt verbinden.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# Een [!DNL Phoenix] basisverbinding met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Phoenix] -connector bevindt zich in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te lopen om een verbinding te maken [!DNL Phoenix] database naar [!DNL Experience Platform].

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Phoenix] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Phoenix]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Phoenix] server. |
| `username` | De gebruikersnaam die u gebruikt om toegang te krijgen tot [!DNL Phoenix] Server. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |
| `port` | De TCP-poort die de [!DNL Phoenix] server gebruikt om naar clientverbindingen te luisteren. Als u verbinding maakt met [!DNL Azure] HDInsights, geef poort 443 op. |
| `httpPath` | De gedeeltelijke URL die overeenkomt met de [!DNL Phoenix] server. /hbasephoenix0 opgeven bij gebruik [!DNL Azure] HDInsightcluster. |
| `enableSsl` | Een booleaanse waarde. Geeft aan of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Phoenix] is: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Zie voor meer informatie over het aan de slag gaan [dit Phoenix-document](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Phoenix] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Phoenix]:

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
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}",
            "port": {PORT},
            "httpPath": "{PATH}",
            "enableSsl": {SSL}
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
| `auth.params.host` | De gastheer van de [!DNL Phoenix] server. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Phoenix] verbinding. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Phoenix] verbinding. |
| `auth.params.port` | De haven van TCP voor uw [!DNL Phoenix] verbinding. |
| `auth.params.httpPath` | Het gedeeltelijke http-pad voor uw [!DNL Phoenix] verbinding. |
| `auth.params.enableSsl` | De booleaanse waarde die opgeeft of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De [!DNL Phoenix] Verbindingsspecificatie-id: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Antwoord**

Een succesvol antwoord retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Phoenix] verbinding met de [!DNL Flow Service] API en hebben de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u [databases verkennen met de Flow Service API](../../explore/database-nosql.md).
