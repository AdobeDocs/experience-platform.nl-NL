---
description: Deze pagina verklaart hoe te om het /sample-profiles API eindpunt van Destination SDK te gebruiken om steekproefprofielen te produceren die op een bronschema worden gebaseerd. U kunt deze voorbeeldprofielen gebruiken om de op een bestand gebaseerde doelconfiguratie te testen.
title: Voorbeeldprofielen genereren op basis van een bronschema
source-git-commit: fa092e4d1828d9ecd5bc98e3f225fa377f38065f
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---


# Voorbeeldprofielen genereren op basis van een bronschema

## Overzicht {#overview}

De eerste stap bij het testen van uw op een bestand gebaseerde bestemming is het gebruik van de `/sample-profiles` eindpunt om een steekproefprofiel te produceren dat op uw bestaand bronschema wordt gebaseerd.

Voorbeeldprofielen zijn bedoeld om u te helpen de JSON-structuur van een profiel te begrijpen. Bovendien geven ze u een backbone die u kunt aanpassen met uw eigen profielgegevens voor verdere doeltests.

## Aan de slag {#getting-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Vereisten {#prerequisites}

Voordat u de `/sample-profiles` aan, zorg ervoor u aan de volgende voorwaarden voldoet:

* U hebt een bestaande op dossier-gebaseerde bestemming die door de Destination SDK wordt gecreeerd en u kunt het in uw zien [doelcatalogus](../ui/destinations-workspace.md).
* U hebt minstens één activeringsstroom voor uw bestemming in de gebruikersinterface van het Experience Platform gemaakt. De `/sample-profiles` het eindpunt leidt tot de profielen die op het bronschema worden gebaseerd dat u in uw activeringsstroom bepaalde. Zie de [activeringszelfstudie](../ui/activate-batch-profile-destinations.md) voor informatie over het maken van een activeringsstroom.
* Als u de API-aanvraag met succes wilt uitvoeren, hebt u de id van de doelinstantie nodig die overeenkomt met de doelinstantie die u wilt testen. Krijg bestemmingsidentiteitskaart die u in de API vraag, van URL zou moeten gebruiken, wanneer het doorbladeren van een verbinding met uw bestemming in Platform UI.

   ![UI-afbeelding die laat zien hoe u de id van de doelinstantie opgehaald kunt krijgen via de URL.](assets/get-destination-instance-id.png)

## Voorbeeldprofielen genereren voor doeltesten {#generate-sample-profiles}

U kunt steekproefprofielen produceren die op uw bronschema door een verzoek van de GET aan `/sample-profiles` eindpunt met bestemmingsidentiteitskaart van de bestemmingsinstantie van de bestemming die u wilt testen.

**API-indeling**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Parameters query | Beschrijving |
| -------- | ----------- |
| `destinationInstanceId` | De id van de doelinstantie waarvoor u voorbeeldprofielen genereert. Zie de [voorwaarden](#prerequisites) voor meer informatie over het verkrijgen van deze id. |
| `count` | *Optioneel*. Het aantal voorbeeldprofielen dat u wilt genereren. De parameter kan waarden gebruiken tussen `1 - 1000`. Als deze eigenschap niet is gedefinieerd, genereert de API één voorbeeldprofiel. |

**Verzoek**

Het volgende verzoek produceert een steekproefprofiel dat op het bronschema wordt gebaseerd dat in de bestemmingsinstantie met het overeenkomstige wordt bepaald `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count=2' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met het gespecificeerde aantal steekproefprofielen, met segmentlidmaatschap, identiteiten, en profielattributen terug die aan het bronXDM schema beantwoorden.

>[!NOTE]
>
> De reactie keert slechts segmentlidmaatschap, identiteiten, en profielattributen terug die in de bestemmingsinstantie worden gebruikt. Zelfs als uw bronschema andere gebieden heeft, worden deze genegeerd.

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

![Afbeelding die de toewijzing van de UI aan de velden vanuit de API-reactie weergeeft.](assets/sample-api-response-mapping.png)

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segmentMembership` | Een object map dat het segmentlidmaatschap van de persoon beschrijft. Voor meer informatie over `segmentMembership`, lezen [Details segmentlidmaatschap](../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Een tijdstempel van de laatste keer dat dit profiel voor het segment kwalificeerde. |
| `status` | Geeft aan of het segmentlidmaatschap is gerealiseerd als onderdeel van de huidige aanvraag. De volgende waarden worden geaccepteerd: <ul><li>`existing`: Het profiel maakte al deel uit van het segment voorafgaand aan de aanvraag en blijft bij het lidmaatschap.</li><li>`realized`: Het profiel voert het segment in als onderdeel van de huidige aanvraag.</li><li>`exited`: Het profiel verlaat het segment als deel van het huidige verzoek.</li></ul> |
| `identityMap` | A map-type field that describes the various identity values for an individual, together with their associated namespaces. Voor meer informatie over `identityMap`, zie [basis van schemacompositie](../../xdm/schema/composition.md#identityMap). |

{style=&quot;table-layout:auto&quot;}

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u voorbeeldprofielen kunt genereren op basis van het bronschema dat u hebt geconfigureerd in uw bestemming [activeringsstroom](../ui/activate-batch-profile-destinations.md).

U kunt deze profielen nu aanpassen of ze gebruiken zoals ze door de API worden geretourneerd. [test uw op dossier-gebaseerde bestemmingsconfiguratie](file-based-destination-testing-api.md).