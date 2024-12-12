---
description: Leer hoe u opties voor bestandsindeling kunt configureren wanneer u gegevens activeert naar bestandsbestemmingen
title: Opties voor bestandsindeling configureren voor op bestanden gebaseerde doelen
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 4dd6e8685ff5cc61342b20e971216416918b95da
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 0%

---

# Opties voor bestandsindeling configureren voor op bestanden gebaseerde doelen

>[!IMPORTANT]
> 
>De opmaakopties voor bestanden die in dit document worden beschreven, zijn momenteel alleen beschikbaar voor CSV-bestanden.

De optie om diverse dossier te vormen formatterend opties voor de uitgevoerde dossiers is beschikbaar aan u wanneer u [ ](/help/destinations/ui/connect-destination.md) met een op dossier-gebaseerde bestemming, zoals [ Amazon S3 ](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [ Azure Blob ](/help/destinations/catalog/cloud-storage/azure-blob.md#connect) verbindt, of [ SFTP ](/help/destinations/catalog/cloud-storage/sftp.md#connect).

U kunt verschillende opmaakopties voor geëxporteerde bestanden configureren met de interface van het Experience Platform. U kunt verschillende eigenschappen van de geëxporteerde bestanden aanpassen aan de vereisten van het systeem voor het ontvangen van bestanden aan uw zijde, zodat u de bestanden die u van het Experience Platform hebt ontvangen, optimaal kunt lezen en interpreteren.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuratie van bestandsindeling voor CSV-bestanden {#file-configuration}

Om het dossier te tonen die opties formatteren, begin [ met bestemmings ](/help/destinations/ui/connect-destination.md) werkschema verbinden. Selecteer **Type van Gegevens: Segmenten** en **het type van Dossier: CSV** om de dossier te tonen formatterend montages beschikbaar voor de uitgevoerde `CSV` dossiers.

>[!IMPORTANT]
>
>Mogelijk zijn niet al deze opties beschikbaar voor de bestemming waarmee u verbinding maakt. Het is aan de bestemmingsontwikkelaar om te bepalen welke dossier het formatteren opties zij in hun bestemming willen steunen. De bestemmingsontwikkelaar kan bepalen welke opties beschikbaar zijn wanneer het verbinden met de bestemming. De vereiste opties zijn duidelijk met een asterisk in de UI van het Experience Platform.
> 
>De Adobe-gebouwde bestemmingen van de cloudopslag - [ Amazon S3 ](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ Azure Blob ](/help/destinations/catalog/cloud-storage/azure-blob.md), [ Azure Gegevens Meer Gen2 van de Opslag ](/help/destinations/catalog/cloud-storage/adls-gen2.md), [ Gegevens Landing Zone ](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [ de Opslag van de Wolk van Google ](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [ SFTP ](/help/destinations/catalog/cloud-storage/sftp.md) - steunt momenteel slechts de zes hieronder benadrukte opties CSV.

![ Beeld dat enkele beschikbare dossier het formatteren opties toont.](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Scheidingsteken {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Scheidingsteken"
>abstract="Gebruik dit besturingselement om een scheidingsteken in te stellen voor elk veld en elke waarde. Raadpleeg de documentatie voor voorbeelden van elke selectie."

Met dit besturingselement kunt u een scheidingsteken instellen voor elk veld en elke waarde in de geëxporteerde CSV-bestanden. Beschikbare opties zijn:

* Colon `(:)`
* Komma `(,)`
* Pipe `(|)`
* Puntkomma `(;)`
* Tab `(\t)`

#### Voorbeelden

Bekijk de voorbeelden hieronder van de inhoud in de geëxporteerde CSV-bestanden met elke selectie in de gebruikersinterface.

* Voorbeeld van uitvoer met **[!UICONTROL Colon `(:)`]** geselecteerd: `male:John:Doe`
* Voorbeeld van uitvoer met **[!UICONTROL Comma `(,)`]** geselecteerd: `male,John,Doe`
* Voorbeeld van uitvoer met **[!UICONTROL Pipe `(|)`]** geselecteerd: `male|John|Doe`
* Voorbeeld van uitvoer met **[!UICONTROL Semicolon `(;)`]** geselecteerd: `male;John;Doe`
* Voorbeeld van uitvoer met **[!UICONTROL Tab `(\t)`]** geselecteerd: `male \t John \t Doe`

### Aanhalingsteken {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Aanhalingsteken"
>abstract="Gebruik deze optie als u dubbele aanhalingstekens wilt verwijderen uit geëxporteerde tekenreeksen. Raadpleeg de documentatie voor voorbeelden van elke selectie."

Met deze optie kunt u bepalen of dubbele aanhalingstekens moeten worden verwijderd of binnen geëxporteerde tekenreeksen moeten worden bewaard.

De beschikbare opties zijn:

* **[!UICONTROL Null Character (\0000)]**. Gebruik deze optie om dubbele aanhalingstekens te verwijderen uit geëxporteerde CSV-bestanden.
* **[!UICONTROL Double Quotes (")]**. Gebruik deze optie als de tekenreekswaarden een scheidingsteken of dubbele aanhalingstekens bevatten. Met deze optie kunt u de scheidingstekens of dubbele aanhalingstekens behouden in geëxporteerde CSV-bestanden, zodat u precies kunt zien welke waarde overeenkomt met welk veld.

#### Voorbeelden

Neem bijvoorbeeld de invoerwaarde `Anna,"Doe,John"` .

Bekijk de voorbeelden hieronder van de inhoud van geëxporteerde CSV-bestanden met elk van de selecties in de gebruikersinterface.

* Voorbeeld van uitvoer met **[!UICONTROL Null Character (\0000)]** geselecteerd: `Anna,Doe,John`
* Voorbeeld van uitvoer met **[!UICONTROL Double Quotes (")]** geselecteerd: `Anna,"Doe,John"`

### Escape-teken {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Escape-teken"
>abstract="Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken voor aanhalingstekens binnen een reeds geciteerde waarde. Raadpleeg de documentatie voor voorbeelden van elke selectie."

Gebruik deze optie om één teken in te stellen voor het omzeilen van aanhalingstekens binnen een reeds geciteerde waarde. Deze optie is bijvoorbeeld handig wanneer u een tekenreeks tussen dubbele aanhalingstekens plaatst, waarbij een deel van de tekenreeks al tussen dubbele aanhalingstekens staat. Met deze optie bepaalt u welk teken de binnenste dubbele aanhalingstekens moet vervangen. Beschikbare opties zijn:

* Achterste schuine streep `(\)`
* Enkel aanhalingsteken `(')`

#### Voorbeelden

Bekijk de voorbeelden hieronder van de inhoud van geëxporteerde CSV-bestanden met elk van de selecties in de gebruikersinterface.

* Voorbeeld van uitvoer met **[!UICONTROL Back slash `(\)`]** geselecteerd: `"Test,\"John\",LastName"`
* Voorbeeld van uitvoer met **[!UICONTROL Single quote `(')`]** geselecteerd: `"Test,'"John'",LastName"`

### Uitvoer van lege waarde {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Uitvoer van lege waarde"
>abstract="Gebruik deze optie om in te stellen hoe lege waarden moeten worden weergegeven in de geëxporteerde CSV-bestanden. Raadpleeg de documentatie voor voorbeelden van elke selectie."

Gebruik dit besturingselement om de tekenreeksrepresentatie van een lege waarde in te stellen. Met deze optie bepaalt u hoe lege waarden worden weergegeven in uw geëxporteerde CSV-bestanden. Beschikbare opties zijn:

* **[!UICONTROL Null (null)]**
* **Leeg Koord in Dubbele Citaten (&quot;&quot;)**
* **[!UICONTROL Empty string]**

#### Voorbeelden

Bekijk de voorbeelden hieronder van de inhoud van geëxporteerde CSV-bestanden met elk van de selecties in de gebruikersinterface.

* Voorbeeld van uitvoer met **[!UICONTROL null]** geselecteerd: `male,NULL,TestLastName` . In dit geval transformeert Experience Platform de lege waarde in een null-waarde.
* Voorbeeld uitvoer met **&quot;&quot;** selected: `male,"",TestLastName`. In dit geval transformeert Experience Platform de lege waarde in twee dubbele aanhalingstekens.
* Voorbeeld van uitvoer met **[!UICONTROL Empty string]** geselecteerd: `male,,TestLastName` . In dit geval behoudt het Experience Platform de lege waarde en exporteert het zoals het is (zonder dubbele aanhalingstekens).

>[!TIP]
>
>Het verschil tussen de lege uitvoer van waarden en de null-waarde die in de onderstaande sectie wordt uitgevoerd, is dat een lege waarde een werkelijke waarde heeft die leeg is. De waarde NULL heeft helemaal geen waarde. Beschouw de lege waarde als een leeg glas op de tafel en de null-waarde als een geheel niet-glazen glas op de tafel.

### Uitvoer van waarde Null {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Uitvoer van waarde Null"
>abstract="Gebruik dit besturingselement om de tekenreeksrepresentatie van een null-waarde in te stellen in de geëxporteerde bestanden. Raadpleeg de documentatie voor voorbeelden van elke selectie."

Gebruik dit besturingselement om de tekenreeksrepresentatie van een null-waarde in te stellen in de geëxporteerde bestanden. Met deze optie bepaalt u hoe null-waarden worden weergegeven in uw geëxporteerde CSV-bestanden. Beschikbare opties zijn:

* **[!UICONTROL Null (null)]**
* **Leeg Koord in Dubbele Citaten (&quot;&quot;)**
* **[!UICONTROL Empty string]**

#### Voorbeelden

Bekijk de voorbeelden hieronder van de inhoud van geëxporteerde CSV-bestanden met elk van de selecties in de gebruikersinterface.

* Voorbeeld van uitvoer met **[!UICONTROL null]** geselecteerd: `male,NULL,TestLastName` . In dit geval vindt geen transformatie plaats en bevat het CSV-bestand de null-waarde.
* Voorbeeld uitvoer met **&quot;&quot;** selected: `male,"",TestLastName`. In dit geval vervangt Experience Platform de null-waarde door dubbele aanhalingstekens om een lege tekenreeks.
* Voorbeeld van uitvoer met **[!UICONTROL Empty string]** geselecteerd: `male,,TestLastName` . In dit geval vervangt Experience Platform de null-waarde door een lege tekenreeks (zonder dubbele aanhalingstekens).

### Compressie-indeling {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Compressie-indeling"
>abstract="Hiermee stelt u in welk compressietype u wilt gebruiken bij het opslaan van gegevens naar het bestand. Ondersteunde opties zijn GZIP en NONE. Raadpleeg de documentatie voor voorbeelden van elke selectie."

Hiermee stelt u in welk compressietype u wilt gebruiken bij het opslaan van gegevens naar het bestand. Ondersteunde opties zijn GZIP en NONE. Met deze optie bepaalt u of u gecomprimeerde bestanden wilt exporteren.

### Codering

*niet getoond in het het schermschot UI*. Hiermee wordt de codering (charset) van opgeslagen CSV-bestanden opgegeven. De opties zijn UTF-8 of UTF-16.

### Char om te ontsnappen aan aanhalingsteken

*niet getoond in het het schermschot UI*. Een markering die aangeeft of waarden die aanhalingstekens bevatten, altijd tussen aanhalingstekens moeten worden geplaatst.

Standaard worden alle waarden met een aanhalingsteken verwijderd.

### Lijnscheidingsteken

*niet getoond in het het schermschot UI*. Hiermee definieert u het lijnscheidingsteken dat moet worden gebruikt voor schrijven. De maximumlengte is 1 teken.

### Voorloopspatie negeren

*niet getoond in het het schermschot UI*. Een markering die aangeeft of witruimten die de regelafstand bepalen van waarden die worden geëxporteerd, moeten worden overgeslagen.

Voorbeeld van uitvoer met **[!UICONTROL True]** geselecteerd: `"male","John","TestLastName"`
Voorbeeld van uitvoer met **[!UICONTROL False]** geselecteerd: `" male","John","TestLastName"`

### Navolgende witruimte negeren

Niet weergegeven in de gebruikersinterfaceschermopname. Een vlag die aangeeft of overlopende witruimten van waarden die worden geëxporteerd, moeten worden overgeslagen.

Voorbeeld van uitvoer met **[!UICONTROL True]** geselecteerd: `"male","John","TestLastName"`
Voorbeeld van uitvoer met **[!UICONTROL False]** geselecteerd: `"male ","John","TestLastName"`

### Volgende stappen {#next-steps}

Na het lezen van dit document, weet u nu hoe te om dossieruitvoeropties voor uw Csv- gegevensdossiers te vormen om de dossierinhoud aan de vereisten van uw stroomafwaartse systeem van de dossierontvangst aan te passen. Daarna, kunt u het [ op dossier-gebaseerde zelfstudie van de bestemmingsactivering ](/help/destinations/ui/activate-batch-profile-destinations.md) lezen beginnen dossiers naar uw aangewezen plaats van de wolkenopslag uit te voeren.
