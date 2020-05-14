---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Maak een Apache Spark op Azure HDInsights-connector met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---


# Maak een Apache Spark op Azure HDInsights-connector met de Flow Service API

>[!NOTE]
>De Apache Spark op Azure HDInsights-connector is in bèta. De functies en documentatie kunnen worden gewijzigd.

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Apache Spark op Azure HDInsights (hierna &quot;Spark&quot; genoemd) aan Experience Platform te koppelen.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met de Vonk te verbinden gebruikend de Dienst API van de Stroom.

### Vereiste referenties verzamelen

Opdat de Dienst van de Stroom met Vonk verbindt, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP adres of de gastheernaam van de server van de Vonk. |
| `username` | De gebruikersnaam die u gebruikt om tot de Server van de Vonk toegang te hebben. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De identiteitskaart van de verbindingsspecificatie voor Vonk is: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

Voor meer informatie over begonnen worden verwijs naar [dit document](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)van Vonk.

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

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Slechts één verbinding wordt vereist per de rekening van de Vonk aangezien het kan worden gebruikt om veelvoudige bronschakelaars tot stand te brengen om verschillende gegevens in te brengen.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een verbinding van de Vonk tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het POST- verzoek worden verstrekt. De identiteitskaart van de verbindingsspecificatie voor Vonk is `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | De gastheer van de server van de Vonk. |
| `auth.params.username` | De gebruikersnaam die aan uw verbinding van de Vonk wordt gekoppeld. |
| `auth.params.password` | Het wachtwoord verbonden aan uw verbinding van de Vonk. |
| `connectionSpec.id` | ID van de de verbindingsspecificatie van de Vonk: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding van de Vonk gecreeerd gebruikend de Dienst API van de Stroom en hebt de unieke waarde van identiteitskaart van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u databases kunt [verkennen met behulp van de Flow Service API](../../explore/database-nosql.md).