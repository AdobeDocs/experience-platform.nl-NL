---
keywords: Experience Platform;aan de slag;inhoud ai;handel ai;inhoud en handel ai;sleutelwoordextractie;Trefwoordextractie
solution: Experience Platform, Intelligent Services
title: Trefwoordextractie in de API voor Inhoud en Handel
topic: Developer guide
description: De service voor het uitnemen van trefwoorden extraheert bij een tekstdocument automatisch trefwoorden of trefwoorden die het onderwerp van het document het best beschrijven. Voor het uitpakken van trefwoorden wordt een combinatie van algoritmen voor herkenning van benoemde entiteit (NER) en zonder toezicht gebruikt voor het extraheren van trefwoorden.
translation-type: tm+mt
source-git-commit: d10c00694b0a3b2a9da693bd59615b533cfae468
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 2%

---


# Trefwoordextractie

>[!NOTE]
>
>[!DNL Content and Commerce AI] is in bèta. De documentatie kan worden gewijzigd.

De service voor het uitnemen van trefwoorden extraheert bij een tekstdocument automatisch trefwoorden of trefwoorden die het onderwerp van het document het best beschrijven. Voor het uitpakken van trefwoorden wordt een combinatie van algoritmen voor herkenning van benoemde entiteit (NER) en zonder toezicht gebruikt voor het extraheren van trefwoorden.

De benoemde entiteiten die worden herkend door [!DNL Content and Commerce AI], worden weergegeven in de volgende tabel:

| Entiteitsnaam | Beschrijving |
| --- | --- |
| PERSON | Mensen, inclusief fictie. |
| NORP | Nationaliteiten of religieuze of politieke groeperingen. |
| GPE | Landen, steden en staten. |
| LOC | Niet-GPE-locaties, bergketens, waterlichamen. |
| FAC | Gebouwen, luchthavens, snelwegen, bruggen, enz. |
| ORG | Bedrijven, agentschappen, instellingen, enz. |
| PRODUCT | Objecten, voertuigen, voedingsmiddelen, enz. (Geen services.) |
| GEBEURTENIS | Hurricanes, gevechten, oorlogen, sportevenementen, enz. |
| WORK_OF_ART | Titels van boeken, liederen, enz. |
| WET | Benoemde documenten die in wetten zijn gemaakt. |
| TAAL | Elke benoemde taal. |

>[!NOTE]
>
>Als u PDF&#39;s wilt verwerken, slaat u de instructies voor [het uitpakken van PDF-trefwoorden](#pdf-extraction) in dit document over. Ondersteuning voor aanvullende bestandstypen, zoals docx, ppt en amd xml, wordt ook ingesteld op releasedatum op een later tijdstip.

**API-indeling**

```http
POST /services/v1/predict
```

**Verzoek**

In het volgende verzoek worden trefwoorden uit een document geëxtraheerd op basis van de invoerparameters die in de payload worden opgegeven.

Vereenvoudigde JSON van het invoerbestand:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

>[!CAUTION]
>
>`analyzer_id` bepaalt welke  [!DNL Sensei Content Framework] wordt gebruikt. Controleer of u de juiste `analyzer_id` hebt voordat u uw verzoek indient. Voor de service voor het extraheren van trefwoorden is de `analyzer_id`-id:
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\",
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| Eigenschap | Beschrijving | Verplicht |
| --- | --- | --- |
| `analyzer_id` | De [!DNL Sensei] service-id waarin uw verzoek is geïmplementeerd. Deze id bepaalt welke van [!DNL Sensei Content Frameworks] worden gebruikt. Neem voor aangepaste services contact op met het AI-team voor Inhoud en Handel om een aangepaste id in te stellen. | Ja |
| `application-id` | De id van de gemaakte toepassing. | Ja |
| `data` | Een array die een JSON-object bevat met elk object in de array die een document vertegenwoordigt. Elke parameter die als onderdeel van deze array wordt doorgegeven, overschrijft de algemene parameters die buiten de array `data` zijn opgegeven. Alle overige eigenschappen die hieronder in deze tabel worden beschreven, kunnen worden overschreven vanuit `data`. | Ja |
| `language` | Taal van invoertekst. De standaardwaarde is `en`. | Nee |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline`. | Ja |
| `encoding` | De coderingsindeling van invoertekst. Dit kan `utf-8` of `utf-16` zijn. De standaardwaarde voor deze eigenschap is `utf-8`. | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. Gebruik de waarde `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). Gebruik de waarde `0` om alle resultaten te retourneren. Wanneer gebruikt in combinatie met `threshold`, is het aantal teruggekeerde resultaten het laagste van één van beide vastgestelde grenzen. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. Voor deze eigenschap is een geldig JSON-object vereist. Zie [appendix](#appendix) voor meer informatie over de douaneparameters. | Nee |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als dit niet wordt overgegaan, wordt een auto-geproduceerde identiteitskaart toegewezen. | Nee |
| `content` | De inhoud die wordt gebruikt door de service voor het extraheren van trefwoorden. De inhoud kan onbewerkte tekst zijn (&#39;inline&#39;-inhoudstype). <br> Als de inhoud een bestand is op S3 (&#39;s3-bucket&#39; inhoudstype), geeft u de ondertekende URL door. Wanneer de inhoud deel van verzoek-lichaam uitmaakt, zou de lijst van gegevenselementen slechts één voorwerp moeten hebben. Wanneer meerdere objecten worden doorgegeven, wordt alleen het eerste object verwerkt. | Ja |

**Antwoord**

Een geslaagde reactie retourneert een JSON-object dat geëxtraheerde trefwoorden in de `response`-array bevat.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## Uitpakken van PDF-trefwoorden {#pdf-extraction}

De service voor het extraheren van trefwoorden ondersteunt PDF&#39;s, maar u moet een nieuwe Analyzer-id gebruiken voor PDF-bestanden en het documenttype wijzigen in PDF. Zie het onderstaande voorbeeld voor meer informatie.

**API-indeling**

```http
POST /services/v1/predict
```

**Verzoek**

Met de volgende aanvraag worden trefwoorden uit een PDF-document geëxtraheerd op basis van de invoerparameters die in de laadbewerking zijn opgegeven.

>[!CAUTION]
>
>`analyzer_id` bepaalt welke  [!DNL Sensei Content Framework] wordt gebruikt. Controleer of u de juiste `analyzer_id` hebt voordat u uw verzoek indient. Voor het extraheren van PDF-trefwoorden is de `analyzer_id`-id:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| Eigenschap | Beschrijving | Verplicht |
| --- | --- | --- |
| `analyzer_id` | De [!DNL Sensei] service-id waarin uw verzoek is geïmplementeerd. Deze id bepaalt welke van [!DNL Sensei Content Frameworks] worden gebruikt. Neem voor aangepaste services contact op met het AI-team voor Inhoud en Handel om een aangepaste id in te stellen. | Ja |
| `application-id` | De id van de gemaakte toepassing. | Ja |
| `data` | Een array die een JSON-object bevat met elk object in de array die een document vertegenwoordigt. Elke parameter die als onderdeel van deze array wordt doorgegeven, overschrijft de algemene parameters die buiten de array `data` zijn opgegeven. Alle overige eigenschappen die hieronder in deze tabel worden beschreven, kunnen worden overschreven vanuit `data`. | Ja |
| `language` | Taal van invoer. De standaardwaarde is `en` (Engels). | Nee |
| `content-type` | Wordt gebruikt om het inhoudstype van de invoer aan te geven. Deze moet worden ingesteld op `file`. | Ja |
| `encoding` | De coderingsindeling van de invoer. Deze moet worden ingesteld op `pdf`. Er zijn meer coderingstypen ingesteld die op een latere datum worden ondersteund. | Ja |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. Gebruik de waarde `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). Gebruik de waarde `0` om alle resultaten te retourneren. Wanneer gebruikt in combinatie met `threshold`, is het aantal teruggekeerde resultaten het laagste van één van beide vastgestelde grenzen. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. Voor deze eigenschap is een geldig JSON-object vereist. Zie [appendix](#appendix) voor meer informatie over de douaneparameters. | Nee |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als dit niet wordt overgegaan, wordt een auto-geproduceerde identiteitskaart toegewezen. | Nee |
| `content` | Deze moet worden ingesteld op `file`. | Ja |

**Antwoord**

Een geslaagde reactie retourneert een JSON-object dat geëxtraheerde trefwoorden in de `response`-array bevat.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

Voor meer informatie en een voorbeeld over het gebruik van extractie naar PDF met instructies over het instellen, implementeren en integreren van de AEM cloudservice. Bezoek de [CCAI PDF extractiewerker github repository](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Bijlage {#appendix}

De volgende lijst bevat de beschikbare parameters die van binnen `custom` kunnen worden gebruikt.

| Naam | Beschrijving | Verplicht |
| --- | --- | --- |
| `min-n` | Het minimale aantal woorden dat vereist is in de trefwoorden. | Nee |
| `entity-types` | Typen te retourneren entiteiten. Zie de tabel met benoemde entiteitsherkenning aan het begin van dit document. | Nee |