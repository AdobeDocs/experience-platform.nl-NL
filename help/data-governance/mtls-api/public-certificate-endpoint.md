---
title: Eindpunt van openbaar certificaat
description: Leer hoe te om uw openbare certificaten terug te winnen gebruikend het /public-certificate eindpunt van de Dienst MTLS API.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Openbaar certificaateindpunt

>[!NOTE]
>
>Adobe biedt geen ondersteuning meer voor het statische downloaden van openbare mTLS-certificaten. Gebruik deze API om geldige certificaten op te halen voor uw integratie. Automatisch ophalen is nu vereist om onderbreking van de service te voorkomen.

Deze gids verklaart hoe te om het openbare certificaateindpunt te gebruiken om openbare certificaten voor de toepassingen van Adobe van uw organisatie veilig terug te winnen. Het omvat een voorbeeld API vraag en gedetailleerde instructies om ontwikkelaars te helpen voor authentiek verklaren en gegevensuitwisseling verifiëren.

## Aan de slag

Alvorens verder te gaan, herzie [ begonnen gids ](./getting-started.md) voor belangrijke details over vereiste kopballen en hoe te om voorbeeld API vraag te interpreteren.

## API-paden {#paths}

De volgende informatie is de essentiële API-paden die u nodig hebt om de mTLS Service API te gebruiken. Dit zijn onder andere de platformgateway-URL, het basispad voor de API en een voorbeeld van een volledig pad voor het ophalen van een openbaar certificaat.

- PLATFORM Gateway URL: `https://platform.adobe.io/`
- Basispad voor deze API: `/data/core/mtls`
- Voorbeeld van een volledig pad: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Uw openbare certificaten ophalen {#list}

Voer een GET-verzoek in bij het `/v1/certificate/public-certificate` -eindpunt om de openbare certificaten op te halen voor Adobe-toepassingen van uw organisatie.

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
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
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

## Automatisering van certificaatlevenscyclus {#certificate-lifecycle-automation}

Adobe automatiseert de levenscyclus van openbare mTLS certificaten om continuïteit te verzekeren en de onderbrekingen van de dienst te verminderen.

- Certificaten worden 60 dagen voor het verstrijken opnieuw afgegeven.
- Certificaten worden 30 dagen voor het verlopen ingetrokken.

>[!NOTE]
>
>Deze chronologie zal in tijd korten in groepering met [ CA/B de richtlijnen van het Forum ](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), die erop gericht zijn certificaatlevens tot een maximum van 47 dagen te verminderen.

U moet uw integratie bijwerken om geautomatiseerde herwinning via API te steunen. Vertrouw niet op handmatige certificaatdownloads of statische kopieën, aangezien deze kunnen resulteren in verlopen of ingetrokken certificaten.

## Volgende stappen

Nadat u uw openbare certificaten hebt opgehaald met behulp van de API, werkt u uw integratie bij om dit eindpunt regelmatig aan te roepen voordat certificaten verlopen. Om deze vraag interactively te testen, bezoek de [ MTLS API verwijzingspagina ](https://developer.adobe.com/experience-platform-apis/references/mtls-service/). Voor bredere begeleiding op op certificaat-gebaseerde integratie, zie de [ encryptie van Gegevens in het overzicht van Adobe Experience Platform ](../../landing/governance-privacy-security/encryption.md) of het [ overzicht van het Beheer van Gegevens ](../home.md).
