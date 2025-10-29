---
description: Leer hoe u de API voor bestemmingstests kunt gebruiken om voorbeeldprofielen voor uw streamingdoel te genereren. U kunt deze gebruiken voor doeltests.
title: Voorbeeldprofielen genereren op basis van een bronschema
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---


# Voorbeeldprofielen genereren op basis van een bronschema {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API eindpunt**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt van `/authoring/sample-profiles` .

## Verschillende profieltypen genereren voor verschillende API&#39;s {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Gebruik dit API-eindpunt om voorbeeldprofielen te genereren voor twee afzonderlijke gebruiksgevallen. U kunt:
>
>* produceren profielen om te gebruiken wanneer [&#x200B; creërend en het testen van een malplaatje van de berichttransformatie &#x200B;](create-template.md) - door *bestemmingsidentiteitskaart* als vraagparameter te gebruiken.
>* produceren profielen om te gebruiken wanneer het maken van vraag aan [&#x200B; test als uw bestemming correct &#x200B;](streaming-destination-testing-overview.md) wordt gevormd - door *identiteitskaart van de bestemmingsinstantie* als vraagparameter te gebruiken.

U kunt voorbeeldprofielen genereren op basis van het Adobe XDM-bronschema (om te gebruiken bij het testen van uw bestemming) of het doelschema dat door uw bestemming wordt ondersteund (om te gebruiken bij het maken van uw sjabloon). Om het verschil tussen Adobe XDM bronschema en doelschema te begrijpen, lees de overzichtssectie van het [&#x200B; formaat van het Bericht &#x200B;](../../functionality/destination-server/message-format.md) artikel.

De doeleinden waarvoor de voorbeeldprofielen kunnen worden gebruikt, zijn niet onderling verwisselbaar. De profielen die op *worden geproduceerd bestemmingsidentiteitskaart* kunnen slechts worden gebruikt om uw malplaatjes en de profielen van de berichttransformatie te amberen die op *worden geproduceerd identiteitskaart van de bestemmingsinstantie* kunnen slechts worden gebruikt om uw bestemmingspunten te testen.

## Aan de slag met API-bewerkingen voor het genereren van voorbeeldprofielen {#get-started}

Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Voorbeeldprofielen genereren op basis van het bronschema dat moet worden gebruikt voor het testen van uw bestemming {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Voeg de steekproefprofielen toe hier aan de vraag van HTTP worden geproduceerd wanneer [&#x200B; het testen van uw bestemming &#x200B;](streaming-destination-testing-overview.md).

U kunt steekproefprofielen produceren die op het bronschema worden gebaseerd door een verzoek van GET aan het `authoring/sample-profiles/` eindpunt te doen en identiteitskaart van een bestemmingsinstantie te verstrekken die u op de bestemmingsconfiguratie creeerde die u wilt testen.

Als u de id van een doelinstantie wilt ophalen, moet u eerst een verbinding maken in de gebruikersinterface van Experience Platform met uw doel voordat u probeert uw doel te testen. Lees het [&#x200B; activeer bestemmingsleerprogramma &#x200B;](../../../ui/activation-overview.md) en zie hieronder het uiteinde voor hoe te om identiteitskaart van de bestemmingsinstantie aan gebruik voor dit API te krijgen.

>[!IMPORTANT]
>
>* Als u deze API wilt gebruiken, moet u een bestaande verbinding met uw doel hebben in de gebruikersinterface van Experience Platform. Lees [&#x200B; verbind met bestemming &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) en [&#x200B; activeer profielen en publiek aan een bestemming &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html) voor meer informatie.
>* Na het vestigen van de verbinding aan uw bestemming, krijg identiteitskaart van de bestemmingsinstantie die u in API vraag aan dit eindpunt zou moeten gebruiken wanneer [&#x200B; doorbladert een verbinding met uw bestemming &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>
>![&#x200B; beeld UI hoe te om identiteitskaart van de bestemmingsinstantie &#x200B;](../../assets/testing-api/get-destination-instance-id.png) te krijgen

**API formaat**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De id van de doelinstantie waarop u voorbeeldprofielen genereert. |
| `{COUNT}` | *Facultatief*. Het aantal voorbeeldprofielen dat u genereert. De parameter kan waarden aannemen tussen `1 - 1000` . <br> Als de tellingsparameter niet wordt gespecificeerd, dan wordt het standaardaantal geproduceerde profielen bepaald door de `maxUsersPerRequest` waarde in de [&#x200B; configuratie van de bestemmingsserver &#x200B;](../../authoring-api/destination-server/create-destination-server.md). Als deze eigenschap niet is gedefinieerd, genereert Adobe één voorbeeldprofiel. |

{style="table-layout:auto"}


**Verzoek**

Met de volgende aanvraag worden voorbeeldprofielen gegenereerd, geconfigureerd door de parameters `{DESTINATION_INSTANCE_ID}` en `{COUNT}` query.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met het gespecificeerde aantal steekproefprofielen, met publiekslidmaatschap, identiteiten, en profielattributen terug die aan het bronXDM schema beantwoorden.

>[!TIP]
>
> De reactie retourneert alleen het publiekslidmaatschap, de identiteiten en de profielkenmerken die in de doelinstantie worden gebruikt. Zelfs als uw bronschema andere gebieden heeft, worden deze genegeerd.

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
| `segmentMembership` | A map object that describes the person&#39;s publiek membership. Voor meer informatie over `segmentMembership`, lees [&#x200B; de Details van het Lidmaatschap van de Publiek &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Een tijdstempel van de laatste keer dat dit profiel voor het segment kwalificeerde. |
| `xdm:status` | Een tekenreeksveld dat aangeeft of het publieklidmaatschap is gerealiseerd als onderdeel van de huidige aanvraag. De volgende waarden worden geaccepteerd: <ul><li>`realized`: Het profiel maakt deel uit van het segment.</li><li>`exited`: Het profiel sluit het publiek af als onderdeel van de huidige aanvraag.</li></ul> |
| `identityMap` | A map-type field that describes the various identity values for an individual, together with their associated namespaces. Voor meer informatie over `identityMap`, lees [&#x200B; Basis van schemacompositie &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#identityMap). |

{style="table-layout:auto"}

## Voorbeeldprofielen genereren op basis van het doelschema dat moet worden gebruikt bij het maken van een sjabloon voor berichttransformatie {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Gebruik de steekproefprofielen hier worden geproduceerd wanneer het ontwerpen van uw malplaatje, in [&#x200B; geven malplaatjestap &#x200B;](render-template-api.md#multiple-profiles-with-body) terug.

U kunt steekproefprofielen produceren die op het doelschema worden gebaseerd die een verzoek van GET aan het `authoring/sample-profiles/` eindpunt indienen en bestemmingsidentiteitskaart van de bestemmingsconfiguratie verstrekken die op wordt gebaseerd waarop u uw malplaatje creeert.

>[!TIP]
>
>* De doel-id die u hier moet gebruiken, is de `instanceId` die overeenkomt met een doelconfiguratie die is gemaakt met het `/destinations` -eindpunt. Verwijs naar [&#x200B; een bestemmingsconfiguratie &#x200B;](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) voor meer details terugwinnen.

**API formaat**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_ID}` | De id van de doelconfiguratie waarop u voorbeeldprofielen genereert. |
| `{COUNT}` | *Facultatief*. Het aantal voorbeeldprofielen dat u genereert. De parameter kan waarden aannemen tussen `1 - 1000` . <br> Als de tellingsparameter niet wordt gespecificeerd, dan wordt het standaardaantal geproduceerde profielen bepaald door de `maxUsersPerRequest` waarde in de [&#x200B; configuratie van de bestemmingsserver &#x200B;](../../authoring-api/destination-server/create-destination-server.md). Als deze eigenschap niet is gedefinieerd, genereert Adobe één voorbeeldprofiel. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag worden voorbeeldprofielen gegenereerd, geconfigureerd door de parameters `{DESTINATION_ID}` en `{COUNT}` query.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met het gespecificeerde aantal steekproefprofielen, met publiekslidmaatschap, identiteiten, en profielattributen terug die aan het doelXDM schema beantwoorden.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
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
                    "status": "realized"
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
                    "status": "realized"
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

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om steekproefprofielen te produceren die moeten worden gebruikt wanneer [&#x200B; het testen van een malplaatje van de berichttransformatie &#x200B;](create-template.md) of wanneer [&#x200B; het testen als uw bestemming correct &#x200B;](streaming-destination-testing-overview.md) wordt gevormd.
