---
title: Sects, eindpunt
description: Leer hoe te om vraag aan het /secrets eindpunt in Reactor API te maken.
exl-id: 76875a28-5d13-402d-8543-24db7e2bee8e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 1%

---

# Sects, eindpunt

Een geheim is een middel dat slechts binnen gebeurtenis bestaat die eigenschappen (eigenschappen met een `platform` kenmerk ingesteld op `edge`). Zij staan gebeurtenis toe door:sturen om aan een ander systeem voor veilige gegevensuitwisseling voor authentiek te verklaren.

Deze gids toont u hoe te om vraag aan te maken `/secrets` eindpunt in de Reactor-API. Voor een gedetailleerde uitleg van de verschillende geheime types en hoe deze te gebruiken, gelieve te verwijzen naar het overzicht op hoog niveau over [geheimen](../guides/secrets.md) voordat u terugkeert naar deze handleiding.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe te voor authentiek te verklaren aan API.

## Een lijst met geheimen voor een eigenschap ophalen {#list-property}

U kunt een lijst maken van de geheimen die tot een bezit behoren door een verzoek van de GET te doen.

**API-indeling**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De id van de eigenschap waarvan u de geheimen wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRe005d921bb724bc88c3ff28e3e916f04/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwoord**

Een succesvolle reactie retourneert een lijst met geheimen die bij de eigenschap horen.

```json
{
  "data": [
    {
      "id": "SE8bd20bd5d16b49ee9d925929e292526c",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:29.777Z",
        "updated_at": "2021-07-16T22:29:29.777Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
          },
          "data": {
            "id": "PRe005d921bb724bc88c3ff28e3e916f04",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/environment"
          },
          "data": {
            "id": "EN80ad9efbf4ff4f15bebd770613378a75",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c",
        "property": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Een lijst met geheimen ophalen voor een omgeving {#list-environment}

U kunt een lijst maken van de geheimen die bij een omgeving horen door een GET-aanvraag in te dienen.

**API-indeling**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| Parameter | Beschrijving |
| --- | --- |
| `{ENVIRONMENT_ID}` | De id van de omgeving waarvan u de geheimen wilt vermelden. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/EN0a1b00749daf4ff48a34d2ec37286aa7/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwoord**

Een succesvol antwoord geeft een lijst met geheimen die bij de omgeving horen.

```json
{
  "data": [
    {
      "id": "SE57b5ea69acde4595825b85befd1675b3",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:35.447Z",
        "updated_at": "2021-07-16T22:29:35.447Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
          },
          "data": {
            "id": "PRb302ca3557334c13b130da719222ec97",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/environment"
          },
          "data": {
            "id": "EN0a1b00749daf4ff48a34d2ec37286aa7",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3",
        "property": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Een geheim opzoeken {#lookup}

U kunt een geheim opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET te omvatten.

**API-indeling**

```http
GET /secrets/{SECRET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SECRET_ID}` | De id van het geheim dat u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwoord**

Een succesvol antwoord geeft de details van het geheim terug.

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## Een geheim maken {#create}

U kunt een geheim tot stand brengen door een verzoek van de POST te doen.

>[!NOTE]
>
>Wanneer u een nieuw geheim creeert, keert API een directe reactie terug die informatie voor die middel bevat. Tegelijkertijd wordt een geheime uitwisselingstaak in werking gesteld om te testen of de referentie-uitwisseling functioneel is. Deze taak wordt asynchroon verwerkt en werkt de statusattributen van het geheim aan bij `succeeded` of `failed` afhankelijk van het resultaat.

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De id van de eigenschap waarop u het geheim wilt definiëren. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR9eff664dc6014217b76939bb78b83976/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Secret",
            "type_of": "simple-http",
            "credentials": {
              "username": "example_username",
              "password": "pass12345"
            }
          },
          "relationships": {
            "environment": {
              "data": {
                "id": "EN04cdddbdb6574170bcac9f470f3b8087",
                "type": "environments"
              }
            }
          },
          "type": "secrets"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | Een unieke, beschrijvende naam voor het geheim. |
| `type_of` | Het type van authentificatiereferentie het geheim vertegenwoordigt. Bevat drie toegestane waarden:<ul><li>`token`: Een tokenreeks.</li><li>`simple-http`: Een gebruikersnaam en wachtwoord.</li><li>`oauth2`: Referenties die voldoen aan de OAuth-norm.</li></ul> |
| `credentials` | Een object dat de referentie-waarden voor het geheim bevat. Afhankelijk van de `type_of` -kenmerk, moeten verschillende eigenschappen worden opgegeven. Zie de sectie over [geloofsbrieven](../guides/secrets.md#credentials) in de geheimengids voor meer informatie over de eisen voor elk type. |
| `relationships.environment` | Elk geheim moet met een milieu worden geassocieerd wanneer het eerst wordt gecreeerd. De `data` object binnen deze eigenschap moet het `id` van het milieu, het geheim dat wordt toegekend, samen met een `type` waarde van `environments`. |
| `type` | Het type resource dat wordt gemaakt. Voor deze aanroep moet de waarde `secrets`. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvol antwoord geeft de details van het geheim terug. Let erop dat sommige eigenschappen, afhankelijk van het type geheim, onder `credentials` kan verborgen zijn.

```json
{
  "data": { 
    "id": "SE39fdf431f8ad4600bbc24ea73fcb1154", 
    "type": "secrets", 
    "attributes": { 
    "created_at": "2021-07-14T19:33:25.628Z", 
    "updated_at": "2021-07-14T19:33:25.628Z", 
    "name": "Example Secret", 
    "type_of": "simple-http", 
    "activated_at": null, 
    "expires_at": null, 
    "refresh_at": null, 
    "status": "pending", 
    "credentials": { 
      "username": "example_username" 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    } 
  } 
}
```

## Een test `oauth2` geheim {#test}

>[!NOTE]
>
>Deze bewerking kan alleen worden uitgevoerd op geheimen met een `type_of` waarde van `oauth2`.

U kunt een `oauth2` geheim door zijn identiteitskaart in de weg van een verzoek van de PATCH te omvatten. De testbewerking voert een uitwisseling uit en neemt de respons van de vergunningverlenende dienst op in de `test_exchange` kenmerk in het geheim `meta` object. Met deze bewerking wordt het geheim zelf niet bijgewerkt.

**API-indeling**

```http
PATCH /secrets/{SECRET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SECRET_ID}` | De id van de `oauth2` geheim dat u wilt testen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SE6c15a7a64f9041b5985558ed3e19a449 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2"
          },
          "meta": {
            "action": "test"
          },
          "id": "SE6c15a7a64f9041b5985558ed3e19a449",
          "type": "secrets"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Moet een `type_of` eigenschap met een waarde van `oauth2`. |
| `meta` | Moet een `action` eigenschap met een waarde van `test`. |
| `id` | De id van het geheim dat u test. Dit moet overeenkomen met de id die is opgegeven in het aanvraagpad. |
| `type` | Het type bron dat wordt gebruikt. Moet worden ingesteld op `secrets`. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

In een succesvol antwoord worden de details van het geheim geretourneerd, waarbij het antwoord van de vergunningverlenende dienst is opgenomen onder `meta.test_exchange`.

```json
{ 
  "data": { 
    "id": "SE6c15a7a64f9041b5985558ed3e19a449", 
    "type": "secrets", 
    "attributes": { 
      "activated_at": null, 
      "created_at": "2021-07-14T19:33:25.628Z", 
      "credentials": { 
        "authorization_url": "https://athorization_url.test/token/authorize?required_param=value",
        "client_id": "test_client_id", 
        "client_secret": "test_client_secret", 
        "refresh_offset": 14400, 
      },
      "expires_at": null, 
      "name": "Example Secret", 
      "refresh_at": null, 
      "status": "pending", 
      "type_of": "oauth2", 
      "updated_at": "2021-07-14T19:33:25.628Z", 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    }, 
    "meta": { 
      "test_exchange": { 
        "access_token": "FpIkBn3zxW0fH6EBC4MB", 
        "expires_in": 36000, 
        "token_type": "Bearer", 
      } 
    } 
  } 
}
```

## Een geheim opnieuw proberen {#retry}

Het opnieuw proberen van een geheim is het manueel teweegbrengen van de geheime uitwisseling. U kunt een geheim opnieuw proberen door zijn identiteitskaart in de weg van een verzoek van de PATCH te omvatten.

**API-indeling**

```http
PATCH /secrets/{SECRET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SECRET_ID}` | De id van het geheim dat u opnieuw wilt proberen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "token"
          },
          "meta": {
            "action": "retry"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Moet een `type_of` eigenschap die overeenkomt met die van het geheim dat wordt bijgewerkt (`token`, `simple-http`, of `oauth2`). |
| `meta` | Moet een `action` eigenschap met een waarde van `retry`. |
| `id` | De id van het geheim dat u opnieuw probeert. Dit moet overeenkomen met de id die is opgegeven in het aanvraagpad. |
| `type` | Het type bron dat wordt gebruikt. Moet worden ingesteld op `secrets`. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie retourneert de details van het geheim, waarbij de status is ingesteld op `pending`. Nadat de uitwisseling heeft voltooid, zal de status van het geheim bijwerken aan `succeeded` of `failed` afhankelijk van het resultaat.

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## Een geheim verwijderen {#delete}

U kunt een geheim schrappen door zijn identiteitskaart in de weg van een verzoek van de DELETE te omvatten. Dit is een vaste verwijdering met een onmiddellijk effect waarvoor geen bibliotheek opnieuw hoeft te worden gepubliceerd.

Deze bewerking verwijdert het geheim uit de omgeving waaraan het is gerelateerd en de onderliggende bron wordt verwijderd.

>[!WARNING]
>
>Als u om het even welke opgestelde regels hebt die een geschrapt geheim van verwijzingen voorzien, zullen die regels onmiddellijk ophouden te functioneren. Alle gegevenselementen die naar dit geheim verwijzen, moeten achteraf worden bijgewerkt of verwijderd.

**API-indeling**

```http
DELETE /secrets/{SECRET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SECRET_ID}` | De id van het geheim dat u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege antwoordinstantie om aan te geven dat het geheim is verwijderd uit het systeem.

## De notities voor een geheim weergeven {#notes}

Met de Reactor-API kunt u notities toevoegen aan bepaalde bronnen, waaronder geheimen. Notities zijn tekstuele annotaties die geen invloed hebben op het gedrag van de bron en kunnen worden gebruikt voor verschillende gebruiksgevallen.

>[!NOTE]
>
>Zie de [leidraad voor notitiepunten](./notes.md) voor meer informatie over het maken en bewerken van notities voor Reactor API-bronnen.

U kunt alle notities met betrekking tot een geheim ophalen door een GET-aanvraag in te dienen.

**API-indeling**

```http
GET /secrets/{SECRET_ID}/notes
```

| Parameter | Beschrijving |
| --- | --- |
| `{SECRET_ID}` | De id van het geheim waarvan u de notities wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met notities die bij het geheim horen.

```json
{
  "data": [
    {
      "id": "NTe666dbcc2f204218b6fde2fe60ab7043",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Doe",
        "author_email": "jdoe@example.com",
        "created_at": "2021-07-16T22:29:58.259Z",
        "text": "This is a secret note."
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1"
          },
          "data": {
            "id": "SE591d3b86910f4e6883f0e1c36e54bff1",
            "type": "secrets"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1",
        "self": "https://reactor.adobe.io/notes/NTe666dbcc2f204218b6fde2fe60ab7043"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Gerelateerde bronnen ophalen voor een geheim {#related}

De volgende vraag toont aan hoe te om de verwante middelen voor een geheim terug te winnen. Wanneer [een geheim opzoeken](#lookup), worden deze relaties vermeld in het `relationships` eigenschap.

Zie de [relatiehulplijn](../guides/relationships.md) voor meer informatie over relaties in de Reactor-API.

### Opzoeken naar een verwante omgeving voor een geheim {#environment}

U kunt de omgeving die een geheim gebruikt, opzoeken door eraan toe te voegen `/environment` naar het pad van een GET-aanvraag.

**API-indeling**

```http
GET /secrets/{SECRET_ID}/environment
```

| Parameter | Beschrijving |
| --- | --- |
| `{SECRET_ID}` | De id van het geheim waarvan u de omgeving wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwoord**

Een succesvolle reactie retourneert de details van de omgeving.

```json
{
  "data": {
    "id": "EN33e8d63ac647448da1f77ced5c3c8580",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2021-07-16T22:19:13.438Z",
      "library_path": "bc12f2b85d11/b9a3067414ff",
      "library_name": "launch-3b6c4eea15ae-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-3b6c4eea15ae-development.min.js",
          "minified": true,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.min.js"
          ],
          "license_path": "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
        },
        {
          "library_name": "launch-3b6c4eea15ae-development.js",
          "minified": false,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": null,
      "stage": "development",
      "updated_at": "2021-07-16T22:19:13.438Z",
      "status": "succeeded",
      "token": "3b6c4eea15ae"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/host",
          "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/relationships/host"
        },
        "data": {
          "id": "HT7d5cf665463e46a1968ada1ceb1b5ca7",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/property"
        },
        "data": {
          "id": "PRba81d3027db846b084212391aa5d2f1f",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRba81d3027db846b084212391aa5d2f1f",
      "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### De verwante eigenschap opzoeken voor een geheim {#property}

U kunt de eigenschap die eigenaar is van een geheim opzoeken door deze toe te voegen `/property` naar het pad van een GET-aanvraag.

**API-indeling**

```http
GET /secrets/{SECRET_ID}/property
```

| Parameter | Beschrijving |
| --- | --- |
| `{SECRET_ID}` | De id van het geheim waarvan u het bezit wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de eigenschap.

```json
{
  "data": {
    "id": "PR2d191feafef54c5da4ddb5ef647d4867",
    "type": "properties",
    "attributes": {
      "created_at": "2021-07-16T22:26:25.320Z",
      "enabled": true,
      "name": "Kessel Edge Example Property",
      "updated_at": "2021-07-16T22:26:25.320Z",
      "platform": "edge",
      "development": false,
      "token": "8efbe7023155"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/company"
        },
        "data": {
          "id": "COc26fb19f87d24cbe827a70ad2a672093",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/COc26fb19f87d24cbe827a70ad2a672093",
      "data_elements": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments",
      "extensions": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions",
      "rules": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules",
      "self": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "edit_property",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
