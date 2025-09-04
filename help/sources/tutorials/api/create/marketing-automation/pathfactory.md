---
title: Een PathFactory Base Connection maken met de Flow Service API
description: Leer hoe u uw PathFactory-account op Experience Platform verifieert met behulp van de Flow Service API.
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# Een [!DNL PathFactory] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees dit document om te leren hoe te om een basisverbinding voor [!DNL PathFactory] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

In de volgende sectie vindt u aanvullende informatie die u moet weten als u verbinding wilt maken met [!DNL PathFactory] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen {#gather-credentials}

U moet de volgende waarden opgeven om toegang te krijgen tot uw PathFactory-account op de Experience Platform:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Gebruikersnaam | Uw [!DNL PathFactory] gebruikersnaam van de account. Dit is essentieel voor het identificeren van uw account in het systeem. |
| Wachtwoord | Het wachtwoord dat aan uw [!DNL PathFactory] account is gekoppeld. Zorg ervoor dat dit veilig blijft om ongeoorloofde toegang te voorkomen. |
| Domein | Het domein dat aan uw [!DNL PathFactory] account is gekoppeld. Dit verwijst doorgaans naar de unieke id in de [!DNL PathFactory] URL. |
| Toegangstoken | Een uniek token dat wordt gebruikt voor API-verificatie om te zorgen voor veilige communicatie tussen uw systemen en [!DNL PathFactory] . |
| API-eindpunten | Specifieke API-eindpunten voor toegang tot gegevens: Bezoekers, Sessies en Paginaweergaven. Elk eindpunt komt overeen met verschillende gegevenssets die u kunt ophalen. **Nota:** deze zijn vooraf bepaald door [!DNL PathFactory] en zijn specifiek voor de gegevens u van plan bent toegang te hebben: <ul><li>**Eindpunt van Bezoekers**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Eindpunt van zittingen**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Eindpunt van de Mening van de Pagina**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Voor meer informatie over hoe te om uw geloofsbrieven te beveiligen en te gebruiken, en hoe te om uw toegangstoken te verkrijgen en te verfrissen, bezoek het [[!DNL PathFactory]  Centrum van de Steun ](https://support.pathfactory.com/categories/adobe/). Deze bron bevat uitgebreide handleidingen voor het beheer van uw referenties en voor een effectieve en veilige API-integratie.

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL PathFactory] -verificatiegegevens op als onderdeel van de aanvraagprocedure.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL PathFactory] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.clientId` | De client-id die aan uw [!DNL PathFactory] -toepassing is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan de toepassing [!DNL PathFactory] is gekoppeld. |
| `connectionSpec.id` | The [!DNL PathFactory] connection specification ID: `ea1c2a08-b722-11eb-8529-0242ac130003` . |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL PathFactory] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om marketing automatiseringsgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/marketing-automation.md)
