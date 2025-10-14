---
solution: Experience Platform
title: Naleving van gegevensgebruik afdwingen voor een publiekssegment met behulp van API's
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het afdwingen van definities van compatibiliteitssegmenten voor gegevensgebruik met API's.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 0%

---

# Compatibiliteit met gegevensgebruik afdwingen voor een segmentdefinitie met behulp van API&#39;s

Deze zelfstudie behandelt de stappen voor het afdwingen van de naleving van gegevensgebruik voor segmentdefinities die API&#39;s gebruiken.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van [!DNL Adobe Experience Platform] :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] is een algemene opslag van opzoekentiteiten en wordt gebruikt om [!DNL Experience Data Model (XDM)] -gegevens te beheren binnen [!DNL Experience Platform] . Het profiel voegt gegevens over diverse activa van ondernemingsgegevens samen en verleent toegang tot die gegevens in een verenigde presentatie.
   - [&#x200B; beleid van de Fusie &#x200B;](../../profile/api/merge-policies.md): Regels die door [!DNL Real-Time Customer Profile] worden gebruikt om te bepalen welke gegevens in een verenigde mening onder bepaalde voorwaarden kunnen worden samengevoegd. Het beleid van de fusie kan voor de doeleinden van het Beleid van Gegevens worden gevormd.
- [[!DNL Segmentation]](../home.md): Hoe [!DNL Real-Time Customer Profile] een grote groep personen in het archief Profiel verdeelt in kleinere groepen die vergelijkbare kenmerken hebben en op dezelfde manier reageren op marketingstrategieën.
- [&#x200B; Beheer van Gegevens &#x200B;](../../data-governance/home.md): Het Beleid van gegevens verstrekt de infrastructuur voor het etiketteren en de handhaving van het gegevensgebruik, gebruikend de volgende componenten:
   - [&#x200B; de gebruiksetiketten van Gegevens &#x200B;](../../data-governance/labels/user-guide.md): De etiketten die worden gebruikt om datasets en gebieden in termen van het niveau van gevoeligheid te beschrijven waarmee om hun respectieve gegevens te behandelen.
   - [&#x200B; het gebruiksbeleid van Gegevens &#x200B;](../../data-governance/policies/overview.md): Configuraties die wijzen op welke marketing acties op gegevens worden toegestaan die door de bijzondere etiketten van het gegevensgebruik worden gecategoriseerd.
   - [&#x200B; de handhaving van het Beleid &#x200B;](../../data-governance/enforcement/overview.md): Staat u toe om het beleid van het gegevensgebruik af te dwingen en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.
- [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen naar de API&#39;s van [!DNL Experience Platform] te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [&#x200B; documentatie van het zandbakoverzicht &#x200B;](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een samenvoegingsbeleid voor een segmentdefinitie opzoeken {#merge-policy}

Dit werkschema begint door tot een bekende segmentdefinitie toegang te hebben. Segmentdefinities die zijn ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] bevatten een samenvoegbeleid-id binnen de segmentdefinitie. Dit samenvoegbeleid bevat informatie over welke datasets in de segmentdefinitie moeten worden omvat, die beurtelings om het even welke toepasselijke etiketten van het gegevensgebruik bevatten.

Met de API [!DNL Segmentation] kunt u een segmentdefinitie opzoeken aan de hand van de id om het bijbehorende samenvoegbeleid te vinden.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de details van de segmentdefinitie terug.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
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

Het beleid van de fusie bevat informatie over hun brondatasets, die beurtelings de etiketten van het gegevensgebruik bevatten. U kunt de details van een samenvoegbeleid opzoeken door de id van het samenvoegbeleid op te geven in een GET-aanvraag naar de [!DNL Profile] API. Meer informatie over fusiebeleid kan in de [&#x200B; gids van het het eindpunt van samenvoegingsbeleid &#x200B;](../../profile/api/merge-policies.md) worden gevonden.

**API formaat**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | Identiteitskaart van het samenvoegbeleid dat in de [&#x200B; vorige stap &#x200B;](#merge-policy) wordt verkregen. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie retourneert de details van het samenvoegingsbeleid.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
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
| `attributeMerge.type` | Het configuratietype van de gegevensbelangrijkheid voor het samenvoegbeleid. Als de waarde `dataSetPrecedence` is, worden de gegevenssets die aan dit samenvoegbeleid zijn gekoppeld, onder `attributeMerge > data > order` weergegeven. Als de waarde `timestampOrdered` is, worden alle datasets die zijn gekoppeld aan het schema waarnaar in `schema.name` wordt verwezen, gebruikt door het samenvoegbeleid. |
| `attributeMerge.data.order` | Als `attributeMerge.type` `dataSetPrecedence` is, zal dit attribuut een serie zijn die IDs van de datasets bevat die door dit fusiebeleid worden gebruikt. Deze id&#39;s worden in de volgende stap gebruikt. |

## Gegevenssets evalueren voor beleidsovertredingen

>[!NOTE]
>
> In deze stap wordt ervan uitgegaan dat u ten minste één actief beleid voor gegevensgebruik hebt dat voorkomt dat specifieke marketingacties worden uitgevoerd op gegevens die bepaalde labels bevatten. Als u geen toepasselijk gebruiksbeleid voor de datasets hebt die worden geëvalueerd, te volgen gelieve het [&#x200B; leerprogramma van de beleidsverwezenlijking &#x200B;](../../data-governance/policies/create.md) om tot één te leiden alvorens met deze stap verder te gaan.

Zodra u IDs van de brondatasets van het fusiebeleid hebt verkregen, kunt u de [&#x200B; Dienst API van het Beleid &#x200B;](https://www.adobe.io/experience-platform-apis/references/policy-service/) gebruiken om die datasets tegen specifieke marketing acties te evalueren om voor de schendingen van het gegevensgebruiksbeleid te controleren.

Om de datasets te evalueren, moet u de naam van de marketing actie in de weg van een POST- verzoek verstrekken, terwijl het verstrekken van dataset IDs binnen het verzoeklichaam, zoals aangetoond in het voorbeeld hieronder.

**API formaat**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschrijving |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | De naam van de marketing actie verbonden aan het beleid van het gegevensgebruik u de datasets door evalueert. Afhankelijk van of het beleid is gedefinieerd door Adobe of door uw organisatie, moet u respectievelijk `/marketingActions/core` of `/marketingActions/custom` gebruiken. |

**Verzoek**

Het volgende verzoek test de `exportToThirdParty` marketing actie tegen datasets die in de [&#x200B; vorige stap &#x200B;](#datasets) worden verkregen. De aanvraaglading is een serie die IDs van elke dataset bevat.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

Een succesvolle reactie keert URI voor de marketing actie, de etiketten van het gegevensgebruik terug die uit de verstrekte datasets werden verzameld, en een lijst van om het even welk beleid van het gegevensgebruik dat als resultaat van het testen van de actie tegen die etiketten werd geschonden. In dit voorbeeld wordt het beleid Gegevens exporteren naar derden weergegeven in de array `violatedPolicies` om aan te geven dat de marketingactie een beleidsovertreding heeft veroorzaakt.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | Een array met vermelding van eventuele beleidsregels voor gegevensgebruik die zijn overtreden door de marketingactie (opgegeven in `marketingActionRef` ) te testen op basis van de opgegeven `duleLabels` . |

Met de gegevens die in de API-reactie worden geretourneerd, kunt u protocollen in uw ervaringstoepassing instellen om beleidsovertredingen op de juiste wijze af te dwingen.

## Gegevensvelden filteren

Als uw segmentdefinitie geen evaluatie overgaat, kunt u de gegevens aanpassen inbegrepen in de segmentdefinitie door één van de twee hieronder geschetste methodes.

### Het samenvoegbeleid van de segmentdefinitie bijwerken

Het bijwerken van het samenvoegbeleid van een segmentdefinitie zal de datasets en de gebieden aanpassen die zullen worden omvat wanneer de segmentbaan in werking wordt gesteld. Zie de sectie over [&#x200B; het bijwerken van een bestaand fusiebeleid &#x200B;](../../profile/api/merge-policies.md#update) in de API zelfstudie van het fusiebeleid voor meer informatie.

### Specifieke gegevensvelden beperken bij het exporteren van de segmentdefinitie

Wanneer u een segmentdefinitie naar een gegevensset exporteert met de API [!DNL Segmentation] , kunt u de gegevens die in de exportbewerking zijn opgenomen, filteren met de parameter `fields` . Alle gegevensvelden die aan deze parameter worden toegevoegd, worden in de exportbewerking opgenomen, terwijl alle andere gegevensvelden worden uitgesloten.

Overweeg een segmentdefinitie die gegevensvelden met de naam &quot;A&quot;, &quot;B&quot; en &quot;C&quot; heeft. Als u alleen veld C wilt exporteren, bevat de parameter `fields` alleen veld C. Op deze manier worden de velden A en B uitgesloten bij het exporteren van de segmentdefinitie.

Zie de sectie over [&#x200B; het uitvoeren van een segmentdefinitie &#x200B;](./evaluate-a-segment.md#export) in het segmenteringsleerprogramma voor meer informatie.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de etiketten van het gegevensgebruik verbonden aan een segmentdefinitie opgezocht en hen getest op beleidsschendingen tegen specifieke marketing acties. Voor meer informatie over het Beleid van Gegevens in [!DNL Experience Platform], gelieve het overzicht voor [&#x200B; het Beleid van Gegevens &#x200B;](../../data-governance/home.md) te lezen.
