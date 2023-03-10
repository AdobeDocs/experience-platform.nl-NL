---
keywords: OCR;aanwezigheid van tekst;optische tekenherkenning
solution: Experience Platform
title: Aanwezigheid van tekst en optische tekenherkenning
description: In de API voor inhoudslabeling kan de service Aanwezigheid van tekst/Optische tekenherkenning (OCR) aangeven of er tekst aanwezig is in een bepaalde afbeelding. Als er tekst aanwezig is, kan OCR de tekst retourneren.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: feebf4c20d20afcdcfe4523e0b61bff5b999084c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Aanwezigheid van tekst en optische tekenherkenning

Met de OCR-service (Text Presence/Optical Character Recognition) kunt u aangeven of de afbeelding tekst bevat. Als er tekst aanwezig is, kan OCR de tekst retourneren.

De volgende afbeelding is gebruikt in de voorbeeldaanvraag die in dit document wordt weergegeven:

![Voorbeeldafbeelding](../images/sample_image.png)

**API-indeling**

```http
POST /services/v2/predict
```

**Verzoek**

Met het volgende verzoek wordt gecontroleerd of er tekst aanwezig is op basis van de invoerafbeelding die in de lading is opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

Uitvoering met inline-afbeelding:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**Antwoord**

Als het antwoord met succes is beantwoord, wordt de tekst geretourneerd die is aangetroffen in het dialoogvenster `tags` lijst voor elke afbeelding die in de aanvraag is doorgegeven. Als een bepaalde afbeelding geen tekst bevat, `is_text_present` is 0 en `tags` is een lege lijst.

[result0, result1, ...]: lijst met reacties voor elk invoerdocument. Elk resultaat is een dict met toetsen:

1. request_element_id: overeenkomende index met het invoerbestand voor deze reactie, 0 voor de eerste afbeelding in de documentenlijst van de aanvraag, 1 voor de volgende afbeelding enzovoort.
2. tags: lijst met woordenboeken, elk woordenboek heeft twee sleutels: tekst, een herkend woord uit de afbeelding, en relevantie, die wordt berekend als het deel van het gebied van het selectiekader van de geëxtraheerde tekst in vergelijking met de volledige afbeelding. 0,01 wordt omgezet in een tekst die minstens 1% van de afbeelding in beslag neemt.
3. is_text_present: 0 of 1, afhankelijk van of er tekst aanwezig is in de afbeelding. Als de labels 0 zijn, is de lijst leeg.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.05604639115920341
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**Verzoek**

Met het volgende verzoek wordt gecontroleerd of er tekst aanwezig is op basis van de invoerafbeelding die in de lading is opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

Uitvoering met URL:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| Eigenschap | Beschrijving | Verplicht |
| --- | --- | --- |
| `documents` | Lijst met JSON-elementen waarbij elk item in de lijst één afbeelding vertegenwoordigt. Alle parameters die als onderdeel van deze lijst worden doorgegeven, overschrijven de algemene parameter die buiten de lijst is opgegeven voor het overeenkomstige lijstelement. | Ja |
| `sensei:multipart_field_name` | field_name om de weg van het inputdossier van te lezen. | Ja |
| `repo:path` | Vooraf ondertekende URL naar afbeeldingselement. | Ja |
| `sensei:repoType` | &quot;HTTP&quot; (voor presigned-url). | Nee |
| `dc:format` | Gecodeerde indeling van invoerafbeelding. Alleen afbeeldingsindelingen zoals JPEG, JPG, PNG en TIF zijn toegestaan voor het coderen van afbeeldingen. De dc:indeling wordt vergeleken met toegestane indelingen. | Nee |
| `correct_with_dictionary` | Of de woorden met een Engels woordenboek moeten worden gecorrigeerd? Als deze optie niet is ingeschakeld, kunnen niet-Engelse woorden worden herkend. Standaard is waar: ingeschakeld.) Als het woordenboek is ingeschakeld, hoeft u niet altijd een Engels woord te hebben. We proberen het te corrigeren, maar als dit niet mogelijk is binnen een bepaalde bewerkingsafstand, retourneren we het oorspronkelijke woord. | Nee |
| `filter_with_dictionary` | Of u de woorden wilt filteren zodat deze alleen de woorden uit het Engelse woordenboek bevatten? Als dit wordt ingeschakeld, zullen de geretourneerde woorden altijd bij het grote Engels horen, dat 470 kB-woorden omvat. | Nee |
| `min_probability` | Wat is de minimale waarschijnlijkheid voor de erkende woorden? Alleen de woorden die uit de afbeelding zijn geëxtraheerd en die een grotere waarschijnlijkheid hebben dan min_likely, worden door de service geretourneerd. De standaardwaarde is ingesteld op 0,2. | Nee |
| `min_relevance` | Wat is de minimale relevantie voor de erkende woorden? Alleen de woorden die uit de afbeelding zijn geëxtraheerd en die relevanter zijn dan min_relevantie, worden door de service geretourneerd. De standaardwaarde is ingesteld op 0,01. De relevantie wordt berekend als het deel van het gebied van het selectiekader van de geëxtraheerde tekst ten opzichte van de volledige afbeelding. 0,01 wordt omgezet in een tekst die minstens 1% van de afbeelding in beslag neemt. | Nee |

| Naam | Datatype | Vereist | Standaard | Waarden | Beschrijving |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | Vooraf ondertekende URL van de afbeelding waaruit tekst moet worden geëxtraheerd. |
| `sensei:repoType` | string | - | - | HTTPS | Type repo waar de afbeelding wordt opgeslagen. |
| `sensei:multipart_field_name` | string | - | - | - | Gebruik deze optie wanneer u de afbeelding doorgeeft als een meerdelig argument in plaats van vooraf ondertekende URL&#39;s te gebruiken. |
| `dc:format` | string | Ja | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | De codering van afbeeldingen wordt gecontroleerd aan de hand van toegestane invoercoderingstypen voordat deze wordt verwerkt. |