---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handboek voor ontwikkelaars van catalogusservice
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# [!DNL Catalog Service] bijlage ontwikkelaarsgids

Dit document bevat aanvullende informatie die u helpt bij het werken met de [!DNL Catalog] API.

## Verwante objecten weergeven {#view-interrelated-objects}

Sommige [!DNL Catalog] objecten kunnen met andere [!DNL Catalog] objecten verweven zijn. Alle velden die vooraf worden ingesteld door `@` in antwoordladingen, verwijzen naar verwante objecten. De waarden voor deze velden hebben de vorm van een URI, die kan worden gebruikt in een afzonderlijke aanvraag voor een GET om de gerelateerde objecten op te halen die ze vertegenwoordigen.

De voorbeelddataset die in het document is geretourneerd bij het [opzoeken van een specifieke dataset](look-up-object.md) , bevat een `files` veld met de volgende URI-waarde: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. De inhoud van het `files` veld kan worden weergegeven door deze URI te gebruiken als het pad voor een nieuwe aanvraag voor een GET.

**API-indeling**

```http
GET {OBJECT_URI}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_URI}` | De URI die wordt verschaft door het veld met onderling verwante objecten (exclusief het `@` symbool). |

**Verzoek**

Het volgende verzoek gebruikt URI verstrekte het `files` bezit van de voorbeelddataset om een lijst van de bijbehorende dossiers van de dataset terug te winnen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Maak veelvoudige verzoeken in één enkele vraag

Het worteleindpunt van [!DNL Catalog] API staat voor veelvoudige verzoeken toe om binnen één enkele vraag worden gemaakt. De aanvraaglading bevat een serie van voorwerpen die wat normaal individuele verzoeken vertegenwoordigen, die dan in orde worden uitgevoerd.

Als deze verzoeken wijzigingen of toevoegingen zijn aan [!DNL Catalog] en een van de wijzigingen mislukt, worden alle wijzigingen ongedaan gemaakt.

**API-indeling**

```http
POST /
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe dataset, dan leidt tot verwante meningen voor die dataset. Dit voorbeeld toont het gebruik van malplaatjetaal aan toegangswaarden die in vorige vraag voor gebruik in verdere vraag zijn teruggekeerd.

Als u bijvoorbeeld wilt verwijzen naar een waarde die is geretourneerd uit een vorige subaanvraag, kunt u een verwijzing maken in de indeling: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (waarbij `{REQUEST_ID}` de door de gebruiker opgegeven id voor het subverzoek is, zoals hieronder wordt getoond). U kunt naar elk kenmerk verwijzen dat beschikbaar is in de hoofdtekst van het reactieobject van een vorige subaanvraag door deze sjablonen te gebruiken.

>[!NOTE]
>
>Wanneer een uitgevoerde sub-request slechts de verwijzing naar een voorwerp (zoals het gebrek voor de meeste POST en PUT verzoeken in Catalog API) terugkeert, is deze verwijzing aliased aan de waarde `id` en kan als `<<{OBJECT_ID}.id>>`. worden gebruikt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | Door de gebruiker opgegeven id die aan het reactieobject is gekoppeld, zodat u verzoeken aan reacties kunt koppelen. [!DNL Catalog] slaat deze waarde niet op en retourneert deze gewoon in de reactie voor referentiedoeleinden. |
| `resource` | Het bronnenpad ten opzichte van de hoofdmap van de [!DNL Catalog] API. Het protocol en domein moeten geen deel uitmaken van deze waarde en moeten worden voorafgegaan door &quot;/&quot;. <br/><br/> Wanneer het gebruiken van PATCH of DELETE als sub-request `method`, omvat objecten identiteitskaart in de middelweg. Om niet met user-provided te worden verward `id`, gebruikt de middelweg identiteitskaart van het [!DNL Catalog] voorwerp zelf (bijvoorbeeld, `resource: "/dataSets/1234567890"`). |
| `method` | De naam van de methode (GET, PUT, POST, PATCH of DELETE) met betrekking tot de actie die in het verzoek wordt uitgevoerd. |
| `body` | Het JSON-document dat normaal gesproken zou worden doorgegeven als de payload in een POST-, PUT- of PATCH-aanvraag. Deze eigenschap is niet vereist voor GET- of DELETE-aanvragen. |

**Antwoord**

Een geslaagde reactie retourneert een array met objecten met de objecten `id` die u aan elke aanvraag hebt toegewezen, de HTTP-statuscode voor de individuele aanvraag en de reactie `body`. Aangezien de drie voorbeeldaanvragen allemaal waren om nieuwe objecten te maken, is de array `body` van elk object een array die alleen de id van het nieuwe object bevat, net als de standaard met de meest geslaagde reacties van POSTEN in [!DNL Catalog].

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

Wees voorzichtig bij het inspecteren van de reactie op een meervoudige aanvraag, aangezien u de code van elke individuele subaanvraag moet verifiëren en niet alleen op de HTTP-statuscode voor de aanvraag van de bovenliggende POST moet vertrouwen.  Het is mogelijk voor één enkel sub-verzoek om 404 (zoals een verzoek van de GET op een ongeldige middel) terug te keren terwijl het algemene verzoek 200 terugkeert.

## Aanvullende aanvraagheaders

[!DNL Catalog] biedt verschillende headerconventies om u te helpen de integriteit van uw gegevens tijdens updates te behouden.

### If-Match

Het is een goede gewoonte om objectversioning te gebruiken om het type gegevensbeschadiging te voorkomen dat optreedt wanneer een object door meerdere gebruikers bijna tegelijk wordt opgeslagen.

Bij het bijwerken van een object kunt u het beste eerst een API-aanroep uitvoeren om het object dat moet worden bijgewerkt, weer te geven (GET). Bevatten binnen de reactie (en elke aanroep waarbij de reactie één object bevat) is een `E-Tag` koptekst die de versie van het object bevat. Als u de objectversie toevoegt als een aanvraagkoptekst die `If-Match` in de aanroepen van de update (PUT of PATCH) is genoemd, wordt de update alleen succesvol uitgevoerd als de versie hetzelfde is. Hierdoor wordt botsing met gegevens voorkomen.

Als de versies niet overeenkomen (het object is gewijzigd door een ander proces sinds u het hebt opgehaald), ontvangt u HTTP-status 412 (Voorwaarde mislukt) om aan te geven dat toegang tot de doelbron is geweigerd.

### Pragma

Soms wilt u een object valideren zonder de informatie op te slaan. Als u de `Pragma` koptekst met de waarde &#39; `validate-only` allows&#39; gebruikt, kunt u alleen POST- of PUT-aanvragen voor validatiedoeleinden verzenden, zodat wijzigingen in de gegevens niet worden voortgezet.

## Gegevenscompressie

Compaction is een [!DNL Experience Platform] service waarbij gegevens uit kleine bestanden worden samengevoegd in grotere bestanden zonder dat gegevens worden gewijzigd. Om prestatieredenen is het soms nuttig om een set kleine bestanden te combineren in grotere bestanden, zodat u sneller toegang hebt tot gegevens wanneer u hierom wordt gevraagd.

Wanneer de bestanden in een ingesloten batch zijn gecomprimeerd, wordt het bijbehorende [!DNL Catalog] object bijgewerkt voor controledoeleinden.