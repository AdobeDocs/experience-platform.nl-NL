---
title: Een Phoenix Base-verbinding maken met de Flow Service API
description: Leer hoe u een Phoenix-database met de Flow Service API met Adobe Experience Platform kunt verbinden.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: efffd6ce1ed541ce20ee6500e42165465f2fa6a0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Een [!DNL Phoenix] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie bevat stappen voor het maken van een basisverbinding en het verbinden van uw [!DNL Phoenix] account aan Adobe Experience Platform [!DNL Flow Service] API.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Experience Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Experience Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Phoenix] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

U moet de volgende verificatiereferenties opgeven om verbinding te kunnen maken met uw [!DNL Phoenix] aan Experience Platform.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Phoenix] server. |
| `username` | De gebruikersnaam die u gebruikt voor toegang [!DNL Phoenix] Server. |
| `password` | Het wachtwoord voor de gebruiker. |
| `port` | De TCP-poort die de [!DNL Phoenix] server gebruikt om naar clientverbindingen te luisteren. Als u verbinding maakt met [!DNL Azure HDInsights]en geeft u de poort op als 443. Als deze parameter niet wordt opgegeven, wordt de standaardwaarde 8765 gebruikt. |
| `httpPath` | De gedeeltelijke URL die overeenkomt met de [!DNL Phoenix] server. /hbasephoenix0 opgeven bij gebruik [!DNL Azure] HDInsightcluster. |
| `enableSsl` | Een booleaanse waarde. Geeft aan of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Phoenix] is: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Zie voor meer informatie over het aan de slag gaan [dit Phoenix-document](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een basisverbinding tot stand te brengen, doe een verzoek van de POST aan `/connections` als u uw [!DNL Phoenix] verificatiegegevens in de aanvraaginstantie.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Aan de hand van deze zelfstudie hebt u een [!DNL Phoenix] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/database-nosql.md)
