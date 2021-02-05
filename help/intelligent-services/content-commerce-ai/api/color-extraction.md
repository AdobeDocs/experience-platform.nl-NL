---
keywords: Experience Platform;aan de slag;inhoud ai;handel ai;inhoud en handel ai;kleur extractie;Kleur extractie
solution: Experience Platform, Intelligent Services
title: Kleurextractie in de API voor Inhoud en Handel
topic: Developer guide
description: Wanneer u een afbeelding opgeeft, kan de service voor kleurextractie het histogram van pixelkleuren berekenen en deze sorteren op dominante kleuren in emmers.
translation-type: tm+mt
source-git-commit: d10c00694b0a3b2a9da693bd59615b533cfae468
workflow-type: tm+mt
source-wordcount: '712'
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

![testafbeelding](../images/QQAsset1.jpg)

**API-indeling**

```http
POST /services/v1/predict
```

**Verzoek**

In het volgende voorbeeldverzoek wordt de methode full-image gebruikt voor het extraheren van kleuren.

In het volgende verzoek worden kleuren uit een afbeelding geëxtraheerd op basis van de invoerparameters die in de lading zijn opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

>[!CAUTION]
>
>`analyzer_id` bepaalt welke  [!DNL Sensei Content Framework] wordt gebruikt. Controleer of u de juiste `analyzer_id` hebt voordat u uw verzoek indient. Voor service voor kleurextractie is de `analyzer_id`-id:
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

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
| `analyzer_id` | De [!DNL Sensei] service-id waarin uw verzoek is geïmplementeerd. Deze id bepaalt welke van [!DNL Sensei Content Frameworks] worden gebruikt. Neem voor aangepaste services contact op met het AI-team voor Inhoud en Handel om een aangepaste id in te stellen. | Ja |
| `application-id` | De id van de toepassing die u hebt gemaakt. | Ja |
| `data` | Een array die JSON-objecten bevat. Elk object in de array vertegenwoordigt een afbeelding. Elke parameter die als onderdeel van deze array wordt doorgegeven, overschrijft de algemene parameters die buiten de array `data` zijn opgegeven. Alle overige eigenschappen die hieronder in deze tabel worden beschreven, kunnen worden overschreven vanuit `data`. | Ja |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als dit niet wordt overgegaan, wordt een auto-geproduceerde identiteitskaart toegewezen. | Nee |
| `content` | De inhoud die door de service voor kleurextractie moet worden geanalyseerd. Als de afbeelding deel uitmaakt van de hoofdtekst van het verzoek, gebruikt u `-F file=@<filename>` in de opdracht Krullen om de afbeelding door te geven, zodat deze parameter een lege tekenreeks blijft. <br> Als de afbeelding een bestand is op S3, geeft u de ondertekende URL door. Wanneer de inhoud deel uitmaakt van de aanvraaginstantie, mag de lijst met gegevenselementen slechts één object bevatten. Wanneer meerdere objecten worden doorgegeven, wordt alleen het eerste object verwerkt. | Ja |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline`. | Nee |
| `encoding` | De bestandsindeling van de invoerafbeelding. Momenteel kunnen alleen JPEG- en PNG-afbeeldingen worden verwerkt. De standaardwaarde voor deze eigenschap is `jpeg`. | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. Gebruik de waarde `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). Gebruik de waarde `0` om alle resultaten te retourneren. Wanneer gebruikt in combinatie met `threshold`, is het aantal teruggekeerde resultaten het laagste van één van beide vastgestelde grenzen. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. | Nee |
| `historic-metadata` | Een array waarvan metagegevens kunnen worden doorgegeven. | Nee |

**Antwoord**

Wanneer de reactie is gelukt, worden de details van de geëxtraheerde kleuren geretourneerd. Elke kleur wordt vertegenwoordigd door een `feature_value` sleutel, die de volgende informatie bevat:

- Een kleurnaam
- Het percentage waarmee deze kleur wordt weergegeven in verhouding tot de afbeelding
- De RGB-waarde van de kleur

In het eerste voorbeeldobject hieronder betekent `feature_value` van `White,0.59,251,251,243` dat de gevonden kleur wit is, wit in 59% van de afbeelding en een RGB-waarde van 251.251.243 heeft.

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
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
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
| `feature_value` | Een array waarvan de objecten sleutels met dezelfde eigenschapnaam bevatten. Deze toetsen bevatten een tekenreeks die de kleurnaam vertegenwoordigt, een percentage dat deze kleur aangeeft ten opzichte van de afbeelding die is verzonden in `content_id` en de RGB-waarde van de kleur. |
