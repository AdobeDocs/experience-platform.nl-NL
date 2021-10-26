---
keywords: Experience Platform;home;populaire onderwerpen;dataset api;beheer gegevensgebruik;gegevensgebruik api
solution: Experience Platform
title: 'Labels voor gegevensgebruik voor gegevenssets beheren met API''s '
topic-legacy: developer guide
description: Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API voor catalogusservice die metagegevens van gegevenssets beheert.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: ef711b1cbe0664f556e19ff6c64e9803d3cb1a21
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Gegevensgebruikslabels voor gegevenssets beheren met behulp van API&#39;s

De [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) staat u toe om gebruiksetiketten voor datasets toe te passen en uit te geven. Het maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de [!DNL Catalog Service] API die gegevenssetmetagegevens beheert.

In dit document wordt beschreven hoe u labels voor gegevenssets en velden kunt beheren met de [!DNL Dataset Service API]. Voor stappen over hoe te om de etiketten van het gegevensgebruik zelf te beheren die API vraag gebruiken, zie [eindhulplijn voor labels](../api/labels.md) voor de [!DNL Policy Service API].

## Aan de slag

Volg de stappen in het dialoogvenster [aan de slag, sectie](../../catalog/api/getting-started.md) in de de ontwikkelaarsgids van de Catalogus om de vereiste geloofsbrieven te verzamelen om vraag te maken aan [!DNL Platform] API&#39;s.

Als u aanroepen wilt uitvoeren naar de eindpunten die in dit document worden beschreven, moet u beschikken over de `id` waarde voor een specifieke gegevensset. Als u deze waarde niet hebt, raadpleegt u de handleiding [Catalogusobjecten weergeven](../../catalog/api/list-objects.md) om id&#39;s van uw bestaande gegevenssets te zoeken.

## De etiketten van de raadpleging voor een dataset {#look-up}

U kunt de etiketten van het gegevensgebruik opzoeken die op een bestaande dataset zijn toegepast door een verzoek van de GET tot aan [!DNL Dataset Service] API.

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

U kunt een reeks etiketten voor een dataset tot stand brengen door hen in de nuttige lading van een POST of een verzoek van de PUT aan te verstrekken [!DNL Dataset Service] API. Als u een van deze methoden gebruikt, worden bestaande labels overschreven en vervangen door de labels in de payload.

**API-indeling**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvoor u etiketten creeert. |

**Verzoek**

Het verzoek van de PUT van het voorbeeld hieronder werkt de bestaande etiketten voor een dataset, evenals een specifiek gebied binnen die dataset bij. De velden in de payload zijn gelijk aan de velden die vereist zijn voor een POST-aanvraag.

Wanneer het maken van API vraag die de bestaande etiketten van een dataset (PUT) bijwerkt, en `If-Match` kopbal die op de huidige versie van de dataset-etiket entiteit in de Dienst van de Dataset wijst moet worden omvat. Om gegevensbotsingen te verhinderen, zal de dienst slechts de datasetentiteit bijwerken als inbegrepen `If-Match` tekenreeks komt overeen met de laatste versietag die door het systeem voor die dataset is gegenereerd.

>[!NOTE]
>
>Als er momenteel geen labels voor de betrokken gegevensset bestaan, kunnen nieuwe labels alleen worden toegevoegd via een verzoek van de POST, waarvoor geen `If-Match` header. Nadat labels aan een gegevensset zijn toegevoegd, kunt u een `etag` Er wordt een waarde toegewezen die kan worden gebruikt om de labels op een later tijdstip bij te werken of te verwijderen.

Om de meest recente versie van de dataset-etiket entiteit terug te winnen, maak een [Verzoek om GET](#look-up) aan de `/datasets/{DATASET_ID}/labels` eindpunt. De huidige waarde wordt geretourneerd in de reactie onder een `etag` header. Wanneer het bijwerken van bestaande datasetetiketten, moeten de beste praktijken eerst een raadplegingsverzoek voor de dataset uitvoeren om zijn recentste te halen `etag` waarde vóór gebruik van die waarde in het dialoogvenster `If-Match` koptekst van uw volgende verzoek om PUT.

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
| `optionalLabels` | Een lijst van om het even welke individuele gebieden binnen de dataset die u etiketten aan wilt toevoegen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de [!DNL Experience Data Model] (XDM)-kenmerken van het veld. De volgende drie eigenschappen zijn vereist:<ul><li>id</code>: De URI $id</code> waarde van het schema dat aan het veld is gekoppeld.</li><li>contentType</code>: Het inhoudstype en het versienummer van het schema. Dit moet de vorm aannemen van een van de <a href="../../xdm/api/getting-started.md#accept">Koppen accepteren</a> voor een XDM opzoekverzoek.</li><li>schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

**Antwoord**

Een succesvolle reactie keert de bijgewerkte reeks etiketten voor de dataset terug.

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

## Volgende stappen

Door dit document te lezen hebt u geleerd hoe u gegevensgebruikslabels voor gegevenssets en velden kunt beheren met de [!DNL Dataset Service] API.

Zodra u de etiketten van het gegevensgebruik op dataset en gebied-niveau hebt toegevoegd, kunt u beginnen gegevens in te nemen [!DNL Experience Platform]. Als u meer wilt weten, begint u met het lezen van de [documentatie over gegevensinvoer](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie voor meer informatie de [overzicht van beleidsregels voor gegevensgebruik](../policies/overview.md).

Voor meer informatie over het beheren van datasets in [!DNL Experience Platform], zie de [Overzicht van gegevenssets](../../catalog/datasets/overview.md).
