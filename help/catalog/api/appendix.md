---
keywords: Experience Platform;home;populaire onderwerpen;Catalogusservice;Catalogus api;appendix
solution: Experience Platform
title: Bijlage Catalog Service API-handleiding
topic: developer guide
description: Dit document bevat aanvullende informatie die u helpt bij het werken met de Catalog-API in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---


# [!DNL Catalog Service] API-hulplijnbijlage

Dit document bevat aanvullende informatie die u helpt bij het werken met de [!DNL Catalog]-API.

## Verwante objecten weergeven {#view-interrelated-objects}

Sommige [!DNL Catalog]-objecten kunnen met andere [!DNL Catalog]-objecten worden verweven. Alle velden die worden voorafgegaan door `@` in antwoordladingen geven gerelateerde objecten aan. De waarden voor deze velden hebben de vorm van een URI, die kan worden gebruikt in een afzonderlijke aanvraag voor een GET om de gerelateerde objecten op te halen die ze vertegenwoordigen.

De voorbeelddataset die in het document op [wordt teruggekeerd die een specifieke dataset](look-up-object.md) opzoeken bevat een `files` gebied met de volgende waarde van URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. De inhoud van het veld `files` kan worden weergegeven door deze URI te gebruiken als het pad voor een nieuwe GET-aanvraag.

**API-indeling**

```http
GET {OBJECT_URI}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_URI}` | De URI die wordt verschaft door het veld voor onderling verwante objecten (behalve het symbool `@`). |

**Verzoek**

Het volgende verzoek gebruikt URI verstrekte het bezit `files` van de voorbeelddataset om een lijst van de bijbehorende dossiers van de dataset terug te winnen.

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

Als deze verzoeken wijzigingen of toevoegingen aan [!DNL Catalog] zijn en om het even welke veranderingen ontbreken, zullen alle veranderingen terugkeren.

**API-indeling**

```http
POST /
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe dataset, dan leidt tot verwante meningen voor die dataset. Dit voorbeeld toont het gebruik van malplaatjetaal aan toegangswaarden die in vorige vraag voor gebruik in verdere vraag zijn teruggekeerd.

Als u bijvoorbeeld wilt verwijzen naar een waarde die is geretourneerd uit een vorige subaanvraag, kunt u een verwijzing maken in de indeling: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (waarbij `{REQUEST_ID}` de door de gebruiker opgegeven id voor de subaanvraag is, zoals hieronder wordt getoond). U kunt naar elk kenmerk verwijzen dat beschikbaar is in de hoofdtekst van het reactieobject van een vorige subaanvraag door deze sjablonen te gebruiken.

>[!NOTE]
>
>Wanneer een uitgevoerde sub-request slechts de verwijzing naar een voorwerp (zoals het gebrek voor de meeste POST en PUT verzoeken in Catalog API) terugkeert, wordt deze verwijzing aliased aan de waarde `id` en kan als `<<{OBJECT_ID}.id>>` worden gebruikt.

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
| `resource` | Het middelweg met betrekking tot de wortel van [!DNL Catalog] API. Het protocol en domein moeten geen deel uitmaken van deze waarde en moeten worden voorafgegaan door &quot;/&quot;. <br/><br/> Wanneer het gebruiken van PATCH of DELETE als sub-request  `method`, omvat objecten identiteitskaart in de middelweg. Om niet met gebruiker-geleverde `id` te worden verward, gebruikt de middelweg identiteitskaart van [!DNL Catalog] voorwerp zelf (bijvoorbeeld, `resource: "/dataSets/1234567890"`). |
| `method` | De naam van de methode (GET, PUT, POST, PATCH of DELETE) met betrekking tot de actie die in het verzoek wordt uitgevoerd. |
| `body` | Het JSON-document dat normaal gesproken zou worden doorgegeven als de payload in een POST-, PUT- of PATCH-aanvraag. Deze eigenschap is niet vereist voor GET- of DELETE-aanvragen. |

**Antwoord**

Een succesvolle reactie keert een serie van voorwerpen terug die `id` bevatten die u aan elk verzoek, de de statuscode van HTTP voor het individuele verzoek, en de reactie `body` toewees. Aangezien de drie voorbeeldverzoeken allemaal waren om nieuwe objecten te maken, is `body` van elk object een array die alleen de id van het nieuwe object bevat, zoals de standaard met de meest succesvolle POST-reacties in [!DNL Catalog].

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

Bij het bijwerken van een object kunt u het beste eerst een API-aanroep uitvoeren om het object dat moet worden bijgewerkt, weer te geven (GET). Bevatten binnen de reactie (en elke aanroep waarbij de reactie één object bevat) is een `E-Tag`-koptekst die de versie van het object bevat. Als u de objectversie toevoegt als een aanvraagkoptekst met de naam `If-Match` in de aanroepen van de update (PUT of PATCH), wordt de update alleen succesvol als de versie hetzelfde is, waardoor een botsing met gegevens wordt voorkomen.

Als de versies niet overeenkomen (het object is gewijzigd door een ander proces sinds u het hebt opgehaald), ontvangt u HTTP-status 412 (Voorwaarde mislukt) om aan te geven dat toegang tot de doelbron is geweigerd.

### Pragma

Soms wilt u een object valideren zonder de informatie op te slaan. Met de koptekst `Pragma` met de waarde `validate-only` kunt u POST- of PUT-aanvragen alleen verzenden voor validatiedoeleinden, zodat wijzigingen in de gegevens niet worden voortgezet.

## Gegevenscompressie

Compactie is een [!DNL Experience Platform] service die gegevens uit kleine bestanden samenvoegt in grotere bestanden zonder gegevens te wijzigen. Om prestatieredenen is het soms nuttig om een set kleine bestanden te combineren in grotere bestanden, zodat u sneller toegang hebt tot gegevens wanneer u hierom wordt gevraagd.

Wanneer de bestanden in een ingesloten batch zijn gecomprimeerd, wordt het bijbehorende [!DNL Catalog]-object bijgewerkt voor controledoeleinden.