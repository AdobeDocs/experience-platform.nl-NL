---
keywords: tekstclassificatie;Tekstclassificatie
solution: Experience Platform
title: Tekstclassificatie in de API voor inhoud en Commerce
description: Als de tekstclassificatiedienst een tekstfragment opgeeft, kan deze in een of meer labels indelen. De classificatie kan single-label, multi-label, of hiërarchisch zijn.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Tekstclassificatie

>[!NOTE]
>
>Inhoud en Commerce AI is in bèta. De documentatie kan worden gewijzigd.

Als de tekstclassificatiedienst een tekstfragment opgeeft, kan deze in een of meer labels indelen. De classificatie kan single-label, multi-label, of hiërarchisch zijn.

**API formaat**

```http
POST /services/v1/predict
```

**Verzoek**

In het volgende verzoek wordt tekst uit een fragment geclassificeerd op basis van de invoerparameters die in de payload worden opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

>[!CAUTION]
>
>`analyzer_id` bepaalt welke [!DNL Sensei Content Framework] wordt gebruikt. Controleer of u de juiste `analyzer_id` hebt voordat u een aanvraag indient. Neem contact op met het team voor Inhoud en Commerce AI bèta om uw `analyzer_id` voor deze service te ontvangen.

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
| `analyzer_id` | De service-id van [!DNL Sensei] waarin uw verzoek wordt geïmplementeerd. Deze id bepaalt welke van de [!DNL Sensei Content Frameworks] worden gebruikt. Neem voor aangepaste services contact op met het AI-team van Content en Commerce om een aangepaste id in te stellen. | Ja |
| `application-id` | De id van de gemaakte toepassing. | Ja |
| `data` | Een array die een JSON-object bevat met elk object in de array die een document vertegenwoordigt. Elke parameter die als onderdeel van deze array wordt doorgegeven, overschrijft de algemene parameters die buiten de array `data` zijn opgegeven. Alle overige eigenschappen die hieronder in deze tabel worden beschreven, kunnen worden overschreven vanuit `data` . | Ja |
| `language` | Taal van invoertekst. De standaardwaarde is `en` . | Nee |
| `content-type` | Gebruikt om erop te wijzen of de input deel van het verzoeklichaam of een ondertekende url voor een S3 emmertje uitmaakt. De standaardwaarde voor deze eigenschap is `inline` . | Nee |
| `encoding` | De coderingsindeling van invoertekst. Dit kan `utf-8` of `utf-16` zijn. De standaardwaarde voor deze eigenschap is `utf-8` . | Nee |
| `threshold` | De drempel van de score (0 tot en met 1) waarboven de resultaten moeten worden geretourneerd. Gebruik de waarde `0` om alle resultaten te retourneren. De standaardwaarde voor deze eigenschap is `0` . | Nee |
| `top-N` | Het aantal resultaten dat moet worden geretourneerd (mag geen negatief geheel getal zijn). Gebruik de waarde `0` om alle resultaten te retourneren. Wanneer het samen met `threshold` wordt gebruikt, is het aantal geretourneerde resultaten het laagste van beide limietwaarden. De standaardwaarde voor deze eigenschap is `0` . | Nee |
| `custom` | Aangepaste parameters die moeten worden doorgegeven. Voor deze eigenschap is een geldig JSON-object vereist. | Nee |
| `content-id` | De unieke id voor het gegevenselement dat in de reactie wordt geretourneerd. Als deze waarde niet wordt doorgegeven, wordt een automatisch gegenereerde id toegewezen. | Nee |
| `content` | De inhoud die wordt gebruikt door de tekstclassificatiedienst. De inhoud kan onbewerkte tekst zijn (&#39;inline&#39;-inhoudstype). <br> Als de inhoud een bestand is op S3 (inhoudstype s3-bucket), geeft u de ondertekende URL door. | Ja |

**Reactie**

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
