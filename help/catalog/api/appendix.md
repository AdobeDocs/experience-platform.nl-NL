---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handboek voor ontwikkelaars van catalogusservice
topic: developer guide
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# Handboek voor ontwikkelaars van catalogusservice

Dit document bevat aanvullende informatie die u helpt bij het werken met de Catalog-API.

## Verwante objecten weergeven {#view-interrelated-objects}

Sommige catalogusobjecten kunnen met andere catalogusobjecten worden verweven. Alle velden die vooraf worden ingesteld door `@` in antwoordladingen, verwijzen naar verwante objecten. De waarden voor deze gebieden nemen de vorm van URI aan, die in een afzonderlijke GET verzoek kan worden gebruikt om de verwante voorwerpen terug te winnen zij vertegenwoordigen.

De voorbeelddataset die in het document is geretourneerd bij het [opzoeken van een specifieke dataset](look-up-object.md) , bevat een `files` veld met de volgende URI-waarde: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. De inhoud van het `files` veld kan worden weergegeven door deze URI te gebruiken als het pad voor een nieuwe GET-aanvraag.

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

Het worteleindpunt van Catalog API staat voor veelvoudige verzoeken toe om binnen één enkele vraag worden gemaakt. De aanvraaglading bevat een serie van voorwerpen die wat normaal individuele verzoeken vertegenwoordigen, die dan in orde worden uitgevoerd.

Als deze aanvragen wijzigingen of toevoegingen aan de catalogus zijn en een van de wijzigingen mislukt, worden alle wijzigingen ongedaan gemaakt.

**API-indeling**

```http
POST /
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe dataset, dan leidt tot verwante meningen voor die dataset. Dit voorbeeld toont het gebruik van malplaatjetaal aan toegangswaarden die in vorige vraag voor gebruik in verdere vraag zijn teruggekeerd.

Als u bijvoorbeeld wilt verwijzen naar een waarde die is geretourneerd uit een vorige subaanvraag, kunt u een verwijzing maken in de indeling: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (waarbij `{REQUEST_ID}` de door de gebruiker opgegeven id voor het subverzoek is, zoals hieronder wordt getoond). U kunt naar elk kenmerk verwijzen dat beschikbaar is in de hoofdtekst van het reactieobject van een vorige subaanvraag door deze sjablonen te gebruiken.

>[!NOTE] Wanneer een uitgevoerde sub-request alleen de verwijzing naar een object retourneert (zoals de standaardinstelling is voor de meeste POST- en PUT-aanvragen in de Catalogus-API), wordt deze verwijzing naar de waarde gealiased `id` en kan deze worden gebruikt als `<<{OBJECT_ID}.id>>`.

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
| `id` | Door de gebruiker opgegeven id die aan het reactieobject is gekoppeld, zodat u verzoeken aan reacties kunt koppelen. Deze waarde wordt niet in Catalog opgeslagen en in de reactie geretourneerd ter referentie. |
| `resource` | Het bronnenpad ten opzichte van de hoofdmap van de catalogus-API. Het protocol en domein moeten geen deel uitmaken van deze waarde en moeten worden voorafgegaan door &quot;/&quot;. <br/><br/> Wanneer u PATCH of DELETE gebruikt als de subaanvraag `method`, neemt u de object-id op in het bronnenpad. Om niet met user-provided te worden verward `id`, gebruikt de middelweg identiteitskaart van het voorwerp van de Catalogus zelf (bijvoorbeeld, `resource: "/dataSets/1234567890"`). |
| `method` | De naam van de methode (GET, PUT, POST, PATCH of DELETE) die betrekking heeft op de handeling die plaatsvindt in de aanvraag. |
| `body` | Het JSON-document dat normaal gesproken zou worden doorgegeven als de lading in een POST-, PUT- of PATCH-aanvraag. Deze eigenschap is niet vereist voor GET- of DELETE-aanvragen. |

**Antwoord**

Een geslaagde reactie retourneert een array met objecten met de objecten `id` die u aan elke aanvraag hebt toegewezen, de HTTP-statuscode voor de individuele aanvraag en de reactie `body`. Aangezien de drie voorbeeldaanvragen allemaal waren om nieuwe objecten te maken, is de array `body` van elk object een array die alleen de id van het nieuwe object bevat, net als de standaard met de meest succesvolle POST-reacties in Catalog.

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

Wees voorzichtig bij het inspecteren van de reactie op een meervoudige aanvraag, aangezien u de code van elke individuele subaanvraag moet verifiëren en niet alleen op de HTTP-statuscode voor de bovenliggende POST-aanvraag moet vertrouwen.  Het is mogelijk voor één enkel sub-verzoek om 404 (zoals een GET verzoek op een ongeldige middel) terug te keren terwijl het algemene verzoek 200 terugkeert.

## Aanvullende aanvraagheaders

Catalog biedt verschillende headerconventies om u te helpen de integriteit van uw gegevens tijdens updates te behouden.

### If-Match

Het is een goede gewoonte om objectversioning te gebruiken om het type gegevensbeschadiging te voorkomen dat optreedt wanneer een object door meerdere gebruikers bijna tegelijk wordt opgeslagen.

Bij het bijwerken van een object wordt het beste eerst een API-aanroep uitgevoerd om het object dat moet worden bijgewerkt, weer te geven. Bevatten binnen de reactie (en elke aanroep waarbij de reactie één object bevat) is een `E-Tag` koptekst die de versie van het object bevat. Als u de objectversie toevoegt als een aanvraagheader die `If-Match` in de aanroepen van de update (PUT of PATCH) wordt genoemd, wordt de update alleen succesvol uitgevoerd als de versie hetzelfde is. Zo voorkomt u gegevensconflict.

Als de versies niet overeenkomen (het object is gewijzigd door een ander proces sinds u het hebt opgehaald), ontvangt u HTTP-status 412 (Voorwaarde mislukt) om aan te geven dat toegang tot de doelbron is geweigerd.

### Pragma

Soms wilt u een object valideren zonder de informatie op te slaan. Als u de `Pragma` koptekst gebruikt met de waarde van `validate-only` , kunt u POST- of PUT-aanvragen alleen verzenden voor validatiedoeleinden, zodat wijzigingen in de gegevens niet worden voortgezet.

## Gegevenscompressie

Compaction is een service van het Experience Platform die gegevens uit kleine bestanden samenvoegt tot grotere bestanden zonder gegevens te wijzigen. Om prestatieredenen is het soms nuttig om een set kleine bestanden te combineren in grotere bestanden, zodat u sneller toegang hebt tot gegevens wanneer u hierom wordt gevraagd.

Wanneer de bestanden in een geneste batch zijn gecomprimeerd, wordt het bijbehorende Catalog-object bijgewerkt voor controledoeleinden.