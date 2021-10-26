---
keywords: Experience Platform;thuis;populaire onderwerpen;generische REST;generische rest
solution: Experience Platform
title: Een algemene REST API-basisverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Generic REST API met de Flow Service API kunt verbinden met Adobe Experience Platform.
source-git-commit: 1a9c4d5ba3ba9201378e78c0e92dea5101668a24
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Een algemene REST API-basisverbinding maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Generic REST API] De bron is in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Generic REST API] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Generic REST API], moet u geldige geloofsbrieven voor het authentificatietype van uw keus verstrekken. [!DNL Generic REST API] steunt zowel OAuth 2 vernieuwt code en basisauthentificatie. Zie de volgende lijsten voor informatie over de geloofsbrieven voor de twee gesteunde authentificatietypen.

#### Code voor 2 vernieuwen

| Credentials | Beschrijving |
| --- | --- |
| `host` | De host-URL van de bron waarnaar u een verzoek indient. Deze waarde is vereist en kan niet worden omzeild met `requestParameterOverride`. |
| `authorizationTestUrl` | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `clientId` | (Optioneel) De client-id die aan uw gebruikersaccount is gekoppeld. |
| `clientSecret` | (Optioneel) Het clientgeheim dat aan uw gebruikersaccount is gekoppeld. |
| `accessToken` | De primaire verificatiereferentie die wordt gebruikt voor toegang tot uw toepassing. Het toegangstoken vertegenwoordigt de toestemming van uw toepassing, om tot bepaalde aspecten van de gegevens van een gebruiker toegang te hebben. Deze waarde is vereist en kan niet worden omzeild met `requestParameterOverride`. |
| `refreshToken` | (Optioneel) Een token dat wordt gebruikt om een nieuw toegangstoken te genereren wanneer het toegangstoken is verlopen. |
| `expirationDate` | (Optioneel) Een verborgen waarde die de vervaldatum van uw toegangstoken definieert. |
| `accessTokenUrl` | (Optioneel) Het URL-eindpunt dat wordt gebruikt om uw toegangstoken op te halen. |
| `requestParameterOverride` | (Optioneel) Een eigenschap waarmee u kunt opgeven welke referentie-parameters moeten worden overschreven. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Generic REST API] is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Basisverificatie

| Credentials | Beschrijving |
| --- | --- |
| `host` | De host-URL van de bron waarnaar u een verzoek indient. |
| `username` | De gebruikersnaam die overeenkomt met uw gebruikersaccount. |
| `password` | Het wachtwoord dat overeenkomt met uw gebruikersaccount. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Generic REST API] is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

[!DNL Generic REST API] steunt zowel basisauthentificatie als OAuth 2 verfrist code. Zie de volgende voorbeelden voor begeleiding op hoe te met één van beide authentificatietypen voor authentiek te verklaren.

### Een [!DNL Generic REST API] basisverbinding met OAuth 2-vernieuwingscode

Om een identiteitskaart van de basisverbinding tot stand te brengen gebruikend OAuth 2 verfrist code, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw OAuth 2 geloofsbrieven.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `name` | De naam van uw basisverbinding. Zorg ervoor dat de naam van uw basisverbinding beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw basisverbinding te zoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de basisverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id die is gekoppeld aan [!DNL Generic REST API]. Deze vaste ID is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Het authentificatietype dat u gebruikt om uw bron aan Platform voor authentiek te verklaren. |
| `auth.params.host` | De basis-URL waarmee u verbinding maakt met uw [!DNL Generic REST API] bron. |
| `auth.params.accessToken` | Het overeenkomstige toegangstoken dat wordt gebruikt om uw bron voor authentiek te verklaren. Dit is vereist voor verificatie op basis van OAuth. |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Een [!DNL Generic REST API] basisverbinding met basisverificatie

Als u een [!DNL Generic REST API] basisverbinding die basisauthentificatie gebruikt, doe een verzoek van de POST aan `/connections` eindpunt van [!DNL Flow Service] API terwijl het verstrekken van uw basisauthentificatiegeloofsbrieven.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw basisverbinding. Zorg ervoor dat de naam van uw basisverbinding beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw basisverbinding te zoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor meer informatie over de basisverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id die is gekoppeld aan [!DNL Generic REST API]. Deze vaste ID is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verbinden met Platform. |
| `auth.params.host` | De basis-URL waarmee u verbinding maakt met uw [!DNL Generic REST API] bron. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw [!DNL Generic REST API] bron. Dit is vereist voor basisverificatie. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw [!DNL Generic REST API] bron. Dit is vereist voor basisverificatie. |

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding, inclusief de unieke verbindingsidentificatie (`id`). Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Generic REST API] verbinding met de [!DNL Flow Service] API en hebben de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u [protocoltoepassingen verkennen met behulp van de Flow Service API](../../explore/protocols.md).
