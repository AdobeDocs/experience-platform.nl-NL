---
keywords: Experience Platform;home;populaire onderwerpen;dataset api;beheer gegevensgebruik;gegevensgebruik api
solution: Experience Platform
title: Labels voor gegevensgebruik voor gegevenssets beheren met API's
description: Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API van de Catalogusservice die metagegevens van gegevenssets beheert.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 9f3fa696ed60ce85fa93515e39716d89ec80f1ec
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 0%

---

# Gegevensgebruikslabels voor gegevenssets beheren met behulp van API&#39;s

De [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) kunt u gebruiksetiketten voor datasets toepassen en uitgeven. Het maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de [!DNL Catalog Service] API die gegevenssetmetagegevens beheert.

<!-- >[!IMPORTANT]
>
>Applying labels at the dataset level is only supported for data governance use cases. If you are trying to create access policies for the data, you must [apply labels to the schema](../../xdm/tutorials/labels.md) that the dataset is based on. See the overview on [attribute-based access control](../../access-control/abac/overview.md) for more information. -->

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

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

U kunt een reeks etiketten voor een volledige dataset toepassen door hen in de nuttige lading van een POST of een verzoek van de PUT op te geven [!DNL Dataset Service] API. Het verzoeklichaam is het zelfde voor beide vraag. U kunt geen labels toevoegen aan afzonderlijke gegevenssetvelden.

**API-indeling**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvoor u etiketten creeert. |

**Verzoek**

Het verzoek van de POST van het voorbeeld hieronder werkt de volledige dataset met a bij `C1` label. De velden in de payload zijn gelijk aan de velden die vereist zijn voor een PUT-aanvraag.

<!-- When making API calls that update the existing labels of a dataset (PUT), an `If-Match` header that indicates the current version of the dataset-label entity in Dataset Service must be included. In order to prevent data collisions, the service will only update the dataset entity if the included `If-Match` string matches the latest version tag generated by the system for that dataset. -->

>[!NOTE]
>
>Als er momenteel labels voor de betrokken gegevensset bestaan, kunnen nieuwe labels alleen worden toegevoegd via een verzoek van de PUT, waarvoor een `If-Match` header. Nadat labels aan een gegevensset zijn toegevoegd, is de meest recente `etag` Deze waarde is vereist als u de labels later wilt bijwerken of verwijderen.

Om de meest recente versie van de dataset-etiket entiteit terug te winnen, maak een [Verzoek om GET](#look-up) aan de `/datasets/{DATASET_ID}/labels` eindpunt. De huidige waarde wordt geretourneerd in de reactie onder een `etag` header. Wanneer het bijwerken van bestaande datasetetiketten, moeten de beste praktijken eerst een raadplegingsverzoek voor de dataset uitvoeren om zijn recentste te halen `etag` waarde vóór gebruik van die waarde in de `If-Match` koptekst van uw volgende verzoek om PUT.

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
| `entityId.namespace` | Dit wordt gebruikt om botsingen van identiteitskaart te vermijden. De `namespace` is `AEP`. |
| `entityId.id` | De id van de bron die wordt bijgewerkt. Dit heeft betrekking op de `datasetId`. |
| `entityId.type` | Het type van de bron die wordt bijgewerkt. Dit zal altijd `dataset`. |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die u aan de volledige dataset wilt toevoegen. |
| `parents` | De `parents` array bevat een lijst met `entityId`s dat deze dataset etiketten van zal erven. Datasets kunnen labels overnemen van schema&#39;s en/of gegevenssets. |

**Antwoord**

Een succesvolle reactie keert de bijgewerkte reeks etiketten voor de dataset terug.

>[!IMPORTANT]
>
>De `optionalLabels` eigenschap is vervangen voor gebruik met POST-aanvragen. Het is niet meer mogelijk om gegevensetiketten aan datasetgebieden toe te voegen. Een POST-bewerking zal een fout veroorzaken als een `optionalLabel` waarde aanwezig is. U kunt echter labels uit afzonderlijke velden verwijderen met behulp van een PUT-aanvraag en de `optionalLabels` eigenschap. Zie voor meer informatie de sectie over [het verwijderen van etiketten uit een dataset](#remove).

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

U kunt eerder toegepaste veldlabels verwijderen door de bestaande `optionalLabels` waarde(n) met een subset van de bestaande veldlabels of een lege lijst om deze volledig te verwijderen. Voer een verzoek van de PUT in aan de [!DNL Dataset Service] API om eerder toegepaste labels bij te werken of te verwijderen.

**API-indeling**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvoor u etiketten creeert. |

**Verzoek**

De hieronder dataset waarop de verrichting van de PUT wordt toegepast had C1 optionalLabel op eigenschappen/person/properties/address gebied en C1, C2 optionalLabels op /properties/person/properties/name/properties/fullName gebied. Na de putoptie heeft het eerste veld geen label (label C1 verwijderd) en het tweede veld heeft alleen het label C1 (label C2 verwijderd)

In het onderstaande voorbeeldscenario wordt een aanvraag voor een PUT gebruikt om labels te verwijderen die aan afzonderlijke velden zijn toegevoegd. Voordat het verzoek werd ingediend, `fullName` het veld had `C1` en `C2` toegepaste labels en de `address` veld had al een `C1` label toegepast. De aanvraag PUT negeert bestaande labels `C1, C2` van de `fullName` veld met een `C1` label gebruiken `optionalLabels.labels` parameter. Het verzoek negeert ook het `C1` van de `address` veld met een lege set veldlabels.

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
        "parents": [],
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
| `entityId` | Dit identificeert de specifieke gegevenssetentiteit die moet worden bijgewerkt. De `entityId` moeten de volgende drie waarden bevatten:<br/><br/>`namespace`: Dit wordt gebruikt om botsingen van identiteitskaart te vermijden. De `namespace` is `AEP`.<br/>`id`: De id van de bron die wordt bijgewerkt. Dit heeft betrekking op de `datasetId`.<br/>`type`: Het type van de bron die wordt bijgewerkt. Dit zal altijd `dataset`. |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die u aan de volledige dataset wilt toevoegen. |
| `parents` | De `parents` array bevat een lijst met `entityId`s dat deze dataset etiketten van zal erven. Datasets kunnen labels overnemen van schema&#39;s en/of gegevenssets. |
| `optionalLabels` | Deze parameter wordt gebruikt om etiketten te verwijderen die eerder op een datasetgebied worden toegepast. Een lijst van om het even welke individuele gebieden binnen de dataset die u de etiketten wilt verwijderen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de eigenschap [!DNL Experience Data Model] (XDM)-kenmerken van het veld. De volgende drie eigenschappen zijn vereist:<ul><li><code>id</code>: De URI <code>$id</code> De waarde van het schema dat aan het veld is gekoppeld.</li><li><code>contentType</code>: Het inhoudstype en het versienummer van het schema. Dit moet de vorm aannemen van een van de <a href="../../xdm/api/getting-started.md#accept">Koppen accepteren</a> voor een XDM opzoekverzoek.</li><li><code>schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: Deze waarde moet een subset van de bestaande toegepaste veldlabels bevatten of leeg zijn om alle bestaande veldlabels te verwijderen. De methoden PUT of POST retourneren nu een fout als de `optionalLabels` veld bevat nieuwe of gewijzigde labels. |

**Antwoord**

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

Door dit document te lezen hebt u geleerd hoe u gegevensgebruikslabels voor gegevenssets en velden kunt beheren met de [!DNL Dataset Service] API. U kunt nu definiëren [beleid voor gegevensgebruik](../policies/overview.md) en [toegangsbeheerbeleid](../../access-control/abac/ui/policies.md) op basis van de labels die u hebt toegepast.

Voor meer informatie over het beheren van datasets in [!DNL Experience Platform], zie de [Overzicht van gegevenssets](../../catalog/datasets/overview.md).
