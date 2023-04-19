---
keywords: Experience Platform;aan de slag;inhoud;inhoud labelen;kleur labelen;kleur extraheren;
solution: Experience Platform
title: Kleurlabels in de API voor inhoudtags
description: Als u een afbeelding opgeeft met kleurcodes, kunt u het histogram van pixelkleuren berekenen en deze sorteren op dominante kleuren in emmers.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e6ea347252b898f73c2bc495b0324361ee6cae9b
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 2%

---

# Kleurlabels

Wanneer u een afbeelding opgeeft, kan de service kleurlabels een histogram met pixelkleuren berekenen en deze sorteren op dominante kleuren in emmers. De kleuren in de afbeeldingspixels worden in 40 overheersende kleuren gedicht die representatief zijn voor het kleurenspectrum. Vervolgens wordt een histogram met kleurwaarden berekend tussen deze 40 kleuren. De dienst heeft twee varianten:

**Kleurlabels (volledige afbeelding)**

Met deze methode extraheert u een kleurenhistogram over de hele afbeelding.

**Kleurlabels (met masker)**

Deze methode gebruikt een op diepleren gebaseerde voorgrondextractor om objecten op de voorgrond te identificeren. Nadat de voorgrondobjecten zijn geëxtraheerd, wordt een histogram samen met de hele afbeelding berekend over de dominante kleuren voor zowel de voor- als de achtergrondgebieden.

**Toonextractie**

Naast de hierboven vermelde varianten, kunt u de dienst vormen om een histogram van tonen voor terug te winnen:

- De algemene afbeelding (bij gebruik van de volledige afbeeldingsvariant)
- De algemene afbeelding en de voor- en achtergrondgebieden (wanneer de variant wordt gebruikt met maskering)

De volgende afbeelding is gebruikt in het voorbeeld dat in dit document wordt weergegeven:

![testafbeelding](../images/QQAsset1.jpg)

**API-indeling**

```http
POST /services/v2/predict
```

**Verzoek - volledige afbeeldingsvariant**

In het volgende voorbeeldverzoek wordt de methode full-image gebruikt voor kleurlabeling en worden kleuren uit een afbeelding geëxtraheerd op basis van de invoerparameters die in de payload zijn opgegeven. Zie de tabel onder de voorbeeldlading voor meer informatie over de getoonde inputparameters.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**Reactie - volledige afbeeldingsvariant**

Wanneer de reactie is gelukt, worden de details van de geëxtraheerde kleuren geretourneerd. Elke kleur wordt vertegenwoordigd door een `feature_value` key, die de volgende informatie bevat:

- Een kleurnaam
- Het percentage waarmee deze kleur wordt weergegeven in verhouding tot de afbeelding
- De RGB-waarde van de kleur

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`De gevonden kleur is wit, die wordt aangetroffen in 58,34% van de afbeelding, en heeft een gemiddelde RGB-waarde van 254, 254, 243.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

Het resultaat hier heeft kleur die is uitgepakt voor het &quot;algemene&quot; afbeeldingsgebied.

**Verzoek - variant gemaskeerde afbeelding**

In het volgende voorbeeldverzoek wordt de maskeringsmethode gebruikt voor kleurlabeling. We maken dit mogelijk door de `enable_mask` parameter to `true` in het verzoek.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>Opmerking: Daarnaast stellen we ook de `retrieve_tone` parameter to `true` in bovengenoemd verzoek. Op deze manier kunnen we een histogram ophalen voor de distributie van kleurtinten over warme, neutrale en koele tonen in de algemene, voor- en achtergrondgebieden van de afbeelding.

**Reactie - variant gemaskeerde afbeelding**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

Naast de kleuren uit de hele afbeelding, kunt u nu ook kleuren uit de voor- en achtergrondgebieden zien. Omdat we het ophalen van kleurtonen voor elk van de bovenstaande gebieden mogelijk maken, kunnen we ook een histogram met kleurtonen ophalen.

**Invoerparameters**

| Naam | Datatype | Vereist | Standaard | Waarden | Beschrijving |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Ja | - | Zie hieronder | Lijst met json-elementen waarbij elk item in de lijst één document vertegenwoordigt. |
| `top_n` | getal | Nee | 0 | Niet-negatief geheel getal | Aantal resultaten dat moet worden geretourneerd. 0, om alle resultaten te retourneren. Wanneer gebruikt in combinatie met een drempelwaarde, zal het aantal geretourneerde resultaten kleiner zijn dan een van beide limieten. |
| `min_coverage` | getal | Nee | 0.05 | Reëel nummer | Drempel van dekking waarboven de resultaten moeten worden geretourneerd. Sluit parameter uit om alle resultaten te retourneren. |
| `resize_image` | getal | Nee | Waar | Waar/Onwaar | Of de invoerafbeelding moet worden vergroot of verkleind. Standaard wordt de grootte van de afbeeldingen gewijzigd in 320*320 pixels voordat kleurextractie wordt uitgevoerd. Voor het zuiveren doeleinden kunnen wij de code toestaan om op volledig-beeld te lopen, door dit aan Vals te plaatsen. |
| `enable_mask` | getal | Nee | Onwaar | Waar/Onwaar | Schakelt kleurextractie in/uit |
| `retrieve_tone` | getal | Nee | Onwaar | Waar/Onwaar | Schakelt toonextractie in/uit |

**Object Document**

| Naam | Datatype | Vereist | Standaard | Waarden | Beschrijving |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | Voorgetekende URL van het document waaruit de belangrijkste zinnen moeten worden geëxtraheerd. |
| `sensei:repoType` | string | - | - | HTTPS | Type repo waar het document wordt opgeslagen. |
| `sensei:multipart_field_name` | string | - | - | - | Gebruik deze optie wanneer u het document doorgeeft als een meerdelig argument in plaats van vooraf ondertekende URL&#39;s te gebruiken. |
| `dc:format` | string | Ja | - | &quot;text/plain&quot;,<br>&quot;application/pdf&quot;,<br>&quot;text/pdf&quot;,<br>&quot;text/html&quot;,<br>&quot;text/rtf&quot;,<br>&quot;application/rtf&quot;,<br>&quot;application/msword&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.wordprocessingml.document&quot;,<br>&quot;application/mspowerpoint&quot;,<br>&quot;application/vnd.ms-powerpoint&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.presentationml.presentation&quot; | Documentcodering wordt gecontroleerd op basis van toegestane invoercoderingstypen voordat deze worden verwerkt. |