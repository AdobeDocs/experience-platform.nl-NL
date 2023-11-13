---
keywords: Experience Platform;home;populaire onderwerpen;Catalogusservice;Catalogus api;appendix
solution: Experience Platform
title: Bijlage Catalog Service API Guide
description: Dit document bevat aanvullende informatie die u helpt bij het werken met de Catalog-API in Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# [!DNL Catalog Service] API-hulplijnbijlage

Dit document bevat aanvullende informatie om u te helpen met de [!DNL Catalog] API.

## Verwante objecten weergeven {#view-interrelated-objects}

Sommige [!DNL Catalog] objecten kunnen met andere [!DNL Catalog] objecten. Alle velden die vooraf zijn ingesteld door `@` in reactie op ladingen staan verwante objecten voor. De waarden voor deze velden hebben de vorm van een URI, die kan worden gebruikt in een afzonderlijke aanvraag voor een GET om de gerelateerde objecten op te halen die ze vertegenwoordigen.

De voorbeelddataset die in het document op is teruggekeerd [het zoeken van een specifieke dataset](look-up-object.md) bevat een `files` veld met de volgende URI-waarde: `"@/datasetFiles?datasetId={DATASET_ID}"`. De inhoud van de `files` U kunt dit veld weergeven door deze URI te gebruiken als het pad voor een nieuwe GET-aanvraag.

**API-indeling**

```http
GET {OBJECT_URI}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_URI}` | De URI die wordt verschaft door het veld met onderling verwante objecten (exclusief de `@` symbool). |

**Verzoek**

In het volgende verzoek wordt de URI gebruikt die in de voorbeelddataset is opgegeven `files` bezit om een lijst van de bijbehorende dossiers van de dataset terug te winnen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met verwante objecten. In dit voorbeeld wordt een lijst met gegevenssetbestanden geretourneerd.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Aanvullende aanvraagheaders

[!DNL Catalog] biedt verschillende headerconventies om u te helpen de integriteit van uw gegevens tijdens updates te behouden.

### If-Match

Het is een goede gewoonte om objectversioning te gebruiken om het type gegevensbeschadiging te voorkomen dat optreedt wanneer een object door meerdere gebruikers bijna tegelijk wordt opgeslagen.

Bij het bijwerken van een object kunt u het beste eerst een API-aanroep uitvoeren om het object dat moet worden bijgewerkt, weer te geven (GET). Bevat binnen de reactie (en elke aanroep waarbij de reactie één object bevat) is een `E-Tag` koptekst met de versie van het object. De objectversie toevoegen als een aanvraagheader met de naam `If-Match` in uw update (PUT of PATCH) zal de vraag in de update slechts succesvol resulteren als de versie nog het zelfde is, die helpen gegevensbotsing verhinderen.

Als de versies niet overeenkomen (het object is gewijzigd door een ander proces sinds u het hebt opgehaald), ontvangt u HTTP-status 412 (Voorwaarde mislukt) om aan te geven dat toegang tot de doelbron is geweigerd.

### Pragma

Het kan voorkomen dat u een object wilt valideren zonder de informatie op te slaan. Met de `Pragma` header met een waarde van `validate-only` Hiermee kunt u POST- of PUT-aanvragen alleen verzenden voor validatiedoeleinden, zodat wijzigingen in de gegevens niet worden voortgezet.

## Gegevenscompressie

Compressie is een [!DNL Experience Platform] service die gegevens uit kleine bestanden samenvoegt in grotere bestanden zonder gegevens te wijzigen. Om prestatieredenen is het soms nuttig om een set kleine bestanden te combineren in grotere bestanden, zodat u sneller toegang hebt tot gegevens wanneer u hierom wordt gevraagd.

Wanneer de bestanden in een geneste batch zijn gecomprimeerd, wordt de bijbehorende [!DNL Catalog] -object wordt bijgewerkt voor controledoeleinden.
