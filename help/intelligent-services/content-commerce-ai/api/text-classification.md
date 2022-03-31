---
keywords: tekstclassificatie;Tekstclassificatie
solution: Experience Platform
title: Tekstclassificatie in de API voor inhoud en handel
topic-legacy: Developer guide
description: Wanneer de tekstclassificatiedienst een tekstfragment geeft, kan deze in een of meer labels indelen. De classificatie kan single-label, multi-label, of hiërarchisch zijn.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# Tekstclassificatie

>[!NOTE]
>
>AI van de Inhoud en van de Handel is in bèta. De documentatie kan worden gewijzigd.

Wanneer de tekstclassificatiedienst een tekstfragment geeft, kan deze in een of meer labels indelen. De classificatie kan single-label, multi-label, of hiërarchisch zijn.

**API-indeling**

```http
POST /services/v1/predict
```

**Verzoek**

In het volgende verzoek wordt tekst uit een fragment geclassificeerd op basis van de invoerparameters die in de payload worden opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

>[!CAUTION]
>
>`analyzer_id` bepaalt welke [!DNL Sensei Content Framework] wordt gebruikt. Controleer of u de juiste `analyzer_id` voordat u uw verzoek indient. Neem contact op met het AI bètateam voor Inhoud en Handel om uw `analyzer_id` voor deze service.

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
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| Eigenschap | Beschrijving | Verplicht |
| --- | --- | --- |
| `analyzer_id` | De [!DNL Sensei] service-id waarin uw verzoek is geïmplementeerd. Deze id bepaalt welke van de [!DNL Sensei Content Frameworks] worden gebruikt. Neem voor aangepaste services contact op met het AI-team voor Inhoud en Handel om een aangepaste id in te stellen. | Ja |
| `application-id` | De id van de toepassing die is gemaakt. | Ja |
| `data` | Een array die een JSON-object bevat met elk object in de array die een document vertegenwoordigt. Alle parameters die als onderdeel van deze array worden doorgegeven, overschrijven de algemene parameters die buiten de `data` array. Alle resterende eigenschappen die hieronder in deze tabel worden beschreven, kunnen van binnenuit worden overschreven `data`. | Ja |
| `language` | Taal van invoertekst. De standaardwaarde is `en`. | Nee |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline`. | Nee |
| `encoding` | De coderingsindeling van invoertekst. Dit kan `utf-8` of `utf-16`. De standaardwaarde voor deze eigenschap is `utf-8`. | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. De waarde gebruiken `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). De waarde gebruiken `0` om alle resultaten te retourneren. Indien gebruikt in combinatie met `threshold`, is het aantal geretourneerde resultaten het laagste van de twee ingestelde limieten. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. Voor deze eigenschap is een geldig JSON-object vereist. | Nee |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als deze waarde niet wordt doorgegeven, wordt een automatisch gegenereerde id toegewezen. | Nee |
| `content` | De inhoud die wordt gebruikt door de tekstclassificatiedienst. De inhoud kan onbewerkte tekst zijn (&#39;inline&#39;-inhoudstype). <br> Als de inhoud een bestand is op S3 (&#39;s3-bucket&#39; inhoudstype), geeft u de ondertekende URL door. | Ja |

**Antwoord**

Een geslaagde reactie retourneert de geclassificeerde tekst in een responsarray.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
