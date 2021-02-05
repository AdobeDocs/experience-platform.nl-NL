---
keywords: Experience Platform;home;populaire onderwerpen;dataset api;beheer gegevensgebruik;gegevensgebruik api
solution: Experience Platform
title: 'Labels voor gegevensgebruik voor gegevenssets beheren met API''s '
topic: developer guide
description: Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API voor catalogusservice die metagegevens van gegevenssets beheert.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# Gegevensgebruikslabels voor gegevenssets beheren met behulp van API&#39;s

Met [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Het maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API [!DNL Catalog Service] die metagegevens van gegevenssets beheert.

Dit document behandelt hoe te om etiketten voor datasets en gebieden te beheren gebruikend [!DNL Dataset Service API]. Voor stappen op hoe te om de etiketten van het gegevensgebruik zelf te beheren gebruikend API vraag, zie [etiketeindgids](../api/labels.md) voor [!DNL Policy Service API].

## Aan de slag

Alvorens u deze gids leest, volg de stappen in [begonnen sectie](../../catalog/api/getting-started.md) in de de ontwikkelaarsgids van de Catalogus worden geschetst om de vereiste geloofsbrieven te verzamelen om vraag aan [!DNL Platform] APIs te maken die.

Om vraag aan de eindpunten te maken die in dit document worden geschetst, moet u de unieke `id` waarde voor een specifieke dataset hebben. Als u deze waarde niet hebt, zie de gids op [het vermelden van de voorwerpen van de Catalogus](../../catalog/api/list-objects.md) om identiteitskaarts van uw bestaande datasets te vinden.

## Labels opzoeken voor een gegevensset {#look-up}

U kunt de etiketten van het gegevensgebruik opzoeken die op een bestaande dataset zijn toegepast door een verzoek van de GET aan [!DNL Dataset Service] API te richten.

**API-indeling**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset de waarvan etiketten u omhoog wilt kijken. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de etiketten van het gegevensgebruik terug die op de dataset zijn toegepast.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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

U kunt een reeks etiketten voor een dataset tot stand brengen door hen in de nuttige lading van een POST of een verzoek van de PUT aan [!DNL Dataset Service] API te verstrekken. Als u een van deze methoden gebruikt, worden bestaande labels overschreven en vervangen door de labels in de payload.

**API-indeling**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id`-waarde van de gegevensset waarvoor u labels maakt. |

**Verzoek**

Het volgende verzoek van de PUT werkt de bestaande etiketten voor een dataset, evenals een specifiek gebied binnen die dataset bij. De velden in de payload zijn gelijk aan de velden die vereist zijn voor een POST-aanvraag.

>[!IMPORTANT]
>
>Een geldige `If-Match` kopbal moet worden verstrekt wanneer het indienen van PUT verzoeken aan het `/datasets/{DATASET_ID}/labels` eindpunt. Zie [appendix section](#if-match) voor meer informatie over het gebruiken van de vereiste kopbal.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
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
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die u aan de dataset wilt toevoegen. |
| `optionalLabels` | Een lijst van om het even welke individuele gebieden binnen de dataset die u etiketten aan wilt toevoegen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de [!DNL Experience Data Model] (XDM) kenmerken van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li>id</code>: De URI $id</code>-waarde van het schema dat aan het veld is gekoppeld.</li><li>contentType</code>: Het inhoudstype en het versienummer van het schema. Dit zou de vorm van één van geldige <a href="../../xdm/api/getting-started.md#accept">moeten aannemen kopballen</a> voor een XDM raadplegingsverzoek.</li><li>schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

**Antwoord**

Een succesvolle reactie keert de etiketten terug die aan de dataset zijn toegevoegd.

```json
{
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
```

## Labels uit een gegevensset verwijderen {#remove}

U kunt de etiketten verwijderen die op een dataset worden toegepast door een verzoek van DELETE aan [!DNL Dataset Service] API te doen.

**API-indeling**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvan etiketten u wilt verwijderen. |

**Verzoek**

Het volgende verzoek verwijdert de etiketten voor de dataset die in de weg wordt gespecificeerd.

>[!IMPORTANT]
>
>Een geldige `If-Match` kopbal moet worden verstrekt wanneer het doen van DELETE verzoeken aan het `/datasets/{DATASET_ID}/labels` eindpunt. Zie [appendix section](#if-match) voor meer informatie over het gebruiken van de vereiste kopbal.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**Antwoord**

Een geslaagde HTTP-respons status 200 (OK) die aangeeft dat de labels zijn verwijderd. U kunt [opzoeken bestaande labels](#look-up) voor de dataset in een afzonderlijke vraag om dit te bevestigen.

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u gegevensgebruikslabels voor gegevenssets en velden kunt beheren met de API [!DNL Dataset Service].

Zodra u de etiketten van het gegevensgebruik op dataset en gebied-niveau hebt toegevoegd, kunt u beginnen om gegevens in [!DNL Experience Platform] in te nemen. Als u meer wilt weten, begint u met het lezen van de [documentatie voor gegevensinvoer](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Voor meer informatie, zie [beleidsoverzicht van het gegevensgebruik](../policies/overview.md).

Voor meer informatie over het beheren van datasets in [!DNL Experience Platform], zie [datasetoverzicht](../../catalog/datasets/overview.md).

## Bijlage {#appendix}

De volgende sectie bevat extra informatie over het werken met etiketten gebruikend de Dienst API van de Dataset.

### [!DNL If-Match] header  {#if-match}

Bij het maken van API vraag die de bestaande etiketten van een dataset (PUT en DELETE) bijwerken, moet een `If-Match` kopbal die op de huidige versie van de dataset-etiket entiteit in de Dienst van de Dataset wijst worden omvat. Om gegevensbotsingen te verhinderen, zal de dienst slechts de datasetentiteit bijwerken als inbegrepen `If-Match` koord de recentste versiemarkering aanpast die door het systeem voor die dataset wordt geproduceerd.

>[!NOTE]
>
>Als er momenteel geen labels voor de betrokken gegevensset bestaan, kunnen nieuwe labels alleen worden toegevoegd via een verzoek om POST, waarvoor geen `If-Match`-header vereist is. Zodra de etiketten aan een dataset zijn toegevoegd, wordt een `etag` waarde toegewezen die kan worden gebruikt om de etiketten op een recentere tijd bij te werken of te verwijderen.

Om de meest recente versie van de dataset-etiket entiteit terug te winnen, maak [verzoek ](#look-up) aan het `/datasets/{DATASET_ID}/labels` eindpunt. De huidige waarde wordt geretourneerd in de reactie onder een koptekst `etag`. Wanneer het bijwerken van bestaande datasetetiketten, moeten de beste praktijken eerst een raadplegingsverzoek voor de dataset uitvoeren om zijn recentste `etag` waarde te halen alvorens die waarde in `If-Match` kopbal van uw verdere PUT of DELETE verzoek te gebruiken.