---
keywords: Experience Platform;aan de slag;inhoud;inhoud labelen;kleur labelen;kleur extraheren;
solution: Experience Platform
title: Kleurlabels in de API voor inhoudtags
description: Als u een afbeelding opgeeft met kleurcodes, kunt u het histogram van pixelkleuren berekenen en deze sorteren op dominante kleuren in emmers.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 2%

---

# Kleurlabels

Wanneer u een afbeelding opgeeft, kan de service kleurlabels een histogram met pixelkleuren berekenen en deze sorteren op dominante kleuren in emmers. De kleuren in de afbeeldingspixels worden in 40 overheersende kleuren gedicht die representatief zijn voor het kleurenspectrum. Vervolgens wordt een histogram met kleurwaarden berekend tussen deze 40 kleuren. De dienst heeft twee varianten:

**Kleurlabels (volledige afbeelding)**

Met deze methode extraheert u een kleurenhistogram over de hele afbeelding.

**Kleurlabels (met masker)**

Deze methode gebruikt een op diepleren gebaseerde voorgrondextractor om objecten op de voorgrond te identificeren. Het model is opgeleid voor een catalogus met e-commerceafbeeldingen. Nadat het voorgrondobject is geëxtraheerd, wordt een histogram berekend over de dominante kleuren, zoals eerder beschreven.

De volgende afbeelding is gebruikt in het voorbeeld dat in dit document wordt weergegeven:

![testafbeelding](../images/QQAsset1.jpg)

**API-indeling**

```http
POST /services/v2/predict
```

**Verzoek**

In het volgende voorbeeldverzoek wordt de methode full-image gebruikt voor kleurlabeling.

In het volgende verzoek worden kleuren uit een afbeelding geëxtraheerd op basis van de invoerparameters die in de lading zijn opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| Eigenschap | Beschrijving | Verplicht |
| --- | --- | --- |
| `application-id` | De id van de toepassing die u hebt gemaakt. | Ja |
| `documents` | Een lijst met JSON-elementen waarbij elk item in de lijst één document vertegenwoordigt. | Ja |
| `top_n` | Het aantal resultaten dat moet worden geretourneerd (dit kan geen negatief geheel getal zijn). De waarde gebruiken `0` om alle resultaten te retourneren. Indien gebruikt in combinatie met `threshold`, is het aantal geretourneerde resultaten het laagste van de twee ingestelde limieten. De standaardwaarde voor deze eigenschap is `0`. | Nee |
| `min_coverage` | Drempel van dekking waarboven de resultaten moeten worden geretourneerd. Sluit de parameter uit om alle resultaten te retourneren. | Nee |
| `resize_image` | Geeft aan of de grootte van de invoerafbeelding moet worden gewijzigd. Standaard wordt de grootte van de afbeeldingen gewijzigd in 320*320 pixels voordat kleurlabels worden uitgevoerd. Voor het zuiveren doeleinden kunnen wij de code toestaan om op volledig-beeld te lopen, door dit aan Vals te plaatsen. | Nee |
| `enable_mask` | Schakelt kleurlabeling binnen masker in of uit. | Nee |

| Naam | Datatype | Vereist | Standaard | Waarden | Beschrijving |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | Voorgetekende URL van het document waaruit de belangrijkste zinnen moeten worden geëxtraheerd. |
| `sensei:repoType` | string | - | - | HTTPS | Type repo waar de afbeelding wordt opgeslagen. |
| `sensei:multipart_field_name` | string | - | - | - | Gebruik dit wanneer u een afbeeldingsbestand doorgeeft als een meerdelig argument in plaats van vooraf ondertekende URL&#39;s te gebruiken. |
| `dc:format` | string | Ja | - | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | De codering van afbeeldingen wordt gecontroleerd aan de hand van toegestane invoercoderingstypen voordat deze wordt verwerkt. |

**Antwoord**

Wanneer de reactie is gelukt, worden de details van de geëxtraheerde kleuren geretourneerd. Elke kleur wordt vertegenwoordigd door een `feature_value` key, die de volgende informatie bevat:

- Een kleurnaam
- Het percentage waarmee deze kleur wordt weergegeven in verhouding tot de afbeelding
- De RGB-waarde van de kleur

In het eerste onderstaande voorbeeldobject wordt de `feature_value` van `Mud_Green,0.069,102,72,95` betekent dat de gevonden kleur moddergroen is, moddergroen wordt aangetroffen in 6,9% van de afbeelding en de RGB-waarde 102,72,95 is.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
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
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
