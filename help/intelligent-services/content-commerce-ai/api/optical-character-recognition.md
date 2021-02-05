---
keywords: OCR;aanwezigheid van tekst;optische tekenherkenning
solution: Experience Platform, Intelligent Services
title: Aanwezigheid van tekst en optische tekenherkenning
topic: Developer guide
description: In de AI API voor Inhoud en Handel kan de dienst van de Erkenning van het Karakter van de Tekst Aanwezigheid/Optische (OCR) van het Karakter erop wijzen als de tekst in een bepaalde beeld aanwezig is. Als er tekst aanwezig is, kan OCR de tekst retourneren.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
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
>`analyzer_id` bepaalt welke  [!DNL Sensei Content Framework] wordt gebruikt. Controleer of u de juiste `analyzer_id` hebt voordat u uw verzoek indient. Neem contact op met het AI beta-team van Content and Commerce om uw `analyzer_id` voor deze service te ontvangen.

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
| `analyzer_id` | De [!DNL Sensei] service-id waarin uw verzoek is geïmplementeerd. Deze id bepaalt welke van [!DNL Sensei Content Frameworks] worden gebruikt. Neem voor aangepaste services contact op met het AI-team voor Inhoud en Handel om een aangepaste id in te stellen. | Ja |
| `application-id` | De id van de toepassing die is gemaakt. | Ja |
| `data` | Een array die een JSON-object bevat waarvan elk object in de array één doorgegeven afbeelding vertegenwoordigt. Elke parameter die als onderdeel van deze array wordt doorgegeven, overschrijft de algemene parameters die buiten de array `data` zijn opgegeven. Alle overige eigenschappen die hieronder in deze tabel worden beschreven, kunnen worden overschreven vanuit `data`. | Ja |
| `language` | Taal van invoertekst. De standaardwaarde is `en`. | Nee |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline`. | Nee |
| `encoding` | De bestandsindeling van de invoerafbeelding. Momenteel kunnen alleen JPEG- en PNG-afbeeldingen worden verwerkt. De standaardwaarde voor deze eigenschap is `jpeg`. | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. Gebruik de waarde `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). Gebruik de waarde `0` om alle resultaten te retourneren. Wanneer gebruikt in combinatie met `threshold`, is het aantal teruggekeerde resultaten het laagste van één van beide vastgestelde grenzen. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. Voor deze eigenschap is een geldig JSON-object vereist. | Nee |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als dit niet wordt overgegaan, wordt een auto-geproduceerde identiteitskaart toegewezen. | Nee |
| `content` | De inhoud kan een Raw-afbeelding zijn (inline-inhoudstype). <br> Als de inhoud een bestand is op S3 (inhoudstype s3-bucket), geeft u de ondertekende URL door. | Ja |

**Antwoord**

Een succesvol antwoord retourneert de tekst die is gedetecteerd in de `feature_value`-array. De tekst wordt gelezen en van links naar rechts van boven naar beneden geretourneerd. Dit betekent dat als &quot;I love Adobe&quot; wordt gedetecteerd, uw lading &quot;I&quot;, &quot;love&quot; en &quot;Adobe&quot; teruggeeft in afzonderlijke objecten. In het object krijgt u een `feature_name` dat het woord en een `feature_value` bevat die een betrouwbaarheidsmetrische waarde voor die tekst bevat.

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
