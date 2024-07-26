---
title: Eindpunt van openbaar certificaat
description: Leer hoe te om uw openbare certificaten terug te winnen gebruikend het /public-certificate eindpunt van de Dienst MTLS API.
role: Developer
source-git-commit: ce02c1a15d4e87c130de5e6133edda6b66cc2196
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---

# Openbaar certificaateindpunt

Deze gids verklaart hoe te om het openbare certificaateindpunt te gebruiken om openbare certificaten voor de toepassingen van de Adobe van uw organisatie veilig terug te winnen. Het omvat een voorbeeld API vraag en gedetailleerde instructies om ontwikkelaars te helpen voor authentiek verklaren en gegevensuitwisseling verifiëren.

## Aan de slag

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## API-paden {#paths}

De volgende informatie is de essentiële API-paden die u nodig hebt om de mTLS Service API te gebruiken. Dit zijn onder andere de platformgateway-URL, het basispad voor de API en een voorbeeld van een volledig pad voor het ophalen van een openbaar certificaat.

- PLATFORM Gateway URL: `https://platform.adobe.io/`
- Basispad voor deze API: `/data/core/mtls`
- Voorbeeld van een volledig pad: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Uw openbare certificaten ophalen {#list}

U kunt de openbare certificaten voor om het even welk van de toepassingen van de Adobe van uw organisatie terugwinnen door een verzoek van de GET tot het `/v1/certificate/public-certificate` eindpunt te richten.

**API formaat**

```http
GET /v1/certificate/public-certificate
```

De volgende facultatieve vraagparameters kunnen worden gebruikt wanneer het terugwinnen van uw openbare certificaten.

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `page` | Hiermee geeft u op vanaf welke pagina de resultaten van uw aanvraag moeten beginnen. | `page=5` |
| `limit` | Het maximumaantal openbare certificaten dat u per pagina wilt ophalen. | `limit=20` |

{style="table-layout:auto"}

**Verzoek**

Een steekproefverzoek om de openbare certificaten verbonden aan uw organisatie terug te keren wordt gezien in de doen ineenstorten hieronder sectie.

+++Sampleaanvraag

```shell
curl -X GET https://experience.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP terug en maakt een lijst van de openbare certificaten voor uw organisatie.

+++A monster met succes

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `certCommonName` | De algemene naam (CN) van het certificaat, die doorgaans de naam of identiteit vertegenwoordigt van de server of entiteit waaraan het certificaat wordt uitgegeven. |
| `publicCertificate` | Het daadwerkelijke openbare certificaat in een koordformaat, dat voor het voor authentiek verklaren en het coderen van mededelingen wordt gebruikt. |
| `expiryDate` | De datum en het tijdstip waarop het openbare certificaat verloopt, zoals weergegeven in ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Volgende stappen

Na het lezen van deze handleiding leert u nu hoe u uw openbare certificaten kunt ophalen met de Adobe Experience Platform API. Meer leren over het beheren van klantengegevens om naleving van verordeningen en organisatorisch beleid te verzekeren, zie het [ overzicht van het Beheer van Gegevens ](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->

