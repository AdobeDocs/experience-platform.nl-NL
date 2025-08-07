---
description: Leer hoe u de exportinstellingen voor bestanden configureert voor doelen die met Destination SDK zijn gemaakt.
title: Batchconfiguratie
exl-id: 0ffbd558-a83c-4c3d-b4fc-b6f7a23a163a
source-git-commit: 8e7356bdc5692678e46a61b538d4b6748792a423
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Batchconfiguratie {#batch-configuration}

Met de batch-configuratieopties in Destination SDK kunnen gebruikers de geëxporteerde bestandsnamen aanpassen en het exportschema naar wens configureren.

Wanneer u op dossier-gebaseerde bestemmingen door Destination SDK creeert, kunt u standaarddossier het noemen en de uitvoerschema&#39;s vormen, of u kunt gebruikers de optie geven om deze montages van de UI van Experience Platform te vormen. U kunt bijvoorbeeld gedragingen configureren, zoals:

* Specifieke informatie in de bestandsnaam opnemen, zoals gebruikers-id&#39;s, doel-id&#39;s of aangepaste informatie.
* Gebruikers toestaan de bestandsnaamgeving aan te passen vanuit de gebruikersinterface van Experience Platform.
* Configureer het exporteren van bestanden zodat deze bij ingestelde tijdintervallen kunnen optreden.
* Definieer welke opties voor het aanpassen van bestandsnamen en exportschema&#39;s gebruikers kunnen zien in de gebruikersinterface van Experience Platform.

De de configuratiemontages van de partij maken deel uit van de bestemmingsconfiguratie voor op dossier-gebaseerde bestemmingen.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in de [ configuratieopties ](../configuration-options.md) documentatie of zie de gids op hoe te [ Destination SDK gebruiken om een op dossier-gebaseerde bestemming ](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration) te vormen.

U kunt de instellingen voor de bestandsnaam en het exportschema configureren via het eindpunt van `/authoring/destinations` . Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

In dit artikel worden alle ondersteunde batch-configuratieopties beschreven die u voor uw doel kunt gebruiken en wordt aangegeven welke klanten in de gebruikersinterface van Experience Platform kunnen zien.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Nee |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Ondersteunde parameters {#supported-parameters}

De waarden die u opstelling hier wordt aangehaald in de [ stap van de de publieksuitvoer van het Programma ](../../../ui/activate-batch-profile-destinations.md#scheduling) van het op dossier-gebaseerde werkschema van de bestemmingsactivering.

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
      "ONCE",
      "WEEKLY",
      "MONTHLY"
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
| `allowMandatoryFieldSelection` | Boolean | Ingesteld op `true` zodat klanten kunnen opgeven welke profielkenmerken verplicht zijn. De standaardwaarde is `false` . Zie [ Verplicht attributen ](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) voor meer informatie. |
| `allowDedupeKeyFieldSelection` | Boolean | Ingesteld op `true` zodat klanten deduplicatietoetsen kunnen opgeven. De standaardwaarde is `false` .  Zie [ de sleutels van de Deduplicatie ](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) voor meer informatie. |
| `defaultExportMode` | Enum | Definieert de standaardmodus voor het exporteren van bestanden. Ondersteunde waarden:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> De standaardwaarde is `DAILY_FULL_EXPORT` . Zie de [ documentatie van de partijactivering ](../../../ui/activate-batch-profile-destinations.md#scheduling) voor details over dossieruitvoer die plannen. |
| `allowedExportModes` | Lijst | Hiermee definieert u de exportmodi voor bestanden die beschikbaar zijn voor klanten. Ondersteunde waarden:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lijst | Hiermee definieert u de exportfrequentie voor bestanden die beschikbaar is voor klanten. Ondersteunde waarden:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li><li>`WEEKLY`</li><li>`MONTHLY`</li></ul> |
| `defaultFrequency` | Enum | Definieert de standaard exportfrequentie voor bestanden.Ondersteunde waarden:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li><li>`WEEKLY`</li><li>`MONTHLY`</li></ul> De standaardwaarde is `DAILY` . |
| `defaultStartTime` | String | Hiermee definieert u de standaardbegintijd voor het exporteren van het bestand. Gebruikt een bestandsindeling van 24 uur. De standaardwaarde is &quot;00 :00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | String | *Vereiste*. Lijst met beschikbare bestandsnaammacro&#39;s waaruit gebruikers kunnen kiezen. Op deze manier bepaalt u welke items aan geëxporteerde bestandsnamen worden toegevoegd (gebruikers-id, naam van de organisatie, datum en tijd van export, enzovoort). Zorg er bij het instellen van `defaultFilename` voor dat dubbele macro&#39;s worden vermeden. <br><br> Gesteunde waarden: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Ongeacht de volgorde waarin u de macro&#39;s definieert, geeft de Experience Platform-interface deze altijd weer in de volgorde die hier wordt weergegeven. <br><br> Als `defaultFilename` leeg is, moet de lijst `allowedFilenameAppendOptions` minstens één macro bevatten. |
| `filenameConfig.defaultFilenameAppendOptions` | String | *Vereiste*. Vooraf geselecteerde standaardbestandsnaammacro&#39;s die gebruikers kunnen uitschakelen.<br><br> De macro&#39;s in deze lijst zijn een subset van de gedefinieerde macro&#39;s in `allowedFilenameAppendOptions` . |
| `filenameConfig.defaultFilename` | String | *Facultatief*. Hiermee definieert u de standaardbestandsnamen van macro&#39;s voor de geëxporteerde bestanden. Deze kunnen niet worden overschreven door gebruikers. <br><br> Om het even welke macro die door `allowedFilenameAppendOptions` wordt bepaald zal na de `defaultFilename` macro&#39;s worden toegevoegd. <br><br> Als `defaultFilename` leeg is, moet u minstens één macro in `allowedFilenameAppendOptions` bepalen. |
| `segmentGroupingEnabled` | Boolean | Bepaalt of het geactiveerde publiek in één enkel dossier of veelvoudige dossiers zou moeten worden uitgevoerd, die op publiek [ wordt gebaseerd fusiebeleid ](../../../../profile/merge-policies/overview.md). Ondersteunde waarden: <ul><li>`true` : exporteert één bestand per samenvoegbeleid.</li><li>`false` : exporteert één bestand per publiek, ongeacht het samenvoegbeleid. Dit is het standaardgedrag. U kunt hetzelfde resultaat bereiken door deze parameter volledig in te zetten.</li></ul> |

{style="table-layout:auto"}

## Configuratie bestandsnaam {#file-name-configuration}

Gebruik de configuratiesymbolen voor bestandsnamen om te definiëren wat de geëxporteerde bestandsnamen moeten bevatten. De macro&#39;s in de lijst hieronder beschrijven elementen die in UI in het [ worden gevonden dossier - noem configuratie ](../../../ui/activate-batch-profile-destinations.md#file-names) scherm.

>[!TIP]
> 
>U kunt het beste de macro `SEGMENT_ID` altijd opnemen in de namen van geëxporteerde bestanden. Segment-id&#39;s zijn uniek, dus het opnemen ervan in de bestandsnaam is de beste manier om ervoor te zorgen dat bestandsnamen ook uniek zijn.

| Macro | UI-label | Beschrijving | Voorbeeld |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destination] | Doelnaam in de gebruikersinterface. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Segment ID] | Unieke, door Experience Platform gegenereerde gebruikers-id | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Segment Name] | Door gebruiker gedefinieerde publieksnaam | VIP-abonnee |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Destination ID] | Unieke, door Experience Platform gegenereerde id van de doelinstantie | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Destination Name] | Door gebruiker gedefinieerde naam van de doelinstantie. | Mijn Advertising-bestemming van 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Organization Name] | Naam van de klantenorganisatie in Adobe Experience Platform. | Naam van mijn organisatie |
| `SANDBOX_NAME` | [!UICONTROL Sandbox Name] | Naam van de sandbox die de klant gebruikt. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Date and time] | `DATETIME` en `TIMESTAMP` beide definiëren wanneer het bestand is gegenereerd, maar in verschillende indelingen. <br><br><ul><li>`DATETIME` gebruikt de volgende indeling: YYYMMDD_HMMSS.</li><li>`TIMESTAMP` gebruikt de Unix-indeling van 10 cijfers. </li></ul> `DATETIME` en `TIMESTAMP` sluiten elkaar uit en kunnen niet gelijktijdig worden gebruikt. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Custom text] | Door de gebruiker gedefinieerde aangepaste tekst die in de bestandsnaam moet worden opgenomen. Kan niet worden gebruikt in `defaultFilename` . | Mijn_Aangepaste_tekst |
| `TIMESTAMP` | [!UICONTROL Date and time] | Tijdstempel van 10 cijfers van het tijdstip waarop het bestand is gegenereerd, in Unix-indeling. | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL Merge Policy ID] | Identiteitskaart van het [ samenvoegbeleid ](../../../../profile/merge-policies/overview.md) wordt gebruikt om het uitgevoerde publiek te produceren dat. Gebruik deze macro wanneer u geëxporteerde soorten publiek in bestanden groepeert op basis van het samenvoegbeleid. Gebruik deze macro samen met `segmentGroupingEnabled:true` . | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL Merge Policy Name] | De naam van het [ samenvoegbeleid ](../../../../profile/merge-policies/overview.md) wordt gebruikt om het uitgevoerde publiek te produceren dat. Gebruik deze macro wanneer u geëxporteerde soorten publiek in bestanden groepeert op basis van het samenvoegbeleid. Gebruik deze macro samen met `segmentGroupingEnabled:true` . | Mijn aangepaste samenvoegingsbeleid |

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

![ beeld UI die het scherm van de het configuratieconfiguratie van de dossiernaam met vooraf geselecteerde macro&#39;s toont ](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u dossier het noemen en de uitvoerprogramma&#39;s voor uw op dossier-gebaseerde bestemmingen kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Configuratie van klantverificatie](customer-authentication.md)
* [OAuth2-vergunning](oauth2-authorization.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)
