---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;color extraction;Color extraction
solution: Experience Platform
title: Kleurextractie
topic: Developer guide
description: Wanneer u een afbeelding opgeeft, kan de service voor kleurextractie het histogram van pixelkleuren berekenen en deze sorteren op dominante kleuren in emmers.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---


# Kleurextractie

>[!NOTE]
>
>[!DNL Content and Commerce AI] is in bèta. De documentatie kan worden gewijzigd.

Wanneer u een afbeelding krijgt met kleurextractie, kunt u een histogram met pixelkleuren berekenen en deze sorteren op dominante kleuren in emmers. De kleuren in de afbeeldingspixels worden in 40 overheersende kleuren gedicht die representatief zijn voor het kleurenspectrum. Vervolgens wordt een histogram met kleurwaarden berekend tussen deze 40 kleuren. De dienst heeft twee varianten:

**Kleur extraheren (volledige afbeelding)**

Met deze methode extraheert u een kleurenhistogram over de hele afbeelding.

**Kleur extraheren (met masker)**

Deze methode gebruikt een op diepleren gebaseerde voorgrondextractor om objecten op de voorgrond te identificeren. Het model is opgeleid voor een catalogus met e-commerceafbeeldingen. Nadat het voorgrondobject is geëxtraheerd, wordt een histogram berekend over de dominante kleuren, zoals eerder beschreven.

De volgende afbeelding is gebruikt in het voorbeeld dat in dit document wordt weergegeven:

![testafbeelding](../images/test_image.jpeg)

**API-indeling**

```http
POST /services/v1/predict
```

**Verzoek**

In het volgende voorbeeldverzoek wordt de methode full-image gebruikt voor het extraheren van kleuren.

In het volgende verzoek worden kleuren uit een afbeelding geëxtraheerd op basis van de invoerparameters die in de lading zijn opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

>[!CAUTION]
>
>`analyzer_id` bepaalt welke [!DNL Sensei Content Framework] wordt gebruikt. Controleer of je de juiste gegevens hebt `analyzer_id` voordat je een aanvraag indient.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| Eigenschap | Beschrijving | Verplicht |
| --- | --- | --- |
| `analyzer_id` | De [!DNL Sensei] dienst identiteitskaart dat uw verzoek onder wordt opgesteld. Deze id bepaalt welke van de [!DNL Sensei Content Frameworks] waarden worden gebruikt. | Ja |
| `application-id` | De id van de toepassing die u hebt gemaakt. | Ja |
| `data` | Een array die JSON-objecten bevat. Elk object in de array vertegenwoordigt een afbeelding. Elke parameter die als onderdeel van deze array wordt doorgegeven, overschrijft de algemene parameters die buiten de `data` array zijn opgegeven. Alle overige eigenschappen die hieronder in deze tabel worden beschreven, kunnen van binnenuit worden overschreven `data`. | Ja |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als dit niet wordt overgegaan, wordt een auto-geproduceerde identiteitskaart toegewezen. | Nee |
| `content` | De inhoud die door de service voor kleurextractie moet worden geanalyseerd. Als de afbeelding deel uitmaakt van de hoofdtekst van het verzoek, gebruikt u de opdracht Krullen `-F file=@<filename>` om de afbeelding door te geven, waarbij deze parameter als een lege tekenreeks blijft. <br> Als de afbeelding een bestand is op S3, geeft u de ondertekende URL door. Wanneer de inhoud deel uitmaakt van de aanvraaginstantie, mag de lijst met gegevenselementen slechts één object bevatten. Wanneer meerdere objecten worden doorgegeven, wordt alleen het eerste object verwerkt. | Ja |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline`. | Nee |
| `encoding` | De bestandsindeling van de invoerafbeelding. Momenteel kunnen alleen JPEG- en PNG-afbeeldingen worden verwerkt. De standaardwaarde voor deze eigenschap is `jpeg`. | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. Gebruik de waarde `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). Gebruik de waarde `0` om alle resultaten te retourneren. Wanneer gebruikt in combinatie met `threshold`, is het aantal geretourneerde resultaten het laagste van beide limietwaarden. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. | Nee |
| `historic-metadata` | Een array waarvan metagegevens kunnen worden doorgegeven. | Nee |

**Antwoord**

Wanneer de reactie is gelukt, worden de details van de geëxtraheerde kleuren geretourneerd. Elke kleur wordt vertegenwoordigd door een `feature_value` sleutel, die de volgende informatie bevat:

- Een kleurnaam
- Het percentage waarmee deze kleur wordt weergegeven in verhouding tot de afbeelding
- De RGB-waarde van de kleur

In het eerste onderstaande voorbeeldobject `feature_value` betekent de waarde `White,0.82,239,239,239` van de gevonden kleur wit, wit gevonden in 82% van de afbeelding en heeft een RGB-waarde van 239.239.239.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.82,239,239,239"
              },
              {
                "feature_value": "Dark_Blue,0.11,41,60,86",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Royal_Blue,0.08,63,91,123"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `content_id` | De naam van de afbeelding die is geüpload in uw verzoek om POST. |
| `feature_value` | Een array waarvan de objecten sleutels met dezelfde eigenschapnaam bevatten. Deze toetsen bevatten een tekenreeks die de kleurnaam vertegenwoordigt, een percentage dat deze kleur aangeeft ten opzichte van de afbeelding die in de kleur is verzonden `content_id`, en de RGB-waarde van de kleur. |
