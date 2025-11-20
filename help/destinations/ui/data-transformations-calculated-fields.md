---
title: Transformaties uitvoeren op gegevens die naar cloudopslagbestemmingen worden geëxporteerd met berekende velden
type: Tutorial
description: Begrijp hoe te om de berekende gebiedsfunctionaliteit te gebruiken om transformaties op gegevens uit te voeren die naar de bestemmingen van de wolkenopslag worden uitgevoerd
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: bd9efc1bcf6058827cc5c603b9976c9e42c7ec9e
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 0%

---

# Transformaties uitvoeren op gegevens die naar cloudopslagbestemmingen worden geëxporteerd met berekende velden {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Berekende velden toevoegen"
>abstract="<p>Gebruik **voegt berekende gebied** controle toe om diverse gegevenstransformaties op gegevens uit te voeren die naar de bestemmingen van de wolkenopslag worden uitgevoerd. U kunt bijvoorbeeld hashing toepassen op gegevens, arrays samenvoegen tot tekenreeksen, enzovoort."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/data-transformations-calculated-fields.html#examples" text="Voorbeelden"

>[!AVAILABILITY]
>
>De functionaliteit om transformaties op gegevens uit te voeren die naar de bestemmingen van de wolkenopslag worden uitgevoerd is over het algemeen beschikbaar voor de volgende bestemmingen: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md), evenals om het even welke douane partner-authored wolkenopslag die bestemmingen door [ Destination SDK ](/help/destinations/destination-sdk/overview.md) worden authored.

Voor het uitvoeren van verschillende transformaties op gegevens die naar de bestemmingen van de wolkenopslag worden uitgevoerd, moet u de berekende gebiedsfunctionaliteit in de kaartstap van het de uitvoerwerkschema gebruiken. Ga voor meer informatie over berekende velden naar de onderstaande pagina&#39;s. Deze pagina&#39;s bevatten een inleiding op berekende velden in Data Prep en meer informatie over alle beschikbare functies:

* [UI-gids en -overzicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Functies Data Prep](/help/data-prep/functions.md)

## Vereisten {#prerequisites}

Berekende velden gebruiken voor gegevenstransformaties:

1. [ verbind ](/help/destinations/ui/connect-destination.md) met een gewenste bestemming van de wolkenopslag. Wanneer het verbinden met de gewenste wolkenbestemming, knevel de **[!UICONTROL Export arrays, maps, objects]** [ optie weg ](/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle).
2. Ga door de [ activeringsstappen voor de bestemmingen van de wolkenopslag ](/help/destinations/ui/activate-batch-profile-destinations.md) en krijg aan de [ kaartings ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) stap.

## Werken met berekende velden {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Hiërarchisch uitvoerschema inschakelen"
>abstract="Schakel deze instelling in om het exporteren van arrays, toewijzingen en objecten naar JSON- of Parquet-bestanden in te schakelen."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Berekende velden uitgeschakeld toevoegen"
>abstract="Deze controle wordt onbruikbaar gemaakt omdat u de **series van de Uitvoer, kaarten, voorwerpen** knevel ** wanneer vestiging deze bestemmingsverbinding selecteerde. Om berekende gebieden en de functies te gebruiken beschikbaar binnen, opstelling een nieuwe bestemmingsverbinding met de **series van de Uitvoer, kaarten, voorwerpen** knevel *weg*."

>[!IMPORTANT]
>
>Wanneer u met berekende velden werkt, moet u, naast de gegevenstransformatiefuncties die u toepast, ook de functie `array_to_string` gebruiken om velden samen te voegen tot een tekenreeks.

Selecteer **[!UICONTROL Add calculated field]** in de toewijzingsstap van de activeringsworkflow voor bestemmingen voor cloudopslag.

>[!TIP]
>
>Het besturingselement **[!UICONTROL Add calculated field]** is uitgeschakeld voor doelverbindingen waarvoor het besturingselement **[!UICONTROL Export arrays, maps, and objects]** is uitgeschakeld. [Meer informatie](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle).

![ voeg berekend gebied toe dat in de afbeeldingsstap van het werkschema van de partijactivering wordt benadrukt.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Dit opent een modaal venster waar u functies en gebieden kunt selecteren om attributen uit Experience Platform uit te voeren.

![ Modal venster van de berekende gebiedsfunctionaliteit zonder nog geselecteerde functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Gebruik bijvoorbeeld de functie `array_to_string` in het veld `organizations` , zoals hieronder wordt weergegeven, om de array met organisaties te exporteren als een tekenreeks in een CSV-bestand. Bekijk [ meer informatie over dit en andere voorbeelden verder onder ](#array-to-string-function-export-arrays).

![ Modal venster van de berekende gebiedsfunctionaliteit met de serie-aan-koord geselecteerde functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selecteer **[!UICONTROL Save]** om het berekende veld te behouden en terug te keren naar de toewijzingsstap.

![ Modal venster van de berekende gebiedsfunctionaliteit met de serie-aan-koord geselecteerde functie en sparen benadrukte controle.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Vul de **[!UICONTROL Target field]** weer in de toewijzingsstap van de workflow met een waarde in de kolomkop die u voor dit veld wilt gebruiken in de geëxporteerde bestanden.

![ Afbeeldingsstap met het benadrukte doelgebied.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![ Uitgezochte doelgebied 2 ](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Als u klaar bent, selecteert u **[!UICONTROL Next]** om door te gaan naar de volgende stap van de activeringsworkflow.

![ de stap van de afbeelding met het benadrukte doelgebied en een doelwaarde die binnen wordt gevuld.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Voorbeeld van ondersteunde functies voor het uitvoeren van gegevenstransformaties {#supported-functions}

Alle gedocumenteerde [ functies van de Prep van Gegevens ](/help/data-prep/functions.md) worden gesteund wanneer het activeren van gegevens aan op dossier-gebaseerde bestemmingen.

De functies hieronder, specifiek voor het behandelen van de uitvoer van series, of het toepassen van het hakken op gebieden, worden gedocumenteerd samen met voorbeelden.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## Voorbeelden van functies die worden gebruikt om gegevenstransformaties uit te voeren {#examples}

Zie voorbeelden en verdere informatie in de onderstaande secties voor enkele van de bovenstaande functies. Voor de rest van de vermelde functies, verwijs naar de [ algemene functiedocumentatie in de sectie van de Prep van Gegevens ](/help/data-prep/functions.md).

### `array_to_string` functie om arrays te exporteren {#array-to-string-function-export-arrays}

Gebruik de functie `array_to_string` om de elementen van een array te koppelen in een tekenreeks, met behulp van een gewenst scheidingsteken, zoals `_` of `|` . Deze functie is nuttig wanneer u de elementen van een array van Experience Platform naar een CSV-bestand wilt exporteren.

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals wordt weergegeven in het toewijzingsraster dat is opgenomen met een `array_to_string('_',organizations)` -syntaxis:

* `organizations` array
* `person.name.firstName` tekenreeks
* `person.name.lastName` tekenreeks
* `personalEmail.address` tekenreeks

![ het Voorbeeld van de Toewijzing met inbegrip van de serie_to_string functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. U ziet hoe de elementen van de array met het teken `_` worden samengevoegd tot één tekenreeks.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `filterArray` functie voor het exporteren van gefilterde arrays {#filter-array}

Gebruik de functie `filterArray` om de elementen van een geëxporteerde array te filteren. U kunt deze functie combineren met de functie `array_to_string` die hierboven verder wordt beschreven.

Als u het arrayobject `organizations` van boven doorloopt, kunt u een functie zoals `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))` schrijven die de organisaties met een waarde voor `founded` in het jaar 2021 of recenter retourneert.

![ Voorbeeld van de filterArray functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De twee elementen van de array die aan het criterium voldoen, worden met het teken `_` samengevoegd tot één tekenreeks.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray` functie om getransformeerde arrays te exporteren {#transform-array}

Gebruik de functie `transformArray` om de elementen van een geëxporteerde array te transformeren. U kunt deze functie combineren met de functie `array_to_string` die hierboven verder wordt beschreven.

Als u doorgaat met het array-object `organizations` van bovenaf, kunt u een functie als `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))` schrijven die de namen retourneert van de organisaties die in hoofdletters zijn omgezet.

![ Voorbeeld van de functie transformArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De drie elementen van de array worden getransformeerd en samengevoegd tot één tekenreeks met het teken `_` .

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif` functie om arrays te exporteren {#iif-function-export-arrays}

Gebruik de functie `iif` om elementen van een array onder bepaalde omstandigheden te exporteren. Als u bijvoorbeeld verdergaat met het array-object `organizations` van boven, kunt u een eenvoudige voorwaardelijke functie schrijven, zoals `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")` .

![ het Voorbeeld van de Toewijzing met inbegrip van de functie iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. In dit geval, is het eerste element van de serie Marketing, zodat is de persoon lid van de marketing afdeling.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` functie om arrays te exporteren {#add-to-array-function-export-arrays}

Gebruik de functie `add_to_array` om elementen aan een geëxporteerde array toe te voegen. U kunt deze functie combineren met de functie `array_to_string` die hierboven verder wordt beschreven.

Als u doorgaat met het array-object `organizations` van bovenaf, kunt u een functie als `source: array_to_string('_', add_to_array(organizations,"2023"))` schrijven, die de organisaties retourneert waarvan een persoon lid is in 2023.

![ Voorbeeld van de Afbeelding met inbegrip van de add_to_array functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De drie elementen van de array worden samengevoegd tot één tekenreeks met het teken `_` en 2023 wordt ook toegevoegd aan het einde van de tekenreeks.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `flattenArray` functie voor het exporteren van samengevoegde arrays {#flatten-array}

Gebruik de functie `flattenArray` om een geëxporteerde multidimensionale array samen te voegen. U kunt deze functie combineren met de functie `array_to_string` die hierboven verder wordt beschreven.

Als u doorgaat met het array-object `organizations` van bovenaf, kunt u een functie zoals `array_to_string('_', flattenArray(organizations))` schrijven. De functie `array_to_string` voegt de invoerarray standaard samen tot een tekenreeks.

De resulterende uitvoer is gelijk aan die voor de functie `array_to_string` die verderop wordt beschreven.

### `coalesce` functie om arrays te exporteren {#coalesce-function-export-arrays}

Gebruik de functie `coalesce` om het eerste element van een array met een andere waarde dan null te benaderen en te exporteren naar een tekenreeks.

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals wordt getoond in het toewijzingsraster, door een `coalesce(subscriptions.hasPromotion)` syntaxis te gebruiken om de eerste `true` of `false` -waarde in de array te retourneren:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` tekenreeks
* `person.name.lastName` tekenreeks
* `personalEmail.address` tekenreeks

![ het Voorbeeld van de afbeelding met inbegrip van de kaalkrachtfunctie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De eerste niet-null `true` waarde in de array wordt geëxporteerd naar het bestand.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` functie om arrays te exporteren {#sizeof-function-export-arrays}

Gebruik de functie `size_of` om aan te geven hoeveel elementen er in een array zijn. Als u bijvoorbeeld een array-object `purchaseTime` met meerdere tijdstempels hebt, kunt u met de functie `size_of` aangeven hoeveel afzonderlijke aankopen een persoon heeft gedaan.

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals in de schermafbeelding wordt getoond.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` array die vijf afzonderlijke aankooptijden door de klant aangeeft
* `personalEmail.address` tekenreeks

![ Voorbeeld van het Toewijzen met inbegrip van size_of functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De tweede kolom geeft het aantal elementen in de array aan, overeenkomend met het aantal afzonderlijke aankopen dat de klant heeft gedaan.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Arraytoegang op basis van index {#index-based-array-access}

>[!IMPORTANT]
>
>In tegenstelling tot de andere die functies op deze pagina worden beschreven, om individuele elementen van een serie uit te voeren, te hoeven u *niet* om de **[!UICONTROL Calculated fields]** controle in UI te gebruiken.

U kunt toegang krijgen tot een index van een array om één item uit de array te exporteren. Als u bijvoorbeeld, net als in het bovenstaande voorbeeld voor de functie `size_of` , alleen de eerste keer dat een klant een bepaald product heeft aangeschaft, toegang wilt tot dit bestand en het bestand wilt exporteren, kunt u `purchaseTime[0]` gebruiken om het eerste element van de tijdstempel te exporteren, `purchaseTime[1]` om het tweede element van de tijdstempel te exporteren, `purchaseTime[2]` om het derde element van de tijdstempel te exporteren, enzovoort.

![ het Voorbeeld dat van de afbeelding toont hoe een element van een serie kan worden betreden.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In dit geval ziet het uitvoerbestand er als volgt uit: de eerste keer dat de klant een aankoop heeft gedaan, wordt geëxporteerd:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` - en `last` -functies om arrays te exporteren {#first-and-last-functions-export-arrays}

Gebruik de functies `first` en `last` om het eerste of laatste element in een array te exporteren. Als u bijvoorbeeld doorgaat met het array-object `purchaseTime` met meerdere tijdstempels uit de vorige voorbeelden, kunt u deze gebruiken om de eerste of laatste aanschaftijd die door een persoon is gemaakt, te exporteren.

![ Voorbeeld van het Toewijzen met inbegrip van de eerste en laatste functies.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In dit geval ziet uw uitvoerbestand er als volgt uit: u exporteert de eerste en laatste keer dat de klant een aankoop heeft gedaan:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Hashingfuncties {#hashing-functions}

Andere beschikbare functies zijn specifiek voor het exporteren van arrays of elementen uit een array. U kunt hashingfuncties gebruiken om kenmerken in de geëxporteerde bestanden te hashen. Als u bijvoorbeeld persoonlijke gegevens in kenmerken hebt, kunt u deze velden tijdens het exporteren hashen.

U kunt tekenreekswaarden rechtstreeks hashen, bijvoorbeeld `md5(personalEmail.address)` . U kunt desgewenst ook afzonderlijke elementen van arrayvelden hashen, ervan uitgaande dat elementen in de array tekenreeksen zijn, zoals in het volgende voorbeeld: `md5(purchaseTime[0])`

De ondersteunde hashingfuncties zijn:

| Functie | Voorbeeldexpressie |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}
