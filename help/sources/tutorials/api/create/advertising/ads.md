---
title: Een Google Ads Base Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform met Google Ads kunt verbinden met behulp van de Flow Service API.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# Een basisverbinding voor Google Ads maken met de API [!DNL Flow Service]

>[!WARNING]
>
>De [!DNL Google Ads] -bron is tijdelijk niet beschikbaar. Adobe werkt aan het oplossen van problemen met deze bron.

>[!NOTE]
>
>De Google Ads-bron is bèta. Zie het [ Overzicht van Bronnen ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor Google Ads tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met Google Ads met de API [!DNL Flow Service] .

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met Google Ads als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientCustomerId` | De client-id is het accountnummer dat overeenkomt met de Google Ads-clientaccount die u wilt beheren met de Google Ads-API. Deze id volgt de sjabloon van `123-456-7890` . |
| `loginCustomerId` | De inlogklant-id is het accountnummer dat overeenkomt met uw Google Ads Manager-account en wordt gebruikt om rapportgegevens van een specifieke operationele klant op te halen. Voor meer informatie over login identiteitskaart van de klantenklant, lees de [ API documentatie van Google Ads ](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Met de ontwikkelaarstoken hebt u toegang tot de API voor Google Ads. U kunt dezelfde ontwikkelaarstoken gebruiken om aanvragen in te dienen voor al uw Google Ads-accounts. Haal uw ontwikkelaarstoken door [ het programma openen aan uw managerrekening ](https://ads.google.com/home/tools/manager-accounts/) op en navigeert dan aan de [!DNL API Center] pagina. |
| `refreshToken` | Het token Vernieuwen maakt deel uit van [!DNL OAuth2] -verificatie. Dit teken staat u toe om uw toegangstokens na het verlopen opnieuw te produceren. |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van [!DNL OAuth2] -verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van [!DNL OAuth2] -verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor Google Ads is: `d771e9c1-4f26-40dc-8617-ce58c4b53702` . |

Lees het API overzichtsdocument voor [ meer informatie over het worden begonnen met Ads van Google ](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw de authentificatiegeloofsbrieven van de Advertentie van Google als deel van de verzoekparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor Google Ads gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.clientCustomerID` | De client-id van je Google Ads-account. |
| `auth.params.loginCustomerID` | De aanmeldings-id die overeenkomt met uw Google Ads Manager-account. |
| `auth.params.developerToken` | De ontwikkelaarstoken van uw Google Ads-account. |
| `auth.params.refreshToken` | Het token Vernieuwen van je Google Ads-account. |
| `auth.params.clientID` | De client-id van je Google Ads-account. |
| `auth.params.clientSecret` | Het clientgeheim van je Google Ads-account. |
| `connectionSpec.id` | The Google Ads connection specification ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een basisverbinding voor Google Ads gemaakt met de API [!DNL Flow Service] . U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om reclamegegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/advertising.md)
