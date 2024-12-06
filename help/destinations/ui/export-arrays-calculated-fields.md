---
title: Berekende velden gebruiken om arrays als tekenreeksen te exporteren
type: Tutorial
description: Leer hoe u berekende velden kunt gebruiken om arrays van Real-Time CDP naar cloudopslagdoelen als tekenreeksen te exporteren.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 9b64e39d25ad94aa834c8e207396b37c2a121243
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 0%

---

# Berekende velden gebruiken om arrays als tekenreeksen te exporteren{#use-calculated-fields-to-export-arrays-as-strings}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Ondersteuning van exportarrays"
>abstract="<p>Gebruik **voegt berekende gebied** controle toe om series van int, koord, booleaanse, en objecten waarden van Experience Platform aan uw gewenste bestemming van de wolkenopslag uit te voeren.</p><p> Arrays moeten als tekenreeksen worden geëxporteerd met de functie `array_to_string` . Raadpleeg de documentatie voor uitgebreide voorbeelden en meer ondersteunde functies.</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Voorbeelden"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Bekende beperkingen"

>[!AVAILABILITY]
>
>De functionaliteit voor het exporteren van arrays via berekende velden is over het algemeen beschikbaar.

Leer hoe te om series door berekende gebieden van Real-Time CDP naar [ wolkenopslagbestemmingen ](/help/destinations/catalog/cloud-storage/overview.md) als koorden uit te voeren. Lees dit document om te begrijpen welke gebruiksgevallen door deze functie worden ingeschakeld.

Krijg uitgebreide informatie over berekende gebieden - wat deze zijn en waarom zij belangrijk zijn. Lees de pagina&#39;s die hieronder zijn gekoppeld voor een inleiding tot berekende velden in Data Prep en meer informatie over alle beschikbare functies:

* [UI-gids en -overzicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Functies Data Prep](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Arrays en andere objecttypen in Platform {#arrays-strings-other-objects}

In Experience Platform, kunt u [ schema&#39;s XDM ](/help/xdm/home.md) gebruiken om verschillende gebiedstypes te beheren. Voordat ondersteuning voor arrayexportbewerkingen werd toegevoegd, kon u eenvoudige sleutelwaardepaartypevelden, zoals tekenreeksen, uit Experience Platform exporteren naar de gewenste doelen. Een voorbeeld van zulk een gebied dat voor de uitvoer eerder werd gesteund is `personalEmail.address`:`johndoe@acme.org`.

Andere veldtypen in Experience Platform zijn arrayvelden. Lees meer over [ het beheren van seriegebieden in het Experience Platform UI ](/help/xdm/ui/fields/array.md). Naast de eerder ondersteunde veldtypen kunt u nu arrayobjecten zoals het onderstaande voorbeeld exporteren. Deze objecten worden samengevoegd tot een tekenreeks met de functie `array_to_string` .

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Zie verder onder [ uitgebreide voorbeelden ](#examples) van hoe u diverse functies kunt gebruiken om tot elementen van series, transformatie en filterseries toegang te hebben, arrayelementen in een koord, en meer aansluiten.

## Bekende beperkingen {#known-limitations}

Let op de volgende bekende beperkingen die momenteel van toepassing zijn op deze functionaliteit:

* De uitvoer naar JSON of de dossiers van het Pakket *met hiërarchische schema&#39;s* wordt niet gesteund op dit ogenblik. U kunt series naar CSV, JSON, en de dossiers van het Pakket *als koorden slechts* uitvoeren, door de `array_to_string` functie te gebruiken.

## Vereisten {#prerequisites}

[ verbindt ](/help/destinations/ui/connect-destination.md) met een gewenste bestemming van de wolkenopslag, vooruitgang door de [ activeringsstappen voor de bestemmingen van de wolkenopslag ](/help/destinations/ui/activate-batch-profile-destinations.md) en krijgt aan de [ in kaart brengende ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) stap.

## Berekende velden exporteren {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Hiërarchisch uitvoerschema inschakelen"
>abstract="Schakel in of u hiërarchische structuren zoals arrays wilt exporteren."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Berekende velden uitgeschakeld toevoegen"
>abstract="Dit besturingselement is uitgeschakeld omdat u hebt geselecteerd om platte structuren te exporteren wanneer u verbinding maakt met het doel."

Selecteer **[!UICONTROL Add calculated field]** in de toewijzingsstap van de activeringsworkflow voor bestemmingen voor cloudopslag.

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

## Voorbeeld van ondersteunde functies voor het exporteren van arrays {#supported-functions}

Alle gedocumenteerde [ functies van de Prep van Gegevens ](/help/data-prep/functions.md) worden gesteund wanneer het activeren van gegevens aan op dossier-gebaseerde bestemmingen.

De functies hieronder, specifiek voor het behandelen van de uitvoer van series, zijn gedocumenteerd samen met voorbeelden.

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

## Voorbeelden van functies die worden gebruikt om arrays te exporteren {#examples}

Zie voorbeelden en verdere informatie in de onderstaande secties voor enkele van de bovenstaande functies. Voor de rest van de vermelde functies, verwijs naar de [ algemene functiedocumentatie in de sectie van de Prep van Gegevens ](/help/data-prep/functions.md).

### `array_to_string` functie om arrays te exporteren {#array-to-string-function-export-arrays}

Gebruik de functie `array_to_string` om de elementen van een array te koppelen in een tekenreeks, met behulp van een gewenst scheidingsteken, zoals `_` of `|` .

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

### `filterArray` functie voor het exporteren van gefilterde arrays

Gebruik de functie `filterArray` om de elementen van een geëxporteerde array te filteren. U kunt deze functie combineren met de functie `array_to_string` die hierboven verder wordt beschreven.

Als u doorgaat met het array-object `organizations` van boven, kunt u een functie als `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))` schrijven, die de organisaties in 2021 of hoger met een waarde voor `founded` retourneert.

![ Voorbeeld van de filterArray functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De twee elementen van de array die aan het criterium voldoen, worden met het teken `_` samengevoegd tot één tekenreeks.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray` functie om getransformeerde arrays te exporteren

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

### `flattenArray` functie voor het exporteren van samengevoegde arrays

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

<!--

### Hashing functions {#hashing-functions}

In addition to the functions specific for exporting arrays or elements from an array, you can use hashing functions to hash attributes in the exported files. For example, if you have any personally identifiable information in attributes, you can hash those fields when exporting them. 

You can hash string values directly, for example `md5(personalEmail.address)`. If desired, you can also hash individual elements of array fields, assuming elements in the array are strings, like this: `md5(purchaseTime[0])`

The supported hashing functions are:

|Function | Sample expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` |  `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}

-->