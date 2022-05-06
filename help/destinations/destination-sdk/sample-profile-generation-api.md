---
description: Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/sample-profiles` om voorbeeldprofielen te genereren voor gebruik in bestemmingstests.
title: Voorbeeld van API-bewerkingen voor het genereren van profielen
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Voorbeeld van API-bewerkingen voor het genereren van profielen {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API-eindpunt**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/sample-profiles` API-eindpunt.

## Verschillende profieltypen genereren voor verschillende API&#39;s {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Gebruik dit API-eindpunt om voorbeeldprofielen te genereren voor twee afzonderlijke gebruiksgevallen. U kunt:
>* profielen genereren die moeten worden gebruikt wanneer [Een sjabloon voor berichttransformatie maken en testen](./create-template.md) - door *doel-id* als een queryparameter.
>* produceren profielen aan gebruik wanneer het maken van vraag aan [test als uw bestemming correct wordt gevormd](./test-destination.md) - door *doel-instantie-id* als een queryparameter.


U kunt steekproefprofielen produceren die op of het Adobe XDM bronschema (aan gebruik wanneer het testen van uw bestemming) worden gebaseerd, of het doelschema dat door uw bestemming (aan gebruik wanneer het ontwerpen van uw malplaatje) wordt gesteund. Om het verschil tussen Adobe XDM bronschema en doelschema te begrijpen, lees de overzichtssectie van het [Berichtindeling](./message-format.md) artikel.

De doeleinden waarvoor de voorbeeldprofielen kunnen worden gebruikt, zijn niet onderling verwisselbaar. Profielen die zijn gegenereerd op basis van de *doel-id* kan alleen worden gebruikt om sjablonen en profielen voor berichttransformatie te maken die zijn gegenereerd op basis van de *doel-instantie-id* kan alleen worden gebruikt om het eindpunt van uw bestemming te testen.

## Aan de slag met API-bewerkingen voor het genereren van voorbeeldprofielen {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Voorbeeldprofielen genereren op basis van het bronschema dat moet worden gebruikt voor het testen van uw bestemming {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Voeg de steekproefprofielen toe hier worden geproduceerd die aan de vraag van HTTP wanneer [doel testen](./test-destination.md).

U kunt steekproefprofielen produceren die op het bronschema worden gebaseerd door een verzoek van de GET aan `authoring/sample-profiles/` eindpunt en het verstrekken van identiteitskaart van een bestemmingsinstantie die u gebaseerd op de bestemmingsconfiguratie creeerde die u wilt testen.

Om identiteitskaart van een bestemmingsinstantie te krijgen, moet u een verbinding in het Experience Platform UI aan uw bestemming eerst tot stand brengen alvorens te proberen om uw bestemming te testen. Lees de [doelzelfstudie activeren](/help/destinations/ui/activation-overview.md) en zie de tip hieronder voor hoe u de id van de doelinstantie kunt ophalen voor gebruik voor deze API.

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
| `{COUNT}` | *Optioneel*. Het aantal voorbeeldprofielen dat u genereert. De parameter kan waarden gebruiken tussen `1 - 1000`. <br> Als de telparameter niet wordt gespecificeerd, dan wordt het standaardaantal geproduceerde profielen bepaald door `maxUsersPerRequest` in de [doelserverconfiguratie](./destination-server-api.md#create). Als deze eigenschap niet is gedefinieerd, genereert Adobe één voorbeeldprofiel. |

{style=&quot;table-layout:auto&quot;}


**Verzoek**

Met de volgende aanvraag worden voorbeeldprofielen gegenereerd, geconfigureerd door de `{DESTINATION_INSTANCE_ID}` en `{COUNT}` queryparameters.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
| `segmentMembership` | Een object map dat het segmentlidmaatschap van de persoon beschrijft. Voor meer informatie over `segmentMembership`, lezen [Details segmentlidmaatschap](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Een tijdstempel van de laatste keer dat dit profiel voor het segment kwalificeerde. |
| `xdm:status` | Geeft aan of het segmentlidmaatschap is gerealiseerd als onderdeel van de huidige aanvraag. De volgende waarden worden geaccepteerd: <ul><li>`existing`: Het profiel maakte al deel uit van het segment voorafgaand aan de aanvraag en blijft bij het lidmaatschap.</li><li>`realized`: Het profiel voert het segment in als onderdeel van de huidige aanvraag.</li><li>`exited`: Het profiel verlaat het segment als deel van het huidige verzoek.</li></ul> |
| `identityMap` | A map-type field that describes the various identity values for an individual, together with their associated namespaces. Voor meer informatie over `identityMap`, lezen [Basis van schemacompositie](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Voorbeeldprofielen genereren op basis van het doelschema dat moet worden gebruikt bij het maken van een sjabloon voor berichttransformatie {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Gebruik de voorbeeldprofielen die hier worden gegenereerd bij het maken van de sjabloon in het dialoogvenster [sjabloonstap renderen](./render-template-api.md#multiple-profiles-with-body).

U kunt voorbeeldprofielen genereren op basis van het doelschema. U kunt dan een GET-aanvraag indienen bij de `authoring/sample-profiles/` eindpunt en het verstrekken van bestemmingsidentiteitskaart van de bestemmingsconfiguratie die op wordt gebaseerd waarop u uw malplaatje creeert.

>[!TIP]
>
>* De doel-id die u hier moet gebruiken, is de `instanceId` die met een bestemmingsconfiguratie beantwoordt, die wordt gecreeerd gebruikend `/destinations` eindpunt. Zie de [API-naslaggids voor doelconfiguratie](./destination-configuration-api.md#retrieve-list).


**API-indeling**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_ID}` | De id van de doelconfiguratie waarop u voorbeeldprofielen genereert. |
| `{COUNT}` | *Optioneel*. Het aantal voorbeeldprofielen dat u genereert. De parameter kan waarden gebruiken tussen `1 - 1000`. <br> Als de telparameter niet wordt gespecificeerd, dan wordt het standaardaantal geproduceerde profielen bepaald door `maxUsersPerRequest` in de [doelserverconfiguratie](./destination-server-api.md#create). Als deze eigenschap niet is gedefinieerd, genereert Adobe één voorbeeldprofiel. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met de volgende aanvraag worden voorbeeldprofielen gegenereerd, geconfigureerd door de `{DESTINATION_ID}` en `{COUNT}` queryparameters.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Nadat u dit document hebt gelezen, kunt u nu voorbeeldprofielen genereren die u kunt gebruiken wanneer [het testen van een malplaatje van de berichttransformatie](./create-template.md) of wanneer [testen of uw doel correct is geconfigureerd](./test-destination.md).
