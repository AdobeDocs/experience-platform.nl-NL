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
>abstract="Gebruik de **Berekend veld toevoegen** besturingselement voor het exporteren van eenvoudige arrays met int-, string- of Booleaanse waarden van Experience Platform naar de gewenste locatie voor cloudopslag. Er gelden enkele beperkingen. Raadpleeg de documentatie voor uitgebreide voorbeelden en ondersteunde functies."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Voorbeelden"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Bekende beperkingen"

>[!AVAILABILITY]
>
>* De functionaliteit voor het exporteren van arrays via berekende velden is momenteel in Beta. De documentatie en de functionaliteit kunnen worden gewijzigd.

Leer hoe u arrays via berekende velden van Real-Time CDP in platte schemabestanden exporteert naar [cloudopslagbestemmingen](/help/destinations/catalog/cloud-storage/overview.md). Lees dit document om te begrijpen welke gebruiksgevallen door deze functie worden ingeschakeld.

Krijg uitgebreide informatie over berekende gebieden - wat deze zijn en waarom zij belangrijk zijn. Lees de pagina&#39;s die hieronder zijn gekoppeld voor een inleiding tot berekende velden in Data Prep en meer informatie over alle beschikbare functies:

* [UI-gids en -overzicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Functies Data Prep](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Arrays en andere objecttypen in Platform {#arrays-strings-other-objects}

In Experience Platform kunt u [XDM-schema&#39;s](/help/xdm/home.md) om verschillende veldtypen te beheren. Eerder, kon u eenvoudige zeer belangrijk-waardepaar typegebieden zoals koorden uit Experience Platform naar uw gewenste bestemmingen uitvoeren. Een voorbeeld van een dergelijk veld dat eerder werd ondersteund voor exporteren is `personalEmail.address`:`johndoe@acme.org`.

Andere veldtypen in Experience Platform zijn arrayvelden. Meer informatie over [arrayvelden beheren in de gebruikersinterface van het Experience Platform](/help/xdm/ui/fields/array.md). Naast de eerder ondersteunde veldtypen kunt u nu arrayobjecten exporteren, zoals: `organizations:[marketing, sales, engineering]`. Zie verderop [uitgebreide voorbeelden](#examples) van hoe u verschillende functies kunt gebruiken om toegang te krijgen tot elementen van arrays, arrayelementen aan te sluiten bij een tekenreeks, enzovoort.

## Bekende beperkingen {#known-limitations}

Let op de volgende bekende beperkingen voor de bètaversie van deze functionaliteit:

* Exporteren naar JSON- of Parquet-bestanden met hiërarchische schema&#39;s wordt momenteel niet ondersteund. U kunt arrays alleen exporteren naar CSV-, JSON- en Parquet-bestanden met één schema.
* Op dit moment *u kunt eenvoudige arrays (of arrays met primitieve waarden) alleen exporteren naar cloudopslagdoelen*. Dit betekent dat u arrayobjecten kunt exporteren die tekenreekswaarden, int- of booleaanse waarden bevatten. U kunt geen kaarten of arrays met kaarten of objecten exporteren. In het modale venster met berekende velden worden alleen de arrays weergegeven die u kunt exporteren.

## Vereisten {#prerequisites}

[Verbinden](/help/destinations/ui/connect-destination.md) naar een gewenste locatie voor cloudopslag, doorloopt u de [activeringsstappen voor cloudopslagdoelen](/help/destinations/ui/activate-batch-profile-destinations.md) en ga naar [toewijzing](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) stap.

## Berekende velden exporteren {#how-to-export-calculated-fields}

Selecteer in de toewijzingsstap van de activeringsworkflow voor cloudopslagdoelen de optie **[!UICONTROL (Beta) Add calculated field]**.

![Voeg een berekend veld toe dat is gemarkeerd in de toewijzingsstap van de workflow voor batchactivering.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Hierdoor wordt een modaal venster geopend waarin u kenmerken kunt selecteren die u kunt gebruiken om kenmerken uit Experience Platform te exporteren.

>[!IMPORTANT]
>
>Slechts enkele velden van uw XDM-schema zijn beschikbaar in het dialoogvenster **[!UICONTROL Field]** weergeven. U kunt tekenreekswaarden en arrays met tekenreeks-, int- en booleaanse waarden zien. Bijvoorbeeld de `segmentMembership` array wordt niet weergegeven, omdat deze andere arraywaarden bevat.

![Het modulaire venster van de berekende gebiedsfunctionaliteit zonder nog geselecteerde functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Gebruik bijvoorbeeld de opdracht `join` functie op de `loyaltyID` veld, zoals hieronder weergegeven, om een array van loyale id&#39;s te exporteren als een tekenreeks die is samengevoegd met een onderstrepingsteken in een CSV-bestand. Weergave [meer informatie hierover en andere onderstaande voorbeelden](#join-function-export-arrays).

![Modal venster van de berekende gebiedsfunctionaliteit met de verbindingsfunctie geselecteerd.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selecteren **[!UICONTROL Save]** om het berekende veld te behouden en terug te keren naar de toewijzingsstap.

![Het modulaire venster van de berekende gebiedsfunctionaliteit met de verbindingsfunctie geselecteerd en sparen controle benadrukt.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Vul de stappen voor het toewijzen van de workflow in **[!UICONTROL Target field]** met een waarde van de kolomkop die u voor dit veld wilt gebruiken in de geëxporteerde bestanden.

![De stap van de toewijzing met het benadrukte doelgebied.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Doelveld 2 selecteren](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Indien klaar, selecteert u **[!UICONTROL Next]** om door te gaan naar de volgende stap van de activeringsworkflow.

![Toewijzingsstap met het doelveld gemarkeerd en een doelwaarde ingevuld.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Ondersteunde functies {#supported-functions}

Alle gedocumenteerde [Functies Data Prep](/help/data-prep/functions.md) worden ondersteund bij het activeren van gegevens naar bestandsbestemmingen.

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

Zie voorbeelden en verdere informatie in de onderstaande secties voor enkele van de bovenstaande functies. Voor de overige functies die in de lijst worden vermeld, raadpleegt u de [documentatie over algemene functies in de sectie Data Prep](/help/data-prep/functions.md).

### `join` functie voor het exporteren van arrays {#join-function-export-arrays}

Gebruik de `join` functie om de elementen van een array samen te voegen tot een tekenreeks, met behulp van een gewenst scheidingsteken, zoals `_` of `|`.

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals wordt weergegeven in de afbeelding van het kaartscherm, met behulp van een `join('_',loyalty.loyaltyID)` syntaxis:

* `"organizations": ["Marketing","Sales,"Finance"]` array
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Voorbeeld van toewijzing inclusief de functie join.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. Let op: de drie elementen van de array worden samengevoegd tot één tekenreeks met behulp van de `_` teken.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` functie voor het exporteren van arrays {#iif-function-export-arrays}

Gebruik de `iif` functie om elementen van een array onder bepaalde omstandigheden te exporteren. Bijvoorbeeld, verdergaand met `organizations` arrayobject van bovenaf, u kunt een eenvoudige voorwaardelijke functie schrijven, zoals `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Voorbeeld van toewijzing inclusief de IF-functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. In dit geval, is het eerste element van de serie Marketing, zodat is de persoon lid van de marketing afdeling.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` functie voor het exporteren van arrays {#add-to-array-function-export-arrays}

Gebruik de `add_to_array` functie om elementen toe te voegen aan een geëxporteerde array. U kunt deze functie combineren met de functie `join` hierboven beschreven functie.

Doorgaan met de `organizations` arrayobject van bovenaf, u kunt een functie schrijven zoals `source: join('_', add_to_array(organizations,"2023"))`, de organisaties waarvan een persoon lid is in het jaar 2023 terug te sturen.

![Voorbeeld van toewijzing, inclusief de functie add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. Let op: de drie elementen van de array worden samengevoegd tot één tekenreeks met behulp van de `_` en 2023 wordt ook toegevoegd aan het einde van de tekenreeks.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` functie voor het exporteren van arrays {#coalesce-function-export-arrays}

Gebruik de `coalesce` functie om het eerste element van een array met een andere waarde dan null te benaderen en te exporteren naar een tekenreeks.

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals wordt weergegeven in de afbeelding van het kaartscherm, met behulp van een `coalesce(subscriptions.hasPromotion)` syntaxis om de eerste te retourneren `true` van `false` waarde in de array:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Voorbeeld van toewijzing inclusief de functie voor afspelen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De eerste niet-null `true` De waarde in de array wordt geëxporteerd naar het bestand.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` functie voor het exporteren van arrays {#sizeof-function-export-arrays}

Gebruik de `size_of` functie om aan te geven hoeveel elementen er in een array bestaan. Als u bijvoorbeeld een `purchaseTime` arrayobject met meerdere tijdstempels, kunt u de `size_of` om aan te geven hoeveel afzonderlijke aankopen door een persoon zijn gedaan.

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals in de schermafbeelding wordt getoond.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` array met vijf afzonderlijke aankooptijden voor de klant
* `personalEmail.address` string

![Voorbeeld van toewijzing inclusief de size_of functie.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De tweede kolom geeft het aantal elementen in de array aan, overeenkomend met het aantal afzonderlijke aankopen dat de klant heeft gedaan.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Arraytoegang op basis van index {#index-based-array-access}

U kunt toegang krijgen tot een index van een array om één item uit de array te exporteren. Bijvoorbeeld, gelijkend op het bovenstaande voorbeeld voor `size_of` als u slechts de eerste keer wilt openen en exporteren dat een klant een bepaald product heeft aangeschaft, kunt u `purchaseTime[0]` het eerste element van de tijdstempel exporteren; `purchaseTime[1]` het tweede element van de tijdstempel exporteren; `purchaseTime[2]` om het derde element van de tijdstempel te exporteren, enzovoort.

![Voorbeeld van toewijzing dat aangeeft hoe een element van een array kan worden benaderd.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In dit geval ziet het uitvoerbestand er als volgt uit: de eerste keer dat de klant een aankoop heeft gedaan, wordt geëxporteerd:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` en `last` functies om arrays te exporteren {#first-and-last-functions-export-arrays}

Gebruik de `first` en `last` functies om het eerste of laatste element in een array te exporteren. Bijvoorbeeld, verdergaand met `purchaseTime` arrayobject met meerdere tijdstempels uit de vorige voorbeelden, kunt u deze gebruiken om de eerste of laatste aanschaftijd die door een persoon is gemaakt, te exporteren.

![Voorbeeld van toewijzing inclusief de eerste en laatste functies.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In dit geval ziet uw uitvoerbestand er als volgt uit: u exporteert de eerste en laatste keer dat de klant een aankoop heeft gedaan:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Hashingfuncties {#hashing-functions}

Naast de functies die specifiek zijn voor het exporteren van arrays of elementen uit een array, kunt u hash-functies gebruiken om kenmerken in de geëxporteerde bestanden te hashen. Als u bijvoorbeeld persoonlijke gegevens in kenmerken hebt, kunt u deze velden tijdens het exporteren hashen.

U kunt tekenreekswaarden bijvoorbeeld rechtstreeks hashen `md5(personalEmail.address)`. U kunt desgewenst ook afzonderlijke elementen van arrayvelden hashen, ervan uitgaande dat elementen in de array tekenreeksen zijn, zoals in het volgende voorbeeld: `md5(purchaseTime[0])`

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