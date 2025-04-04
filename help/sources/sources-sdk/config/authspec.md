---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Verificatiespecs voor Self-Serve Bronnen configureren (Batch SDK)
description: Dit document biedt een overzicht van de configuraties die u moet voorbereiden voor het gebruik van Self-Serve Sources (Batch SDK).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Verificatiespecs voor Self-Serve Bronnen configureren (Batch SDK)

Verificatiespects bepalen hoe Adobe Experience Platform-gebruikers verbinding kunnen maken met uw bron.

De array `authSpec` bevat informatie over de verificatieparameters die zijn vereist om een bron te verbinden met Experience Platform. Om het even welke bepaalde bron kan veelvoudige verschillende types van authentificatie steunen.

## Verificatiespects

Self-Serve Bronnen (Batch SDK) ondersteunt OAuth 2 en vernieuwt codes en basisverificatie. Zie de lijsten hieronder voor begeleiding bij het gebruiken van OAuth 2 verfrist code en basisauthentificatie

### Code voor 2 vernieuwen

OAuth 2 verfrist code voor veilige toegang tot een toepassing door een tijdelijk toegangstoken te produceren en een verfrist teken. Het toegangstoken staat u toe om tot uw middelen veilig toegang te hebben zonder het moeten andere geloofsbrieven verstrekken, terwijl verfrist het teken u toestaat om een nieuw toegangstoken te produceren, zodra het toegangstoken verloopt.

+++Voorbeeld van een OAuth 2 vernieuwt code

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

{style="table-layout:auto"}

+++

### Basisverificatie

Basisverificatie is een verificatietype waarmee u toegang krijgt tot uw toepassing door een combinatie van uw gebruikersnaam en wachtwoord voor uw account te gebruiken.

+++ Voorbeeld van basisverificatie weergeven

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
| `authSpec.spec.properties.username` | De gebruikersnaam van de account die aan uw toepassing is gekoppeld. |
| `authSpec.spec.properties.password` | Het accountwachtwoord dat aan uw toepassing is gekoppeld. |
| `authSpec.spec.required` | Hiermee geeft u de velden op die vereist zijn als verplichte waarden die in Experience Platform moeten worden ingevoerd. | `username` |

{style="table-layout:auto"}

+++

### API-sleutelverificatie {#api-key-authentication}

API-sleutelverificatie is een veilige methode voor toegang tot API&#39;s door een API-sleutel en andere relevante verificatieparameters in aanvragen op te geven. Afhankelijk van uw specifieke API-informatie kunt u de API-sleutel verzenden als onderdeel van de aanvraagkoptekst, queryparameters of de hoofdtekst.

De volgende parameters zijn doorgaans vereist wanneer API-sleutelverificatie wordt gebruikt:

| Parameter | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| `host` | string | Nee | De bron-URL. |
| `authKey1` | string | Ja | De eerste vereiste verificatiesleutel voor API-toegang. Het wordt gewoonlijk verzonden in de verzoekkopbal of vraagparameters. |
| `authKey2` | string | Optioneel | Een tweede verificatietoets. Indien vereist, wordt deze sleutel vaak gebruikt om verzoeken verder te bevestigen. |
| `authKeyN` | string | Optioneel | Een extra verificatievariabele die naar wens kan worden gebruikt, maar de API. |

{style="table-layout:auto"}

+++API-sleutelverificatie weergeven

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### Verificatiegedrag

U kunt de parameter `restAttributes` gebruiken om te bepalen hoe de API-sleutel in de aanvraag moet worden opgenomen. In het onderstaande voorbeeld geeft het kenmerk `headerParamName` bijvoorbeeld aan dat `X-Auth-Key1` als koptekst moet worden verzonden.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

Elke verificatiesleutel (zoals `authKey1` , `authKey2` , enz.) kan aan `restAttributes` worden gekoppeld om te bepalen hoe deze als aanvraag wordt verzonden.

Als `authKey1` `"headerParamName": "X-Auth-Key1"` heeft. Dit betekent dat de aanvraagheader `X-Auth-Key:{YOUR_AUTH_KEY1}` moet bevatten. Bovendien hoeven de sleutelnaam en `headerParamName` niet noodzakelijkerwijs hetzelfde te zijn. Bijvoorbeeld:

* De `authKey1` kan `headerParamName: X-Custom-Auth-Key` hebben. Dit betekent dat de aanvraagheader `X-Custom-Auth-Key` in plaats van `authKey1` gebruikt.
* Omgekeerd kan `authKey1` `headerParamName: authKey1` hebben. Dit betekent dat de naam van de aanvraagkoptekst ongewijzigd blijft.

**Voorbeeld API formaat**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## Voorbeeld van verificatiespecificatie

Hieronder ziet u een voorbeeld van een voltooide verificatiespecificatie met een [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) -bron.

+++Specificatie van voorbeeldverificatie weergeven

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

+++

## Volgende stappen

Met uw bevolkte authentificatiespecificaties, kunt u te werk gaan om de bronspecificaties voor de bron te vormen die u aan Experience Platform wilt integreren. Zie het document op [ vormend bronspecificaties ](./sourcespec.md) voor meer informatie.
