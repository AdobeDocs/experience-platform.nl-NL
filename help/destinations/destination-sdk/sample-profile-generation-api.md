---
description: Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/sample-profiles` om voorbeeldprofielen te genereren voor gebruik in bestemmingstests.
title: Voorbeeld van API-bewerkingen voor het genereren van profielen
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Voorbeeld van API-bewerkingen voor het genereren van profielen {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API-eindpunt**:  `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/sample-profiles`.

Met dit API-eindpunt kunt u voorbeeldprofielen genereren voor gebruik:
* Bij het testen van een sjabloon voor berichttransformatie. Lees meer in [Creeer en test een malplaatje van de berichttransformatie](./create-template.md).
* Wanneer het testen als uw bestemming correct wordt gevormd. Lees meer in [Test uw bestemmingsconfiguratie](./test-destination.md).

U kunt steekproefprofielen produceren die op of het Adobe XDM bronschema, of het doelschema worden gebaseerd door uw bestemming wordt gesteund. Om het verschil tussen Adobe XDM bronschema en doelschema te begrijpen, lees [formaat van het Bericht](./message-format.md) artikel.

## Aan de slag met API-bewerkingen voor het genereren van voorbeeldprofielen {#get-started}

Alvorens verder te gaan, te herzien [begonnen gids](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmingsauteur en vereiste kopballen te verkrijgen.

## Voorbeeldprofielen genereren op basis van het bronschema {#generate-sample-profiles-source-schema}

U kunt steekproefprofielen produceren die op het bronschema worden gebaseerd door een verzoek van de GET tot het `authoring/sample-profiles/` eindpunt te richten en identiteitskaart van een bestemmingsinstantie te verstrekken die u op de bestemmingsconfiguratie baseerde die u wilt testen creeerde.

>[!TIP]
>
>* Krijg bestemmingsidentiteitskaart die u hier van URL zou moeten gebruiken wanneer het doorbladeren van een verbinding met uw bestemming.
   >![UI-afbeelding voor het ophalen van bestemmings-ID](./assets/get-destination-instance-id.png)


**API-indeling**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De id van de doelinstantie op basis waarvan u voorbeeldprofielen genereert. |
| `{COUNT}` | *Optioneel*. Het aantal voorbeeldprofielen dat u genereert. De parameter kan waarden tussen `1 - 1000` nemen. <br> Als de telparameter niet wordt gespecificeerd, dan wordt het standaardaantal geproduceerde profielen bepaald door de  `maxUsersPerRequest` waarde in de configuratie [ van de ](./destination-server-api.md#create)bestemmingsserver. Als deze eigenschap niet is gedefinieerd, genereert Adobe één voorbeeldprofiel. |


**Verzoek**

Het volgende verzoek produceert steekproefprofielen, die door `{DESTINATION_INSTANCE_ID}` en `{COUNT}` vraagparameters worden gevormd.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met het gespecificeerde aantal steekproefprofielen, met segmentlidmaatschap, identiteiten, en profielattributen terug die aan het bronXDM schema beantwoorden.

>[!TIP]
>
> De reactie keert slechts segmentlidmaatschap, identiteiten, en profielattributen terug die in de bestemmingsinstantie worden gebruikt. Zelfs als uw bronschema andere gebieden heeft, worden deze genegeerd.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segmentMembership` | Een object map dat het segmentlidmaatschap van de persoon beschrijft. Lees [Details segmentlidmaatschap](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html) voor meer informatie over `segmentMembership`. |
| `lastQualificationTime` | Een tijdstempel van de laatste keer dat dit profiel voor het segment kwalificeerde. |
| `xdm:status` | Geeft aan of het segmentlidmaatschap is gerealiseerd als onderdeel van de huidige aanvraag. De volgende waarden worden geaccepteerd: <ul><li>`existing`: Het profiel maakte al deel uit van het segment voorafgaand aan de aanvraag en blijft bij het lidmaatschap.</li><li>`realized`: Het profiel voert het segment in als onderdeel van de huidige aanvraag.</li><li>`exited`: Het profiel verlaat het segment als deel van het huidige verzoek.</li></ul> |
| `identityMap` | A map-type field that describes the various identity values for an individual, together with their associated namespaces. Voor meer informatie over `identityMap`, lees [Basis van schemacompositie](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |


## Voorbeeldprofielen genereren op basis van het doelschema {#generate-sample-profiles-target-schema}

U kunt steekproefprofielen produceren die op het doelschema worden gebaseerd die een verzoek van de GET tot het `authoring/sample-profiles/` eindpunt richten en bestemmingsidentiteitskaart van de bestemmingsconfiguratie verstrekken die op wordt gebaseerd die u uw malplaatje creeert.

>[!TIP]
>
>* De bestemmingsidentiteitskaart die u hier zou moeten gebruiken is `instanceId` die aan een bestemmingsconfiguratie beantwoordt, die gebruikend het `/destinations` eindpunt wordt gecreeerd. Raadpleeg de [API referentie voor doelconfiguratie](./destination-configuration-api.md#retrieve-list).


**API-indeling**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_ID}` | De id van de doelconfiguratie waarop u voorbeeldprofielen genereert. |
| `{COUNT}` | *Optioneel*. Het aantal voorbeeldprofielen dat u genereert. De parameter kan waarden tussen `1 - 1000` nemen. <br> Als de telparameter niet wordt gespecificeerd, dan wordt het standaardaantal geproduceerde profielen bepaald door de  `maxUsersPerRequest` waarde in de configuratie [ van de ](./destination-server-api.md#create)bestemmingsserver. Als deze eigenschap niet is gedefinieerd, genereert Adobe één voorbeeldprofiel. |

**Verzoek**

Het volgende verzoek produceert steekproefprofielen, die door `{DESTINATION_ID}` en `{COUNT}` vraagparameters worden gevormd.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met het gespecificeerde aantal steekproefprofielen, met segmentlidmaatschap, identiteiten, en profielattributen terug die aan het doelXDM schema beantwoorden.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API-foutafhandeling {#api-error-handling}

De eindpunten van SDK API van de bestemming volgen de algemene API van het Experience Platform foutenmeldingsbeginselen. Raadpleeg [API-statuscodes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) en [headerfouten aanvragen](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in de handleiding voor het oplossen van Platforms.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om steekproefprofielen te produceren die moeten worden gebruikt wanneer [het testen van een malplaatje van de berichttransformatie ](./create-template.md) of wanneer [het testen als uw bestemming correct](./test-destination.md) wordt gevormd.