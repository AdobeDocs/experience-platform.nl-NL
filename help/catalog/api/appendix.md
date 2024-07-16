---
keywords: Experience Platform;home;populaire onderwerpen;Catalogusservice;Catalogus api;appendix
solution: Experience Platform
title: Bijlage Catalog Service API Guide
description: Dit document bevat aanvullende informatie die u helpt bij het werken met de Catalog-API in Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# [!DNL Catalog Service] API-hulplijnbijlage

Dit document bevat aanvullende informatie die u helpt bij het werken met de [!DNL Catalog] -API.

## Verwante objecten weergeven {#view-interrelated-objects}

Sommige [!DNL Catalog] -objecten kunnen met andere [!DNL Catalog] -objecten verweven zijn. Alle velden die vooraf worden ingesteld door `@` in antwoordladingen verwijzen naar gerelateerde objecten. De waarden voor deze velden hebben de vorm van een URI, die kan worden gebruikt in een afzonderlijke aanvraag voor een GET om de gerelateerde objecten op te halen die ze vertegenwoordigen.

De voorbeelddataset die in het document op [ is teruggekeerd die omhoog een specifieke dataset ](look-up-object.md) kijkt bevat a `files` gebied met de volgende waarde van URI: `"@/datasetFiles?datasetId={DATASET_ID}"`. De inhoud van het veld `files` kan worden weergegeven door deze URI te gebruiken als het pad voor een nieuwe GET-aanvraag.

**API formaat**

```http
GET {OBJECT_URI}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_URI}` | De URI die wordt verschaft door het veld voor onderling verwante objecten (exclusief het symbool `@` ). |

**Verzoek**

In het volgende verzoek wordt gebruikgemaakt van de URI die in de eigenschap `files` van de voorbeeldgegevensset is opgegeven, om een lijst met de bijbehorende bestanden van de gegevensset op te halen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

Bij het bijwerken van een object kunt u het beste eerst een API-aanroep uitvoeren om het object dat moet worden bijgewerkt, weer te geven (GET). Bevatten binnen de reactie (en elke aanroep waarbij de reactie één object bevat) is een `E-Tag` -header die de versie van het object bevat. Als u de objectversie toevoegt als een aanvraagheader met de naam `If-Match` in de aanroepen van de update (PUT of PATCH), wordt de update alleen succesvol uitgevoerd als de versie hetzelfde is. Zo voorkomt u gegevensconflict.

Als de versies niet overeenkomen (het object is gewijzigd door een ander proces sinds u het hebt opgehaald), ontvangt u HTTP-status 412 (Voorwaarde mislukt) om aan te geven dat toegang tot de doelbron is geweigerd.

### Pragma

Het kan voorkomen dat u een object wilt valideren zonder de informatie op te slaan. Als u de header `Pragma` met de waarde `validate-only` gebruikt, kunt u POST- of PUT-aanvragen alleen verzenden voor validatiedoeleinden, zodat wijzigingen in de gegevens niet worden voortgezet.

## Gegevenscompressie

Compaction is een [!DNL Experience Platform] -service die gegevens uit kleine bestanden samenvoegt in grotere bestanden zonder gegevens te wijzigen. Om prestatieredenen is het soms nuttig om een set kleine bestanden te combineren in grotere bestanden, zodat u sneller toegang hebt tot gegevens wanneer u hierom wordt gevraagd.

Wanneer de bestanden in een geneste batch zijn gecomprimeerd, wordt het bijbehorende [!DNL Catalog] -object bijgewerkt voor controledoeleinden.
