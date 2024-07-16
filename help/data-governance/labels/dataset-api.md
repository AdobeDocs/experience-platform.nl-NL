---
keywords: Experience Platform;home;populaire onderwerpen;dataset api;beheer gegevensgebruik;gegevensgebruik api
solution: Experience Platform
title: Labels voor gegevensgebruik voor gegevenssets beheren met API's
description: Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API van de Catalogusservice die metagegevens van gegevenssets beheert.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 8db484e4a65516058d701ca972fcbcb6b73abb31
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 0%

---

# Gegevensgebruikslabels voor gegevenssets beheren met behulp van API&#39;s

Met [[!DNL Dataset Service API] ](https://www.adobe.io/experience-platform-apis/references/dataset-service/) kunt u gebruikslabels voor gegevenssets toepassen en bewerken. De klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API van [!DNL Catalog Service] die metagegevens van gegevenssets beheert.

>[!IMPORTANT]
>
>Het toepassen van labels op gegevenssetniveau wordt alleen ondersteund voor gevallen waarin gegevens worden beheerd. Als u probeert om toegangsbeleid voor de gegevens tot stand te brengen, moet u [ etiketten op het schema ](../../xdm/tutorials/labels.md) toepassen dat de dataset op gebaseerd is. Zie het overzicht op [ op attributen-gebaseerde toegangsbeheer ](../../access-control/abac/overview.md) voor meer informatie.

In dit document wordt beschreven hoe u labels voor gegevenssets en velden kunt beheren met de [!DNL Dataset Service API] . Voor stappen op hoe te om de etiketten van het gegevensgebruik zelf te beheren die API vraag gebruiken, zie de [ gids van het etiketteneindpunt ](../api/labels.md) voor [!DNL Policy Service API].

## Aan de slag

Alvorens u deze gids leest, volg de stappen die in [ worden geschetst begonnen sectie ](../../catalog/api/getting-started.md) in de de ontwikkelaarsgids van de Catalogus worden geschetst om de vereiste geloofsbrieven te verzamelen om vraag aan [!DNL Platform] APIs te maken.

Als u aanroepen wilt uitvoeren naar de eindpunten die in dit document worden beschreven, moet u de unieke `id` -waarde voor een specifieke gegevensset hebben. Als u deze waarde niet hebt, zie de gids op [ het van lijstCatalogusvoorwerpen ](../../catalog/api/list-objects.md) om IDs van uw bestaande datasets te vinden.

## De etiketten van de raadpleging voor een dataset {#look-up}

U kunt de labels voor gegevensgebruik opzoeken die zijn toegepast op een bestaande gegevensset door een GET-aanvraag in te dienen op de [!DNL Dataset Service] API.

**API formaat**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvan etiketten u omhoog wilt kijken. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de etiketten van het gegevensgebruik terug die op de dataset zijn toegepast.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die op de dataset zijn toegepast. |
| `optionalLabels` | Een lijst van individuele gebieden binnen de dataset die de etiketten van het gegevensgebruik hebben op hen worden toegepast. |

## Labels toepassen op een gegevensset {#apply}

U kunt een reeks etiketten voor een volledige dataset toepassen door hen in de nuttige lading van een POST of een verzoek van de PUT op [!DNL Dataset Service] API te verstrekken. Het verzoeklichaam is het zelfde voor beide vraag. U kunt geen labels toevoegen aan afzonderlijke gegevenssetvelden.

**API formaat**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` -waarde van de gegevensset waarvoor u labels maakt. |

**Verzoek**

In het onderstaande voorbeeld wordt de gehele gegevensset bijgewerkt met een label `C1` . De velden in de payload zijn gelijk aan de velden die vereist zijn voor een PUT-aanvraag.

Wanneer het maken van API vraag die de bestaande etiketten van een dataset (PUT) bijwerkt, moet een `If-Match` kopbal die op de huidige versie van de dataset-etiket entiteit in de Dienst van de Dataset wijst worden omvat. Om gegevensbotsingen te verhinderen, zal de dienst slechts de datasetentiteit bijwerken als inbegrepen `If-Match` koord de recentste versiemarkering aanpast die door het systeem voor die dataset wordt geproduceerd.

>[!NOTE]
>
>Als er momenteel labels voor de desbetreffende gegevensset bestaan, kunnen nieuwe labels alleen worden toegevoegd via een verzoek om PUT, waarvoor een `If-Match` header is vereist. Zodra de etiketten aan een dataset zijn toegevoegd, wordt de meest recente `etag` waarde vereist om de etiketten in een recentere tijd <br> bij te werken of te verwijderen alvorens de methode van de PUT uit te voeren, moet u een verzoek van de GET op de datasetetiketten uitvoeren. Zorg ervoor dat u alleen de specifieke velden bijwerkt die zijn bedoeld voor wijziging in de aanvraag, en laat de rest ongewijzigd. Bovendien, zorg ervoor dat de vraag van de PUT de zelfde ouderentiteiten zoals de vraag van de GET handhaaft. Elke discrepantie zou resulteren in een fout voor de klant.

Om de meest recente versie van de dataset-etiket entiteit terug te winnen, doe a [ verzoek van de GET ](#look-up) aan het `/datasets/{DATASET_ID}/labels` eindpunt. De huidige waarde wordt geretourneerd in de reactie onder een `etag` -header. Wanneer het bijwerken van bestaande datasetetiketten, moeten de beste praktijken eerst een raadplegingsverzoek voor de dataset uitvoeren om zijn recentste `etag` waarde te halen alvorens die waarde in `If-Match` kopbal van uw verdere verzoek van de PUT te gebruiken.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| Eigenschap | Beschrijving |
| --- | --- |
| `entityId` | Dit identificeert de specifieke gegevenssetentiteit die moet worden bijgewerkt. |
| `entityId.namespace` | Dit wordt gebruikt om botsingen van identiteitskaart te vermijden. De waarde `namespace` is `AEP` . |
| `entityId.id` | De id van de bron die wordt bijgewerkt. Dit verwijst naar `datasetId`. |
| `entityId.type` | Het type van de bron die wordt bijgewerkt. Dit zal altijd `dataset` zijn. |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die u aan de volledige dataset wilt toevoegen. |
| `parents` | De `parents` serie bevat een lijst van `entityId` s die deze dataset etiketten van zal erven. Datasets kunnen labels overnemen van schema&#39;s en/of gegevenssets. |

**Reactie**

Een succesvolle reactie keert de bijgewerkte reeks etiketten voor de dataset terug.

>[!IMPORTANT]
>
>De eigenschap `optionalLabels` is vervangen voor gebruik met POST-aanvragen. Het is niet meer mogelijk om gegevensetiketten aan datasetgebieden toe te voegen. Een POST-bewerking genereert een fout als er een `optionalLabel` -waarde aanwezig is. U kunt labels echter uit afzonderlijke velden verwijderen met behulp van een PUT-aanvraag en de eigenschap `optionalLabels` . Voor meer informatie zie de sectie op [ verwijderend etiketten uit een dataset ](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## Labels uit een gegevensset verwijderen {#remove}

U kunt eerder toegepaste veldlabels verwijderen door de bestaande `optionalLabels` -waarde(n) bij te werken met een subset van de bestaande veldlabels of door een lege lijst om deze volledig te verwijderen. Voer een verzoek van de PUT in op de [!DNL Dataset Service] API om eerder toegepaste labels bij te werken of te verwijderen.

**API formaat**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` -waarde van de gegevensset waarvoor u labels maakt. |

**Verzoek**

De hieronder dataset waarop de verrichting van de PUT wordt toegepast had C1 optionalLabel op eigenschappen/person/properties/address gebied en C1, C2 optionalLabels op /properties/person/properties/name/properties/fullName gebied. Na de putoptie heeft het eerste veld geen label (label C1 verwijderd) en het tweede veld heeft alleen het label C1 (label C2 verwijderd)

In het onderstaande voorbeeldscenario wordt een aanvraag voor een PUT gebruikt om labels te verwijderen die aan afzonderlijke velden zijn toegevoegd. Voordat de aanvraag werd uitgevoerd, waren in het veld `fullName` de labels `C1` en `C2` toegepast en in het veld `address` was al een label `C1` toegepast. De aanvraag PUT negeert bestaande labels `C1, C2` uit het `fullName` veld met een `C1` -label met behulp van de `optionalLabels.labels` -parameter. De aanvraag negeert ook het label `C1` uit het veld `address` met een lege set veldlabels.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| Parameter | Beschrijving |
| --- | --- |
| `entityId` | Dit identificeert de specifieke gegevenssetentiteit die moet worden bijgewerkt. `entityId` moet de volgende drie waarden omvatten:<br/><br/>`namespace`: Dit wordt gebruikt om botsingen van identiteitskaart te vermijden. De waarde `namespace` is `AEP` .<br/>`id`: De id van de bron die wordt bijgewerkt. Dit verwijst naar `datasetId`.<br/>`type`: Het type van de bron die wordt bijgewerkt. Dit zal altijd `dataset` zijn. |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die u aan de volledige dataset wilt toevoegen. |
| `parents` | De `parents` serie bevat een lijst van `entityId` s die deze dataset etiketten van zal erven. Datasets kunnen labels overnemen van schema&#39;s en/of gegevenssets. |
| `optionalLabels` | Deze parameter wordt gebruikt om etiketten te verwijderen die eerder op een datasetgebied worden toegepast. Een lijst van om het even welke individuele gebieden binnen de dataset die u de etiketten wilt verwijderen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de [!DNL Experience Data Model] (XDM)-kenmerken van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li><code> id</code>: De URI <code>$id</code> De waarde van het schema dat aan het veld is gekoppeld.</li><li><code> contentType</code>: Het inhoudstype en het versienummer van het schema. Dit zou de vorm van één van de geldige <a href="../../xdm/api/getting-started.md#accept"> moeten aannemen kopballen </a> voor een XDM raadplegingsverzoek.</li><li><code> schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: deze waarde moet een subset van de bestaande toegepaste veldlabels bevatten of leeg zijn om alle bestaande veldlabels te verwijderen. De methoden PUT of POST retourneren nu een fout als het `optionalLabels` -veld nieuwe of gewijzigde labels heeft. |

**Reactie**

Een succesvolle reactie keert de bijgewerkte reeks etiketten voor de dataset terug.

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u labels voor gegevensgebruik voor gegevenssets en velden kunt beheren met de API [!DNL Dataset Service] . U kunt [ beleid van het gegevensgebruik ](../policies/overview.md) en [ toegangsbeheerbeleid ](../../access-control/abac/ui/policies.md) nu bepalen dat op de etiketten wordt gebaseerd u hebt toegepast.

Voor meer informatie bij het beheren van datasets in [!DNL Experience Platform], zie het [ overzicht van datasets ](../../catalog/datasets/overview.md).
