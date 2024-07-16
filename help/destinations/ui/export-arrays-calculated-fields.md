---
title: (Beta) Berekende velden gebruiken om arrays te exporteren in platte schemabestanden
type: Tutorial
description: Leer hoe u berekende velden kunt gebruiken om arrays in platte schemabestanden van Real-Time CDP naar cloudopslagbestemmingen te exporteren.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# (Beta) Berekende velden gebruiken om arrays te exporteren in platte schemabestanden {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Ondersteuning voor exportarrays"
>abstract="Gebruik **voegt berekende gebied** controle toe om eenvoudige series van int, koord, of booleaanse waarden van Experience Platform naar uw gewenste bestemming van de wolkenopslag uit te voeren. Er gelden enkele beperkingen. Raadpleeg de documentatie voor uitgebreide voorbeelden en ondersteunde functies."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Voorbeelden"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Bekende beperkingen"

>[!AVAILABILITY]
>
>* De functionaliteit voor het exporteren van arrays via berekende velden is momenteel in Beta. De documentatie en de functionaliteit kunnen worden gewijzigd.

Leer hoe te om series door berekende gebieden van Real-Time CDP in vlakke schemadossiers naar [ de bestemmingen van de wolkenopslag ](/help/destinations/catalog/cloud-storage/overview.md) uit te voeren. Lees dit document om te begrijpen welke gebruiksgevallen door deze functie worden ingeschakeld.

Krijg uitgebreide informatie over berekende gebieden - wat deze zijn en waarom zij belangrijk zijn. Lees de pagina&#39;s die hieronder zijn gekoppeld voor een inleiding tot berekende velden in Data Prep en meer informatie over alle beschikbare functies:

* [UI-gids en -overzicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Functies Data Prep](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Arrays en andere objecttypen in Platform {#arrays-strings-other-objects}

In Experience Platform, kunt u [ schema&#39;s XDM ](/help/xdm/home.md) gebruiken om verschillende gebiedstypes te beheren. Eerder, kon u eenvoudige zeer belangrijk-waardepaar typegebieden zoals koorden uit Experience Platform naar uw gewenste bestemmingen uitvoeren. Een voorbeeld van zulk een gebied dat voor de uitvoer eerder werd gesteund is `personalEmail.address`:`johndoe@acme.org`.

Andere veldtypen in Experience Platform zijn arrayvelden. Lees meer over [ het beheren van seriegebieden in het Experience Platform UI ](/help/xdm/ui/fields/array.md). Naast de eerder ondersteunde veldtypen kunt u nu arrayobjecten exporteren, zoals: `organizations:[marketing, sales, engineering]` . Zie verder onder [ uitgebreide voorbeelden ](#examples) van hoe u diverse functies kunt gebruiken om tot elementen van series toegang te hebben, arrayelementen in een koord, en meer aansluiten.

## Bekende beperkingen {#known-limitations}

Let op de volgende bekende beperkingen voor de bètaversie van deze functionaliteit:

* Exporteren naar JSON- of Parquet-bestanden met hiërarchische schema&#39;s wordt momenteel niet ondersteund. U kunt arrays alleen exporteren naar CSV-, JSON- en Parquet-bestanden met één schema.
* Op dit ogenblik, *kunt u eenvoudige series (of series van primitieve waarden) aan de bestemmingen van de wolkenopslag slechts uitvoeren*. Dit betekent dat u arrayobjecten kunt exporteren die tekenreekswaarden, int- of booleaanse waarden bevatten. U kunt geen kaarten of arrays met kaarten of objecten exporteren. In het modale venster met berekende velden worden alleen de arrays weergegeven die u kunt exporteren.

## Vereisten {#prerequisites}

[ verbindt ](/help/destinations/ui/connect-destination.md) met een gewenste bestemming van de wolkenopslag, vooruitgang door de [ activeringsstappen voor de bestemmingen van de wolkenopslag ](/help/destinations/ui/activate-batch-profile-destinations.md) en krijgt aan de [ in kaart brengende ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) stap.

## Berekende velden exporteren {#how-to-export-calculated-fields}

Selecteer **[!UICONTROL (Beta) Add calculated field]** in de toewijzingsstap van de activeringsworkflow voor bestemmingen voor cloudopslag.

![ voeg berekend gebied toe dat in de afbeeldingsstap van het werkschema van de partijactivering wordt benadrukt.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Hierdoor wordt een modaal venster geopend waarin u kenmerken kunt selecteren die u kunt gebruiken om kenmerken uit Experience Platform te exporteren.

>[!IMPORTANT]
>
>Slechts enkele velden in uw XDM-schema zijn beschikbaar in de **[!UICONTROL Field]** -weergave. U kunt tekenreekswaarden en arrays met tekenreeks-, int- en booleaanse waarden zien. De array `segmentMembership` wordt bijvoorbeeld niet weergegeven, omdat deze andere arraywaarden bevat.

![ Modal venster van de berekende gebiedsfunctionaliteit zonder nog geselecteerde functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Gebruik bijvoorbeeld de functie `join` in het veld `loyaltyID` , zoals hieronder wordt weergegeven, om een array van loyale id&#39;s te exporteren als een tekenreeks die is samengevoegd met een onderstrepingsteken in een CSV-bestand. Bekijk [ meer informatie over dit en andere voorbeelden verder onder ](#join-function-export-arrays).

![ Modal venster van de berekende gebiedsfunctionaliteit met geselecteerde toetreedt functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selecteer **[!UICONTROL Save]** om het berekende veld te behouden en terug te keren naar de toewijzingsstap.

![ Modal venster van de berekende gebiedsfunctionaliteit met geselecteerde toetreedt functie en sparen benadrukte controle.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Vul de **[!UICONTROL Target field]** weer in de toewijzingsstap van de workflow met een waarde in de kolomkop die u voor dit veld wilt gebruiken in de geëxporteerde bestanden.

![ Afbeeldingsstap met het benadrukte doelgebied.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![ Uitgezochte doelgebied 2 ](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Als u klaar bent, selecteert u **[!UICONTROL Next]** om door te gaan naar de volgende stap van de activeringsworkflow.

![ de stap van de afbeelding met het benadrukte doelgebied en een doelwaarde die binnen wordt gevuld.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Ondersteunde functies {#supported-functions}

Alle gedocumenteerde [ functies van de Prep van Gegevens ](/help/data-prep/functions.md) worden gesteund wanneer het activeren van gegevens aan op dossier-gebaseerde bestemmingen.

Merk op, echter, dat de uitgebreide beschrijvingen van de gebruikscase en de informatie van de steekproefoutput momenteel voor de volgende functies slechts in de bètaversie van berekende gebieden en seriesteun voor bestemmingen worden verstrekt:

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## Voorbeelden van functies die worden gebruikt om arrays te exporteren {#examples}

Zie voorbeelden en verdere informatie in de onderstaande secties voor enkele van de bovenstaande functies. Voor de rest van de vermelde functies, verwijs naar de [ algemene functiedocumentatie in de sectie van de Prep van Gegevens ](/help/data-prep/functions.md).

### `join` functie om arrays te exporteren {#join-function-export-arrays}

Gebruik de functie `join` om de elementen van een array te koppelen in een tekenreeks, met behulp van een gewenst scheidingsteken, zoals `_` of `|` .

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals wordt weergegeven in de afbeelding met het toewijzingsraster, met behulp van een `join('_',loyalty.loyaltyID)` -syntaxis:

* `"organizations": ["Marketing","Sales,"Finance"]` array
* `person.name.firstName` tekenreeks
* `person.name.lastName` tekenreeks
* `personalEmail.address` tekenreeks

![ het Voorbeeld van de Toewijzing met inbegrip van toetreedt functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De drie elementen van de array worden samengevoegd tot één tekenreeks met het teken `_` .

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
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

Gebruik de functie `add_to_array` om elementen aan een geëxporteerde array toe te voegen. U kunt deze functie combineren met de functie `join` die hierboven verder wordt beschreven.

Als u doorgaat met het array-object `organizations` van bovenaf, kunt u een functie als `source: join('_', add_to_array(organizations,"2023"))` schrijven, die de organisaties retourneert waarvan een persoon lid is in 2023.

![ Voorbeeld van de Afbeelding met inbegrip van de add_to_array functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De drie elementen van de array worden samengevoegd tot één tekenreeks met het teken `_` en 2023 wordt ook toegevoegd aan het einde van de tekenreeks.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

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

### Hashingfuncties {#hashing-functions}

Naast de functies die specifiek zijn voor het exporteren van arrays of elementen uit een array, kunt u hash-functies gebruiken om kenmerken in de geëxporteerde bestanden te hashen. Als u bijvoorbeeld persoonlijke gegevens in kenmerken hebt, kunt u deze velden tijdens het exporteren hashen.

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