---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Verificatiespecificaties configureren voor Self-Serve Sources (Batch SDK)
topic-legacy: overview
description: Dit document biedt een overzicht van de configuraties die u moet voorbereiden om Self-Serve Sources (Batch SDK) te kunnen gebruiken.
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 25e0061cc47ec4179f3f02958eb8bda1714ea139
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---

# Verificatiespecificaties configureren voor Self-Serve Sources (Batch SDK)

De verificatiespecificaties bepalen hoe Adobe Experience Platform-gebruikers verbinding kunnen maken met uw bron.

De `authSpec` array bevat informatie over de verificatieparameters die zijn vereist om een bron te verbinden met een Platform. Om het even welke bepaalde bron kan veelvoudige verschillende soorten authentificatie steunen.

## Verificatiespecificaties

Self-Serve Bronnen (Batch SDK) steunt OAuth 2 verfrist codes en basisauthentificatie. Zie de lijsten hieronder voor begeleiding bij het gebruiken van OAuth 2 verfrist code en basisauthentificatie

### Code voor 2 vernieuwen

OAuth 2 verfrist code voor veilige toegang tot een toepassing door een tijdelijk toegangstoken te produceren en een verfrist teken. Het toegangstoken staat u toe om tot uw middelen veilig toegang te hebben zonder het moeten andere geloofsbrieven verstrekken, terwijl verfrist het teken u toestaat om een nieuw toegangstoken te produceren, zodra het toegangstoken verloopt.

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| Eigenschap | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `authSpec.name` | Geeft de naam van het ondersteunde verificatietype weer. | `oAuth2-refresh-code` |
| `authSpec.type` | Definieert het type verificatie dat door de bron wordt ondersteund. | `oAuth2-refresh-code` |
| `authSpec.spec` | Bevat informatie over het schema van de authentificatie, gegevenstype, en eigenschappen. |
| `authSpec.spec.$schema` | Bepaalt het schema dat voor de authentificatie wordt gebruikt. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definieert het gegevenstype van het schema. | `object` |
| `authSpec.spec.properties` | Bevat informatie over de geloofsbrieven die voor de authentificatie worden gebruikt. |
| `authSpec.spec.properties.description` | Hiermee geeft u een korte beschrijving van de referentie weer. |
| `authSpec.spec.properties.type` | Definieert het gegevenstype van de referentie. | `string` |
| `authSpec.spec.properties.clientId` | De client-id die aan uw toepassing is gekoppeld. De client-id wordt samen met het clientgeheim gebruikt om uw toegangstoken op te halen. |
| `authSpec.spec.properties.clientSecret` | Het clientgeheim dat aan uw toepassing is gekoppeld. Het clientgeheim wordt gebruikt in combinatie met uw client-id om uw toegangstoken op te halen. |
| `authSpec.spec.properties.accessToken` | Met het toegangstoken hebt u toegang tot uw toepassing. |
| `authSpec.spec.properties.refreshToken` | Vernieuw teken wordt gebruikt om een nieuw toegangstoken te produceren, wanneer het toegangstoken verloopt. |
| `authSpec.spec.properties.expirationDate` | Bepaalt de vervaldatum van het toegangstoken. |
| `authSpec.spec.properties.refreshTokenUrl` | De URL die wordt gebruikt om uw vernieuwingstoken op te halen. |
| `authSpec.spec.properties.accessTokenUrl` | De URL die wordt gebruikt om uw vernieuwingstoken op te halen. |
| `authSpec.spec.properties.requestParameterOverride` | Hiermee kunt u referentie-parameters opgeven die moeten worden overschreven bij verificatie. |
| `authSpec.spec.required` | Toont de geloofsbrieven die worden vereist om voor authentiek te verklaren. | `accessToken` |

{style=&quot;table-layout:auto&quot;}


### Basisverificatie

Basisverificatie is een verificatietype waarmee u toegang krijgt tot uw toepassing door een combinatie van uw gebruikersnaam en wachtwoord voor uw account te gebruiken.

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| Eigenschap | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `authSpec.name` | Geeft de naam van het ondersteunde verificatietype weer. | `Basic Authentication` |
| `authSpec.type` | Definieert het type verificatie dat door de bron wordt ondersteund. | `BasicAuthentication` |
| `authSpec.spec` | Bevat informatie over het schema van de authentificatie, gegevenstype, en eigenschappen. |
| `authSpec.spec.$schema` | Bepaalt het schema dat voor de authentificatie wordt gebruikt. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definieert het gegevenstype van het schema. | `object` |
| `authSpec.spec.description` | Geeft meer informatie weer specifiek voor uw verificatietype. |
| `authSpec.spec.properties` | Bevat informatie over de geloofsbrieven die voor de authentificatie worden gebruikt. |
| `authSpec.spec.properties.username` | De accountgebruikersnaam die aan uw toepassing is gekoppeld. |
| `authSpec.spec.properties.password` | Het accountwachtwoord dat aan uw toepassing is gekoppeld. |
| `authSpec.spec.required` | Hiermee geeft u de velden op die verplicht moeten worden ingevuld in het Platform. | `username` |

{style=&quot;table-layout:auto&quot;}

## Voorbeeld van verificatiespecificatie

Hier volgt een voorbeeld van een voltooide verificatiespecificatie met behulp van een [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) bron.

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

## Volgende stappen

Met uw bevolkte authentificatiespecificaties, kunt u te werk gaan om de bronspecificaties voor de bron te vormen die u aan Platform wilt integreren. Het document weergeven op [bronspecificaties configureren](./sourcespec.md) voor meer informatie .
