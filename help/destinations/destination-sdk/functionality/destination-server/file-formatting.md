---
description: Leer hoe te om dossier het formatteren opties voor op dossier-gebaseerde bestemmingen te vormen die met Adobe Experience Platform Destination SDK, via het `/bestemming-servers' eindpunt worden gebouwd.
title: Configuratie bestandsindeling
source-git-commit: 511e02f92b7016a7f07dd3808b39594da9438d15
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 2%

---


# Configuratie bestandsindeling

Destination SDK ondersteunt een flexibele reeks functies die u kunt configureren op basis van uw integratiebehoeften. De ondersteuning voor [!DNL CSV] bestandsindeling.

Wanneer u op een bestand gebaseerde doelen maakt via Destination SDK, kunt u definiëren hoe de geëxporteerde CSV-bestanden moeten worden opgemaakt. U kunt vele opmaakopties aanpassen, zoals, maar niet beperkt tot:

* Of het CSV-bestand een header moet bevatten;
* Welk karakter voor het citeren van waarden te gebruiken;
* Hoe zouden lege waarden eruit moeten zien.

Afhankelijk van uw bestemmingsconfiguratie, zullen de gebruikers bepaalde opties in UI zien wanneer het verbinden met een op dossier-gebaseerd doel. U kunt zien hoe deze opties er in het dialoogvenster [opties voor bestandsindeling voor op bestanden gebaseerde doelen](../../../ui/batch-destinations-file-formatting-options.md) documentatie.


De het formatteren van het dossier montages maken deel uit van de configuratie van de bestemmingsserver voor op dossier-gebaseerde bestemmingen.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of raadpleeg de gids over hoe te [gebruik Destination SDK om een op dossier-gebaseerde bestemming te vormen](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

U kunt de opties voor de bestandsindeling configureren via het dialoogvenster `/authoring/destination-servers` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelserverconfiguratie maken](../../authoring-api/destination-server/create-destination-server.md)
* [Een doelserverconfiguratie bijwerken](../../authoring-api/destination-server/update-destination-server.md)

In deze pagina worden alle ondersteunde instellingen voor bestandsindeling voor geëxporteerde bestanden beschreven `CSV` bestanden.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Nee |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Ondersteunde parameters {#supported-parameters}

U kunt verschillende eigenschappen van de geëxporteerde bestanden aanpassen aan de vereisten van het bestandsontvangstsysteem van uw bestemming, zodat u de bestanden die u van het Experience Platform hebt ontvangen optimaal kunt lezen en interpreteren.

>[!NOTE]
>
>CSV-opties worden alleen ondersteund bij het exporteren van CSV-bestanden. De `fileConfigurations` is niet verplicht bij het instellen van een nieuwe doelserver. Als u geen waarden doorgeeft in de API-aanroep voor de CSV-opties, worden de standaardwaarden van de [referentietabel verderop](#file-formatting-reference-and-example) wordt gebruikt.


## CSV-opties waarbij gebruikers geen configuratieopties kunnen selecteren {#file-configuration-templating-none}

In het onderstaande configuratievoorbeeld zijn alle CSV-opties vooraf gedefinieerd. De exportinstellingen die zijn gedefinieerd in de `csvOptions` parameters zijn definitief en gebruikers kunnen deze niet wijzigen.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

## CSV-opties waar gebruikers configuratieopties kunnen selecteren {#file-configuration-templating-pebble}

In het onderstaande configuratievoorbeeld zijn geen van de CSV-opties vooraf gedefinieerd. De `value` in elk van de `csvOptions` parameters worden gevormd op een overeenkomstig gebied van klantengegevens door `/destinations` eindpunt (bijvoorbeeld [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) voor de `quote` bestandsindeling) en gebruikers kunnen de gebruikersinterface van het Experience Platform gebruiken om een keuze te maken uit de verschillende opties die u configureert in het desbetreffende gegevensveld van de klant. U kunt zien hoe deze opties er in het dialoogvenster [opties voor bestandsindeling voor op bestanden gebaseerde doelen](../../../ui/batch-destinations-file-formatting-options.md) documentatie.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      },
      "maxFileRowCount":5000000
   }
}
```

## Volledige verwijzing en voorbeelden voor ondersteunde opties voor bestandsindeling {#file-formatting-reference-and-example}

>[!TIP]
>
>De hieronder beschreven opmaakopties voor CSV-bestanden worden ook beschreven in de [Handleiding voor Apache Spark voor CSV-bestanden](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). De onderstaande beschrijvingen zijn ontleend aan de gids voor Apache Spark.

Hieronder ziet u een volledige verwijzing naar alle beschikbare opmaakopties voor bestanden in Destination SDK, naast uitvoervoorbeelden voor elke optie.

| Veld | Vereist/optioneel | Beschrijving | Standaardwaarde | Voorbeeld van uitvoer 1 | Voorbeeld van uitvoer 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Vereist | Voor elke optie voor bestandsindeling die u configureert, moet u de parameter toevoegen `templatingStrategy`, die twee waarden kunnen hebben: <br><ul><li>`NONE`: gebruik deze waarde als u niet van plan bent om gebruikers toe te staan tussen verschillende waarden voor een configuratie te selecteren. Zie [deze configuratie](#file-configuration-templating-none) voor een voorbeeld waarin de opties voor bestandsindeling zijn gecorrigeerd.</li><li>`PEBBLE_V1`: gebruik deze waarde als u wilt toestaan dat gebruikers een keuze kunnen maken tussen verschillende waarden voor een configuratie. In dit geval moet u ook een corresponderend gegevensveld voor de klant instellen in het dialoogvenster `/destination` eindpuntconfiguratie, aan oppervlakte de diverse opties aan gebruikers in UI. Zie [deze configuratie](#file-configuration-templating-pebble) voor een voorbeeld waarin gebruikers verschillende waarden voor opties voor bestandsindeling kunnen selecteren.</li></ul> | - | - | - |
| `compression.value` | Optioneel | Compressiecodec die moet worden gebruikt bij het opslaan van gegevens naar een bestand. Ondersteunde waarden: `none`, `bzip2`, `gzip`, `lz4`, en `snappy`. | `none` | - | - |
| `fileType.value` | Optioneel | Hiermee geeft u de indeling voor het uitvoerbestand op. Ondersteunde waarden: `csv`, `parquet`, en `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken van geciteerde waarden, waarbij het scheidingsteken deel kan uitmaken van de waarde. | `null` | Voorbeeld van standaardwaarde: `quote.value: "u0000"` —> `male,NULJohn,LastNameNUL` | Aangepast voorbeeld: `quote.value: "\""` —> `male,"John,LastName"` |
| `csvOptions.quoteAll.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of alle waarden altijd tussen aanhalingstekens moeten worden geplaatst. Standaard worden alleen escape-waarden gebruikt die een aanhalingsteken bevatten. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u een scheidingsteken in voor elk veld en elke waarde. Dit scheidingsteken kan een of meer tekens bevatten. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken voor aanhalingstekens binnen een reeds geciteerde waarde. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of waarden met aanhalingstekens altijd tussen aanhalingstekens moeten worden geplaatst. Standaard worden alle waarden met een aanhalingsteken verwijderd. | `true` | - | - |
| `csvOptions.header.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of de namen van kolommen als de eerste regel in het geëxporteerde bestand moeten worden geschreven. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee wordt aangegeven of witruimten vóór elkaar worden bijgesneden op basis van waarden. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of volgwitruimten moeten worden bijgesneden op basis van waarden. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeksrepresentatie in van een waarde null. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft de datumnotatie aan. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeks in die een tijdstempelindeling aangeeft. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt één teken in dat wordt gebruikt voor escape voor het aanhalingsteken. | `\` wanneer de escape- en aanhalingstekens verschillend zijn. `\0` wanneer de escape- en aanhalingsteken hetzelfde zijn. | - | - |
| `csvOptions.emptyValue.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeksrepresentatie in van een lege waarde. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | Optioneel | Hiermee geeft u het maximale aantal rijen per geëxporteerd bestand op tussen 1.000.000 en 10.000.000 rijen. | 5,000,000 |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe het dossier formatteren in een configuratie van de bestemmingsserver werkt, en hoe u het kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere componenten van de doelserver:

* [Server specs voor bestemmingen die met Destination SDK worden gecreeerd](server-specs.md)
* [Sjabloonspecificaties](templating-specs.md)
* [Berichtindeling](message-format.md)