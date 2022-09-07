---
keywords: Experience Platform;thuis;populaire onderwerpen;Google-advertenties;Google-advertenties;google-advertenties;advertenties
title: Een Google Ads Base Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform met Google Ads kunt verbinden met behulp van de Flow Service API.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# Een Google Ads-basisverbinding maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De Google Ads-bron is bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

In deze zelfstudie worden de stappen doorlopen waarmee u een basisverbinding voor Google Ads kunt maken met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Experience Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Experience Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met Google Ads via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] Als u verbinding wilt maken met Google Ads, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientCustomerId` | De client-id is het accountnummer dat overeenkomt met de Google Ads-clientaccount die u wilt beheren met de Google Ads-API. Deze id volgt de sjabloon van `123-456-7890`. |
| `developerToken` | Met de ontwikkelaarstoken hebt u toegang tot de API voor Google Ads. U kunt dezelfde ontwikkelaarstoken gebruiken om aanvragen in te dienen voor al uw Google Ads-accounts. Haal de ontwikkelaarstoken op door [aanmelden bij uw beheerdersaccount](https://ads.google.com/home/tools/manager-accounts/) en navigeert vervolgens naar de [!DNL API Center] pagina. |
| `refreshToken` | Het token Vernieuwen maakt deel uit van [!DNL OAuth2] verificatie. Dit teken staat u toe om uw toegangstokens na het verlopen opnieuw te produceren. |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van [!DNL OAuth2] verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van [!DNL OAuth2] verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor Google Ads is: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Het API-overzichtsdocument lezen voor [meer informatie over hoe je aan de slag gaat met Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw de authentificatiegeloofsbrieven van Google Adds als deel van de verzoekparameters.

**API-indeling**

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
| `auth.params.developerToken` | De ontwikkelaarstoken van uw Google Ads-account. |
| `auth.params.refreshToken` | Het token Vernieuwen van je Google Ads-account. |
| `auth.params.clientID` | De client-id van je Google Ads-account. |
| `auth.params.clientSecret` | Het clientgeheim van je Google Ads-account. |
| `connectionSpec.id` | De Google Ads-verbindingsspecificatie-id: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een Google Ads-basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om advertentiegegevens naar het Platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/advertising.md)
