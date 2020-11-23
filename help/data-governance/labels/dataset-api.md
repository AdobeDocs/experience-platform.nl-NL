---
keywords: Experience Platform;home;popular topics;dataset api;manage data usage;data usage api
solution: Experience Platform
title: 'Gegevensgebruikslabels voor gegevenssets beheren met behulp van API''s '
topic: developer guide
description: Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API voor catalogusservice die metagegevens van gegevenssets beheert.
translation-type: tm+mt
source-git-commit: 4b5e116d221e6689f95c8da0c54ef3af6827adc1
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Gegevensgebruikslabels voor gegevenssets beheren met behulp van API&#39;s

Met [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) deze optie kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Het maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de [!DNL Catalog Service] API die metagegevens van gegevenssets beheert.

In dit document wordt beschreven hoe u labels voor gegevenssets en velden kunt beheren met de [!DNL Dataset Service API]code. Voor stappen op hoe te om de etiketten van het gegevensgebruik zelf te beheren die API vraag gebruiken, zie de gids [van het](../api/labels.md) etiketteneindpunt voor [!DNL Policy Service API].

## Aan de slag

Voordat u deze handleiding leest, volgt u de stappen in de sectie [Aan de](../../catalog/api/getting-started.md) slag in de handleiding voor ontwikkelaars van catalogi om de vereiste gegevens te verzamelen voor het oproepen van [!DNL Platform] API&#39;s.

Om vraag aan de eindpunten te maken die in dit document worden geschetst, moet u de unieke `id` waarde voor een specifieke dataset hebben. Als u deze waarde niet hebt, raadpleegt u de handleiding bij het [weergeven van catalogusobjecten](../../catalog/api/list-objects.md) om de id&#39;s van uw bestaande gegevenssets te vinden.

## De etiketten van de raadpleging voor een dataset {#look-up}

U kunt de etiketten van het gegevensgebruik opzoeken die op een bestaande dataset zijn toegepast door een verzoek van de GET aan [!DNL Dataset Service] API te richten.

**API-indeling**

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
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvoor u etiketten creeert. |

**Verzoek**

Het volgende verzoek van de PUT werkt de bestaande etiketten voor een dataset, evenals een specifiek gebied binnen die dataset bij. De velden in de payload zijn gelijk aan de velden die vereist zijn voor een POST-aanvraag.

>[!IMPORTANT]
>
>Een geldige `If-Match` kopbal moet worden verstrekt wanneer het maken van PUT verzoeken aan het `/datasets/{DATASET_ID}/labels` eindpunt. Zie de [bijlage sectie](#if-match) voor meer informatie over het gebruiken van de vereiste kopbal.

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
| `optionalLabels` | Een lijst van om het even welke individuele gebieden binnen de dataset die u etiketten aan wilt toevoegen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de kenmerken [!DNL Experience Data Model] (XDM) van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li>id</code>: De URI $id</code> -waarde van het schema dat aan het veld is gekoppeld.</li><li>contentType</code>: Het inhoudstype en het versienummer van het schema. Dit zou de vorm van één van de geldige kopballen <a href="../../xdm/api/getting-started.md#accept">van de</a> Acceptie voor een XDM raadplegingsverzoek moeten hebben.</li><li>schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

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

U kunt de labels verwijderen die op een gegevensset zijn toegepast door een DELETE-aanvraag in te dienen bij de [!DNL Dataset Service] API.

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
>Een geldige `If-Match` kopbal moet worden verstrekt wanneer het doen van DELETE verzoeken aan het `/datasets/{DATASET_ID}/labels` eindpunt. Zie de [bijlage sectie](#if-match) voor meer informatie over het gebruiken van de vereiste kopbal.

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

Een geslaagde HTTP-respons status 200 (OK) die aangeeft dat de labels zijn verwijderd. U kunt de bestaande etiketten [voor de dataset in een afzonderlijke vraag](#look-up) omhoog kijken om dit te bevestigen.

## Volgende stappen

Door dit document te lezen hebt u geleerd hoe u labels voor gegevensgebruik voor gegevenssets en velden kunt beheren met behulp van de [!DNL Dataset Service] API.

Zodra u de etiketten van het gegevensgebruik op dataset en gebied-niveau hebt toegevoegd, kunt u beginnen gegevens in te nemen [!DNL Experience Platform]. Voor meer informatie begint u met het lezen van de [gegevensinvoerdocumentatie](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie het overzicht [van beleidsregels voor](../policies/overview.md)gegevensgebruik voor meer informatie.

Voor meer informatie bij het beheren van datasets in [!DNL Experience Platform], zie het [datasetoverzicht](../../catalog/datasets/overview.md).

## Aanhangsel {#appendix}

De volgende sectie bevat extra informatie over het werken met etiketten gebruikend de Dienst API van de Dataset.

### [!DNL If-Match] header {#if-match}

Wanneer het maken van API vraag die de bestaande etiketten van een dataset (PUT en DELETE) bijwerken, moet een `If-Match` kopbal die op de huidige versie van de dataset-etiket entiteit in de Dienst van de Dataset wijst worden omvat. Om gegevensbotsingen te verhinderen, zal de dienst slechts de datasetentiteit bijwerken als het inbegrepen `If-Match` koord de recentste versiemarkering aanpast die door het systeem voor die dataset wordt geproduceerd.

>[!NOTE]
>
>Als er momenteel geen labels voor de betrokken gegevensset bestaan, kunnen nieuwe labels alleen worden toegevoegd via een verzoek om POST, waarvoor geen `If-Match` koptekst vereist is. Zodra de etiketten aan een dataset zijn toegevoegd, wordt een `etag` waarde toegewezen die kan worden gebruikt om de etiketten in een recentere tijd bij te werken of te verwijderen.

Om de meest recente versie van de dataset-etiket entiteit terug te winnen, doe een [GET verzoek](#look-up) aan het `/datasets/{DATASET_ID}/labels` eindpunt. De huidige waarde wordt geretourneerd in de reactie onder een `etag` koptekst. Wanneer het bijwerken van bestaande datasetetiketten, moeten de beste praktijken eerst een raadplegingsverzoek voor de dataset uitvoeren om zijn recentste `etag` waarde te halen alvorens die waarde in de `If-Match` kopbal van uw verdere PUT of DELETE verzoek te gebruiken.