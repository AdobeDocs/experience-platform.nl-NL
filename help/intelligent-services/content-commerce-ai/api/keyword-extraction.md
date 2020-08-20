---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Kleurextractie
topic: Developer guide
description: De service voor het uitnemen van trefwoorden extraheert bij een tekstdocument automatisch trefwoorden of trefwoorden die het onderwerp van het document het best beschrijven. Voor het uitpakken van trefwoorden wordt een combinatie van algoritmen voor herkenning van benoemde entiteit (NER) en zonder toezicht gebruikt voor het extraheren van trefwoorden.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---


# Trefwoordextractie

>[!NOTE]
>
>[!DNL Content and Commerce AI] is in bèta. De documentatie kan worden gewijzigd.

De service voor het uitnemen van trefwoorden extraheert bij een tekstdocument automatisch trefwoorden of trefwoorden die het onderwerp van het document het best beschrijven. Voor het uitpakken van trefwoorden wordt een combinatie van algoritmen voor herkenning van benoemde entiteit (NER) en zonder toezicht gebruikt voor het extraheren van trefwoorden.

**Ongecontroleerde uitwinning van trefwoorden**

Voor het extraheren van trefwoorden zonder toezicht wordt [[!DNL YAKE]](http://yake.inesctec.pt/) gebruikt. [!DNL YAKE] is een snelle en nauwkeurige automatische methode voor het automatisch uitpakken van trefwoorden zonder toezicht die wordt gebruikt om de belangrijkste trefwoorden in een document te selecteren. De uittreksels van trefwoorden [!DNL YAKE] worden vervolgens gefilterd om alleen zelfstandig naamwoorden te selecteren.

**Erkenning van benoemde entiteit**

Voor herkenning van benoemde entiteit wordt het OntoNotes-model van [[!DNL spaCy]](https://spacy.io/)gebruikt. Dit model wijst context-specifieke symbolische vectoren, deel-van-toespraak (POS) markeringen, gebiedsdeelontleding, en genoemde entiteiten toe. Het OntoNotes-model is een van de belangrijkste [!DNL spaCy] modellen. Meer informatie over het OntoNotes-model vindt u [hier](https://spacy.io/models/en).

De benoemde entiteiten die door [!DNL Content and Commerce AI] worden herkend, worden weergegeven in de volgende tabel:

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

De resultaten van [!DNL OntoNotes] worden gecombineerd met de trefwoorden van [!DNL YAKE], en worden vervolgens gerangschikt op basis van hun belang.

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
>`analyzer_id` bepaalt welke [!DNL Sensei Content Framework] wordt gebruikt. Controleer of je de juiste gegevens hebt `analyzer_id` voordat je een aanvraag indient.

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
| `analyzer_id` | De [!DNL Sensei] dienst identiteitskaart dat uw verzoek onder wordt opgesteld. Deze id bepaalt welke van de [!DNL Sensei Content Frameworks] waarden worden gebruikt. | Ja |
| `application-id` | De id van de toepassing die is gemaakt. | Ja |
| `data` | Een array die een JSON-object bevat met elk object in de array die een document vertegenwoordigt. Elke parameter die als onderdeel van deze array wordt doorgegeven, overschrijft de algemene parameters die buiten de `data` array zijn opgegeven. Alle overige eigenschappen die hieronder in deze tabel worden beschreven, kunnen van binnenuit worden overschreven `data`. | Ja |
| `language` | Taal van invoertekst. De standaardwaarde is `en`. | Nee |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline`. | Ja |
| `encoding` | De coderingsindeling van invoertekst. Dit kan `utf-8` of `utf-16`. De standaardwaarde voor deze eigenschap is `utf-8`. | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. Gebruik de waarde `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). Gebruik de waarde `0` om alle resultaten te retourneren. Wanneer gebruikt in combinatie met `threshold`, is het aantal geretourneerde resultaten het laagste van beide limietwaarden. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. Voor deze eigenschap is een geldig JSON-object vereist. Zie de [bijlage](#appendix) voor meer informatie over de douaneparameters. | Nee |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als deze waarde niet wordt doorgegeven, wordt een automatisch gegenereerde id toegewezen. | Nee |
| `content` | De inhoud die wordt gebruikt door de service voor het extraheren van trefwoorden. De inhoud kan onbewerkte tekst zijn (&#39;inline&#39;-inhoudstype). <br> Als de inhoud een bestand is op S3 (&#39;s3-bucket&#39; inhoudstype), geeft u de ondertekende URL door. Wanneer de inhoud deel van verzoek-lichaam uitmaakt, zou de lijst van gegevenselementen slechts één voorwerp moeten hebben. Wanneer meerdere objecten worden doorgegeven, wordt alleen het eerste object verwerkt. | Ja |

**Antwoord**

Een geslaagde reactie retourneert een JSON-object dat geëxtraheerde trefwoorden in de `response` array bevat.

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

## Aanhangsel {#appendix}

De volgende lijst bevat de beschikbare parameters die van binnen kunnen worden gebruikt `custom`.

| Naam | Beschrijving | Verplicht |
| --- | --- | --- |
| `min-n` | Het minimale aantal woorden dat vereist is in de trefwoorden. | Nee |
| `entity-types` | Typen te retourneren entiteiten. Zie de tabel met benoemde entiteitsherkenning aan het begin van dit document. | Nee |