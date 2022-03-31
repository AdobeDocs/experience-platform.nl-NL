---
keywords: OCR;aanwezigheid van tekst;optische tekenherkenning
solution: Experience Platform
title: Aanwezigheid van tekst en optische tekenherkenning
topic-legacy: Developer guide
description: In de AI API voor Inhoud en Handel kan de dienst van de Erkenning van het Karakter van de Tekst Aanwezigheid/Optische (OCR) van het Karakter erop wijzen als de tekst in een bepaalde beeld aanwezig is. Als er tekst aanwezig is, kan OCR de tekst retourneren.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# Aanwezigheid van tekst en optische tekenherkenning

>[!NOTE]
>
>AI van de Inhoud en van de Handel is in bèta. De documentatie kan worden gewijzigd.

De service Aanwezigheid tekst/Optische tekenherkenning (OCR) kan bij een afbeelding aangeven of er tekst aanwezig is in de afbeelding. Als er tekst aanwezig is, kan OCR de tekst retourneren.

De volgende afbeelding is gebruikt in de voorbeeldaanvraag die in dit document wordt weergegeven:

![testafbeelding](../images/shef.jpeg)

**API-indeling**

```http
POST /services/v1/predict
```

**Verzoek**

Met het volgende verzoek wordt gecontroleerd of er tekst aanwezig is op basis van de invoerafbeelding die in de lading is opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

>[!CAUTION]
>
>`analyzer_id` bepaalt welke [!DNL Sensei Content Framework] wordt gebruikt. Controleer of u de juiste `analyzer_id` voordat u uw verzoek indient. Neem contact op met het AI bètateam voor Inhoud en Handel om uw `analyzer_id` voor deze service.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
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
        "custom": {}
        }]
      }
    }]
  }'
```

| Eigenschap | Beschrijving | Verplicht |
| --- | --- | --- |
| `analyzer_id` | De [!DNL Sensei] service-id waarin uw verzoek is geïmplementeerd. Deze id bepaalt welke van de [!DNL Sensei Content Frameworks] worden gebruikt. Neem voor aangepaste services contact op met het AI-team voor Inhoud en Handel om een aangepaste id in te stellen. | Ja |
| `application-id` | De id van de toepassing die is gemaakt. | Ja |
| `data` | Een array die een JSON-object bevat waarvan elk object in de array één doorgegeven afbeelding vertegenwoordigt. Alle parameters die als onderdeel van deze array worden doorgegeven, overschrijven de algemene parameters die buiten de `data` array. Alle resterende eigenschappen die hieronder in deze tabel worden beschreven, kunnen van binnenuit worden overschreven `data`. | Ja |
| `language` | Taal van invoertekst. De standaardwaarde is `en`. | Nee |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline`. | Nee |
| `encoding` | De bestandsindeling van de invoerafbeelding. Momenteel kunnen alleen JPEG- en PNG-afbeeldingen worden verwerkt. De standaardwaarde voor deze eigenschap is `jpeg`. | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. De waarde gebruiken `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). De waarde gebruiken `0` om alle resultaten te retourneren. Indien gebruikt in combinatie met `threshold`, is het aantal geretourneerde resultaten het laagste van de twee ingestelde limieten. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. Voor deze eigenschap is een geldig JSON-object vereist. | Nee |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als dit niet wordt overgegaan, wordt een auto-geproduceerde identiteitskaart toegewezen. | Nee |
| `content` | De inhoud kan een Raw-afbeelding zijn (inline-inhoudstype). <br> Als de inhoud een bestand is op S3 (inhoudstype s3-bucket), geeft u de ondertekende URL door. | Ja |

**Antwoord**

Als het antwoord met succes is beantwoord, wordt de tekst geretourneerd die is aangetroffen in het dialoogvenster `feature_value` array. De tekst wordt gelezen en van links naar rechts van boven naar beneden geretourneerd. Dit betekent dat als &quot;I love Adobe&quot; wordt gedetecteerd, uw lading &quot;I&quot;, &quot;love&quot; en &quot;Adobe&quot; teruggeeft in afzonderlijke objecten. In het object waaraan u een `feature_name` die het woord en een `feature_value` die een betrouwbaarheidsmaatstaf voor die tekst bevat.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
