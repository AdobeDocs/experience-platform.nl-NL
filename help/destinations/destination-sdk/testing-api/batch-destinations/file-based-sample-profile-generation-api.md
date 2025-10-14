---
description: Deze pagina verklaart hoe te om het /sample-profiles API eindpunt van Destination SDK te gebruiken om steekproefprofielen te produceren die op een bronschema worden gebaseerd. U kunt deze voorbeeldprofielen gebruiken om de op een bestand gebaseerde doelconfiguratie te testen.
title: Voorbeeldprofielen genereren op basis van een bronschema
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Voorbeeldprofielen genereren op basis van een bronschema

De eerste stap in het testen van uw op bestand gebaseerde bestemming is het `/sample-profiles` eindpunt te gebruiken om een steekproefprofiel te produceren dat op uw bestaand bronschema wordt gebaseerd.

Voorbeeldprofielen kunnen u helpen de JSON-structuur van een profiel te begrijpen. Bovendien geven ze u een standaardinstelling die u kunt aanpassen met uw eigen profielgegevens voor verdere doeltests.

## Aan de slag {#getting-started}

Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Vereisten {#prerequisites}

Voordat u het eindpunt `/sample-profiles` kunt gebruiken, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een bestaande op dossier-gebaseerde bestemming die door Destination SDK wordt gecreeerd en u kunt het in uw [&#x200B; doelcatalogus &#x200B;](../../../ui/destinations-workspace.md) zien.
* U hebt ten minste één activeringsstroom voor uw doel gemaakt in de gebruikersinterface van Experience Platform. Het `/sample-profiles` eindpunt leidt tot profielen die op het bronschema worden gebaseerd dat u in uw activeringsstroom bepaalde. Zie het [&#x200B; activeringsleerprogramma &#x200B;](../../../ui/activate-batch-profile-destinations.md) leren hoe te om een activeringsstroom tot stand te brengen.
* Als u de API-aanvraag met succes wilt uitvoeren, hebt u de id van de doelinstantie nodig die overeenkomt met de doelinstantie die u wilt testen. Krijg bestemmingsidentiteitskaart die u in de API vraag, van URL zou moeten gebruiken, wanneer het doorbladeren van een verbinding met uw bestemming in Experience Platform UI.

  ![&#x200B; beeld UI die hoe te om bestemmingsidentiteitskaart van URL te krijgen toont.](../../assets/testing-api/get-destination-instance-id.png)

## Voorbeeldprofielen genereren voor doeltesten {#generate-sample-profiles}

U kunt steekproefprofielen produceren die op uw bronschema worden gebaseerd door een verzoek van GET aan het `/sample-profiles` eindpunt met bestemmingsidentiteitskaart van de instantie van de bestemming te doen die u wilt testen.

**API formaat**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Query-parameters | Beschrijving |
| -------- | ----------- |
| `destinationInstanceId` | De id van de doelinstantie waarvoor u voorbeeldprofielen genereert. Zie de [&#x200B; eerste vereisten &#x200B;](#prerequisites) sectie voor details op hoe te om deze identiteitskaart te verkrijgen. |
| `count` | *Facultatief*. Het aantal voorbeeldprofielen dat u wilt genereren. De parameter kan waarden aannemen tussen `1 - 1000` . Als deze eigenschap niet is gedefinieerd, genereert de API één voorbeeldprofiel. |

**Verzoek**

Met de volgende aanvraag wordt een voorbeeldprofiel gegenereerd op basis van het bronschema dat in de doelinstantie met de bijbehorende `destinationInstanceId` is gedefinieerd.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met het gespecificeerde aantal steekproefprofielen, met publiekslidmaatschap, identiteiten, en profielattributen terug die aan het bronXDM schema beantwoorden.

>[!NOTE]
>
> De reactie retourneert alleen het publiekslidmaatschap, de identiteiten en de profielkenmerken die in de doelinstantie worden gebruikt. Zelfs als uw bronschema andere gebieden heeft, worden deze genegeerd.

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![&#x200B; Beeld dat de afbeelding van UI aan de gebieden van de API reactie toont.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segmentMembership` | A map object that describes the person&#39;s publiek membership. Voor meer informatie over `segmentMembership`, lees [&#x200B; de Details van het Lidmaatschap van de Publiek &#x200B;](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Een tijdstempel van de laatste keer dat dit profiel voor het segment kwalificeerde. |
| `status` | Een tekenreeksveld dat aangeeft of het publieklidmaatschap is gerealiseerd als onderdeel van de huidige aanvraag. De volgende waarden worden geaccepteerd: <ul><li>`realized`: Het profiel maakt deel uit van het segment.</li><li>`exited`: Het profiel sluit het publiek af als onderdeel van de huidige aanvraag.</li></ul> |
| `identityMap` | A map-type field that describes the various identity values for an individual, together with their associated namespaces. Voor meer informatie over `identityMap`, zie [&#x200B; basis van schemacompositie &#x200B;](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om steekproefprofielen te produceren die op het bronschema worden gebaseerd dat u in uw bestemmings [&#x200B; activeringsstroom &#x200B;](../../../ui/activate-batch-profile-destinations.md) vormde.

U kunt deze profielen nu aanpassen of hen gebruiken aangezien zij door API zijn teruggekeerd, om [&#x200B; uw op dossier-gebaseerde bestemmingsconfiguratie &#x200B;](file-based-destination-testing-api.md) te testen.
