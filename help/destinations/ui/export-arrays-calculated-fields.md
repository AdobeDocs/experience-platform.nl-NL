---
title: (bèta) Gebruik berekende velden om arrays te exporteren in platte schemabestanden
type: Tutorial
description: Leer hoe u berekende velden kunt gebruiken om arrays in platte schemabestanden van Real-Time CDP naar cloudopslagbestemmingen te exporteren.
badge: "Bèta"
source-git-commit: b4a18cdf434055be81dacbf19de4dd3e3f229d19
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---


# (bèta) Gebruik berekende velden om arrays te exporteren in platte schemabestanden {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(bèta) Ondersteuning voor exportarrays"
>abstract="Exporteer eenvoudige arrays met int-, string- of booleaanse waarden van Experience Platform naar de gewenste bestemming voor cloudopslag. Er gelden enkele beperkingen. Raadpleeg de documentatie voor uitgebreide voorbeelden en ondersteunde functies."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Voorbeelden"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Bekende beperkingen"

>[!AVAILABILITY]
>
>* De functionaliteit om arrays via berekende velden te exporteren bevindt zich momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

Leer hoe u arrays via berekende velden van Real-Time CDP in platte schemabestanden exporteert naar cloudopslagbestemmingen. Lees dit document om te begrijpen welke gebruiksgevallen door deze functie worden ingeschakeld.

Krijg uitgebreide informatie over berekende gebieden - wat deze zijn en waarom zij belangrijk zijn. Lees de pagina&#39;s die hieronder zijn gekoppeld voor een inleiding tot berekende velden in Data Prep en meer informatie over alle beschikbare functies:

* [UI-gids en -overzicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Functies van voorvoegsel gegevens](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>Niet alle hierboven vermelde functies worden ondersteund *bij het exporteren van velden naar cloudopslagdoelen* de berekende veldfunctionaliteit gebruiken. Zie de [sectie voor ondersteunde functies](#supported-functions) zie hieronder voor meer informatie .

## Arrays en andere objecttypen in Platform {#arrays-strings-other-objects}

In Experience Platform kunt u [XDM-schema&#39;s](/help/xdm/home.md) om verschillende veldtypen te beheren. Eerder, kon u eenvoudige zeer belangrijk-waardepaar typegebieden zoals koorden uit Experience Platform naar uw gewenste bestemmingen uitvoeren. Een voorbeeld van een dergelijk veld dat eerder werd ondersteund voor exporteren is `personalEmail.address`:`johndoe@acme.org`.

Andere veldtypen in Experience Platform zijn arrayvelden. Meer informatie over [arrayvelden beheren in de gebruikersinterface van het Experience Platform](/help/xdm/ui/fields/array.md). Naast de eerder ondersteunde veldtypen kunt u nu arrayobjecten exporteren, zoals: `organizations:[marketing, sales, engineering]`. Zie verderop [uitgebreide voorbeelden](#examples) van hoe u verschillende functies kunt gebruiken om toegang te krijgen tot elementen van arrays, arrayelementen aan te sluiten bij een tekenreeks, enzovoort.

## Bekende beperkingen {#known-limitations}

Let op de volgende bekende beperkingen voor de bètaversie van deze functionaliteit:

* Exporteren naar JSON- of Parquet-bestanden met hiërarchische schema&#39;s wordt momenteel niet ondersteund. U kunt arrays alleen exporteren naar CSV-, JSON- en Parquet-bestanden met één schema.
* Op dit moment *u kunt eenvoudige arrays (of arrays met primitieve waarden) alleen exporteren naar cloudopslagdoelen*. Dit betekent dat u arrayobjecten kunt exporteren die tekenreekswaarden, int- of booleaanse waarden bevatten. U kunt geen kaarten of arrays met kaarten of objecten exporteren. In het modale venster met berekende velden worden alleen de arrays weergegeven die u kunt exporteren.

## Vereisten {#prerequisites}

Voortgang door de [activeringsstappen voor cloudopslagdoelen](/help/destinations/ui/activate-batch-profile-destinations.md) en ga naar [toewijzing](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) stap.

## Berekende velden exporteren {#how-to-export-calculated-fields}

Selecteer in de toewijzingsstap van de activeringsworkflow voor cloudopslagdoelen de optie **[!UICONTROL (Beta) Add calculated field]**.

![Berekend veld toevoegen om te exporteren](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Hierdoor wordt een modaal venster geopend waarin u kenmerken kunt selecteren die u kunt gebruiken om kenmerken uit Experience Platform te exporteren.

>[!IMPORTANT]
>
>Slechts enkele velden van uw XDM-schema zijn beschikbaar in het dialoogvenster **[!UICONTROL Field]** weergeven. U kunt tekenreekswaarden en arrays met tekenreeks-, int- en booleaanse waarden zien. Bijvoorbeeld de `segmentMembership` array wordt niet weergegeven, omdat deze andere arraywaarden bevat.

![Modal venster 1](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Gebruik bijvoorbeeld de opdracht `join` functie op de `loyaltyID` veld, zoals hieronder weergegeven, om een array van loyale id&#39;s te exporteren als een tekenreeks die is samengevoegd met een onderstrepingsteken in een CSV-bestand. Weergave [meer informatie hierover en andere onderstaande voorbeelden](#join-function-export-arrays).

![Modal venster 2](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selecteren **[!UICONTROL Save]** om het berekende veld te behouden en terug te keren naar de toewijzingsstap.

![Modal window 3](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Vul de stappen voor het toewijzen van de workflow in **[!UICONTROL Target field]** met een waarde van de kolomkop die u voor dit veld wilt gebruiken in de geëxporteerde bestanden.

![Doelveld 1 selecteren](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Doelveld 2 selecteren](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Indien klaar, selecteert u **[!UICONTROL Next]** om door te gaan naar de volgende stap van de activeringsworkflow.

![Selecteer Volgende om door te gaan](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Ondersteunde functies {#supported-functions}

Merk op dat slechts de volgende functies in de bètaversie van berekende gebieden en seriesteun voor bestemmingen worden gesteund:

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

![Screenshot toewijzen](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. Let op: de drie elementen van de array worden samengevoegd tot één tekenreeks met behulp van de `_` teken.

```
`First_Name,Last_Name,Organization
John,Doe,"Marketing_Sales_Finance"
```

### `iif` functie voor het exporteren van arrays {#iif-function-export-arrays}

Gebruik de `iif` functie om elementen van een array onder bepaalde omstandigheden te exporteren. Bijvoorbeeld, verdergaand met `organzations` arrayobject van bovenaf, u kunt een eenvoudige voorwaardelijke functie schrijven, zoals `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Screenshot toewijzen voor de eerste en laatste functies](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. In dit geval, is het eerste element van de serie Marketing, zodat is de persoon lid van de marketing afdeling.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `coalesce` functie voor het exporteren van arrays {#coalesce-function-export-arrays}

Gebruik de `coalesce` functie om het eerste element van een array met een andere waarde dan null te benaderen en te exporteren naar een tekenreeks.

U kunt bijvoorbeeld de volgende XDM-velden hieronder combineren, zoals wordt weergegeven in de afbeelding van het kaartscherm, met behulp van een `coalesce(subscriptions.hasPromotion)` syntaxis om de eerste waarde true van false in de array te retourneren:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Screenshot toewijzen voor functie colesce](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

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

![Screenshot voor size_of function toewijzen](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In dit geval ziet het uitvoerbestand er hieronder uit. De tweede kolom geeft het aantal elementen in de array aan, overeenkomend met het aantal afzonderlijke aankopen dat de klant heeft gedaan.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Arraytoegang op basis van index {#index-based-array-access}

U kunt toegang krijgen tot een index van een array om één item uit de array te exporteren. Bijvoorbeeld, gelijkend op het bovenstaande voorbeeld voor `size_of` als u slechts de eerste keer wilt openen en exporteren dat een klant een bepaald product heeft aangeschaft, kunt u `purchaseTime[0]` het eerste element van de tijdstempel exporteren; `purchaseTime[1]` het tweede element van de tijdstempel exporteren; `purchaseTime[2]` om het derde element van de tijdstempel te exporteren, enzovoort.

![Screenshot toewijzen voor toegang tot index](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In dit geval ziet het uitvoerbestand er als volgt uit:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` en `last` functies om arrays te exporteren {#first-and-last-functions-export-arrays}

Gebruik de `first` en `last` functies om het eerste of laatste element in een array te exporteren. Bijvoorbeeld, verdergaand met `purchaseTime` arrayobject met meerdere tijdstempels uit de vorige voorbeelden, kunt u deze gebruiken om de eerste of laatste aanschaftijd die door een persoon is gemaakt, te exporteren.

![Screenshot toewijzen voor de eerste en laatste functies](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In dit geval ziet het uitvoerbestand er als volgt uit:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### `md5` en `sha256` hashingfuncties {#hashing-functions}

Naast de functies die specifiek zijn voor het exporteren van arrays of elementen uit een array, kunt u hash-functies gebruiken voor hashingkenmerken. Als u bijvoorbeeld persoonlijke gegevens in kenmerken hebt, kunt u deze velden tijdens het exporteren hashen.

U kunt tekenreekswaarden bijvoorbeeld rechtstreeks hashen `md5(personalEmail.address)`. U kunt desgewenst ook afzonderlijke elementen van arrayvelden zoals: `md5(purchaseTime[0])`



