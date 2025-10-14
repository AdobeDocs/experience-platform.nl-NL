---
title: Google-advertenties met API's verbinden met Experience Platform
description: Leer hoe u Adobe Experience Platform met Google Ads kunt verbinden met behulp van de Flow Service API.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL Google Ads]

>[!NOTE]
>
>De bron [!DNL Google Ads] is in bèta. Zie het [&#x200B; Overzicht van Bronnen &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees dit leerprogramma leren hoe te om uw [!DNL Google Ads] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Google Ads] via de [!DNL Flow Service] API.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

### Vereiste referenties verzamelen

Voor informatie over authentificatie, lees het [[!DNL Google Ads]  bronoverzicht &#x200B;](../../../../connectors/advertising/ads.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een POST- verzoek aan het `/connections` eindpunt terwijl het verstrekken van uw de authentificatiegeloofsbrieven van Google Ads als deel van de verzoekparameters.

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
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v17"

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
| `auth.params.clientCustomerID` | De client-id van uw [!DNL Google Ads] -account. |
| `auth.params.loginCustomerID` | De aanmeldings-id die overeenkomt met uw [!DNL Google Ads] manager-account. |
| `auth.params.developerToken` | De ontwikkelaarstoken van uw [!DNL Google Ads] account. |
| `auth.params.refreshToken` | Het vernieuwingstoken van uw [!DNL Google Ads] account. |
| `auth.params.clientID` | De client-id van uw [!DNL Google Ads] -account. |
| `auth.params.clientSecret` | Het clientgeheim van uw [!DNL Google Ads] -account. |
| `auth.params.googleAdsApiVersion` | De API-versie van [!DNL Google Ads] die u gebruikt. De meest recente ondersteunde versie op Experience Platform is `v17` . |
| `connectionSpec.id` | The [!DNL Google Ads] connection specification ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Een gegevensstroom maken voor het opnemen van advertentiegegevens

Aan de hand van deze zelfstudie hebt u een [!DNL Google Ads] basisverbinding gemaakt met de [!DNL Flow Service] API en uw [!DNL Google Ads] -account verbonden met Experience Platform. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om reclamegegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/advertising.md)
