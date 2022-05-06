---
keywords: Experience Platform;home;populaire onderwerpen;Catalogusservice;Catalogus api;appendix
solution: Experience Platform
title: Bijlage Catalog Service API-handleiding
topic-legacy: developer guide
description: Dit document bevat aanvullende informatie die u helpt bij het werken met de Catalog-API in Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# [!DNL Catalog Service] API-hulplijnbijlage

Dit document bevat aanvullende informatie om u te helpen met de [!DNL Catalog] API.

## Verwante objecten weergeven {#view-interrelated-objects}

Sommige [!DNL Catalog] objecten kunnen met andere [!DNL Catalog] objecten. Alle velden die vooraf zijn ingesteld door `@` in reactie op ladingen staan verwante objecten voor. De waarden voor deze velden hebben de vorm van een URI, die kan worden gebruikt in een afzonderlijke aanvraag voor een GET om de gerelateerde objecten op te halen die ze vertegenwoordigen.

De voorbeelddataset die in het document op is teruggekeerd [het zoeken van een specifieke dataset](look-up-object.md) bevat een `files` veld met de volgende URI-waarde: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. De inhoud van de `files` U kunt dit veld weergeven door deze URI te gebruiken als het pad voor een nieuwe GET-aanvraag.

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
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
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

## Maak veelvoudige verzoeken in één enkele vraag

Het worteleindpunt van [!DNL Catalog] API staat voor veelvoudige verzoeken toe om binnen één enkele vraag worden gemaakt. De aanvraaglading bevat een serie van voorwerpen die wat normaal individuele verzoeken vertegenwoordigen, die dan in orde worden uitgevoerd.

Als deze verzoeken wijzigingen of toevoegingen zijn aan [!DNL Catalog] en een van de wijzigingen mislukt, worden alle wijzigingen ongedaan gemaakt.

**API-indeling**

```http
POST /
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe dataset, dan leidt tot verwante meningen voor die dataset. Dit voorbeeld toont het gebruik van malplaatjetaal aan toegangswaarden die in vorige vraag voor gebruik in verdere vraag zijn teruggekeerd.

Als u bijvoorbeeld wilt verwijzen naar een waarde die is geretourneerd uit een vorige subaanvraag, kunt u een verwijzing maken in de indeling: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` waarbij `{REQUEST_ID}` is de door de gebruiker opgegeven id voor het subverzoek, zoals hieronder wordt getoond). U kunt naar elk kenmerk verwijzen dat beschikbaar is in de hoofdtekst van het reactieobject van een vorige subaanvraag door deze sjablonen te gebruiken.

>[!NOTE]
>
>Wanneer een uitgevoerde sub-request alleen de verwijzing naar een voorwerp terugkeert (zoals het gebrek voor de meeste POST en PUT verzoeken in Catalog API), wordt deze verwijzing aliased aan de waarde `id` en kan worden gebruikt zoals  `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `resource` | Het bronnenpad ten opzichte van de hoofdmap van het [!DNL Catalog] API. Het protocol en domein moeten geen deel uitmaken van deze waarde en moeten worden voorafgegaan door &quot;/&quot;. <br/><br/> Bij het gebruik van PATCH of DELETE als de subaanvraag `method`, neemt u de object-id op in het bronnenpad. Niet verward te worden met de door de gebruiker opgegeven `id`, gebruikt het bronpad de id van het [!DNL Catalog] object zelf (bijvoorbeeld `resource: "/dataSets/1234567890"`). |
| `method` | De naam van de methode (GET, PUT, POST, PATCH of DELETE) met betrekking tot de actie die in het verzoek wordt uitgevoerd. |
| `body` | Het JSON-document dat normaal gesproken zou worden doorgegeven als de payload in een POST-, PUT- of PATCH-aanvraag. Deze eigenschap is niet vereist voor GET- of DELETE-aanvragen. |

**Antwoord**

Een succesvol antwoord retourneert een array met objecten die de `id` die u aan elke aanvraag hebt toegewezen, de HTTP-statuscode voor de individuele aanvraag en de reactie `body`. Aangezien de drie voorbeeldaanvragen allemaal bedoeld waren om nieuwe objecten te maken, worden `body` van elk object is een array die alleen de id bevat van het nieuwe object, zoals de standaard is met de meest succesvolle POST-reacties in [!DNL Catalog].

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

Bij het bijwerken van een object kunt u het beste eerst een API-aanroep uitvoeren om het object dat moet worden bijgewerkt, weer te geven (GET). Bevat binnen de reactie (en elke aanroep waarbij de reactie één object bevat) is een `E-Tag` koptekst met de versie van het object. De objectversie toevoegen als een aanvraagheader met de naam `If-Match` in uw update (PUT of PATCH) zal de vraag in de update slechts succesvol resulteren als de versie nog het zelfde is, die helpen gegevensbotsing verhinderen.

Als de versies niet overeenkomen (het object is gewijzigd door een ander proces sinds u het hebt opgehaald), ontvangt u HTTP-status 412 (Voorwaarde mislukt) om aan te geven dat toegang tot de doelbron is geweigerd.

### Pragma

Soms wilt u een object valideren zonder de informatie op te slaan. Met de `Pragma` header met een waarde van `validate-only` Hiermee kunt u POST- of PUT-aanvragen alleen verzenden voor validatiedoeleinden, zodat wijzigingen in de gegevens niet worden voortgezet.

## Gegevenscompressie

Compressie is een [!DNL Experience Platform] service die gegevens uit kleine bestanden samenvoegt in grotere bestanden zonder gegevens te wijzigen. Om prestatieredenen is het soms nuttig om een set kleine bestanden te combineren in grotere bestanden, zodat u sneller toegang hebt tot gegevens wanneer u hierom wordt gevraagd.

Wanneer de bestanden in een geneste batch zijn gecomprimeerd, wordt de bijbehorende [!DNL Catalog] object wordt bijgewerkt voor controledoeleinden.
