---
keywords: Experience Platform;huis;populaire onderwerpen;de naleving van het gegevensgebruik;afdwingen;afdwingen de naleving van het gegevensgebruik;de Dienst van de segmentatie;segmentatie;Segmentatie;
solution: Experience Platform
title: Naleving van gegevensgebruik afdwingen voor een publiekssegment met behulp van API's
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het afdwingen van naleving van gegevensgebruik voor de publiekssegmenten van het Profiel van de Klant in real time die APIs gebruiken.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 0%

---

# Compatibiliteit met gegevensgebruik afdwingen voor een publiekssegment met behulp van API&#39;s

In deze zelfstudie worden de stappen beschreven voor het afdwingen van compatibiliteit met gegevensgebruik voor [!DNL Real-time Customer Profile] publiekssegmenten die API&#39;s gebruiken.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Adobe Experience Platform]:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): [!DNL Real-time Customer Profile] is een generische opslag van de raadplegingsentiteit, en wordt gebruikt om te beheren [!DNL Experience Data Model (XDM)] gegevens binnen [!DNL Platform]. Het profiel voegt gegevens over diverse activa van ondernemingsgegevens samen en verleent toegang tot die gegevens in een verenigde presentatie.
   - [Beleid samenvoegen](../../profile/api/merge-policies.md): Regels die worden gebruikt door [!DNL Real-time Customer Profile] om te bepalen welke gegevens onder bepaalde omstandigheden in één weergave kunnen worden samengevoegd. Het beleid van de fusie kan voor de doeleinden van het Beleid van Gegevens worden gevormd.
- [[!DNL Segmentation]](../home.md): Hoe [!DNL Real-time Customer Profile] verdeelt een grote groep individuen in de profielopslag in kleinere groepen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.
- [Gegevensbeheer](../../data-governance/home.md): Gegevensbeheer biedt de infrastructuur voor de etikettering en handhaving van gegevensgebruik, waarbij de volgende componenten worden gebruikt:
   - [Labels voor gegevensgebruik](../../data-governance/labels/user-guide.md): Etiketten die worden gebruikt om gegevenssets en velden te beschrijven in termen van het gevoeligheidsniveau waarmee hun respectieve gegevens worden verwerkt.
   - [Beleid voor gegevensgebruik](../../data-governance/policies/overview.md): Configuraties die aangeven welke marketingacties zijn toegestaan op gegevens die zijn gecategoriseerd door bepaalde labels voor gegevensgebruik.
   - [Beleidshandhaving](../../data-governance/enforcement/overview.md): Hiermee kunt u beleid voor gegevensgebruik afdwingen en gegevensbewerkingen die beleidsovertredingen vormen, voorkomen.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Platform] API&#39;s.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een samenvoegingsbeleid voor een segmentdefinitie opzoeken {#merge-policy}

Dit werkschema begint door tot een bekend publiekssegment toegang te hebben. Segmenten die zijn ingeschakeld voor gebruik in [!DNL Real-time Customer Profile] bevatten een identiteitskaart van het fusiebeleid binnen hun segmentdefinitie. Dit samenvoegbeleid bevat informatie over welke datasets in het segment moeten worden omvat, die beurtelings om het even welke toepasselijke etiketten van het gegevensgebruik bevatten.

Met de [!DNL Segmentation] API, kunt u omhoog een segmentdefinitie door zijn identiteitskaart kijken om zijn bijbehorend fusiebeleid te vinden.

**API-indeling**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | De id van de segmentdefinitie die u wilt opzoeken. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de segmentdefinitie terug.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `mergePolicyId` | De id van het samenvoegbeleid dat voor de segmentdefinitie wordt gebruikt. Dit wordt in de volgende stap gebruikt. |

## Vind de brondatasets van het fusiebeleid {#datasets}

Het beleid van de fusie bevat informatie over hun brondatasets, die beurtelings de etiketten van het gegevensgebruik bevatten. U kunt de details van een fusiebeleid opzoeken door identiteitskaart van het fusiebeleid in een verzoek van de GET aan te verstrekken [!DNL Profile] API. Meer informatie over het samenvoegbeleid vindt u in het gedeelte [eindhulplijn voor samenvoegbeleid](../../profile/api/merge-policies.md).

**API-indeling**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | De id van het samenvoegbeleid dat is verkregen in het dialoogvenster [vorige stap](#merge-policy). |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert de details van het samenvoegbeleid.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schema.name` | De naam van het schema verbonden aan het fusiebeleid. |
| `attributeMerge.type` | Het configuratietype van de gegevensbelangrijkheid voor het samenvoegbeleid. Als de waarde `dataSetPrecedence`, worden de datasets verbonden aan dit fusiebeleid vermeld onder `attributeMerge > data > order`. Als de waarde `timestampOrdered`, dan alle datasets verbonden aan het schema in `schema.name` worden gebruikt door het samenvoegbeleid. |
| `attributeMerge.data.order` | Als de `attributeMerge.type` is `dataSetPrecedence`, zal dit attribuut een serie die IDs van de datasets bevatten door dit fusiebeleid wordt gebruikt. Deze id&#39;s worden in de volgende stap gebruikt. |

## Gegevenssets evalueren voor beleidsovertredingen

>[!NOTE]
>
> In deze stap wordt ervan uitgegaan dat u ten minste één actief beleid voor gegevensgebruik hebt dat voorkomt dat specifieke marketingacties worden uitgevoerd op gegevens die bepaalde labels bevatten. Als u geen toepasselijk gebruiksbeleid voor de datasets hebt die worden geëvalueerd, gelieve te volgen [zelfstudie over het maken van beleid](../../data-governance/policies/create.md) om er een te maken voordat u doorgaat met deze stap.

Zodra u identiteitskaarts van de brondatasets van het fusiebeleid hebt verkregen, kunt u gebruiken [Beleidsservice-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) deze gegevensreeksen te evalueren aan de hand van specifieke marketingacties om na te gaan of er sprake is van schendingen van het gegevensgebruiksbeleid.

Om de datasets te evalueren, moet u de naam van de marketing actie in de weg van een verzoek van de POST verstrekken, terwijl het verstrekken van dataset IDs binnen het verzoeklichaam, zoals aangetoond in het voorbeeld hieronder.

**API-indeling**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketing actie verbonden aan het beleid van het gegevensgebruik u de datasets door evalueert. Afhankelijk van of het beleid door Adobe of uw organisatie werd bepaald, moet u gebruiken `/marketingActions/core` of `/marketingActions/custom`, respectievelijk. |

**Verzoek**

Het volgende verzoek test de `exportToThirdParty` het in de handel brengen van [vorige stap](#datasets). De aanvraaglading is een serie die IDs van elke dataset bevat.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `entityType` | Elk item in de payload-array moet het type entiteit aangeven dat wordt gedefinieerd. Voor dit gebruik is de waarde altijd &quot;dataSet&quot;. |
| `entityID` | Elk punt in de ladingsserie moet unieke identiteitskaart voor een dataset verstrekken. |

**Antwoord**

Een succesvolle reactie keert URI voor de marketing actie, de etiketten van het gegevensgebruik terug die uit de verstrekte datasets werden verzameld, en een lijst van om het even welk beleid van het gegevensgebruik dat als resultaat van het testen van de actie tegen die etiketten werd geschonden. In dit voorbeeld wordt het beleid Gegevens exporteren naar derde partij weergegeven in het dialoogvenster `violatedPolicies` array, die aangeeft dat de marketingactie een beleidsovertreding heeft veroorzaakt.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{IMS_ORG}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{IMS_ORG}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `duleLabels` | Een lijst met gegevensgebruikslabels die uit de verstrekte datasets zijn geëxtraheerd. |
| `discoveredLabels` | Een lijst van de datasets die in de verzoeklading werden verstrekt, tonend de datasetniveau en gebied-vlakke etiketten die in elk werden gevonden. |
| `violatedPolicies` | Een array met voorbeelden van beleidsregels voor gegevensgebruik die zijn overtreden door het testen van de marketingactie (opgegeven in `marketingActionRef`) tegen de verstrekte `duleLabels`. |

Met de gegevens die in de API-reactie worden geretourneerd, kunt u protocollen in uw ervaringstoepassing instellen om beleidsovertredingen op de juiste wijze af te dwingen.

## Gegevensvelden filteren

Als uw publiekssegment geen evaluatie overgaat, kunt u de gegevens aanpassen inbegrepen in het segment door één van de twee hieronder geschetste methodes.

### Het samenvoegbeleid van de segmentdefinitie bijwerken

Het bijwerken van het samenvoegbeleid van een segmentdefinitie zal de datasets en de gebieden aanpassen die zullen worden omvat wanneer de segmentbaan in werking wordt gesteld. Zie de sectie over [bijwerken van een bestaand samenvoegingsbeleid](../../profile/api/merge-policies.md#update) in de zelfstudie over het samenvoegbeleid van de API voor meer informatie.

### Specifieke gegevensvelden beperken bij het exporteren van het segment

Wanneer het uitvoeren van een segment naar een dataset gebruikend [!DNL Segmentation] API, kunt u de gegevens filtreren die in de uitvoer door te gebruiken `fields` parameter. Alle gegevensvelden die aan deze parameter worden toegevoegd, worden in de exportbewerking opgenomen, terwijl alle andere gegevensvelden worden uitgesloten.

Neem bijvoorbeeld een segment met gegevensvelden met de naam &quot;A&quot;, &quot;B&quot; en &quot;C&quot;. Als u alleen veld &quot;C&quot; wilt exporteren, `fields` parameter zou veld &quot;C&quot; alleen bevatten. Op deze manier worden de velden A en B bij het exporteren van het segment uitgesloten.

Zie de sectie over [een segment exporteren](./evaluate-a-segment.md#export) in de segmentatiezelfstudie voor meer informatie.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de labels van het gegevensgebruik verbonden aan een publiekssegment opgezocht en hen getest voor beleidsschendingen tegen specifieke marketing acties. Voor meer informatie over gegevensbeheer in [!DNL Experience Platform], lees het overzicht voor [Gegevensbeheer](../../data-governance/home.md).
