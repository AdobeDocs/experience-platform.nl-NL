---
keywords: Experience Platform;home;populaire onderwerpen;generieke REST;algemene rest
solution: Experience Platform
title: Een algemene REST API-basisverbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Generic REST API met de Flow Service API kunt verbinden met Adobe Experience Platform.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# Een algemene REST API-basisverbinding maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De bron [!DNL Generic REST API] is in bèta. Zie het [&#x200B; Bronoverzicht &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Generic REST API] tot stand te brengen gebruikend [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

### Vereiste referenties verzamelen

Als u wilt dat [!DNL Flow Service] verbinding maakt met [!DNL Generic REST API] , moet u geldige referenties opgeven voor het gewenste verificatietype. [!DNL Generic REST API] ondersteunt zowel OAuth 2 om code te vernieuwen als basisverificatie. Zie de volgende lijsten voor informatie over de geloofsbrieven voor de twee gesteunde authentificatietypen.

#### Code voor 2 vernieuwen

| Credentials | Beschrijving |
| --- | --- |
| `host` | De host-URL van de bron waarnaar u een verzoek indient. Deze waarde is vereist en kan niet worden overgeslagen met `requestParameterOverride` . |
| `authorizationTestUrl` | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| `clientId` | (Optioneel) De client-id die aan uw gebruikersaccount is gekoppeld. |
| `clientSecret` | (Optioneel) Het clientgeheim dat aan uw gebruikersaccount is gekoppeld. |
| `accessToken` | De primaire verificatiereferentie die wordt gebruikt voor toegang tot uw toepassing. Het toegangstoken vertegenwoordigt de toestemming van uw toepassing, om tot bepaalde aspecten van de gegevens van een gebruiker toegang te hebben. Deze waarde is vereist en kan niet worden overgeslagen met `requestParameterOverride` . |
| `refreshToken` | (Optioneel) Een token dat wordt gebruikt om een nieuw toegangstoken te genereren wanneer het toegangstoken is verlopen. |
| `expirationDate` | (Optioneel) Een verborgen waarde die de vervaldatum van uw toegangstoken definieert. |
| `accessTokenUrl` | (Optioneel) Het URL-eindpunt dat wordt gebruikt om uw toegangstoken op te halen. |
| `requestParameterOverride` | (Optioneel) Een eigenschap waarmee u kunt opgeven welke referentie-parameters moeten worden overschreven. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Generic REST API] is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62` . |

#### Basisverificatie

| Credentials | Beschrijving |
| --- | --- |
| `host` | De host-URL van de bron waarnaar u een verzoek indient. |
| `username` | De gebruikersnaam die overeenkomt met uw gebruikersaccount. |
| `password` | Het wachtwoord dat overeenkomt met uw gebruikersaccount. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Generic REST API] is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62` . |

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

[!DNL Generic REST API] ondersteunt zowel basisverificatie als OAuth 2-vernieuwingscode. Zie de volgende voorbeelden voor begeleiding op hoe te met één van beide authentificatietypen voor authentiek te verklaren.

### Een [!DNL Generic REST API] basisverbinding maken met OAuth 2-vernieuwingscode

Om een identiteitskaart van de basisverbinding tot stand te brengen gebruikend OAuth 2 verfrist code, doe een POST- verzoek aan het `/connections` eindpunt terwijl het verstrekken van uw OAuth 2 geloofsbrieven.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Generic REST API] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `connectionSpec.id` | De verbindingsspecificatie-id die aan [!DNL Generic REST API] is gekoppeld. Deze vaste id is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62` . |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verifiëren bij Experience Platform. |
| `auth.params.host` | De basis-URL waarmee verbinding wordt gemaakt met de [!DNL Generic REST API] -bron. |
| `auth.params.accessToken` | Het overeenkomstige toegangstoken dat wordt gebruikt om uw bron voor authentiek te verklaren. Dit is vereist voor verificatie op basis van OAuth. |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Een [!DNL Generic REST API] basisverbinding maken met behulp van basisverificatie

Als u een [!DNL Generic REST API] -basisverbinding wilt maken met behulp van basisverificatie, vraagt u een POST-aanvraag naar het `/connections` eindpunt van de [!DNL Flow Service] API en geeft u uw basisverificatiegegevens op.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Generic REST API] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `connectionSpec.id` | De verbindingsspecificatie-id die aan [!DNL Generic REST API] is gekoppeld. Deze vaste id is: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62` . |
| `auth.specName` | Het verificatietype dat u gebruikt om uw bron te verbinden met Experience Platform. |
| `auth.params.host` | De basis-URL waarmee verbinding wordt gemaakt met de [!DNL Generic REST API] -bron. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw [!DNL Generic REST API] -bron. Dit is vereist voor basisverificatie. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw [!DNL Generic REST API] -bron. Dit is vereist voor basisverificatie. |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde basisverbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om de bestandsstructuur en inhoud van uw bron in de volgende stap te verkennen.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Generic REST API] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om protocolgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/protocols.md)
