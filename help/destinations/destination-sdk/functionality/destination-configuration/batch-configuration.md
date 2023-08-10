---
description: Leer hoe te om de montages van de dossieruitvoer voor bestemmingen te vormen die met Destination SDK worden gebouwd.
title: Batchconfiguratie
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 3%

---


# Batchconfiguratie {#batch-configuration}

Gebruik de opties voor batchconfiguratie in Destination SDK om gebruikers toe te staan de geëxporteerde bestandsnamen aan te passen en het exportschema te configureren volgens hun voorkeur.

Wanneer u op dossier-gebaseerde bestemmingen door Destination SDK creeert, kunt u standaarddossier het noemen en de uitvoerprogramma&#39;s vormen, of u kunt gebruikers de optie geven om deze montages van het Platform UI te vormen. U kunt bijvoorbeeld gedragingen configureren, zoals:

* Specifieke informatie in de bestandsnaam opnemen, zoals gebruikers-id&#39;s, doel-id&#39;s of aangepaste informatie.
* Gebruikers toestaan de bestandsnaam aan te passen vanuit de gebruikersinterface van het Platform.
* Configureer het exporteren van bestanden zodat deze bij ingestelde tijdintervallen kunnen optreden.
* Definieer welke opties voor het aanpassen van bestandsnamen en exportschema&#39;s gebruikers kunnen zien in de gebruikersinterface van het Platform.

De de configuratiemontages van de partij maken deel uit van de bestemmingsconfiguratie voor op dossier-gebaseerde bestemmingen.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of bekijk de gids over hoe te [gebruik Destination SDK om een op dossier-gebaseerde bestemming te vormen](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

U kunt de instellingen voor de bestandsnaam en het exportschema configureren via het dialoogvenster `/authoring/destinations` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

Dit artikel beschrijft alle gesteunde opties van de partijconfiguratie die u voor uw bestemming kunt gebruiken, en toont welke klanten in Platform UI zullen zien.

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

De waarden die u hier instelt, worden weergegeven in het dialoogvenster [Het exporteren van publiek plannen](../../../ui/activate-batch-profile-destinations.md#scheduling) stap van de workflow voor activering van bestandsdoelen.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   "segmentGroupingEnabled": true
   }
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolean | Instellen op `true` zodat klanten kunnen opgeven welke profielkenmerken verplicht zijn. De standaardwaarde is `false`. Zie [Verplichte kenmerken](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) voor meer informatie . |
| `allowDedupeKeyFieldSelection` | Boolean | Instellen op `true` om klanten toe te staan deduplicatietoetsen te specificeren. De standaardwaarde is `false`.  Zie [Deduplicatietoetsen](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) voor meer informatie . |
| `defaultExportMode` | Enum | Definieert de standaardmodus voor het exporteren van bestanden. Ondersteunde waarden:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> De standaardwaarde is `DAILY_FULL_EXPORT`. Zie de [documentatie voor batchactivering](../../../ui/activate-batch-profile-destinations.md#scheduling) voor meer informatie over het plannen van het exporteren van bestanden. |
| `allowedExportModes` | Lijst | Hiermee definieert u de exportmodi voor bestanden die beschikbaar zijn voor klanten. Ondersteunde waarden:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lijst | Hiermee definieert u de exportfrequentie voor bestanden die beschikbaar is voor klanten. Ondersteunde waarden:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definieert de standaard exportfrequentie voor bestanden.Ondersteunde waarden:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> De standaardwaarde is `DAILY`. |
| `defaultStartTime` | Tekenreeks | Hiermee definieert u de standaardbegintijd voor het exporteren van het bestand. Gebruikt een bestandsindeling van 24 uur. De standaardwaarde is &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Tekenreeks | *Vereist*. Lijst met beschikbare bestandsnaammacro&#39;s waaruit gebruikers kunnen kiezen. Op deze manier bepaalt u welke items aan geëxporteerde bestandsnamen worden toegevoegd (gebruikers-id, naam van de organisatie, datum en tijd van export, enzovoort). Wanneer instellen `defaultFilename`, moet u dubbele macro&#39;s voorkomen. <br><br>Ondersteunde waarden: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Ongeacht de orde waarin u de macro&#39;s bepaalt, zal Experience Platform UI altijd hen in de hier voorgestelde orde tonen. <br><br> Indien `defaultFilename` is leeg, de `allowedFilenameAppendOptions` lijst moet ten minste één macro bevatten. |
| `filenameConfig.defaultFilenameAppendOptions` | Tekenreeks | *Vereist*. Vooraf geselecteerde standaardbestandsnaammacro&#39;s die gebruikers kunnen uitschakelen.<br><br> De macro&#39;s in deze lijst zijn een subset van de macro&#39;s die zijn gedefinieerd in `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Tekenreeks | *Optioneel*. Hiermee definieert u de standaardbestandsnamen van macro&#39;s voor de geëxporteerde bestanden. Deze kunnen niet worden overschreven door gebruikers. <br><br>Elke macro gedefinieerd door `allowedFilenameAppendOptions` wordt toegevoegd na de `defaultFilename` macro&#39;s. <br><br>Indien `defaultFilename` is leeg, moet u ten minste één macro definiëren in `allowedFilenameAppendOptions`. |
| `segmentGroupingEnabled` | Boolean | Hiermee bepaalt u of het geactiveerde publiek moet worden geëxporteerd in één bestand of in meerdere bestanden, op basis van het publiek [samenvoegingsbeleid](../../../../profile/merge-policies/overview.md). Ondersteunde waarden: <ul><li>`true`: exporteert één bestand per samenvoegbeleid.</li><li>`false`: exporteert één bestand per publiek, ongeacht het samenvoegbeleid. Dit is het standaardgedrag. U kunt hetzelfde resultaat bereiken door deze parameter volledig in te zetten.</li></ul> |

{style="table-layout:auto"}

## Configuratie bestandsnaam {#file-name-configuration}

Gebruik de configuratiesymbolen voor bestandsnamen om te definiëren wat de geëxporteerde bestandsnamen moeten bevatten. De macro&#39;s in de onderstaande tabel beschrijven de elementen in de gebruikersinterface in het dialoogvenster [bestandsnaamconfiguratie](../../../ui/activate-batch-profile-destinations.md#file-names) scherm.

>[!TIP]
> 
>Als beste praktijken moet u altijd omvatten `SEGMENT_ID` in de geëxporteerde bestandsnamen. Segment-id&#39;s zijn uniek, dus het opnemen ervan in de bestandsnaam is de beste manier om ervoor te zorgen dat bestandsnamen ook uniek zijn.

| Macro | UI-label | Beschrijving | Voorbeeld |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destination] | Doelnaam in de gebruikersinterface. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Segment ID] | Unieke, door Platforms gegenereerde gebruikers-id | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Segment Name] | Door gebruiker gedefinieerde publieksnaam | VIP abonnee |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Destination ID] | Unieke, door Platform gegenereerde id van de doelinstantie | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Destination Name] | Door gebruiker gedefinieerde naam van de doelinstantie. | Mijn advertentiebestemming van 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Organization Name] | Naam van de klantenorganisatie in Adobe Experience Platform. | Naam van mijn organisatie |
| `SANDBOX_NAME` | [!UICONTROL Sandbox Name] | Naam van de sandbox die de klant gebruikt. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Date and time] | `DATETIME` en `TIMESTAMP` beide definiëren wanneer het bestand is gegenereerd, maar in verschillende indelingen. <br><br><ul><li>`DATETIME` gebruikt de volgende indeling: YYYMMDD_HMMSS.</li><li>`TIMESTAMP` gebruikt de Unix-indeling van 10 cijfers. </li></ul> `DATETIME` en `TIMESTAMP` elkaar uitsluiten en niet gelijktijdig kunnen worden gebruikt. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Custom text] | Door de gebruiker gedefinieerde aangepaste tekst die in de bestandsnaam moet worden opgenomen. Kan niet gebruiken in `defaultFilename`. | Mijn_Aangepaste_tekst |
| `TIMESTAMP` | [!UICONTROL Date and time] | Tijdstempel van 10 cijfers van het tijdstip waarop het bestand is gegenereerd, in Unix-indeling. | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL Merge Policy ID] | De id van de [samenvoegingsbeleid](../../../../profile/merge-policies/overview.md) gebruikt om het geëxporteerde publiek te genereren. Gebruik deze macro wanneer u geëxporteerde soorten publiek in bestanden groepeert op basis van het samenvoegbeleid. Deze macro samen gebruiken met `segmentGroupingEnabled:true`. | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL Merge Policy Name] | De naam van [samenvoegingsbeleid](../../../../profile/merge-policies/overview.md) gebruikt om het geëxporteerde publiek te genereren. Gebruik deze macro wanneer u geëxporteerde soorten publiek in bestanden groepeert op basis van het samenvoegbeleid. Deze macro samen gebruiken met `segmentGroupingEnabled:true`. | Mijn aangepaste samenvoegingsbeleid |

{style="table-layout:auto"}

### Voorbeeld van configuratie bestandsnaam

In het onderstaande configuratievoorbeeld ziet u de overeenkomst tussen de configuratie die wordt gebruikt in de API-aanroep en de opties die worden weergegeven in de UI.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![UI-afbeelding die het configuratiescherm voor de bestandsnaam met vooraf geselecteerde macro&#39;s weergeeft](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u dossier het noemen en de uitvoerprogramma&#39;s voor uw op dossier-gebaseerde bestemmingen kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Configuratie van klantverificatie](customer-authentication.md)
* [OAuth2-verificatie](oauth2-authentication.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)